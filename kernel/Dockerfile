ARG	BASE_KERNEL=crunos/kernel-base:latest

FROM	$BASE_KERNEL AS ksrc


FROM    scratch

COPY    --from=ksrc /kernel /
COPY	--from=ksrc /kernel.tar /
COPY	--from=ksrc /firmware.tar /
