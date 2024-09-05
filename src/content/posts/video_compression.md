---
title: Video Compression Paper list
published: 2024-09-05
description: A list of video compression papers
tags: [VideoCompression]
category: Compression
draft: false
---

# LDP low delay P-frame coding


* Neural Video Codec
    * DCVC: [Deep Contextual Video Compression](https://proceedings.neurips.cc/paper/2021/file/96b250a90d3cf0868c83f8c965142d2a-Paper.pdf), NeurIPS 2021, in [this folder](./DCVC/).
    * DCVC-TCM: [**T**emporal **C**ontext **M**ining for Learned Video Compression](https://ieeexplore.ieee.org/document/9941493), in IEEE Transactions on Multimedia, and [arxiv](https://arxiv.org/abs/2111.13850), in [this folder](./DCVC-TCM/).
    * DCVC-HEM: [**H**ybrid Spatial-Temporal **E**ntropy **M**odelling for Neural Video Compression](https://arxiv.org/abs/2207.05894), ACM MM 2022, in [this folder](./DCVC-HEM/).
        -  The first end-to-end neural video codec to exceed H.266 (VTM) using the highest compression ratio configuration, in terms of both PSNR and MS-SSIM.
        -  The first end-to-end neural video codec to achieve rate adjustment in single model.
    * DCVC-DC: [Neural Video Compression with **D**iverse **C**ontexts](https://arxiv.org/abs/2302.14402), CVPR 2023, in [this folder](./DCVC-DC/).
        -  The first end-to-end neural video codec to exceed [ECM](https://jvet-experts.org/doc_end_user/documents/27_Teleconference/wg11/JVET-AA0006-v1.zip) using the highest compression ratio low delay configuration with a intra refresh period roughly to one second (32 frames), in terms of PSNR and MS-SSIM for RGB content.
        -  The first end-to-end neural video codec to exceed ECM using the highest compression ratio low delay configuration with a intra refresh period roughly to one second (32 frames), in terms of PSNR for YUV420 content.
    * DCVC-FM: [Neural Video Compression with **F**eature **M**odulation](https://arxiv.org/abs/2402.17414), CVPR 2024, in [this folder](./DCVC-FM/).
        -  The first end-to-end neural video codec to exceed ECM using the highest compression ratio low delay configuration with only one intra frame, in terms of PSNR for both YUV420 content and RGB content in a single model.
        -  The first end-to-end neural video codec that support a large quality and bitrate range in a single model.
* Neural Image Codec
    * [EVC: Towards Real-Time Neural Image Compression with Mask Decay](https://openreview.net/forum?id=XUxad2Gj40n), ICLR 2023, in [this folder](./EVC/).
