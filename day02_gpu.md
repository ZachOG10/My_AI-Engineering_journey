# uv venv (Recommended)
uv is the fastest Python package manager (10-100x faster than pip). It handles virtual environments, Python versions, and dependency resolution in one tool.

# venv (Built-in)
If you can't install uv, Python ships with venv. 
It is slower than uv, but works everywhere Python is installed.

# conda (When You Need It)
Conda manages non-Python dependencies like CUDA toolkits, cuDNN, and C libraries. Use it when:
- You need a specific CUDA toolkit version without installing it system-wide
- You're on a shared cluster where you can't install system packages
- A library's install instructions say "use conda"
# One rule:
* if you use conda for an environment, use conda for all packages in that environment. Mixing pip install into a conda env causes dependency conflicts that are painful to debug.
# CUDA (Compute Unified Device architecture)

# Lockfiles:
A lockfile pins every dependency (including transitive ones) to exact versions. This guarantees reproducibility: anyone who installs from the lockfile gets exactly the same packages.

# Key Terms
    Term	What people say	What it actually means
* Virtual environment	"A venv"	An isolated directory containing a Python interpreter and packages, separate from the system Python
* Lockfile	"Pinned dependencies"	A file listing every package and its exact version, guaranteeing identical installs across machines
* pyproject.toml	"The new setup.py"	The standard Python project configuration file, replacing setup.py/setup.cfg/requirements.txt
* Transitive dependency	"A dependency of a dependency"	Package B depends on C; if you install A which depends on B, C is a transitive dependency of A
* CUDA mismatch	"My GPU isn't working"	PyTorch was compiled for a different CUDA version than what your GPU driver supports

# Doker for AI
* Docker wraps your code, runtime, libraries, and system tools into an isolated unit called a container. Think of it as a lightweight virtual machine, except it shares the host OS kernel instead of running its own, so it starts in seconds instead of minutes.

# AI projects need Docker more than most
* GPU drivers are fragile. CUDA 12.4 code does not run on CUDA 11.8. Docker isolates the CUDA toolkit inside the container while sharing the host GPU driver through the NVIDIA Container Toolkit.
* Model weights are large. A 7B parameter model is 14 GB in fp16. You do not want to re-download it every time you rebuild. Docker volumes let you mount a models directory from the host.
* Multi-service architectures are common. A real AI application is not just a Python script. It is an inference server, a vector database for RAG, maybe a web frontend. Docker Compose orchestrates all of these with one command.

## Key vocabulary
    Term	What it means
*   Image	A read-only template. Your recipe. Built from a Dockerfile.
*   Container	A running instance of an image. Your kitchen.
*   Dockerfile	Instructions to build an image. Layer by layer.
* Volume	Persistent storage that survives container restarts.
* docker-compose	A tool for defining multi-container applications in YAML.
# common container patterns in AI
- Dev container
- Training container
- Inference container

## Key Terms
    Term	        What people say	            What it actually means
* Container	        "Lightweight VM"	An isolated process using the host kernel, with its own filesystem and network
* Image layer	    "Cached step"	Each Dockerfile instruction creates a layer. Unchanged layers are cached, so rebuilds are fast.
* NVIDIA Container Toolkit	"GPU in Docker"	A runtime hook that exposes host GPUs to containers via --gpus flag
* Volume mount  	"Shared folder"	A directory on the host mapped into the container. Changes persist after the container stops.
* Base image	    "Starting point"	The FROM image your Dockerfile builds on top of. Determines what is pre-installed.

## Data management

- Data is fuel, how you mange it determines how fast you go.
# Data splits
Every ML project needs three splits:

1. Train: The model learns from this (typically 80%)
2. Validation: You check progress during training (typically 10%)
3. Test: Final evaluation after training is done (typically 10%)

# Terminal and shell
# Terminal is where AI engineers live, get comfortable here.

# The three redirects you need:

# Symbol	What it does
- >	    Write stdout to file (overwrite)
- >>	Append stdout to file
- 2>	Write stderr to file
- 2>&1	Send stderr to same place as stdout
- |	    Send stdout of one command as stdin to the next

# The difference between &, nohup, and screen/tmux:

# Method	Survives terminal close?	Can reattach?
- command &	            No	                   No
- nohup command &	    Yes                No (check log file)
- screen / tmux	        Yes	                   Yes