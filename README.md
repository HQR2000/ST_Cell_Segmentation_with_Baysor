# Spatial Transcriptomic Data Cell Segmentation with Baysor

## Introduction

In this project we aims at creating a baseline for cell segmentation on spatial transcriptomic data using [Baysor](https://github.com/kharchenkolab/Baysor). 

Baysor is a tool for performing cell segmentation on imaging-based spatial transcriptomics data. It optimizes segmentation considering the likelihood of transcriptional composition, size and shape of the cell. In this project we will introduce the whole process of installing Baysor, setting up environmment and using Baysor for cell segmentation in a spatial transcriptomic dataset.

##Data

The data we used as example is the mouse brain spatial transcriptomic data provided by BGI... It contains totally `24716264` transcripts with spatial location and the specific gene expression of the transcript.

Description of the dataset:

  -**geneID:** The gene assocaited with the transcript

  -**x, y:** These two columns are the spatial coordinates of the transcript

  -**MIDCount:** It is a count of the number of unique molecular identifiers (UMIs) that map to a particular gene in a particular spot






