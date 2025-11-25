# MNE-M/EEG_Analysis
This Repo is for the work-through of M/EEG analysis with MNE Python following [Richard Höchenberger's workshop](https://www.youtube.com/watch?v=t-twhNqgfSY&t=423s).


# Setup
Unlike the *conda virtual environment setup* [Richard Höchenberger mentioned in this workshop](https://www.youtube.com/watch?v=t-twhNqgfSY&t=423s), we will setup a *python virtual environment (venv)* using [MNE Advanced Setup](https://mne.tools/stable/install/advanced.html#advanced-setup):
```bash
# 1. Create the venv
python3 -m venv .venv

# 2. Activate the venv
source .venv/bin/activate

# 3. Install dependencies
pip install -r reqs.txt
```

After the setup is complete, if you have a **GPU** and would like **MNE-Python** to utilize [NVIDIA CUDA GPU processing](https://developer.nvidia.com/cuda-zone) to speed up some operations (e.g. *FIR filtering*) by roughly an order of magnitude, then do:

```bash
# 1. Activate the venv
source .venv/bin/activate

# 2. Install Cupy (Note: This install is for CUDA version 13, if you have different version of cuda please have a look here: https://docs.cupy.dev/en/stable/install.html)
pip install cupy-cuda13x

# 3. Permanently enable CUDA in MNE
python3 -c "import mne; mne.utils.set_config('MNE_USE_CUDA', 'true')"
```

> _**Note:** If the **cupy** installs all correctly, then **CUDA** should work in **MNE**. You can use CUDA in methods that state that they allow passing `'n_jobs='cuda'`, such as `mne.io.Raw.filter()` and `mne.io.Raw.resample()`, and they should run faster than the CPU-based multithreading such as `n_jobs=8`._

# Update Logs

## 25th Of Nov, 2025

> ###  10:41 pm (IST)
> #### Updates:
>   + Updated the [README.md](./README.md) file enable CUDA in MNE instructions.


> ###  09:20 pm (IST)
> #### Updates:
>   + Updated the [reqs.txt](./reqs.txt), with a new python lib. <span style="color: red;">Please update your python venv, the easist way for the moment would be:</span>
> ```bash
> # 1. Activate the venv
> source .venv/bin/activate
>
> # 2. Install the new/updated dependencies
> pip install -r reqs.txt
> ```
>   + Updated the [README.md](./README.md) file enable CUDA in MNE instructions.


> ###  09:30 pm (IST)
> #### Updates:
>   + Updated the [README.md](./README.md) file *cupy* install instructions.

> ###  09:20 pm (IST)
> #### Updates:
>   + Updated the [reqs.txt](./reqs.txt), with a new python lib. <span style="color: red;">Please update your python venv, the easist way for the moment would be:</span>
> ```bash
> # 1. Activate the venv
> source .venv/bin/activate
>
> # 2. Install the new/updated dependencies
> pip install -r reqs.txt
> ```
>   + Updated the [README.md](./README.md) file.


## 24th Of Nov, 2025

> ###  07:16 pm (IST)
> #### New:
> + Added [reqs.txt](./reqs.txt), containing necessary python libs for the venv.
>
> #### Updates:
>   + Updated the [README.md](./README.md) file.
