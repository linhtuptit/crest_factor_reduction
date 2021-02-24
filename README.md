# crest_factor_reduction
This is an algorithm used to reduce the PAPR (Peak To Average Power Ratio) of the transmitted signals so that the power amplifier can operate more efficiently. In this project, THREE algorithms of Crest Factor Reduction technique are presented consisting of: Hard Clipper (HC-CFR), Peak Windowing (PW-CFR) and Peak Cancellation (PC-CFR)
1. Hard Clipper technique  
The clipped signal is computed as follows: ![x_{clip}\big(n\big)=x\big(n\big)c\big(n\big)](https://latex.codecogs.com/svg.latex?&space;x_{clip}\big(n\big)=x\big(n\big)c\big(n\big))  
in which, clipping function ![c\big(n\big)](https://latex.codecogs.com/svg.latex?&space;c\big(n\big)) is determined using a threshole ![Th](https://latex.codecogs.com/svg.latex?&space;Th) that is the target PAPR value and be depicted as belows:  
If ![|x\big(n\big)|>=Th](https://latex.codecogs.com/svg.latex?&space;|x\big(n\big)|>=Th), then: ![c\big(n\big)=\frac{Th}{|x\big(n\big)|}](https://latex.codecogs.com/svg.latex?&space;c\big(n\big)=\frac{Th}{|x\big(n\big)|})  
If ![|x\big(n\big)|<Th](https://latex.codecogs.com/svg.latex?&space;|x\big(n\big)|<Th), then: ![c\big(n\big)=1](https://latex.codecogs.com/svg.latex?&space;c\big(n\big)=1)  
As a result, hard clipper technique can cause sharp corners in a clipped output signal, which leads to an unwanted out-of-band emission.  
![hard_clipper.png](/image/pending.jpeg?raw=true) 
2. Peak Windowing technique [1]  
To reduce unwanted out-of-band emission in the previous technique, the peak windowing algorithm will replace the clipping coefficients ![c\big(n\big)](https://latex.codecogs.com/svg.latex?&space;c\big(n\big)) with ![b\big(n\big)](https://latex.codecogs.com/svg.latex?&space;b\big(n\big)), where: ![b\big(n\big)=1-\sum_{k=-\infty}^{\infty}a_{k}w\big(n-k\big)](https://latex.codecogs.com/svg.latex?&space;b\big(n\big)=1-\sum_{k=-\infty}^{\infty}a_{k}w\big(n-k\big)), in which, ![w\big(n\big)](https://latex.codecogs.com/svg.latex?&space;w\big(n\big)) is the windowing function (Blackman, Hamming, Hanning, etc) and ![a_{k}](https://latex.codecogs.com/svg.latex?&space;a_{k}) is  weighting coefficient.  
To maintain a maximum allowed amplitude of ![Th](https://latex.codecogs.com/svg.latex?&space;Th), ![b\big(n\big)](https://latex.codecogs.com/svg.latex?&space;b\big(n\big)) can not greater than ![c\big(n\big)](https://latex.codecogs.com/svg.latex?&space;c\big(n\big)), it means that the inequality ![1-\sum_{k=-\infty}^{\infty}a_{k}w\big(n-k\big)<=c\big(n\big)](https://latex.codecogs.com/svg.latex?&space;1-\sum_{k=-\infty}^{\infty}a_{k}w\big(n-k\big)<=c\big(n\big)) must satisfy for all data samples.  
3. Peak Cancellation technique
4. Refrerence  
[1] Hiten N. Mistry, 2006, "Implementation of a Peak Windowing Algorithm for Crest Factor Reduction in WCDMA", Master Thesis of Engineering, SIMON FRASER UNIVERSITY
[2]  
