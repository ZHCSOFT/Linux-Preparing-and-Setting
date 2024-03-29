### Preparing basic packages and source code
```
sudo apt update
sudo apt install gcc g++ flex gcc-multilib
```

```
cd ~/Downloads
git clone https://github.com/gcc-mirror/gcc.git
cd gcc
```
Check and switch version required by command `git branch -a` and checkout to specific branch you need
```
git checkout remotes/origin/releases/gcc-11
./contrib/download_prerequisites
```

### Build and Installation
```
mkdir build && cd build
../configure --prefix=/usr/local/gcc-11 --enable-bootstrap --enable-languages=c,c++ --enable-threads=posix --enable-checking=release --enable-multilib --with-system-zlib
make --jobs=$(nproc --all)
sudo make install
```

### Set alternatives and manage symlinks
Check current gcc and g++ link status
```
ls -al /usr/bin/gcc*
ls -al /usr/bin/g++*
```
Assume we have gcc-7 currently (Check current gcc version by `gcc -v` and g++ by `g++ -v`)
```
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 100
sudo update-alternatives --install /usr/bin/gcc gcc /usr/local/gcc-11/bin/gcc 90

sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-9 100
sudo update-alternatives --install /usr/bin/g++ g++ /usr/local/gcc-11/bin/g++ 90
```

### Apply alternatives
```
sudo update-alternatives --config gcc
```
Enter the number of selection you specify
```
sudo update-alternatives --config g++
```
Likewise, enter the number of selection you specify,
