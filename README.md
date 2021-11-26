# Local Conda environments via Singularity

How to fetch the image:
```
$ singularity pull https://github.com/bast/singularity-conda/releases/download/0.2.0/conda.sif
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

---

I have used this wonderful guide as starting point and inspiration:
https://github.com/singularityhub/singularity-deploy
