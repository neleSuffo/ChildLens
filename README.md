# ChildLens: An Egocentric Video and Audio Dataset for Child Development Research

This is the official repository for the **ChildLens** dataset and our associated publication, which introduces a new resource for analyzing children's naturalistic everyday experiences.

<p align="center">
  <img src="docs/figures/childlens_concept.png" alt="An illustration of the ChildLens dataset and its components, including a child wearing the camera vest." style="width:75%;">
</p>

ChildLens is a unique egocentric video and audio dataset capturing 109 hours of experiences from 62 children aged three to five years. The recordings were made in children's home environments using a child-friendly vest equipped with a wide-lens camera and a microphone.

The dataset includes detailed annotations for:
- **Location classes** (5 categories)
- **Activity classes** (14 categories, including audio-only, video-only, and multimodal activities)
- **Voice types** in the audio stream

This repository provides all the code necessary to replicate the benchmark performance results presented in our paper. We demonstrate the application of two state-of-the-art models on the ChildLens dataset:

- **Temporal Activity Localization:** Using the Boundary-Matching Network (BMN).
- **Audio Voice Type Classification:** Using a Voice Type Classifier (VTC) to detect and classify speech into categories such as Key Child, Other Child, Male Adult, and Female Adult.

The ChildLens dataset is a powerful tool for advancing computer vision and audio analysis techniques and will be made freely available for research purposes.

### How to use this repository?

1.  **Installation:** Learn how to set up your environment and install the required dependencies.
2.  **Dataset Access:** Follow the instructions to access the ChildLens dataset via our institutional repository.
3.  **Applying the Models:** Replicate the benchmark results by running our provided scripts for:
    - [Temporal Activity Localization (BMN)](./docs/bmn_benchmark.md)
    - [Voice Type Classification (VTC)](./docs/vtc_benchmark.md)
4.  **Evaluation:** Use our evaluation scripts to compute the performance metrics for your own models on the ChildLens dataset.
5.  **Going further:** Explore our documentation for tips on using the dataset and code for new research applications.

### References

The ChildLens paper:

[1] ChildLens: An Egocentric Video and Audio Dataset for Child Development Research

```text
@article{your_paper_citation,
  title={ChildLens: An Egocentric Video and Audio Dataset for Child Development Research},
  author={[Your Authors]},
  journal={arXiv preprint},
  year={2025},
  volume={},
  pages={},
  eprint={...},
  eprinttype={arxiv}
}
