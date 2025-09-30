# Earth Observation Example Workflows

This repository includes some example workflows and experiments which you can run locally to view the expected outputs. These workflows can then be used to demonstrate cross-platform execution for OGC processing.

The currently included examples are:
- water-bodies: a workflow that determines possible areas of water within a given region using NDWI and Otsu threshold. These regions are marked on the generated GeoTIFF(s). This workflow returns a STAC Catalog containing the generated items and each output will have it's own STAC item. Multiple images can be processed at once as the workflow uses scatter functionality for parallel processing, if supported by the executing service. This workflow is borrowed from the [EOEPCA examples](https://github.com/EOEPCA/deployment-guide/blob/main/scripts/processing/oapip/examples/app-water-bodies-cloud-native.1.5.0.cwl)