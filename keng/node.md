## 2019-8-31

q: request 传的content-length，和实际计算的content-length不符，会导致请求失败。
r: 解决办法: content-length设置为空，或者先剔除再重新计算。
