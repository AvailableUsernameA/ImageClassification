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
    A[Scanner program saves<br>image as *.png<br>in watched directory] 
    B[Monitor watches directory]
    B --> C{New PNG<br>detected?}
    C -->|Yes| D[Wait 1s :configurable:<br>Classification Model PyTorch]
    C -->|No| F
    D --> E[Move & rename:<br>part123_OK.png or<br>part123_NG.png]
    E --> F[Result logged]
    F --> G[Wait 5s :configurable]
    G --> B











