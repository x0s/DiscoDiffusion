# Migration from machine to machine

## On host machine

```
### on host machine
# we archive tne environment with conda-pack
$ conda install -c conda-forge conda-pack

# Get directory where env is stored
conda info --envs

# Pack environment disco_v5 into disco_v5.tar.gz
$ conda pack -n disco_v5
```

## On receiving machine

Prerequisites:
- Install anaconda https://www.anaconda.com/products/distribution
- Install git
- Install ffmpeg
 1. Download ffmpeg [here](https://www.gyan.dev/ffmpeg/builds/ffmpeg-release-full.7z)
 2. Extract archive in `C:\programData\ffmpeg` for instance
 3. Add `C:\programData\ffmpeg\bin`to Windows `PATH` environment variable
 4. Type `ffmpeg -version` in CLI to check it's working

#### 1. Copy whole project
```
# Make sure you have at least 40GB available
# Download "DiscoDiffusion" from NAS at TS_prod/SERVICE/2022-04 AI research/backup_migration/
# Unzip the archive in YOUR_PROJECT_PATH (ex: C:\Users\your_name\Project)
```

#### 2. Set the virtual environment
```
# Open anaconda3 prompt from Window menu
# Then, untar environment archive disco_v5.tar.gz in anaconda env directory (works on Windows):
$ cd %CONDA_PREFIX%\envs
$ mkdir disco_v5
$ tar -xzf YOUR_PROJECT_PATH\DiscoDiffusion\disco_v5.tar.gz -C disco_v5
$ activate disco_v5
$ conda-unpack
```

#### 3. Pull last version of notebook from repo

If you don't have access internet on host machine, it's better to fetch&merge last version on host machine before packing the environment
```
# Go to your project
$ cd YOUR_PROJECT_PATH\DiscoDiffusion

$ Set your git credentials
$ git config user.name "Your Name"
$ git config user.email "youremail@provider.com"

# get last version of notebook from repo
$ git fetch origin
$ git checkout main
$ git merge origin/main
```

## Troubleshooting
```
# if Jupyter still points to python version (not the python in active env :/)
$ conda install -c conda-forge jupyterlab --force-reinstall

# Or without internet, use active python (in env)
$ python -m jupyter lab
```
