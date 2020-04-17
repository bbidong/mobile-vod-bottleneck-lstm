# 数据集
只用下载`VID dataset 86GB`这个，其中的test没有Annotations

datasets目录下的`train_VID_list.txt`等txt文件可通过`get_VID_list.py`,  `get_VID_seq_list.py`得到

- `train_VID_list.txt`: 保存train数据集3862个snippets中所有img(前提：object个数>0)的路径
- `val_VID_list.txt`: 保存val数据集每个snippets（555个）的前20个frame的路径，见 paper Section 4.1 最后一段，但不知为啥一共是11080个（11080/20=554）
- `train_VID_seqs_list.txt`: 把`train_VID_list.txt`的10行合成1行
- `val_VID_seqs_list.txt`: 同理
# 环境
- python 3.6 (3.5会报错)
# 文件结构
- ·evaluate.py·: 评估
- `datasets/vid_dataset.py`: 读取数据集，读取Annotations
- `dataloaders/data_preprocessing.py`: 处理数据，resize, mean, std等
- `network/predictor.py`: 给定img，进行数据处理（按照config/mobilenetv1_ssd_config.py的参数resize,mean,std）, 模型前传，
