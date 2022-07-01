## CH1 Introduction

This chapter gives an introduction to digital signal processing and shows software implementations with the MATLAB programming tool.

---

### :heartpulse: classifications of digital audio effects

+ Digital implementation technique: in chronological order(时间顺序)

+ Processing domain:based on the domain where the signal processing is applied 
  
  + time domain
  
  + frequency domain
  
  + time and frequency domain

+ Applied processing

+ Control type

+ based on perceptual attributes(感知属性)
  
  + loudness：响度是声音在时间中的感知强度。通常使用一个名为分贝的对数尺度:响度是$L_{dB} = 20 log_{10}I$，其中$I$表示声强。在响度上加20分贝等价于将声强级乘以10。
  
  + time and rhythm
  
  + pitch:composed of height and chroma(色度)
  
  + spatial hearing(空间听觉)
  
  + timbre

+ Semantic descriptors

---

### :yellow_heart: simple basics of digital

+ digital signal
  
  + ADC(analog-to-digital):sampling, quantization, 采样率$f_{s}=1/T$，单位为HZ
  + DAC(digital-to-analog)
  + discrete-time axis，normalized discrete-time axis
  + block processing;sample by sample processing

+ spectrum analysis
  
  + discrete fourier transform(离散傅里叶变换)
  
  + Inverse discrete Fourier transform (IDFT)（反离散傅里叶变换）
  
  + Spectrogram

+ digital systems
