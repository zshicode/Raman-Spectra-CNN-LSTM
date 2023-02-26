# PyTorch implementation of CNN and LSTM for Raman spectrum recognition

Deep learning has been widely applied for Raman spectroscopy. This repo contributes PyTorch implementation of vanilla CNN and LSTM for Raman spectrum recognition (Liu et al., 2017; Yu et al., 2021).

## Requirements

The code has been tested running under Python 3.9.12, with the following packages and their dependencies installed:

```
numpy==1.16.5
pandas==1.4.2
pytorch==1.7.1
sklearn==0.21.3
```

## Usage

```bash
python main.py --c 2 --model LSTM
```

## Datasets

This repo validates the models on two datasets proposed by Yu et al. (2021). The region of the Raman spectra data is from 600 to 1800 cm-1. The dimension of the Raman spectra data is 1200. Following Yu et al. (2021), the Raman spectra of each sample is preprocessed by 0-1 normalization.

The binary classification dataset `bin.csv` consists of the Raman spectra data from two kinds of microbes, *Acinetobacter baumannii* (Label 0) and *Pseudomonas nitritireducens* (Label 1). 

The multi-class classification dataset `multi.csv` consists of the Raman spectra data from eight strains of *Urechis unicinctus*, named SX-1 to SX-8 (Label 0 to 7). 

## Results

Deep learning models can achieve 99% accuracy on binary classification dataset, and 95% accuracy on multi-class classification dataset. For comparison, this repo also implements SVM and random forest for this task, see `baseline.py`.

## Options

We adopt an argument parser by package  `argparse` in Python, and the options for running code are defined as follow:

```python
parser = argparse.ArgumentParser()
parser.add_argument('--use-cuda', default=False,
                    help='CUDA training.')
parser.add_argument('--seed', type=int, default=1, help='Random seed.')
parser.add_argument('--epochs', type=int, default=200,
                    help='Number of epochs to train.')
parser.add_argument('--lr', type=float, default=0.01,
                    help='Learning rate.')
parser.add_argument('--wd', type=float, default=1e-5,
                    help='Weight decay (L2 loss on parameters).')
parser.add_argument('--hidden', type=int, default=64,
                    help='Dimension of representations')
parser.add_argument('--c', type=int, default=2,
                    help='Num of classes')
parser.add_argument('--d', type=int, default=1200,
                    help='Num of spectra dimension')
parser.add_argument('--model', type=str, default='CNN',
                    help='Model')                    

args = parser.parse_args()
args.cuda = args.use_cuda and torch.cuda.is_available()
```

## References

Deng, L. et al. Scale-adaptive deep model for bacterial raman spectra identification. IEEE J. Biomed. Health Inform. 26(1), 369-378 (2022) .

Gu, J. et al. Conformal prediction based on raman spectra for the classification of chinese liquors. Appl. Spectrosc. 73 (7), 759-766 (2019) .

Ho. C. et al. Rapid identification of pathogenic bacteria using Raman spectroscopy and deep learning. Nat. Commun. 10, 4927 (2019) .

Liu, J. et al. Deep convolutional neural networks for raman spectrum recognition: a unified solution. Analyst 142 (21), 4067-4074 (2017) .

Liu, J. et al. Dynamic spectrum matching with one-shot learning. Chemometr. Intel. Lab. Sys. 184, 175-181 (2019) .

Yu, S. et al. Analysis of raman spectra by using deep learning methods in the identification of marine pathogens. Anal. Chem. 93 (32), 11089-11098 (2021) .

Zhong, N. et al. Accurate prediction of salmon storage time using improved raman spectroscopy. J. Food Eng. 293, 110378 (2021) .
