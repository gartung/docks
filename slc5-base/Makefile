.PHONY: all build

BUILD_REPO := hepsw/build-slc5-base
REPO := hepsw/slc5-base
TAG := 5.11

all: build
	@echo "done"

build: Dockerfile
	docker build --rm --tag=$(BUILD_REPO):$(TAG) .
	docker tag --force $(BUILD_REPO):$(TAG) $(BUILD_REPO):latest
	docker run $(BUILD_REPO):$(TAG) /bin/true
	mkdir -p build
	docker cp $(shell docker ps -q -l):/build/docker.tar build
	cat build/docker.tar | docker import - $(REPO):$(TAG)
	docker tag --force $(REPO):$(TAG) $(REPO):latest

upload: build
	docker push $(REPO):$(TAG)

