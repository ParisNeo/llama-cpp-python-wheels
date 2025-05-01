# Pre-compiled Wheels for llama-cpp-python

[![Build Wheels Workflow Status](https://github.com/ParisNeo/llama-cpp-python-wheels/actions/workflows/build-wheels.yml/badge.svg)](https://github.com/ParisNeo/llama-cpp-python-wheels/actions/workflows/build-wheels.yml)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Original llama-cpp-python Repo](https://img.shields.io/github/stars/abetlen/llama-cpp-python?style=social)](https://github.com/abetlen/llama-cpp-python)
[![GitHub Releases](https://img.shields.io/github/downloads/ParisNeo/llama-cpp-python-wheels/total?label=Wheel%20Downloads)](https://github.com/ParisNeo/llama-cpp-python-wheels/releases)

This repository automatically builds and hosts pre-compiled Python wheels for the excellent [`abetlen/llama-cpp-python`](https://github.com/abetlen/llama-cpp-python) package.

The goal is to simplify the installation process for users on various platforms and architectures by providing wheels with different backend accelerations (CPU, CUDA, Metal, etc.), avoiding the need for a local compiler setup in many cases.

**Maintained by:** [ParisNeo](https://github.com/ParisNeo)

## Installation

You can install the pre-compiled wheels using `pip`. There are two primary methods:

### Method 1: Using `--extra-index-url` (Recommended)

This method uses `pip` to automatically find the appropriate wheel for your platform and Python version from our hosted index on GitHub Pages. You need to specify the backend you want to use in the URL.

**General Format:**

```bash
pip install llama-cpp-python --extra-index-url https://parisneo.github.io/llama-cpp-python-wheels/whl/<backend>/
```

Replace `<backend>` with the desired backend identifier (see [Supported Configurations](#supported-configurations) below).

**Examples:**

*   **CPU Only (using OpenBLAS):**
    ```bash
    pip install llama-cpp-python --extra-index-url https://parisneo.github.io/llama-cpp-python-wheels/whl/cpu/
    ```

*   **NVIDIA CUDA 12.1 (if available):**
    ```bash
    # Make sure you have CUDA 12.1 Toolkit installed and compatible drivers
    pip install llama-cpp-python --extra-index-url https://parisneo.github.io/llama-cpp-python-wheels/whl/cu121/
    ```

*   **Apple Metal (for M1/M2/M3 Macs, if available):**
    ```bash
    pip install llama-cpp-python --extra-index-url https://parisneo.github.io/llama-cpp-python-wheels/whl/metal/
    ```

*   _(Add examples for other backends like ROCm, Vulkan as they become available)_

**Note:** The GitHub Pages index might take a few minutes to update after a new build finishes.

### Method 2: Manual Download from Releases

You can also manually download the specific wheel file for your system from the [**Releases Page**](https://github.com/ParisNeo/llama-cpp-python-wheels/releases).

1.  Go to the [Releases Page](https://github.com/ParisNeo/llama-cpp-python-wheels/releases).
2.  Find the latest release corresponding to the `llama-cpp-python` version you need.
3.  Under "Assets", locate the `.whl` file that matches your:
    *   Operating System (Linux, macOS, Windows)
    *   Architecture (e.g., `x86_64`, `amd64`, `aarch64`, `arm64`)
    *   Python Version (e.g., `cp310` for Python 3.10, `cp311` for Python 3.11)
    *   Backend (indicated in the filename, e.g., `cpu`, `cu121`, `metal`)
4.  Download the wheel file.
5.  Install it using pip:
    ```bash
    pip install /path/to/downloaded/llama_cpp_python-...-....whl
    ```

## Supported Configurations

This table outlines the configurations we aim to build wheels for. Status may vary based on CI runner availability and backend complexity. Please check the [Releases Page](https://github.com/ParisNeo/llama-cpp-python-wheels/releases) for the definitive list of available wheels.

| OS      | Architecture | Python Version(s) | Backend         | CMake Flags (Example)                        | Status       | Index Suffix |
| :------ | :----------- | :---------------- | :-------------- | :------------------------------------------- | :----------- | :----------- |
| Linux   | `x86_64`     | 3.9, 3.10, 3.11, 3.12 | CPU (OpenBLAS)  | `-DGGML_BLAS=ON -DGGML_BLAS_VENDOR=OpenBLAS` | ✅ Available | `cpu`        |
| Linux   | `aarch64`    | 3.9, 3.10, 3.11, 3.12 | CPU (OpenBLAS)  | `-DGGML_BLAS=ON -DGGML_BLAS_VENDOR=OpenBLAS` | ✅ Available | `cpu`        |
| Windows | `AMD64`      | 3.9, 3.10, 3.11, 3.12 | CPU (OpenBLAS)  | `-DGGML_BLAS=ON -DGGML_BLAS_VENDOR=OpenBLAS` | ✅ Available | `cpu`        |
| macOS   | `x86_64`     | 3.9, 3.10, 3.11, 3.12 | CPU (OpenBLAS)  | `-DGGML_BLAS=ON -DGGML_BLAS_VENDOR=OpenBLAS` | ✅ Available | `cpu`        |
| macOS   | `arm64`      | 3.9, 3.10, 3.11, 3.12 | CPU (OpenBLAS)  | `-DGGML_BLAS=ON -DGGML_BLAS_VENDOR=OpenBLAS` | ✅ Available | `cpu`        |
| macOS   | `arm64`      | 3.9, 3.10, 3.11, 3.12 | Metal           | `-DGGML_METAL=on`                            | ✅ Available | `metal`      |
| Linux   | `x86_64`     | 3.9, 3.10, 3.11, 3.12 | CUDA 11.8       | `-DGGML_CUDA=on ...`                         | ⏳ Planned   | `cu118`      |
| Linux   | `x86_64`     | 3.9, 3.10, 3.11, 3.12 | CUDA 12.1       | `-DGGML_CUDA=on ...`                         | ⏳ Planned   | `cu121`      |
| Linux   | `x86_64`     | 3.9, 3.10, 3.11, 3.12 | ROCm (hipBLAS)  | `-DGGML_HIPBLAS=on`                          | 🚧 Experimental | `rocm`       |
| Linux   | `x86_64`     | 3.9, 3.10, 3.11, 3.12 | Vulkan          | `-DGGML_VULKAN=on`                           | 🚧 Experimental | `vulkan`     |
| Windows | `AMD64`      | 3.9, 3.10, 3.11, 3.12 | CUDA 11.8       | `-DGGML_CUDA=on ...`                         | ⏳ Planned   | `cu118`      |
| Windows | `AMD64`      | 3.9, 3.10, 3.11, 3.12 | CUDA 12.1       | `-DGGML_CUDA=on ...`                         | ⏳ Planned   | `cu121`      |

*(✅ = Generally Available, ⏳ = Planned/In Progress, 🚧 = Experimental/May Require Specific Setup)*

## How it Works

This repository uses GitHub Actions and [`cibuildwheel`](https://github.com/pypa/cibuildwheel) to automate the build process.

1.  A workflow (`.github/workflows/build-wheels.yml`) checks out the specified version of `abetlen/llama-cpp-python`.
2.  It runs `cibuildwheel` across a matrix of target operating systems, architectures, Python versions, and backend configurations.
3.  Required dependencies and CMake arguments (`CMAKE_ARGS`) specific to each backend are set during the build.
4.  Successfully built wheels are uploaded as artifacts.
5.  A final job gathers all wheels and uploads them to a GitHub Release.
6.  (If configured) Another step updates the simple index on the `gh-pages` branch for the `--extra-index-url` method.

## Contributing

Contributions are welcome! Please feel free to open an Issue or Pull Request if you notice problems, have suggestions for improvement, or want to help add support for new platforms or backends.

*   **Reporting Issues:** If a wheel doesn't work or a build fails, please provide details about your OS, Python version, architecture, and the exact command you used.
*   **Adding Backends:** Adding support for complex backends like CUDA or ROCm often requires specific CI runner setup or complex installation scripts. Contributions in this area are highly appreciated.

## License

The code and workflows within *this* repository (`ParisNeo/llama-cpp-python-wheels`) are licensed under the [**Apache License 2.0**](LICENSE).

The underlying `llama-cpp-python` package is distributed under the [MIT License](https://github.com/abetlen/llama-cpp-python/blob/main/LICENSE.md). The wheels built by this repository contain the compiled code from `llama-cpp-python` and its dependencies (like `llama.cpp`), which are subject to their respective licenses (primarily MIT).

## Acknowledgements

*   Huge thanks to **[@abetlen](https://github.com/abetlen)** for creating and maintaining `llama-cpp-python`.
*   Thanks to **[@ggerganov](https://github.com/ggerganov)** and all contributors to the core `llama.cpp` project.