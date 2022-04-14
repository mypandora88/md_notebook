## opencv软件库
OpenCV是一个基于Apache2.0许可（开源）发行的跨平台计算机视觉和机器学习软件库，可以运行在Linux、Windows、Android和Mac OS操作系统上。它轻量级而且高效——由一系列 C 函数和少量 C++ 类构成，同时提供了Python、Ruby、MATLAB等语言的接口，实现了图像处理和计算机视觉方面的很多通用算法。

OpenCV用C++语言编写，它具有C ++，Python，Java和MATLAB接口，并支持Windows，Linux，Android和Mac OS，OpenCV主要倾向于实时视觉应用，并在可用时利用MMX和SSE指令， 如今也提供对于C#、Ch、Ruby，GO的支持。

OpenCV Python只是一个与Python一起使用的原始C++库的包装类。通过使用它，所有OpenCV数组结构都能被转化为NumPy数组或从NumPy数组转化而来。这样就可以轻松地将其与其他使用NumPy的库集成。例如，SciPy和Matplotlib等库。

### 计算机视觉
在机器视觉系统中，计算机会从相机或者硬盘接收栅格状排列的数字，也就是说，最关键的是，机器视觉系统不存在一个预先建立的模式识别机制。没有自动控制焦距和光圈，也不能将多年的经验联系在一起。大部分的视觉系统都还处于一个非常朴素原始的阶段。

图 1 展示了一辆汽车。在这张图片中，我们看到后视镜位于驾驶室旁边。但是对于计算机而言，看到的只是按照栅格状排列的数字。所有在栅格中给出的数字还有大量的噪声，所以每个数字只能给我们提供少量的信息，但是这个数字栅格就是计算机所能够“看见”的全部了。我们的任务变成将这个带有噪声的数字栅格转换为感知结果“后视镜”。

![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220112110911.png)

图 2 给出了为什么计算机视觉如此困难的另一些解释。

![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220112110938.png)

#### 场景信息可以辅助计算机视觉
考虑这样一个例子，一个移动机器人需要在一栋建筑中找到并且拿起一个订书机。机器人就可能用到这样的事实：桌子通常放在办公室里，而订书机通常收纳在桌子里。这也同样给出了一个关于尺寸的推断：订书机的大小一定可以被桌子所收纳。

更进一步，这还可以帮助减少在订书机不可能出现的地方错误识别订书机的概率（比如天花板或者窗口）。机器人可以安全忽略掉 200 英尺高的订书机形状的飞艇，因为飞艇没有满足被放置在木制桌面上的先验信息。

#### 使用统计的方法来对抗噪声
计算机视觉所面临的下一个问题是噪声，我们一般使用统计的方法来对抗噪声。

比如，我们很难通过单独的像素点和它的相邻像素点判断其是否是一个边缘点，但如果观察它在一个区域的统计规律，边缘检测就会变得更加简单了。

一个真正的边缘应该表现为一个区域内一连串独立的点，所有点的朝向都与其最接近的点保持一致。我们也可以通过时间上的累计统计对噪声进行抑制，当然也有通过现有数据建立噪声模型来消除噪声的方法。例如，因为透镜畸变很容易建模，我们只需要学习一个简单的多项式模型来描述畸变就可以几乎完美矫正失真图像。

### OpenCV的基础操作？
Opencv能完成以下从加载图像到调整大小等基本操作：

- 使用OpenCV加载图片
>```
>Import cv2
> # colored Image
> Img = cv2.imread ("Penguins.jpg",1)  
> # Black and White (gray scale)  
> Img_1 = cv2.imread ("Penguins.jpg",0)  
>  ```

- 查看图片形状/分辨率
>```
>Import cv2  
># Black and White (gray scale)  
>Img = cv2.imread ("Penguins.jpg",0)  
>Print(img.shape)  
> ```

- 显示图片
> ```
> import cv2  
> # Black and White (gray scale)  
> Img = cv2.imread ("Penguins.jpg",0)  
> cv2.imshow("Penguins", img)  
> cv2.waitKey(0)  
> # cv2.waitKey(2000)  
> cv2.destroyAllWindows()
> ```

- 调整图像大小
> ```
> import cv2  
> # Black and White (gray scale)  
> img = cv2.imread ("Penguins.jpg",0)  
> resized_image = cv2.resize(img, (650,500))  
> cv2.imshow("Penguins", resized_image)  
> cv2.waitKey(0)  
> cv2.destroyAllWindows()
> ```

### 使用OpenCV进行人脸检测
- 第一步：想一想我们的先决条件。我们首先需要一个图像。然后，我们需要创建一个级联分类器，它最后会给我们提供面部特征。
- 第二步：这一步要使用到OpenCV读取图像和特征文件。所以这个时候，原始数据点是NumPy数组的形式。我们要做的就是搜索面部 NumPy n维数组的行和列的值。这是具有面部矩形坐标的数组。
- 第三步：最后一步是使用矩形面框显示图像。

![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220112110019.png)

### 使用OpenCV捕获视频
