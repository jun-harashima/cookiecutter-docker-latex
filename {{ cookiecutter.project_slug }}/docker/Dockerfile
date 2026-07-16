FROM alpine:3.22

RUN apk --no-cache add \
    make \
    texlive-most \
{%- if cookiecutter.macro in ['platex', 'xelatex', 'lualatex'] %}
    texlive-langextra \
{%- endif %}
{%- if cookiecutter.macro == 'xelatex' %}
    texlive-xetex \
    fontconfig \
{%- endif %}
{%- if cookiecutter.macro == 'lualatex' %}
    texlive-luatex \
{%- endif %}
{%- if cookiecutter.macro in ['latex', 'platex'] %}
    ghostscript \
{%- endif %}
{%- if cookiecutter.macro in ['platex', 'xelatex', 'lualatex'] %}
    font-noto-cjk \
{%- endif %}
    texlive

WORKDIR /work

CMD ["/bin/sh"]
