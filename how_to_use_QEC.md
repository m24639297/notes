## syncronization to cluster

Unison synchronization: 
`unison-hpc-qec-playground`

Force to sync to local version
`unison hpc-qec-playground -auto -batch -prefer /Users/pktsai/Desktop/pk/Yale/research/QEC-Playground`

## On cluster
### Build Rust Code
First request an interactive shell: 
`srun --pty -t 2:00:00 --mem=8G --cpus-per-task=4 -p interactive bash`.

(new version?)
`salloc -t 2:00:00 --mem=8G`

In the shell run 
`cargo build --release` 
to compile.

### run something:
run.sh:

`#!/bin/bash`

`#SBATCH --job-name=JOB_NAME`

`#SBATCH --out="JOB_NAME_%a.out"`

`#SBATCH --error="JOB_NAME_%a.err"`

`#SBATCH --time=12:00:00`

`#SBATCH --nodes=1 --ntasks=1 --cpus-per-task=4 --mem=8G`

`#SBATCH --array=1-10`

`#SBATCH --mail-type=END,FAIL`

`if [ $SLURM_ARRAY_TASK_ID -eq 1 ]`

`then `

`    srun cargo run ...`

`fi`

and run `sbatch run.sh`


## rust command
`cargo run --release -- tool benchmark '[17,19]' '[1,1]' '[0.2]' --bias-eta 1000 --code-type rotated-tailored-code --decoder tailored-mwpm --decoder-config '{"pcmg":true,"naive_residual_decoding":true}' --noise-model tailored-sc-bell-init-phenomenological -m10000000 -e20000 -p0 --time-budget 30 --ignore-logical-j`

help: `cargo run --release -- tool benchmark --help`
