## CH7 Time-frequency processing

A digital audio effect based on time-frequency representations requires three steps: an **analysis** (sound to representation), a **transformation** (of the representation) and a **resynthesis** (getting back to a sound).

<img src="file:///C:/Users/wang/AppData/Roaming/marktext/images/2022-07-02-11-19-48-image.png" title="" alt="" data-align="center">

---

#### Phase vocoder basics

+ Filter bank summation model（滤波组求和）：
  
  + 通过一簇等宽、中心频率从0~fs/2的带通滤波器将信号分割成一个个频段的“单频”信号，然后进行处理，最后叠加还原。

+ block-by-block analysis/synthesis model(逐块分析/综合模型)
  
  + 通过逐步步进的方式，重叠地从原始信号中取出 Analysis_block，步进长度为analysis len。之后对Analysis block中的信号进行FFT变换至频域，在频域中对频域信息(幅值、相位)按需求进行处理(Processing)，最后通过IFFT还原频域信号至时域，并进行综合相加(Synthesis and overlap)，得出Synthesis block。同样的，综合相加也有步进长度，为Synthesis len。
    

---

#### Phase vocoder implementations

+ filter bank approach

+ Direct FFT/IFFT approach

+ FFT analysis/sum of sinusoids approach

+ Gaboret approach

---

#### Phase vocoder effects

+ Time-frequency filtering（时频滤波）
  
  + fast convolution

+ Dispersion（频散）

+ Time stretching（时间拉伸）
  
  + **first way**: model a sound by the sum of sinusoids, expand the amplitude and frequency functions
  
  + **second way**: uses the sliding Fourier transform as the model for resynthesis:  spread the image of a sliding FFT over time and calculate new phases, then reconstruct a new sound with the help of inverse FFTs

+ Pitch shifting(音高修改)

+ Stable/transient components separation（稳定/瞬态组件分离）

+ Mutation between two sounds（两个声音之间的突变）

+ Robotization（自动化）

+ Whisperization（耳语）

+ Denoising（去噪）

+ Spectral panning（光谱平移）
