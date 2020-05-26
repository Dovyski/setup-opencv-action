# Payload Info

This action downloads, compiles and installs OpenCV using the informed version.

Check out the [`.github/workflows/main.yml`](https://github.com/Dovyski/setup-opencv-action/blob/master/.github/workflows/main.yml) file to see this action working.

## Inputs

| Name  | Description | Default  |
|---|---|---|
| `opencv-verion` | **[Required]** OpenCV version to be installed. | `4.0.0` |
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

## Usage

See [action.yml](action.yml)

Basic:
```yaml
steps:
- uses: actions/checkout@v2
- uses: Dovyski/setup-opencv-action@v1
  with:
    opencv-version: '4.0.0'
```

Custom build and install:
```yaml
steps:
- uses: actions/checkout@v2
- uses: Dovyski/setup-opencv-action@v1
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
- uses: Dovyski/setup-opencv-action@v1
  with:
    opencv-version: master
```

Matrix Testing:
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
        uses: Dovyski/setup-opencv-action@v1
        with:
          opencv-version: ${{ matrix.opencv }}
```
