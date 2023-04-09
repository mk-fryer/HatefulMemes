# Hateful Memes using MMF

The example tries to replicate the model developed in DrivenData's [blog post](https://www.drivendata.co/blog/hateful-memes-benchmark/) on the Hateful Memes.

## Colab Installation

```
from google.colab import drive
drive.mount('/content/gdrive/')
```

```
%cd /content/gdrive/MyDrive/hm_project
git clone https://github.com/mk-fryer/HatefulMemes
```

```
%cd /content/gdrive/MyDrive/hm_project/HatefulMemes
!pip install -r requirements.txt
```

## Prerequisites

Please follow prerequisites for the Hateful Memes dataset at [this link](https://fb.me/hm_prerequisites).

## Running (working on getting this to function properly...)

Run training with the following command on the Hateful Memes dataset:

```
!mmf_convert_hm --zip_file=../data.zip --bypass_checksum=1 --password={put_password_here}

%env MMF_USER_DIR="/content/gdrive/MyDrive/hm_project/hm_example_mmf"

mmf_run config="configs/experiments/defaults.yaml"  model=concat_vl dataset=hateful_memes training.num_workers=0
```

We set `training.num_workers=0` here to avoid memory leaks with fasttext.
Please follow [configuration](https://mmf.readthedocs.io/en/latest/notes/configuration_system.html) document to understand how to use MMF's configuration system to update parameters.

## Directory Structure

```
├── configs
│   ├── experiments
│   │   └── defaults.yaml
│   └── models
│       └── concat_vl.yaml
├── __init__.py
├── models
│   ├── concat_vl.py
├── processors
│   ├── processors.py
├── README.md
└── requirements.txt
```

Some notes:

1. Configs have been divided into `experiments` and `models` where experiments will contain training configs while models will contain model specific config we implmented.
2. `__init__.py` imports all of the relevant files so that MMF can find them. This is what `env.user_dir` actually looks for.
3. `models` directory contains our model implementation, in this case specifically `concat_vl`.
4. `processors` contains our project specific processors implementation, in this case, we implemented FastText processor for Sentence Vectors.

## Issues/Feedback/Questions

Please open up issues related to this repository directly on [MMF](https://github.com/facebookresearch/mmf/issues/new/choose).


