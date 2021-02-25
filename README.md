# crest_factor_reduction
This is an algorithm used to reduce the PAPR (Peak To Average Power Ratio) of the transmitted signals so that the power amplifier can operate more efficiently. In this project, THREE algorithms of Crest Factor Reduction technique are presented consisting of: Hard Clipper (HC-CFR), Peak Windowing (PW-CFR) and Peak Cancellation (PC-CFR)

# **Table of Contents**  
- [Hard Clipper Technique ](#Hard-Clipper-Technique)  
- [Peak Windowing Technique](#Peak-Windowing-Technique)  
- [Peak Cancellation Technique](#Peak-Cancellation-Technique)  

## **Hard Clipper Technique**  
The clipped signal is computed as follows: ![x_{clip}\big(n\big)=x\big(n\big)c\big(n\big)](https://latex.codecogs.com/svg.latex?&space;x_{clip}\big(n\big)=x\big(n\big)c\big(n\big))  
in which, clipping function ![c\big(n\big)](https://latex.codecogs.com/svg.latex?&space;c\big(n\big)) is determined using a threshole ![Th](https://latex.codecogs.com/svg.latex?&space;Th) that is the target PAPR value and be depicted as belows:  
If ![|x\big(n\big)|>=Th](https://latex.codecogs.com/svg.latex?&space;|x\big(n\big)|>=Th), then: ![c\big(n\big)=\frac{Th}{|x\big(n\big)|}](https://latex.codecogs.com/svg.latex?&space;c\big(n\big)=\frac{Th}{|x\big(n\big)|})  
If ![|x\big(n\big)|<Th](https://latex.codecogs.com/svg.latex?&space;|x\big(n\big)|<Th), then: ![c\big(n\big)=1](https://latex.codecogs.com/svg.latex?&space;c\big(n\big)=1)  
As a result, hard clipper technique can cause sharp corners in a clipped output signal, which leads to an unwanted out-of-band emission.  
![hard_clipper.jpg](/image/hc_cfr.jpg?raw=true) 

## **Peak Windowing Technique**  
To reduce unwanted out-of-band emission in the previous technique, the peak windowing algorithm [1] will replace the clipping coefficients ![c\big(n\big)](https://latex.codecogs.com/svg.latex?&space;c\big(n\big)) with ![b\big(n\big)](https://latex.codecogs.com/svg.latex?&space;b\big(n\big)), where:  
![b\big(n\big)=1-\sum_{k=-\infty}^{\infty}a_{k}w\big(n-k\big)](https://latex.codecogs.com/svg.latex?&space;b\big(n\big)=1-\sum_{k=-\infty}^{\infty}a_{k}w\big(n-k\big))  
in which, ![w\big(n\big)](https://latex.codecogs.com/svg.latex?&space;w\big(n\big)) is the windowing function (Blackman, Hamming, Hanning, etc) and ![a_{k}](https://latex.codecogs.com/svg.latex?&space;a_{k}) is  weighting coefficient.  
To maintain a maximum allowed amplitude of ![Th](https://latex.codecogs.com/svg.latex?&space;Th), ![b\big(n\big)](https://latex.codecogs.com/svg.latex?&space;b\big(n\big)) can not greater than ![c\big(n\big)](https://latex.codecogs.com/svg.latex?&space;c\big(n\big)), it means that the inequality ![1-\sum_{k=-\infty}^{\infty}a_{k}w\big(n-k\big)<=c\big(n\big)](https://latex.codecogs.com/svg.latex?&space;1-\sum_{k=-\infty}^{\infty}a_{k}w\big(n-k\big)<=c\big(n\big)) must satisfy for all data samples.  
As a result, the sharp cornes are smoothed by windowing technique as in below figure, that leads to the decrease of unwanted out-of-band emission.  
![peak_windowing.jpg](/image/pw_cfr.jpg?raw=true)

## **Peak Cancellation Technique**  
Peak cancellation [2] is an algorithm to reduce the PAPR of a signal. Interestingly, it aims to strike a balance between the out-of-band emission and in-band waveform quality when compressing the signal to a target PAPR. Hence, unlike Hard Clipper and Peak Windowing, the quality of out-of-band and in-band of ouput signal with Peak Cancellation technique is so outstanding in comparation with the previous techniques. The block diagram of Peak Cancellation Technique is depicted in [2]:  

![peak_cancellation_structure.png](/image/pc_cfr_structure.png?raw=true) 

The peak detector block works on the signal magnitudes to produce a peak location indicator along with magnitude and phase information for each peak. The peak scaling block is designed to compensate the difference between the peak magnitudes and the clipping threshold. The magnitude difference is combined with the phase information to extract the complex weighting that is used to scale the cancellation pulse coefficients.  
CPG (Cancellation Pulse Generator) generates cancellation pulse that cancel only one peak at a given time. The length of the cancellation pulse (depending on signal bandwidth) combined with the number of CPGs determines the rate at which signal peaks can be cancelled.  
The allocator block assigns CPGs to incoming peaks. When a new peak is detected by peak detector block, the allocator assigns an idle CPG to the cancellation of that peak and the CPG is tagged that it is allocated. Once allocated, a CPG becomes unavailable for the length of the cancellation pulse. If all CPGs are busy when a new peak is detected, it will not be cancelled and wait to the next phase. In case having multiple of detected peaks, multiple iterations of the algorithm are necessary to eliminate the peaks that were not cancelled during the previous phases of the algorithm. The final step in the algorithm is to subtract the summation of the CPG outputs from a delayed version of the input signal.

![peak_cancellation.jpg](/image/pc_cfr.jpg?raw=true) 

## **Reference**  
- [1] Hiten N. Mistry, 2006, "Implementation of a Peak Windowing Algorithm for Crest Factor Reduction in WCDMA", Master Thesis of Engineering, SIMON FRASER UNIVERSITY  
- [2] Xilinx, 2011, "DS846: LogiCORE IP Peak CancellationCrest Factor Reduction v3.0", https://www.xilinx.com/Attachment/PC-CFR%20v3.0.pdf 
