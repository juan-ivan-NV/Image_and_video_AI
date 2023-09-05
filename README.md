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

docker build -t sd_testx .
docker build -t sdtestx .

docker run --gpus all -p 8080:8080 sdtestx

docker run -it --gpus all -p 9080:7860 sdtestx

go inside the folder where volume folder is located.

docker container run -it -v C:/Users/coldc/Documents/github_jinb/testings/SD_datadir/volumen:/home/sduser/ -p 9080:7860 --gpus=all sdui


copy a model from pc host to the container

docker cp v2-1_768-nonema-pruned.ckpt 4794bf357665:app/stable-diffusion-webui/models/Stable-diffusion


launch 
http://localhost:8080/


issue on ui 

PermissionError: [Errno 13] Permission denied: 'outputs/txt2img-images'
https://github.com/AUTOMATIC1111/stable-diffusion-webui/issues


### to run with python
python3 launch.py 

### to run with on linux or inside a docker container
sudo bash webui.sh -f




Ignore everyone lmao. I HAVE A 1050 and can run 768z512
refer to https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Troubleshooting

You JUST HAVE TO DO THIS
Edit webui-user.bat
modify this line to
set COMMANDLINE_ARGS=--medvram


https://github.com/AUTOMATIC1111/stable-diffusion-webui/tree/master
https://github.com/AUTOMATIC1111/stable-diffusion-webui/issues/9093
https://gist.github.com/kalaspuffar/122ce8edf050b3471d3a53fa0c6f44a3
https://github.com/Vayioleta/DockerStableDiff-Eden/tree/main


Original image

<code>
FROM universonic/cuda:11.7.1-ubuntu2210-base

COPY entrypoint.sh /app/entrypoint.sh

RUN apt update && \ 
apt install -y python3 python3-pip python3-venv git wget libgl1-mesa-dev libglib2.0-0 libsm6 libxrender1 libxext6 && \ 
rm -rf /var/lib/apt/lists/* && \ 
groupadd -g 1000 sdgroup && \ 
useradd -m -s /bin/bash -u 1000 -g 1000 --home /app sduser && \ 
ln -s /app /home/sduser && \ 
chown -R sduser:sdgroup /app && \ 
chmod +x /app/entrypoint.sh 

USER sduser
WORKDIR /app

RUN git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui stable-diffusion-webui

VOLUME /app/stable-diffusion-webui/extensions
VOLUME /app/stable-diffusion-webui/models
VOLUME /app/stable-diffusion-webui/outputs
VOLUME /app/stable-diffusion-webui/localizations

EXPOSE 8080

ENV PYTORCH_CUDA_ALLOC_CONF=garbage_collection_threshold:0.9,max_split_size_mb:512

ENTRYPOINT ["/app/entrypoint.sh", "--update-check", "--xformers", "--listen", "--port", "8080"]
CMD ["--medvram"]
</code>




# Deep Fake

Testing colab

https://colab.research.google.com/drive/1d16nYI_1VVWaD9c5Wk4sr4VNwYJFyUy3?usp=sharing