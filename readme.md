# ResCapsGuard | Res2TCNGuard

This repository provides a code for training and evaluating audio anti-spoofing systems ResCapsGuard and Res2TCNGuard proposed in 'Capsule-based and TCN-based approaches for spoofing detection in voice biometry'



### Data preparation
We train/validate/evaluate models using the ASVspoof 2019 logical access dataset [1].

Manual preparation is available via 
- ASVspoof2019 dataset: https://datashare.ed.ac.uk/handle/10283/3336
  1. Download `LA.zip` and unzip it
  2. Set your dataset and labels directories in the corresponding variables `train_path_flac`(`dev_path_flac`,`eval_path_flac`) and `train_label_path`(`dev_label_path`,`eval_label_path`)

### Training 
To train new model we provide [train.py](https://github.com/wh1t3tea/anti-spoof/blob/main/train.py):
```bash
git clone https://github.com/wh1t3tea/anti-spoof
cd anti-spoof

pip install requirements.txt

python train.py configs/config_res2tcnguard.json
```

### Pre-trained model

We provide models checkpoints:

| Model            | Config                                                                                                        | Weights                                                                                     |EER | t-DCF|
|------------------|---------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|--- |--|
| __Res2TCNGuard__ | [config_res2tcnguard.json](https://github.com/wh1t3tea/anti-spoof/blob/main/configs/config_res2tcnguard.json) | [__Res2TCNGuard__](https://github.com/wh1t3tea/anti-spoof/blob/main/weights/best_1.495.pth) |1.49|0.0451|
| __ResCapsGuard__ | [config_rescapsguard.json](https://github.com/wh1t3tea/anti-spoof/blob/main/configs/config_rescapsguard.json) | [__ResCapsGuard__](https://github.com/wh1t3tea/anti-spoof/blob/main/weights/new_capsules_changed_sinc_layer.pth) |2.25|0.0744|

### Evaluation
To evaluate pre-trained models on eval set of ASVspoof 2019 follow:

```bash
python eval.py \
--config configs/config_res2tcnguard.json \ 
--eval_label_path ../LA/ASVspoof2019_LA_cm_protocols/ASVspoof2019.LA.cm.eval.trl.txt \
--eval_path_flac ..LA/ASVspoof2019_LA_eval
```



### License
```
MIT License

Copyright (c) 2024 MTUCI 

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

### Acknowledgements
This repository is built on top of several open source projects. 
- [min t-DCF implementation](https://www.asvspoof.org/resources/tDCF_python_v2.zip)

The dataset we use is ASVspoof 2019 [1]
- https://www.asvspoof.org/index2019.html

### References
[1] ASVspoof 2019: A large-scale public database of synthesized, converted and replayed speech
```bibtex
@article{wang2020asvspoof,
  title={ASVspoof 2019: A large-scale public database of synthesized, converted and replayed speech},
  author={Wang, Xin and Yamagishi, Junichi and Todisco, Massimiliano and Delgado, H{\'e}ctor and Nautsch, Andreas and Evans, Nicholas and Sahidullah, Md and Vestman, Ville and Kinnunen, Tomi and Lee, Kong Aik and others},
  journal={Computer Speech \& Language},
  volume={64},
  pages={101114},
  year={2020},
  publisher={Elsevier}
}
```