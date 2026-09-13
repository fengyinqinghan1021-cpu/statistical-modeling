# -
统计建模 旅游景区方面
这是一个基于 Python 实现的旅游景区数据分析项目，主要包含旅游评论数据采集、中文文本预处理、LDA 主题建模以及主题可视化等代码。

项目主要针对旅游景区网络评论数据进行处理，将原始评论转换为结构化文本数据，并利用自然语言处理和机器学习方法提取评论中的潜在主题。

🌟 核心功能
🕷️ 1. 景区评论数据采集

使用 Python 浏览器自动化方式访问携程景区页面，并进入评论页面获取游客评论。

主要采集：

💬 评论内容
⭐ 评论评分

代码通过 ChromiumPage 打开指定景区页面，并循环访问评论页面进行数据采集。

核心流程：

打开景区页面
      ↓
进入评论页面
      ↓
获取评论列表
      ↓
提取评论内容
      ↓
提取评分
      ↓
写入 CSV
      ↓
进入下一页
      ↓
循环采集

代码默认循环采集多个页面，并在无法找到下一页时结束采集。

🧹 2. 中文文本预处理

对采集得到的评论数据进行清洗和中文分词。

主要处理步骤：

原始评论
   ↓
删除换行符
   ↓
删除特殊字符
   ↓
保留中文字符
   ↓
加载停用词表
   ↓
jieba 中文分词
   ↓
删除停用词
   ↓
输出处理结果

代码使用 re 对文本中的特殊字符和非中文字符进行处理，并使用 jieba 加载自定义词典进行中文分词。

处理后的数据保存为：

news_content_processed.xlsx
🧠 3. LDA 主题模型

使用 sklearn 中的 LatentDirichletAllocation 对旅游评论进行主题建模。

主要代码流程：

处理后的评论
      ↓
CountVectorizer
      ↓
构建词频矩阵
      ↓
LDA 模型
      ↓
提取主题词
      ↓
确定评论主题
      ↓
导出结果

代码设置：

最大特征词数量：500
主题数量：4
最大迭代次数：50
学习方式：batch
random_state：0

具体实现使用 CountVectorizer 将文本转换为词频矩阵，再通过 LatentDirichletAllocation 训练主题模型。

🔎 4. 主题关键词提取

模型训练完成后，对每一个主题中的词语按照权重进行排序，提取每个主题中权重最高的关键词。

代码默认：

每个主题提取 10 个关键词

并输出：

Topic #0
Topic #1
Topic #2
Topic #3

对应的主题关键词。

📋 5. 评论主题分类

通过：

lda.transform(tf)

计算每条评论属于不同主题的概率。

随后选择概率最大的主题作为该评论的主要主题，并将结果写入：

topic

字段。

最终将结果保存到：

data_topic.xlsx




📊 6. LDA 主题可视化

项目使用 pyLDAvis 对训练完成的 LDA 模型进行可视化。

输出：

topic.html

可以通过浏览器打开 HTML 文件查看 LDA 主题分布及主题关键词关系。

📈 7. 主题数量选择

代码通过改变 LDA 的主题数量，对不同主题数量下的模型进行训练，并计算：

Perplexity（困惑度）
Score（似然分数）

主题数量范围：

1 ~ 15

随后使用 matplotlib 绘制主题数量与模型指标之间的关系曲线，用于辅助确定合适的主题数量。

🛠️ 技术栈
数据处理
Python
Pandas
NumPy
文本处理
Jieba
正则表达式 re
停用词过滤
自定义词典
机器学习
Scikit-learn
CountVectorizer
Latent Dirichlet Allocation
数据可视化
Matplotlib
PyLDAvis
数据采集
ChromiumPage
浏览器自动化
📦 安装依赖

建议使用 Python 3.x 环境。

安装项目主要依赖：

pip install pandas
pip install numpy
pip install jieba
pip install scikit-learn
pip install matplotlib
pip install pyLDAvis

如果运行评论采集代码，还需要安装代码所使用的浏览器自动化相关环境。

📁 代码结构

推荐 GitHub 仓库按照下面的方式整理：

tourism-data-analysis/
│
├── README.md
│
├── crawler/
│   └── ctrip_crawler.py
│
├── lda/
│   └── lda_model.py
│
├── data/
│   ├── 汇总评论.xlsx
│   ├── user_dict.txt
│   └── 哈工大停用词表.txt
│
└── output/
    ├── news_content_processed.xlsx
    ├── data_topic.xlsx
    └── topic.html
🚀 使用方法
1. 准备评论数据

将评论数据整理为 Excel 文件：

汇总评论.xlsx

代码通过 Pandas 读取 Excel：

df = pd.read_excel(file_path)

并对其中的评论内容进行处理。

2. 准备自定义词典

将自定义词典放置在代码指定的位置：

user_dict.txt

程序运行时会通过：

jieba.load_userdict(user_dict_path)

加载自定义词典。

3. 准备停用词表

代码使用：

哈工大停用词表.txt

读取停用词，并在中文分词后过滤停用词。

4. 运行 LDA

运行 LDA Python 文件：

python lda_model.py

程序依次完成：

Excel 数据读取
      ↓
文本清洗
      ↓
中文分词
      ↓
停用词过滤
      ↓
词频矩阵构建
      ↓
LDA 模型训练
      ↓
主题关键词提取
      ↓
评论主题分类
      ↓
Excel 结果输出
      ↓
LDA HTML 可视化
📤 输出文件
news_content_processed.xlsx

保存经过：

文本清洗
中文分词
停用词过滤

后的评论数据。

data_topic.xlsx

保存 LDA 模型计算后的评论主题分类结果。

topic.html

保存 PyLDAvis 生成的 LDA 主题交互式可视化结果。

⚠️ 注意事项

输入文件路径

LDA 代码中的 Excel、停用词表和自定义词典均通过文件路径读取，运行前需要确认文件位置与代码中的路径一致。

中文编码

停用词表使用：

encoding='utf-8'

因此文本文件应保证使用 UTF-8 编码。

LDA 主题数量

当前代码默认设置：

n_topics = 4

如需重新进行主题数量分析，可以运行困惑度和 Score 计算部分的代码。

爬虫页面结构

携程页面的 CSS/XPath 选择器如果发生变化，需要根据当前网页结构修改对应选择器。

数据采集

评论采集代码属于浏览器自动化采集程序，实际使用时请合理控制访问频率，并遵守目标网站的相关规则。

📌 当前代码实现
✅ 携程景区评论采集
✅ 评论内容与评分提取
✅ Excel 数据读取
✅ 文本清洗
✅ 中文分词
✅ 停用词过滤
✅ CountVectorizer 词频向量化
✅ LDA 主题建模
✅ 主题关键词提取
✅ 评论主题分类
✅ LDA 主题可视化
✅ 困惑度计算
✅ Score 计算
✅ Matplotlib 曲线绘制
📜 License

本项目仅用于学习、数据分析和统计建模相关实践。

使用或修改本项目代码时，请遵守相关数据平台的使用规则及适用法律法规。
