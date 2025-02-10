---
license: mit
tags:
- vocoder
- audio
- speech
- tts
---

# Model Card for Model ID

[HuggingFace 🤗 - Repository](https://huggingface.co/Respair/HiFormer_Vocoder) (Please Check HuggingFace, I often update there + the checkpoints I train)

**DDP is very un-stable, please use the single-gpu training script** - if you still want to do it, I suggest uncommenting the grad clipping lines; that should help a lot.

This Vocoder, is a combination of [HiFTnet](https://github.com/yl4579/HiFTNet) and [Ringformer](https://github.com/seongho608/RingFormer). it supports Ring Attention, Conformer and Neural Source Filtering etc.
This repository is experimental, expect some bugs and some hardcoded params.

The default setting is 44.1khz - 128 Mel bins. but I have provided the necessary script for the 24khz version in the LibriTTS checkpoint's folder.

Huge Thanks to [Johnathan Duering](https://github.com/duerig) for his help. I mostly implemented this based on his [STTS2 Fork](https://github.com/duerig/StyleTTS2/tree/main).


**NOTE**: 

There are Three checkpoints available so far where you can grab them from 🤗:
  - HiFormer 24khz (trained for roughly 117K~ steps on LibriTTS (360 + 100) and 40 hours of other English datasets.)
  - HiFormer 44.1khz (trained for roughly 280K~ steps on a Large (more than 1100 hours) private Multilingual dataset, covering Arabic, Persian, Japanese, English, Russian and also Singing voice in Chinese and Japanese with Quranic recitations in Arabic. **This is the best checkpoint available so far.**
  - HiFTNet 44.1khz (trained for ~100K steps, on a similar dataset to HiFormer 44.1khz, but slightly smaller and no singing voice.) to use this Checkpoint you should head to the [HiFTNet's repository](https://github.com/yl4579/HiFTNet).

Ideally I wanted to train them all up to 1M steps, but I don't think I can do that for a while. so, while the quality should be reasonably good, you may still want to fine-tune them on your downstream task.

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
## Training
```bash
CUDA_VISIBLE_DEVICES=0 python train_single_gpu.py --config config_v1.json --[args]
```
For the F0 model training, please refer to [yl4579/PitchExtractor](https://github.com/yl4579/PitchExtractor). This repo includes a pre-trained F0 model on a Mixture of Multilingual data for the previously mentioned configuration. I'm going to quote the HiFTnet's Author: "Still, you may want to train your own F0 model for the best performance, particularly for noisy or non-speech data, as we found that F0 estimation accuracy is essential for the vocoder performance." 

## Inference
Please refer to the notebook [inference.ipynb](https://github.com/Respaired/HiFormer_Vocoder/blob/main/RingFormer/inference.ipynb) for details.
