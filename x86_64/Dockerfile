FROM amd64/ubuntu:20.04
SHELL ["/bin/bash", "-c"]
USER root

# Setup system environment and required packages
ENV DEBIAN_FRONTEND=noninteractive 
RUN apt-get update && apt-get -y upgrade && apt-get -y install wget && apt-get install ffmpeg libsm6 libxext6 curl git-all -y
ENV PATH="/root/.local/bin:${PATH}"
WORKDIR /root

RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh && \
    chmod u+x Miniconda3-latest-Linux-x86_64.sh && \
    bash ./Miniconda3-latest-Linux-x86_64.sh -b && \
    rm ./Miniconda3-latest-Linux-x86_64.sh
ENV PATH="/root/miniconda3/bin/:${PATH}"

# install scallop
RUN mkdir /root/packages && \
    mkdir /root/packages/scallop && \
    mkdir /root/packages/scallop/bin && \
    mkdir /root/packages/scallop/lib && \
    mkdir /root/labs
ENV PATH="/root/packages/scallop/bin:${PATH}"

# Setup conda virtual environment for scallop
WORKDIR /root/packages/scallop/lib
ADD ./x86_64/scallopy-0.2.2-cp38-cp38-manylinux_2_31_x86_64.whl /root/packages/scallop/lib/scallopy-0.2.2-cp38-cp38-manylinux_2_31_x86_64.whl
ADD ./x86_64/scallop-0.2.2-py3-none-any.whl /root/packages/scallop/lib/scallop-0.2.2-py3-none-any.whl
ADD ./x86_64/scallopy_ext-0.2.2-py3-none-any.whl /root/packages/scallop/lib/scallopy_ext-0.2.2-py3-none-any.whl
ADD ./x86_64/scallop_clip-0.0.1-py3-none-any.whl /root/packages/scallop/lib/scallop_clip-0.0.1-py3-none-any.whl
ADD ./x86_64/scallop_face_detection-0.0.1-py3-none-any.whl /root/packages/scallop/lib/scallop_face_detection-0.0.1-py3-none-any.whl
ADD ./x86_64/scallop_gpt-0.0.1-py3-none-any.whl /root/packages/scallop/lib/scallop_gpt-0.0.1-py3-none-any.whl
ADD ./x86_64/scallop_gpu-0.0.1-py3-none-any.whl /root/packages/scallop/lib/scallop_gpu-0.0.1-py3-none-any.whl
ADD ./x86_64/scallop_opencv-0.0.1-py3-none-any.whl /root/packages/scallop/lib/scallop_opencv-0.0.1-py3-none-any.whl
ADD ./x86_64/scallop_transformers-0.0.1-py3-none-any.whl /root/packages/scallop/lib/scallop_transformers-0.0.1-py3-none-any.whl

RUN conda update -n base -c defaults conda
RUN source /root/miniconda3/etc/profile.d/conda.sh && \
    conda init bash && \
    . ~/.bashrc && \
    conda create --name scallop-env python=3.8 -y && \
    conda activate scallop-env && \
    conda install pytorch torchvision torchaudio cpuonly -c pytorch -y && \
    python -m pip install --upgrade pip && \
    python -m pip install ./scallopy-0.2.2-cp38-cp38-manylinux_2_31_x86_64.whl && \
    python -m pip install ./scallop-0.2.2-py3-none-any.whl && \
    python -m pip install ./scallopy_ext-0.2.2-py3-none-any.whl && \
    python -m pip install ./scallop_clip-0.0.1-py3-none-any.whl && \
    python -m pip install ./scallop_face_detection-0.0.1-py3-none-any.whl && \
    python -m pip install ./scallop_gpt-0.0.1-py3-none-any.whl && \
    python -m pip install ./scallop_gpu-0.0.1-py3-none-any.whl && \
    python -m pip install ./scallop_opencv-0.0.1-py3-none-any.whl && \
    python -m pip install ./scallop_transformers-0.0.1-py3-none-any.whl && \
    python -m pip install notebook && \
    python -m pip install ipywidgets && \
    python -m pip install tqdm && \
    python -m pip install matplotlib && \
    python -m pip install gym

RUN curl -L https://api.loke.aws.unit.no/dlr-gui-backend-resources-content/v2/contents/links/61be4ec7-8c11-4a4a-a9f4-827144e4ab4f0c2764c1-80a0-4083-bbfa-68419f889b80e4692358-979b-458e-97da-c1a1660b3314 -o WIDERFace_DSFD_RES152.pth
RUN mkdir -p /root/.cache/torch/hub/checkpoints && cp WIDERFace_DSFD_RES152.pth /root/.cache/torch/hub/checkpoints/

ADD ./labs /root/labs
ADD ./x86_64/scli /root/packages/scallop/bin/scli
ADD ./x86_64/sclrepl /root/packages/scallop/bin/sclrepl
WORKDIR /root/labs
