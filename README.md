# ECCV2024: Adapting Fine-Grained Cross-View Localization to Areas without Fine Ground Truth
[[`Paper`](https://link.springer.com/chapter/10.1007/978-3-031-72751-1_23))] [[`Arxiv`](https://arxiv.org/abs/2406.00474))] [[`Presentation`](https://www.youtube.com/watch?v=U9njuEIdVL8)] [[`BibTeX`](#citation)]

![](figures/overview.png)


### Abstract
Given a ground-level query image and a geo-referenced aerial image that covers the query's local surroundings, fine-grained cross-view localization aims to estimate the location of the ground camera inside the aerial image. Recent works have focused on developing advanced networks trained with accurate ground truth (GT) locations of ground images. However, the trained models always suffer a performance drop when applied to images in a new target area that differs from training. In most deployment scenarios, acquiring fine GT, i.e. accurate GT locations, for target-area images to re-train the network can be expensive and sometimes infeasible. In contrast, collecting images with noisy GT with errors of tens of meters is often easy. Motivated by this, our paper focuses on improving the performance of a trained model in a new target area by leveraging only the target-area images without fine GT. We propose a weakly supervised learning approach based on knowledge self-distillation. This approach uses predictions from a pre-trained model as pseudo GT to supervise a copy of itself. Our approach includes a mode-based pseudo GT generation for reducing uncertainty in pseudo GT and an outlier filtering method to remove unreliable pseudo GT. Our approach is validated using two recent state-of-the-art models on two benchmarks. The results demonstrate that it consistently and considerably boosts the localization accuracy in the target area.

### Datasets
VIGOR dataset can be found at https://github.com/Jeff-Zilence/VIGOR.
We use the revised ground truth from https://github.com/tudelft-iv/SliceMatch <br />
KITTI dataset can be found at https://github.com/shiyujiao/HighlyAccurate <br />

### Models
Our trained models are available at: https://drive.google.com/drive/folders/1Uw1HukdXxuINDs65zi96oIDy2XNM2k2m?usp=sharing

### Training and Testing
Note: We modified the original [CCVPE](https://github.com/tudelft-iv/CCVPE) model slightly. It now also uses reflect padding in the aerial encoder, which is why our teacher model performs slightly better than the original CCVPE.

Training the final student model on VIGOR: `python train_CCVPE_on_VIGOR.py ` <br />

Testing the final student model: `python evaluate_CCVPE_on_VIGOR.py --inference_on=test --model=final_student --known_ori=True ` <br />
If you wish to test the teacher or the auxiliary student model, use `--model=teacher` or `--model=auxiliary_student`.
Testing with unknown orientation: `--known_ori=False`.

Generate Pseudo GT from the teacher or auxiliary student model: `python evaluate_CCVPE_on_VIGOR.py --inference_on=train --model=teacher --known_ori=True `


### Citation
```
@inproceedings{xia2024adapting,
  title={Adapting fine-grained cross-view localization to areas without fine ground truth},
  author={Xia, Zimin and Shi, Yujiao and Li, Hongdong and FP Kooij, Julian},
  booktitle={European Conference on Computer Vision},
  pages={397--415},
  year={2024},
  organization={Springer}
}
```
