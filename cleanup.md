:construction: Under construction !!! :construction:

[[_TOC_]]

# Quotas on servers

Your `home`, `scratch` and the `project` folders in `/work/` have a quota for the number of files and occupied space

```bash
# occupied space and quotas
df -h
# number of files and quotas
df -h -i
```

To free up space:
- remove temporary data
- compress and archive not used data
  - compression: to save space
  - archiving: to reduce the number of files
- move data
  - final results: move to `XXXXX` (see [here](Dry-lab-guidelines#Data))
  - temporary/preliminary data: `scratch` (see [here](Dry-lab-guidelines#working-directory))

# Cleanup

## Conda

`conda` environments can be very large and contain a lot of files.

```bash
# list installed environments
conda info --envs
# remove not used environments
rm -r path/to/conda/env/
```

```bash
# remove unused packages and caches
conda remove --all
```

## Snakemake

*TODO*

- `.snakemake`
  - logs
  - conda env.s
  - meta files
  - ...

## Compressing and archiving data

*TODO: info and references*

- `zip`
- `tar`
- `gzip`, `pigz`
- `bzip2`, `pbzip2`

```bash
# tar: archive folder
tar -cvf path/to/archive.tar path/to/folder/
# tar: archive files
tar -cvf path/to/archive.tar /path/to/file1 /path/to/file2 ...

# tar: list contents
tar -tvf path/to/archive.tar

# extract archive
tar -xvf path/to/archive.tar
```

```bash
# zip: compress and archive folders
zip -r path/to/archive.zip path/to/folder/
# zip: compress and archive files
zip path/to/archive.zip /path/to/file1 /path/to/file2 ...

# zip: update an archive
zip -u path/to/archive.zip /path/to/file1 /path/to/file2 ...

# zip: list contents
unzip -l path/to/archive.zip

# zip: extract and decompress
unzip path/to/archive.zip
```

```bash
# gzip: compress files
TODO

# tar + pigz: archive and compress a folder
tar -cvf - path/to/folder/ | pigz --best -p {cpus} > path/to/archive.tar.gz

# tar + gzip: list contents
tar -ztvf path/to/archive.tar.gz

# tar + gzip: extract files
tar -zxvf path/to/archive.tar.gz
```

```bash
# bzip2
TODO

# pbzip2
TODO
```
