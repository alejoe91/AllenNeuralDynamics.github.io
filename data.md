---
layout: page
title: Data Access
---

The Allen Institute for Neural Dynamics (AIND) is committed to FAIR, Open, and Reproducible science. We therefore share all of the data we collect publicly with rich metadata as near to the time of collection as possible. We share data at all stages of the data lifecycle, including preliminary data collected during methods development, processed data that we are actively improving, or highly curated data used in a publication.

## aind-open-data

In addition to sharing curated datasets with modality-specific NIH data archives like DANDI and BIL, we are also excited to share all of our data in one public S3 bucket generously hosted by the Registry of Open Data on AWS. 

All data is stored here: `s3://aind-open-data`

### Bucket Organization
AIND’s mission to share data early with full reproducibility has significant implications on how data and metadata should be organized and represented. Organizational principles include:

* **Immutability**: once data is collected it should not be touched to ensure reproducibility.
* **Metadata Accessibility**: metadata must be trivial to find and read for humans and machines.
* **Cloud Compatibility**: data should be stored in cloud-friendly formats.

Based on these principles, `s3://aind-open-data` is organized as a flat list of data assets, where a data asset is simply a logical collection of files. Derived data assets are separate from their source assets, meaning they are not stored in the same path or directory.

Inspired by [BIDS](https://bids-specification.readthedocs.io/en/stable/) and the [HCA metadata schema](https://data.humancellatlas.org/metadata/structure), metadata describing a data asset is stored as sidecar JSON files that live adjacent to the data they describe. These JSON files conform to the schemas defined in [aind-data-schema](https://github.com/allenNeuralDynamics/aind-data-schema/).

As soon as possible, data in this bucket are stored in cloud-friendly formats, including NWB-Zarr for physiology and OME-Zarr for imaging. We aspire to produce data in these formats at the time of acquisition.

### Naming Conventions
Raw data assets are named:

`<modality>_<subject-id>_<acquisition-date>_<acquisition-time>`

Derived data assets are named:

`<source-data-asset-name>_<label>_<acquisition-date>_<acquisition-time>`

A raw extracellular ephys asset would look like this:

```
    ecephys_123456_2022-12-12_05-06-07/
        ecephys/
            <ephys data>
        behavior/
            <video data>
        data_description.json
        subject.json
        procedures.json
        processing.json
        rig.json
        acquisition.json
```

A spike-sorting result asset would look like this:

```
    ecephys_123456_2022-12-12_05-06-07_sorted-ks25_2022-12-12_06-07-08/
        sorted/
            <sorted ephys data>
        data_description.json
        subject.json
        procedures.json
        processing.json
        rig.json
        acquisition.json
````

## Benchmark Data

### aind-benchmark-data/ephys-compression

Extracellular electrophysiology data is growing at a remarkable pace. This data, collected neuropixels probes by the Allen Institute and the International Brain Lab can be used to benchmark throughput rates and storage ratios of various data compression algorithms. 

All data is available within the `aind-benchmark-data` bucket at `s3://aind-benchmark-data/ephys-compression`.




