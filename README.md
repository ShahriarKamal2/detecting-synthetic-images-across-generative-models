# Detecting Synthetic Images Across Generative Models

An undergraduate research project examining synthetic-image classification and the generalization of image-forensics features across generative models.

The project explores **pixel-inconsistency detection (PiD)** and **signal-domain features** (high-pass noise residuals, frequency-spectrum information, and image statistics) with a custom **attention-enhanced convolutional neural network (CNN)**. Experiments were conducted in two phases: three-class classification and binary real-vs-fake detection with cross-generator robustness testing.

> **Research takeaway:** High validation accuracy on a familiar dataset does not necessarily translate into reliable detection of images from different generators or after common image transformations.

## Research phases

| Phase | Question | Task | Notebook | Documentation |
| --- | --- | --- | --- | --- |
| **01** | Can the model distinguish real, GAN-generated, and diffusion-generated images? | Three-class classification | [Phase 01 notebook](phase-01/01_three_class_classification.ipynb) | [Phase 01 details](phase-01/README.md) |
| **02** | Does a detector trained on ProGAN generalize to other synthetic-image sources and image degradations? | Binary classification and robustness evaluation | [Phase 02 notebook](phase-02/02_cross_generator_robustness.ipynb) | [Phase 02 details](phase-02/README.md) |

## Approach

Both phases share a feature-extraction strategy:

1. Resize RGB images to 224 × 224.
2. Extract a **3-channel PiD reconstruction residual** using RGB/YUV transforms.
3. Extract **12 signal channels** from high-pass residuals, Fourier-spectrum magnitudes, and per-image means and standard deviations.
4. Concatenate the **15 feature channels** and pass them through a custom CNN with squeeze-and-excitation (SE) attention blocks.
5. Predict one of three classes in Phase 01 or one of two classes in Phase 02.

The Phase 01 model has **1,636,099 trainable parameters**; the Phase 02 binary model has **1,635,970**. The classifier head changes to fit each task.

## Recorded results

These figures come from the uploaded notebook outputs and Phase 02 training log; they are **not independently reproduced** by this repository packaging step.

| Metric | Phase 01 | Phase 02 |
| --- | --- | --- |
| Classes | Real / GAN / Diffusion | Real / Fake |
| Training data | 6,000 balanced images | 115,218 ProGAN images |
| Validation data | 1,500 images | 28,806 images |
| Best recorded validation accuracy | **95.73%** | **99.93%** |
| Additional tests | Classification report and confusion matrix | Eight AIGIBench subsets under four image conditions |

**Do not compare the two validation accuracy figures as if they were the same task or benchmark.** Phase 01 uses three classes and a local dataset. Phase 02 uses binary labels on ProGAN data and separately reports test-set performance across other generators.

### Phase 02 — Generalization and robustness

Average accuracy across the **eight evaluated AIGIBench subsets**, with 500 real + 500 fake images per subset:

| Evaluation condition | Mean accuracy |
| --- | ---: |
| Original images | **60.3%** |
| JPEG compression (quality 50) | 50.0% |
| Gaussian noise (σ = 4/255) | 44.7% |
| 2× nearest-neighbor downsample / upsample | 59.8% |
| **Average across all four conditions** | **53.7%** |

Some subsets were substantially more difficult than others (e.g., BlendFace and FaceSwap). Under JPEG compression, the model classified all evaluated images as real (100% real accuracy, 0% fake accuracy), a notable robustness failure.

For per-subset figures see [Phase 02 results](results/phase-02/subset_accuracy.csv).

## Repository structure

```text
detecting-synthetic-images-across-generative-models/
├── README.md
├── phase-01/
│   ├── README.md
│   └── 01_three_class_classification.ipynb
├── phase-02/
│   ├── README.md
│   └── 02_cross_generator_robustness.ipynb
├── results/
│   ├── phase-01/                    # Validation report, log, and visualization
│   └── phase-02/                    # Per-subset results and experiment log
├── docs/
│   ├── DATASETS_AND_REPRODUCIBILITY.md
│   ├── REFERENCES.md
│   └── UPLOAD_TO_GITHUB.md
├── requirements.txt
└── .gitignore
```

## Getting started

```bash
git clone https://github.com/<your-username>/detecting-synthetic-images-across-generative-models.git
cd detecting-synthetic-images-across-generative-models
python -m venv .venv
# Activate .venv in your shell, then:
pip install -r requirements.txt
jupyter notebook
```

**Before running:** Follow each phase's README to prepare its dataset and adapt its environment-specific paths. Phase 01 expects a **local Windows directory** and a compatible, manually arranged GenImage-derived image folder layout; Phase 02 was written for **Kaggle** and downloads substantial amounts of data. The notebooks are organized research code, not a tested one-command pipeline.

## Datasets, attribution, and limitations

- **Phase 01 dataset reference — GenImage:** [official dataset GitHub](https://github.com/GenImage-Dataset/GenImage) · [project website](https://genimage-dataset.github.io/) · [paper](https://arxiv.org/abs/2306.08571). This reference was supplied by the project author. The local three-class subset used in the recorded experiment was manually prepared; the notebook does not contain a file manifest, so the exact upstream generator mix and images **cannot be independently established from the notebook alone**. See the [Phase 01 dataset instructions](phase-01/README.md#dataset-source-and-preparation).
- **Phase 02 benchmark — AIGIBench:** uses the [AIGIBench dataset](https://huggingface.co/datasets/HorizonTEL/AIGIBench) and its [official research repository](https://github.com/HorizonTEL/AIGIBench), from the study *Is Artificial Intelligence Generated Image Detection a Solved Problem?* by Li et al. (NeurIPS 2025 Datasets and Benchmarks). Respect the dataset's stated **CC BY-NC-SA 4.0** license.
- Phase 02 evaluates **eight selected subsets**, not the benchmark's full 25-subset suite. Reported averages must not be presented as an official full-benchmark result.
- The **GenImage website** specifies CC BY-NC-SA 4.0 plus additional terms. Do not redistribute its image data without checking the terms; this repository contains **no downloaded images**.
- Phase 01's captured execution **resumed from a completed checkpoint** (epoch 10/10); its result reflects a saved model, not training performed during that captured run.
- Both phases should be considered exploratory research, not production-ready image authenticity classifiers.

See [Datasets and reproducibility](docs/DATASETS_AND_REPRODUCIBILITY.md) and [Dataset/research references](docs/REFERENCES.md) for additional detail.

## Publishing to GitHub

The image datasets and trained model weights are **not included**. The repository includes clean notebooks, source-linked dataset guidance, recorded experimental metrics, dependencies, and a `.gitignore` that excludes downloaded archives and weights. Follow the [GitHub upload guide](docs/UPLOAD_TO_GITHUB.md) to publish the project.


## Project information

**Project:** Detecting Synthetic Images Across Generative Models  
**Type:** Undergraduate directed research / capstone  
**Course:** CSE498R — Directed Research  
**Institution:** North South University, Bangladesh  
**Contributors:** Add the names and roles of the actual project team before publishing.

## License

**Not yet selected.** Confirm ownership and obtain agreement from your project contributors before adding an open-source code license. The third-party dataset's CC BY-NC-SA 4.0 license is separate from any license you may later choose for your code.
