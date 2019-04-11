# Use Caffe2 image as parent image
FROM caffe2/caffe2:snapshot-py2-cuda9.0-cudnn7-ubuntu16.04


RUN apt-get update -y && \
    apt-get install -y python-pip python-dev wget nano

RUN apt-get update && apt-get install -y vim git

RUN mv /usr/local/caffe2 /usr/local/caffe2_build
ENV Caffe2_DIR /usr/local/caffe2_build

ENV PYTHONPATH /usr/local/caffe2_build:${PYTHONPATH}
ENV LD_LIBRARY_PATH /usr/local/caffe2_build/lib:${LD_LIBRARY_PATH}

# Clone the Detectron repository
RUN git clone https://github.com/facebookresearch/densepose /densepose

COPY ./app.py /densepose/app.py

# Install Python dependencies
RUN pip install -r /densepose/requirements.txt

RUN pip install Flask
RUN pip install opencv-python
RUN pip install requests
# Install the COCO API
RUN git clone https://github.com/cocodataset/cocoapi.git /cocoapi
WORKDIR /cocoapi/PythonAPI
RUN make install

# Go to Densepose root
WORKDIR /densepose



# Set up Python modules
RUN make

# [Optional] Build custom ops
RUN make ops

RUN pip install PyYAML==3.12

RUN cd DensePoseData && bash get_densepose_uv.sh

RUN cd DensePoseData && bash get_DensePose_COCO.sh

RUN cd DensePoseData && bash get_eval_data.sh

EXPOSE 5000

WORKDIR /densepose

RUN cd /densepose

ENTRYPOINT [ "python2" ]

CMD [ "app.py" ]
 