
# Speaker Extraction
Using Deep Learning to extract just the Primary speaker from a noisy audio file containing noise, music or even secondary speakers.  
## About
An implementation in PyTorch of [this](https://arxiv.org/abs/1810.04826) paper by good folks at
Google. I made some changes after weeks of trial and error, and am presenting
the results here.    
***Note***: Thanks to [this awesome github repo](https://github.com/mindslab-ai/voicefilter),
I was able to figure out how to do most of the things.  

## Results
Sadly, github markdown doesn't allow showing audio directly. Checkout [TODO](https://TODO) to view the results or
download the files directly from `res/input` and `res/output`. 

## Setup
### Data preparation  
From a corpus of ~700 files, ~400 were manually selected and the noise was removed using audacity. Also, ~200
from the original were selected and the noise extracted from them(noise includes human blabber, and weird
household noises). These are then randomly padded to ensure there's no the sounds don't unintentionally occupy
the beginning or the ending. Finally these are randomly mixed to prepare a 10000 sample final dataset.

### Model Architecture
Since the motive was to reduce the noise irrespective of the speaker, I've ditched the Embedder mentioned in
the paper. Even without the target speaker's embeddings, the Model works fairly well. This maybe due to the
randomisation in the data preparation step, or just dumb luck.  
The Extractor is the same model as mentioned in the paper: 6 CNNs, a bilinear LSTM, and 2 Fully connected Layers.
The output is a mask tensor which is applied on the original audio file to get the filtered audio. I tried to add
more CNNs, and adding residual-connections in between those, but the vanilla network seemed to perform better
anyways(No Losses to back me up here :P).
