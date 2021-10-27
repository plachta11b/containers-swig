# containers-swig
Dockerfiles used to build swig win/linux images

```powershell
# Clone repository
git clone https://github.com/plachta11b/containers-swig.git
cd containers-swig
```

## Linux
Comming soon. Use [this one](https://gist.github.com/rcoup/35e11e31d069689c9c09a70cc2fc7a0d) instead for now.

## Windows

### Build windows image
Image uses Windows Server Core by default. Read [win-containers-eula](https://docs.microsoft.com/en-us/virtualization/windowscontainers/images-eula) and [Legal Notice](https://github.com/microsoft/containerregistry/blob/main/legal/Container-Images-Legal-Notice.md) before using corresponding Windows Dockerfile.
```powershell
# Build image
docker build -t swig:win-x64-latest -f win/x64/Dockerfile .

```
### Usage
Use of --workdir instead of --outdir is recommended as later flag was not working as expected during image testing.
```powershell
# Use swig to build wrapper
docker run -v ${PWD}:C:\app\ --workdir C:/app/js_dir swig:swig:win-x64-latest C:\usr\src\swig\swig.exe -c++ -javascript -node -outcurrentdir C:\app\cpp_dir\app.i
```

## SWIG
- [Project page](http://www.swig.org/)
- [Github page](https://github.com/swig/swig)
- [Issue](https://github.com/swig/swig/issues/1112)
