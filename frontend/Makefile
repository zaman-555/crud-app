# Variables
IMAGE_NAME = crud-fe
TAG = v1.1
DOCKERFILE = Dockerfile

# Build the Docker image
build:
	docker build -t $(IMAGE_NAME):$(TAG) -f $(DOCKERFILE) .

# Run the container
run: build
	docker run -p 3000:3000 --rm $(IMAGE_NAME):$(TAG)

# Run the container in detached mode
run-detached: build
	docker run -d -p 3000:3000 --name $(IMAGE_NAME)-container $(IMAGE_NAME):$(TAG)

# Stop the running container
stop:
	docker stop $(IMAGE_NAME)-container || true

# Remove the container
rm: stop
	docker rm $(IMAGE_NAME)-container || true

# Push the image to registry
push:
	docker push $(IMAGE_NAME):$(TAG)

# Clean up local images
clean: rm
	docker rmi $(IMAGE_NAME):$(TAG) || true

# Tag the image with a new tag
tag:
	docker tag $(IMAGE_NAME):$(TAG) $(IMAGE_NAME):$(NEW_TAG)

# Help target to show available commands
help:
	@echo "Available targets:"
	@echo "  build        - Build the Docker image"
	@echo "  run          - Build and run the container interactively"
	@echo "  run-detached - Build and run the container in background"
	@echo "  stop         - Stop the running container"
	@echo "  rm           - Remove the container"
	@echo "  push         - Push the image to registry"
	@echo "  clean        - Remove the container and image"
	@echo "  tag NEW_TAG= - Tag the image with a new tag"
	@echo "  help         - Show this help message"