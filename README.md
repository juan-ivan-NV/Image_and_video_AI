# Image_and_video_AI
Repo made to storage and test technologies like stable diffusion, deep fake...


Stable Diffusion web UI

►  <a href = "https://hub.docker.com/r/universonic/stable-diffusion-webui">Private Docker image</a> of stable-diffusion-webui for NVIDIA GPUs.

  
## Source 1

https://github.com/AbdBarho/stable-diffusion-webui-docker

Tested but container only working with SD version 1.5 only

Documented issue <a href = "https://github.com/AbdBarho/stable-diffusion-webui-docker/discussions/454
"> here. </a>

<code>
docker compose --profile [ui] up --build
for example:
docker compose --profile invoke up --build
or
docker compose --profile auto up --build
</code>

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

Again not working due SD models

## Testing previos image form scratch

https://github.com/universonic/docker-stable-diffusion-webui

docker build -t sd_testx .
docker build -t sdtestx .

docker run --gpus all -p 8080:8080 sdtestx



copy a model from pc host to the container

docker cp v2-1_768-nonema-pruned.ckpt 4794bf357665:app/stable-diffusion-webui/models/Stable-diffusion


sudo python3 launch.py
http://localhost:8080/


issue on ui 

PermissionError: [Errno 13] Permission denied: 'outputs/txt2img-images'
https://github.com/AUTOMATIC1111/stable-diffusion-webui/issues