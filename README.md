# crest_factor_reduction
This is an algorithm used to reduce the PAPR (Peak To Average Power Ratio) of the transmitted signals so that the power amplifier can operate more efficiently. In this project, THREE algorithms of Crest Factor Reduction technique are presented consisting of: Hard Clipper (HC-CFR), Peak Windowing (PW-CFR) and Peak Cancellation (PC-CFR)

# **Table of Contents**  
- [Hard Clipper Technique ](#Hard-Clipper-Technique)  
- [Peak Windowing Technique](#Peak-Windowing-Technique)  
- [Peak Cancellation Technique](#Peak-Cancellation-Technique)  

## **Hard Clipper Technique**  
The clipped signal is computed as follows: <img src="https://render.githubusercontent.com/render/math?math=x_{clip}\big(n\big) = x\big(n\big)c\big(n\big)">, in which, clipping function <img src="https://render.githubusercontent.com/render/math?math=c\big(n\big)"> is determined using a threshole <img src="https://render.githubusercontent.com/render/math?math=Th"> that is the target PAPR value and be depicted as belows:  
If <img src="https://render.githubusercontent.com/render/math?math=\big|x\big(n\big)\big| \geq Th">, then: <img src="https://render.githubusercontent.com/render/math?math=c\big(n\big)=\frac{Th}{x\big(n\big)}">  
If <img src="https://render.githubusercontent.com/render/math?math=\big|x\big(n\big)\big| < Th">, then: <img src="https://render.githubusercontent.com/render/math?math=c\big(n\big)=1">    
As a result, hard clipper technique can cause sharp corners in a clipped output signal, which leads to an unwanted out-of-band emission.  

![hard_clipper.jpg](/image/hc_cfr.jpg?raw=true) 

## **Peak Windowing Technique**  
To reduce unwanted out-of-band emission in the previous technique, the peak windowing algorithm [1] will replace the clipping coefficients <img src="https://render.githubusercontent.com/render/math?math=c\big(n\big)"> with <img src="https://render.githubusercontent.com/render/math?math=b\big(n\big)">, where: <img src="https://render.githubusercontent.com/render/math?math=b\big(n\big)=1-\sum_{k=-\infty}^{\infty}a_{k}w\big(n-k\big)"> in which, <img src="https://render.githubusercontent.com/render/math?math=w\big(n\big)"> is the windowing function (Blackman, Hamming, Hanning, etc) and <img src="https://render.githubusercontent.com/render/math?math=a_{k}"> is  weighting coefficient.  
To maintain a maximum allowed amplitude of <img src="https://render.githubusercontent.com/render/math?math=Th">, <img src="https://render.githubusercontent.com/render/math?math=b\big(n\big)"> can not greater than <img src="https://render.githubusercontent.com/render/math?math=c\big(n\big)">, it means that the inequality <img src="https://render.githubusercontent.com/render/math?math=1-\sum_{k=-\infty}^{\infty}a_{k}w\big(n-k\big) \leq c\big(n\big)"> must satisfy for all data samples.  
As a result, the sharp cornes are smoothed by windowing technique as in below figure, that leads to the decrease of unwanted out-of-band emission.  

![peak_windowing.jpg](/image/pw_cfr.jpg?raw=true)

## **Peak Cancellation Technique**  
Peak cancellation [2] is an algorithm to reduce the PAPR of a signal. Interestingly, it aims to strike a balance between the out-of-band emission and in-band waveform quality when compressing the signal to a target PAPR. Hence, unlike Hard Clipper and Peak Windowing, the quality of out-of-band and in-band of ouput signal with Peak Cancellation technique is so outstanding in comparation with the previous techniques. The block diagram of Peak Cancellation Technique is depicted in [2]:  

![peak_cancellation_structure.png](/image/pc_cfr_structure.png?raw=true) 

The peak detector block works on the signal magnitudes to produce a peak location indicator along with magnitude and phase information for each peak. The peak scaling block is designed to compensate the difference between the peak magnitudes and the clipping threshold. The magnitude difference is combined with the phase information to extract the complex weighting that is used to scale the cancellation pulse coefficients.  
CPG (Cancellation Pulse Generator) generates cancellation pulse that cancel only one peak at a given time. The length of the cancellation pulse (depending on signal bandwidth) combined with the number of CPGs determines the rate at which signal peaks can be cancelled.  
The allocator block assigns CPGs to incoming peaks. When a new peak is detected by peak detector block, the allocator assigns an idle CPG to the cancellation of that peak and the CPG is tagged that it is allocated. Once allocated, a CPG becomes unavailable for the length of the cancellation pulse. If all CPGs are busy when a new peak is detected, it will not be cancelled and wait to the next phase. In case having multiple of detected peaks, multiple iterations of the algorithm are necessary to eliminate the peaks that were not cancelled during the previous phases of the algorithm. The final step in the algorithm is to subtract the summation of the CPG outputs from a delayed version of the input signal.  
As a result, the sharp cornes are smoothed efficiently by peak cancellation technique as in the below figure and the good balance between the out-of-band emission and in-band waveform quality is observed. 

![peak_cancellation.jpg](/image/pc_cfr.jpg?raw=true) 

## **Reference**  
- [1] Hiten N. Mistry, 2006, "Implementation of a Peak Windowing Algorithm for Crest Factor Reduction in WCDMA", Master Thesis of Engineering, Simon Fraser University  
- [2] Xilinx, 2011, "DS846: LogiCORE IP Peak Cancellation Crest Factor Reduction v3.0", https://www.xilinx.com/Attachment/PC-CFR%20v3.0.pdf 
