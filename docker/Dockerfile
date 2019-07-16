# sudo docker build -t foo:detectron .
# sudo docker run --runtime=nvidia -it  -w / -v $PWD:/mnt/ -e HOST_PERMS="$(id -u):$(id -g)" foo:detectron bash
# python tools/infer_simple.py     --cfg configs/12_2017_baselines/e2e_mask_rcnn_R-101-FPN_2x.yaml     --output-dir /mnt/detectron-visualizations     --image-ext jpg     --wts https://dl.fbaipublicfiles.com/detectron/35861858/12_2017_baselines/e2e_mask_rcnn_R-101-FPN_2x.yaml.02_32_51.SgT4y1cO/output/train/coco_2014_train:coco_2014_valminusminival/generalized_rcnn/model_final.pkl     /mnt/woot

# Use Caffe2 image as parent image
# FROM caffe2/caffe2:snapshot-py2-cuda9.0-cudnn7-ubuntu16.04

# use nvidia repo instead, skip the other stuff
FROM nvcr.io/nvidia/caffe2:18.08-py2


# RUN mv /usr/local/caffe2 /usr/local/caffe2_build
# ENV Caffe2_DIR /usr/local/caffe2_build

# ENV PYTHONPATH /usr/local/caffe2_build:${PYTHONPATH}
# ENV LD_LIBRARY_PATH /usr/local/caffe2_build/lib:${LD_LIBRARY_PATH}

# Clone the Detectron repository
RUN git clone https://github.com/iGoog/detectron /detectron

# Install Python dependencies
RUN pip install -r /detectron/requirements.txt

# need pyyaml==3.12, not >= - fixed in forked repo
# RUN pip install \
#         numpy>=1.13 \
#         pyyaml==3.12 \
#         matplotlib \
#         opencv-python>=3.2 \
#         setuptools \
#         Cython \
#         mock \
#         scipy \
#         six \
#         future \
#         protobuf


# Install the COCO API
RUN git clone https://github.com/cocodataset/cocoapi.git /cocoapi
WORKDIR /cocoapi/PythonAPI
RUN make install

# Go to Detectron root
WORKDIR /detectron

# Set up Python modules
RUN make

# This one does not work due to detected arch, trying edited file.
# [Optional] Build custom ops
# RUN make ops


