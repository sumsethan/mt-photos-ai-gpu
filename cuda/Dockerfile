FROM nvidia/cuda:11.7.1-cudnn8-devel-ubuntu22.04
#FROM tensorflow/tensorflow:2.12.0-gpu
USER root
# 镜像加速
#COPY cuda/sources.list /etc/apt/sources.list
RUN apt update && \
    apt install -y wget libgl1-mesa-glx libglib2.0-0 libsm6 libxrender1 libfontconfig  python3 pip && \
    wget http://nz2.archive.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.1_1.1.1f-1ubuntu2.22_amd64.deb && \
    dpkg -i libssl1.1_1.1.1f-1ubuntu2.22_amd64.deb && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/log/*
# 如果 libssl1.1_1.1.1f-1ubuntu2.22_amd64.deb 404 not found
# 请打开 http://nz2.archive.ubuntu.com/ubuntu/pool/main/o/openssl/ 查找 libssl1.1_1.1.1f-1ubuntu2.22_amd64.deb 对应的新版本
WORKDIR /app

COPY cuda/requirements.txt .

# 安装依赖包
RUN python3 -m pip install paddlepaddle-gpu==2.5.1.post112 -f https://www.paddlepaddle.org.cn/whl/linux/cudnnin/stable.html
RUN pip3 install --no-cache-dir -r requirements.txt
COPY cuda/server.py .

ENV API_AUTH_KEY=mt_photos_ai_extra
ENV CLIP_MODEL=ViT-B-16
EXPOSE 8000

CMD [ "python3", "/app/server.py" ]
