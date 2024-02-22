# spksrc
```bash
sudo dpkg --add-architecture i386 && sudo apt-get update
sudo apt update

ls /usr/bin | grep python

sudo apt install autoconf-archive autogen automake autopoint bash bc bison build-essential check cmake curl cython3 debootstrap ed expect fakeroot flex g++-multilib gawk gettext git gperf imagemagick intltool jq libbz2-dev libc6-i386 libcppunit-dev libffi-dev libgc-dev libgmp3-dev libltdl-dev libmount-dev libncurses5-dev libpcre3-dev libssl-dev libtool libunistring-dev lzip mercurial moreutils ninja-build patchelf php pkg-config python3-distutils rename ruby-mustache rsync scons subversion swig texinfo unzip xmlto zip zlib1g-dev

wget https://bootstrap.pypa.io/pip/2.7/get-pip.py -O - | sudo python2
sudo pip2 install wheel httpie

wget https://bootstrap.pypa.io/get-pip.py -O - | sudo python3
sudo pip3 install meson==1.0.0

git clone https://github.com/SynoCommunity/spksrc.git
cd spksrc/
make setup

ls spk
ls diyspk

cd spk/transmission
make arch-rtd1296-7.2
```



# pkgscripts-ng
```bash
apt-get install git
mkdir -p /toolkit
cd /toolkit
git clone https://github.com/SynologyOpenSource/pkgscripts-ng

apt-get install cifs-utils \
    python \
    python-pip \
    python3 \
    python3-pip

/toolkit
├── pkgscripts-ng/
│   ├── include/
│   ├── EnvDeploy    (deployment tool for chroot environment)
│   └── PkgCreate.py (build tool for package)
└── build_env/       (directory to store chroot environments)

# 手动下载环境 tarball
https://archive.synology.com/download/ToolChain/toolkit/7.2
/toolkit
├── pkgscripts-ng/
└── toolkit_tarballs/
    ├── base_env-7.2.txz
    ├── ds.rtd1296-7.2.dev.txz
    └── ds.rtd1296-7.2.env.txz

cd /toolkit/pkgscripts-ng/
git checkout DSM7.2
./EnvDeploy -v 7.2 -p rtd1296 -D

/home/keyneko/Documents/GitHub/toolkit/build_env/ds.rtd1296-7.2/usr/local/aarch64-unknown-linux-gnu/aarch64-unknown-linux-gnu/sysroot
/home/keyneko/Documents/GitHub/toolkit/build_env/ds.rtd1296-7.2/usr/local/sysroot/usr/lib/modules/DSM-7.2/build

mkdir -p ../source
cd ../source
git clone https://github.com/SynologyOpenSource/ExamplePackages.git
cp -a ExamplePackages/ExamplePackage/ ./

$ tree -L 2
.
├── build_env
│   └── ds.rtd1296-7.2
├── envdeploy.log
├── envdeploy.log.old
├── pkgscripts-ng
│   ├── EnvDeploy
│   ├── include
│   ├── ParallelProjects.py
│   ├── PkgCreate.py
│   ├── ProjectDepends.py
│   ├── README.md
│   ├── SynoBuild
│   ├── SynoCC
│   ├── SynoCustomize
│   └── SynoInstall
├── source
│   ├── ExamplePackage
│   └── ExamplePackages
└── toolkit_tarballs
    ├── base_env-7.2.txz
    ├── ds.rtd1296-7.2.dev.txz
    └── ds.rtd1296-7.2.env.txz

# 构建并打包
./PkgCreate.py -v 7.2 -p rtd1296 -c ExamplePackage
./PkgCreate.py -v 7.2 -p rtd1296 -c r8152

.
├── result_spk
│   └── ExamplePackage-1.0.0-0001
│       ├── ExamplePackage-armv8-1.0.0-0001_debug.spk
│       └── ExamplePackage-armv8-1.0.0-0001.spk


# make -C /usr/local/aarch64-unknown-linux-gnu/aarch64-unknown-linux-gnu/sysroot/usr/lib/modules/DSM-7.2/build M=/source/r8152 modules
# /usr/local/aarch64-unknown-linux-gnu/bin/aarch64-unknown-linux-gnu-cc -std=c99 -o spk_su spk_su.c

# r8152套件安装失败，ssh登录后执行下指令，重新安装套件修复
sudo install -m 4755 -o root -D /var/packages/r8152/target/r8152/spk_su /opt/sbin/spk_su
```
