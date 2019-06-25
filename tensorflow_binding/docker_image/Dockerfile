FROM nvidia/cuda:10.0-cudnn7-devel-ubuntu18.04

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y git cmake python3 python3-pip

RUN pip3 install -U pip
RUN pip install tensorflow-gpu==1.13.1

ENV CUDA_HOME /usr/local/cuda
ENV LD_LIBRARY_PATH $LD_LIBRARY_PATH:/usr/local/cuda/extras/CUPTI/lib64:/usr/local/cuda/compat/:/usr/local/cuda/lib64/:/usr/lib/x86_64-linux-gnu/
ENV TENSORFLOW_SRC_PATH /usr/local/lib/python3.6/dist-packages/tensorflow/

RUN git clone https://github.com/hyoungjun-noh/warp-ctc.git && \
    cd warp-ctc && \
    mkdir build && \
    cd build && \
    cmake .. && \
    make

RUN cd warp-ctc/tensorflow_binding && \
    python3 setup.py install

ENV LD_LIBRARY_PATH $LD_LIBRARY_PATH:/usr/local/lib/python3.6/dist-packages/warpctc_tensorflow-0.1-py3.6-linux-x86_64.egg/warpctc_tensorflow/
