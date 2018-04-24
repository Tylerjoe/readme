# 服装关键点检测模型训练和测试说明
本模型使用了全卷积网络解决服装关键点定位问题，给出了基于tensorflow的代码模型。

需要依赖tensorflow和opencv

## 参数文件
用于调整模型的所有参数都放在'config.cgf'里面。

	training_txt_file : 存放图片信息的txt文件路径
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
  
## 训练
'config.cgf'中的img_directory添加存放图片文件夹的路径，training_txt_file添加图片信息的txt文件的路径，其他的训练参数可以可以相应调整。

运行train_launcher.py文件开始训练，会自动的载入'config.cgf'文件中的相关参数。

训练相关的.py文件：

	train_launcher.py : 训练程序进入文件
	datagen.py : 训练初始化文件
	hourglass_tiny.py : 训练模型文件

在训练结束后，后自动的保存
