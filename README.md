# Image_and_video_AI
Repo made to storage and test technologies like stable diffusion, deep fake...


Stable Diffusion web UI

►  <a href = "https://hub.docker.com/r/universonic/stable-diffusion-webui">Private Docker image</a> of stable-diffusion-webui for NVIDIA GPUs.

  
## Source 1

https://github.com/AbdBarho/stable-diffusion-webui-docker

Tested but container only working with SD version 1.5 only

Documented issue <a href = "https://github.com/AbdBarho/stable-diffusion-webui-docker/discussions/454
"> here. </a>

## source 2 testing docker image

https://hub.docker.com/r/universonic/stable-diffusion-webui


docker pull universonic/stable-diffusion-webui

docker run --gpus all --restart unless-stopped -p 8080:8080 -v /SD_datadir/extensions:/app/stable-diffusion-webui/extensions -v /SD_datadir/models:/app/stable-diffusion-webui/models -v /SD_datadir/outputs:/app/stable-diffusion-webui/outputs -v /SD_datadir/localizations:/app/stable-diffusion-webui/localizations --name stable-diffusion-webui -d universonic/stable-diffusion-webui

Directory schema

SD_datadir
    extensions
    models
    outputs
    localizations