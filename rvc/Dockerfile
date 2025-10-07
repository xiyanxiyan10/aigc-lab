FROM ubuntu:miniconda

RUN apt-get update -y && apt-get install git -y
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y -q\
    libsodium-dev \
    m4 \
    autoconf \
    openssh-server \
    libtool \
    vim    \
    pdsh   \
    git    \
    git-lfs \
    ninja-build \
    build-essential \
    libncurses5-dev \
    libgdbm-dev \
    libnss3-dev \
    libssl-dev \
    libreadline-dev \
    libffi-dev \
    zlib1g-dev \
    libsqlite3-dev \
    libaio-dev  \
    iputils-ping \
    curl \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update -y && apt-get install ffmpeg aria2 wget git -y
RUN cd /root && git clone https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI.git
RUN cd /root/Retrieval-based-Voice-Conversion-WebUI && conda create -n rvc-webui python=3.8 && conda init && . /root/.bashrc && conda activate rvc-webui && pip install torch torchvision torchaudio
RUN cd /root/Retrieval-based-Voice-Conversion-WebUI && conda init && . /root/.bashrc && conda activate rvc-webui && pip install "pip<24" && pip install -r requirements.txt && pip install gradio==3.48.0
RUN cd /root/Retrieval-based-Voice-Conversion-WebUI && conda init && . /root/.bashrc && conda activate rvc-webui && pip install demucs

RUN aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/lj1995/VoiceConversionWebUI/resolve/main/hubert_base.pt -d assets/hubert -o hubert_base.pt
RUN aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/lj1995/VoiceConversionWebUI/resolve/main/rmvpe.pt -d assets/rmvpe -o rmvpe.pt
