# PyData - Santiago #2

This tutorial contains 2 notebooks `Presentation.ipynb` and `NycTaxi.ipynb`.

## Presentation 
On the first notebook we generate a 20M dummy dataset and show how `dask.delayed` and `dask.dataframe` work.

## NycTaxi
In order to run this notebook we need to download 
* [2017 Yellow Taxi Trip Data](https://data.cityofnewyork.us/Transportation/2017-Yellow-Taxi-Trip-Data/biws-g3hs)
* [2018 Yellow Taxi Trip Data](https://data.cityofnewyork.us/Transportation/2018-Yellow-Taxi-Trip-Data/t29m-gskq)

each one is a CSV of roughly 10 GB and 112M rows and they have the same scheme (columns order and dtypes). The goal is to read this data and do some analytics on a old laptop with 16GB of RAM and a slow cpu `Intel(R) Core(TM) i3-4000M CPU @ 2.40GHz`. With this machine is neither possible to load a single file. The focus is on the workflow which is listed below

**Dask workflow**
* Split the data in smaller files
* Change `dtypes` and convert to parquet
* Clean the data and (again) save to parquet
* Take advantage of the fact that `parquet` is a columnar storage format.

### References
* [Dask - Best Practices](https://docs.dask.org/en/latest/best-practices.html)
* [Parquet](https://parquet.apache.org/)

# Prepare

You are supposed to have [anaconda](https://docs.anaconda.com/anaconda/install/) or [miniconda](https://docs.conda.io/en/latest/miniconda.html) installed. Then the following packages

```bash
conda install -c conda-forge jupyterlab
conda install -c conda-forge nodejs 
jupyter labextension install @jupyterlab/toc # Optional
jupyter labextension install dask-labextension
```
Load the environment with `conda env create -f environment.yml` and add the kernel to jupyter via
```bash
conda activate pydata_stg && \
python -m ipykernel install --user --name pydata_stg && \
conda deactivate
```

## List of packages used

* `dask`
* `pyarrow`
* `python-graphviz` # optional
* `holidays` # cos we need them!
