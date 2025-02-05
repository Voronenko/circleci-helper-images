FROM cimg/python:3.11.11-node

ARG TFENV_VERSION=3.0.0
ARG BUILD_DATE

# Metadata
LABEL org.opencontainers.image.title="debug-pod" \
      org.opencontainers.image.url="https://hub.docker.com/repository/docker/softasap/circleci-helper-images/" \
      org.opencontainers.image.source="https://github.com/Voronenko/circleci-helper-images" \
      org.opencontainers.image.created=$BUILD_DATE \
      org.opencontainers.image.authors="Vyacheslav Voronenko <git@voronenko.info>" \
      org.opencontainers.image.description="Ansible helper image over official circleci Python with node, with ansible and tfenv installed ontop" \
      org.opencontainers.image.version.python="3.11.11" \
      org.opencontainers.image.version.node="v20.18.1" \
      org.opencontainers.image.version.poetry="2.0.1" \
      org.opencontainers.image.version.tfenv="3.0.0"

USER root

ENV POETRY_VERSION=2.0.1
ENV POETRY_HOME="/opt/poetry"
ENV POETRY_VIRTUALENVS_CREATE=false
ENV PATH="$POETRY_HOME/bin:$PATH"

RUN curl -sSL https://install.python-poetry.org | python3 - && \
    poetry --version

COPY ./pyproject.toml ./poetry.lock /tmp/
RUN cd /tmp && poetry install --no-root --no-interaction --no-ansi

RUN curl -sLo /tmp/tfenv.tar.gz "https://github.com/tfutils/tfenv/archive/refs/tags/v${TFENV_VERSION}.tar.gz" \
    && tar -C /tmp -xf /tmp/tfenv.tar.gz \
    && mv "/tmp/tfenv-${TFENV_VERSION}/bin"/* /usr/local/bin/ \
    && mkdir -p /usr/local/lib/tfenv \
    && mv "/tmp/tfenv-${TFENV_VERSION}/lib" /usr/local/lib/tfenv/ \
    && mv "/tmp/tfenv-${TFENV_VERSION}/libexec" /usr/local/lib/tfenv/ \
    && mkdir -p /usr/local/share/licenses \
    && mv "/tmp/tfenv-${TFENV_VERSION}/LICENSE" /usr/local/share/licenses/tfenv \
    && rm -rf /tmp/tfenv* \
    ;
ENV TFENV_ROOT=/usr/local/lib/tfenv
ENV TFENV_CONFIG_DIR=/var/tfenv
VOLUME /var/tfenv

USER circleci
