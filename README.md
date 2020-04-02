# sdrf-openms

Usage:

python parse_sdrf.py convert-openms -s sdrf.tsv

## Description:

- experiment settings (search engine settings etc.)
- experimental design

The experimental settings file contains one row for every raw file. Columns contain relevevant parameters like precursor mass tolerance, modifications etc. These settings can usually be derived from the sdrf file.

| Filename | FixedModifications | VariableModifications | Label | PrecursorMassTolerance | PrecursorMassToleranceUnit | FragmentMassTolerance | FragmentMassToleranceUnit | DissociationMethod | Enzyme |
| ------------- |-------------|-----|---| ------------- |-------------|-----|---| ------------- |-------------|
| A0218_1A_R_FR01.raw | Acetyl (Protein N-term) | Gln->pyro-glu (Q),Oxidation (M) | label free sample| 10 | ppm | 10 | ppm | HCD | Trypsin |
| A0218_1A_R_FR02.raw | Acetyl (Protein N-term) | Gln->pyro-glu (Q),Oxidation (M) | label free sample| 10 | ppm | 10 | ppm | HCD | Trypsin |


The experimental design file contains information how to unambiguously map a single quantitative value. Most entries can
be derived from the sdrf file. However, definition of conditions might need manual changes.

- **Fraction_Group** identifier that indicates which fractions belong together. In the case of label-free data, the fraction group identifier has the same cardinality as the sample identifier.
- The **Fraction** identifier indicates which fraction was measured in this file. In the case of unfractionated data the fraction identifier is 1 for all samples.
- The **Label** identifier. 1 for label-free, 1 and 2 for SILAC light/heavy, e.g. 1-10 for TMT10Plex
- The **Spectra_Filepath** (e.g., path = "/data/SILAC_file.mzML")
- The **Sample** that has been measured (e.g., sample = 1)
- **MSstats_Condition** the condition identifier as used by MSstats
- **MSstats_BioReplicate** an identifier to indicate replication. (MSstats requires that there are no duplicate entries. E.g., if MSstats_Condition, Fraction_Group group and Fraction number are the same - as in the case of biological or technical replication, one uses the MSstats_BioReplicate to make entries non-unique)

| Fraction_Group| Fraction      | Spectra_Filepath  | Label | Sample| MSstats_Condition      | MSstats_BioReplicate  |
| ------------- |-------------|-----|---| ------------- |-------------|-----|
| 1 | 1 | A0218_1A_R_FR01.raw | 1 | 1 | 1 | 1 |
| 1 | 2 | A0218_1A_R_FR02.raw | 1 | 1 | 1 | 1 |
| . | . | ... | . | . | . | . |
| 1 | 15 | A0218_2A_FR15.raw | 1 | 1 | 1 | 1 |
| 2 | 1 | A0218_2A_FR01.raw | 1 | 2 | 2 | 1 |
| . | . | ... | . | . | . | . |
| . | . | ... | . | . | . | . |
| 10 | 15 | A0218_10A_FR15.raw | 1 | 10 | 10 | 1 |

For details, please see the MSstats documentation
