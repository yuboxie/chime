# CHIME: CHinese Internet Meme Explanation Dataset

[![Paper](https://img.shields.io/badge/Paper-arXiv-red)](https://arxiv.org/abs/2510.00567)
[![Paper](https://img.shields.io/badge/Paper-ACL_Anthology-red)](https://aclanthology.org/2025.emnlp-main.863/)
[![Dataset](https://img.shields.io/badge/Dataset-Available-green)](https://github.com/yuboxie/chime)
[![License](https://img.shields.io/badge/License-MIT-blue)](LICENSE)

> **Are Large Language Models Chronically Online Surfers? A Dataset for Chinese Internet Meme Explanation**
>
> *Yubo Xie¹, Chenkai Wang², Zongyang Ma³, Fahui Miao¹*
>
> ¹Shanghai Maritime University, ²École Polytechnique Fédérale de Lausanne, ³Xi'an Jiaotong Liverpool University

## 📖 Overview

CHIME is a comprehensive dataset for evaluating Large Language Models' understanding of Chinese Internet memes. The dataset contains **1,458** popular phrase-based memes from the Chinese Internet, each annotated with detailed metadata including meaning, origin, example sentences, and meme types.

### 🎯 Key Features

- **Comprehensive Coverage**: 1,458 Chinese Internet memes across 6 different types
- **Rich Annotations**: Meaning, origin, example sentences, profanity/offense labels
- **Evaluation Framework**: Two tasks for assessing LLM meme comprehension
- **Cultural Depth**: Covers linguistically and culturally nuanced content

## 📊 Dataset Statistics

| Meme Type               | Count | Percentage |
| ----------------------- | ----- | ---------- |
| Experience (现象)       | 561   | 38.5%      |
| Quotation (引用)        | 438   | 30.0%      |
| Stylistic Device (修辞) | 214   | 14.7%      |
| Homophonic Pun (谐音)   | 133   | 9.1%       |
| Slang (俗语)            | 60    | 4.1%       |
| Abbreviation (缩写)     | 52    | 3.6%       |

- **Profanity**: 75 memes (5.1%)
- **Offensive Content**: 127 memes (8.7%)
- **Memes with Origins**: 525 memes (36.0%)

## 🏗️ Dataset Structure

Each meme entry contains:

```json
{
  "meme": "网络梗词",
  "meaning": "梗词的含义和解释",
  "origin": "梗词的来源和背景（可能为null）",
  "examples": [
    "使用示例1",
    "使用示例2",
    "使用示例3"
  ],
  "profanity": false,
  "offense": false,
  "type_cn": "中文分类",
  "type_en": "English Category"
}
```

**Field Descriptions:**
- `meme` (string): The Internet meme term
- `meaning` (string): Detailed explanation of the meme's meaning and usage
- `origin` (string|null): Background information about the meme's origin
- `examples` (array): List of real usage examples in context
- `profanity` (boolean): Whether the meme contains profanity
- `offense` (boolean): Whether the meme is potentially offensive
- `type_cn` (string): Meme category in Chinese
- `type_en` (string): Meme category in English

## 🔬 Evaluation Tasks

### Task 1: Meme Explanation
- **Objective**: Generate meaning, origin, and example sentences for given memes
- **Evaluation**: Automatic metrics (cosine similarity, BERTScore, BARTScore) + Human evaluation
- **Findings**: Models struggle with culturally nuanced memes (quotation, homophonic pun)

### Task 2: Multiple Choice Questions (MCQ)
- **Objective**: Select the most appropriate meme to fill blanks in contextual sentences
- **Dataset**: 1,268 MCQs with 5 options each
- **Findings**: Human performance (88.6%) outperforms best LLM (80.9%)

## 📈 Benchmark Results

### Explanation Task (Human Evaluation - % Agree)

| Model             | Meaning  | Origin   | Example  |
| ----------------- | -------- | -------- | -------- |
| **DeepSeek-V3**   | **73.6** | 35.4     | **77.4** |
| GLM-4-Plus        | 68.5     | **35.9** | 70.7     |
| GPT-4o            | 53.9     | 18.5     | 55.0     |
| Claude 3.5 Sonnet | 51.0     | 14.4     | 51.7     |
| Qwen2.5-72B       | 45.7     | 14.4     | 46.8     |
| GLM-4-9B          | 40.4     | 7.7      | 41.1     |
| Qwen2.5-7B        | 33.9     | 9.7      | 34.0     |

### MCQ Task (Accuracy)

| Model             | Average  | Experience | Quotation | Stylistic Device | Homophonic Pun | Slang | Abbreviation |
| ----------------- | -------- | ---------- | --------- | --------- | ---------- | ----- | ------------ |
| **DeepSeek-V3**   | **80.9** | 83.1       | 79.1      | 82.8      | 71.3       | 85.8  | 83.3         |
| GLM-4-Plus        | 76.4     | 78.4       | 74.8      | 81.7      | 64.0       | 80.4  | 79.2         |
| GPT-4o            | 73.4     | 77.9       | 70.8      | 76.1      | 54.9       | 85.8  | 75.0         |
| Claude 3.5 Sonnet | 71.8     | 75.8       | 64.4      | 77.8      | 59.7       | 80.0  | 72.9         |
| Qwen2.5-72B       | 69.0     | 73.3       | 69.1      | 69.1      | 48.6       | 86.9  | 67.1         |
| GLM-4-9B          | 52.6     | 57.4       | 52.7      | 53.6      | 36.0       | 65.4  | 50.4         |
| Qwen2.5-7B        | 51.6     | 60.2       | 52.0      | 52.4      | 29.4       | 64.2  | 51.2         |

## 📁 Repository Structure

```
chime/
├── data/
│   ├── chime_full.json          # Complete dataset
│   └── chime_mcq.json           # MCQ test set
├── LICENSE
└── README.md
```

## 🎯 Key Findings

1. **Performance Varies by Meme Type**: Models perform better on experience and slang memes, struggle with quotation and homophonic pun memes
2. **Origin Attribution Challenges**: All models consistently struggle to provide accurate meme origins
3. **Cultural Context Matters**: Culturally and linguistically nuanced memes pose significant challenges
4. **Receptive vs. Productive Understanding**: Models find it easier to recognize appropriate usage than to generate explanations

## 📝 Citation

If you use the CHIME dataset in your research, please cite our paper:

```bibtex
@inproceedings{xie-etal-2025-large,
    title = "Are Large Language Models Chronically Online Surfers? A Dataset for {C}hinese {I}nternet Meme Explanation",
    author = "Xie, Yubo  and
      Wang, Chenkai  and
      Ma, Zongyang  and
      Miao, Fahui",
    booktitle = "Proceedings of the 2025 Conference on Empirical Methods in Natural Language Processing",
    month = nov,
    year = "2025",
    address = "Suzhou, China",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2025.emnlp-main.863/",
    pages = "17073--17094",
    ISBN = "979-8-89176-332-6"
}
```

## ⚖️ Ethical Considerations

- The dataset contains some potentially offensive or inappropriate content, clearly labeled for research purposes
- All personally identifiable information has been anonymized
- We encourage responsible use of this dataset for advancing cultural understanding in AI systems

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📧 Contact

- **Yubo Xie** (Corresponding Author): yuboxie@hotmail.com

## 🙏 Acknowledgments

- Thanks to Geng Baike (梗百科) for providing the source material
- Thanks to all annotators who contributed to the dataset creation
- Special thanks to the research community for valuable feedback

---

**Note**: This dataset is intended for research purposes only. Please use responsibly and consider the ethical implications of your research.
