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
<h3 align="center">A lymph node segmentation dataset from contrast CT</h3>

[![license](https://img.shields.io/github/license/DAVFoundation/captain-n3m0.svg?style=flat-square)](https://github.com/raidionics/LyNoS/blob/main/LICENSE.md)
[![CI/CD](https://github.com/raidionics/LyNoS/actions/workflows/deploy.yml/badge.svg)](https://github.com/raidionics/LyNoS/actions/workflows/deploy.yml)
<a target="_blank" href="https://huggingface.co/spaces/andreped/LyNoS"><img src="https://img.shields.io/badge/🤗%20Hugging%20Face-Spaces-yellow.svg"></a>
[![paper](https://img.shields.io/badge/paper-pdf-D12424)](https://doi.org/10.1080/21681163.2022.2043778)

**LyNoS** was developed by SINTEF Medical Image Analysis to accelerate medical AI research.

</div>

## [Brief intro](https://github.com/raidionics/LyNoS#brief-intro)

This repository contains the LyNoS dataset described in ["_Mediastinal lymph nodes segmentation using 3D convolutional neural network ensembles and anatomical priors guiding_"](https://doi.org/10.1080/21681163.2022.2043778). The original pretrained model was made openly available [here](https://github.com/dbouget/ct_mediastinal_structures_segmentation). However, we have gone ahead and made a web demonstration to more easily test the pretrained model. The application was developed using [Gradio](https://www.gradio.app) for the frontend and the segmentation is performed using the [Raidionics](https://raidionics.github.io/) backend.

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
docker build -t LyNoS .
docker run -it -p 7860:7860 LyNoS
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

The code in this repository is released under [MIT license](https://github.com/raidionics/LyNoS/blob/main/LICENSE.md).
