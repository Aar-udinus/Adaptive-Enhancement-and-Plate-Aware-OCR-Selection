Adaptive Enhancement and Plate-Aware OCR Selection for Robust License Plate Recognition in Hazy Conditions

This repository provides the official implementation of the method proposed in the paper:

Adaptive Enhancement and Plate-Aware OCR Selection for Robust License Plate Recognition in Hazy Conditions

The code is released to support reproducibility, transparency, and further research in Automatic License Plate Recognition (ALPR) under adverse visual conditions.

📌 Overview

Automatic License Plate Recognition (ALPR) systems often suffer performance degradation under hazy conditions due to low contrast, blur, and reduced visibility. To address this challenge, this work proposes an adaptive, OCR-oriented pipeline that avoids fixed preprocessing and instead selects the most plausible OCR output based on plate structure and confidence.

The proposed pipeline consists of:

- Global dehazing using Dark Channel Prior (DCP) (dataset-level)

- License plate detection and cropping using YOLOv11

- Adaptive lightweight enhancement on cropped plate regions,Multi-branch OCR using PaddleOCR

- Plate-aware scoring and selection to obtain the final plate output

🧠 Method Pipeline Input Image (Hazy Scene) | (DCP-applied) | YOLOv11 | Plate Crop 

<img src="https://github.com/Aar-udinus/Adaptive-Enhancement-and-Plate-Aware-OCR-Selection/blob/main/OCR-Aware-Selection.png">
🔧 Adaptive Enhancement Variants

Instead of enforcing a single preprocessing strategy, the system generates three lightweight enhancement variants for each cropped plate image:

- RAW Original cropped plate image without additional enhancement.

- CLAHE-light Contrast Limited Adaptive Histogram Equalization with conservative parameters to improve local contrast without distorting character shapes.

- SR2× + CLAHE-light Lightweight 2× upscaling (bicubic interpolation) followed by CLAHE-light, designed for small or low-resolution plates.

- Each variant is processed independently by PaddleOCR.

🔍 Plate-Aware OCR Selection

For each license plate, multiple OCR candidates are generated. The final output is selected using a plate-aware scoring mechanism based on:

- Structural validity of license plate format

- Character ambiguity resolution (e.g., O–0, I–1, B–8)

- OCR confidence score

This adaptive selection strategy improves end-to-end recognition accuracy without aggressive visual enhancement.

📊 Experimental Results (Summary)

- The proposed adaptive method achieves:

- 100% readability rate

- 92.67% end-to-end exact accuracy

- 98.45% average character accuracy

- These results outperform fixed preprocessing baselines such as direct crop OCR and super-resolution-only pipelines under hazy condition.

⚙️ Environment Setup Python >= 3.9 opencv-python paddleocr paddlepaddle torch numpy

⚠️ Note: The project is tested on GPU-based environments. 

▶️ How to Run
- Processing with Dark Chanel Prior (DCP),Detect and crop license plates 
  processing DCP and Yolov11.ipynb

- Apply adaptive enhancement and Select final OCR result
  Adaptive-Aware-Selection.ipynb

- Evaluate performance
  Adaptive-Aware-Selection.ipynb

📁 Dataset

License plate images are sourced from public datasets (e.g., Mendeley Data).

Due to licensing constraints, raw datasets are not redistributed in this repository.

Ground truth labels are provided in text format for evaluation.

📜 License

This project is released for research and academic use only.

📬 Contact

For questions or collaboration, please contact: 📧 aaruniska@gmail.com
