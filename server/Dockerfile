FROM python:3.10
LABEL org.opencontainers.image.source https://github.com/boxmein/c
WORKDIR /app
RUN ["pip", "install", "--no-cache-dir", "poetry"]

COPY ./pyproject.toml /app/pyproject.toml
COPY ./poetry.lock /app/poetry.lock
RUN ["poetry", "config", "virtualenvs.create", "false"]
RUN ["poetry", "install", "--no-root"]

ADD src/ /app
CMD ["gunicorn", "main:app", "-w", "4", "--threads", "12", "--bind", "0.0.0.0:80"]

# documentation
ARG GIT_COMMIT=dev
ARG GIT_BRANCH=dev
ARG VERSION=dev
ENV GIT_COMMIT=${GIT_COMMIT} \
    GIT_BRANCH=${GIT_BRANCH} \
    VERSION=${VERSION}