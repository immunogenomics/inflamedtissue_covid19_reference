## Overview
This repo provides the source code for our analysis and figures for 

- Fan Zhang, Joseph R. Mears, Lorien Shakib, Jessica I. Beynor, Sara Shanaj, Ilya Korsunsky, Aparna Nathan, Accelerating Medicines Partnership Rheumatoid Arthritis and Systemic Lupus Erythematosus (AMP RA/SLE) Consortium, Laura T. Donlin*, Soumya Raychaudhuri*. IFN-γ and TNF-α drive a CXCL10+ CCL2+ macrophage phenotype expanded in severe COVID-19 lungs and inflammatory diseases with tissue inflammation. In review, 2021.

## Source code 

This repo covers code for major analyses and figure generations:
 - We built an immune cell reference consisting of >300,000 single-cell transcriptomic profiles from COVID-19 affected lungs and tissues from healthy subjects and patients with 5 inflammatory diseases: rheumatoid arthritis (RA), Crohn’s disease (CD), ulcerative colitis (UC), lupus, and interstitial lung disease. 
 - We tested the association of shared immune states with severe/inflamed status compared to healthy control using mixed-effects modeling. 
 - We observed a CXCL10+ CCL2+ inflammatory macrophage state that is shared and strikingly abundant in severe COVID-19 bronchoalveolar lavage samples, inflamed RA synovium, inflamed CD ileum and UC colon. 
 - We found this macrophage phenotype is induced upon co-stimulation by IFN-γ and TNF-α.
 
 Expension and generalization of this reference:
 - This reference (Zhang, et al, 2021) can be used to investigate other inflammatory diseases and their connections with COVID-19 in terms of immune cell responses. 
 - Notebook of using Symphony (Kang, In review, 2021) to map Sepsis (Reyes, *Nature Medicine*, 2020) cells to our cross-diseased tissue single-cell reference that reflects shared inflammatory structures.


## Raw data access
The single-cell RNA-seq data for blood-derived macrophages are available in the Gene Expression Omnibus database with accession number GSE168710.

## Contact
Send us an email (fanzhang@broadinstitute.org and jmears@broadinstitute.org) if you have additional questions!
