# YUV Video Compression and Layered Encoding with FFmpeg and H.264/AVC

This repository contains the fourth lab assignment for the **Multimedia Information Systems** course, completed by **Eray Samet Gündüz**. The project explores video compression techniques using **FFmpeg** and **H.264/AVC encoding**, focusing on different resolutions, CRF values, and single vs. multi-layer encoding configurations.

## Objective

The primary goal of this project is to understand how compression factors such as resolution, CRF (Constant Rate Factor), and encoder layers affect video quality and file size.

## Tools Used

- **FFmpeg**: For converting and compressing raw YUV video (`kendo0.yuv`)
- **H.264/AVC Encoder (JM Reference Software)**: For single-layer and double-layer encoding experiments

## Project Steps

### 1. Raw YUV Compression Using FFmpeg

Two CRF settings were applied at 1080p:

```bash
ffmpeg -s 1920x1080 -i kendo0.yuv -r 30 -s 1920x1080 -c:v libx264 -preset slow -crf 23 kendo0_1080.mp4
ffmpeg -s 1920x1080 -i kendo0.yuv -r 30 -s 1920x1080 -c:v libx264 -preset slow -crf 30 kendo0_1080_q30.mp4
```

Key observations:
- Lower CRF values yield higher visual quality but larger file sizes.
- Increasing CRF from 23 to 30 significantly reduced file size with visible quality degradation.

The same process was repeated for 720p resolution, further reducing file sizes, but with more noticeable visual quality loss compared to 1080p.

### 2. Single and Double Layer Encoding with H.264/AVC

Using the H.264/AVC JM encoder:
- Two configuration files were prepared:
  - `encoder_single.cfg` for single-layer encoding
  - `encoder_double.cfg` for double-layer encoding

Encoding commands used:

```bash
H264AVCENCODERLibTestStatic -pf encoder_single.cfg
H264AVCENCODERLibTestStatic -pf encoder_double.cfg
```

The output showed:
- Single-layer encoding produced the smallest file size but with lower quality.
- Double-layer encoding increased file size but retained more detail across layers.

## Results Summary

| Encoding Type     | CRF | Resolution | Output Quality | File Size Impact |
|-------------------|-----|------------|----------------|------------------|
| FFmpeg CRF 23     | 23  | 1080p      | High           | Large            |
| FFmpeg CRF 30     | 30  | 1080p      | Moderate       | Smaller          |
| FFmpeg CRF 30     | 30  | 720p       | Lower          | Very Small       |
| H.264 Single-Layer| —   | —          | Lowest         | Smallest         |
| H.264 Double-Layer| —   | —          | Higher         | Larger           |

## Conclusion

This project demonstrates how various compression settings and encoder configurations impact video fidelity and size. It also provides hands-on experience with both practical tools (FFmpeg) and academic encoding frameworks (H.264 JM Encoder).