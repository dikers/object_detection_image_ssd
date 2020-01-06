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
 
 
 
### 训练模型

参考[server-train.ipynb](./server-train.ipynb)


### 使用模型

参考 [client-camera.py](./client-camera.py)

---------------------------------------------------

### 第一步 准备图片

录制需要识别物体的视频， 或者直接拍摄图片

安装ffmpeg   
```
 ffmpeg -ss 00:00 -i test.mov -f image2  -s 640x426 -r 1 -t 01:00 test_%3d.jpg
 
 -ss 开始时间
 -i  视频路径
 -f  类型
 -s  大小
 -r   速率， 每秒一张图片
 -t 结束时间
 201_%3d.jpg  对图片进行命名

```

将所有的图片放置到一个文件夹
```shell
raw-data/
    JPEGImages/   #所有图片
    Annotations/  #所有xml标记信息

```

然后进行打标签工作

---------------------------------
### 第二步 打标签

打标签工具下载地址
[项目地址](https://github.com/wkentaro/labelme)

![image](https://github.com/wkentaro/labelme/raw/master/examples/instance_segmentation/.readme/annotation.jpg)

```
Ctrl + u	Load all of the images from a directory
Ctrl + r	Change the default annotation target dir
Ctrl + s	Save
Ctrl + d	Copy the current label and rect box
Space	Flag the current image as verified
w	Create a rect box
d	Next image
a	Previous image
del	Delete the selected rect box
Ctrl++	Zoom in
Ctrl--	Zoom out
↑→↓←	Keyboard arrows to move selected rect box
```


分别设置图片的文件夹位置  和生成的xml保存路径， 然后进行打标签工作。 

===================================
### 第三步  上传图片和xml标签数据到服务器

图片上传路径        base_dir + 'JPEGImages/' 

标记数据上传路径     base_dir + 'Annotations/' 


将本地图片和xml 标记数据 压缩， 然后上传到服务器上

```shell
#压缩本地文件 zip 格式
zip raw-data.zip  raw-data/
scp  -i "~/bin/key.pem"  raw-data.zip  ec2-user@ip_adress:/home/ec2-user/examples/object_detection_image_ssd/
```

登录到服务器

```shell

cd /home/ec2-user/examples/object_detection_image_ssd/
rm -fr raw-data
unzip raw-data.zip
```
新建好的路径如下： 
```
object_detection_image_ssd/
    raw-data/
        JPEGImages/   #所有图片
        Annotations/  #所有xml标记信息

```



