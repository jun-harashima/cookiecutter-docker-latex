FROM alpine:3.8

RUN apk add texlive perl=5.26.2-r1

{% if cookiecutter.editor == 'emacs' -%}
RUN apk add emacs
{%- endif %}

WORKDIR /work
