# <p align="center">Probabilistic Encounter Modeling for PFM‑1 Landmine Detection: A Comparative Benchmark of Hypergeometric Risk Models, SAM/ACE Detectors, and Kriging‑Enhanced Soft Classification</p>

<p align="center">
  <a href="https://arxiv.org/abs/2602.10434"><img src="https://img.shields.io/badge/Paper-IGARSS%202026-blue" alt="Paper"></a>
  <a href="https://huggingface.co/datasets/SagarLekhak/pfm1-landmine-uav-vnir-hsi-IGARSS-2026"><img src="https://img.shields.io/badge/Dataset-UAV%20Hyperspectral-green" alt="Dataset"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License: MIT"></a>
</p>

This repository contains the code and annotations for our SSRN paper on **"Stochastic modeling of pfm1 landmine encounters: comparative assessment of hypergeometric risk models and SAM/ACE detectors in UAV imagery"** by [Sumanta Kumar Das](https://scholar.google.com/citations?user=Mkf-WgsAAAAJ&hl=en), [Prasanna Reddy Pulakurthi](https://www.prasannapulakurthi.com/), [Ramesh Bhatta](https://scholar.google.com/citations?user=O7m5LxEAAAAJ&hl=en), and [Emmett J. Ientilucci](https://www.rit.edu/directory/ejipci-emmett-ientilucci).


## Dataset Description

This dataset [1](#ref1) contains Visible and Near-Infrared (VNIR) Hyperspectral Imaging (HSI) data prepared for the IEEE International Geoscience and Remote Sensing Symposium (IGARSS) 2026.

This specific version is a refined subset of the original benchmark dataset [2](#ref2). While the original release provided full radiance cubes, broad GCP/AeroPoint data, and reference ground spectra of all the targets, this version focuses on a spatially subsetted region containing only PFM-1 landmine targets and includes high-accuracy, pixel-wise binary ground truth masks.

The data was collected over a controlled test field seeded with 143 realistic surrogate landmine and UXO targets (surface, partially buried, and fully buried). Data acquisition was performed using a Headwall Nano-Hyperspec® sensor mounted on a multi-sensor UAV platform flown at an altitude of ~20.6 m [2](#ref2).

For more details regarding data acquisition and preprocessing, go to the original paper [2](#ref2).

- **Sensor:** [Headwall Nano-Hyperspec®]
- **Spectral Range:** [398–1002 nm]
- **Number of Bands:** [270 bands]
- **Approximate GSD:** [Approx. 1.29 cm]


## Installation

### Setup

```bash
# Clone the repository
git clone https://github.com/PrasannaPulakurthi/pfm1-hsi-benchmark.git
cd pfm1-hsi-benchmark

# Create a virtual environment
python -m venv .venv
source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

## Usage

### Download the Dataset
```python
from huggingface_hub import snapshot_download

snapshot_download(repo_id="SagarLekhak/pfm1-landmine-uav-vnir-hsi-IGARSS-2026", repo_type="dataset", local_dir="./data")
```
 
### Run Classical Detection Methods

```bash
# Full Region evaluation
jupyter notebook Full_Region.ipynb

# PFM-1 Region evaluation
jupyter notebook PFM-1_Region.ipynb

# Independent Test Region evaluation
jupyter notebook FL_Test_Region.ipynb
```

### Data Visualization

```bash
jupyter notebook Visualize_Data.ipynb
```

Visualize the hyperspectral dataset, ground truth masks, and spectral signatures.

## Results

### Performance Summary (Test Region)

| Method      | Average Precision (AP) | ROC-AUC |
|-------------|------------------------|---------|
| SAM         | 0.144                 | 0.797   |
| MF          | 0.358                 | 0.982   |
| ACE         | **0.691**             | **0.989** |
| CEM         | 0.589                 | 0.983   |
| **Spectral-NN** | **0.814**         | 0.982   |

### Key Findings

1. **ROC-AUC alone is misleading**: All methods achieve high AUC (>0.98) but vastly different precision-recall performance
2. **Spectral-NN achieves best AP**: Outperforms all classical methods with AP=0.814
3. **Scene composition matters**: Performance varies significantly between Full Region, PFM-1 Region, and Test Region
4. **Precision-focused evaluation is critical**: For rare-target detection with extreme class imbalance

### Precision-Recall Curves

![PR Curves](assets/pr_curve.jpg)

*Precision-Recall curves*

### ROC Curves

![ROC Log Scale](assets/roc_results.jpg)

*Log-scale ROC curves revealing Spectral-NN's superior performance at operationally critical low false-positive rates*


## Citation
If you use this dataset, please cite the specific IGARSS 2026 work [1](#ref1) and the original benchmark [2](#ref2):

<a name="ref1"></a>
**[1] IGARSS 2026 Work:**
```bibtex
@misc{lekhak2026benchmarkingdeeplearningstatistical,
      title={Benchmarking Deep Learning and Statistical Target Detection Methods for PFM-1 Landmine Detection in UAV Hyperspectral Imagery}, 
      author={Sagar Lekhak and Prasanna Reddy Pulakurthi and Ramesh Bhatta and Emmett J. Ientilucci},
      year={2026},
      eprint={2602.10434},
      archivePrefix={arXiv},
      primaryClass={eess.IV},
      url={https://arxiv.org/abs/2602.10434}, 
}
```

<a name="ref2"></a>
**[2] Original Benchmark Dataset:**
```bibtex
@misc{lekhak2026uavbasedvnirhyperspectralbenchmark,
      title={A UAV-Based VNIR Hyperspectral Benchmark Dataset for Landmine and UXO Detection}, 
      author={Sagar Lekhak and Emmett J. Ientilucci and Jasper Baur and Susmita Ghosh},
      year={2026},
      eprint={2510.02700},
      archivePrefix={arXiv},
      primaryClass={eess.IV},
      url={https://arxiv.org/abs/2510.02700}, 
}
```
## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
