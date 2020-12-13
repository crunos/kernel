# kernel

Clone repository and build all the images
- kernel-base
- kernel
- firmware
- firmware-all
- modules-all

```
git clone https://github.com/crunos/kernel.git

for IMG in kernel-base kernel firmware firmware-all modules-all; do \
    docker run --rm -ti \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v $(pwd):$(pwd) \
    -w $(pwd) \
    crunos/os-builder:latest \
    pkg build -disable-content-trust -org crunos -force -hash latest kernel/$IMG/; \
done
```
