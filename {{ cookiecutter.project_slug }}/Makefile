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

{%- if cookiecutter.macro == 'pdflatex' %}
export LATEX=pdflatex
{%- elif cookiecutter.macro == 'platex' %}
export LATEX=platex
{%- else %}
export LATEX=latex
{%- endif %}

build:
	docker build -t $(IMAGE_NAME) -f $(DOCKERFILE) .

create:
	docker run -it -v $(PWD):/work --name $(CONTAINER_NAME) $(IMAGE_NAME)

attach:
	@echo "$$START_DOCKER_CONTAINER" | $(SHELL)
	@echo "Launched $(CONTAINER_NAME)..."
	docker attach $(CONTAINER_NAME)

clean: remove-image remove-container

remove-image:
	docker image rm $(IMAGE_NAME)

remove-container:
	docker rm $(CONTAINER_NAME)

compile:
	$(LATEX) -output-directory=src src/main.tex
	bibtex src/main
	$(LATEX) -output-directory=src src/main.tex
	$(LATEX) -output-directory=src src/main.tex
	dvipdfmx -o src/main.pdf src/main.dvi
