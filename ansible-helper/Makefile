IMAGE_NAME := softasap/circleci-helper-images
PREFIX := cimg_py311_ansible
DATE_TAG := $(shell date +%Y%m%d)
IMAGE_TAGS := $(PREFIX)_latest $(PREFIX)_$(DATE_TAG)

build:
	$(foreach tag, $(IMAGE_TAGS), docker build --build-arg BUILD_DATE=$(DATE_TAG)  -t $(IMAGE_NAME):$(tag) .;)
push:
	$(foreach tag, $(IMAGE_TAGS), docker push $(IMAGE_NAME):$(tag);)
