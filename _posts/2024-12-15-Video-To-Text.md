---
title: Video To Text
commentable: true
Edit: 2024-12-15
mathjax: true
mermaid: true
tags: python
categories: Computer-Science
description: Use Python and the iFLYTEK API to convert MP4 video files into TXT text files.
---
To convert video files into text files, there are two steps to finish to achieve the goal.

1. Convert videos into audio.
2. Call the iFLYTEK API to achieve the conversion from audio to text.

# MP4 To MP3

```python
from moviepy import AudioFileClip

my=AudioFileClip("myvideo.mp4") # 你的视频地址
my.write_audiofile("my.mp3") # 设置生成的音频
```

# MP3 To TXT

After converting the video into audio, we will then continue to complete the conversion of audio into text. Here, we will utilize the [iFLYTEK](https://www.xfyun.cn/?ch=bd05-105&bd_vid=11434242351308717943) API. 