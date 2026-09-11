# UBC-OCEAN silver medal submission

Inference notebook that scored **26th of 1326** (silver) in
[UBC Ovarian Cancer Subtype Classification and Outlier Detection (UBC-OCEAN)](https://www.kaggle.com/competitions/UBC-OCEAN).

| | |
| --- | --- |
| Medal | Silver |
| Private rank | 26 / 1326 |
| Selected run | public 0.56, private 0.53 |
| Awarded | 2024-01-03 |
| Team | Tahsin (solo, `reasat`) |
| Certificate | https://www.kaggle.com/certification/competitions/reasat/UBC-OCEAN |

## What is in this repo

### Submission (pinned medal version)

`submission/bow-global-2023-12-14-20-32-38-with-other.ipynb` is the **exact Kaggle kernel version that was selected**, not the later kernel revision.

- Kernel: https://www.kaggle.com/code/reasat/bow-global-2023-12-14-20-32-38-with-other?scriptVersionId=157255213
- `scriptVersionId`: `157255213`
- Distinctive setting in this version: `MAX_SAMPLE_PER_IMAGE = 50` (a later version used 75 and timed out on rescoring)

### Training notebooks

These are the Lightning `trainer.fit` kernels on this account for UBC-OCEAN (both were private on Kaggle).

| Path | Kaggle kernel | Role |
| --- | --- | --- |
| `train/maxvit-bow-train/` | [reasat/maxvit-bow-train](https://www.kaggle.com/code/reasat/maxvit-bow-train) | Bag-of-windows MaxViT on pre-extracted tiles |
| `train/maxvit-all-wsi-in-train/` | [reasat/maxvit-all-wsi-in-train](https://www.kaggle.com/code/reasat/maxvit-all-wsi-in-train) | Earlier single-tile MaxViT baseline on the same tile dump |

No named kernel was found for the TinyViT 7-class patch classifier. Its Lightning logs/checkpoint exist only as dataset [reasat/2023-12-09-17-07-51](https://www.kaggle.com/datasets/reasat/2023-12-09-17-07-51). The medal BOW checkpoint is a later 3-fold run stored as [reasat/2023-12-14-20-32-38](https://www.kaggle.com/datasets/reasat/2023-12-14-20-32-38); the closest matching train *code* is `maxvit-bow-train` (the inference graph later added a global-thumbnail branch).

Tile dump used in training: [jirkaborovec/tiles-of-cancer-2048px-scale-0-25](https://www.kaggle.com/datasets/jirkaborovec/tiles-of-cancer-2048px-scale-0-25). Starting point: [Jirka Borovec's Lightning+timm notebooks](https://www.kaggle.com/code/jirkaborovec/cancer-subtype-tiles-w-lightning-timm-models).

## Weights (not in git)

Checkpoints stay on Kaggle. Do not commit `.ckpt` files.

| Role | Kaggle dataset | Path used in the medal notebook |
| --- | --- | --- |
| Patch classifier | [reasat/2023-12-09-17-07-51](https://www.kaggle.com/datasets/reasat/2023-12-09-17-07-51) | `tiny_vit_21m_512.dist_in22k_ft_in1k/version_0/checkpoints/epoch=4-step=9925.ckpt` |
| Bag-of-windows model | [reasat/2023-12-14-20-32-38](https://www.kaggle.com/datasets/reasat/2023-12-14-20-32-38) | `fold_0/maxvit_tiny_tf_512/version_0/checkpoints/epoch=99-step=3400.ckpt` |

Competition WSI images are the official `UBC-OCEAN` input; they are not copied here.

See `provenance.json` for the machine-readable pin.
