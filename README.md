# Deep learning approach for KIR imputation

# DEEPKIR
#### KIR genomic haplotype complex:
![DEEPKIR_benchmarking](https://github.com/tzhang-nmdp/DEEPKIR/blob/main/fig/KIR_summary.png)
KIR

## Installation
``` r
conda env create -f pytorch.yml
conda activate pytorch
```
## Model training
``` r
python train.py --ref reference/test --sample reference/test --model reference/test --kir reference/test --model-dir reference/model
```
## Imputation
``` r
$ python impute.py --sample SAMPLE (.bgl.phased (.haps)/.bim/.fam) --model MODEL (.model.json) --hla HLA (.hla.json) --model-dir MODEL_DIR --out OUT
```

#### Deep learning framework design:
![DEEPKIR_benchmarking](https://github.com/tzhang-nmdp/DEEPKIR/blob/main/fig/DEEPKIR_2nd_phase_design.png)
The 2nd phase of DEEPKIR aim to solve graph-based genomic mapping / protein interaction

