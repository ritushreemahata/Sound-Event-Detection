# Sound-Event-Detection
Polyphonic Sound Event Detection using a Convolutional Recurrent Neural Network (CRNN) trained on TUT Sound Events 2016 achieves Val F1=0.820 and Val AUC=0.931 across 17 environmental sound classes.
# Sound Event Detection using CRNN

A deep learning system for **polyphonic sound event detection** built with
TensorFlow/Keras. The model detects 17 environmental sound classes from raw
audio and outputs frame-level onset/offset timestamps for each event.

Trained and evaluated on the
[TUT Sound Events 2016](https://zenodo.org/record/996424) dataset.

---

## Results

| Metric | Value | Epoch |
|---|---|---|
| Validation F1 Score | **0.820** | 68 |
| Validation AUC | **0.931** | 54 |
| Validation BCE Loss | **0.0432** | 74 |
| Training stopped | Epoch 82 | (EarlyStopping, best=74) |

---

## Architecture — CRNN
## CRNN Architecture

<p align="center">
  <img src="assets/Architecture Diagram.png" width="800">
</p>

---

## Dataset

**TUT Sound Events 2016** — Development Set

- 22 WAV recordings, ~2 hours total
- 17 sound classes across 2 scenes (Home + Residential Area)
- Manual strong labels (precise onset + offset timestamps)
- Source: Tampere University of Technology
- DOI: [10.5281/zenodo.996424](https://zenodo.org/record/996424)

Sound classes include: bird singing, car passing by, people walking,
water tap running, dishes, cupboard, wind blowing, children shouting,
and 9 more.

---

## Feature Extraction

| Parameter | Value |
|---|---|
| Sample rate | 22,050 Hz |
| FFT window | 2,048 samples (~93 ms) |
| Hop length | 512 samples (~23 ms) |
| Mel filters | 40 |
| Segment length | 128 frames (~3 seconds) |
| Overlap | 50% |

---

## Training Configuration

| Parameter | Value |
|---|---|
| Optimizer | Adam (lr = 0.001) |
| Loss | Binary Cross-Entropy |
| Batch size | 32 |
| Max epochs | 100 |
| EarlyStopping patience | 8 |
| ReduceLROnPlateau patience | 5, factor 0.5 |
| Dropout | 0.3 throughout |

The learning rate was automatically reduced 5 times during training
(0.001 → 0.0005 → 0.00025 → 0.000125 → 0.0000625 → 0.00003125),
with each reduction giving measurable F1 improvements.

---



