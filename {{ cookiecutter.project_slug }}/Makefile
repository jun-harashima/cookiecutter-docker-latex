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
export LATEXMK_OPT=-pdf
{%- elif cookiecutter.macro == 'platex' %}
export LATEXMK_OPT=-pdfdvi -latex=platex -e '$$dvipdf=q/dvipdfmx %O -o %D %S/; $$bibtex=q/pbibtex/'
{%- elif cookiecutter.macro == 'xelatex' %}
export LATEXMK_OPT=-pdfxe
{%- elif cookiecutter.macro == 'lualatex' %}
export LATEXMK_OPT=-pdflua
{%- else %}
export LATEXMK_OPT=-pdfdvi -e '$$dvipdf=q/dvipdfmx %O -o %D %S/'
{%- endif %}

build:
	docker build -t $(IMAGE_NAME) -f $(DOCKERFILE) .

create:
	docker run -it -v $(PWD):/work --name $(CONTAINER_NAME) $(IMAGE_NAME)

attach:
	@echo "$$START_DOCKER_CONTAINER" | $(SHELL)
	@echo "Launched $(CONTAINER_NAME)..."
	docker attach $(CONTAINER_NAME)

clean: remove-container remove-image

remove-image:
	docker image rm $(IMAGE_NAME)

remove-container:
	docker rm $(CONTAINER_NAME)

compile:
	latexmk $(LATEXMK_OPT) -output-directory=src src/main.tex
