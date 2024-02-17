# Local Conda environments via Singularity

The nice thing about this approach is that you don't need to install Conda and
you don't need to modify your environment/bashrc/settings.

I use it to install dependencies that may be tough to install on a
supercomputer or on my NixOS environment.

How to fetch the image:
```
$ singularity pull https://github.com/bast/singularity-conda/releases/download/0.6.0/conda.sif
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

First time you run either of the above commands it will take a bit of time
since it needs to install the dependencies into the `environment` folder.
However, subsequent runs will start basically immediately since the environment
is then there.


## Micromamba and environment files

Under the hood, it uses
[Micromamba](https://mamba.readthedocs.io/en/latest/user_guide/micromamba.html)
instead of Conda in order to speed up installations but it should not really
matter for the functionality.

The one place where I found it to matter is that you have to specify `channels`
in the environment file.

Instead of this (example taken from [conda
documentation](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#create-env-file-manually)):
```yaml
name: stats
dependencies:
  - numpy
  - pandas
```
You need to do this:
```yaml
name: stats
channels:
  - defaults
dependencies:
  - numpy
  - pandas
```

But I believe that specifying channels explicitly is anyway good practice.


## Running on a supercomputer/cluster

On a cluster you might need to bind folders like here:
```
$ env SINGULARITY_BIND="/cluster" ./conda.sif python
```

---

I have used this wonderful guide as starting point and inspiration:
https://github.com/singularityhub/singularity-deploy
