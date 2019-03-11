# Singularity image definition for FSL

Making it easier to start using [FSL](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/) on e.g. HPC.

[![https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg](https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg)](https://singularity-hub.org/collections/2514)

## License

See [LICENSE.txt](LICENSE.txt), particularly the conditions regarding commercial use.

## Running FSL within a Singularity container using this Singularity image definition 

The quickest way to start using FSL via this Singularity image is to 
pull the image from the [SingularityHub](http://singularity-hub.org/) on-line repository:

```sh
export SINGULARITY_CACHEDIR="/home/$USER/singularity_cache"
mkdir -p "${SINGULARITY_CACHEDIR}"
singularity pull --name fsl-debian-stretch-singularity-latest.sif shub://rses-singularity/fsl-debian-stretch-singularity:latest 
singularity exec "${SINGULARITY_CACHEDIR}/fsl-debian-stretch-singularity-latest.sif" /bin/bash
```

After running `singularity exec` you are then able to run commands 'within' a FSL 'container' e.g. 
`fsl-selftest` or `fsl5.0-gps`. Note that most FSL commands start with `fsl5.0-`.

A note re SingularityHub: the [FSL image provided via SingularityHub](https://www.singularity-hub.org/collections/2514) is 
rebuilt whenever there is a push to this GitHub repository.

## Building a Singularity image and running a FSL container *without* using SingularityHub

If you don't want to use the SingularityHub-built image then you can build it yourself **on your own machine** (not HPC):

 1. Make sure you have Singularity installed.
 1. Ensure you're read the [FSL license](LICENSE.txt).
 1. Inspect the [Singularity image definition in this repo](Singularity); this includes steps to:
      - Install FSL.
      - Install the [FSL Evaluation and Example Data Suite (FEEDS)](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FEEDS).
 1. Start building an image file:
    ```sh
    sudo SINGULARITY_TMPDIR=$HOME/.cache/singularity singularity build ./fsl-debian-stretch-singularity.sif ./Singularity
    ```

To start a FSL container using this image:

```sh
singularity exec ./fsl-debian-stretch-singularity.sif /bin/bash
```

then from the resulting shell start the FSL command you want to use.

## Testing FSL inside a container

Run:

```sh
fsl-selftest
```
