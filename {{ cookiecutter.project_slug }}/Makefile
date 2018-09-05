define START_DOCKER_CONTAINER
if [ `$(DOCKER) inspect -f {% raw -%}{{.State.Running}}{%- endraw %} $(CONTAINER_NAME)` = "false" ] ; then
        $(DOCKER) start $(CONTAINER_NAME)
fi
endef

export PWD=`pwd`
export PROJECT_NAME={{ cookiecutter.project_slug }}
export IMAGE_NAME=$(PROJECT_NAME)-image
export CONTAINER_NAME=$(PROJECT_NAME)-container
export HOST_PORT={{ cookiecutter.host_port }}
export CONTAINER_PORT=8888
export DOCKERFILE=docker/Dockerfile

init-docker: ## initialize Docker image
	docker build -t $(IMAGE_NAME) -f $(DOCKERFILE) .

create-container: ## create Docker container
	docker run -it -v $(PWD):/work -p $(HOST_PORT):$(CONTAINER_PORT) --name $(CONTAINER_NAME) $(IMAGE_NAME)

start-container: ## start Docker container
	@echo "$$START_DOCKER_CONTAINER" | $(SHELL)
	@echo "Launched $(CONTAINER_NAME)..."
	docker attach $(CONTAINER_NAME)

profile: ## show profile of the project
	@echo "CONTAINER_NAME: $(CONTAINER_NAME)"
	@echo "IMAGE_NAME: $(IMAGE_NAME)"

clean: clean-container clean-image ## remove all artifacts

clean-container: ## remove Docker container
	docker rm $(CONTAINER_NAME)

clean-image: ## remove Docker image
	docker image rm $(IMAGE_NAME)
