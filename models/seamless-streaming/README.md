---
license: cc-by-nc-4.0
inference: False
tags:
  - audio-to-audio
  - text-to-speech
library_name: seamless_communication
language:
- af
- am
- ar
- as
- az
- be
- bn
- bs
- bg
- ca
- cs
- zh
- cy
- da
- de
- el
- en
- et
- fi
- fr
- or
- om
- ga
- gl
- gu
- ha
- he
- hi
- hr
- hu
- hy
- ig
- id
- is
- it
- jv
- ja
- kn
- ka
- kk
- mn
- km
- ky
- ko
- lo
- ln
- lt
- lb
- lg
- lv
- ml
- mr
- mk
- mt
- mi
- my
- nl
- nb
- ne
- ny
- oc
- pa
- ps
- fa
- pl
- pt
- ro
- ru
- sk
- sl
- sn
- sd
- so
- es
- sr
- sv
- sw
- ta
- te
- tg
- tl
- th
- tr
- uk
- ur
- uz
- vi
- wo
- xh
- yo
- ms
- zu
- ary
- arz
- yue
- kea
---

# SeamlessStreaming
SeamlessStreaming is a multilingual streaming translation model. It supports:

- Streaming Automatic Speech Recognition on 96 languages.
- Simultaneous translation on 101 source languages for speech input.
- Simultaneous translation on 96 target languages for text output.
- Simultaneous translation on 36 target languages for speech output.

![SeamlessStreaming architecture](streaming_arch.png)

## SeamlessStreaming  models
| Model Name         | #params | checkpoint                                                                              | metrics                                                                              |
| ------------------ | ------- | --------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| SeamlessStreaming  | 2.5B    | [🤗 Model card](https://huggingface.co/facebook/seamless-streaming) - [monotonic decoder checkpoint](https://huggingface.co/facebook/seamless-streaming/resolve/main/seamless_streaming_monotonic_decoder.pt) - [streaming UnitY2 checkpoint](https://huggingface.co/facebook/seamless-streaming/resolve/main/seamless_streaming_unity.pt)  | [metrics](https://dl.fbaipublicfiles.com/seamless/metrics/streaming/seamless_streaming.zip)  |

The evaluation data ids for FLEURS, CoVoST2 and CVSS-C can be found [here](https://dl.fbaipublicfiles.com/seamless/metrics/evaluation_data_ids.zip)


## Evaluating SeamlessStreaming models
To reproduce our results, or to evaluate using the same metrics over your own test sets, please check out the [Evaluation README here](../../src/seamless_communication/cli/streaming/README.md). Streaming evaluation depends on the SimulEval library.

## Seamless Streaming demo

### Running on HF spaces
You can simply duplicate the space to run it. [🤗 HF Space](https://huggingface.co/spaces/facebook/seamless-streaming)

## Running locally

### Install backend seamless_server dependencies

> [!NOTE]
> Please note: we *do not* recommend running the model on CPU. CPU inference will be slow and introduce noticable delays in the simultaneous translation.

> [!NOTE]
> The example below is for PyTorch stable (2.1.1) and variant cu118. 
> Check [here](https://pytorch.org/get-started/locally/) to find the torch/torchaudio command for your variant. 
> Check [here](https://github.com/facebookresearch/fairseq2#variants) to find the fairseq2 command for your variant.

If running for the first time, create conda environment and install the desired torch version. Then install the rest of the requirements:
```
cd seamless_server
conda create --yes --name smlss_server python=3.8 libsndfile==1.0.31
conda activate smlss_server
conda install --yes pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia
pip install fairseq2 --pre --extra-index-url https://fair.pkg.atmeta.com/fairseq2/whl/nightly/pt2.1.1/cu118
pip install -r requirements.txt
```

### Install frontend streaming-react-app dependencies
```
conda install -c conda-forge nodejs
cd streaming-react-app
npm install --global yarn
yarn
yarn build  # this will create the dist/ folder
```


### Running the server

The server can be run locally with uvicorn below.
Run the server in dev mode:

```
cd seamless_server
uvicorn app_pubsub:app --reload --host localhost
```

Run the server in prod mode:

```
cd seamless_server
uvicorn app_pubsub:app --host 0.0.0.0
```

To enable additional logging from uvicorn pass `--log-level debug` or `--log-level trace`.


### Debuging

If you enable "Server Debug Flag" when starting streaming from the client, this enables extensive debug logging and it saves audio files in /debug folder. 

## Citation

For EMMA, please cite :
```bibtex
@article{ma_efficient_2023,
  author={Ma, Xutai and Sun, Anna and Ouyang, Siqi and Inaguma, Hirofumi and Tomasello, Paden},
  title={Efficient Monotonic Multihead Attention},
  year={2023},
  url={https://ai.meta.com/research/publications/efficient-monotonic-multihead-attention/},
}
```

For SeamlessStreaming, please cite :
```bibtex
@inproceedings{seamless2023,
   title="Seamless: Multilingual Expressive and Streaming Speech Translation",
   author="{Seamless Communication}, Lo{\"i}c Barrault, Yu-An Chung, Mariano Coria Meglioli, David Dale, Ning Dong, Mark Duppenthaler, Paul-Ambroise Duquenne, Brian Ellis, Hady Elsahar, Justin Haaheim, John Hoffman, Min-Jae Hwang, Hirofumi Inaguma, Christopher Klaiber, Ilia Kulikov, Pengwei Li, Daniel Licht, Jean Maillard, Ruslan Mavlyutov, Alice Rakotoarison, Kaushik Ram Sadagopan, Abinesh Ramakrishnan, Tuan Tran, Guillaume Wenzek, Yilin Yang, Ethan Ye, Ivan Evtimov, Pierre Fernandez, Cynthia Gao, Prangthip Hansanti, Elahe Kalbassi, Amanda Kallet, Artyom Kozhevnikov, Gabriel Mejia, Robin San Roman, Christophe Touret, Corinne Wong, Carleigh Wood, Bokai Yu, Pierre Andrews, Can Balioglu, Peng-Jen Chen, Marta R. Costa-juss{\`a}, Maha Elbayad, Hongyu Gong, Francisco Guzm{\'a}n, Kevin Heffernan, Somya Jain, Justine Kao, Ann Lee, Xutai Ma, Alex Mourachko, Benjamin Peloquin, Juan Pino, Sravya Popuri, Christophe Ropers, Safiyyah Saleem, Holger Schwenk, Anna Sun, Paden Tomasello, Changhan Wang, Jeff Wang, Skyler Wang, Mary Williamson",
  journal={ArXiv},
  year={2023}
}
```

