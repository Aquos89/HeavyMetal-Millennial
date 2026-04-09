# 🎸 Heavy Metal & the Millennial Generation
### A Comparative Study of Manual and Machine Learning-Based Lyrical Topic Analysis

> **Studienleistung – Maschinelles Lernen (Übung)**  
> Oscar Aquite · Matrikelnummer: 2480950

---

## 📖 Overview

This project compares two approaches to thematic analysis of heavy metal lyrics from the millennial era (2000–2009):

- **Manual analysis** — Evan Chabot's 2012 qualitative study of 250 songs, coded into 115 thematic categories
- **ML-based analysis** — Automated topic modelling using Word2Vec and LDA, applied to a corpus of 68,000+ English-language songs

The goal is to evaluate how well computational methods replicate or diverge from human interpretive analysis in the context of music and cultural studies.

---

## 🗂️ Project Structure

```
├── Metal_(1).ipynb         # Main notebook (full pipeline)
├── metal_manual.csv        # Chabot (2012) manual classification dataset
└── README.md
```

---

## 🔬 Methodology

### 1. Data Acquisition
- Dataset: [Refined Large Metal Lyrics Archive (228k songs)](https://www.kaggle.com/datasets/sebastianeck/refined-large-metal-lyrics-archive-228k-songs) via Kaggle API
- Filter: English-language songs released between 2000 and 2009 → **~68,000 songs**

### 2. Preprocessing
- Tokenization and lowercasing with `gensim.utils.simple_preprocess`
- Stopword removal with `nltk`
- Accent stripping (`deacc=True`)

### 3. Word2Vec Model
- Trained on the filtered corpus (`vector_size=100`, `window=5`, `min_count=5`)
- Used for: semantic similarity queries, vector arithmetic, and category vector generation

### 4. Topic Modelling (LDA)
| Configuration | Topics | Perplexity | Coherence (c_v) |
|---|---|---|---|
| LDA Model A | 115 | -11.52 | 0.341 |
| LDA Model B | 10 | -7.96 | 0.341 |

- Topic titles generated via Word2Vec centroid + GPT-assisted labelling
- 115 topics mapped to Chabot's (2012) classification scheme
- 10-topic model used for broader thematic grouping

### 5. Assigned-Category Classification (Multi-label)
- 10 semantic categories defined based on Chabot's framework
- Songs vectorized via mean Word2Vec embeddings
- Cosine similarity against category centroid vectors (`threshold = 0.4`)
- **Coverage: 74.87%** · **Avg. labels/song: 2.10**

### 6. Manual vs. ML Comparison
- Frequencies and proportions compared across both models
- New song classification demo included

---

## 📊 Thematic Categories

| Category | Description |
|---|---|
| `death` | Death, Pain, and Decay |
| `existence` | Existentialism and Psychology |
| `fantasy` | Fantasy, Mythology, and the Supernatural |
| `religion` | Religion, Anti-Religion, and Spirituality |
| `identity` | Identity, Individualism, and Self-Overcoming |
| `war` | War, Power, and Domination |
| `violence` | Violence, Crime, and Punishment |
| `love` | Love, Sex, and Relationships |
| `society` | Society and Social Critique |
| `other` | Other / Miscellaneous |

---

## 🧰 Tech Stack

| Library | Purpose |
|---|---|
| `gensim` | Word2Vec, LDA, Dictionary, CoherenceModel |
| `scikit-learn` | PCA, t-SNE, cosine similarity |
| `nltk` | Stopwords |
| `pandas` | Data manipulation |
| `matplotlib` / `plotly` | Visualizations |
| `langdetect` | Language filtering |
| `kagglehub` | Dataset download |
| `numpy` | Vector operations |

---

## 🚀 Getting Started

### Requirements

```bash
pip install gensim==4.3.2 scikit-learn pandas nltk matplotlib plotly langdetect kagglehub
```

> ⚠️ Recommended: `numpy==1.24.4`, `scipy==1.11.4` for compatibility with gensim 4.3.2

### Kaggle Credentials

You will need a `kaggle.json` file with your Kaggle API credentials to download the dataset. Place it in:

```
~/.kaggle/kaggle.json
```

Or upload it directly in Google Colab when prompted.

### Run

Open and run `Metal_(1).ipynb` sequentially. The notebook is organized into the following sections:

1. Library installation
2. Data acquisition (Kaggle API)
3. Data preparation & preprocessing
4. Word2Vec training & exploration
5. LDA topic modelling (115 and 10 topics)
6. Assigned-category classification
7. Manual vs. ML comparison
8. Conclusions

---

## 📈 Key Findings

- Both manual and ML analyses consistently identify **introspective themes** as dominant in millennial metal — e.g., *Existentialism*, *Reflection*, *Inner Darkness*
- The 115-topic LDA model showed better perplexity than the 10-topic version, suggesting finer granularity improves predictive fit
- The ML model diverges from Chabot's manual coding in topic frequency rankings, but aligns in broad thematic trends
- Themes traditionally associated with the genre (violence, war) ranked lower than expected in both approaches

---

## 📚 References

- Chabot, Evan (2012). *Millennials and Heavy Metal*. University of Central Florida.
- Arnett, J.J. (1991). Heavy metal music and reckless behavior among adolescents. *Journal of Youth and Adolescence*, 20(6), 573–592.
- Blei, D.M., Ng, A.Y., & Jordan, M.I. (2003). Latent Dirichlet Allocation. *JMLR*, 3, 993–1022.
- Mikolov, T. et al. (2013). Efficient Estimation of Word Representations in Vector Space. *arXiv:1301.3781*.

---

## 📄 License

This project was developed for academic purposes at [University Name]. Not intended for commercial use.
