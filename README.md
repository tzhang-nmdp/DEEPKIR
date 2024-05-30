# Deep learning approach for KIR imputation (DEEPKIR)

## KIR genomic haplotype complex:
![DEEPKIR_benchmarking](https://github.com/tzhang-nmdp/DEEPKIR/blob/main/fig/KIR_summary.png)
KIR

<b>
------------------------------------------------------------------------------------------------------------------------------------------------------
</b>

### Installation
``` r
conda env create -f pytorch.yml
conda activate pytorch
```
### Model training
``` r
# run test data from 1KGP (KIR3DL1/KIR3DS1/KIR3DL2)
python train.py --ref reference/test (.bgl.phased (.haps)/.bim/.fam) --sample reference/test --model reference/test (.model.json) --kir reference/test (.kir.json) --model-dir reference/model
```

##### Arguments and options
| Option name   | Descriptions                                                 | Required | Default   |
| ------------- | ------------------------------------------------------------ | -------- | --------- |
| `--ref`       | HLA reference data (.bgl.phased, and .bim format).           | Yes      | None      |
| `--sample`    | Sample SNP data of the MHC region (.bim format).             | Yes      | None      |
| `--model`     | Model configuration (.model.json format).                    | Yes      | None      |
| `--kir`       | HLA information of the reference data (.hla.json format).    | Yes      | None      |
| `--model-dir` | Directory for saving trained models.                         | No       | {BASE\_DIR}/model   |
| `--num-epoch` | Number of epochs to train.                                   | No       | 100       |
| `--patience`  | Patience for early-stopping. If you prefer no early-stopping, specify the same value as `--num-epoch`. | No       | 16        |
| `--val-split` | Ratio of splitting data for validation.                      | No       | 0.1       |
| `--max-digit` | Maximum resolution of alleles to impute ("2-digit", "4-digit", or "6-digit"). | No       | "4-digit" |

### Imputation
``` r
$ python impute.py --sample SAMPLE (.bgl.phased (.haps)/.bim/.fam) --model MODEL (.model.json) --kir KIR (.kir.json) --model-dir MODEL_DIR --out OUT
```
##### Outputs

- {OUT}.deephla.phased

  Imputed allele phased (best-guess genotypes) data. 

  Rows are markers and columns are individuals.

  First column is marker name; and subsequent columns are genotypes as two columns per individual.

- {OUT}.deephla.dosage

  Imputed allele dosage data. 

  First, second, and third columns are marker name, allele1 ("P"), and allele2 ("A"); and subsequent columns are dosages as one column per individual.

  Rows are markers and columns are individuals, as one column per individual. 

<b>
------------------------------------------------------------------------------------------------------------------------------------------------------
</b>

## Deep learning framework design:
![DEEPKIR_benchmarking](https://github.com/tzhang-nmdp/DEEPKIR/blob/main/fig/DEEPKIR_2nd_phase.png)
The 2nd phase of DEEPKIR aim to solve graph-based genomic mapping / protein interaction

