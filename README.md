# DeepSTN+

Keras implementation of ***DeepSTN+: Context-aware Spatial-Temporal Neural Network for Crowd Flow Prediction in Metropolis. Ziqian Lin^, Jie Feng^, Ziyang Lu, Yong Li, and Depeng Jin. AAAI 2019.*** (^ indicates equal contribution) [PDF](https://vonfeng.github.io/files/AAAI19_DeepSTN+.pdf) If our codes is helpful to your research, you can cite our work by:
```latex
@article{lin2019deepstn+:,
title={DeepSTN+: Context-aware Spatial Temporal Neural Network for Crowd Flow Prediction in Metropolis},
author={Lin, Ziqian and Feng, Jie and Lu, Ziyang and Li, Yong and Jin, Depeng},
booktitle={Thirty-Thrid AAAI Conference on Artificial Intelligence},
year={2019}
}
```

# Datasets

Similar to [ST-ResNet](https://github.com/lucktroy/DeepST), our dataset is from the [NYC Bike](https://www.citibikenyc.com/system-data). Besides, we collect 9 types of PoIs for this dataset. The spatial map size of the dataset is 21x12. The dataset is in the folder /DATA/dataBikeNYC flow_data.npy ( TimeLenth x In&OutFlow x MapHeight x MapWidth = 4392 x 2 x 21 x 12 ) and poi_data.npy ( PoICategories x MapHeight x MapWidth = 9 x 21 x 12 ) for directly used.

# Requirements

- python 3.5
- Keras 2.0
- NumPy

# Project Structure

File BikeNYC corresponds the Dataset BikeNYC in the Paper DeepSTN+.

- /DATA
  - dataBikeNYC contain dataset flow_data.npy and poi_data.npy
  - lzq_read_data_time_poi.py transfer flow_data.npy and poi_data.npy to the input of the DeepSTN+ network
- /DST_network baseline from [ST-ResNet](https://github.com/lucktroy/DeepST)
  - ilayer.py 
  - metrics.py
  - STResNet.py 
- /DeepSTN_00/SCORE are used to save the results of DeepSTN
- /DeepSTN_10/SCORE are used to save the results of DeepSTN+plus
- /DeepSTN_01/SCORE are used to save the results of DeepSTN+PoI$*$time
- /DeepSTN_11/SCORE are used to save the results of DeepSTN+plus+PoI$*$time
- /DeepSTN_network
  - DeepSTN_net.py  model codes for DeepSTN+
  - metrics.py contains the metric RMSE
- /ComparisonBikeNYC.py ***you can run this file to get the results of ST-ResNet and DeepSTN in the paper.***

# Usage

> python ComparisonBikeNYC.py

# Other parameters:

> Refer to ComparisonBikeNYC.py and DeepSTN_net.py 

- for training:
  - epoch, batch_size, lr, days_test, iterate_num
  - XDST, X11, X10, X01, X00,  trainDST, train11, train10, train01, train00
- model definition:
  H, W, channel, T, 
  len_closeness, len_period, len_trend, 
  T_closeness, T_period, T_trend, 
  pre_F, conv_F, R_N, drop,
  is_plus, plus, rate,
  is_pt, P_N, T_F, PT_F,
  is_summary, kernel1, isPT_F
