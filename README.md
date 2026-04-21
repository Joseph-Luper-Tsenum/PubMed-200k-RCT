# PubMed RCT 20k: Sentence Role Classification for Clinical Trial Abstracts

A deep learning NLP pipeline for sentence-level rhetorical role classification in biomedical abstracts using:

1. A BiLSTM baseline.
2. A transformer fine-tune model (PubMedBERT).

This project is part of BME6938 Medical AI coursework (University of Florida, Spring 2026).

## Clinical Context

Clinical trial abstracts are structured around rhetorical components such as background, objective, methods, results, and conclusions. Automatically classifying sentences into these categories supports:

- Biomedical literature mining.
- Evidence synthesis workflows.
- Downstream information extraction in clinical NLP pipelines.

## Task Definition

Dataset: armanc/pubmed-rct20k (Hugging Face)

Sentence-level 5-class classification:

- BACKGROUND
- OBJECTIVE
- METHODS
- RESULTS
- CONCLUSIONS

## Key Results (Test Set)

| Model | Accuracy | Macro F1 | Weighted F1 | Perplexity |
|---|---:|---:|---:|---:|
| BiLSTM baseline | 0.8395 | 0.7758 | 0.8397 | 1.7614 |
| BiomedNLP-PubMedBERT-base-uncased-abstract | 0.8664 | 0.8085 | 0.8677 | 1.5653 |

### Interpretation

- The transformer outperforms the BiLSTM across all headline metrics.
- Largest gains are in Macro F1 (+0.0327), showing improved balance across classes.
- Perplexity is lower for the transformer, indicating better probabilistic fit.

## Dataset Summary

From the project notebooks:

- Train: 176,642 sentences
- Validation: 29,672 sentences
- Test: 29,578 sentences

Class distribution is moderately imbalanced, with METHODS and RESULTS as the most frequent categories and OBJECTIVE as the least frequent.

## Modeling Approach

### 1) BiLSTM Baseline

- Embedding -> BiLSTM -> Dropout -> Linear classifier
- Uses class weights from training data
- Checkpoint: models/lstm_best.pt

### 2) Transformer Fine-Tune

- Base model: microsoft/BiomedNLP-PubMedBERT-base-uncased-abstract
- Fallback option in notebook: distilbert-base-uncased
- Checkpoint: models/transf_best.pt

## Repository Structure

```text
Project3/
├── README.md
├── requirements.txt
├── EDA_PubMedRCT20k.ipynb
├── Model_PubMedRCT20k.ipynb
├── figures/
│   ├── abstract_lengths.png
│   ├── char_features.png
│   ├── class_distribution.png
│   ├── confusion_matrices_comparison.png
│   ├── eda_summary.png
│   ├── error_by_length.png
│   ├── lstm_confusion_matrix.png
│   ├── lstm_training_curves.png
│   ├── model_comparison.png
│   ├── per_class_f1.png
│   ├── sentence_lengths.png
│   ├── top_words_per_class.png
│   ├── transf_confusion_matrix.png
│   └── transf_training_curves.png
├── logs/
└── models/
	├── lstm_best.pt
	└── transf_best.pt
```

## Environment Setup

Install dependencies:

```bash
pip install -r requirements.txt
```

The pinned versions in requirements.txt were captured from the active notebook kernel used for this project.

## Quick Start

1. Run exploratory analysis notebook:

```bash
jupyter notebook EDA_PubMedRCT20k.ipynb
```

2. Run modeling notebook:

```bash
jupyter notebook Model_PubMedRCT20k.ipynb
```

## Reproducibility Notes

- Random seeds are set in the modeling notebook for Python, NumPy, and PyTorch.
- Data, figures, and model artifact directories are created automatically by notebook code.
- Reported metrics in this README come from recorded notebook outputs.

## Dependencies Used in This Project

Core packages:

- datasets==4.6.1
- matplotlib==3.10.8
- numpy==2.4.2
- pandas==3.0.1
- scikit-learn==1.8.0
- seaborn==0.13.2
- torch==2.10.0
- tqdm==4.67.3
- transformers==5.3.0

Optional:

- wordcloud (conditionally imported in EDA notebook)

## Authors

Joseph Luper Tsenum: PhD Researcher in Biomedical Engineering (Modeling and Biomedical Data Science Specialization), University of Florida. Joseph develops Generative AI platforms for designing novel oligonucleotides and applies machine learning methods to biomedical data analysis and drug discovery.

## Team Contributions

| Member | Contributions |
|---|---|
| Joseph L. Tsenum | Pipeline architecture, model training, transformer fine-tune model implementation, report writing, GitHub management |
| Haibin Fan | Transformer fine-tune model setup, hyperparameter tuning, training dynamics analysis, report writing |
| Ayushi Elhence | Data exploration, literature review, evaluation analysis |

## Collaboration

Throughout the project, the team maintained a highly collaborative workflow, meeting regularly to discuss progress, make decisions, and coordinate tasks. As a group, the team collectively shaped the direction of the project and worked together across all stages, including data preprocessing, model development, evaluation, report preparation, and application development.

Meetings were held where team members jointly reviewed analyses, implemented modeling approaches, and refined the outputs for each phase. The final notebooks and project artifacts were compiled collaboratively to ensure consistency and reproducibility across the entire pipeline.

Joseph was responsible for ensuring that the various components of the project, including data preprocessing, modeling outputs, explainability analyses, and any interactive deliverables, remained aligned and coherent across phases. At the same time, the collaborative contributions of the entire team made it possible to efficiently develop supporting documentation and presentation materials, as different sections produced by team members were integrated into a unified narrative.

This project reflects the type of collaborative environment commonly encountered in real-world industry and research settings, where interdisciplinary teams contribute complementary expertise. Team members were able to work together productively, resolve challenges constructively, and learn from one another's technical strengths and soft skills, resulting in a cohesive and well-executed final product.

## Citation

If you use this work, please cite:

```bibtex
@misc{tsenum2026pubmedrct20k,
	title={PubMed RCT 20k Sentence Role Classification with BiLSTM and PubMedBERT},
	author={Tsenum, Joseph Luper and Fan, Haibin and Elhence, Ayushi},
	year={2026},
	institution={University of Florida},
	note={BME6938 Medical AI, Project 3}
}
```

## Disclaimer

This project is for research and educational use only. It is not a clinical decision support tool.
