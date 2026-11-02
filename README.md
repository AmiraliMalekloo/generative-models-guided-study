# Generative Models and Robust Classifiers on CIFAR-10

This repository contains notebooks from a short guided study. I explored generative modeling on CIFAR-10 cats and targeted attacks on standard and adversarially trained classifiers. My aim was to understand their behavior through experiments, rather than to propose a new method.

## Notebooks

| Notebook | Experiment |
|---|---|
| `BigGan.ipynb` | Reduced BigGAN-style model; saved outputs correspond to cat-only training |
| `StyleGan1.ipynb` | Unconditional, reduced StyleGAN1-style model on cats. currently I provide it's drive link because it is large. I will provide the code itself in this repository later : https://drive.google.com/file/d/1cThoQ7eXEgTUCLXBmyIN3eQZq8jAqip8/view?usp=drive_link |
| `StyleGan2.ipynb` | Unconditional, reduced StyleGAN2-style model on cats. currently I provide it's drive link because it is large. I will provide the code itself in this repository later :  https://drive.google.com/file/d/1LH4ewNxc5yhqhtWUQ9GOdM4HWRcw3HM9/view?usp=drive_link |
| `SDE-based(1).ipynb` | Budget-adapted continuous VP/DDPM++ score model on cats. currently I provide it's drive link because it is large. I will provide the code itself in this repository later :   https://drive.google.com/file/d/1o1-CPL8HsHkUX2mvVQN642AiPSTutiOL/view?usp=drive_link |
| `ResNet(1).ipynb` | Targeted attacks on ResNet20 checkpoints |
| `PreAct(1).ipynb` | Targeted attacks on PreActResNet18 checkpoints |

## Main observations

Some GAN outputs appeared repetitive or blurred. The SDE run appeared more varied, but it used a different architecture and a longer budget. I do not treat this as a controlled ranking of GANs and SDE models.

The SDE output records 94,608 completed updates, 30 skipped updates and 7.95 hours including setup. BigGAN-style training records 66,913 generator steps, while StyleGAN2 records 53,501 steps. These step counts do not represent equal computational work.

The classifier experiments examine target confidence as the perturbation budget increases. For example, the ResNet20 Linf-trained model reaches mean target confidence of 2.0% at 5/255 and 56.3% at 25/255 under targeted PGD-100. These values describe selected sample-target pairs, not full-test robust accuracy or image realism.

## Report

See [the experiment report](experiments_report.pdf) for methods, saved results, figures, interpretation and limitations. Place the supplied PDF beside this README. Figures in the report are extracted from saved notebook outputs. Training was not rerun for the report.

## Running the notebooks

Import a notebook into Kaggle and enable a GPU. Review its settings and setup cells before running. The generative notebooks download CIFAR-10; internet access and sufficient session quota are needed. Most saved generative runs use one Tesla T4 even when two GPUs are visible. The SDE notebook selects the eight-hour `high` preset; the GAN notebooks use approximately four-hour budgets, including setup. Download time can substantially reduce training time.

Classifier evaluation requires the saved checkpoints expected by each notebook. Paths printed under `/kaggle/working` describe historical runtime files; the notebooks do not automatically include those checkpoints or exported CSV files. Review checkpoint and data paths before evaluation. Use compatible, trusted checkpoints.

## Important limitations

- BigGAN and StyleGAN notebooks describe reduced independent implementations inspired by the papers, not official benchmark reproductions.
- BigGAN headings and visible defaults mention ten classes, whereas saved outputs show cat-only training. Re-running visible defaults may not reproduce the saved run.
- The classifier selection code chooses random wrong targets, while some text and plot labels still say easiest/hardest. Do not interpret those labels as a verified target-difficulty comparison.
- GAN losses, denoising MSE, target confidence and image quality are different quantities. No unmeasured FID or statistical significance is claimed.
- The notebooks are preserved unchanged. Saved outputs may reflect an earlier execution state.
- Noise-only variation with a fixed StyleGAN latent is not a test of diversity across independently sampled latents.

## Contribution and code provenance

This was a guided study involving reading, running and adapting experimental pipelines, and interpreting model behavior. The SDE notebook embeds pinned upstream source from [score_sde_pytorch](https://github.com/yang-song/score_sde_pytorch), commit `cb1f359f4aadf0ff9a5e122fe8fffc9451fd6e44`. Preserve its Apache 2.0 license and notices. Credit for the model families belongs to the papers below. AI assistance was used in preparing this report and README. This statement does not specify or certify the authorship history of individual notebook cells.

## Related papers

- [BigGAN: Large Scale GAN Training for High Fidelity Natural Image Synthesis](https://arxiv.org/abs/1809.11096)
- [StyleGAN: A Style-Based Generator Architecture for Generative Adversarial Networks](https://arxiv.org/abs/1812.04948)
- [StyleGAN2: Analyzing and Improving the Image Quality of StyleGAN](https://arxiv.org/abs/1912.04958)
- [Score-Based Generative Modeling through Stochastic Differential Equations](https://arxiv.org/abs/2011.13456)
- [Image Synthesis with a Single (Robust) Classifier](https://papers.neurips.cc/paper_files/paper/2019/hash/6f2268bd1d3d3ebaabb04d6b5d099425-Abstract.html)
- [Adversarial Examples Are Not Bugs, They Are Features](https://arxiv.org/abs/1905.02175)
