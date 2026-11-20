# Dataset and paper references

These are the upstream **sources** cited by the experiments. They are not repositories containing this project's trained model weights or image datasets.

## Phase 01 — GenImage

- **Project GitHub:** https://github.com/GenImage-Dataset/GenImage
- **Project website:** https://genimage-dataset.github.io/
- **Original paper:** Zhu, M., Chen, H., Yan, Q., Huang, X., Lin, G., Li, W., Tu, Z., Hu, H., Hu, J., & Wang, Y. (2023). *GenImage: A Million-Scale Benchmark for Detecting AI-Generated Image*. arXiv:2306.08571. https://arxiv.org/abs/2306.08571
- **Use and licensing:** The GenImage website provides terms including CC BY-NC-SA 4.0 and an explicit restriction on commercial use.

Official project BibTeX:

```bibtex
@misc{zhu2023genimage,
  title={GenImage: A Million-Scale Benchmark for Detecting AI-Generated Image},
  author={Mingjian Zhu and Hanting Chen and Qiangyu Yan and Xudong Huang and Guanyu Lin and Wei Li and Zhijun Tu and Hailin Hu and Jie Hu and Yunhe Wang},
  year={2023},
  eprint={2306.08571},
  archivePrefix={arXiv},
  primaryClass={cs.CV}
}
```

**Scope note:** The exact files selected for the Phase 01 local three-class experiment are not individually identified in the supplied notebook. The source links above were supplied by the project author.

## Phase 02 — AIGIBench

- **Official benchmark GitHub:** https://github.com/HorizonTEL/AIGIBench
- **Dataset hosted on Hugging Face:** https://huggingface.co/datasets/HorizonTEL/AIGIBench
- **Paper:** Li, Z., et al. (2025). *Is Artificial Intelligence Generated Image Detection a Solved Problem?* arXiv:2505.12335. https://arxiv.org/abs/2505.12335
- **Dataset license:** CC BY-NC-SA 4.0, as listed by the Hugging Face dataset card.

Phase 02 downloads the ProGAN training categories and selected test ZIP archives from AIGIBench. Its eight evaluated test subsets are **not the full 25-subset AIGIBench benchmark**. The AIGIBench authors note that their Setting-I ProGAN training data comes from ForenSynths, while GenImage Stable Diffusion V1.4 data enters their separate Setting-II configuration.

## This project's code and documentation

A separate code license is **not yet assigned**. Choose a license only after confirming permissions from the project's authors and contributors; dataset permissions are independent of code licensing.
