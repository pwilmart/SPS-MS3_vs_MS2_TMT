# SPS-MS3_vs_MS2_TMT

## Comparison of SPS MS3 TMT data to MS2 TMT data

#### Added to Github January 23, 2020 (finished up Feb. 1, 2020)

---

## Notebooks:

- [Combined analysis (both platforms)](https://pwilmart.github.io/TMT_analysis_examples/MORG-75_combined.html)
- [Fusion SPS MS3 data only](https://pwilmart.github.io/TMT_analysis_examples/MORG-75_Fusion.html)
- [Q-Exactive HF MS2 data only](https://pwilmart.github.io/TMT_analysis_examples/MORG-75_QE.html)

## Overview
This is unpublished data from the [Terry Morgan lab](https://www.ohsu.edu/school-of-medicine/pathology/morgan-research-laboratory) at OHSU. Tandem mass tags were used to label human vulvar vestibulitis tissue samples. There were 4 control samples, 8 primary vestibulitis, and 2 secondary vestibulitis. The 14 samples were distributed across two TMT 10-plex channels. Two of the controls (41 and 42) were repeated in the second TMT-plex. A master pool of all samples was created, and duplicate channels of the pooled standard were included in each 10-plex run.

The [Internal Reference Scaling method](https://github.com/pwilmart/IRS_validation) was used to adjust each TMT experiment onto a common reporter ion scale. The data was acquired on a first generation Thermo Fusion Tribrid instrument using the SPS MS3 method in August 2015. An on-line high pH separation was used to fractionate the samples into 17 first dimensions. A low pH 2-hour gradient was used for the second dimension. Data analysis used the open source [PAW pipeline](https://github.com/pwilmart/PAW_pipeline) to confidently identify proteins with high sensitivity and aggregate reporter ion signals.

The samples (saved in the minus 80 freezer) were run under similar LC conditions on a Q-Exactive HF in May 2017. The [PAW pipeline](https://github.com/pwilmart/PAW_pipeline) is flexible enough to mix SPS MS3 data from the Fusion with the MS2 data on the QE. We can even use the IRS method to put all of the data on the same intensity scale since the same pooled standard channels are present in all runs. IRS can only adjust data if it is observed in each of the 4 plexes (the intersection of the results). That reduces the number of quantifiable proteins to about 3700, but with the advantage that we will have data for those proteins from both platforms. Then, we can safely do some head-to-head comparisons.

Statistical analysis used the Bioconductor package [edgeR](https://bioconductor.org/packages/release/bioc/html/edgeR.html) in a [Jupyter notebook](https://jupyter.org) running an R kernel. The data have not yet been published and are not publicly available at this time.

---

## What is in the Notebooks

The [Fusion notebook](https://pwilmart.github.io/TMT_analysis_examples/MORG-75_Fusion.html) is a separate analysis of the data from the original experiment. The [Q-Exactive notebook](https://pwilmart.github.io/TMT_analysis_examples/MORG-75_QE.html) is an analysis in a very similar notebook layout of the same TMT-labeled samples (from the freezer) run under similar LC conditions using a Q-Exactive HF platform. The Fusion experiment used the synchronous precursor selection (SPS) MS3 scan TMT method developed for more accurate reporter ion measurements. The second experiment on the Q-Exactive platform acquired the reporter ions in the high-resolution MS2 scans.

The platform-specific notebooks are very similar in layout and can be simultaneously scrolled in side-by-side browser windows for a nice qualitative comparison.

The IRS method could be used in this case to put all data (each platform was data from two 10-plex TMT labelings) into one single report because the same pooled standard channels were present in each of the 4 plexes. This facilitated a more direct comparison between platforms that is in the [combined notebook](https://pwilmart.github.io/TMT_analysis_examples/MORG-75_combined.html)

The data have not been published, so the HTML versions of the notebooks are all that can be shared at this time.

---

## What do you lose if you do IRS?

The Internal Reference Scaling (IRS) method ([publication link](https://www.mcponline.org/content/16/5/873); [first (detailed) repo](https://github.com/pwilmart/IRS_normalization); [second (more background) repo](https://github.com/pwilmart/IRS_validation)) by its design is limited to the **intersection** of proteins identified across multiple plexes. This can seem like a significant loss compared to the **union** of proteins identified in the experiment (over all of the plexes). The question naturally arises - will a lot be lost during IRS? The answer is mostly **no**.

The easiest thing to do is to count protein identifications. How many proteins do I see in each plex? How many in the whole experiment? And how many are seen in every plex? The problem is that low abundance proteins are counted with equal weight as high abundance proteins. We are doing quantitative measurements in these experiments, so we can do better than counting proteins. We can compare reporter ion intensity sums. Let's count things both ways to see the difference.

We have a 2-plex experiment done on the Fusion using the slower SPS MS3 method. We have another experiment of the same samples ran on a Q-Exactive HF where the sampling depth was a little better. We can see what is the usable overlap (what we have after IRS) in each experiment separately. We were also able to do a combined IRS analysis, where the usable IRS set are the proteins seen in all 4 plexes. We will look at the separate platforms first, then work up the combined data.

#### Fusion SPS MS3 experiment

##### By protein count (comma is thousands separator)

Category|Number of Proteins|Percentage of total
--------|------------------|-------------------
Union of all proteins reported|4,312
Without contaminants and decoys|4,225
Quantifiable (having reporter ion signals)|4,094|100%
Intersection of quantifiable proteins|3,650|89.1%
Unique to Plex 1|265|6.5%
Unique to Plex 2|179|4.4%

We did a reasonable fractionation for each plex, loaded a lot of sample, used a sensitive ID pipeline, and used a robust protein identification criterion (2 peptides per protein). We actually do very well having almost 90% of the total proteins quantifiable after IRS. How good this overlap will be depends all of the factors in the first sentence. Your sample, your separation, your instrument, your processing pipeline, etc. will all affect how good or bad the overlap seems.

##### By Sums of reporter ion intensities

Category|Sum of Intensities|Percentage of total
--------|------------------|-------------------
Total quantifiable set|4,955,816,354|100.00%
Total intersection set|4,945,183,984|99.79%
Total unique to Plex 1|6,450,278|0.13%
Total unique to Plex 2|4,182,092|0.08%

This picture is a little different. By relative abundance, 99.8% of the protein signals are retained after IRS. The proteins we do not consistently in each plex are **very** low in abundance. I am not making any claims about whether or not those proteins might be of great interest to the scientific questions being asked. I am just characterizing their measured quantities.

#### Q-Exactive HF MS2 experiment

##### By protein count (comma is thousands separator)

Category|Number of Proteins|Percentage of total
--------|------------------|-------------------
Union of all proteins reported|5,632
Without contaminants and decoys|5,443
Quantifiable (having reporter ion signals)|5,415|100%
Intersection of quantifiable proteins|4,900|90.5%
Unique to Plex 1|324|6.0%
Unique to Plex 2|191|3.5%

The numbers of identified proteins on the QE are larger than from the Fusion, but the pattern is very similar. We have 90% of the proteins surviving the IRS method.

##### By Sums of reporter ion intensities

Category|Sum of Intensities|Percentage of total
--------|------------------|-------------------
Total quantifiable set|278,979,563,457|100.00%
Total intersection set|278,241,678,866|99.74%
Total unique to Plex 1|504,565,586|0.18%
Total unique to Plex 2|233,319,005|0.08%

The pattern by reporter ion intensity for the QE is just like for the Fusion. We have 99.7% of the measurements associated with the proteins after IRS, and **very little** associated with proteins unique to each plex.

---

#### Combined Data (tallies by plaform)

##### By protein count (comma is thousands separator)

Category|Number of Proteins|Percentage of total
--------|------------------|-------------------
Union of all proteins reported|5,874
Without contaminants and decoys|5,646
Quantifiable (having reporter ions in any plex)|5,598|100%
Proteins with reporter ions in **all** plexes|3,720|66.5%
Proteins with any reporter ions in QE|5,539|99.0%
Proteins with any reporter ions in Fusion|4,643|82.9%

I have counted things differently compared to the individual platforms above. Since we are talking about quantification, I am not trying to tally which protein identifications were seen on both platforms versus each individual platform. The question is more like of all of the proteins seen between both platforms, how many had some quantifiable signal on each platform.

##### By Sums of reporter ion intensities

Category|Sum of Intensities|Percentage of total
--------|------------------|-------------------
Total quantifiable in either platform (union)|140,252,615,007|100.00%
Total quantifiable in both platforms (intersection)|139,043,945,271|99.14%
Total unique to QE|422,371,825|0.30%
Total unique to Fusion|57,896,371|0.04%

Even though we have quite a few more protein identifications on the Q-Exactive compared to the Fusion, they are still all very low abundance proteins. We had 5,598 quantifiable proteins across both platforms. The subset that had reporter ion signals in all of the 4 plexes was **only** 3,720 (only 66.5% of all IDs), yet those 3,720 proteins account for 99.14% of the reporter ion totals.

We basically have the Q-Exactive data being a superset of the Fusion data for this experiment. Of the 5,646 total proteins (excluding contaminants and decoys), there were 154 proteins unique to the Fusions, 1,247 proteins unique to the QE, and 4,245 proteins seen on both platforms. For the most part, everything we saw on the Fusion was seen on the Q-Exactive.

To conclude, when we count very low abundance proteins as protein identifications, with the same weight as highly abundant proteins, we grossly **exaggerate the differences** between samples and experiments. If we use some abundance weighted counting (we used intensities here, but we always have at least spectral counts available), we get a much more accurate picture. We see that the limitation of having to observe reporter ions from proteins in each plex of a multiplex experiment to perform IRS is not really much of an issue in this case.

---

Phil Wilmarth - 20200123, 20200128, and 20200201
