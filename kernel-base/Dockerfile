FROM    fedora:latest AS ksrc
  
RUN     curl -s https://repos.fedorapeople.org/repos/thl/kernel-vanilla.repo | tee /etc/yum.repos.d/kernel-vanilla.repo

ARG     KERNEL_PKG=kernel
ARG     KERNEL_FILE=vmlinuz

ENV     KERNEL_PKG=$KERNEL_PKG
ENV     KERNEL_FILE=$KERNEL_FILE

RUN     dnf -y --enablerepo=kernel-vanilla-mainline install $KERNEL_PKG

RUN     for d in /lib/modules/*; do depmod -b . $(basename $d); done

RUN     mkdir -p /out /mnt/lib


### kernel
RUN	cp -a $(find / -name $KERNEL_FILE -print -quit) /mnt/kernel


### modules default ###
COPY    files/ /

RUN     /collect-modules.sh                             # ToDo: check firmware dependencies?

WORKDIR /out

RUN     tar -cf /mnt/kernel.tar .


### firmware default dependencies ###
RUN     set -e && \
        for fw in $(find lib/modules -name \*.ko.xz -exec modinfo --field=firmware {} \;); do \
                mkdir -p "lib/firmware/$(dirname $fw)" && \
                [ -f "/lib/firmware/$fw" ] && cp "/lib/firmware/$fw" "lib/firmware/$fw"; \
        done

RUN     tar --exclude=lib/modules -cf /mnt/firmware.tar .


### modules / firmware all
RUN	cp -a /lib/modules /lib/firmware /mnt/lib/

RUN     ls -lh /mnt/
RUN	ls -lh /mnt/lib/


FROM    scratch

COPY    --from=ksrc /mnt/ /
