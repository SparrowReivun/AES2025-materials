# A Scalable Two-Stage Automatic Mixing System

This repository contains the source code for **Stage 1**,auto level balance of the "Scalable Two-Stage Automatic Mixing System," as presented at **AES 2025**.

The system addresses the scalability bottleneck in Deep Learning (DL) mixing. While end-to-end DL models often fail on real-world sessions (60–100+ tracks), our hybrid approach combines robust signal processing with neural style transfer to achieve high-fidelity mixes at scale with unlimited number of un-predefined track.

## 🔗 Quick Links & Resources

  * **📄 Presentation Slides:** [AES LA Slides (PDF)](https://github.com/user-attachments/files/23107900/A.Scalable.Two-Stage.Automatic.Mixing.System_AES_LA.pdf)
  * **🎧 Subjective Listening Test:**
      * [English Version](https://golisten.ucd.ie/task/mushra-test/664270ad552c347eae0085d1)
      * [Chinese Version](https://golisten.ucd.ie/task/mushra-test/66570ca6552c347eae008736)
  * **🤖 Stage 1 System - Rule-Based Intra-Group Level Balancing:** this repo.
  * **🤖 Stage 2 System - DL-based Inter-Group Audio Mixing:** [Diff-MST GitHub Repository](https://github.com/sai-soum/Diff-MST?tab=readme-ov-file)
  * **💾 Audio Examples (coming soon):** [Zenodo Archive](https://doi.org/10.5281/zenodo.17171082)

-----

## 💡 The Core Concept

Our pipeline decomposes the mixing task into two distinct stages to maximize robustness and artistic flexibility.

### Stage 1: Intra-Group Level Balancing (This Repo)

**The Problem:** Standard loudness metrics (like ITU-R BS.1770 / LUFS) often fail when applied to individual, narrowband instrument tracks (e.g., Hi-hats, Bass), resulting in perceptual imbalances.
**The Solution:** We implement a **Rule-Based System** that:

1.  Extracts pitch ($f_0$) using an ensemble of **PYIN** and **PESTO**.
2.  Calculates **Spectral Centroid** and **Bandwidth**.
3.  Applies dynamic bandpass filtering based on these features *before* measuring loudness.
4.  Balances tracks into cohesive stems (subgroups) ready for style transfer.

### Stage 2: Inter-Group Style Transfer for Audio Mixing
To resolve the recent scarcity of robust, open-source DL mixing architectures (before this paper is accepted), we integrate **Diff-MST** (ISMIR 2024) as our second stage. This framework processes the spectrally balanced stems from Stage 1 to finalize the audio mixing, potentially in specified artistic character.

* **Architecture:** A Transformer-based controller that predicts parameters for Differentiable Signal Processing (DSP) modules, specifically Equalization (EQ), Compression, and Panning.
* **Reference-Guided Control:** The model applies processing to stems based on a target reference track. For this study, we utilized high-fidelity Rock recordings from the **Cambridge-MT dataset** as style references.
* **Evaluation:** Our subjective listening tests benchmarked this 2-stage hybrid system directly against human expert mixes within the same musical genre.


-----

## 🛠️ Usage

### 1\. Prerequisites

The code relies on several signal processing and machine learning libraries.

```bash
pip install -r requirements.txt
```

### 2\. Data Preparation

Your data should be organized by project folders. Each folder should contain the raw `.wav` stems.

**Directory Structure Example:**

```text
/Users/username/AES2025-materials/data/
├── Allegria_MendelssohnMovement1_STEMS/   # Subfolder 1, as an example
│   ├── violin1.wav
│   ├── cello.wav
│   └── ...
├── song2_STEMS/  # Subfolder 2
│   ├── vocal.wav
│   └── ...
```

### 3\. Running the Code

1.  Open `src/sparrow5.4-pesto.py`.

2.  Modify the `total_path` variable at the bottom of the script to match your local data directory:

    ```python
    if __name__ == '__main__':
        total_path = r'/Users/your_username/path/to/data' # Update this path
    ```

3.  Run the script:

    ```bash
    python src/sparrow5.4-pesto.py
    ```

-----

## 📊 Outputs & Methodology

The script processes every subfolder in the target path and generates three variations of mixed stems for comparison:

| Output Folder | Methodology | Description |
| :--- | :--- | :--- |
| **`output/p_lufs`** | **Proposed Method** | **Narrowband Loudness:** Uses $f_0$ and Centroid-informed filtering to match perceptual loudness. Recommended for Stage 2 input. |
| `output//lufs` | Baseline | **Fullband LUFS:** Standard integrated loudness matching. |
| `output//centroid` | Experimental | **Centroid Adjustment:** Gain balancing based purely on spectral energy distribution. |

**Analysis Data:**
The system also outputs `results.json` and `results.csv` containing extracted features ($f_0$, spectral bandwidth, applied gain) for further analysis.

-----

## 📝 Abstract

> Automatic mixing research has evolved from knowledge-engineering to data-driven deep learning. However, scalability remains a major hurdle; most DL models cannot handle real-world projects with 30-100+ tracks. We propose a scalable two-stage architecture. Stage 1 utilizes a refined rule-based level balancing system incorporating spectral centroid and fundamental frequency features to handle intra-group balancing. Stage 2 employs a differentiable mixing style transfer model. Subjective listening tests demonstrate that our approach consistently outperforms LUFS-based baselines and allows deep learning models to successfully mix projects with over 100 tracks, surpassing traditional rule-based systems.

-----

## 📚 Citation

If you utilize this code or methodology, please reference the AES 2025 paper:

```bibtex
@inproceedings{shi2025scalable,
  title     = {A Scalable Two-Stage Automatic Mixing System Integrating Machine Learning and Domain Knowledge},
  author    = {Shi, Jinjie and Xie, Kunzhu and Ma, Yinghao and Reiss, Joshua},
  booktitle = {Audio Engineering Society Convention 159},
  month     = {October},
  year      = {2025},
  url       = {https://aes2.org/publications/elibrary-page/?id=23076},
  number    = {10232}
}
```
