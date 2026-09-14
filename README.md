# AngleDrop 历史版本

接触角（Contact Angle）自动测量工具 AngleDrop 的版本存档。这里按时间顺序保留了各历史版本，最新版本在 [8cheh/AngleDrop](https://github.com/8cheh/AngleDrop)。

## 项目简介

AngleDrop（Angle from Pictures）从单张液滴图像出发，定位液滴、检测固-液界面（基线）、提取轮廓，再用几何或物理模型算出接触角。

项目分两条技术路线演进：

- CUPET：自研算法集，圆拟合 → 多项式切线 → Young–Laplace 拟合
- CSIEC：参照 [OpenDrop](https://github.com/jdber1/opendrop) 的算法思想，Y–L 全局拟合 + 局部多项式

## 目录结构

```
AngleDrop_Old/
├── v0(not usable)/                    早期理论 + AI 生成代码（弃用）
│   ├── v0. Theory/                    理论探索
│   └── v0. AI-generated Programs(Wasted)/   AI 生成程序（已弃用）
├── v1.0 Round(matlab)/                MATLAB 手动三点定圆（球冠近似）
├── v1.3.alpha Enhancer/               图像增强探索
├── v1.7.alpha using SAM/              SAM 分割 + 双参数 Young–Laplace
├── v2.2 Two contact points/           手动双接触点 + 多项式切线
├── v3.7 Angle-AssistantAP/            Flask 网页版（单参数 Y–L）
├── v4.4.alpha ALL in one/             全自动一体化管线
├── index_v4.4.html                    浏览器端 OpenCV.js 原型
├── Summer Vacation ver2.9/            CSIEC：Y–L 全局拟合 + 局部多项式
└── Summer Vacation ver,alpha 3.5 Data/   数据集（176 张液滴图）
```

## 版本演进

### CUPET

| 版本 | 目录 | 算法要点 |
|---|---|---|
| v0 | `v0(not usable)` | 早期理论与 AI 生成代码（弃用）|
| v1.0 | `v1.0 Round(matlab)` | MATLAB 手动三点定圆（球冠近似）|
| v1.3 | `v1.3.alpha Enhancer` | 图像增强探索 |
| v1.7 | `v1.7.alpha using SAM` | SAM 分割 + 双参数 Young–Laplace |
| v2.2 | `v2.2 Two contact points` | 手动双接触点 + 多项式切线 |
| v3.7 | `v3.7 Angle-AssistantAP` | Flask 网页版，单参数 Y–L |
| v4.4 | `v4.4.alpha ALL in one` | 全自动管线，Y–L + 圆 + 多项式三重校验 |

底层是三种算法：

1. 圆拟合法（球冠近似）。液滴近似为理想球冠（重力可忽略，Bo ≪ 1），对轮廓做最小二乘圆拟合，由圆心和半径求接触角。
2. 多项式切线法。只在接触点附近的局部窗口内用多项式拟合轮廓，取接触点处的一阶导作为切线。
3. Young–Laplace 拟合法（ADSA）。数值积分轴对称 Young–Laplace ODE，把形状参数拟合到实测轮廓，读取接触线处的切线角。

### CSIEC

| 版本 | 目录 | 算法要点 |
|---|---|---|
| v2.9 | `Summer Vacation ver2.9` | Y–L 全局拟合 + 局部多项式，双方法并行 |

### 数据集

`Summer Vacation ver,alpha 3.5 Data/` 下有 176 张液滴图（`pictures/` 目录，`drop_image_1.jpg` 到 `drop_image_176.jpg`），用来测各版本算法。

`result/` 目录里是 OpenDrop 自己的输出，不能当接触角真值——OpenDrop 在这批图上大多失败。

## 背景：接触角

接触角 θ 是固-液-气三相接触线上，液滴界面切线与固体表面之间的夹角，用来衡量材料表面润湿性：

- θ < 90°：亲水
- θ > 90°：疏水
- θ ≳ 150°：超疏水

## 许可与联系

历史版本存档，仅供教学使用。如欲使用代码，请先联系 huangbache@outlook.com。
