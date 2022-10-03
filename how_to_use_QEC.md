## syncronization to cluster

Unison synchronization: ` unison-hpc-qec-playground`

Force to sync to local version
`unison hpc-qec-playground -auto -batch -prefer /Users/pktsai/Desktop/pk/Yale/research/QEC-Playground`

## On cluster
### Build Rust Code
First request an interactive shell: 
`srun --pty -t 2:00:00 --mem=8G --cpus-per-task=4 -p interactive bash`.

In the shell run 
`cargo build --release` 
to compile.

### run something:
run.sh:


> `#!/bin/bash`
> `#SBATCH --job-name=JOB_NAME`
> `#SBATCH --out="slurm-%j.out"`
> `#SBATCH --error="slurm-%j.err"`
> `#SBATCH --time=5:00:00`
> `#SBATCH --nodes=1 --ntasks=1 --cpus-per-task=36 --mem=8G `
> `#SBATCH --mail-type=ALL`
> `echo -n "Start "`
> `srun <<command>>`
> `echo "done"`

and run `sbatch run.sh`


## rust command
`cargo run --release -- tool benchmark '[3]' '[4]' '[0.1]' --bias_eta 1e200 --code_type RotatedTailoredCode --decoder tailored-mwpm --decoder_config '{"pcmg":true,"naive_residual_decoding":true}' --error_model tailored-sc-bell-init-phenomenological -m1000000 -e20000 -p0 --time_budget 7200 --ignore_logical_j;`