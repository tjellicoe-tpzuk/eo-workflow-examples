# Earth Observation Example Workflows

This repository includes some example workflows and experiments which you can run locally to view the expected outputs. These workflows can then be used to demonstrate cross-platform execution for OGC processing.

The currently included examples are:
- water-bodies: a workflow that determines possible areas of water within a given region using NDWI and Otsu threshold. These regions are marked on the generated GeoTIFF(s). This workflow returns a STAC Catalog containing the generated items and each output will have it's own STAC item. Multiple images can be processed at once as the workflow uses scatter functionality for parallel processing, if supported by the executing service. This workflow is borrowed from the [EOEPCA examples](https://github.com/EOEPCA/deployment-guide/blob/main/scripts/processing/oapip/examples/app-water-bodies-cloud-native.1.5.0.cwl)
  - There are two workflows defined in this CWL file, the first, `detect_water_body`, computes the output TIFF, and the second, `water_bodies`, calls the first workflow and also wraps the output in a STAC Catalog, to improve integration with other OGC services.
  - Both workflows accept the same parameters:
    - `stac_items` - links to the Sentinel-2 COG STAC items containing GeoTIFF data you wish to process
    - `aoi` - coordinates defining the area of interest we wish to crop the inputs to
    - `epsg` - the coordinate system for the input data, to be used when cropping the input
    - `bands` - the band names to use in the NDWI calculations
  - The expected output from this workflow is a set of GeoTIFF files highlighting the regions of water in the input images, you will get a single image for each STAC item input.

## How to run these workflows
- CWL workflows can be run in two ways. The first method is to use the `cwltool` Python package, installed with `pip install cwltool`, to execute the CWL workflow directly from the command line. You will need to specify the workflow step you wish to run when executing the workflow. This should normally be the top-level `Workflow` defined in the CWL file, rather than the individual `CommandLineTool` steps, but either can be executed. When running an experiment, you can provide the parameters you wish to use either directly on the command line, or by specifying a json or yaml file that specifies your workflow inputs.