# containers-swig
Dockerfiles used to build swig win/linux images

```powershell
# Clone repository
git clone https://github.com/plachta11b/containers-swig.git
cd containers-swig
```

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
