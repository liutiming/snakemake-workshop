# Guide to snakemake on Sanger 5
## installation 
### install snakemake 

#### create conda env
```
conda create --prefix FULL-PATH 
e.g.
conda create --prefix /lustre/scratch119/realdata/mdt2/teams/martin/users/tl11/snakemake_env
```
#### install mamba
`conda install -c conda-forge mamba`

#### install snakemake 
`mamba install snakemake `

#### install snakemake profile 
`mamba install -c conda-forge cookiecutter`

```
# create configuration directory that snakemake searches for profiles
profile_dir="${HOME}/.config/snakemake"
mkdir -p "$profile_dir"
# use cookiecutter to create the profile in the config directory
template="gh:Snakemake-Profiles/lsf"
cookiecutter --output-dir "$profile_dir" "$template"
```

#### profile setting (required by the step above)
```
LSF_UNIT_FOR_LIMITS=MB

jobscript: "lsf_jobscript.sh"
use-conda: "True"
use-singularity: "False"
printshellcmds: "True"
restart-times: "0"
jobs: "500"
cluster: "lsf_submit.py"
cluster-status: "lsf_status.py"
max-jobs-per-second: "10"
max-status-checks-per-second: "10"
```

### set up for workshop  
#### prepare a directory
```
$ mkdir snakemake-tutorial
$ cd snakemake-tutorial
$ wget https://github.com/snakemake/snakemake-tutorial-data/archive/v5.24.1.tar.gz
$ tar --wildcards -xf v5.24.1.tar.gz --strip 1 "*/data" "*/environment.yaml"
```

#### create workshop env
```
mamba env create --prefix=../snakemake_tutorial_env --file environment.yaml
```

## common snakemake command 
```
-n
dry run 

-s
choose snakemake file e.g. extraction.smk 

-f
force run 

--profile 
choose a profile (needed for submit jobs on farm)
```

