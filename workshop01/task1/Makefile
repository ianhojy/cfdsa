# Makefile

# Docker Registry
DOCKER_REGISTRY=ianhojy/workshop01

# Docker image name
IMAGE_NAME=workshop01-image

# Full Docker image tag
IMAGE_TAG=$(DOCKER_REGISTRY):latest

# Container name derived from image name
CONTAINER_NAME=$(IMAGE_NAME)-container

# Dockerfile location
DOCKERFILE=Dockerfile

# Default port value
PORT?=5000
INTERNAL_PORT?=5000

# Default instance name
INSTANCE_NAME?=workshop01-instance

# Default instance hash
INSTANCE_HASH?=hash123

.PHONY: build run push clean stop docker-login

# Build Docker image
build:
	@echo "Building Docker image $(IMAGE_NAME)..."
	docker build -t $(IMAGE_TAG) -f $(DOCKERFILE) .

# Run Docker container with environment variables
run:
	@echo "Running container $(CONTAINER_NAME)..."
	docker run --rm -d --name $(CONTAINER_NAME) -p $(PORT):${INTERNAL_PORT} -e PORT=${INTERNAL_PORT} -e INSTANCE_NAME="$(INSTANCE_NAME)" -e INSTANCE_HASH="$(INSTANCE_HASH)" $(IMAGE_TAG)

stop:
	@echo "Stopping container $(CONTAINER_NAME)..."
	-docker stop $(CONTAINER_NAME)

# Push Docker image to registry
push:
	@echo "Pushing image $(IMAGE_TAG) to registry..."
	docker push $(IMAGE_TAG)

clean:
	@echo "Removing container $(CONTAINER_NAME) if it exists..."
	-docker rm -f $(CONTAINER_NAME)

# Build, run and push
all: build run push
