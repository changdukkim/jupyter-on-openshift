FROM quay.io/jupyteronopenshift/s2i-minimal-notebook-py36:2.5.0

USER root

COPY . /tmp/src

RUN rm -rf /tmp/src/.git* && \
    chown -R 1001 /tmp/src && \
    chgrp -R 0 /tmp/src && \
    chmod -R g+w /tmp/src && \
    rm -rf /tmp/scripts && \
    mv /tmp/src/.s2i/bin /tmp/scripts && \
    mkdir -p /opt/app-root/src/.keras/datasets && \
    chmod 777 /opt/app-root/src/.keras/datasets && \
    cp /tmp/src/mnist.npz /opt/app-root/src/.keras/datasets/

ENV XDG_CACHE_HOME=/opt/app-root/src/.cache

USER 1001

RUN /tmp/scripts/assemble

CMD [ "/opt/app-root/builder/run" ]
