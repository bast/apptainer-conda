# Local Conda environments via Singularity

How to fetch the image:
```
$ singularity pull https://github.com/bast/singularity-conda/releases/download/0.3.0/conda.sif
```

## Usage

- Reads: `environment.yml`
- Creates: `environment` (folder)

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

---

I have used this wonderful guide as starting point and inspiration:
https://github.com/singularityhub/singularity-deploy
