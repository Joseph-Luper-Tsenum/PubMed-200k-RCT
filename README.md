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

Haibin Fan: Master’s Student in Biomedical Engineering (Medical Imaging and AI), University of Florida. Haibin works on medical imaging analysis and develops data-driven models for clinical applications, including ultrasound treatment planning and healthcare prediction tasks.

Ayushi Elhence: Fourth-year undergraduate student in Biomedical Engineering at the University of Florida.

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

# Declaration of AI Use

We acknowledge the use of Claude Sonnet 4.6 and GitHub Copilot AI tools to support our understanding and assist with coding, particularly in implementing the PyTorch training loops, HuggingFace integration, and visualization code. All model design decisions, hyperparameter choices, and analytical interpretations are our own. 

## References

- P. B. Jensen et al., "Mining electronic health records: towards better research applications and clinical care," Nat. Rev. Genet., vol. 13, no. 6, pp. 395–405, 2012.​
​
- I. J. Marshall and B. C. Wallace, "Toward systematic review automation: a practical guide to using machine learning tools in research synthesis," Syst. Rev., vol. 8, no. 163, 2019.​
​
- F. Dernoncourt and J. Y. Lee, "PubMed 200k RCT: a dataset for sequential sentence classification in medical abstracts," arXiv:1710.06071, 2017.​
​
- S. Hochreiter and J. Schmidhuber, "Long short-term memory," Neural Comput., vol. 9, no. 8, pp. 1735–1780, 1997.​
​
- Y. Gu et al., "Domain-specific language model pretraining for biomedical natural language processing," ACM Trans. Comput. Healthcare, vol. 3, no. 1, pp. 1–23, 2022.​
​
- G. Guyatt et al., "Users' guides to the medical literature: IX. A method for grading health care recommendations," JAMA, vol. 274, no. 22, pp. 1800–1804, 1995.​
​
- A. Merity et al., "Regularizing and optimizing LSTM language models," in ICLR, 2018.​
​
- D. Jin and P. Szolovits, "Hierarchical neural networks for sequential sentence classification in medical scientific abstracts," in EMNLP, 2018, pp. 3100–3109.​
​
- I. Beltagy, K. Lo, and A. Cohan, "SciBERT: A pretrained language model for scientific text," in EMNLP, 2019.​
​
- J. Lee et al., "BioBERT: a pre-trained biomedical language representation model for biomedical text mining," Bioinformatics, vol. 36, no. 4, pp. 1234–1240, 2020.

- A. Cohan et al., "A discourse-aware attention model for abstractive summarization of long documents," in NAACL-HLT, 2018.​
​
- K. Huang et al., "Clinical XLNet: Modeling sequential clinical notes and predicting prolonged mechanical ventilation," in ACL BioNLP, 2020.​
​
- A. Mulyar, E. Ozler, and M. Finlayson, "MT-clinical BERT: scaling clinical information extraction with multitask learning," J. Am. Med. Inform. Assoc., vol. 28, no. 10, pp. 2108–2115, 2021.​
​
- M. Agarwal and H. Yu, "Automatically classifying sentences in full-text biomedical articles into introduction, methods, results and discussion," Bioinformatics, vol. 25, no. 23, pp. 3174–3180, 2009.​
​
- B. C. Wallace et al., "Extracting PICO sentences from clinical trial reports using supervised distant supervision," J. Mach. Learn. Res., vol. 17, no. 1, pp. 4572–4596, 2016.​
​
- J. Devlin et al., "BERT: Pre-training of deep bidirectional transformers for language understanding," in NAACL-HLT, 2019.​
​
- A. Paszke et al., "PyTorch: An imperative style, high-performance deep learning library," in NeurIPS, 2019.​
​
- T. Wolf et al., "HuggingFace's Transformers: State-of-the-art natural language processing," in EMNLP, 2020.​
​
- F. Pedregosa et al., "Scikit-learn: Machine learning in Python," JMLR, vol. 12, pp. 2825–2830, 2011.​
​
- M. E. Peters et al., "Deep contextualized word representations," in NAACL-HLT, 2018.
​
## Disclaimer

This project is for research and educational use only. It is not a clinical decision support tool.
