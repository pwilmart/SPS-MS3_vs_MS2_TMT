# SPS-MS3_vs_MS2_TMT

## Comparison of SPS MS3 TMT data to MS2 TMT data

#### Added January 23, 2020

---

## Notebooks:

- [Combined analysis (both platforms)](https://pwilmart.github.io/TMT_analysis_examples/MORG-75_combined.html)
- [Fusion SPS MS3 data only](https://pwilmart.github.io/TMT_analysis_examples/MORG-75_Fusion.html)
- [Q-Exactive HF MS2 data only](https://pwilmart.github.io/TMT_analysis_examples/MORG-75_QE.html)

## Overview
This is unpublished data from the [Terry Morgan lab](https://www.ohsu.edu/school-of-medicine/pathology/morgan-research-laboratory) at OHSU. Tandem mass tags were used to label human vulvar vestibulitis tissue samples. There were 4 control samples, 8 primary vestibulitis, and 2 secondary vestibulitis. The 14 samples were distributed across two TMT 10-plex channels. Two of the controls (41 and 42) were repeated in the second TMT-plex. A master pool of all samples was created, and duplicate channels of the pooled standard were included in each 10-plex run.

The [Internal Reference Scaling method](https://github.com/pwilmart/IRS_validation) was used to adjust each TMT experiment onto a common reporter ion scale. The data was acquired on a first generation Thermo Fusion Tribrid instrument using the SPS MS3 method in August 2015. An on-line high pH separation was used to fractionate the samples into 17 first dimensions. A low pH 2-hour gradient was used for the second dimension. Data analysis used the open source PAW pipeline to confidently identify proteins with high sensitivity and aggregate reporter ion signals.

The samples (saved in the minus 80 freezer) were run under similar LC conditions on a Q-Exactive HF in May 2017. The [PAW pipeline](https://github.com/pwilmart/PAW_pipeline) is flexible enough to mix SPS MS3 data from the Fusion with the MS2 data on the QE. We can even use the IRS method to put all of the data on the same intensity scale since the same pooled standard channels are present in all runs. IRS can only adjust data if it is observed in each of the 4 plexes (the intersection of the results). That reduces the number of quantifiable proteins to about 3700, but with the advantage that we will have data for those proteins from both platforms. Then, we can safely do some head-to-head comparisons.

Statistical analysis used the Bioconductor package [edgeR](https://bioconductor.org/packages/release/bioc/html/edgeR.html) in a [Jupyter notebook](https://jupyter.org) running an R kernel. The data have not yet been published and are not publicly available at this time.

---

## What is in the Notebooks

The [Fusion notebook](https://pwilmart.github.io/TMT_analysis_examples/MORG-75_Fusion.html) is a separate analysis of the data from the original experiment. The [Q-Exactive notebook](https://pwilmart.github.io/TMT_analysis_examples/MORG-75_QE.html) is an analysis in a very similar notebook layout of the same TMT-labeled samples (from the freezer) run under similar LC conditions using a Q-Exactive HF platform. The Fusion experiment used the synchronous precursor selection (SPS) MS3 scan TMT method developed for more accurate reporter ion measurements. The second experiment on the Q-Exactive platform acquired the reporter ions in the high-resolution MS2 scans.

The platform-specific notebooks are very similar in layout and can be simultaneously scrolled in side-by-side browser windows for a nice qualitative comparison.

The IRS method cold be used in this case to put all data (each platform was data from two 10-plex TMT labelings) into one single report because the same pooled standard channels were present in each of the 4 plexes. This facilitated a more direct comparison between platforms that is in the [combined notebook](https://pwilmart.github.io/TMT_analysis_examples/MORG-75_combined.html)

The data have not been published, so the HTML versions of the notebooks are all that can be shared at this time.

---

Phil Wilmarth - 20200123
