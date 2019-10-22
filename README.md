# cryptoHomework
CryptoHomework(PKUss)

# SM4可逆性证明
## 加密过程
### X<sub>i+4</sub> = X<sub>i</sub>	xor (X<sub>i+1</sub> xor X<sub>i+2</sub> xor X<sub>i+3</sub> xor rk<sub>i</sub>)
### 经过32轮加密后最终得到密文（X<sub>32</sub>,X<sub>33</sub>,X<sub>34</sub>,X<sub>35</sub>）
## 解密过程
### 将密文反序 (X<sub>35</sub>,X<sub>34</sub>,X<sub>33</sub>,X<sub>32</sub>)
### 则密文可表示为 (Y<sub>0</sub>,Y<sub>1</sub>,Y<sub>2</sub>,Y<sub>3</sub>)
### 利用归纳假设法
### 目前有 Y<sub>i</sub> = X<sub>35-i</sub>(32≤i≤35)
### 不妨假设Y<sub>i</sub> = X<sub>35-i</sub>
### 解密过程中轮秘钥序列与加密相反则
### Y<sub>4</sub> = Y<sub>0</sub> xor (Y<sub>1</sub> xor Y<sub>2</sub> xor Y<sub>3</sub> xor rk<sub>32</sub>)
### Y<sub>4</sub> = X<sub>35</sub> xor (X<sub>34</sub> xor X<sub>33</sub> xor X<sub>32</sub> xor rk<sub>31</sub>)
### 将X<sub>35</sub> = X<sub>31</sub> xor (X<sub>32</sub> xor X<sub>33</sub> xor X<sub>34</sub> xor rk<sub>31</sub>) 带入得
### Y<sub>4</sub> = X<sub>31</sub> xor (X<sub>32</sub> xor X<sub>33</sub> xor X<sub>34</sub> xor rk<sub>31</sub>) xor (X<sub>34</sub> xor X<sub>33</sub> xor X<sub>32</sub> xor rk<sub>31</sub>)
### 化简后得
### Y<sub>4</sub> = X<sub>31</sub>
### 证明Y<sub>i</sub> = X<sub>35-i</sub>成立
### 则sm4算法加密是可逆的

## 加密PKU logo
### 利用**gmssl**与**ImageMagic**加密pku logo
#### 查看图片信息
![image](https://github.com/agenthtb/cryptoHomework/blob/master/Image/pku.jpg)

`identify pku.jpg`

`pku.jpg JPEG 150x150 150x150+0+0 8-bit sRGB 10620B 0.000u 0:00.000`
#### 将图片由转为jpg转为rgba
`convert -depth 8 pku.jpg pku.rgba`

#### 利用gmssl加密图片(密码为1901210642)
`gmssl enc -sms4-ecb -e -in pku.rgba -out pku_ecb.rgba`
`gmssl enc -sms4-cbc -e -in pku.rgba -out pku_cbc.rgba`

#### 将加密后的rgba转为jpg1
`convert -size 150x150 -depth 8 pku_ecb.rgba pku_ecb.jpg`

![image](https://github.com/agenthtb/cryptoHomework/blob/master/Image/pku_ecb.jpg)

`convert -size 150x150 -depth 8 pku_cbc.rgba pku_cbc.jpg`

![image](https://github.com/agenthtb/cryptoHomework/blob/master/Image/pku_cbc.jpg)
