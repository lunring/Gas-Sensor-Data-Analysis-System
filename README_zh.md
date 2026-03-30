# 气体传感器数据分析系统 (GSDAS)

气体传感器数据分析系统（Gas Sensor Data Analysis System）是一个开源图形用户界面工具，旨在简化气体传感器动态响应-恢复曲线的分析过程。该程序使用 Python 3 编写，采用 matplotlib、pandas、NumPy 和 SciPy 等开源库进行数据可视化、处理和拟合。图形界面使用 PyQt 构建，因为它提供了出色的灵活性和跨操作系统兼容性。该系统可以同时分析最多八个共享同一时间数据的样品，将分析过程缩短至几分钟，并使用统一的计算标准来获取气体传感器的三个核心参数：响应值、响应时间和恢复时间。

当前为 Beta 测试版本，采用 GNU 许可证。

欢迎提交建议和错误报告！

## 功能特性

典型的气体传感器响应-恢复曲线是将传感器信号作为时间的函数进行绘制。现代工业或学术界的实验平台可以在多个暴露周期内同时记录多个传感器的数据，产生大量需要分析的数据。如果手动分析，不仅繁琐，还容易出错。

气体传感器数据分析系统可以处理包含最多八个共享同一时间数据的样品的 CSV 文件。系统假设第一列为时间数据，其余各列为记录传感器信号的不同通道。

系统提供以下功能：

1. 绘制和可视化数据；
2. 定义感兴趣的数据区域；
3. 数据归一化用于对比分析；
4. 同时计算数据文件中所有通道的响应值、响应时间和恢复时间；
5. 对响应数据进行幂律（Power-law）拟合；
6. 线性拟合，斜率即为灵敏度（响应/浓度）；
7. 导出所有分析数据；

## 系统要求

| 项目 | 要求 |
|------|------|
| 操作系统 | Windows 8 / 8.1 / 10 |
| 处理器 | 1.6 GHz |
| 内存 | 4 GB RAM |

## 安装方式

### 方式一：独立安装版

下载 `gsdas 0.9.exe` 安装程序，点击 [此处](https://drive.google.com/drive/folders/1eW2FeAMugAU2CMUTQ32T6FijdTAGAont?usp=sharing) 获取。

### 方式二：从源码运行

1. 克隆仓库：
```bash
git clone https://github.com/lunring/Gas-Sensor-Data-Analysis-System.git
cd Gas-Sensor-Data-Analysis-System
```

2. 创建虚拟环境并安装依赖：
```bash
python -m venv venv
venv\Scripts\activate          # Windows
# source venv/bin/activate     # Linux/Mac

pip install PyQt5 matplotlib pandas numpy scipy
```

3. 运行程序：
```bash
python "gsdas 0.9.4.py"
```

## 测试数据

为方便测试软件的全部功能，提供以下测试数据文件：

### dataSample_1

该数据集对应四个不同的 rGO（还原氧化石墨烯）基传感器，通过控制 NO<sub>2</sub> 暴露（0.5 ~ 5 ppm）记录其电阻变化。每个暴露周期持续 10 分钟，恢复 50 分钟。有关测量的实验详情，请参阅 dataSample_1 文件中的实验说明。

### dataSample_2

该数据集对应两个 ZnO 基传感器在控制 O<sub>3</sub> 暴露（50 ~ 500 ppb）下的稳定性测试，测试持续一个月。通道 1、2、3 是一个传感器在三周内的数据，通道 4、5、6 是另一个类似样品在相同三周内的数据。

每个暴露周期持续 15 分钟，恢复 60 分钟。有关测量的实验详情，请参阅 dataSample_2 文件中的实验说明。

### dataSample_3

该数据集对应聚苯胺（PANI）薄膜在控制氨气暴露（50 ~ 500 ppm）下的动态响应-恢复曲线。

每个暴露周期持续 15 分钟，恢复 45 分钟。有关测量的实验详情，请参阅 dataSample_3 文件中的实验说明。

## 信号类型说明

系统支持以下三种响应计算方式：

| 类型 | 公式 | 说明 |
|------|------|------|
| ΔS/S0 (%) | (R<sub>f</sub> - R<sub>0</sub>) / R<sub>0</sub> × 100% | 相对变化百分比（默认） |
| ΔS | R<sub>f</sub> - R<sub>0</sub> | 绝对变化值 |
| S(gas)/S(air) | R<sub>f</sub> / R<sub>0</sub> | 气体/空气信号比 |

其中 R<sub>0</sub> 为暴露前的初始信号值，R<sub>f</sub> 为暴露结束时的信号值。

附加选项：
- **Signal/conc**：将响应值除以浓度，用于消除浓度影响
- **Sensitivity**：通过线性回归计算灵敏度（斜率）

## 作者

Bruno S. de Lima, Weverton A. S. Silva, Amadou L. Ndiaye, Valmor R. Mastelaro, Jérôme Brunet

## 致谢

本工作得到了圣保罗研究基金会（São Paulo Research Foundation）的资金支持。

## 许可证

本项目采用 GNU 许可证，详见 [LICENSE](LICENSE) 文件。
