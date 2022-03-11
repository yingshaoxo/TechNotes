# How to build obs in m1 macos

## Links
- https://www.kilinbox.net/2021/02/obsarmbuild.html
- https://obsproject.com/wiki/install-instructions#macos-xcode-project
- https://www.jianshu.com/p/8616e3475900
- https://obsproject.com/forum/threads/obs-mac-m1-arm-compile-progress-scripting.147059/

## bash commands
### simple building
```bash
git clone --recursive https://github.com/obsproject/obs-studio.git

cd obs-studio
# git checkout "27.2.3"
git checkout -b main "27.2.3"

cd CI

mv ./full-build-macos.sh ./full-build-macos.sh.bak

curl -O https://lib.kilinbox.net/build_obs_mac/2022-03-02/full-build-macos.sh

chmod 755 ./full-build-macos.sh

cd ..
./CI/full-build-macos.sh -b -p

#./CI/full-build-macos.sh -b

codesign -s - -f --deep ./build/OBS.app
```

### build with xcode
```bash
cd obs-studio
mkdir -p builds_project/xcode
cd builds_project/xcode

cmake -DCMAKE_OSX_DEPLOYMENT_TARGET=10.13 -DBUILD_BROWSER=OFF -DDISABLE_PYTHON=ON -G Xcode ../..
```


## Conclustion
As I tested out.

We could use command lines to build the OBS in m1 macOS.

But we can't run and debug the OBS directly from Xcode for now.

Since they do not have good support for m1 chip.

(The auto-complete works in xcode even if it can't build the OBS, weird