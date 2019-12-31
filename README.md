# 物品识别

使用SSD 算法识别图片中的物体
```

├── README.md                   说明文件
├── SSD300                      SSD算法模型
├── client-camera.py            本地摄像机识别代码
├── server-train.ipynb          服务器上训练模型的代码   
├── dataset                     临时文件
├── output                      模型和log输出文件夹
└── raw-data                    训练数据文件夹
    ├── Annotations             标记数据
    └── JPEGImages              图片文件

```
 
 
 
###训练模型
参考[server-train.ipynb](./server-train.ipynb)


###使用模型

参考 [client-camera.py](./client-camera.py)