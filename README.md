# 江歌案舆情分析报告

## 项目背景
江歌案自2016年11月3日发生以来，引发了广泛的社会关注和舆论讨论。该案件不仅涉及法律层面的审判，还引发了关于道德责任、媒体伦理以及网络舆论等诸多社会问题的探讨。

## 需求说明
本项目旨在通过大数据分析技术，对江歌案相关的舆情数据进行收集、整理与分析，以了解公众对该案件的态度和情感倾向，揭示舆论热点与趋势，并探讨媒体在报道中的表现及其对公众认知的影响。

## 研究方法
1. **数据获取**：通过爬虫技术获取社交媒体平台、新闻网站等渠道中与“江歌案”相关的文本数据；同时手动收集媒体报道、网友评论等，以保证数据的多样性。
2. **数据预处理**：对采集到的文本数据进行清洗，去除HTML标签、特殊字符、Emoji等；使用中文分词工具（如jieba）进行分词处理，并去除常见停用词。
3. **模型分析**：利用情感分析模型对文本数据进行情感倾向判断，分析公众对江歌案的正面、负面和中性情感分布；同时结合主题提取技术，挖掘舆论关注的热点主题。
4. **结果可视化**：运用Python的matplotlib、seaborn、pyecharts等库，绘制柱状图、词云图、时间序列曲线等，直观呈现分析结果。
## 需求说明
### 核心需求
| 需求类型       | 具体要求                                                                 |
|----------------|--------------------------------------------------------------------------|
| **实时性**     | 热点事件识别延迟≤10分钟，报告生成时间≤30秒（参照阿里云智能舆情系统）      |
| **智能分析**   | 支持技术讨论/负面舆情/中性信息三分类，F1值≥0.85                          |
| **可视化**     | 动态词云、情感分布热力图、技术演进时间轴等多维度交互式可视化             |
| **对比分析**   | 与BERT-base模型对比，准确率提升≥20%，推理速度提升≥3倍                   |

### 非功能需求
- **数据安全**：符合《数据安全法》要求，支持本地化部署（加密传输+数据脱敏）
- **扩展性**：支持接入抖音、B站弹幕等非结构化数据源
- **交互性**：移动端实时推送+自然语言交互查询

---

## 研究方法
### 技术架构
```mermaid
graph TD
    A[数据采集层] --> B[文本预处理]
    B --> C[多模态分析]
    C --> D[可视化层]
    D --> E[决策支持]
    
    C --> F[情感分析]
    C --> G[主题建模]
    C --> H[趋势预测]
    
    A --> I[多源数据接入]
    I --> A

```

## 数据来源
1. 社交媒体平台（如微博）上的用户评论和讨论。
2. 新闻网站和媒体平台的相关报道。
3. 手动收集的媒体报道、网友评论等。

## 实现过程
### 数据采集
通过爬虫程序获取大量与江歌案相关的文本数据，并存储为结构化格式。

### 数据预处理
对采集到的数据进行清洗和分词处理，去除无关信息和停用词。

### 情感分析与主题提取
利用情感分析模型对文本数据进行情感倾向判断，并提取舆论热点主题。

### 可视化呈现
根据分析结果，绘制柱状图、词云图等可视化图表，展示公众情感倾向和舆论热点。

## 核心代码

### 数据采集代码
```python
import requests
from bs4 import BeautifulSoup

def crawl_data(url):
    # 发起请求获取网页内容
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')
    # 提取相关文本数据
    text_data = soup.find_all('p')
    return [p.get_text() for p in text_data]
   ```
###数据预处理代码
```python
import jieba
import re

# 去除HTML标签、特殊字符、Emoji等
def text_clean(text):
    text = re.sub(r'<.*?>', '', text)  # 去除HTML标签
    text = re.sub(r'[^\u4e00-\u9fa5a-zA-Z0-9]', '', text)  # 去除特殊字符
    return text

# 中文分词
def chinese_tokenization(text):
    words = jieba.cut(text)
    return ' '.join(words)

# 去除停用词
def remove_stopwords(words, stopwords):
    return [word for word in words if word not in stopwords]
```
###情感分析代码  
```python
from some_sentiment_analysis_model import SentimentModel

# 加载情感分析模型
model = SentimentModel()

# 对文本数据进行情感分析
def analyze_sentiment(text_data):
    sentiments = model.predict(text_data)
    return sentiments

```
###主题提取代码
```python
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.cluster import KMeans

# 提取文本主题
def extract_topics(text_data, n_clusters=5):
    vectorizer = TfidfVectorizer()
    X = vectorizer.fit_transform(text_data)
    kmeans = KMeans(n_clusters=n_clusters)
    kmeans.fit(X)
```
###可视化代码
```python
import matplotlib.pyplot as plt
from wordcloud import WordCloud

# 绘制词云图
def plot_wordcloud(text_data):
    wordcloud = WordCloud(font_path='simhei.ttf').generate(' '.join(text_data))
    plt.imshow(wordcloud, interpolation='bilinear')
    plt.axis('off')
    plt.show()

    return kmeans.labels_
```
## 参考资料

- [阿里通义千问 QWQ-32B 官方文档](https://xxxx.aliyun.com)
- [LaTeX 入门文档](https://www.latex-project.org/help/)
- [Python 爬虫与 NLP 教程](https://realpython.com/)

---

通过本项目，我们展示了如何利用阿里通义千问 QWQ-32B 实现从数据采集、情感分析到自动生成高质量舆情报告的整个流程，为国内舆情监控与大数据分析提供了有效实践参考。
```
