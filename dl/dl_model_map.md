# 深度学习知识地图

## 1、模型地图

模型分类：小模型、大模型

1. 小模型
   * CV
     * 检测
       * Anchor-based一阶段
         * Yolo系列
           * Yolov1
           * Yolov2
           * Yolov3
           * Yolov4
           * Yolov5
           * Yolov6
           * Yolov7
           * YoloX
       * Anchor-based二阶段
         * RCNN
         * fast RCNN
         * faster RCNN
       * Anchor-Free
     * 分类
     * 分割
       * SAM
     * 生成
       * GAN
   * NLP
     * RNN
     * LSTM
     * Bert
   * 推荐系统
2. 大模型
   - 大语言模型
     - GPT系列
       - GPT3
       - GPT3.5
       - GPR4
     - llama系列
       - llama
       - llama2
     - 国内系列
       - 清华智谱-GLM
         - ChatGLM
       - 百度-文心一言
       - 阿里-通义千问
       - 科大讯飞-星火认知
   - 大图像模型
     - AIGC
       - stable diffuision

## 2、训练优化

训练加速常用手段: 训练加速、模型加速

1. 训练加速
   1. 并行训练
      - 张量并行
      - 数据并行
      - 流水并行
2. 模型加速
   1. 轻量化网络
      - 卷积分解
      - 分组卷积
   2. 模型压缩与量化
      - 网络剪枝
      - 模型量化
      - 知识蒸馏

## 3、推理优化

推理优化方向

1. 分布式并行计算：DeepSpeed、FlexFlow
   - 数据并行
   - 张量并行
   - 流水线并行
2. 服务化schedule：
   - 动态批处理：ORCA、FastServer、vLLM、TGI 
3. 低精度加速：
   - 模型压缩
     - 剪枝稀疏化
     - 量化
     - 蒸馏
4. 计算优化
   - 子图融合: FasterTransofmer、DeepSpeed 、MLC LLM
5. 模型算法优化：
   - Transformer 结构优化
6. 显存优化
   - 硬件系统升级

## 参考

1. [深度学习百科及面试资源](https://paddlepedia.readthedocs.io/en/latest/index.html) · [百度飞浆](https://www.paddlepaddle.org.cn/wholechain)
2. [推理优化](https://zhuanlan.zhihu.com/p/665089816)

课程
1. [CNN、RNN、GAN、LSTM、Transform五大深度神经网络](https://www.bilibili.com/video/BV1oN4y1m75i)
2. [从入门到精通CNN、RNN、GAN、GNN、DQN、Transformer](https://www.bilibili.com/video/BV1TQ4y147sD)

博客
1. [AIGC 绘画理论与保姆级实战](https://zhuanlan.zhihu.com/p/617042733)