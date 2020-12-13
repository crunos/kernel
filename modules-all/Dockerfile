ARG	BASE_KERNEL=crunos/kernel-base

FROM	$BASE_KERNEL AS ksrc



FROM	scratch

COPY	--from=ksrc /lib/modules /lib/modules
