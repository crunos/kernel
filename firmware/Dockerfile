ARG	BASE_KERNEL=crunos/kernel-base:latest
ARG	BASE_IMG=alpine:latest

FROM	$BASE_KERNEL AS ksrc

FROM	$BASE_IMG AS build

WORKDIR	/mnt

COPY	--from=ksrc /firmware.tar /

RUN	tar -xf /firmware.tar 

RUN	ls -lh /mnt/lib/firmware



FROM	scratch

COPY	--from=build /mnt/ /
