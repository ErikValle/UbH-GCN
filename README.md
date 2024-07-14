# UbH-GCN [ECCV 2024]

Official Implementation of [Upper-body Hierarchical Graph for Skeleton Based Emotion Recognition in Assistive Driving]

## Abstract
Emotion recognition plays a crucial role in enhancing the safety and enjoyment of assistive driving experiences. By enabling intelligent systems to perceive and understand human emotions, we can significantly improve human-machine interactions. Current research in emotion recognition emphasizes facial expressions, speech and physiological signals, often overlooking body movement's expressive potential. Existing most methods, reliant on full-body poses and graph convolutional networks with predetermined adjacency matrices, face challenges in driving scenarios, including limited visibility, restricted movement and imbalanced data distribution, which affect model generalization and accuracy. To overcome these limitations, we introduce an innovative emotion recognition method tailored for assistive driving. Our method leverages upper-body skeleton sequences, overcoming the constraints of full-body pose capture in driving scenario. Our architecture employs an upper-body hierarchical graph (UbH-Graph) to dynamically capture upper-body movement and emotion relationships. We uniquely incorporate class-specific variations during training, balancing feature distribution and enhancing emotion recognition. Our method outperforms existing multimodal approaches on the assistive driving dataset and demonstrates robustness and adaptability on the daily action dataset.

## Dependencies

- Python >= 3.9
- PyTorch >= 2.0.1
- torchpack == 0.2.2
- PyYAML, matplotlib, einops, sklearn, tqdm, tensorboardX, h5py
- Run `pip install -e torchlight` 

## Data Preparation

### AIDE
1. Request dataset from here: https://github.com/ydk122024/AIDE
2. Extract `AIDE_Dataset/` to `./data/AIDE/raw_data/`

### Data Processing

#### Directory Structure

Put downloaded data into the following directory structure:

```
- data/
  - AIDE/
    - raw_data
      ... # raw data of AIDE
    - processed_data
      ... # processed data of AIDE
  - Emliya/
    - raw_data
      ...
    - processed_data
      ...
```

#### Generating Data

- Generate AIDE dataset:

```
 cd ./data/AIDE
 # Get skeleton
 python get_raw_skes_data.py
```


## Training & Testing

### Training

- AIDE
```
# Example: training UbH-GCN (joint root 1) on AIDE with GPU 0
python main.py --config ./config/AIDE/joint_root_1.yaml --device 0
```

- To train your own model, put model file `your_model.py` under `./model` and run:

```
# Example: training your own model on AIDE
python main.py --config ./config/AIDE/your_config.yaml --model model.your_model.Model --work-dir ./work_dir/your_work_dir/ --device 0
```
### Testing

- To test the trained models saved in <work_dir>, run the following command:

```
python main.py --config <work_dir>/config.yaml --work-dir <work_dir> --phase test --save-score True --weights <work_dir>/xxx.pt --device 0
```

- To ensemble the results of different modalities, run 
```
# Example: six-way ensemble for NTU-RGB+D 120 cross-subject
python ensemble.py --datasets AIDE --main-dir ./work_dir/AIDE/
```

### Pretrained Weights

- Pretrained weights for AIDE can be downloaded from the following link [[Google Drive]]() or [[Baidu Yun]]().

## Acknowledgements
This repo is based on [2s-AGCN](https://github.com/lshiwjx/2s-AGCN), [CTR-GCN](https://github.com/Uason-Chen/CTR-GCN) and [HD-GCN](https://github.com/Jho-Yonsei/HD-GCN). The data processing is borrowed from [AIDE](https://github.com/ydk122024/AIDE).

Thanks to the original authors for their awesome works!

# Citation

Please cite this work if you find it useful:
```BibTex

```

# Contact
If you have any questions, feel free to contact: wujh23@xs.ustb.edu.cn