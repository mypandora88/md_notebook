## 第6章 短路计算 IEC法

IEC法中的源分三种：
- 馈电网络
- 电动机
- 发电机

IEC法特点：
- 一切皆是阻抗（**配四4.2节计算**）
- 阻抗要进行修正，计算 $K_T$
- 假想源，使用等效电压源 $cU_n/\sqrt3$ 来代替

注意：
- 变压器计算阻抗时，电压选择短路点侧的电压
- 另外折算时，使用变压器的变比（不要使用2侧母线额定电压比）

### 计算步骤
![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220105223542.png)

电压系数c选择：
![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220105231350.png)

最大&最小短路电流注意点：
![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220105232921.png)

### 阻抗计算
注意中间如果有变压器的时候要进行折算
![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220112222144.png)

- 馈电网络
![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220112222748.png)

- 双绕组变压器
![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220112224622.png)

- 三绕组变压器
![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220112230623.png)

- 电缆架空线
![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220114222254.png)

- 限流电抗器
![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220114224742.png)

- 同步电动机
![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220114225512.png)

- 发变组
见考点总结

- 异步电动机
![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220114232615.png)

### 短路电流计算
![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220116093011.png)

#### 短路电流初始值计算
![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220115231707.png)

#### 短路电流峰值计算
![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220115232501.png)

#### 短路直流分量计算（断路器开断的直流分量）
![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220115234030.png)

#### 短路开断电流（断路器开断的交流分量）
![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220115235537.png)

#### 稳态短路分量（交流分量稳定值）
![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220116094601.png)

### 短路电流热效应
![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220116100315.png)

### 其它
![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220115232156.png)