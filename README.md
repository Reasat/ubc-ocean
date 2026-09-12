# UBC-OCEAN silver medal

Silver medal (26th of 1326) on [UBC Ovarian Cancer Subtype Classification and Outlier Detection](https://www.kaggle.com/competitions/UBC-OCEAN). Solo, January 2024.

[Certificate](https://www.kaggle.com/certification/competitions/reasat/UBC-OCEAN)

The task is five ovarian-cancer subtypes (CC, EC, HGSC, LGSC, MC) on whole-slide images and TMAs, plus an `Other` class for outliers.

## Method

Two models, trained separately, composed only at inference. Not end-to-end.

**Patch classifier (TinyViT).** 7-way tile classifier: the five tumor types plus Stroma and Necrosis. Used as a gate: keep tumor tiles, drop the rest.

**Bag-of-windows subtype model (MaxViT).** Shared `maxvit_tiny_tf_512` encoder over a bag of six 512px tiles plus the slide thumbnail. Concatenate features, adaptive avg+max pool, MLP → five subtype logits.

### Inference

1. Load the slide (pyvips). Grid into tiles. Drop empty / mostly-white background.
2. TinyViT scores each remaining tile. Keep only tumor classes.
3. Pack kept tiles into bags of six. Encode bags with the thumbnail. Average bag logits → softmax → subtype. If no tiles survive, predict `Other`.
4. TMAs: same bag path, then overwrite with TinyViT on the whole TMA (90/180/270° TTA). Stroma or Necrosis becomes `Other`.

### Training

The two networks were trained independently (not a two-stage train loop, not joint backprop).

- Patch classifier: tile-level 7-class training. Slide labels as weak tumor labels; Stroma/Necrosis for non-tumor tiles.
- Subtype model: slide-level bags of six tiles (later run also used the thumbnail). Five-class labels from `train.csv`.

Weights stay on Kaggle:

- Patch classifier: [reasat/2023-12-09-17-07-51](https://www.kaggle.com/datasets/reasat/2023-12-09-17-07-51)
- Bag-of-windows model: [reasat/2023-12-14-20-32-38](https://www.kaggle.com/datasets/reasat/2023-12-14-20-32-38) (fold 0)

Tiles for training came from [jirkaborovec/tiles-of-cancer-2048px-scale-0-25](https://www.kaggle.com/datasets/jirkaborovec/tiles-of-cancer-2048px-scale-0-25).

## Code in this repo

- `submission/` — selected inference notebook (the medal run).
- `train/` — Lightning notebooks that the medal training code was based on.

`train/maxvit-all-wsi-in-train/` is a single-tile baseline: one random tile per slide through a full MaxViT classifier.

`train/maxvit-bow-train/` is a bag-of-windows trainer: six tiles per slide, shared MaxViT encoder, concat avg+max pool, 5-class head. The medal subtype run followed this setup (later adding a thumbnail branch and 3-fold training).
