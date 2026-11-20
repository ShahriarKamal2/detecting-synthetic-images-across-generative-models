# Datasets, reproducibility, and responsible publication

## Phase 01 — GenImage reference and local three-class subset

The project author identified **GenImage** as the Phase 01 source:

- GitHub: https://github.com/GenImage-Dataset/GenImage
- Official website and dataset-use terms: https://genimage-dataset.github.io/
- Paper: https://arxiv.org/abs/2306.08571

GenImage's upstream folder convention groups files by generator (`BigGAN`, `Stable Diffusion V1.4`, etc.), then `train` / `val`, then `ai` (generated) / `nature` (real). The Phase 01 notebook instead scans the parent of `C:\Dataset\hybrid_pid_full_data` and derives **Real / GAN / Diffusion** classes from keywords in file and folder paths. It is a custom three-class experiment, **not the official binary GenImage protocol**.

Its recorded local run found 17,500 real, 2,500 GAN, and 15,000 diffusion images, and balanced those to 2,500 per class. The uploaded notebook does not include the subset manifest, download commands, provenance of each local file, exact split membership, or dataset hashes. We therefore provide **GenImage as the author-provided source**, but cannot assert that particular GenImage generator subsets account for every recorded input image. Re-check label inference rules and upstream terms before claiming full reproducibility.

The GenImage project website states CC BY-NC-SA 4.0 with additional restrictions, including non-commercial use. No image files are bundled.

## Phase 02 — AIGIBench

The supplied code downloads dataset archives using the official AIGIBench [Hugging Face dataset](https://huggingface.co/datasets/HorizonTEL/AIGIBench) and evaluates 8 selected subsets. The dataset card states **CC BY-NC-SA 4.0**. Research/data reference: [HorizonTEL/AIGIBench](https://github.com/HorizonTEL/AIGIBench), *Is Artificial Intelligence Generated Image Detection a Solved Problem?* (Li et al., 2025).

Please follow the upstream dataset's license and usage terms. Do not commit downloaded archives or derived copies of third-party images without verifying redistribution rights.

## Notes on rerunning

- Phase 01 requires an edited local filesystem path and an appropriate three-class dataset. Check the `infer_three_class_label` heuristic before using external images; it defaults some generic `fake` labels to Diffusion.
- A saved Phase 01 checkpoint may cause the 10-epoch training loop to be skipped. The provided output was created in this resumed/completed state.
- Phase 02 was designed for Kaggle paths (`/kaggle/tmp`, `/kaggle/working`) and a CUDA GPU. Its use of `torch.cuda.amp` may need updates for future PyTorch releases. The original run's exact package versions and GPU type were not specified.
- The original Phase 02 notebook included a function that recursively deleted general `/tmp` and `/var/tmp` contents. The organized notebook replaces it with a limited project-cache cleanup to prevent unintended removal of unrelated runtime files. Dataset download/extraction and model/evaluation logic have otherwise been kept intact.
- The packaged notebooks have their large or misleading execution outputs cleared; original recorded results are preserved in `results/` files. No code was retrained as part of this reorganization.

## Interpretability and scope

Phase 01 is a three-class local validation experiment. Phase 02 is a binary real/fake study where training uses ProGAN images. The Phase 02 aggregate includes ProGAN itself and seven other test subsets. It reports 8 of the benchmark's 25 test subsets, so do not represent 53.7% as an official full AIGIBench score. In the JPEG experiment, fake recognition fell to zero across all evaluated subsets.

## Before making this repository public

1. Obtain permission from all relevant project contributors and confirm rights to publish research code and the model design.
2. Confirm the exact Phase 01 GenImage generator subsets and reconcile them with the three-class labels; verify dataset reuse and display rights.
3. Confirm output files contain no private credentials, API keys, or personal paths you do not wish to expose.
4. Add a software `LICENSE` only after deciding on the appropriate license with the rights holders.
5. If you re-run the experiment, record software versions, random seeds, hardware, the exact dataset version and any changes to code.
