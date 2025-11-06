# Automated Glue Inspection System (Engine Parts)

**PyTorch-based real-time image classification for quality control**  
*Code not public due to intellectual property restrictions.*

---

## Background
In the production process, adhesive is applied to a certain component of an engine. However, in some cases, the adhesive may be incompletely applied. To ensure quality control, each part needs to be visually inspected and classified as either:  
OK: Adhesive has been properly applied.  
NG: Adhesive application is incomplete or defective.  



## Workflow Overview

Here’s how the image classification and processing pipeline works:

- **Scanning Program**: The scanning program captures an image of the part and saves it as a PNGfile in the designated scanning directory.  
- **Monitoring Program**:  
    The monitoring program continuously watches the scanning directory for new PNG files.  
    Once a new PNG is detected, it retrieves the image name and waits for one second(configurable) to avoid read-write conflicts — this is safe given that the station cycle time is 150 seconds, leaving ample processing time.  
    After the delay, the monitoring program starts the image classification process (e.g., using a trained model to determine OK/NG).  
- **Classification & File Management**:  
After classification, the monitoring program moves the image from the scanning directory to a target (output) directory.  
It then renames the image by appending either _OKor _NGto the filename, indicating the classification result.  
- **Downstream Processing**:
  Other programs or systems further process the images located in the target directory, based on their OK/NG labels.  

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











