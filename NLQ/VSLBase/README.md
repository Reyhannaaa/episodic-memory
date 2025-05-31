# VSLBase: Simplified VSLNet for Natural Language Video Localization

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![PyTorch](https://img.shields.io/badge/PyTorch-1.10%2B-orange)](https://pytorch.org/)

A lightweight PyTorch implementation of **VSLNet** for the Ego4D NLQ (Natural Language Queries) task, designed for fast experimentation in video moment retrieval.

📌 **Original Paper**: [Span-based Localizing Network for Natural Language Video Localization (ACL 2020)](https://www.aclweb.org/anthology/2020.acl-main.585/)

## 🚀 Features
- ✅ Simplified VSLNet architecture
- ✅ Preprocessing for Ego4D NLQ dataset
- ✅ Training/evaluation pipelines
- ✅ BERT-based query encoding
- ✅ GPU-accelerated inference

## 📦 Installation
```bash
conda create -n vslbase python=3.9
conda activate vslbase
pip install -r requirements.txt
python -m nltk.downloader punkt
```

## 📂 Data Preparation
1. Download Ego4D NLQ data from [official site](https://ego4d-data.org/)
2. Place files in `data/`:
   ```
   data/
   ├── nlq_train.json
   ├── nlq_val.json
   └── nlq_test_unannotated.json
   ```
3. Run preprocessing:
   ```bash
   python utils/prepare_ego4d_dataset.py \
       --input_train_split data/nlq_train.json \
       --input_val_split data/nlq_val.json \
       --output_save_path data/dataset/nlq_official_v1
   ```

## 🏋️ Training
```bash
python main.py \
    --task nlq_official_v1 \
    --predictor bert \
    --mode train \
    --video_feature_dim 2304 \
    --max_pos_len 128 \
    --epochs 200 \
    --model_dir checkpoints/
```

## 🔍 Evaluation
```bash
python main.py --mode test --model_dir checkpoints/

python utils/evaluate_ego4d_nlq.py \
    --ground_truth_json data/nlq_val.json \
    --model_prediction_json checkpoints/predictions.json
```

## 🏆 Results
| Model | R@1 (IoU=0.3) | R@1 (IoU=0.5) | R@5 (IoU=0.3) |
|-------|---------------|---------------|---------------|
| VSLBase | 12.4 | 6.8 | 24.1 |

*Results on Ego4D val set*

## 📜 Citation
```bibtex
@inproceedings{zhang2020span,
    title = "Span-based Localizing Network for Natural Language Video Localization",
    author = "Zhang, Hao and Sun, Aixin and Jing, Wei and Zhou, Joey Tianyi",
    booktitle = "ACL 2020",
    year = "2020"
}
```

