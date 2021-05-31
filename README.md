# Blood-pressure-estimation
Blood pressure estimation with PPG signal. 

목표 : 
1. AAMI standard 를 만족하는 모델 학습 (Mean error 5 mmHg, standard deviation 8mmHg 이하)
2. Transfer learning 

## Dataset 

MIMIC-III 
https://mimic.physionet.org/

MIMIC -II
https://archive.ics.uci.edu/ml/datasets/Cuff-Less+Blood+Pressure+Estimation

## Preprocessing 

PPG, ABP : 30s epoch
SBP = max(ABP)
DBP = min(ABP)

PPG signal

![image](https://user-images.githubusercontent.com/24654400/120130146-6aa63c80-c200-11eb-8b4b-2547eb26baec.png)
![image](https://user-images.githubusercontent.com/24654400/120130165-74c83b00-c200-11eb-93cb-27c742e5d434.png)

Butterworth band-pass filter(0.5 ~ 10Hz) 적용 

Blood pressure가 너무 높거나 너무 낮은 subject 제외 (diastolic < 30 mmHg or > 120 mmHg, systolic < 55 mmHg or > 185 mmHg)



---
### 1. Spectrogram method
Reference : Schlesinger, Oded, et al. "Estimation and Tracking of Blood Pressure Using Routinely Acquired Photoplethysmographic Signals and Deep Neural Networks." Critical Care Explorations 2.4 (2020).

논문에서 사용한 방법: 
Short-time Fourier transform (STFT) of sub-windows of length 6 seconds with a Hamming window and with 95% of overlap between adjacent sub-windows.


![image](https://user-images.githubusercontent.com/24654400/120131020-7135b380-c202-11eb-9bf9-d81066fc04a5.png)

2. PPG derivative
* 적용 예정 

## Models

2D-CNN 기반 regrssion model 

Tensorflow version (2.5.0)

GCP AI platform 사용 
GPU : NVIDIA Tesla T4

* Vertex AI (사용 예정) 

## Training 

![image](https://user-images.githubusercontent.com/24654400/120137487-62093280-c20f-11eb-9da2-9eaca0b86d41.png)

Model summary:


논문에서 사용한 모델 구현 

![image](https://user-images.githubusercontent.com/24654400/120137717-dfcd3e00-c20f-11eb-8cad-80fcad471f2e.png)


![image](https://user-images.githubusercontent.com/24654400/120140052-ac40e280-c214-11eb-93a8-c601e87183c5.png)

--> 학습이 잘되지 않음, 원인 분석 필요


## TO DO) 
Preprocessing 단계에서 calibration, current 잘 나뉘었는지 확인

Input pipeline 확인


## Evaluation 


"Google supported this work by providing Google Cloud credit"

