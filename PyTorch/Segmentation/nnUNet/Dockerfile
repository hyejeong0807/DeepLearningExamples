ARG FROM_IMAGE_NAME=nvcr.io/nvidia/pytorch:21.02-py3
FROM ${FROM_IMAGE_NAME}

ADD . /workspace/nnunet_pyt
WORKDIR /workspace/nnunet_pyt

RUN pip install --upgrade pip
RUN pip install --disable-pip-version-check -r requirements.txt
RUN pip install --disable-pip-version-check -r triton/requirements.txt
RUN pip install pytorch-lightning==1.0.0 --no-dependencies
RUN pip install torchtext==0.6.0 --no-dependencies
RUN pip install monai==0.4.0 --no-dependencies
RUN pip install --extra-index-url https://developer.download.nvidia.com/compute/redist/ nvidia-dali-cuda110==0.30.0
RUN pip install torch_optimizer==0.0.1a15 --no-dependencies
RUN pip install numpy==1.20.3
RUN pip install nvidia-pyindex==1.0.9
RUN pip install nvidia-dlprof==1.2.0
RUN pip install nvidia_dlprof_pytorch_nvtx==1.2.0

RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
RUN unzip -qq awscliv2.zip
RUN ./aws/install
RUN rm -rf awscliv2.zip aws

# Install Perf Client required library
RUN apt-get update && apt-get install -y libb64-dev libb64-0d

# Install Triton Client Python API and copy Perf Client
#COPY --from=triton-client /workspace/install/ /workspace/install/
#RUN pip install /workspace/install/python/triton*.whl
