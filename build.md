* [ffmpeg build](https://blog.csdn.net/Mmagic1/article/details/124888438) ffmpeg build 方法

### 准备工作
- 在MSYS2中更新基础依赖项，输入：pacman -Syu
- 安装MinGW-w64等工具项，输入：pacman -S --needed base-devel mingw-w64-x86_64-toolchain
- 安装完成后，关闭MSYS2窗口，在"开始"菜单中，选择“MSYS2 MinGW x64”，运行弹出窗口，切换到FFmpeg源码文件夹路径，进行配置，输入:
- ./configure --enable-shared --prefix=./build --enable-gpl --enable-libx264 --disable-x86asm
- make -j8
- make install

### 根据第11点，生成的exe中，是不包含ffplay.exe中，原因是系统缺少SDL，运行

- pacman -S mingw-w64-x86_64-SDL2，即可安装SDL

### ffmpeg源码的decoder中是不包括x264的，需要额外编译x264

- 下载：wget https://code.videolan.org/videolan/x264/-/archive/master/x264-master.tar.bz2 
- 解压：tar -jxvf E:/ffmpeg/x264-master.tar.bz2 -C E:/ffmpeg/x264
- 编译：./configure --prefix=/bin --enable-static --host=mingw64 --disable-cli --disable-asm
- make clean
- make -j8
- make install

### 配置x264 路径 C:\msys64\etc\profile

- PKG_CONFIG_PATH="/bin/lib/pkgconfig"