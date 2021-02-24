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
3. Peak Cancellation technique
4. Refrerence  
[1] Hiten N. Mistry, 2006, "Implementation of a Peak Windowing Algorithm for Crest Factor Reduction in WCDMA", Master Thesis of Engineering, SIMON FRASER UNIVERSITY
[2]  
