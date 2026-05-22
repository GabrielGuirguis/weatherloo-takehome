# Task 3: Dataset Understanding

## 1. What is the time step?

The dataset takes a snapshot every 6 hours. Hence, to cover a 120-hour window, at least **21** timesteps are needed (120 ÷ 6 + 1, inclusive of both endpoints).

## 2. What timezone / time standard does the dataset use?

The dataset uses **UTC** time. Timestamps are represented in the ISO 8601 format, such as `2021-12-31T18:00:00`. 

Such timestamps in the data do not contain timezone offsets, as would appear at the end of a fully qualified timestamp—for example: `2026-05-22T14:30:00-05:00`. That offset corresponds to Eastern Time in New York; as of late May 2026, it is 5 hours behind UTC.

## 3. What do the numbers 1440×721 refer to?

1440×721 refers to the dimensions of the grid covered by this data. This means each snapshot has 1440×721 cells = **1.04 M** cells per snapshot. Each axis is represented by points **0.25°** away from each other. For example, the range of the latitude being -90° to 90° (inclusive) means that there should be 180° / 0.25 (°/datapoint) + 1 (datapoint for one latitude endpoint)= **720** latitude datapoints for each longitude datapoint, which all increment by 0.25°.

## 4. What is Zarr?

**Zarr** is an open-source data format and library used to work with **compressed, multidimensional arrays**. It is available in Python and other languages, and provides cloud-ready **APIs** with performance-related features such as **parallel processing** and **chunking**.

For this ERA5 dataset, the store on GCS is a single Zarr group: each weather variable (e.g. `10m_wind_speed`) is stored as its own chunked array, which lets tools like xarray read one timestep or region without downloading the full dataset.