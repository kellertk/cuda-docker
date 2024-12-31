Docker-only build for Home Assistant Wyoming Whisper add-on with CUDA support

Based on https://github.com/rhasspy/wyoming-addons

## Usage

```bash
docker build -t wyoming-whisper-cuda .
docker run -it -p 10300:10300 -v <data-dir>:/data --device nvidia.com/gpu=all \
  wyoming-whisper-cuda --model medium-int8 --language en --beam-size 5 \
  --device cuda
```

There's also a `.container` file for use with [podman](https://podman.io/).
Place it in `/etc/containers/systemd`, which should give you a
`wyoming-whisper.service` for systemd.
