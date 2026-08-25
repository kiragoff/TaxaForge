# TaxaForge

An R pipeline for processing raw taxonomic abundance tables from separate sequencing runs and generating customizable bubble plots with `ggplot2`. Because you can't process data from separate sequencing runs together, or the error correction will introduce even more errors than you started with.

If you've ever tried to carry out visualization of separate sequencing runs that's already been reduced to a CSV or a TSV, you know it can be a giant pain. If you've ever tried to figure out the best way to display your data within a bubble plot, you know getting it just right can ALSO be a giant pain. 

I built this script to streamline the process. It's designed to be agnostic to upstream sequencing technique, addresses common bottlenecks like handling unclassified taxonomy, and provides flexible options for visualization and sample/taxa ordering.

## Core Features

* **Delimiter Detection:** Automatically sniffs file contents to handle both comma- and tab-delimited inputs correctly.
* **Taxonomy Rescue:** Resolves unclassified or missing lower-level classifications by inheriting the last known parent rank (with customizable naming styles like prefix, suffix, or parent-failed labels).
* **Flexible Abundance Handling:** Toggle easily between raw read counts and relative abundance (%); select top N taxa on an overall or per-sample basis.
* **Advanced Sorting & Layouts:** Calculation engine lets you dynamically select your taxonomic level of interest; allows for optional faceting based on an additional taxonomic level.
* **Metadata Integration:** Optional sample sorting and ordering driven by external metadata files.

## Dependencies

This script relies on the following R packages:
* `tidyverse`
* `ggtext`
* `paletteer`

## Usage

1. Place your taxonomic tables in your project directory.
2. Update the configuration variables at the top of the chunks (such as file paths, target taxonomic level, and top N cutoffs).
3. Run the script to generate and export the plot as a high-resolution PNG.

## Example Output
<img src = "https://github.com/kiragoff/TaxaForge/blob/main/figures/bubbleplot_boxed_Genus_byPhylum_sample_top10_relative_20260822.png" height = "600px"> <img src = "https://github.com/kiragoff/TaxaForge/blob/main/figures/bubbleplot_boxed_Family_byPhylum_sample_top10_relative_withLabels_20260822.png" height = "600px"> 

### Known Limitations & Roadmap
* **Sorting behaviour:** A sorting issue currently affects one specific sorting mode; when this mode is active and certain other configurations are active, output ordering may be incorrect. This issue is documented and will be addressed in a future update.
* **Modularization refactor:** The current workflow exposes a large number of configuration options in a single script. The workflow is functional, but future development will separate processing, taxonomy handling, calculation, and visualization into more modular components to improve usability and maintainability.
