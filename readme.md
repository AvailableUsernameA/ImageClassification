# Automated Glue Inspection System (Engine Parts)

**PyTorch-based real-time image classification for quality control**  
*Code not public due to intellectual property restrictions.*

---

## System Overview

Automated visual inspection system for detecting **incomplete glue application** on engine components.

- **Input**: Scanned images (PNG) from production station
- **Output**: Classifies as `OK` (complete) or `NG` (incomplete/defective)
- **Accuracy**: **97%** on validation set (internal test data)
- **Takt Time**: 150 seconds per station → **ample processing window**

---

## Workflow Design

```mermaid
graph TD
    A[Scanner saves image as *.png] --> B[Monitor watches directory]
    B --> C{New PNG detected?}
    C -->|Yes| D[Wait 1s (configurable)]
    D --> E[Move & rename: part123_OK.png or part123_NG.png]
    E --> F[Classification Model (PyTorch)]
    F --> G[Result logged + UI alert]

