# Leveraging Object Detection for Diverse and Accurate Long-Horizon Events Forecasting

**Implementation of object detection for MTPPs. The loss is placed in ```hotpp/losses/detection.py```. Configs and results can be found in the experiments folder.**

# Installation
Sometimes the following parameters are necessary for successful dependency installation:
```sh
CXX=<c++-compiler> CC=<gcc-compiler> pip install .
```

# Training and evaluation
The code is divided into the core library and dataset-specific scripts and configuration files.

The dataset-specific part is located in the `experiments` folder. Each subfolder includes data preparation scripts, model configuration files, and a README file. Data files and logs are usually stored in the same directory. All scripts must be executed from the directory of the specific dataset. Refer to the individual README files for more details.

To train the model, use the following command:
```sh
python3 -m hotpp.train --config-dir configs --config-name <model>
```

To evaluate a specific checkpoint, use the following command:
```sh
python3 -m hotpp.evaluate --config-dir configs --config-name <model>
```

To run multiseed training and evaluation:
```sh
python3 -m hotpp.train_multiseed --config-dir configs --config-name <model>
```

# Evaluation results
### Transactions
| Method              | Acc.      | mAP      | MAE       | OTD  Val / Test     | T-mAP  Val / Test   |
|:--------------------|:----------|:---------|:----------|:--------------------|:--------------------|
| MostPopular         | 32.78     | 0.86     | 0.752     | 7.37 / 7.38         | 1.06 / 0.99         |
| RecentHistory       | 19.60     | 0.87     | 0.924     | 7.40 / 7.44         | 2.46 / 2.49         |
| MAE-CE              | 34.08     | 3.47     | 0.693     | 6.88 / 6.90         | 5.82 / 5.88         |
| MAE-CE-K            | 33.69     | 3.25     | 0.698     | 7.18 / 7.19         | 4.42 / 4.43         |
| RMTPP               | 34.15     | 3.47     | 0.749     | 6.86 / 6.88         | 7.08 / 6.69         |
| RMTPP-K             | 33.63     | 3.24     | 0.749     | 7.10 / 7.11         | 5.82 / 5.52         |
| NHP                 | 35.43     | 3.41     | 0.696     | 6.97 / 6.98         | 5.59 / 5.61         |
| AttNHP              | 31.12     | 1.21     | 0.717     | 7.52 / 7.50         | 1.71 / 1.48         |
| ODE                 | 35.60     | 3.34     | 0.695     | 6.96 / 6.97         | 5.53 / 5.52         |
| HYPRO               | 34.26     | 3.46     | 0.758     | 7.04 / 7.05         | 7.79 / 7.05         |
| DeTPP               | 35.04     | 3.85     | 0.688     | **6.65** / **6.66** | 9.18 / 9.17         |
| DeTPP+              | **38.29** | **4.67** | **0.638** | 6.68 / 6.70         | **9.59** / **9.26** |

### MIMIC-IV
| Method              | Acc.      | mAP       | MAE      | OTD  Val / Test       | T-mAP  Val / Test     |
|:--------------------|:----------|:----------|:---------|:----------------------|:----------------------|
| MostPopular         | 4.77      | 2.75      | 14.52    | 19.82 / 19.82         | 0.55 / 0.54           |
| RecentHistory       | 1.02      | 2.63      | 5.34     | 19.75 / 19.73         | 2.41 / 2.49           |
| MAE-CE              | 58.59     | **47.32** | 3.00     | **11.51** / **11.53** | 21.93 / 21.67         |
| MAE-CE-K            | 57.91     | 44.60     | 3.07     | 13.17 / 13.18         | 22.46 / 22.30         |
| RMTPP               | 58.33     | 46.24     | 3.89     | 13.64 / 13.71         | 21.49 / 21.08         |
| RMTPP-K             | 57.48     | 43.47     | 3.62     | 14.68 / 14.72         | 20.70 / 20.39         |
| NHP                 | 24.97     | 11.12     | 6.53     | 18.59 / 18.60         | 7.26 / 7.32           |
| AttNHP              | 42.75     | 28.55     | 3.08     | 14.66 / 14.68         | 22.64 / 22.46         |
| ODE                 | 43.21     | 25.34     | 2.93     | 14.71 / 14.74         | 15.41 / 15.18         |
| HYPRO               | 58.35     | 45.45     | 3.95     | 14.82 / 14.87         | 16.94 / 16.77         |
| DeTPP               | 28.62     | 25.44     | **2.74** | 12.86 / 12.85         | **30.92** / **30.63** |
| DeTPP+              | **58.66** | 46.56     | 3.01     | 12.94 / 12.95         | 30.73 / 30.35         |

