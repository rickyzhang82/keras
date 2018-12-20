help:
	@cat Makefile

DATA?="${HOME}/Data"
DOCKER_FILE=Dockerfile
BACKEND=tensorflow
PYTHON_VERSION?=3.6
CUDA_VERSION?=9.0
CUDNN_VERSION?=7
TEST=tests/
SRC?=/home/Ricky/keras-workspace
CUDA_DEVICES=NVIDIA_VISIBLE_DEVICES='0'

build:
	docker build -t keras --build-arg python_version=$(PYTHON_VERSION) --build-arg cuda_version=$(CUDA_VERSION) --build-arg cudnn_version=$(CUDNN_VERSION) -f $(DOCKER_FILE) .

bash: 
	docker run -it --runtime=nvidia -v $(SRC):/src/workspace -v $(DATA):/data --env KERAS_BACKEND=$(BACKEND) keras bash

ipython: 
	docker run -it --runtime=nvidia -v $(SRC):/src/workspace -v $(DATA):/data --env KERAS_BACKEND=$(BACKEND) keras ipython

notebook: 
	CPU=0 docker run -it --runtime=nvidia -e $(CUDA_DEVICES) -v $(SRC):/src/workspace -v $(DATA):/data -p 8888:8888 --env KERAS_BACKEND=$(BACKEND) keras

test: 
	docker run -it --runtime=nvidia -v $(SRC):/src/workspace -v $(DATA):/data --env KERAS_BACKEND=$(BACKEND) keras py.test $(TEST)

