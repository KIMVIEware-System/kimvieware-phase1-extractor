# kimvieware-phase1-extractor
This service is responsible for extracting symbolic execution paths from Systems Under Test (SUTs) for various programming languages.

## Setup and Dependencies

### Python Dependencies
Install the required Python packages:
```bash
pip install -r requirements.txt
```

### libclang Setup (for C/C++ Extraction)
The C/C++ extractor (`src/extractors/c_extractor.py`) relies on `libclang` for parsing C/C++ code. `libclang` is part of the LLVM project.

**Important:** You need to have LLVM/Clang installed on your system.
On Ubuntu/Debian, you can install it via:
```bash
sudo apt update
sudo apt install clang-18 llvm-18-dev libclang-18-dev
```
Or use the official LLVM repositories for the latest versions.

The `c_extractor.py` attempts to find `libclang.so` in common locations. If it fails, you might need to set the `CLANG_LIBRARY_PATH` environment variable to the directory containing your `libclang.so` file before running the service.

Example:
```bash
export CLANG_LIBRARY_PATH=/usr/lib/llvm-18/lib/
# Then run the extractor service
python src/extractor_service.py
```

## Environment Variables
*   `EXTRACTOR_MAX_PATHS`: Maximum number of paths to extract per job (default: 1000). Set this to control resource usage.

## Usage
Run the extractor service:
```bash
python src/extractor_service.py
```
This service will listen for messages on the `validation.completed` RabbitMQ queue.