Only for 6.x kernel.

Based on - [Building ZFS](https://openzfs.github.io/openzfs-docs/Developer%20Resources/Building%20ZFS.html)

Install some depensies:
```
apt install build-essential autoconf automake libtool gawk alien fakeroot dkms libblkid-dev \
  uuid-dev libudev-dev libssl-dev zlib1g-dev libaio-dev libattr1-dev libelf-dev \
  python3 python3-dev python3-setuptools python3-cffi libffi-dev python3-packaging git libcurl4-openssl-dev \
  debhelper-compat dh-python po-debconf python3-all-dev python3-sphinx parallel
```

Now we need kernel headers, on armbian with edge 6.8 kernel you can install them with:
```
apt install linux-headers-edge-rockchip-rk3588
```

Clone zfs repo:
```
git clone -b master --single-branch https://github.com/openzfs/zfs
```

Compile:
```
cd zfs
./autogen.sh
./configure
make -s -j$(nproc)
```

Install:
```
make install; ldconfig; depmod
```
