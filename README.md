# 服装关键点检测模型训练和测试说明
本模型使用了全卷积网络解决服装关键点定位问题，给出了基于tensorflow的代码模型。

## 运行环境
tensorflow1.3.0，
opencv2.4，
python3.5，
numpy 1.13.3

## 参数文件
用于调整模型的所有参数都放在'config.cgf'里面。

	training_txt_file : 存放图片信息的csv文件路径
	img_directory : 图片存放路径
	img_size : 图片的大小
	hm_size : 热图的大小
	num_joints : 关键点的数量
	joint_list: 关键点列表
	name : 训练模型名
	nFeats: 卷积层中特征的数量
	nStacks: stack的数量
	nModules : 模型数量
	nLow : 下采样的数
	dropout_rate : 训练结尾神经元舍弃的比例
	batch_size : batch的大小
	nEpochs : epoch的大小
	epoch_size : 每个epoch中循环次数
	learning_rate: 学习率
	learning_rate_decay: 学习率的衰减速度（一般设为（0.0-0.99））
	decay_step : 学习率衰减次数
	valid_iteration : 用于validation的数量
	log_dir_test : 测试文件的路径
	log_dir_train : 训练文件的路径
	saver_step : 写入训练文件的步长
	saver_directory:保存训练模型的路径
  

## 训练步骤
1.运行TRAIN/preprocess.py将数据分为训练集和测试集
```
$ cd TRAIN/
$ python preprocess.py
```
2.运行TRAIN/run.py，其中初始学习率默认设为1e-4
```
$ python run.py
```
3.观测结果，当loss-coor开始震荡，学习率调整为1e-5，继续训练，知道梯度不再下降

## 测试步骤
1.运行TEST/run.py进行测试，结果保存在csv文件
```
$ cd TEST/
$ python run.py
```
## 补充说明
### 工程结构
所有的训练数据和测试数据都在data文件夹下

测试过程的中间文件都保存在log文件夹下

最终的测试结果保存在log/hgs/eva/testb_multi_avg/submit.csv中
```Shell
Project
   	TRAIN
   		models.py
		preprocess.py
		run.py
	TEST
		models.py
		run.py
	data
		train
			Annotation
			train.csv
			Images
			...
		test
			Images
			...
	log
		hgs
			eva
				test_multi_flip_avg
				submit.csv
				model1
				...
				model2
				...
				console
				epoch0...
				...
   
```
### 整体思路
根据Hourglass关节定位模型进行改进


