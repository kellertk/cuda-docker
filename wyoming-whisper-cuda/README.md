Docker-only build for Home Assistant Wyoming Whisper add-on with CUDA support

Based on https://github.com/rhasspy/wyoming-addons

## Usage

```bash
docker build -t wyoming-whisper-cuda .
docker run -it -p 10300:10300 -v <data-dir>:/data --device nvidia.com/gpu=all \
  wyoming-whisper-cuda --model medium-int8 --language en --beam-size 5 \
  --device cuda
```
