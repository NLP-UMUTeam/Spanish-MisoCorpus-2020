# Spanish-MisoCorpus-2020
## Detecting misogyny in Spanish tweets: An approach based on linguistic features and word embeddings  
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.18243769.svg)](https://doi.org/10.5281/zenodo.18243769)


Spanish-MisoCorpus-2020 is a Spanish Twitter corpus for misogyny detection, originally released in 2020.
The dataset includes several thematic subsets (e.g. SELA, VARW, DDSS) and was manually annotated following detailed annotation guidelines.

This repository provides:
- the original data distribution used in the publication,
- and an updated, consolidated version designed to improve reuse and FAIR compliance.

### TL-DR: Highlights
- Compilation of **Spanish MisoCorpus-2020**, a balanced corpus of Spanish tweets related to misogyny.
- 7,682 tweets annotated as **misogyny** vs **not misogyny**, with each instance reviewed by at least two annotators.
- Three complementary subsets:
  1. **VARW** – Violence Against Relevant Women  
  2. **SELA** – European Spanish vs Latin American Spanish  
  3. **DDSS** – Discredit, Dominance, Sexual harassment and Stereotype   
- Manual annotation guidelines that consider figurative language, out-of-domain content and news accounts.
- Baseline and proposed models based on **linguistic features** and **average word embeddings (AWE+LF)**, achieving up to **85.175% accuracy** and outperforming bag-of-words models.
- External validation on existing misogyny and hate-speech corpora (AMI, HatEval), where the proposed model improves previous baselines.

---

### Authors

- **José Antonio García-Díaz** — University of Murcia  
  [Google Scholar](https://scholar.google.com/citations?user=ek7NIYUAAAAJ) · [ORCID](https://orcid.org/0000-0002-3651-2660)

- **Mar Cánovas-García** — University of Murcia  

- **Ricardo Colomo-Palacios** — Østfold University College  
  [Google Scholar](https://scholar.google.es/citations?user=CpqizXUAAAAJ&hl=es) · [ORCID](https://orcid.org/0000-0002-1555-9726)

- **Rafael Valencia-García** — University of Murcia  
  [Google Scholar](https://scholar.google.com/citations?user=GLpBPNMAAAAJ) · [ORCID](https://orcid.org/0000-0003-2457-1791)  

> **Affiliations**  
> *Faculty of Computer Science, University of Murcia, Spain*  
> *Faculty of Computer Sciences, Østfold University College, Norway*

---

### Publication
> **Detecting misogyny in Spanish tweets. An approach based on linguistics features and word embeddings**  
> *Future Generation Computer Systems*, Volume 114, 2021, Pages 506–518.

- **DOI:** https://doi.org/10.1016/j.future.2020.08.032

---

### Abstract
Online social networks provide unprecedented reach to spread messages that target and harass women. Misogyny in Spanish social media is often subtle and context-dependent, which makes its automatic detection particularly challenging. This work has a twofold contribution. First, the authors compile **Spanish MisoCorpus-2020**, a balanced corpus of Spanish tweets labelled as *misogyny* or *not misogyny*, and structured into three subsets: tweets attacking highly visible women (**VARW**), tweets written in European vs. Latin American Spanish (**SELA**), and tweets reflecting general misogynistic traits such as discredit, dominance, sexual harassment and stereotyping (**DDSS**). Second, they propose a classification approach based on **average word embeddings** combined with **linguistic features** (AWE+LF) to analyse which phenomena contribute most to misogyny detection. Using several machine-learning classifiers (Random Forest, SMO, Linear SVM), the best configuration reaches an overall accuracy of **85.175%**, outperforming a bag-of-words baseline and models using only linguistic features or only embeddings. The approach is also evaluated on external datasets for misogyny and hate speech in Spanish, obtaining competitive results and confirming the usefulness of Spanish MisoCorpus-2020 for research on online misogyny.   

---

### Dataset
The repository contains two main data distributions:

#### 1. Original distribution (legacy)
The original dataset distribution follows the structure used in the associated publication, where tweets are grouped into multiple text files according to subset and class label. These files are preserved for reproducibility purposes.


#### 2. Consolidated FAIR-friendly distribution (recommended)

A consolidated, tabular version of the dataset is provided to facilitate reuse and interoperability.

- `corpus/misocorpus_public.csv`
  - Public version of the dataset.
  - Contains tweet identifiers and annotations only (no tweet text).
  - Fully compliant with Twitter Terms of Service.

  - Restricted version including tweet text.
  - Available for research purposes upon request.


#### Notes about the dataset
Spanish MisoCorpus-2020 is a **balanced binary classification corpus** of Spanish tweets labelled as:

- `misogyny`
- `not-misogyny`

Tweets were compiled from multiple sources, including:

- tweets directed at **relevant women** (activists, politicians, journalists)  
- tweets authored from **European Spanish** and **Latin American Spanish** users  
- tweets discussing general misogynistic topics such as gender violence or harassment   

Each tweet was annotated by at least two annotators; inter-coder agreement measured with **Krippendorff’s Alpha** reached **0.6864**, which is acceptable given the ambiguity of the domain.

#### Access
Due to Twitter’s Terms of Service, the publicly available version of the dataset only includes tweet identifiers and annotations.

The full version of the dataset, including tweet text, can be made available for research purposes upon request. Access is granted under controlled conditions and for non-commercial research use only.

```
https://forms.gle/dEghDPJJ8QrKTDTT9
```

Each subset is distributed in two files: one containing IDs of tweets labelled as *misogyny* and another with IDs labelled as *not misogyny*.

#### Corpus Statistics

The following table summarizes the size and annotation density of each subset and of the full corpus:

| Name             | Misogyny | Not misogyny | Mean \# annotations |
|------------------|---------:|-------------:|--------------------:|
| VARW             | 2,094    | 2,094        | 2.1529              |
| SELA             | 2,081    | 2,081        | 2.3076              |
| DDSS             | 1,665    | 1,665        | 2.1595              |
| **MisoCorpus-2020** | **3,841** | **3,841**     | **2.2240**           |

Note that VARW, SELA and DDSS are **not disjoint**: some tweets belong to more than one subset, so their sizes do not sum to the total number of tweets in MisoCorpus-2020.

---

## Modelling and Evaluation

The paper evaluates several models:

- **Baseline:** Bag-of-Words (BoW) with TF–IDF features.   
- **Proposed approach:**  
  - **Average Word Embeddings (AWE)** using pre-trained Spanish fastText embeddings.  
  - **Linguistic features (LF)** capturing spelling, punctuation, lexical and stylistic traits.  
  - Combined **AWE+LF** to exploit both semantic and linguistic signals.   

Experiments are run with three classifiers:

- Random Forest (RF)  
- Sequential Minimal Optimization (SMO, SVM)  
- Linear SVM (LSVM) 

The best result for MisoCorpus-2020 is obtained with **AWE+LF + SMO**, achieving an accuracy of **85.175%**, clearly outperforming the BoW baseline and single-feature models. 

### Summary of Classification Results (Accuracy %)

| Classifier | Model  | VARW  | SELA   | DDSS   | SMC-2020 |
|------------|--------|-------|--------|--------|----------|
| **RF**     | BoW      | 78.930 | 76.967 | 74.734 | 76.215  |
|            | AWE      | **82.092** | **81.307** | **79.063** | 77.232 |
|            | LF       | 81.112 | 81.740 | 77.613 | 79.237  |
|            | AWE+LF   | 82.092 | 81.307 | 78.912 | **79.302** |
| **SMO**    | BoW      | 78.524 | 76.918 | 74.003 | 73.798  |
|            | AWE      | **84.886** | 82.100 | **81.360** | 81.020 |
|            | LF       | 82.403 | 80.057 | 77.976 | 78.938 |
|            | AWE+LF   | 84.886 | **85.175** | 81.208 | **85.175** |
| **LSVM**   | BoW      | 80.053 | 78.476 | 77.698 | 77.060  |
|            | AWE      | **84.480** | **81.859** | **81.148** | 80.825 |
|            | LF       | 82.283 | 81.115 | 79.245 | 79.263 |
|            | AWE+LF   | 84.480 | 83.734 | 80.755 | **82.882** |


The model is also validated on the **AMI 2018** misogyny dataset and the **HatEval 2019** hate-speech dataset (Task A), where it improves both previous maxima and baselines in macro-averaged F1, confirming the close relationship between misogyny and hate speech against women. 

---

## Licence

The dataset is distributed under the Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0) licence.

This licence applies to the annotations and dataset structure. Tweet text remains subject to Twitter’s Terms of Service.


## Provenance
The dataset was manually annotated by trained annotators following detailed annotation guidelines.
Each instance was reviewed by at least two annotators, with disagreements resolved through discussion.

The original release did not include predefined train/test splits.
An additional split strategy has been later introduced to facilitate experimental reproducibility, while preserving the original data distribution.


---

## Acknowledgments
This work has been supported by the *Spanish National Research Agency (AEI)* and the *European Regional Development Fund (FEDER/ERDF)* through projects **KBS4FIA (TIN2016-76323-R)** and **LaTe4PSP (PID2019-107652RB-I00)**. 
In addition, José Antonio García-Díaz has been supported by *Banco Santander* and *University of Murcia* through the **Doctorado industrial programme**.

---

## Citation
If you use this dataset in your research, please cite the following paper:

```
@article{garcia2021detecting,
  title={Detecting misogyny in Spanish tweets. An approach based on linguistics features and word embeddings},
  author={Garc{\'\i}a-D{\'\i}az, Jos{\'e} Antonio and C{\'a}novas-Garc{\'\i}a, Mar and Colomo-Palacios, Ricardo and Valencia-Garc{\'\i}a, Rafael},
  journal={Future Generation Computer Systems},
  volume={114},
  pages={506--518},
  year={2021},
  publisher={Elsevier}
}
```

or the Zenodo record:
```
García-Díaz, J. A. et al. (2026).
Spanish-MisoCorpus-2020: A Spanish Twitter Corpus for Misogyny Detection.
Zenodo. https://doi.org/10.5281/zenodo.18243769
```

