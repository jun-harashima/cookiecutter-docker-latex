FROM alpine:3.8

RUN apk add texlive

{% if cookiecutter.editor == 'emacs' -%}
RUN apk add emacs
{%- endif %}