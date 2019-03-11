# Singularity image definition for FSL

Making it easier to start using [FSL](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/) on e.g. HPC.

## License

See [LICENSE.txt](LICENSE.txt), particularly the conditions regarding commercial use.

## Preparations

1. Make sure you have Singularity installed.
2. Ensure you're read the [FSL license](LICENSE.txt).
4. If `/tmp` is 'small' (e.g. 'only' 16GB) then Singularity will run out of space when trying to build your image, 
   so you may want to create a directory somewhere else for Singularity to write temporary files to:

    ```sh
    mkdir -p -m 0700 $HOME/.cache/singularity 
    ```
## Building the image

The build process as defined in our `Singularity` file installs 
FSL plus 
the [FSL Evaluation and Example Data Suite (FEEDS)](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FEEDS).

```sh
sudo SINGULARITY_TMPDIR=$HOME/.cache/singularity singularity build ./fsl-debian-stretch-singularity.sif ./Singularity
```

## Starting FSL inside a container

To run the container from this image:

```sh
singularity exec ./fsl-debian-stretch-singularity.sif /bin/bash
```

then from the resulting shell start the FSL command you want to use.

## Testing FSL inside a container

Run:

```sh
fsl-selftest
```
