# Feature Fusion for Pretrained Speech Models in Recognizing Mad Thabi'i Readings of Iqro' Volume 2

Code and experimental results for recognizing the 69 *mad thabi'i* (prolonged-vowel) reading items of Iqro' Volume 2 with four pretrained speech models (wav2vec2-base, HuBERT-base, WavLM-base-plus, Whisper-tiny) under three input scenarios: baseline, +MFCC (20) fusion, and +log-Mel (80) fusion (12 experiments in total), evaluated on a speaker-independent split (7 training / 1 validation / 2 test speakers).

The task is to recognize which reading was produced, including whether its vowels were prolonged. Makhraj and other aspects of tajweed are not assessed.

## Repository structure

```
iqro2-madthabii-feature-fusion/
├── IQRO_Panjang_Speaker_12Eksperimen.ipynb   # full pipeline: preprocessing, features, training, evaluation (Google Colab)
├── result/                    # metrics, per-epoch history and test predictions of all 12 runs
│   ├── Skenario_1/ (baseline)  # <model>/history.csv, <model>/test_predictions.csv, ...
│   ├── Skenario_2/ (+MFCC)
│   ├── Skenario_3/ (+log-Mel)
│   ├── _shared/                # speaker split, CTC tokenizer, Whisper processor, feature statistics
│   └── summary_final_report.csv
├── requirements.txt
└── README.md
```

## Dataset

2,055 utterances (10 adult speakers, 5 male / 5 female, aged 19–22, 3 repetitions of 69 reading items, 81 transcription labels: 69 target readings and 12 reading variants), recorded in an ordinary residential room with a wired earphone microphone on Android smartphones and segmented in Audacity. Labels follow the reading actually produced by each speaker. The audio recordings are **not included** in this repository; they are available from the corresponding author upon reasonable request.

## How to run

1. Open `IQRO_Panjang_Speaker_12Eksperimen.ipynb` in Google Colab (GPU runtime; experiments were run on an NVIDIA L4).
2. Set the dataset and output paths in the configuration cell.
3. Run all cells. Finished runs are skipped automatically, interrupted runs resume from the last checkpoint.

## Results (test set: 405 utterances from 2 unseen speakers)

| Scenario | Model | Accuracy (%) | WER (%) | CER (%) | PER (%) | Invalid (%) | Inference (ms) |
|---|---|---|---|---|---|---|---|
| Baseline | wav2vec2-base | 78.02 | 21.98 | 3.72 | 3.98 | 19.01 | 2.67 |
| Baseline | HuBERT-base | 75.80 | 24.20 | 3.74 | 4.05 | 20.25 | 2.67 |
| Baseline | WavLM-base-plus | 80.74 | 19.26 | 2.79 | 2.86 | 15.80 | 3.68 |
| Baseline | Whisper-tiny | 89.88 | 10.12 | 2.17 | 2.13 | 5.43 | 8.11 |
| +MFCC (20) | wav2vec2-base | 83.21 | 16.79 | 2.53 | 2.65 | 12.35 | 2.68 |
| +MFCC (20) | HuBERT-base | 61.73 | 38.27 | 6.62 | 6.96 | 35.06 | 2.72 |
| +MFCC (20) | WavLM-base-plus | 84.44 | 15.56 | 2.84 | 3.10 | 11.11 | 3.51 |
| +MFCC (20) | Whisper-tiny | 88.64 | 11.36 | 3.27 | 3.32 | 7.16 | 8.47 |
| +log-Mel (80) | wav2vec2-base | 79.51 | 20.49 | 3.46 | 3.92 | 18.52 | 2.72 |
| +log-Mel (80) | HuBERT-base | 60.74 | 39.26 | 7.52 | 7.73 | 35.31 | 2.73 |
| +log-Mel (80) | WavLM-base-plus | 84.94 | 15.06 | 2.25 | 2.46 | 12.84 | 3.62 |
| +log-Mel (80) | Whisper-tiny | 89.14 | 10.86 | 2.73 | 2.65 | 6.67 | 8.66 |

## Citation

If you use this code, please cite:

F. R. Husna, S. Hidayat, "Feature fusion for pretrained speech models in recognizing mad thabi'i readings of Iqro' Volume 2: An ablation study," El-Cezeri Journal of Science and Engineering, 2026 (under review).

## License

Code: MIT License. Contact: [fadhilahraisa12@students.unnes.ac.id](mailto:fadhilahraisa12@students.unnes.ac.id)
