# Setup OpenCV

This action downloads, compiles and installs OpenCV. You can choose the version to be installed, as well as how the build/install should occour. If you just want OpenCV installed and ready for use in your Github Actions, this is for you.

Check out the [`.github/workflows/basic.yml`](https://github.com/Dovyski/setup-opencv-action/blob/master/.github/workflows/basic.yml) file to see this action working.

> **NOTICE:** this action was created to support CI testings of [cvui](https://github.com/Dovyski/cvui), a GUI library for OpenCV.

## Inputs

| Name  | Description | Default value |
|---|---|---|
| `opencv-verion` | OpenCV version to be installed. | - |
| `opencv-extra-modules` | If [opencv-contrib](https://github.com/opencv/opencv_contrib) (extra modules) should be included in the instalation. | `true` |
| `install-deps` | If dependencies should be installed as well, e.g. libs, cmake, etc. | `true` |
| `CMAKE_BUILD_TYPE` | | `RELEASE` |
| `CMAKE_CXX_COMPILER` | | `g++` |
| `CMAKE_INSTALL_PREFIX` | | `/usr/local` |
| `WITH_TBB` | | `ON` |
| `WITH_IPP` | | `ON` |
| `BUILD_NEW_PYTHON_SUPPORT` | | `OFF` |
| `WITH_V4L` | | `OFF` |
| `ENABLE_PRECOMPILED_HEADERS` | | `ON` |
| `INSTALL_C_EXAMPLES` | | `OFF` |
| `INSTALL_PYTHON_EXAMPLES` | | `OFF` |
| `BUILD_EXAMPLES` | | `OFF` |
| `WITH_QT` | | `OFF` |
| `WITH_OPENGL` | | `OFF` |
| `GENERATE_PKGCONFIG` | | `OFF` |

## Usage

See [action.yml](action.yml)

Basic:
```yaml
steps:
- uses: actions/checkout@v2
- uses: Dovyski/setup-opencv-action@v1.1
  with:
    opencv-version: '4.0.0'
```

Custom build and install:
```yaml
steps:
- uses: actions/checkout@v2
- uses: Dovyski/setup-opencv-action@v1.1
  with:
    opencv-version: 4.0.0
    ENABLE_PRECOMPILED_HEADERS: OFF
    INSTALL_C_EXAMPLES: ON
    BUILD_EXAMPLES: ON
```

Install development version (master branch, not released yet):
```yaml
steps:
- uses: actions/checkout@v2
- uses: Dovyski/setup-opencv-action@v1.1
  with:
    opencv-version: master
```

Matrix testing:
```yaml
jobs:
  build:
    runs-on: ubuntu-18.04
    strategy:
      matrix:
        opencv: [ '3.4.0', '4.0.0', '4.1.0' ]
    name: OpenCV ${{ matrix.opencv }}
    steps:
      - uses: actions/checkout@v2
      - name: Setup opencv
        uses: Dovyski/setup-opencv-action@v1.1
        with:
          opencv-version: ${{ matrix.opencv }}
```
