---
title: 'LyNoS: automatic lymph node segmentation using deep learning'
colorFrom: indigo
colorTo: indigo
sdk: docker
app_port: 7860
emoji: 🫁
pinned: false
license: mit
app_file: demo/app.py
---

<div align="center">
<h1 align="center">🫁 LyNoS 🤗</h1>
<h3 align="center">A multilabel lymph node segmentation dataset from contrast CT</h3>

[![license](https://img.shields.io/github/license/DAVFoundation/captain-n3m0.svg?style=flat-square)](https://github.com/raidionics/LyNoS/blob/main/LICENSE.md)
[![CI/CD](https://github.com/raidionics/LyNoS/actions/workflows/deploy.yml/badge.svg)](https://github.com/raidionics/LyNoS/actions/workflows/deploy.yml)
<a target="_blank" href="https://huggingface.co/spaces/dbouget/LyNos"><img src="https://img.shields.io/badge/🤗%20Hugging%20Face-Spaces-yellow.svg"></a>
<a href="https://colab.research.google.com/gist/andreped/274bf953771059fd9537877404369bed/lynos-load-dataset-example.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>
[![paper](https://img.shields.io/badge/paper-pdf-D12424)](https://doi.org/10.1080/21681163.2022.2043778)

**LyNoS** was developed by SINTEF Medical Image Analysis to accelerate medical AI research.

</div>

## [Brief intro](https://github.com/raidionics/LyNoS#brief-intro)

This repository contains the LyNoS dataset described in ["_Mediastinal lymph nodes segmentation using 3D convolutional neural network ensembles and anatomical priors guiding_"](https://doi.org/10.1080/21681163.2022.2043778).
The dataset has now also been uploaded to Zenodo and the Hugging Face Hub enabling users to more easily access the data through Python API.

We have also developed a web demo to enable others to easily test the pretrained model presented in the paper. The application was developed using [Gradio](https://www.gradio.app) for the frontend and the segmentation is performed using the [Raidionics](https://raidionics.github.io/) backend.

## [Dataset](https://github.com/raidionics/LyNoS#data) <a href="https://colab.research.google.com/gist/andreped/274bf953771059fd9537877404369bed/lynos-load-dataset-example.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

### [Accessing dataset](https://github.com/raidionics/LyNoS#accessing-dataset)

The dataset contains 15 CTs with corresponding lymph nodes, azygos, esophagus, and subclavian carotid arteries manual annotations. The folder structure is described below.

The easiest way to access the data is through Python with Hugging Face's [datasets](https://pypi.org/project/datasets/) package:
```
from datasets import load_dataset

# downloads data from Zenodo through the Hugging Face hub
# - might take several minutes (~5 minutes in CoLab)
dataset = load_dataset("andreped/LyNoS")
print(dataset)

# list paths of all available patients and corresponding features (ct/lymphnodes/azygos/brachiocephalicveins/esophagus/subclaviancarotidarteries)
for d in dataset["test"]:
  print(d)
```

A detailed interactive demo on how to load and work with the data can be seen on CoLab. Click the CoLab badge <a href="https://colab.research.google.com/gist/andreped/274bf953771059fd9537877404369bed/lynos-load-dataset-example.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a> to see the notebook or alternatively click [here](https://github.com/raidionics/LyNoS/blob/main/notebooks/lynos-load-dataset-example.ipynb) to see it on GitHub.


### [Dataset structure](https://github.com/raidionics/LyNoS#dataset-structure)

```
└── LyNoS.zip
    ├── stations_sto.csv
    └──  LyNoS/
        ├── Pat1/
        │   ├── pat1_data.nii.gz
        │   ├── pat1_labels_Azygos.nii.gz
        │   ├── pat1_labels_Esophagus.nii.gz
        │   ├── pat1_labels_LymphNodes.nii.gz
        │   └── pat1_labels_SubCarArt.nii.gz
        ├── [...]
        └── Pat15/
            ├── pat15_data.nii.gz
            ├── pat15_labels_Azygos.nii.gz
            ├── pat15_labels_Esophagus.nii.gz
            ├── pat15_labels_LymphNodes.nii.gz
            └── pat15_labels_SubCarArt.nii.gz
```

### [Lymph nodes stations](https://github.com/raidionics/LyNoS#lymph-nodes-stations)
For each labelled lymph node in the dataset, the primary, secondary, and up to the tertiary station have been manually assigned according to the IASLC Lung Cancer Staging guidelines, and more specifically following the [2009 map](https://radiologyassistant.nl/chest/mediastinum/mediastinum-lymph-node-map).
The stations considered can be organized as follows:
```
├── Supraclavicular nodes (stations 1R and 1L)
├── Superior mediastinal nodes (stations 2-4)
│   ├── Upper paratracheal (stations 2R and 2L)
│   ├── Pre-vascular (stations 3aR and 3aL)
│   ├── Pre-vertebral (station 3P)
│   └── Lower paratracheal (stations 4R and 4L)
├── Aortic nodes (stations 5-6)
│   ├── Subaortic (station 5)
│   └── Para-aortic (station 6)
├── Inferior mediastinal nodes (stations 7-9)
│   ├── Subcarinal (stations 7R and 7L)
│   ├── Paraesophageal (stations 8R and 8L)
│   └── Pulmonary ligament (station 9)
└── Hilar, lobar, and (sub)segmental nodes (stations 10-14)
    ├── Hilar (stations 10R and 10L)
    ├── Interlobar middle-lower (stations 11R and 11L)
    ├── Lobar (stations 12R and 12L)
    ├── Segmental (stations 13R and 13L)
    └── Subsegmental (stations 14R and 14L)
```
### [NIH Dataset Completion](https://github.com/raidionics/LyNoS#nih-dataset-completion)
A larger dataset made of 90 patients featuring enlarged lymph nodes has also been made available by the National Institutes of Health, and is available for download on the official [web-page](https://wiki.cancerimagingarchive.net/pages/viewpage.action?pageId=19726546).
As a supplement to this dataset, lymph nodes segmentation masks have been refined for all patients and stations have been manually assigned to each, available [here](https://drive.google.com/uc?id=1iVCnZc1GHwtx9scyAXdANqz2HdQArTHn).    

## [Demo](https://github.com/raidionics/LyNoS#demo) <a target="_blank" href="https://huggingface.co/spaces/dbouget/LyNos"><img src="https://img.shields.io/badge/🤗%20Hugging%20Face-Spaces-yellow.svg"></a>

To access the live demo, click on the `Hugging Face` badge above. Below is a snapshot of the current state of the demo app.

<img width="1904" height="1050" alt="image" src="https://github.com/user-attachments/assets/c97adaa9-41f8-426c-84ca-54ab87fc9441" />

## [Continuous integration](https://github.com/raidionics/LyNoS#continuous-integration)

| Build Type | Status |
| - | - |
| **HF Deploy** | [![Deploy](https://github.com/raidionics/LyNoS/workflows/Deploy/badge.svg)](https://github.com/raidionics/LyNoS/actions) |
| **File size check** | [![Filesize](https://github.com/raidionics/LyNoS/workflows/Check%20file%20size/badge.svg)](https://github.com/raidionics/LyNoS/actions) |
| **Formatting check** | [![Filesize](https://github.com/raidionics/LyNoS/workflows/Linting/badge.svg)](https://github.com/raidionics/LyNoS/actions) |

## [Development](https://github.com/raidionics/LyNoS#development)

### [Docker](https://github.com/raidionics/LyNoS#docker)

Alternatively, you can deploy the software locally. Note that this is only relevant for development purposes. Simply dockerize the app and run it:

```
docker build -t lynos .
docker run -it -p 7860:7860 lynos
```

Then open `http://127.0.0.1:7860` in your favourite internet browser to view the demo.

### [Python](https://github.com/raidionics/LyNoS#python)

It is also possible to run the app locally without Docker. Just setup a virtual environment and run the app.
Note that the current working directory would need to be adjusted based on where `LyNoS` is located on disk.

```
git clone https://github.com/raidionics/LyNoS.git
cd LyNoS/

virtualenv -python3 venv --clear
source venv/bin/activate
pip install -r ./demo/requirements.txt

python demo/app.py --cwd ./
```

## [Citation](https://github.com/raidionics/LyNoS#citation)

If you found the dataset and/or web application relevant in your research, please cite the following reference:
```
@article{bouget2021mediastinal,
  author = {David Bouget and André Pedersen and Johanna Vanel and Haakon O. Leira and Thomas Langø},
  title = {Mediastinal lymph nodes segmentation using 3D convolutional neural network ensembles and anatomical priors guiding},
  journal = {Computer Methods in Biomechanics and Biomedical Engineering: Imaging \& Visualization},
  volume = {0},
  number = {0},
  pages = {1-15},
  year  = {2022},
  publisher = {Taylor & Francis},
  doi = {10.1080/21681163.2022.2043778},
  URL = {https://doi.org/10.1080/21681163.2022.2043778},
  eprint = {https://doi.org/10.1080/21681163.2022.2043778}
}
```

## [License](https://github.com/raidionics/LyNoS#license)

The code in this repository is released under [MIT license](https://github.com/raidionics/LyNoS/blob/main/LICENSE).
