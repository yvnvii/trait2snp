# trait2snp
# Abstract
While genome-wide association studies (GWAS) have identified thousands of SNP-trait associations and their corresponding odds ratios (ORs), the standard interpretive pipeline typically flows in a forward direction, from genotype to trait. Yet, many real-world contexts, including clinical triage, low-resource environments, or forensic investigations, lack genotype data, while phenotypic features are abundant.

Here, we introduce a statistical construct, the posterior relative risk (pRR): an inversion of conventional relative risks that enables probabilistic estimation of genotype conditional on trait presence, using only summary-level data (trait prevalence, allele frequency, and published ORs). This method reframes existing SNP–trait associations into a reverse-inferential structure, facilitating probabilistic genotype estimation without new data collection or individual-level genomic access. The approach marks a conceptual shift from predictive modeling to epistemological reinterpretation of existing genomic knowledge.

We also introduce a new statistical framework, the trait-coexpression enrichment ratio (TCER): an inferrence of SNP enrichment based on the co-occurrence of phenotypic traits. By modeling the joint prevalence of traits A and B with explicit correlation bounds, and extending this model conditionally on genotype presence, we derive interpretable estimates of SNP probability given trait co-expression. 

Our approach has generalizability to other clinically significant and pleiotropic variants (e.g., BRCA1, CFTR) and unlocks untapped inferential potential in publicly available GWAS and PheWAS results. This reverse-inference (from phenotype to genotype) framework repurposes existing summary statistics for genotype estimation in settings where individual-level DNA is unavailable. It offers a novel paradigm for genomic inference, leveraging traits to reconstruct genotypes, with broad applications in population screening, forensic reconstruction, and equitable healthcare delivery.

# Introduction

## Background/Gaps
Genome-wide association studies (GWAS) have identified thousands of single nucleotide polymorphisms (SNPs) associated with a wide array of traits and diseases. These associations are overwhelmingly interpreted in a forward direction: from genotype to phenotype. That is, the presence of a particular SNP is used to infer increased or decreased likelihood of a particular trait. However, in many real-world contexts—including clinical practice, epidemiological studies, forensic investigations, and low-resource settings—genotype information is unavailable or impractical to obtain, whereas phenotypic information is abundant.
Despite the ubiquity of odds ratios (ORs) describing SNP → trait associations, no standard framework exists for reversing this inference to estimate the likelihood of genotype given a phenotype. This gap limits the utility of GWAS data in reverse-inferential contexts, effectively discarding a potentially rich source of latent genomic information encoded in observable traits.
Previous Bayesian applications in genomic studies have focused on effect size estimation or association strength, rather than direct inference of genotype probabilities from traits. Our approach uniquely operationalizes this reverse inference at the single-variant level using only publicly available summary data.
Odds ratios of many SNPs are available, but not fully interpreted in reverse directions.
In some cases, an individual genomic-level survey may not be easily possible in terms of costs, accessibility, and privacy.

## Aim of this study
In this study, we introduce a new statistical metric called the Posterior Relative Risk (pRR) to complement the conventional odds ratio. Whereas standard odds ratios estimate the likelihood of a phenotype given a genotype, pRR estimates the relative likelihood of carrying a specific genotype given the presence or absence of a phenotype.
It is algebraically derived from published forward ORs, along with trait and allele frequencies. Unlike predictive models that require individual-level data or machine learning, pRR enables a computationally simple, interpretable, and entirely retrospective reinterpretation of public GWAS results.
We use only summary data that is already available, showing how we can introduce a new interpretation of existing data epistemological shift
We demonstrate how rRR enables trait-to-genotype inference without new data collection, thereby expanding the informational value of existing genomic studies.

# Methods
## Theoretical Framework
Odds ratio bayesian conversion
  Odds ratio -> P(SNP|trait)

### Definition of pRR
The posterior relative risk(pRR) quantifies how much more likely an individual is to carry a specific genetic variant (e.g., a SNP) given the presence of a particular trait or disease, based on population-level summary statistics.
Formally:
$rRR = \frac{P(S \mid T)}{P(S \mid\overline{T})}$  

Comparison with forward (conventional) OR
$$OR=P(Trait∣SNP)/P(\overline{Trait}∣SNP)P(Trait∣\overline{SNP})/P(\overline{Trait}∣\overline{SNP})\text{OR} = \frac{P(\text{Trait} \mid \text{SNP}) / P(\overline{\text{Trait}} \mid \text{SNP})}{P(\text{Trait} \mid \overline{\text{SNP}}) / P(\overline{\text{Trait}} \mid \ \text{SNP})}$$

### Multi-Trait Inference (P(SNP|traitA and traitB))
1. When you know joint prevalence of two trait
- Use joint distribution and then do simulation
2. When you do not know joint prevalence of two trait
- Suppose P(A and B) under each correlation coefficient $r$ (r_min < r < r_max)
- Sensitivity analysis
  
In multi-trait reverse inference, estimating the conditional probability of carrying a SNP given the presence of multiple traits requires knowledge of the joint trait prevalence, P(A∩B). However, joint prevalence is often unavailable in summary-level data.

To address this, we assume a range of plausible correlation coefficients r between traits and use a bivariate Bernoulli approximation to estimate joint prevalence:  
$$P(A \cap B) \approx P(A)P(B) + r\sqrt{P(A)(1 - P(A))P(B)(1 - P(B))}$$  
By sweeping r∈[r_min,r_max], we generate a bounded range for the inferred probability P(SNP∣A∩B). This provides a robust estimate even in the absence of precise phenotypic correlation data.

This approach not only adds transparency but also enhances the applicability of the pRR framework in real-world settings where genotypic data is scarce and phenotypic correlation is uncertain.

# Validation Strategy

- Analytical comparison between model-predicted genotype frequencies and observed data
  - UK Biobank
- Sensitivity analysis using OR, P(trait), P(SNP) confidence intervals
- Simulation for multi-trait conditions and trait correlation
- (Bayesian network or copula modeling for joint trait effects)

- Multi-Trait Inference
  - Estimation of P(SNP | trait A ∩ trait B)
  - Demonstration of additive (log pRR) and simulation-based integration
  - Sensitivity analysis under varying correlation structures

