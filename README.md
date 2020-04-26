# flutter_jit

### 步骤

* 代理

> Shadowsocks

```shell script
export http_proxy=http://127.0.0.1:1087;export https_proxy=http://127.0.0.1:1087;
```

> 12VPN

```shell script
export http_proxy=http://127.0.0.1:16005;export https_proxy=http://127.0.0.1:16005;
```

* 切换工作目录

```shell script
cd docker/build
```

* 配置depot_tools工具

```shell script
git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git
export PATH=$PATH:$PWD/depot_tools
```

* 修改 engine/.gclient

```text
solutions = [
  {
    "managed": False,
    "name": "src/flutter",
    "url": "https://github.com/flutter/engine.git@af51afceb8886cc11e25047523c4e0c7e1f5d408",
    "custom_deps": {},
    "deps_file": "DEPS",
    "safesync_url": "",
  },
]
```

> 修改 "url" -> "https://github.com/flutter/engine.git" + "@" + "${engine.version}"

* 同步源码（用时比较久）

```shell script
gclient sync --verbose
```

* 编译（用时比较久）

> 切换工作目录

```shell script
cd engine/src/
```

> (默认) Android debug

```shell script
# arm
./flutter/tools/gn --android --runtime-mode debug --android-cpu arm
ninja -C out/android_debug
./flutter/tools/gn --runtime-mode debug --android-cpu arm
ninja -C out/host_debug

# arm64
./flutter/tools/gn --android --runtime-mode debug --android-cpu arm64
ninja -C out/android_debug_arm64
./flutter/tools/gn --runtime-mode debug --android-cpu arm64
ninja -C out/host_debug_arm64
```


> (默认) Android profile

```shell script
# arm
./flutter/tools/gn --android --runtime-mode profile --android-cpu arm
ninja -C out/android_profile
./flutter/tools/gn --runtime-mode profile --android-cpu arm
ninja -C out/host_profile

# arm64
./flutter/tools/gn --android --runtime-mode profile --android-cpu arm64
ninja -C out/android_profile_arm64
./flutter/tools/gn --runtime-mode profile --android-cpu arm64
ninja -C out/host_profile_arm64
```

> (默认) Android release

```shell script
# arm
./flutter/tools/gn --android --runtime-mode release --android-cpu arm
ninja -C out/android_release
./flutter/tools/gn --runtime-mode release --android-cpu arm
ninja -C out/host_release

# arm64
./flutter/tools/gn --android --runtime-mode release --android-cpu arm64
ninja -C out/android_release_arm64
./flutter/tools/gn --runtime-mode release --android-cpu arm64
ninja -C out/host_release_arm64
```

> Android JIT release

```shell script
# arm
./flutter/tools/gn --android --runtime-mode jit_release --android-cpu arm
ninja -C out/android_jit_release
./flutter/tools/gn --runtime-mode jit_release --android-cpu arm
ninja -C out/host_jit_release

# arm64
./flutter/tools/gn --android --runtime-mode jit_release --android-cpu arm64
ninja -C out/android_jit_release_arm64
./flutter/tools/gn --runtime-mode jit_release --android-cpu arm64
ninja -C out/host_jit_release_arm64
```

* 使用

```shell script
flutter build apk --local-engine=android_jit_release --local-engine-src-path=/path/to/engine/src
```