### Retweet
| Method              | Acc.      | mAP       | MAE       | OTD  Val / Test       | T-mAP  Val / Test     |
|:--------------------|:----------|:----------|:----------|:----------------------|:----------------------|
| MostPopular         | 58.50     | 39.85     | 18.82     | 174.9 / 173.5         | 25.15 / 23.91         |
| RecentHistory       | 50.29     | 35.73     | 21.87     | 152.3 / 150.3         | 29.12 / 29.24         |
| MAE-CE              | 59.95     | 46.53     | 18.27     | 173.3 / 172.7         | 34.90 / 31.75         |
| MAE-CE-K            | 59.55     | 45.09     | **18.21** | 168.6 / 167.9         | 37.11 / 34.73         |
| RMTPP               | 60.07     | 46.81     | 18.45     | 167.6 / 166.7         | 47.86 / 44.74         |
| RMTPP-K             | 59.99     | 46.34     | 18.33     | 164.7 / 163.9         | 49.07 / 46.16         |
| NHP                 | **60.08** | **46.83** | 18.42     | 167.0 / 165.8         | 48.31 / 45.07         |
| AttNHP              | 60.03     | 46.74     | 18.39     | 173.3 / 171.6         | 28.32 / 25.85         |
| ODE                 | 59.95     | 46.65     | 18.38     | 166.5 / 165.3         | 48.70 / 44.81         |
| HYPRO               | 59.87     | 46.69     | 18.75     | 171.4 / 170.7         | 49.90 / 46.99         |
| DeTPP               | 59.46     | 45.82     | 18.34     | 137.9 / 134.4         | 60.96 / 57.37         |
| DeTPP+              | 60.04     | 46.76     | 18.35     | **136.4** / **132.9** | **61.47** / **57.93** |

### Amazon
| Method              | Acc.      | mAP       | MAE       | OTD  Val / Test     | T-mAP  Val / Test     |
|:--------------------|:----------|:----------|:----------|:--------------------|:----------------------|
| MostPopular         | 33.46     | 9.58      | 0.304     | 7.20 / 7.18         | 8.59 / 8.31           |
| RecentHistory       | 24.23     | 8.15      | 0.321     | 6.43 / 6.41         | 9.73 / 9.21           |
| MAE-CE              | 35.73     | 17.14     | 0.242     | 6.58 / 6.52         | 21.94 / 22.56         |
| MAE-CE-K            | 35.11     | 16.48     | 0.246     | 6.72 / 6.68         | 22.06 / 22.57         |
| RMTPP               | 35.76     | 17.21     | 0.294     | 6.62 / 6.57         | 19.70 / 20.06         |
| RMTPP-K             | 35.06     | 16.37     | 0.300     | 6.92 / 6.87         | 17.85 / 18.12         |
| NHP                 | 11.06     | 11.22     | 0.449     | 9.04 / 9.02         | 26.24 / 26.29         |
| AttNHP              | 31.83     | 9.70      | 0.461     | 7.32 / 7.30         | 14.50 / 14.62         |
| ODE                 | 7.54      | 10.14     | 0.492     | 9.48 / 9.46         | 23.54 / 22.96         |
| HYPRO               | 35.69     | 17.21     | 0.295     | 6.63 / 6.61         | 20.58 / 20.53         |
| DeTPP               | 34.32     | 15.84     | 0.260     | **6.03** / **5.98** | 36.88 / 37.18         |
| DeTPP+              | **35.77** | **17.27** | **0.237** | **6.03** / **5.98** | **37.08** / **37.20** |

### StackOverflow
| Method              | Acc.      | mAP       | MAE       | OTD  Val / Test       | T-mAP  Val / Test     |
|:--------------------|:----------|:----------|:----------|:----------------------|:----------------------|
| MostPopular         | 42.90     | 5.45      | 0.744     | 13.56 / 13.77         | 6.10 / 5.56           |
| RecentHistory       | 26.42     | 5.20      | 0.934     | 14.52 / 14.55         | 8.67 / 6.72           |
| MAE-CE              | 45.41     | 13.00     | 0.641     | 13.57 / 13.64         | 8.78 / 8.31           |
| MAE-CE-K            | 44.85     | 11.16     | 0.644     | 13.41 / 13.51         | 12.42 / 11.42         |
| RMTPP               | 45.43     | 13.33     | 0.701     | 12.95 / 13.17         | 13.26 / 12.72         |
| RMTPP-K             | 44.89     | 11.72     | 0.689     | 12.92 / 13.13         | 14.91 / 14.30         |
| NHP                 | 44.53     | 10.86     | 0.715     | 13.02 / 13.24         | 12.67 / 11.96         |
| AttNHP              | 45.17     | 12.67     | 0.705     | 13.08 / 13.30         | 11.95 / 11.13         |
| ODE                 | 44.38     | 10.12     | 0.711     | 13.04 / 13.27         | 11.37 / 10.52         |
| HYPRO               | 45.18     | 12.88     | 0.715     | 13.04 / 13.26         | 15.57 / 14.69         |
| DeTPP               | 44.81     | 12.33     | 0.660     | **11.95** / **12.06** | **24.44** / **23.11** |
| DeTPP+              | **45.53** | **14.00** | **0.639** | 12.04 / 12.14         | 23.80 / 22.72         |

# Tests
To run tests, use the following command:
```sh
pytest tests
```
