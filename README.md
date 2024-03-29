[![](https://images.microbadger.com/badges/image/alpin3/ulx3s-qt.svg)](https://microbadger.com/images/alpin3/ulx3s-qt "Get your own image badge on microbadger.com")

# ulx3s-qt

Everyhing needed for ulx3s FPGA (with QT support)

# Run

If you don't plan repluggin the FPGA often, just run with device path where your FPGA is connected:

```
docker run --device=/dev/ttyUSB0 -it alpin3/ulx3s-qt
```

If you don't care too much about security and plan repluggin a lot:

```
docker run --privileged -v /dev:/dev -it alpin3/ulx3s-qt
```

Check out [Docker - a way to give access to a host USB or serial device?](https://stackoverflow.com/questions/24225647/docker-a-way-to-give-access-to-a-host-usb-or-serial-device)

# Static binaries

Note: nextpr is dynamically linked due to Python/QT dynamic requirements.

If you just plan to get the static binaries yourself:
```
docker run -it --name ulx3sbin alpin3/ulx3s-qt true
docker cp ulx3sbin:/usr/local/bin static-bin
docker rm ulx3sbin
```

If you just plan to build the static binaries yourself:
```
git clone https://github.com/alpin3/ulx3s-qt.git
cd ulx3s-qt
docker build -t test/ulx3s .
docker run -it --name ulx3sbin test/ulx3s true
docker cp ulx3sbin:/usr/local/bin static-bin
docker rm ulx3sbin
```

## Examples

Typical usage (with QT):

```
XSOCK=/tmp/.X11-unix
XAUTH=/tmp/.docker.xauth
xauth nlist :0 | sed -e 's/^..../ffff/' | xauth -f $XAUTH nmerge -
docker run -v $XSOCK:$XSOCK -v $XAUTH:$XAUTH -e XAUTHORITY=$XAUTH alpin3/ulx3s-qt
```




