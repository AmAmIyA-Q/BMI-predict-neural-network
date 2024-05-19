##  二方互信息回归预测神经网络（BMI-predict-neural-network）

用于预测多体物理量子系统二方互信息的 Python 代码，可以进一步用于计算系统的三方互信息，研究信息置乱现象。

Python code used to predict the bipartite mutual information of multi-body physical quantum systems can be further used to calculate the tripartite mutual information of the system and study the phenomenon of information scrambling.

## 数据集产生

Jupyter notebook 代码  ```density_matrix_generator.ipynb``` 用于产生随机的密度矩阵，产生的矩阵既包括纯态也包含混合态。产生密度矩阵的原理如下：

Jupyter Notebook code ``` dentity_matrix_generator. ipynb ``` is used to generate a random density matrix that includes both pure and mixed states. The principle of generating density matrix is as follows:

$$\hat{\rho}=\sum_i P_i|\psi_i\rangle\langle\psi_i|,~\sum_i P_i =1.$$

更进一步，通过计算矩阵偏迹获得子系统的密度矩阵：

Furthermore, by calculating the matrix bias, the density matrix of the subsystem is obtained:

$$\rho_A=Tr_B(\rho_{AB})$$

$$\rho_B=Tr_A(\rho_{AB})$$
<!-- $$\mathrm{Tr}_B(C)=\sum_{i=0}^{n-1}(I_n\otimes \langle i|)C(I_n\otimes|i\rangle)$$


$$\mathrm{Tr}_A(C)=\sum_{i=0}^{n-1}\left( \langle i|\otimes I_n\right)C(|i \rangle\otimes I_n)$$ -->

最后根据二方互信息、冯诺依曼熵、可观测量的计算方法，产生数据集。

Finally, based on the calculation methods of mutual information, von Neumann entropy, and observability, a dataset is generated.

$$I_2(A:B)=S\left(\rho_A\right)+S\left(\rho_B\right)-S\left(\rho_{AB}\right),$$

$$S\left(\rho\right)=-\sum_i\left(\lambda_i\log\lambda_i\right)$$

$$o_i(\rho)=\mathrm{trace}(O_i\rho)$$

数据集文件夹目录结构：

Dataset folder directory structure:


```
├── data
│   ├── all
│   ├── entropy_A
│   ├── entropy_AB
│   ├── entropy_B
│   ├── I2
│   ├── if_pure
│   ├── observable0
│   ├── observable1
│   ├── observable10
│   ├── observable11
│   ├── observable12
│   ├── observable13
│   ├── observable14
│   ├── observable15
│   ├── observable2
│   ├── observable3
│   ├── observable4
│   ├── observable5
│   ├── observable6
│   ├── observable7
│   ├── observable8
│   ├── observable9
│   ├── rho_A
│   ├── rho_AB
│   └── rho_B
```

## 多层感知机 MPL 训练 （Multi layer perceptron MPL training）

预测系统二方互信息分为两步，第一步确定系统的可分离性，可分离系统的二方互信息为零；第二步确定不可分离系统的二方互信息。

### 可分离系统分类器

代码见 ```MPL_classification.ipynb```

神经网络结构如图所示：
![](https://img2.imgtp.com/2024/05/20/pg404N3G.png)

验证集上的准确率可以达到 97%。
![](https://img2.imgtp.com/2024/05/20/G7DBKWKs.png)

### 二方互信息回归器

代码见 ```MPL_entropy_16.ipynb```

神经网络结构如图所示：
![](https://img2.imgtp.com/2024/05/20/9jpin4x0.png)

验证集上的 $MSE$ 损失可以达到 $\approx 7\times 10^{-5}$ 。

![](https://img2.imgtp.com/2024/05/20/765oqUio.png)

