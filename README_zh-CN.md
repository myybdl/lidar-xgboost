# xgboot 点云分类 

## 文件与目录说明
    /data   数据集
    /docu
    /img
    01. XGBoost Tuning for Aerial LiDAR Data Classification.ipynb
    02. XGBoost for Aerial LiDAR Data Classification with extended training dataset.ipynb
    03. XGBoost for Aerial LiDAR Data Classification with EDA.ipynb

    - 中文版
        01. XGBoost调参用于点云分类.ipynb            
    - 自己的点云数据
        01. XGBoost调参用于点云分类 -PowerLine.ipynb

    01 1块训练验证（01.Train_Test_Area.csv），测试（01.Test_Area.csv） =>训练90+%，测试50+%，过拟合
    02 6块训练验证（02.Train_Validation_Area_1～6），测试（02.Test_Area.csv） =》测试精度更低，仍然过拟合
    03 EDA - 探索性数据分析 =》略有提高

    01 具体操作
        对比默认参数和优化调参，GridSearch搜索特征权重；
        训练数据调整介绍太多的类型，自动生成太少的样本，最后一样的数量；
        选择了8个特征

## 开发环境
    conda create -n MLvsLiDAR python==3.6 scikit-learn pandas 
    matplotlib =>只是显示一个类别分布直方图，基本没用，反而要讲pandas和numpy降级，不装
    conda install py-xgboost-gpu
    xgboost,sklearn,pandas,numpy
## 工作记录
1. 运行问题：cv_results_ 是在sklearn的 0.18.1提出的 ，早期版本中不是这个函数，而是 grid_scores_
2. 考虑结合Urban项目代码，提取一些空间特征
3. 最好用标准数据集做测试，有对比

## GPU使用
    conda安装GPU版本xgboost
    GPU算法(gpu_exact, gpu_hist)配NVIDIA GPUs，多GPUs只在Linux平台支持
    使用方法：
        param['gpu_id'] = 0
        param['max_bin'] = 16
        param['tree_method'] = 'gpu_hist'