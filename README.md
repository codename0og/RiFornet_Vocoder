---
license: mit
tags:
- vocoder
- audio
- speech
- tts
---

# Model Card for Model ID

[HuggingFace 🤗 - Repository](https://huggingface.co/Respair/HiFormer_Vocoder)

**DDP is very un-stable, please use the single-gpu training script** - if you still want to do it, I suggest uncommenting the grad clippimng lines; that should help a lot.

This Vocoder, is a combination of [HiFTnet](https://github.com/yl4579/HiFTNet) and [Ringformer](https://github.com/seongho608/RingFormer). it supports Ring Attention, Conformer and Neural Source Filtering etc.
This repository is experimental, expect some bugs and some hardcoded params.

The default setting is 44.1khz - 128 Mel bins. if you want to change it to 24khz, copy the config from HiFTnet (make sure to copy its pitch extractor, both the model + the checkpoint.), then change 128 to 80 in LN-384 of the models.py. then uncomment the "multiscale_subband_cfg" for the 24khz version.

Huge Thanks to [Johnathan Duering](https://github.com/duerig) for his help. I mostly implemented this based on his [STTS2 Fork](https://github.com/duerig/StyleTTS2/tree/main).

**This is highly experimental, I have not conducted a full session training. I just tested that the loss goes down and the eval samples sound reasonable for ~10K steps of minimal training.**


## Pre-requisites
1. Python >= 3.10
2. Clone this repository:
```bash
git clone https://github.com/Respaired/HiFormer_Vocoder
cd HiFormer_Vocoder/Ringformer
```
3. Install python requirements: 
```bash
pip install -r requirements.txt
```

## Training
```bash
CUDA_VISIBLE_DEVICES=0 python train_single_gpu.py --config config_v1.json --[args]
```
For the F0 model training, please refer to [yl4579/PitchExtractor](https://github.com/yl4579/PitchExtractor). This repo includes a pre-trained F0 model on a Mixture of Multilingual data for the previously mentioned configuration. I'm going to quote the HiFTnet's Author: "Still, you may want to train your own F0 model for the best performance, particularly for noisy or non-speech data, as we found that F0 estimation accuracy is essential for the vocoder performance." 

## Inference
Please refer to the notebook [inference.ipynb](https://github.com/Respaired/HiFormer_Vocoder/blob/main/RingFormer/inference.ipynb) for details.
