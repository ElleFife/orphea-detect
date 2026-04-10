# orphea-detect

```markdown
# Orphea Detect

Open source AI music detection. Built for independent artists.

[![MIT License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![HuggingFace Space](https://img.shields.io/badge/HuggingFace-Space-blue)](https://huggingface.co/spaces/OrpheaLabs/orphea-detect)

---

## What it does

Upload a track. Get back a human score, a verdict, and a breakdown of what the model actually found. Takes 30 seconds. No login, no paywall, no data stored without your consent.

Accepts MP3, WAV, FLAC, AIFF up to 20MB. Analyzes the first 30 seconds.

**[Try it on HuggingFace Spaces](https://huggingface.co/spaces/OrpheaLabs/orphea-detect)**

---

## Why we built this

Artists are getting flagged, removed, and dismissed as AI without any way to push back. Sync licensing desks, streaming platforms, and labels are all scrutinizing provenance now, and independent artists have no tool, no recourse, and no seat at the table.

This project is part of Orphea Labs, a research and policy org working at the intersection of AI, music, and artist rights.

---

## How it works

```
Your audio file
      |
Mel-spectrogram extraction (first 30 seconds)
      |
MobileNetV3 classifier fine-tuned on FakeMusicCaps
      |
Human score + verdict + signal breakdown
```

Trained on [FakeMusicCaps](https://huggingface.co/datasets/polimi-ispl/FakeMusicCaps), ~10,000 clips of AI-generated vs human-made music.

---

## Be honest about what this is

This is a probabilistic tool, not a court document.

- It was trained on specific generators. Suno, Udio, and anything released after our training cutoff may behave unexpectedly.
- MP3 compression, pitch shifting, and time-stretching all degrade accuracy.
- A high human score is not legal proof of anything.
- Out-of-domain accuracy is meaningfully lower than the headline benchmark numbers.

Full eval results including out-of-domain scores are in the [model card](https://huggingface.co/OrpheaLabs/orphea-detect-v1).

---

## Model

| Detail | Value |
|---|---|
| Architecture | MobileNetV3-Small |
| Input | Mel-spectrogram, 128 bands, first 30s |
| Training data | FakeMusicCaps, 8,000 clips |
| Task | Binary: AI vs human |
| HuggingFace | [OrpheaLabs/orphea-detect-v1](https://huggingface.co/OrpheaLabs/orphea-detect-v1) |

---

## Run locally

```bash
git clone https://github.com/ElleFife/orphea-detect
cd orphea-detect
pip install -r requirements.txt
python detect.py --file your_track.mp3
```

Requires Python 3.9+, torch, librosa, transformers, huggingface_hub.

---

## Contribute

**Researchers and ML engineers:** submit a better model via PR, run the eval suite on a new generator, or improve the augmentation pipeline. See [CONTRIBUTING.md](CONTRIBUTING.md) for the eval protocol.

**Artists:** use the tool, report wrong results as issues, and optionally contribute your track to the open dataset (opt-in, your call).

**Policy researchers:** the model card has citation details. Reach out via GitHub issues if you want to collaborate.

---

## Leaderboard

Open benchmark evaluated on FakeMusicCaps and SONICS. Want to submit a model? See [CONTRIBUTING.md](CONTRIBUTING.md).

| Model | F1 in-domain | F1 out-of-domain | Submitted by |
|---|---|---|---|
| MobileNetV3-MelSpec | pending | pending | Orphea Labs |

---

## Roadmap

- [x] Repo setup, MIT license
- [ ] v1.0 — MobileNetV3 baseline, Gradio Space live
- [ ] v1.1 — Augmentation (pitch shift, MP3 compression simulation)
- [ ] v1.2 — Out-of-domain eval on SONICS
- [ ] v2.0 — Stem separation, per-stem detection
- [ ] v2.0 — Multi-model ensemble
- [ ] v3.0 — Community dataset contributions, automated leaderboard

---

## Citation

```bibtex
@software{orphea_detect_2026,
  author    = {{Orphea Labs}},
  title     = {Orphea Detect: Open Source AI Music Detection},
  year      = {2026},
  publisher = {Orphea Labs},
  url       = {https://github.com/ElleFife/orphea-detect},
  license   = {MIT}
}
```

---

MIT License. See [LICENSE](LICENSE).

Orphea Labs · For independent artists worldwide
```
