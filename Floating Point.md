# Floating Point

## 1. Scientific Notation

### 1.1 Translating To and From SN

-  For positive ,shift the decimal to the right 
  $$
  1.011_{2}*2^4=>10110_{2}=22_{10}
  $$

- For negative,shift the decimal to the left
  $$
  1.011_{2}*2^{-2}=>0.01011_{2}=0.34375_{10}
  $$
  

## 2.IEEE Floating Point Standard

### 2.1 Goals

- Help programmer with *errors* in real arithmetic
  - +∞，-∞,NaN,+/- 0

### 2.2 Encoding: Single Precision

### 2.2.1 Scientific->IEEE Floating Point

- split a 32-bit into 3 fields 
  $$
  (-1)^{\rm\textcolor{orange}{Sign}}*\,1.\rm\textcolor{red}{Sinificand}_{two}*2^{\textcolor{blue}{Exponent}_{two}}
  $$
  

 | Sign | Exponent | Significand |
 | :-: | :---: | :--: |
 | 1bit |  8bits   |   23bits    |

$$
\rm{Ex:}\textcolor{orange}{0}\textcolor{blue}{011\,1111\,1}\textcolor{red}{100\,0000\,0000\,0000\,0000\,0000}_{2}
$$



### 2.2.2 The Exponent Field

- Biased Notation

  - We Don't like -1 looks bigger than 0 in 2's complement
    $$
    -1_{10}=11111111_{2}\\
    0_{10}=00000000_{2}
    $$

  - Use biased notation with bias of *-127*
    $$
    \rm{Exponent\,Field}:0(00000000_{2})\,to \,255(11111111_{2})\\
    \rm{Actual\,exponent}:-127(00000000_{2})\,to \,128(11111111_{2})
    $$

### 2.2.3 The Significand Field

- For
    $$
    1.\rm\textcolor{red}{Significand}=1+\rm\textcolor{red}{Value\,of\,significand}
    $$

- Node that all significand represents decimal numbers
  $$
  \rm{Ex:}\textcolor{orange}{0}\textcolor{blue}{011\,1111\,1}\textcolor{red}{100\,0000\,0000\,0000\,0000\,0000}_{2}\\
  =(-1)^\textcolor{orange}{0}*(1.\textcolor{red}{1}_{2})*2^{(\textcolor{blue}{127}-127)}
  $$
  

## 3 Floating Point Special Cases

| Exponent | Significand |     Meaning      |
| :------: | :---------: | :--------------: |
|    0     |      0      |       +-0        |
|    0     |  non-zero   | +- denorm  fl.pt |
|  1~254   |  anything   |     +-fl.pt      |
|   255    |      0      |       +-∞        |
|   255    |  non-zero   |      +-NaN       |

- Denormalized numbers
  - the gap between 0 and biggest decimal number is 
    $$
    \mathop{1}\limits_{the\,implicit\,1}.\textcolor{red}{00..00}_{2}*2^{(\textcolor{blue}{1}-127)}=2^{-126}
    $$
  
  - in order to represent the numbers between the gap,we **take out the implicit 1**

## 4.Floating Point Limitations

- Overflow : exponent is larger than can be represented
- Underflow: Negative exponent is larger than can be represented
- 
