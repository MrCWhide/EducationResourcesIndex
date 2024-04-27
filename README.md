# Education Resources Index

**Calculation of educational resource allocation to promote educational equity**
（关于推进教育共富的研究成果以及ERI指数计算工具）

**Author**: 浙江师范大学附属中学 陈怀德 (Chen Huaide)

## 背景

共同富裕是新时代中国特色社会主义教育的根本价值。教育在推动实现社会主义现代化远景目标，促进全体人民共同富裕的历史进程中具有基础性、战略性作用。面向实现现代化的新要求，共同富裕以及教育的作用被赋予更加深远的中国特色的新涵义。

在这一背景下，浙江师范大学附属中学（金华二中）一直努力探索如何推进教育共富这一重要课题。我校全面贯彻党和国家的教育方针和民族政策，坚持育人为本，以立德树人为根本任务，将“以人为本、注重发展、重视过程”作为品德评价的基本理念，着力培养“高品质、有活力”的附中人。

## 研究重点

使用数学方法衡量教育资源分配情况是研究的重点方法。

笔者建立了一个数学模型来衡量教育资源分配情况——ERI指数。

### 变量选取

- **GDP（Gross Domestic Product）**：地区的国内生产总值，反映了该地区的经济发展水平。
- **EB（Education Budget）**：教育支出预算，用于教育事业的经费。
- **TB（Technology Budget）**：科技支出预算，用于科技教育的经费。
- **CCLAI（Capita Campus Land Area Index）**：校园占地面积指数。
- **CFFI（Campus Football Field Index）**：校园足球场指数，反映了校园体育设施的情况。
- **NVL（the Number of Volumes in Library）**：图书册数，衡量了图书馆的藏书规模。
- **NDT（the Number of Digital Terminals）**：数字终端数，表示教育机构的数字化程度。
- **NC（the Number of Classrooms）**：教室间数，反映了教学场所的数量。
- **NNMC（the Number of Networked Multimedia Classrooms）**：网络多媒体教室数量，表示具有网络多媒体设备的教室数量。
- **TVTED（Total Value of Teaching Equipment and Devices）**：教学仪器设备总价值，反映了教学设备的质量和数量。
- **CGSAI（Capita Green Space Area Index）**：绿化用地面积指数。

### 数学模型设计

教育资源指数（ERI）可以通过建立多元线性回归模型计算得出。其中，Xi是变量i对应的数值；Coefi是变量i对应的系数（通过对数据的分析确立的合适的数值）；作为误差值在一般情况下可以忽略成0。

使用Python算法对其基础性表达如下：（不是带有图形化界面的最终程序，仅仅提供算法伪代码表示一下）

```python
# -*- coding: utf-8 -*-
# Coded by Chen Huaide on 2024/4/16

import numpy as np

# 模型的系数
coef = np.array([
    0.0001,  # GDP
    0.00005, #教育支出预算
    0.00005, #科技支出预算
    0.00001, #人均校园占地面积指数
    0.00001, #校园足球场指数
    0.00003, #图书册数
    0.00003, #数字终端数
    0.00003, #教室间数
    0.00003, #网络多媒体教室数量
    0.00003, #教学仪器设备总价值
    0.00001 #人均绿化用地面积指数
])

# 需导入具体数据列表
Group_List={GDP,EB,TB,PCCLAI,CFFI,NVL,NDT,NC,NNMC,TVTED,PCGSAI}  # ignored

# 变量代入
GDP = np.array([Group_List{GDP}])  # （亿元）
EB = np.array([Group_List{EB}])  # （万元）
TB = np.array([Group_List{TB}])  # （万元）
PCCLAI = np.array([Group_List{PCCLAI}])  # (平方米)
CFFI = np.array([Group_List{CFFI}])  # (个数)
NVL = np.array([Group_List{NVL}])  # 册数
NDT = np.array([Group_List{NDT}])  # 终端数
NC = np.array([Group_List{NC}])  # 间数 Number of Classrooms
NNMC = np.array([Group_List{NNMC}])  # 网络多媒体教室数量
TVTED = np.array([Group_List{TVTED}])  # 教学仪器设备总价值
PCGSAI = np.array([Group_List{PCGSAI}])  # 绿化用地面积指数

# 带入求解
eri_list = []
for i in range(len(GDP)):
    eri = (GDP[i] * coef[0] + EB[i] * coef[1] + TB[i] * coef[2] + PCCLAI[i] * coef[3] + CFFI[i] * coef[4] + NVL[i] * coef[5] + NDT[i] * coef[6] + NC[i] * coef[7] + NNMC[i] * coef[8] + TVTED[i] * coef[9] + PCGSAI[i] * coef[10])
    eri_list.append(round(eri,4))  # 保留4位小数

# 输出
print(f"ERI指数：", eri_list)
#©Coded by Chen Huaide on 2024/4/16
```

### 注意

在使用时需要带入具体的各省份的数据列表。

### 数据整合

1. **GDP数据**：来自中经数据 [中经数据](https://wap.ceidata.cei.cn/)。
2. **2022年各省学校资产情况**：来自国务院网站。
3. **EB、TB等数据**：来自各省年度财政报告。
4. **其他数据来源**：政府文件、国家统计局 [国家统计局](https://www.stats.gov.cn/gk/)。

通过代入上述数据，您可以计算出各省不同学段的ERI指数。
