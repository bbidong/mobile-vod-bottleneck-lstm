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
- `evaluate.py`: 把预测结果按class保存在`eval_results`下，以`det_test_airplane.txt`为例，格式如下，从左往右依次为 img路径，score概率，x1, y1, x2, y2 
  > ILSVRC2015_val_00000000/000006 0.010405004 442.01465 26.026163 619.0668 200.16707
  
  然后计算每个预测结果和对应Annotations的IOU, 如果IOU>阈值，则为TP, 否则为FP, 接着得到precision, recall, 计算AP
- `datasets/vid_dataset.py`: evaluate的时候用，读取数据集，读取Annotations
- `datasets/vid_dataset_new.py`: train的时候用
  - class ImagenetDataset: single frame用，`self.db`保存着训练数据的image_path, boxes, lables, 格式如下：
  
![](https://github.com/bbidong/mobile-vod-bottleneck-lstm/blob/master/zxd/fig/ImagenetDataset_db.PNG)
  
- `dataloaders/data_preprocessing.py`: 处理数据，resize, mean, std等
- `network/predictor.py`: 给定img，进行数据处理（按照config/mobilenetv1_ssd_config.py的参数resize,mean,std）, 模型前传，nmt筛选，输出预测结果
