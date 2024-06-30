```
apk update && \
apk add \
  git \
  alpine-sdk \
  linux-headers \
  libusb-dev \
  libusb-compat-dev \
  libtool \
  automake \
  autoconf \
  python3 \
  python3-dev \
  py3-setuptools \
  mariadb-dev \
  gd-dev \
  dbus-dev \
  gettext \
  gettext-dev


### compile Serdisplib
-----------------------
wget https://netcologne.dl.sourceforge.net/project/serdisplib/serdisplib/2.02/serdisplib-2.02.tar.gz?viasf=1 -O serdisplib.tar.gz
tar -xvzf serdisplib.tar.gz
cd serdisplib-2.02
./configure --enable-libusb
make
make install
cd ..


### compile LCD4Linux
----------------------
ln -s /usr/bin/automake /usr/bin/automake-1.14
ln -s /usr/bin/aclocal /usr/bin/aclocal-1.14
git clone https://github.com/djusHa/lcd4linux.git
cd lcd4linux
libtoolize && automake --add-missing
./configure --prefix=/usr --bindir=/usr/sbin --with-drivers="all" --with-plugins='all,!seti,!isdn,!raspi,!xmms,!mpd,!dvb,!huawei,!dbus,!mpris_dbus' --with-python PYTHON_VERSION="3.12"
make
make install
cp lcd4linux.conf.sample /etc/lcd4linux.conf
chmod 0600 /etc/lcd4linux.conf
```
