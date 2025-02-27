
<!-- README.md is generated from README.Rmd. Please edit that file -->

# IntoValue Dataset

## Overview

This dataset is modified from the [main IntoValue
dataset](https://doi.org/10.5281/zenodo.5141342), and includes updated
registry data from ClinicalTrials.gov and DRKS. It also includes
additional data on associated results publications, including links in
the registries and trial registration number reporting in the
publications.

Detailed documentation for the parent IntoValue dataset is provided in a
data dictionary and readme alongside the [dataset in
Zenodo](https://doi.org/10.5281/zenodo.5141342). This readme serves to
highlight/document changes.

Note that `summary_results_date` for DRKS summary results was changed
from the parent IntoValue dataset. The parent dataset included only a
subset of summary results *manually* found during searches, whereas this
dataset includes additional summary results found via *automated*
search. The parent dataset used the `summary_results_date` manually
extracted from *PDFs*, whereas this dataset uses the
`summary_results_date` manually extracted from DRKS’ *change history*
and reflects the date the results were uploaded and made publicly
available.

## Data sources

This dataset builds on several sources, detailed below. The latest query
date is provided when applicable. Raw data, when permissible (i.e., not
for full-text), is shared in either this repository or in
[Zenodo](https://zenodo.org/record/5506434), depending on its size.

| Source                            | Type                          | Date       | Raw Data                                                                                                                  | Script                                                                                                            |
|-----------------------------------|-------------------------------|------------|---------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| IntoValue                         | Trials                        | NA         | <https://doi.org/10.5281/zenodo.5141342>                                                                                  | [get-intovalue.R](https://github.com/maia-sh/intovalue-data/blob/main/scripts/01_get-intovalue.R)                 |
| PubMed                            | Bibliometric                  | 2022-05-19 | [Zenodo](https://zenodo.org/record/5506434/files/pubmed.zip?download=1) \[last update: 2021-08-15\]                       | [get-pubmed.R](https://github.com/maia-sh/intovalue-data/blob/main/scripts/02_get-pubmed.R)                       |
| ClinicalTrials.gov/ AACT          | Registry                      | 2022-05-19 | [Zenodo](https://zenodo.org/record/5506434/files/ctgov.zip?download=1) \[last update: 2021-08-15\]                        | [get-process-aact.R](https://github.com/maia-sh/intovalue-data/blob/main/scripts/06_get-process-aact.R)           |
| DRKS                              | Registry                      | 2022-05-19 | [Zenodo](https://zenodo.org/record/5506434/files/drks.zip?download=1) \[last update: 2021-08-15\]                         | [get-drks.R](https://github.com/maia-sh/intovalue-data/blob/main/scripts/08_get-drks.R)                           |
| Unpaywall/ institutional licenses | Full-text PDF                 | NA         | NA, available only on local server `/data01/responsible_metrics/intovalue-data/fulltext`                                  | [get-ft-pdf.R](https://github.com/maia-sh/intovalue-data/blob/main/scripts/03_get-ft-pdf.R)                       |
| GROBID                            | Full-text XML                 | NA         | NA, available only on local server `/data01/responsible_metrics/intovalue-data/fulltext`                                  | PDF-to-XML conversion done in Python                                                                              |
| Unpaywall                         | Open access status            | 2022-08-20 | [oa-unpaywall.csv](https://github.com/maia-sh/intovalue-data/blob/main/data/raw/open-access/oa-unpaywall.csv)             | [get-oa-unpaywall-data.R](https://github.com/maia-sh/intovalue-data/blob/main/scripts/13_get-oa-unpaywall-data.R) |
| ShareYourPaper                    | Green open access permissions | 2022-08-20 | [oa-syp-permissions.csv](https://github.com/maia-sh/intovalue-data/blob/main/data/raw/open-access/oa-syp-permissions.csv) | [get-oa-permissions.py](https://github.com/maia-sh/intovalue-data/blob/main/scripts/14_get-oa-permissions.py)     |

## Data directories

Aside from full-text publications, the data directories should be
entirely reproducible from scripts. The data directory structure should
look as follows. Directories with a large number of individual raw files
are indicated with curly braces.

    ├── data
        ├── processed
        │   ├── codebook.csv
        │   ├── trials.csv
        │   ├── trials.rds
        │   ├── pubmed
        │   │   ├── pubmed-abstract.rds
        │   │   ├── pubmed-ft-retrieved.rds
        │   │   ├── pubmed-main.rds
        │   │   └── pubmed-si.rds
        │   ├── registries
        │   │   ├── ctgov
        │   │   │   ├── ctgov-crossreg.rds
        │   │   │   ├── ctgov-facility-affiliations.rds
        │   │   │   ├── ctgov-ids.rds
        │   │   │   ├── ctgov-lead-affiliations.rds
        │   │   │   ├── ctgov-references.rds
        │   │   │   └── ctgov-studies.rds
        │   │   ├── drks
        │   │   │   ├── drks-crossreg.rds
        │   │   │   ├── drks-facility-affiliations.rds
        │   │   │   ├── drks-ids.rds
        │   │   │   ├── drks-lead-affiliations.rds
        │   │   │   ├── drks-references.rds
        │   │   │   └── drks-studies.rds
        │   │   ├── registry-crossreg.rds
        │   │   ├── registry-references.rds
        │   │   └── registry-studies.rds
        │   └── trn
        │       ├──  cross-registrations.rds
        │       ├──  n-cross-registrations.rds
        │       ├──  trn-abstract.rds
        │       ├──  trn-all.rds
        │       ├──  trn-ft-doi.rds
        │       ├──  trn-ft-pmid.rds
        │       ├──  trn-reported-long.rds
        │       ├──  trn-reported-wide.rds
        │       └──  trn-si.rds
        └── raw
            ├── intovalue.csv
            ├── pubmed {raw files named [pmid].xml}
            ├── registries
            │   ├── ctgov
            │   │   ├── centers.csv
            │   │   ├── designs.csv
            │   │   ├── facilities.csv
            │   │   ├── ids.csv
            │   │   ├── interventions.csv
            │   │   ├── officials.csv
            │   │   ├── references.csv
            │   │   ├── responsible-parties.csv
            │   │   ├── sponsors.csv
            │   │   └── studies.csv
            │   └── drks {raw files named [drks trn]}
            ├── fulltext
            │   ├── doi
            │   │   ├── pdf {raw files named [doi].pdf}
            │   │   └── xml {raw files named [doi].tei.xml}
            │   └── pmid
            │       ├── pdf {raw files named [pmid].pdf}
            │       └── xml {raw files named [pmid].tei.xml}
            └── open-access
                ├── oa-syp-permissions.csv
                └── oa-unpaywall.csv

## Analysis dataset

We are interested in interventional trials with a German UMC lead
completed between 2009 and 2017. Due to changes in the registry as well
as discrepancies between IntoValue 1 and 2, we re-apply the IntoValue
exclusion criteria and deduplicate to get the analysis dataset.

``` r
trials <-
  trials_all %>% 

  filter(

    # Re-apply the IntoValue exclusion criteria
    iv_completion,
    iv_status,
    iv_interventional,
    has_german_umc_lead,

    # In case of dupes, exclude IV1 version
    !(is_dupe & iv_version == 1)
  )
    
n_iv_trials <- nrow(trials)
```

**Number of included trials**: 2895

For analyses by UMC, split trials by UMC lead city:

``` r
trials_by_umc <-
  trials %>% 
  mutate(lead_cities = strsplit(as.character(lead_cities), " ")) %>%
  tidyr::unnest(lead_cities)
```

Some analyses apply only to trials with a results publication
(optionally limited to journal articles to exclude dissertations and
abstracts) with a PMID that resolves to a PubMed record and for which we
could acquire the full-text as a PDF.

``` r

trials_pubs <-
  trials %>% 
  filter(
    # publication_type == "journal publication", #optional
    has_pubmed,
    has_ft,
  )

n_iv_trials_pubs <- nrow(trials_pubs)
trials_same_pmid <- janitor::get_dupes(trials_pubs, pmid)
n_trials_same_pmid <- n_distinct(trials_same_pmid$id)
n_pmids_same_trial <- n_distinct(trials_same_pmid$pmid)
n_pmids_dupes <- unique(range(trials_same_pmid$dupe_count))
```

**Number of trials with results publications**: 1895

In general, there is max 1 publication per trial and max 1 trial per
publication. However, there are 68 trials associated with the same 34
publications (i.e., 2 publications per trial). Since the unit of
analysis is trials, we disregard this double-counting of publications.

## TRN reporting in abstract

``` r
n_trn_abs <- nrow(filter(trials_pubs, has_iv_trn_abstract))

prop_trn_abs <- n_trn_abs/n_iv_trials_pubs
```

<!-- $$ \text{TRN in abstract (%)} = \frac{\text{Number of trials with PubMed publications with TRN in abstract}}{\text{Number of trials with PubMed publications available as PDF full-text}}$$ -->

**Numerator**: Number of trials with PubMed publications with IntoValue
TRN in abstract

**Denominator**: Number of trials with PubMed publications available as
PDF full-text

38% (714/1895) of trials report a TRN in the abstract of their results
publication.

## TRN reporting in full-text

``` r
n_trn_ft <- nrow(filter(trials_pubs, has_iv_trn_ft))

prop_trn_ft <- n_trn_ft/n_iv_trials_pubs
```

**Numerator**: Number of trials with PubMed publications with IntoValue
TRN in PDF full-text

**Denominator**: Number of trials with PubMed publications available as
PDF full-text

60% (1136/1895) of trials report a TRN in the full-text (PDF) of their
results publication.

## Linked publication in registry

``` r

# ClinicalTrials.gov
trials_ctgov <- filter(trials_pubs, registry == "ClinicalTrials.gov")

n_iv_trials_pubs_ctgov <- nrow(trials_ctgov)

n_reg_pub_link_ctgov <- nrow(filter(trials_ctgov, has_reg_pub_link))

prop_reg_pub_link_ctgov <- n_reg_pub_link_ctgov/ n_iv_trials_pubs_ctgov

n_auto <- nrow(filter(trials_ctgov, reference_derived))
n_manual <- nrow(filter(trials_ctgov, reference_derived))

# DRKS
trials_drks <- filter(trials_pubs, registry == "DRKS")

n_iv_trials_pubs_drks <- nrow(trials_drks)

n_reg_pub_link_drks <- nrow(filter(trials_drks, has_reg_pub_link))

prop_reg_pub_link_drks <- n_reg_pub_link_drks/ n_iv_trials_pubs_drks
```

*Registry Limitations*: ClinicalTrials.gov includes a often-used PMID
field for references. In addition, ClinicalTrials.gov automatically
indexes publications from PubMed using TRN in the secondary identifier
field. In contrast, DRKS includes references as a free-text field,
leaving trialists to decide whether to enter any publication
identifiers.

We consider a publication “linked” if the PMID or DOI is included in the
trial registrations. Note that some publications are included in the
registrations without a PMID or DOI (i.e., publication title and/or URL
only).

**Numerator**: Number of trials with PubMed publications PMIDs and/or
DOIs linked in trial registration

**Denominator**: Number of trials with PubMed publications available as
PDF full-text

59% (859/1448) of trials on clinicaltrials.gov include a link (i.e.,
PMID, DOI) to their PubMed publication (as available in the IntoValue
dataset). This includes 660 (77%) trials with automatically indexed
publications (i.e., using TRN in PubMed’s secondary identifier field)
and 660 (77%) trials with manually added publications.

23% (104/447) of trials on DRKS include a link (i.e., PMID, DOI) to
their PubMed publication (as available in the IntoValue dataset).

## Registry summary results

``` r
trials_pubs %>% 
  count(registry, has_summary_results) %>% 
  knitr::kable()
```

| registry           | has_summary_results |    n |
|:-------------------|:--------------------|-----:|
| ClinicalTrials.gov | FALSE               | 1292 |
| ClinicalTrials.gov | TRUE                |  156 |
| DRKS               | FALSE               |  442 |
| DRKS               | TRUE                |    5 |

*Registry Limitations*: ClinicalTrials.gov includes a structured summary
results field. In contrast, DRKS includes summary results with other
references, and summary results were inferred based on keywords, such as
Ergebnisbericht or Abschlussbericht, in the reference title.

## EUCTR Cross-registrations

``` r

tbl_euctr <-
  trials %>% 
  tbl_cross(
    row = has_crossreg_eudract,
    col = registry,
    margin = "column",
    percent = "column",
    label = list(
      has_crossreg_eudract ~ "EUCTR TRN in Registration",
      registry ~ "Registry"
    )
  )

as_kable(tbl_euctr)
```

|                           | ClinicalTrials.gov |   DRKS    |    Total    |
|:--------------------------|:------------------:|:---------:|:-----------:|
| EUCTR TRN in Registration |                    |           |             |
| FALSE                     |    1,908 (85%)     | 556 (87%) | 2,464 (85%) |
| TRUE                      |     345 (15%)      | 86 (13%)  |  431 (15%)  |

Of the 2895 unique trials completed between 2009 and 2017 and meeting
the IntoValue inclusion criteria, we found that 431 (15%) include an
EUCTR id in their registration, and are presumably cross-registered in
EUCTR. This includes 345 (15%) from ClinicalTrials.gov and 86 (13%) from
DRKS.

## Documentation TODOs

- Update data dictionary
- Add information about categories of data changes from IV1/2 dataset
