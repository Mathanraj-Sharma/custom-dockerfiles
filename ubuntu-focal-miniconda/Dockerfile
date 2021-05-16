FROM ubuntu

# environment variables for conda installation
ENV PATH="/root/miniconda3/bin:${PATH}"
ARG PATH="/root/miniconda3/bin:${PATH}"

# get environment.yml file from --build-args and download to docker image
ARG environment
ADD $environment ./

RUN apt update

RUN apt install -y software-properties-common

RUN add-apt-repository universe \
	&& add-apt-repository multiverse

RUN apt install -y wget && rm -rf /var/lib/apt/lists/*

RUN apt update

RUN apt install -y make 

# download and install Miniconda
RUN wget \
    https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh \
    && mkdir /root/.conda \
    && bash Miniconda3-latest-Linux-x86_64.sh -b \
    && rm -f Miniconda3-latest-Linux-x86_64.sh 

# create tf-gpu environment
RUN conda env create -f $environment

# config conda 
RUN conda init bash \
	&& conda config --set auto_activate_base false \
	&& echo "conda activate tf-gpu" >> ~/.bashrc

# install git
RUN apt install -y git

