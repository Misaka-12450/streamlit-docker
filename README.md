# streamlit-docker

A Dockerfile to help builda Streamlit container image based on [the official guide](https://docs.streamlit.io/deploy/tutorials/docker), with Python `requirements.txt` support. The image will always run `pip install -r requirements.txt` on startup to ensure that requirements are up to date.

## Build

### Multiarch
```sh
docker buildx build \
  --platform linux/amd64,linux/arm64 \
  -t misaka-12450/streamlit-docker:latest \
  --push .
```

### x86-64
```sh
docker buildx build \
  --platform linux/amd64 \
  -t misaka-12450/streamlit-docker:latest \
  --push .
```

### arm64
```sh
docker buildx build \
  --platform linux/arm64 \
  -t misaka-12450/streamlit-docker:latest \
  --push .
```

## Use

Streamlit files are mounted in `/app` of the container.

### Docker Compose
```yaml
services:
  streamlit:
    image: misaka-12450/streamlit:latest
    ports:
      - '8501:8501'
    volumes:
      - 'app:/app'
    restart: unless-stopped

volumes:
  app:
```

Remember to upload your Streamlit files and `requirements.txt` to `/app`. On Linux, the Docker volume may be located in `/var/lib/docker/volumes`.
