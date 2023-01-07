# Local Conda environments via Singularity

The nice thing about this approach is that you don't need to install Conda and
you don't need to modify your environment/bashrc/settings.

I use it to install dependencies that may be tough to install on a
supercomputer or on my NixOS environment.

How to fetch the image:
```
$ singularity pull https://github.com/bast/singularity-conda/releases/download/0.3.0/conda.sif
```

## Usage

- Reads the Conda environment file
  [environment.yml](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#create-env-file-manually).
- Creates the folder `environment`.

Run `myscript.py` inside the Conda environment defined by `environment.yml`:
```
$ ./conda.sif python myscript.py
```

Open Python shell inside the Conda environment defined by `environment.yml`:
```
$ ./conda.sif python
```

When running for the first time (and thus installing the environment),
the installer will inform you that:
```
# To activate this environment, use
#
#     $ conda activate /home/user/example/environment
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```
But you can ignore this. The container image will automatically activate the
environment for you.

First time you run either of the above commands it will take a bit of time
since it needs to install the dependencies into the `environment` folder.
However, subsequent runs will start basically immediately since the environment
is then there.

---

I have used this wonderful guide as starting point and inspiration:
https://github.com/singularityhub/singularity-deploy
