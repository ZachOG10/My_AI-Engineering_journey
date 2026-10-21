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
Virtual environment	"A venv"	An isolated directory containing a Python interpreter and packages, separate from the system Python
Lockfile	"Pinned dependencies"	A file listing every package and its exact version, guaranteeing identical installs across machines
pyproject.toml	"The new setup.py"	The standard Python project configuration file, replacing setup.py/setup.cfg/requirements.txt
Transitive dependency	"A dependency of a dependency"	Package B depends on C; if you install A which depends on B, C is a transitive dependency of A
CUDA mismatch	"My GPU isn't working"	PyTorch was compiled for a different CUDA version than what your GPU driver supports

# Doker for AI