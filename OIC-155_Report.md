# OIC-155 MDMA and Oxytocin_Report

Total Hours: 19

## Authorship and Methods

Research supported by the Optical Imaging Core should be acknowledged and considered for authorship. Please refer to our [SharePoint page](https://vanandelinstitute.sharepoint.com/sites/optical/SitePages/Acknowledgements-and-Authorship.aspx) for guidelines.

Please include our RRID in the methods section for any research supported by the OIC. RRID:SCR_021968

### Sample Acknowledgement

We thank the Van Andel Institute Optical Imaging Core (RRID:SCR_021968), especially [staff name], for their assistance with [technique/technology]. This research was supported in part by the Van Andel Institute Optical Imaging Core (RRID:SCR_021968) (Grand Rapids, MI).

## Summary of Request

Mouse brain sections were stained for several markers of interest to assess neuronal activity. Analysis goal was to register the brain sections to the Allen Brain Atlas, segment GFP+ cells and measure signal intensity of GFP channel.

## Brief summary of analysis pipeline

QuPath v5.1, ABBA, and CellPose v3.1.1 were used for this project.

## Data

> Mice underwent AAV targeting of their OXT neurons and were subjected to behavioral testing with/without MDMA treatment and inhibition of OXT neurons.

8 sets of serial sections were collected, stained for DAPI, cFOS, and AAV, and imaged on the Zeiss AxioScan at 20X as multi scene images.

![Example Image](/Images/Example_Image.png)

## Analysis Pipeline

The ImageJ and QuPath extension, [ABBA](https://abba-documentation.readthedocs.io/en/latest/), was used to register each set of brain sections to the Allen Brain Atlas.

![Example Registration](/Images/Example_Registration.png)

The cellpose v3.1.1 cyto3 model was used as the backbone for transfer learning to improve segmentation of the GFP+ cells using the CellPose GUI and training ROIs from different samples to include natural variation observed across the data sets. [cFOS_V3](/models/cFOS_V3) was the model used for detecting GFP+ cells in all samples.

![Example Cell Detections](/Images/Example_CellDetection.png)

## Output

Quantification were exported as a csv for each sample using *sample#*_Brain_Region_Counts and *sample#*_Cell_Detection_Measurements as the naming scheme.

**Brain Region Counts Key**

| Value | Meaning|
|-|-|
|Image|Brain slice/image that the data came from|
|Object ID| Unique Identifier for the object|
|Name | Name of the brain region (acronym)|
|Classification| Name of brain region and L/R hemisphere designation |
|Centroid X/Y µm|Center of annotation object in XY coordinates|
|ID| Brain region identification number|
|Side| L or R hemisphere|
|Num Detections| Number of GFP+ cells in region|

**Cell Detection Measurements Key**

| Value | Meaning|
|-|-|
|Image|Brain slice/image that the data came from|
|Object ID| Unique Identifier for the object|
|Parent| Parent object the detection belongs to (likely Root for all)|
|Centroid X/Y µm|Center of annotation object in XY coordinates|
|AF488: Mean/Median/Min/Max/Std.Dev.| Calculated value of fluorescence intensity|
