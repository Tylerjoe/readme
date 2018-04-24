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
运行train/train_launcher.py，其中初始学习率默认设为0.00025，训练过程中，每隔3000步，学习率衰减百分比0.96
```
$ cd train/
$ python train_launcher.py
```

## 测试步骤
运行test/test_launcher.py进行测试，结果保存为csv文件
```
$ cd test/
$ python test_launcher.py
```
## 补充说明
### 工程结构
所有的训练数据在train/data文件夹下，测试数据在test/data文件夹下

测试过程的中间文件都保存在log_dir文件夹下

```Shell
Project
   	train
		data
			Images
			Annotations
   		model.py
		mydatagen.py
		train_launcher.py
		myconfig.cfg
	test
		data
			Images
		model.py
		predictClass.py
		myconfig.cfg
		test_launcher.py
```
### 整体思路
使用经典Hourglass定位模型进行改进



