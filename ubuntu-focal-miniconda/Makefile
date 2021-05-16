PYTHON_ENVIRONMENT:=./environment.yml

all:
	docker --version

docker_build: ./Dockerfile ./environment.yml
	echo $(NVIDIA)
	docker build -t handwash:lts -f ./Dockerfile --build-arg environment=$(PYTHON_ENVIRONMENT) .
	
.PHONY: docker_run
docker_run:
	docker run -it \
		--rm \
		--init \
		-v `pwd`:`pwd` \
		-w `pwd` \
		handwash:lts \

.PHONY: remove_all_docker_containers
remove_all_docker_containers:
	docker rm $(docker ps -a -q)
