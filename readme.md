
###  概述

本项目对上海海洋大学（SHOU）202 份「大学生食堂消费模式调查问卷」进行完整的数据处理与统计分析。采用 **模块化 Python 架构**（6 个 py 文件），从原始 Excel 问卷数据出发，经过 10 步清洗流水线后，生成 8 张可视化图表并完成 3 项统计假设检验，最终输出一份结构化 Markdown 分析报告。

###  架构设计

```
config.py          ← 全局配置、路径、全部映射字典
data_reader.py     ← 读取 Excel 原始数据
data_cleaner.py    ← 10步清洗流水线（去元数据/重命名/前缀剥离/文本标准化/代码映射/区间转数值/李克特编码/多选题展开/IQR检测）
visualizer.py      ← 8张 matplotlib 图表生成
statistics.py      ← t检验 + ANOVA + Tukey HSD 事后比较
main.py            ← 编排入口
```

###  产出物（位于 `output/`）

| 文件 | 说明 |
|------|------|
| `cleaned_survey.xlsx` | 清洗后数据（202行 × 54列） |
| `fig1_consumption_hist.png` | 消费金额直方图 + KDE |
| `fig2_boxplot_gender.png` | 性别分组箱线图 |
| `fig3_boxplot_grade.png` | 年级分组箱线图 |
| `fig4_boxplot_region.png` | 生源地区域分组箱线图 |
| `fig5_meal_period_bar.png` | 就餐时段偏好柱状图 |
| `fig6_dish_type_pie.png` | 菜品类型饼图 |
| `fig7_living_expense_bar.png` | 月生活费柱状图 |
| `fig8_likert_bar.png` | 李克特满意度均值±SE图 |
| `statistics_results.txt` | 统计检验完整结果 |

### 🔬 统计检验结论（α=0.05）

| 检验 | 统计量 | p值 | 结论 |
|------|--------|-----|------|
| t检验（性别） | t = -2.464 | **0.015** |  显著 — 女生(14.48元) > 男生(12.85元) |
| 方差分析（年级） | F = 0.576 | 0.631 |  不显著 |
| 方差分析（区域） | F = 0.509 | 0.677 |  不显著 |

###  报告

分析报告见 [`报告_大学生食堂消费模式调查统计分析.md`](报告_大学生食堂消费模式调查统计分析.md)，涵盖研究问题概述、调查设计、数据整理、描述性统计、统计模型分析及对策建议七个章节。

---

### 使用方法
1. 先安装依赖
<br>

  `pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple`
2. 运行 main.py 出图像
<br>

  `python main.py`
3. 运行 _extract_stats.py 出数据报告

<br>

  `python _extract_stats.py`


