VENDOR := dghadge
IMAGE := scheduled-task
VERSION := $(shell git rev-parse HEAD)
BUILD_DATE := $(shell date -R)
VCS_URL := $(shell basename `git rev-parse --show-toplevel`)
VCS_REF := $(shell git log -1 --pretty=%h)
NAME := $(shell basename `git rev-parse --show-toplevel`)
ECR_REPO_PREFIX := 420279361566.dkr.ecr.us-east-1.amazonaws.com

build:
	docker build --rm -t ${VENDOR}/${IMAGE} --build-arg VERSION="${VERSION}" \
	--build-arg BUILD_DATE="${BUILD_DATE}" \
	--build-arg VCS_URL="${VCS_URL}" \
	--build-arg VCS_REF="${VCS_REF}" \
	--build-arg NAME="${NAME}" \
	--build-arg VENDOR="${VENDOR}" .

run:
	docker run --rm -p 8080:80 ${VENDOR}/${IMAGE}

tag:
	docker tag ${VENDOR}/${IMAGE}:latest ${ECR_REPO_PREFIX}/scheduled-task:latest

push:
	docker push ${ECR_REPO_PREFIX}/scheduled-task:latest

clean:
	docker images -q -f "dangling=true" | \
		xargs -I {} docker rmi {}
	docker volume ls -q -f "dangling=true" | \
		xargs -I {} docker volume rm {}

inspect:
	docker inspect --format='{{range $$k, $$v := .Config.Labels}}{{$$k}}={{$$v}}{{println}}{{end}}' ${IMAGE}

print:
	@echo VERSION=${VERSION}
	@echo BUILD_DATE=${BUILD_DATE}
	@echo VCS_URL=${VCS_URL}
	@echo VCS_REF=${VCS_REF}
	@echo NAME=${NAME}
	@echo VENDOR=${VENDOR}
	@echo IMAGE=${IMAGE}
