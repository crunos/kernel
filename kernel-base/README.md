# kernel base

```
docker run --rm -ti \
	-v /var/run/docker.sock:/var/run/docker.sock \
	-v $(pwd):$(pwd) \
	-w $(pwd) \
	crunos/os-builder:latest \
	pkg build -disable-content-trust -org crunos --force -hash latest \
  https://github.com/crunos/kernel-base.git#main
```
