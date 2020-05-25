# Payload Info

This action downloads, compiles and installs OpenCV using the informed version.

Check out the [`.github/workflows/main.yml`](https://github.com/Dovyski/setup-opencv-action/blob/master/.github/workflows/main.yml) file to see this action working.

## Inputs

### `opencv-verion`
**Required** OpenCV version to be installed. Default `"."`.

### `opencv-extra-modules`
If `opencv-contrib` (extra modules) should be included in the instalation. Default `true`.

### `install-deps`
If dependencies should be installed as well. Default `true`.

### `CMAKE_BUILD_TYPE`
Default `RELEASE`.

### `CMAKE_CXX_COMPILER`
Default `g++`.

### `CMAKE_INSTALL_PREFIX`
Default `/usr/local`.

### `WITH_TBB`
Default `ON`.

### `WITH_IPP`
Default `ON`.

### `BUILD_NEW_PYTHON_SUPPORT`
Default `OFF`.

### `WITH_V4L`
Default `OFF`.

### `ENABLE_PRECOMPILED_HEADERS`
Default `ON`.

### `INSTALL_C_EXAMPLES`
Default `OFF`.

### `INSTALL_PYTHON_EXAMPLES`
Default `OFF`.

### `BUILD_EXAMPLES`
Default `OFF`.

### `WITH_QT`
Default `OFF`.

### `WITH_OPENGL`
Default `OFF`.

## Usage

See [action.yml](action.yml)

Basic:
```yaml
steps:
- uses: actions/checkout@v2
- uses: actions/setup-opencv@v1
  with:
    opencv-version: '4.0.0'
```

Install development version (master):
```yaml
steps:
- uses: actions/checkout@v2
- uses: actions/setup-opencv@v1
  with:
    opencv-version: 'master'
```

Matrix Testing:
```yaml
jobs:
  build:
    runs-on: ubuntu-16.04
    strategy:
      matrix:
        opencv: [ '3.4.0', '4.0.0', '4.1.0' ]
    name: OpenCV ${{ matrix.opencv }} sample
    steps:
      - uses: actions/checkout@v2
      - name: Setup opencv
        uses: actions/setup-opencv@v1
        with:
          opencv-version: ${{ matrix.opencv }}
```
