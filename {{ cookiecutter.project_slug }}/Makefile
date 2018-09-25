define START_DOCKER_CONTAINER
if [ `docker inspect -f {% raw -%}{{.State.Running}}{%- endraw %} $(CONTAINER_NAME)` = "false" ] ; then
        docker start $(CONTAINER_NAME)
fi
endef

export PWD=`pwd`
export START_DOCKER_CONTAINER
export PROJECT_NAME={{ cookiecutter.project_slug }}
export IMAGE_NAME=$(PROJECT_NAME)-image
export CONTAINER_NAME=$(PROJECT_NAME)-container
export DOCKERFILE=docker/Dockerfile

create-image:
	docker build -t $(IMAGE_NAME) -f $(DOCKERFILE) .

create-container:
	docker run -it -v $(PWD):/work --name $(CONTAINER_NAME) $(IMAGE_NAME)

start-container:
	@echo "$$START_DOCKER_CONTAINER" | $(SHELL)
	@echo "Launched $(CONTAINER_NAME)..."
	docker attach $(CONTAINER_NAME)

clean: clean-container clean-image

clean-container:
	docker rm $(CONTAINER_NAME)

clean-image:
	docker image rm $(IMAGE_NAME)

compile-tex: ## compile main.tex
	latex src/main.tex
	bibtex src/main
