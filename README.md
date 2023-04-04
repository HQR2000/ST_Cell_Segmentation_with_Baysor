# Spatial Transcriptomic Data Cell Segmentation with Baysor

## Content

- [Introduction](#index1)
- [Data](#index2)
- []()

## <span id = 'index1'>Introduction</span>

In this project we aims at creating a baseline for cell segmentation on spatial transcriptomic data using [Baysor](https://github.com/kharchenkolab/Baysor). 

Baysor is a tool for performing cell segmentation on imaging-based spatial transcriptomics data. It optimizes segmentation considering the likelihood of transcriptional composition, size and shape of the cell. 

In this project we will introduce the whole process of installing Baysor, setting up environmment and using Baysor for cell segmentation in a spatial transcriptomic dataset.

## <span id = 'index2'>Data</span>

The data we used as example is the mouse brain spatial transcriptomic data provided by BGI... It contains totally `24716264` transcripts with spatial location and the specific gene expression of the transcript.

Description of the dataset:

- **geneID:** The gene assocaited with the transcript

- **x, y:** These two columns are the spatial coordinates of the transcript

- **MIDCount:** It is a count of the number of unique molecular identifiers (UMIs) that map to a particular gene in a particular spot

![Example](https://github.com/HQR2000/ST_Cell_Segmentation_with_Baysor/blob/main/public/Example.png)

## Installation&Environmental Setting

During our experiment, the installation of Baysor and environmental setting leads to quite a lot problems. We tried several ways of using Baysor including using Docker, building CLI application source and downloading binary of Baysor but most of these methods couldn't work properly. 

After trying different combination of different packages, we finally comes up with a workable version of Baysor and we will introduce the whole process of environmental setting and an example of using Baysor to do cell segmentation in spatial transcriptomic data in the following pages. This example works properly on M1 Macbook Air with macOS Monterey 12.5.1.

### Packages Installation

**Miniconda**

For Macbook with M1 chips, we encourage to use Miniconda to install Python and other third parties library. The Miniconda installation can be found in [HERE](https://docs.conda.io/projects/conda/en/latest/user-guide/install).

**Libraries**

The third-party library will be used include:

- `pandas` is a popular data manipulation library for Python. It is used for data analysis, data cleaning, and data visualization.

After installing Miniconda, run the following code to create a virtual environment and install the libraries:

```
#Update of conda
conda update conda

#Create a virtual environment with `Python 3.9.12` for the project, replace [NAME] with the name you want for the virtual envrionment
conda create --name [NAME] python=3.9.12

#Activate the virtual environment
conda activate [NAME]

#Install libraries
conda install pandas

#Deactivate the virtual environment
conda deactivate [NAME]
```

 
 






