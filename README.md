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

`submission/bow-global-2023-12-14-20-32-38-with-other.ipynb` is the **exact Kaggle kernel version that was selected**, not the later kernel revision.

- Kernel: https://www.kaggle.com/code/reasat/bow-global-2023-12-14-20-32-38-with-other?scriptVersionId=157255213
- `scriptVersionId`: `157255213`
- Distinctive setting in this version: `MAX_SAMPLE_PER_IMAGE = 50` (a later version used 75 and timed out on rescoring)

The notebook is a bag-of-windows MaxViT (`maxvit_tiny_tf_512`) plus a TinyViT patch classifier, with a global thumbnail branch. It started from [Jirka Borovec's public tile-training notebook](https://www.kaggle.com/code/jirkaborovec/cancer-subtype-tiles-w-lightning-timm-models).

## Weights (not in git)

Checkpoints stay on Kaggle. Do not commit `.ckpt` files.

| Role | Kaggle dataset | Path used in the notebook |
| --- | --- | --- |
| Patch classifier | [reasat/2023-12-09-17-07-51](https://www.kaggle.com/datasets/reasat/2023-12-09-17-07-51) | `tiny_vit_21m_512.dist_in22k_ft_in1k/version_0/checkpoints/epoch=4-step=9925.ckpt` |
| Bag-of-windows model | [reasat/2023-12-14-20-32-38](https://www.kaggle.com/datasets/reasat/2023-12-14-20-32-38) | `fold_0/maxvit_tiny_tf_512/version_0/checkpoints/epoch=99-step=3400.ckpt` |

Competition WSI images are the official `UBC-OCEAN` input; they are not copied here.

See `provenance.json` for the machine-readable pin.
