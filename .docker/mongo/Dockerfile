FROM mongo:latest

ARG USER_ID
ARG GROUP_ID

RUN if [ ${USER_ID:-0} -ne 0 ] && [ ${GROUP_ID:-0} -ne 0 ]; then \
    userdel -f mongodb &&\
    if getent group mongodb ; then groupdel mongodb; fi && \
    groupadd -g ${GROUP_ID} mongodb && \
    useradd -l -u ${USER_ID} -g mongodb mongodb && \
    install -d -m 0755 -o mongodb -g mongodb /home/mongodb && \
    chown --changes --silent --no-dereference --recursive \
          --from=999:999 ${USER_ID}:${GROUP_ID} \
        /home/mongodb \
        /data/db \
        /data/configdb \
    ;fi

USER mongodb