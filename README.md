# Spatial Transcriptomic Data Cell Segmentation with Baysor

![Segmentation](https://github.com/HQR2000/ST_Cell_Segmentation_with_Baysor/blob/main/public/segmentation.png)

## Content

- [Introduction](#index1)
- [Data](#index2)
- [Installation&Environmental Setting](#index3)
- [Running Baysor](#index4)

## <span id = 'index1'>Introduction</span>

In this project we aims at creating a baseline for cell segmentation on spatial transcriptomic data using [Baysor](https://github.com/kharchenkolab/Baysor). 

Baysor is a Julia package for performing cell segmentation on imaging-based spatial transcriptomics data. It optimizes segmentation considering the likelihood of transcriptional composition, size and shape of the cell. 

In this project we will introduce the whole process of installing Baysor, setting up environmment and a example of using Baysor for cell segmentation in the spatial transcriptomic data.

## <span id = 'index2'>Data</span>

The data we used as example is the mouse brain spatial transcriptomic data provided by BGI. It contains totally `24716264` transcripts with spatial location and the specific gene expression of the transcript.

Overview of the dataset:

- **geneID:** The gene assocaited with the transcript

- **x, y:** These two columns are the spatial coordinates of the transcript

- **MIDCount:** It is a count of the number of unique molecular identifiers (UMIs) that map to a particular gene in a particular spot

![Example](https://github.com/HQR2000/ST_Cell_Segmentation_with_Baysor/blob/main/public/Example.png)

## Installation&Environmental Setting

During our experiment, the installation of Baysor and environmental setting leads to quite a lot problems. We tried several ways of using Baysor including using Docker, building CLI application source and downloading binary of Baysor but most of these methods couldn't work properly. 

After trying different combination of different packages, we finally comes up with a workable version of Baysor and we will introduce the whole process of environmental setting and an example of using Baysor to do cell segmentation in spatial transcriptomic data in the following pages. This example works properly on M1 Macbook Air with macOS Monterey 12.5.1.

### <span id = 'index3'>Packages Installation</span>

**Miniconda**

For Macbook with M1 chips, we encourage to use Miniconda to install Python and other third parties library. 

The Miniconda installation can be found in [HERE](https://docs.conda.io/projects/conda/en/latest/user-guide/install).

**Libraries**

The third-party library will be used include:

- `pandas` is a popular data manipulation library for Python. It is used for data analysis, data cleaning, and data visualization.

After installing Miniconda, run the following code to create a virtual environment and install the libraries:

```
# Update of conda
conda update conda

# Create a virtual environment with `Python 3.9.12` for the project, replace [NAME] with the name you want for the virtual envrionment
conda create --name [NAME] python=3.9.12

# Activate the virtual environment
conda activate [NAME]

# Install libraries
conda install pandas

# Deactivate the virtual environment
conda deactivate [NAME]
```

After running the code above, you will have a virtual environment with:
- `Python` 3.9.12
- `pandas` 1.5.3

**Julia&Baysor Intallation**

Different ways to install and use Baysor can be found in [HERE](https://github.com/kharchenkolab/Baysor#installation). There are basically three ways to use Baysor: 

1. Binary download and use as Julia package 
2. Build CLI application from source
3. Use docker

However, each of these options have variable issues and problems caused by compatibility. 

Therefore, after testing various version of Julia and Baysor, we come up with a workable way to install Baysor on our machine. 

This instruction is also suitable for machine with Linux system and Macbook with M1 chip.

**Julia Installation**

Download **Julia v1.8.3** from [Julia v1.8.3](https://julialang.org/downloads/oldreleases/).(**Important!!!** For Macbook with M1 chip, download the `tar.gz` for `x86` but not `ARM64` architecture)

After unzipping the file, the binary of Julia v1.8.3 can be found in `~julia-1.8.3/bin`. Add the path to the $PATH by following the instruction [HERE](https://wpbeaches.com/how-to-add-to-the-shell-path-in-macos-using-terminal).

**Baysor-master Installation**

To download the Baysor-master .zip file from GitHub, run the following code:

```
# Download .zip file from GitHub
curl -L -O https://github.com/kharchenkolab/Baysor/archive/refs/heads/master.zip

# Unzip master.zip, change directory
unzip master.zip

# Move to the Baysor-master folder
cd Baysor-master
```

Then use Julia to compile Baysor-master by using the following code:

```
#Activate the Julia interactive interpreter
julia
```

If you meet the safety open problem on Macbook, following [this](https://support.apple.com/en-us/HT202491) instruction to allow the executation of the apps download from Internet.

When you successfully activate the Julia interactive interpreter, run the following code to compile Baysor-master:

```
using Pkg
Pkg.add(Pkg.PackageSpec(;name="PackageCompiler"))
Pkg.activate(".")
Pkg.instantiate()

# Exit Julia
exit()

# Compile Baysor-master
julia ./bin/build.jl
```

After compiling Baysor-master, you can now see the `Baysor` binary in the `~Baysor-master/Baysor/bin` folder, add this folder to your $PATH as what we've done for Julia v1.8.3.

Then, you should now be able to run Baysor on your machine. To check whether the installation is successful, type `Baysor -h` to see whether you have the help text for Baysor like this:

```
Usage: baysor <command> [options]

Commands:
        run             run segmentation of the dataset
        preview         generate preview diagnostics of the dataset

```

If you see this message on your screen, you have successfully installed Baysor on your machine.

## <span id = 'index4'>Running Baysor</span>

Now you can use Baysor to do cell segmentation on spatial transcriptomic dataset.

## Preview

As the help text of Baysor mentioned, there is a `preview` option for Baysor, which allows you to have an overview of the dataset.

By running the `baysor preview` option on your dataset, Baysor will come up with a **preview.html** containing the transcript, noise level and gene structure plots. 

An example running of `baysor preview` looks like follow:

```
Baysor preview -x [x] -y [y] -g [geneID] [ST.csv]
```

In the command, you should replace `[x]`, `[y]` with the corresponding coordinates in your spatial transcriptomic data and [geneID] with the gene expression for the transcript. The `[ST.csv]` should be the location of your spatial transcriptomic data in `.csv` format.

## Formal Run

The `baysor run` option is actually running hundreds of iterations to wait for the result to convergence, therefore it requires extremely large memory and a long time for the computing. If your memory is not enough for the computing, the program will kiiled itself automatically. So if you decide to have a formal run using Baysor, please make sure you have enough memory on your machine.

A formal run of Baysor looks like follow:

```
Baysor run -x [x] -y [y] -g [geneID] -m 15 -s 3 -p [ST.csv]
```

Just like the `baysor preview` option, you should replace `[x]`, `[y]` and `[geneID]` with the coordinates and gene expression of the transcripts in your spatial transcriptomic dataset. 

Besides, there are another two parameters should be manually set. The first one is `-m`, which stands for the minimum number of molecules for a cell. And the second one, `-s`, refer to the expected radius of a cell, and in the paper of Baysor, the author encourage to set it with a value `3`.





 
 






