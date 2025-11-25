# syntax=docker/dockerfile:1.6
ARG BASE
FROM ${BASE}
ARG INSTANCE_NAME
ENV INSTANCE_NAME="${INSTANCE_NAME}"

USER root

COPY --chown=51773:51773 ./iris.script /tmp/iris.script


RUN su - irisowner -c "\
    iris start \"$INSTANCE_NAME\" \
   && iris session \"$INSTANCE_NAME\" < /tmp/iris.script \
   && iris stop \"$INSTANCE_NAME\" quietly" \
 && rm -f /tmp/iris.script

USER 51773
