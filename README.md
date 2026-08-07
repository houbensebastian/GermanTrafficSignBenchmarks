# German Traffic Sign Benchmarks

This site presents two benchmark data sets for computer vision and machine learning research, compiled by the Real-Time Computer Vision group at the Institut für Neuroinformatik (INI), Ruhr-Universität Bochum:

- **[GTSDB — German Traffic Sign Detection Benchmark](#gtsdb--german-traffic-sign-detection-benchmark)**, a single-image detection benchmark presented at IJCNN 2013.
- **[GTSRB — German Traffic Sign Recognition Benchmark](#gtsrb--german-traffic-sign-recognition-benchmark)**, a large multi-category classification benchmark used in a competition at IJCNN 2011.


> **Status notice:** Online submission/leaderboard functionality was retired in 2019 due to maintenance overhead. The datasets, software packages, and previously submitted results remain available for download and reference.

---

## GTSDB — German Traffic Sign Detection Benchmark

The successor to GTSRB: a single-image **detection** problem (localizing signs in full-color images), presented at IJCNN 2013.

**Highlights**
- Single-image detection problem
- 900 images total: 600 training / 300 evaluation
- Signs grouped into three categories chosen to suit detectors with different characteristics
- Was accompanied by an online evaluation and ranking system (now retired)

### Sign categories

Corrected class-ID groupings (see the 2013-01-07 erratum below):

- **Prohibitory** = classes `0,1,2,3,4,5,7,8,9,10,15,16` — circular, white background, red border
- **Mandatory** = classes `33,34,35,36,37,38,39,40` — circular, blue background
- **Danger** = classes `11,18,19,20,21,22,23,24,25,26,27,28,29,30,31` — triangular, white background, red border

### Downloads

- Full training/test dataset with annotations (originally `TrainIJCNN2013.zip` and companion test archive)
- C++ and MATLAB code snippets for reading ground truth, running/evaluating a detector, and formatting submissions
- Baseline results: a Viola–Jones (Haar) detector, a Hough-like circle/triangle voting detector, and a HOG+LDA sliding-window detector

*(Re-host these archives and update the links above as needed.)*

### Citation

> S. Houben, J. Stallkamp, J. Salmen, M. Schlipsing, C. Igel. **Detection of Traffic Signs in Real-World Images: The German Traffic Sign Detection Benchmark.** *International Joint Conference on Neural Networks*, no. 1288, 2013.

```bibtex
@inproceedings{Houben-IJCNN-2013,
    author = {Sebastian Houben and Johannes Stallkamp and Jan Salmen and Marc Schlipsing and Christian Igel},
    booktitle = {International Joint Conference on Neural Networks},
    title = {Detection of Traffic Signs in Real-World Images: The {G}erman {T}raffic {S}ign {D}etection {B}enchmark},
    number = {1288},
    year = {2013}
}
```

### Final competition results (IJCNN 2013)

Perfect results were achieved in individual categories by:
- **wgy@HIT501** — Prohibitory, Mandatory
- **visics** — Prohibitory, Danger
- **LITS1** — Prohibitory

---

## GTSRB — German Traffic Sign Recognition Benchmark

A single-image, multi-class classification problem.

**Highlights**
- More than 40 classes
- More than 50,000 images in total
- Large, lifelike database with reliable ground truth (semi-automatic annotation)
- Each physical traffic sign instance is unique within the dataset (occurs only once in the real world)

### Dataset structure

The training set is organized as:
- One directory per class
- Each directory contains a CSV annotation file (`GT-<ClassID>.csv`) plus the training images
- Images are grouped by **tracks**: each track contains 30 images of a single physical traffic sign

### Image format
- One traffic sign per image
- A 10% border (at least 5 pixels) is included around the traffic sign
- Images are stored as PPM (Portable Pixmap, P6)
- Sizes vary from 15×15 to 250×250 pixels; images are not necessarily square, and the sign is not necessarily centered
- The sign's bounding box is included in the annotations

### Annotation format

CSV files, semicolon-separated, containing:

| Field | Description |
|---|---|
| `Filename` | Filename of the corresponding image |
| `Width` | Image width |
| `Height` | Image height |
| `ROI.x1`, `ROI.y1` | Top-left corner of the traffic sign bounding box |
| `ROI.x2`, `ROI.y2` | Bottom-right corner of the traffic sign bounding box |
| `ClassId` | Assigned class label (training data only) |

### Result submission format

A single CSV file, semicolon-separated, no header, no filename quoting. One row per test image: `filename;classId`

```
00000.ppm; 4
00001.ppm; 22
00002.ppm; 16
00003.ppm; 7
00004.ppm; 6
00005.ppm; 2
...
```

### Pre-calculated features

To lower the barrier for participants without an image-processing background, three pre-computed feature sets are provided (same directory layout as the image set; see each archive's `Feature_description.txt` for parameters):

- **HOG features** — three configurations (vector lengths 1568, 1568, and 2916), computed with the reference implementation from INRIA's object localization toolkit (Dalal & Triggs, HOG for Human Detection, CVPR 2005).
- **Haar-like features** — 5 feature types at multiple sizes (12 variants total), 11,584-dimensional feature vector.
- **Hue histograms** — a 256-bin HSV hue histogram per image.

### Code snippets

- **MATLAB** — iterate over training/test sets, read images and annotations, with hooks for your own training/classification code.
- **C++** — trains a linear (LDA) classifier on the pre-calculated features using the [Shark](http://shark-project.sourceforge.net/) machine learning library; used to generate the baseline results.
- **Python** — reads the training set and class IDs (depends on matplotlib).

### Result analysis application

A GPLv2-licensed desktop tool (Qt 4.7 / CMake) for comparing approaches, inspecting confusion matrices, and browsing misclassified images. Source code is available in the downloads below; it has mainly been tested on Windows/Visual Studio.

### Downloads

- **Dataset (images, features, ground truth):** [External hosting mirror](https://sid.erda.dk/public/archives/daaeac0d7ce1152aea9b61d9f1e19370/published-archive.html)
- **MATLAB code:** `GTSRB_Matlab_code.zip`
- **C++ code:** `GTSRB_CPP_code.zip`
- **Python code:** `GTSRB_Python_code.zip`
- **Result analysis app (source):** `tsr-analysis-src.zip`

*(Original download links pointed to `benchmark.ini.rub.de/Dataset/...`; update these to wherever you re-host the files.)*

### Citation

Please cite the following paper when using or referring to the GTSRB dataset:

> J. Stallkamp, M. Schlipsing, J. Salmen, and C. Igel. **The German Traffic Sign Recognition Benchmark: A multi-class classification competition.** In *Proceedings of the IEEE International Joint Conference on Neural Networks*, pages 1453–1460, 2011.

The full dataset and competition results are additionally described in:

> J. Stallkamp, M. Schlipsing, J. Salmen, C. Igel. **Man vs. computer: Benchmarking machine learning algorithms for traffic sign recognition.** *Neural Networks*, 2012. doi: [10.1016/j.neunet.2012.02.016](http://dx.doi.org/10.1016/j.neunet.2012.02.016)

```bibtex
@inproceedings{Stallkamp-IJCNN-2011,
    author = {Johannes Stallkamp and Marc Schlipsing and Jan Salmen and Christian Igel},
    booktitle = {IEEE International Joint Conference on Neural Networks},
    title = {The {G}erman {T}raffic {S}ign {R}ecognition {B}enchmark: A multi-class classification competition},
    year = {2011},
    pages = {1453--1460}
}

@article{Stallkamp2012,
    title = {Man vs. computer: Benchmarking machine learning algorithms for traffic sign recognition},
    journal = {Neural Networks},
    year = {2012},
    issn = {0893-6080},
    doi = {10.1016/j.neunet.2012.02.016},
    author = {J. Stallkamp and M. Schlipsing and J. Salmen and C. Igel}
}
```

### Final competition results (IJCNN 2011)

| Rank | Team | Representative | Method | Correct recognition rate |
|---|---|---|---|---|
| 1 | IDSIA | Dan Ciresan | Committee of CNNs | 99.46% |
| 2 | INI | — | Human performance | 98.84% |
| 3 | sermanet | Pierre Sermanet | Multi-scale CNNs | 98.31% |
| 4 | CAOR | Fatin Zaklouta | Random forests | 96.14% |

---

## About

Both benchmarks were compiled by the **Real-Time Computer Vision** research group at the **Institut für Neuroinformatik (INI)**, Ruhr-Universität Bochum. GTSRB was the subject of a competition at IJCNN 2011 (San Jose, CA); GTSDB was proposed for and presented at IJCNN 2013 (Dallas, TX).

## Acknowledgements

Both datasets were made possible with help from Lukas Caup, Sebastian Houben, Lukas Kubik, Bastian Petzka, Stefan Tenbült, and Marc Tschentscher (annotation support); Sebastian Houben (MATLAB code samples); Lukas Kubik and Bastian Petzka (original web site). Annotations were created with the *Advanced Development & Analysis Framework (ADAF)* provided by [Nisys GmbH](http://www.nisys.de/). The project was supported by Germany's Federal Ministry of Education and Research (BMBF).

## People / Contact

For questions or comments: **tsr-benchmark@ini.rub.de**

- **Johannes Stallkamp** — PhD student, Institut für Neuroinformatik, Real-Time Computer Vision group; research on computer vision for advanced driver assistance systems.
- **Marc Schlipsing** — PhD student, Real-Time Computer Vision group, Institut für Neuroinformatik.
- **Jan Salmen** — PhD student and (since 2009) group leader, Real-Time Computer Vision, Institut für Neuroinformatik.
- **Christian Igel** — Professor with special duties in Machine Learning, Department of Computer Science (DIKU), University of Copenhagen; formerly Juniorprofessor for Optimization of Adaptive Systems at INI.

---

## Selected news / history

A condensed timeline of major milestones from the original site (full historical news has been trimmed for this page):

- **2019-05-08** — Downloads moved to an external hosting service after high server load forced a temporary shutdown of the original download section.
- **2019-04-16** — Online submission system deactivated (low usage, high maintenance cost); previously submitted datasets, software, and results remain available.
- **2014-08-20** — Server migration completed.
- **2013-11-05** — GTSDB citation published.
- **2013-08-06** — GTSDB special session held at IJCNN 2013.
- **2013-03-01** — GTSDB submission phase closed; final results published.
- **2012-12-01** — GTSDB announced as the successor to GTSRB.
- **2012-03-16** — GTSRB journal paper ("Man vs. Computer") accepted in *Neural Networks*.
- **2011-08-03** — Final GTSRB competition results announced at IJCNN 2011.
- **2010-12-01** — GTSRB competition started; training data released.
- **2010-11-26** — Website opened.

---

*This page consolidates and replaces the original multi-page site at `benchmark.ini.rub.de`. Last content sync: August 2026, based on a site last modified 2019-05-10.*
