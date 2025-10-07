# Epic and Story Planning
[lucid diagram](
https://lucid.app/lucidchart/9fb4df66-99f8-4e25-a9af-e735435a943a/edit?page=0.8TjqwgrVR-&invitationId=inv_8dc11a6b-ec0a-40ca-a943-1679575223c5)

[JIRA board](https://digitial-product-engineering.atlassian.net/jira/software/c/projects/COGEN/summary)

## Data Foundation
### Platform setup with data model

Provision Snowflake infrastructure 
* Development team onboarding
* Foundation ready for initial import of data


### Import data from Legacy Systems

add data from existing systems:
* GATR
* GAMP
* RAR/Persephone
* Blast DB
* GIN
* Greenphyl
* Merci

### FastAPI Development

❓ belongs in Bioinformatics Workflow now ?

### Testing & Documentation

* Test data integrity
  * total number of species and genomes
  * count of gene models in specific genomes
  * GO IDs attached to a specific protein
* Documentation for Phase 2 - data ingestion and frontend development

## Data Ingestion Pipelines (Replacements)

### Ingest Annotation Metadata (GATR)

Replace existing GraphQL mutation functions - see [GATR GraphQL API docs](https://gatr.pro.intra/api/graphql) for full list. Includes create, update, delete functions for data like:
* Species
* Line  
* Assembly
* Annotation tracks per assembly

### Ingest Genome and Gene Annotation Metadata (GAMP)

Need method to add data from existing analysis pipelines:
* Genome metrics - genome stats, chromosome stats (inc telomeres), contamination stats, genome BUSCO
* Gene quality metrics - protein BUSCO, gene simple stats, transcript quality scores
* Links to Blast files. filepaths?

### Ingest genome and annotation data (RAR/Persephone)

Need method to add and update data: either continue to import from RAR's MariaDB database, or perform a second data load to CoGen via existing genome loading pipeline. 
* data updated multiple times per day most business days
* needs to handle deletions

### Ingest Blast metadata (BlastDB)

Need method to add data from existing firefly tool
* data: Blast library name, species (NCBI ID, name), version, description, date, tags
* coordinate with firefly owner (Magnus Riffel)

### Ingest homolog data (Greenphyl)
Need method to add data from existing analysis pipelines:


### Ingest homolog data (Greenphyl)
Need method to add data from existing analysis pipelines:

### Ingest genome comparison data (Merci)

?

## Bioinformatics Workflow - Data Export?

### Annotation Metadata Retrieval (GATR & GAMP)

**GATR Export:**
* Needs to replace existing GraphQL query functions - see [GATR GraphQL API docs](https://gatr.pro.intra/api/graphql) for full list
  - Search for species, line, assembly, annotations, etc

**GAMP Export:**
* Needs to replace existing GraphQL query functions - see [GAMP GraphQL API docs](https://gamp.app.intra/api/graphql) for full list
  - Includes gene and genome quality statistics, links to Blast files, etc

### Gene Data Retrieval

**Search Terms:**
* Gene ID, Protein ID, Transcript ID
* Physical coordinates (Seq, coord 1, coord 2)

**Returns:**
* Gene ID, Protein ID, Transcript ID
* Physical coordinates (Seq, coord 1, coord 2)
* Function annotation - GO terms, PFAM, etc [GIN data fields]
* Quality scores

### Homolog Delivery (Greenphyl)

**Search Terms:**
* Gene ID, Protein ID, Transcript ID

**Returns:**
* Gene ID, Protein ID, Transcript ID
* Species, genome
* Homology quality metrics?

### FASTA Sequence Retrieval

Per Rod example: 
```
select upper(getReference(1,42,'corn_B73_v5','4')) from dual

This will return the DNA sequence from position 1 to 41 for corn_B73_v5 assembly for sequence_name = '4'
```

## Front end / visualization

### Genome annotation work tracking (GATR)
Genome annotation tracks report
* Given a genome name, show annotation tracks status in the analytical pipeline. 

Genome annotation tracks data editing
* Ability to add, edit, or delete an annotation track associated with a genome.

### Genome metadata (GAMP)

Species report
* Given species name, show genomes for species in a tabular form. allow user to filter and choose columns. Replaces https://gamp.app.intra/species/Zea%20mays%20(corn%2C%20maize)

Genome report page for a genome.
* Given genome name, provide a report with genome metrics (genome stats, chromosome stats (inc telomeres), contamination stats, genome BUSCO). Replaces GAMP genome page, https://gamp.app.intra/assembly/corn_B73_v6

Genome report for multiple genomes
* Given species name or names, list genomes and provide a report with genome metrics. By default, show number of sequences, number of chromosomes, chromosomes with telomeres, genome BUSCO). Replaces SIRE_reports, i.e. https://demeter.nafta.syngenta.org/GAMP/SIRE_reports/Zea_mays.html


### Gene annotation metadata (GAMP and GIN)

Gene quality comparison view. 
* Choose species (potentially multiple), create a tabular report with gene stats (genecount, transcript count, 5' and 3' UTR counts) plus BUSCO scores and transcript quality (high, medium, low). Replace existing https://demeter.nafta.syngenta.org/GAMP/gene_reports/Zea_mays.html


### Gene functional annotation data (GIN)

### Homolog delivery (Greenphyl)

### Genome comparison delivery (Merci)

KADMAS-style report on genome similarity (example https://demeter.nafta.syngenta.org/GAMP/kadmas_reports/wgas_reports/Zea_mays.html)


## AI enhancements

### Semantic model docs?
generate docs describing semantic model for each data system in CoGen:
* GATR
* GAMP
* RAR/Persephone
* Blast DB
* GIN
* Greenphyl
* Merci

## Legacy Application Retirement

### Communication plan

 * present project to multiple groups, get feedback
   * Digital
     * Bioinformatics
     * reference data / seeds common 
   * Other Seeds groups ?
   * ? Vegetables ?
   * ? CP ?
 * contact owners of tools that currently use data: 
   * Bioinformatics
     * Josh's team
       *  Agrigear
     * Arvind's team
        * TreC / Eve-Com by the end of 2025: needs access to gene annotation (RAR DB), submission information (SSP), gene assemblies (GAMP) and Construct ID (Genie)
        * GEDI: needs access to gene annotation (RAR DB)
    * DataLake team - replace existing links with CoGen
  

### Retire AWS infrastructure components
