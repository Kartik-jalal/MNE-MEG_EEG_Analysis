# MNE-M/EEG_Analysis
This repository documents my work following the M/EEG analysis with MNE Python tutorial from [Richard Höchenberger's Pybrain workshop](https://www.youtube.com/watch?v=t-twhNqgfSY&t=423s).
<br />
<br />
The original workshop code is available in this [Github repo](https://github.com/hoechenberger/pybrain_mne/), and the datasets can be downloaded from [Google Drive](https://drive.google.com/drive/folders/1uxBHfSZd8r7JpFP-wnFBv_goBMAin6EJ).


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

To make sure MNE-Python was installed correctly, type the following command in a terminal:
```bash
# 1. Activate the venv
source .venv/bin/activate

# 2. display mne setup system information
python -c "import mne; mne.sys_info()"
```

This should display some system information along with the versions of MNE-Python and its dependencies. Typical output looks like this:
```bash
Platform                Windows-10-10.0.20348-SP0
Python                  3.10.12 | packaged by conda-forge | (main, Jun 23 2023, 22:34:57) [MSC v.1936 64 bit (AMD64)]
Executable              C:\Miniconda3\envs\mne\python.exe
CPU                     Intel64 Family 6 Model 85 Stepping 7, GenuineIntel (2 cores)
Memory                  7.0 GB

Core
├☑ mne                  1.6.0.dev67+gb12384562
├☑ numpy                1.25.2 (OpenBLAS 0.3.23.dev with 1 thread)
├☑ scipy                1.11.2
├☑ matplotlib           3.7.2 (backend=QtAgg)
├☑ pooch                1.7.0
└☑ jinja2               3.1.2

Numerical (optional)
├☑ sklearn              1.3.0
├☑ nibabel              5.1.0
├☑ nilearn              0.10.1
├☑ dipy                 1.7.0
├☑ openmeeg             2.5.6
├☑ pandas               2.1.0
└☐ unavailable          numba, cupy

Visualization (optional)
├☑ pyvista              0.41.1 (OpenGL 3.3 (Core Profile) Mesa 10.2.4 (git-d92815a) via Gallium 0.4 on llvmpipe (LLVM 3.4, 256 bits))
├☑ pyvistaqt            0.0.0
├☑ ipyvtklink           0.2.2
├☑ vtk                  9.2.6
├☑ qtpy                 2.4.0 (PyQt5=5.15.8)
├☑ ipympl               0.9.3
├☑ pyqtgraph            0.13.3
└☑ mne-qt-browser       0.5.2

Ecosystem (optional)
└☐ unavailable          mne-bids, mne-nirs, mne-features, mne-connectivity, mne-icalabel, mne-bids-pipeline
```


# [Richard Höchenberger's Pybrain MNE submodule](./richard_höchenbergers_pybrain_mne/)
For reference, I have also added [Richard Höchenberger's Pybrain MNE git repo](https://github.com/hoechenberger/pybrain_mne/) as a submodule in this repo and to pull the submodule after cloning this repo, please do:
```bash
git submodule update --init
```

# Chapters

## [Chapter 1](./chapter_1.ipynb)
In this chapter we look at how to retrieve, read, visualise, extract important details, crop, filter and compute psd on the raw data using *mne*.

## [Chapter 2](./chapter_2.ipynb)
In this chapter we will be working with [**Brain Imaging Datastructure (BIDS)**](https://bids-specification.readthedocs.io/en/stable/), it was built to organise *MRI* datasets and make them manageable and recenlty it has been amended for *EEG/MEG* datastorage as well.

## [Chapter 3](./chapter_3.ipynb)
In this chapter we will focus on creating epochs and avaraging these epochs to generate evoked responses (ERP/ERF).

## [Chapter 4](./chapter_4.ipynb)
In this chapter we will look into how to remove ECG, EOG artefacts from our epoched data using **'amplitude based critia'**, **'SSP'** and **'ICA'**.

## [Chapter 5](./chapter_5.ipynb)
This chapter covers loading pre-processed EEGLAB data and applying a standard montage to define sensor locations.

## [Chapter 6](./chapter_6.ipynb)
This chapter covers Spatio-Temporal decoding and Temporal decoding (Sliding Estimator) using Machine learning techniques with the help of `mne.decodding` and **Scikit-Learn**.

# Update Logs

## 09th of Jan, 2025

> ### 10:15 pm (IST)
> #### New:
>   + Added [Chapter 6](./chapter_6.ipynb) jupyter notebook.
>   + Added [Temporal Decoding time course plot](./imgs/temporal_decoding_res.png) used in [Chapter 6](./chapter_6.ipynb) jupyter notebook.
>
> #### Updates:
>   + Updated the [README.md](./README.md).

## 03th of Jan, 2025

> ### 10:41 pm (IST)
> #### New:
>   + Added [Chapter 5](./chapter_5.ipynb) jupyter notebook.
>
> #### Updates:
>   + Updated the [README.md](./README.md).
>   + Updated [.gitignore](./.gitignore).


## 02th of Jan, 2025

> ### 12:53 am (IST)
> #### New:
>   + Added [Chapter 4](./chapter_4.ipynb) jupyter notebook.
>   + Added [imgs](./imgs) dir - which contains images used in the notebooks.
>
> #### Updates:
>   + Updated [Chapter 1](./chapter_1.ipynb), [Chapter 2](./chapter_2.ipynb) and [Chapter 3](./chapter_3.ipynb) jupter notebooks - change the `matplotlib` backend to `QtAgg` from `Qt5Agg`, and also put `import mne_bids` in the next cell of *Libraries & Config* section to fix the *Qt* conflict.

## 10th of Dec, 2025

> ### 09:03 pm (IST)
> #### New:
>   + Added [Chapter 3](./chapter_3.ipynb) jupyter notebook.


## 09th of Dec, 2025

> ### 06:40 pm (IST)
> #### New:
>   + Added [Chapter 2](./chapter_2.ipynb) jupyter notebook.
>
> #### Updates:
>   + Updated the [reqs.txt](./reqs.txt), with a new python lib. <code style="color : yellow">Please update your python venv, the easist way for the moment would be:</code>
>> ```bash
>> # 1. Activate the venv
>> source .venv/bin/activate
>>
>> # 2. Install the new/updated dependencies
>> pip install -r reqs.txt
>> ```
>   + Updated the [README.md](./README.md).
>   + Updated [.gitignore](./.gitignore).
>   + Updated [Chapter 1](./chapter_1.ipynb) jupyter notebook.

## 29th Of Nov, 2025

> ###  07:46 pm (IST)
> #### New:
>   + Added [Chapter 1](./chapter_1.ipynb) jupyter notebook.
>   + Added Richard's provided github repo containing his workshop notebooks for quick references.
>
> #### Updates:
>   + Updated the [README.md](./README.md).
>   + Updated [.gitignore](./.gitignore).

## 25th Of Nov, 2025

> ###  11:38 pm (IST)
> #### Updates:
>   + Updated the [README.md](./README.md) file Setup instructions.

> ###  10:41 pm (IST)
> #### Updates:
>   + Updated the [README.md](./README.md) file enable CUDA in MNE instructions.

> ###  09:20 pm (IST)
> #### Updates:
>   + Updated the [reqs.txt](./reqs.txt), with a new python lib. <code style="color : yellow">Please update your python venv, the easist way for the moment would be:</code>
>> ```bash
>> # 1. Activate the venv
>> source .venv/bin/activate
>>
>> # 2. Install the new/updated dependencies
>> pip install -r reqs.txt
>> ```
>   + Updated the [README.md](./README.md) file enable CUDA in MNE instructions.


> ###  09:30 pm (IST)
> #### Updates:
>   + Updated the [README.md](./README.md) file *cupy* install instructions.

> ###  09:20 pm (IST)
> #### Updates:
>   + Updated the [reqs.txt](./reqs.txt), with a new python lib. <code style="color: yellow">Please update your python venv, the easist way for the moment would be:</code>
>> ```bash
>> # 1. Activate the venv
>> source .venv/bin/activate
>>
>> # 2. Install the new/updated dependencies
>> pip install -r reqs.txt
>> ```
>   + Updated the [README.md](./README.md) file.


## 24th Of Nov, 2025

> ###  07:16 pm (IST)
> #### New:
> + Added [reqs.txt](./reqs.txt), containing necessary python libs for the venv.
>
> #### Updates:
>   + Updated the [README.md](./README.md) file.
