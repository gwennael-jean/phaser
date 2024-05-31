FROM bitnami/node:20.14.0

ARG USER_NAME
ARG USER_ID
ARG GROUP_ID

RUN apt-get update && apt-get install -y \
    curl \
    git \
    openssh-client \
    iputils-ping \
    && rm -rf /var/lib/apt/lists/*

RUN if [ ${USER_ID:-0} -ne 0 ] && [ ${GROUP_ID:-0} -ne 0 ] && [ ${USER_NAME:-root} != "root" ]; then \
    userdel -f ${USER_NAME} &&\
    if getent group ${USER_NAME} ; then groupdel ${USER_NAME}; fi &&\
    groupadd -g ${GROUP_ID} ${USER_NAME} &&\
    useradd -l -u ${USER_ID} -g ${USER_NAME} ${USER_NAME} &&\
    install -d -m 0755 -o ${USER_NAME} -g ${USER_NAME} /home/${USER_NAME} &&\
    chown --changes --silent --no-dereference --recursive --from=33:33 ${USER_ID}:${GROUP_ID} \
        /home/${USER_NAME} \
;fi

RUN npm i -g npm@10.8.1

USER ${USER_NAME:-root}

CMD ["npm", "run", "dev"]