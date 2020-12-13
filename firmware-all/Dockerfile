ARG	BASE_KERNEL=crunos/kernel-base:latest

FROM	$BASE_KERNEL AS ksrc



FROM	scratch

COPY	--from=ksrc /lib/firmware /lib/firmware
