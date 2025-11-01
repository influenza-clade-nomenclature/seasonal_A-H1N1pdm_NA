# Clade and subclade nomenclature for the NA segment of seasonal A/H1N1pdm influenza viruses

This repository defines subclades of the neuradminidase segment of seasonal A/H1N1pdm influenza viruses.
These designations are called subclades in analogy to the HA segment, even though no corresponding clade nomenclature exists for NA.
These subclades don't necessarily correspond to groups of viruses with distinct phenotypes but are meant to facilitate discussion of viral genetic diversity and to capture the frequency dynamics of co-circulating viral variants that often don't have distinct properties.


## Designations

Each subclade is defined by a machine readable `yaml` file in the subdirectory `subclades`.
The yaml-files have the following structure:
```
name: C.5.1
unaliased_name: A.1.1.1.3.2.5.1
parent: C.5
representatives: []
defining_mutations:
- locus: NA
  position: 49
  state: D
- locus: nuc
  position: 1312
  state: G
clade: none
```
The field `clade` is set to `none` for all `NA` clades, but kept in case such a nomenclature is added.

The defining mutations are relative using nucleotide and NA coordinates defined in
```
##gff-version 3
##sequence-region CY121682.1 1 1432
CY121682.1      feature cds    9       1418    .       +       .       name="NA"
```
Note that these defining mutations are not exhaustive. They represent a genotypic constellation sufficient to distinguish the clade from its parent.

## [Subclade summary](.auto-generated/subclades.md)

## Subclade short names (aliases)
The subclade names are designed with a systematic way to shorten their names inspired by the pango-lineage system for SARS-CoV-2.
The initial part of the hierarchical names can be collapsed into a single letter (and possibly eventually double letters).
These aliases are defined in [config/aliases.json](config/aliases.json).


## Configuration
Parameters and mutation weights for the automated subclade suggestion algorithm can be found in the directory `config`.

## Update auto-generated files
After adding new clades, run the following commands to update the files generated from the individual yamls.
```
# generate the markdown summary of the clade definitions
python ../helper-scripts/generate_markdown_summary.py --input-dir subclades --lineage h1n1pdm --segment na

# generate the tsv file with clade-defining info that can be used to annotate clades in augur
python ../helper-scripts/construct_tsv.py --input-dir subclades --output-tsv .auto-generated/subclades.tsv --output-alias-tsv .auto-generated/subclade-summary.tsv
python ../helper-scripts/construct_tsv.py --input-dir subclades subclade-proposals --output-tsv .auto-generated/subclade-proposals.tsv

# To add the result to the repo, do:

git add .auto-generated/subclades.tsv .auto-generated/subclade-proposals.tsv .auto-generated/subclades.md  .auto-generated/subclade-summary.tsv
git commit -m "update auto-generated files"
```

