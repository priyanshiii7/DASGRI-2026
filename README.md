# Multimodal Text Detection and Recognition in Medical Images
### Research Paper — Submitted to DASGRI 2026 (Springer LNNS: ComSIA 2026)

> Automating text extraction from medical images using CNNs and Transformers to eliminate manual annotation bottlenecks in clinical workflows.

---

## The Problem

Medical images — X-rays, MRIs, pathology slides — contain critical embedded text: patient identifiers, diagnostic notes, measurement labels. Manually extracting this text is:
- **Slow** — creates bottlenecks in clinical workflows
- **Error-prone** — manual transcription introduces mistakes
- **Unscalable** — healthcare generates millions of images daily

Standard OCR systems fail here. They're built for clean documents, not complex medical scans with low-contrast text, variable orientations, overlapping structures, and domain-specific abbreviations. Specialized medical OCRs cap out at **88–92% accuracy** — not good enough for clinical use.

---

## The Solution

A **two-stage multimodal pipeline** that integrates text detection and recognition end-to-end:

```
Medical Image Input
        ↓
Preprocessing (normalize formats, reduce noise)
        ↓
ResNet-50 Backbone → Visual Feature Extraction
        ↓
EAST Architecture → Text Detection Module
(handles variable orientations, sizes, low-contrast)
        ↓
Multimodal Integration Layer
(fuses visual features + textual context)
        ↓
Output: Localized text + Confidence scores
```

---

## Architecture

### Visual Feature Extraction
- **ResNet-50** backbone — captures both low-level and high-level image features
- Preserves spatial context for faint or irregular text in medical scans
- Fused with textual information through a multimodal integration layer

### Text Detection Module
- Adapted **EAST (Efficient and Accurate Scene Text Detector)** architecture
- Tuned specifically for medical imaging characteristics
- Handles: variable text orientations, multiple font sizes, low-contrast backgrounds
- Outputs bounding boxes + confidence scores for each detected text region

### Text Recognition
- Transformer-based recognition module processes detected regions
- Handles domain-specific medical vocabulary and abbreviations
- Simultaneous detection and recognition in a unified pipeline

---

## Datasets

Three real-world medical imaging modalities tested:

| Dataset | Content | Challenge |
|---|---|---|
| **Chest X-Rays** | Patient IDs, scan details, measurement labels | Standardized layout, clearer contrast |
| **Brain MRIs** | Slice positions, orientation markers, scan parameters | Variable orientations, lower contrast |
| **Pathology Slides** | Whole-slide images (WSIs), tissue annotations | Extremely large images, complex backgrounds |

---

## Implementation

| Component | Choice | Reason |
|---|---|---|
| Framework | PyTorch | Flexibility + GPU acceleration |
| Backbone | ResNet-50 | Strong image feature extraction |
| Text Detector | EAST | Real-time capable, no post-processing needed |
| Optimizer | Adam | Adaptive, works well across vision tasks |
| Learning Rate | 0.001 | Standard for CNN-based training |
| Batch Size | 16 | Balances stability with GPU memory constraints |
| Epochs | ~50 with early stopping | Prevents overfitting |
| Hardware | NVIDIA GPU (16GB+ VRAM) | Required for large medical image processing |

---

## Expected Results

Based on state-of-the-art benchmarks:

| Metric | Expected Performance |
|---|---|
| Mean IoU (text detection) | **0.75 – 0.80** |
| Best performing modality | Chest X-Rays (standardized layout) |
| Most challenging modality | Pathology Slides (complex backgrounds) |

Performance variation across modalities reflects real-world imaging complexity — demonstrating the system's robustness across diverse clinical scenarios.

---

## Clinical Impact

- **Workflow automation** — eliminates manual text annotation from radiologist pipelines
- **Error reduction** — removes human transcription mistakes from clinical records
- **Scalability** — handles the volume of images modern healthcare generates
- **Regulatory alignment** — designed with FDA AI/ML medical device guidelines in mind

---

## Research Contributions

1. A unified theoretical framework for multimodal text detection + recognition in medical images
2. Adaptation of EAST architecture specifically for medical imaging constraints
3. Cross-modality evaluation across X-rays, MRIs, and pathology slides
4. Analysis of challenges: low-contrast text, curved text, domain-specific abbreviations, multilingual limitations

---

## Known Limitations & Future Work

- Currently optimized for **English machine-printed text** only
- Handwritten clinical annotations remain a challenge
- Multilingual recognition requires specialized training data
- Real-time deployment on standard hospital hardware needs model pruning/quantization
- Clinical validation studies with practicing radiologists needed

---

## Tech Stack

`Python` `PyTorch` `ResNet-50` `EAST` `CNN` `Transformers` `Computer Vision` `Medical Imaging` `Deep Learning`

---

## Publication

**Submitted to:** Springer LNNS — ComSIA 2026 (DASGRI Conference)  
**Author:** Priyanshi Rathore, Government Engineering College Bikaner  
**Contact:** priyanshirathore57@gmail.com

---

## Related Work
- [XAI for Clinical Decision Support](https://github.com/priyanshiii7/XAI) — companion research on Explainable AI in medical diagnosis
- [Healthcare Monitoring System](https://github.com/priyanshiii7/healthcare_monitoring) — real-time IoT health data pipeline
