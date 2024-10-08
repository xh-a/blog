---
title: 用C++实现算数编码
published: 2024-09-27
description: "如何用c++实现算数编码并使用压缩pytorch的整数参数"
#image: "./cover.jpeg"
tags: ["Arithmetic Coding"]
category: Compression
draft: false
---

## 浮点误差

$ \frac{x-0.5+\mu}{\sigma} \neq \frac{x+1+\mu-0.5}{\sigma} $
所以一开始分low和high来分别计算cdf的上界和下界


## 保证cdf每个区间的长度大于等于1

对于cdf这个离散累积函数来说，如果要对每个区间都加上1，可以直接加上一个累计序列：
```c++
cdf[0] += 0
cdf[1] += 1
....
cdf[n] += n
```
就能保证每个区间的长度都大于等于1，且对概率分布影响非常小

## 整数存储区间L,R

```c++

void ArithmeticCoderBase::update(uint32_t total, uint32_t symLow, uint32_t symHigh){

	uint64_t range = high - low + 1;
	uint64_t newLow  = low + symLow  * range / total;
	uint64_t newHigh = low + symHigh * range / total - 1;
	low = newLow;
	high = newHigh;
    
    # 将最高位相同的bit位移出
	while (((low ^ high) & halfRange) == 0) {
		shift();
		low  = ((low  << 1) & stateMask);
		high = ((high << 1) & stateMask) | 1;
	}
    
    # 可能是用来保证数字之差大于quaterRange+2
	while ((low & ~high & quarterRange) != 0) {
		underflow();
		low = (low << 1) ^ halfRange;
		high = ((high ^ halfRange) << 1) | halfRange | 1;
	}
}

```



## 可能存在的bug
### torchjpeg.codec 需要对输入的tensor加入continuous
笔者在使用torchjpeg的时候，会出现dct完全正确的情况下，转化为jpeg图片出现解码完全不是同一张图片的情况，原因竟然是在torchjpeg.codec需要提前对输入的数据加入continuous，可能c在访问变量的时候，要求存储是连续的吧


### hyper目前存在的问题
存储quantized_cdf表格，目前把scale设置了-100,100, 如果出现超过这个范围的数字就会导致编解码失败。同时这个范围过大，如果同时也存储cdf表的话，会导致模型文件过大。

### malloc分配内存来代理 io写入
存在着爆内存的风险



