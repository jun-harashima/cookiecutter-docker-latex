# cookiecutter-docker-latex

This is a minimal cookiecutter template for compiling a LaTeX file using Docker.

## Requirements

- Cookiecutter 1.6 or later
- Docker version 17 or later

## Quick Start

Run the following command:

```
$ cookiecutter https://github.com/jun-harashima/cookiecutter-docker-latex
```

Then, answer the following questions:

```
project_name [project_name]: awesome-paper
project_slug [awesome_paper]:
```

In the above example, `cookiecutter` command makes `awesome_paper` directory which has the following directories and files:

- Makefile
- docker
  - Dockerfile
- src
  - main.tex
  - main.bib

Now you can compile a LaTeX file in a Docker container. First, build an image from the Dockerfile as follows:

```
make build
```

Then, create a container from the image like this:

```
make create
```

You are now in `work` directory	associated with the host directory. Finally, you can start writing a LaTeX file as you like. Write the file using your favorite editor in the host. Then, compile it using the following command in the container:

```
make compile
```

You may escape from the container to take a rest. You can restart your work like this:

```
make attach
```

When you complete writing the LaTeX file (or give up writing it), remove the image and container as follows:

```
make clean
```

## License

Apache version 2.0
