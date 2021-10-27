# escape=`

ARG FROM_IMAGE=mcr.microsoft.com/windows/servercore:ltsc2019
ARG SWIG_VERSION=latest

FROM ${FROM_IMAGE}

# install manual
# http://swig.org/Doc2.0/Windows.html#Windows_swig_exe

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

RUN Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

RUN choco install --yes mingw --version=11.1.0
RUN choco install --yes msys2 --version=20210604.0.0 --params "/NoUpdate"
RUN choco install --yes git

SHELL [ "C:\\tools\\msys64\\msys2_shell.cmd -defterm -mingw64 -no-start -full-path -here -c" ]

RUN "pacman -V" || exit /b 0

RUN "yes | pacman -S --noconfirm autoconf" || exit /b 0
RUN "yes | pacman -S --noconfirm automake" || exit /b 0
RUN "yes | pacman -S --noconfirm bison" || exit /b 0
RUN "yes | pacman -S --noconfirm pcre" || exit /b 0
RUN "yes | pacman -S --noconfirm pcre-devel" || exit /b 0

RUN "yes | pacman -S make"

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]
RUN mkdir /usr/src
WORKDIR C:/usr/src
RUN git clone https://github.com/swig/swig.git
WORKDIR C:/usr/src/swig

SHELL [ "C:\\tools\\msys64\\msys2_shell.cmd -defterm -mingw64 -no-start -full-path -here -c" ]
RUN 'wget https://sourceforge.net/projects/pcre/files/pcre/8.45/pcre-8.45.tar.gz'
RUN './Tools/pcre-build.sh'
RUN './autogen.sh'
RUN './configure CXXFLAGS="-static -static-libgcc -static-libstdc++" CFLAGS="-static -static-libgcc -static-libstdc++"'
RUN 'make'
RUN 'make install'

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

# USAGE EXAMPLE
# docker build -t swig:win-x64-latest -f win/x64/Dockerfile .
# docker run -v ${PWD}:C:\app\ --workdir C:/app/js_dir swig:swig:win-x64-latest C:\usr\src\swig\swig.exe -c++ -javascript -node -outcurrentdir C:\app\cpp_dir\app.i
