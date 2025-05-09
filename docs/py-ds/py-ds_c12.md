## 第十二章：数据分析中的机器学习

![](img/chapterart.png)

*机器学习*是一种数据分析方法，应用程序利用现有数据发现模式并做出决策，而无需显式编程。换句话说，应用程序能够自主学习，无需人工干预。作为一种强大的数据分析技术，机器学习在许多领域得到应用，包括但不限于分类、聚类、预测分析、学习关联、异常检测、图像分析和自然语言处理。

本章概述了一些基本的机器学习概念，然后深入探讨了两个机器学习实例。首先，我们将进行情感分析，开发一个模型来预测与产品评论相关的星级评分（从一到五颗星）。之后，我们将开发另一个模型来预测股票价格的变化。

## 为什么选择机器学习？

机器学习让计算机能够完成一些使用传统编程技术很难甚至不可能完成的任务。例如，假设你需要构建一个图像处理应用程序，能够根据提交的照片区分不同种类的动物。在这个假设的场景中，你已经有了一个代码库，可以识别图像中物体（比如动物）的边缘。通过这种方式，你可以将照片中的动物转换为一组特征性的线条。但是，如何才能程序化地区分两种不同动物的线条——比如一只猫和一只狗呢？

传统的编程方法是手动编写规则，将每一种特征线条组合映射到一个动物上。不幸的是，这个方法需要大量的代码，并且在提交一张新照片时，如果该照片的边缘不符合任何手动定义的规则，系统可能完全失效。相比之下，基于机器学习算法的应用程序并不依赖预定义的逻辑，而是依靠应用程序从之前见过的数据中自动学习。因此，基于机器学习的照片标记应用程序会寻找从之前照片中提取的线条组合中的模式，然后根据概率统计对新照片中的动物进行预测。

## 机器学习的类型

数据科学家区分了几种不同类型的机器学习。其中最常见的是监督学习和无监督学习。在本章中，我们主要关注监督学习，但本节将简要概述这两种类型。

### 监督学习

*有监督学习*使用标记数据集（称为*训练集*）来教会模型在给定新的、先前未见过的数据时，产生期望的输出。从技术上讲，有监督学习是一种推断函数的技术，该函数基于训练集将输入映射到输出。您在第三章中已经看到了一个有监督学习的例子，我们使用一组示例产品评论训练模型，预测新的产品评论是正面还是负面。

有监督学习算法的输入数据可以表示现实世界对象或事件的特征。例如，您可能会使用待售房屋的特征（如面积、卧室和浴室的数量等）作为预测房价的算法的输入。这些房价将是算法的输出。您会用一组输入-输出对来训练该算法，这些输入-输出对由不同房屋的特征及其相关房价组成，然后将新房屋的特征输入给它，并将这些新房屋的估计房价作为输出。

其他有监督学习算法设计用来处理的不是特征，而是*观察数据*：通过观察某种活动或行为收集的数据。例如，考虑一个由监控机场噪音水平的传感器生成的时间序列。这些观察到的噪音水平数据可能会提交给一个机器学习算法，同时提供诸如时间和星期几等信息，以便算法能够学习预测未来几个小时的噪音水平。在这个例子中，时间和星期几是输入，噪音水平是输出。换句话说，该算法将被设计用来预测未来的观察数据。

房价预测和噪音水平预测都是*回归*的例子，回归是一种常见的有监督学习技术，用于预测连续值。另一种常见的有监督学习技术是*分类*，它使模型为每个输入分配有限个类别标签中的一个。区分有利和不利的产品评论就是分类的一个例子，其他*情感分析*应用也是如此，其中文本片段被识别为正面或负面。我们将在本章后面探讨一个情感分析的例子。

### 无监督学习

*无监督学习*是一种机器学习技术，其中没有训练阶段。您只需提供输入数据，而没有任何相应的输出值供其学习。从这个意义上讲，无监督机器学习模型必须独立工作，发现输入数据中的隐藏模式。

非监督学习的一个很好的例子是*关联分析*，在这种学习方式中，机器学习应用会识别数据集中彼此之间有亲和力的项目。在第十一章中，你对一组交易数据进行了关联分析，识别出了经常一起购买的商品。你使用了 Apriori 算法，该算法不需要示例输出数据进行学习；它将所有交易数据作为输入，搜索交易中的频繁项集，从而实现无监督学习。

## 机器学习如何工作

一个典型的机器学习流程依赖于三个主要组件：

+   学习数据

+   应用于数据的统计模型

+   需要处理的新数据

以下部分将更详细地介绍这些组件。

### 学习数据

机器学习基于计算机系统能够学习的理念，因此任何机器学习算法都需要数据来进行学习。正如我们之前讨论的那样，这些数据的性质取决于机器学习模型是监督学习还是非监督学习。在监督学习中，学习的数据以输入-输出对的形式出现，这样可以训练模型根据新的输入预测输出。而在非监督学习中，模型只接收输入数据，通过挖掘其中的模式来生成输出。

虽然所有机器学习应用都需要数据来进行学习，但这些数据的格式可能因算法而异。许多算法从组织成表格的数据集进行学习，其中行代表不同的实例，比如可能是单个对象或特定时间点，而列则代表与这些实例相关的属性。一个经典的例子是鸢尾花数据集（[`archive.ics.uci.edu/ml/datasets/Iris`](https://archive.ics.uci.edu/ml/datasets/Iris)）。它有 150 行，每一行包含关于不同鸢尾花标本的观察数据。以下是该数据集的前四行：

```py
sepal length   sepal width   petal length   petal width   species
5.1            3.5           1.4            0.2           Iris-setosa
4.9            3.0           1.4            0.2           Iris-setosa
4.7            3.2           1.3            0.2           Iris-setosa
4.6            3.1           1.5            0.2           Iris-setosa
```

前四列代表不同的属性或特征，描述的是标本的不同特征。第五列包含每个实例的标签：鸢尾花的具体物种名称。如果你用这个数据集训练一个分类模型，你将把前四列的值作为自变量或输入，而第五列则作为因变量或输出。通过从这些数据中学习，理想情况下，模型能够根据物种分类新的鸢尾花标本。

其他机器学习算法则从非表格数据中学习。例如，我们在上一章中讨论过的用于关联分析的 Apriori 算法，它将不同大小的交易（或购物篮）作为输入数据。下面是一个简单的交易集示例：

```py
(butter, cheese)
(cheese, pasta, bread, milk)
(milk, cheese, eggs, bread, butter)
(bread, cheese, butter)
```

除了机器学习数据如何结构化的问题外，所使用的数据类型也因算法而异。正如前面的例子所示，一些机器学习算法处理的是数值或文本数据。也有一些算法是专门设计来处理照片、视频或音频数据的。

### 统计模型

无论机器学习算法需要什么样的数据格式，输入数据必须以某种方式进行转换，以便能够分析并生成输出。这时*统计模型*就派上用场了：统计数据被用来创建数据的表示形式，这样算法就能识别变量之间的关系、发现洞察、对新数据进行预测、生成推荐等等。统计模型是任何机器学习算法的核心。

例如，Apriori 算法使用支持度度量作为统计模型来寻找频繁项集。（如第十一章所讨论，支持度是包含某个项集的交易的百分比。）具体来说，算法识别所有可能的项集并计算相应的支持度度量，然后仅选择支持度足够高的项集。以下是一个简单的示例，说明算法背后的工作原理：

```py
Itemset         Support
--------------  -------
butter, cheese  0.75
bread, cheese   0.75
milk, bread     0.50
bread, butter   0.50
```

这个例子只展示了两项集合。实际上，在计算每个可能的两项集合的支持度之后，Apriori 算法会继续分析每个三项集合、四项集合，依此类推。然后，算法使用所有大小项集的支持度值来生成频繁项集的列表。

### 之前未见过的数据

在监督学习中，一旦你在示例数据上训练好模型，就可以将其应用于新的、之前未见过的数据。然而，在这样做之前，你可能需要评估模型，这就是为什么通常做法是将初始数据集拆分为训练集和测试集。前者是模型学习的数据，后者则是用于测试目的的之前未见过的数据。

测试数据仍然包含输入和输出，但模型只看到输入数据。然后，将实际输出与模型预测的输出进行比较，以评估其预测的准确性。一旦确保模型的准确性达到可接受的水平，你就可以使用新的输入数据进行预测分析。

在无监督学习的情况下，数据没有区分“用于学习的数据”和“之前未见过的数据”。所有数据本质上都是之前未见过的，模型通过分析其潜在特征来尝试从中学习。

## 情感分析示例：对产品评论进行分类

现在我们已经复习了机器学习的基础知识，您可以进行样本情感分析了。如前所述，这种自然语言处理技术允许您以编程方式确定一篇文章是积极的还是消极的。 （在某些应用中，还有更多类别，如中立、非常积极或非常消极。）实质上，情感分析是一种分类形式，是一种监督的机器学习技术，将数据排序为离散类别。

在第三章中，您使用 scikit-learn 对来自亚马逊的一组产品评论执行了基本的情感分析。您训练了一个模型来识别评论是好是坏。在本节中，您将扩展该章节中的工作。您将直接从亚马逊获取一组实际的产品评论，并用它来训练分类模型。该模型的目标是预测评论的星级评分，即一到五级。因此，模型将评论排序为五种可能的类别，而不仅仅是两种。

### 获取产品评论

在构建模型的第一步是从亚马逊下载一组实际的产品评论。一个简单的方法是使用亚马逊评论导出器，这是一个 Google Chrome 浏览器扩展程序，可以将亚马逊产品的评论下载为 CSV 文件。您可以从这个页面用一键安装这个扩展程序到您的 Chrome 浏览器：[`chrome.google.com/webstore/detail/amazon-reviews-exporter-c/njlppnciolcibljfdobcefcngiampidm`](https://chrome.google.com/webstore/detail/amazon-reviews-exporter-c/njlppnciolcibljfdobcefcngiampidm)。

安装了该扩展程序后，在 Chrome 中打开亚马逊产品页面。在这个示例中，我们将使用 No Starch Press 的 *Python Crash Course* 由 Eric Matthes 的亚马逊页面 (https://www.amazon.com/Python-Crash-Course-2nd-Edition/dp/1593279280)，目前有 445 条评论。要下载这本书的评论，请找到并点击 Chrome 工具栏中的亚马逊评论导出器按钮。

一旦您将评论保存为 CSV 文件，您可以按以下方式将其读入 pandas DataFrame 中：

```py
import pandas as pd
df = pd.read_csv('reviews.csv')
```

在继续之前，您可能想查看评论的总数以及 DataFrame 中加载的前几条评论：

```py
print('The number of reviews: ', len(df))
print(df[['title', 'rating']].head(10))
```

输出应该看起来像这样：

```py
The number of reviews:  445
                                               title  rating
0  Great inner content! Not that great outer qual...       4
1                                Very enjoyable read       5
2                                The updated preface       5
3  Good for beginner but does not go too far or deep       4
4                                 Worth Every Penny!       5
5                                 Easy to understand       5
6                             Great book for python.       5
7                   Not bad, but some disappointment       4
8  Truely for the person that doesn't know how to...       3
9        Easy to Follow, Good Intro for Self Learner       5
```

这个视图仅显示每条记录的`title`和`rating`字段。我们将评论标题视为模型中的独立变量（即输入），评分作为依赖变量（输出）。请注意，我们忽略了每条评论的完整文本，仅关注标题。对于训练情感分类模型来说，这似乎是合理的，因为标题通常代表评论者对产品感受的总结。相比之下，完整的评论文本通常包含其他非情感信息，例如书籍内容的描述。

### 清洗数据

在你处理真实世界数据之前，几乎总是需要进行数据清洗。在这个具体的例子中，你需要过滤掉不是用英语写的评论。为此，你需要一种方法来编程地确定每个评论的语言。有几个具有语言检测功能的 Python 库；我们将使用 google_trans_new。

#### 安装 google_trans_new

使用`pip`安装 google_trans_new 库，如下所示：

```py
$ **pip install google_trans_new**
```

在继续之前，确保 google_trans_new 已修复已知的 bug，该 bug 会在语言检测过程中抛出`JSONDecodeError`异常。为此，请在 Python 会话中运行以下测试：

```py
$ **from google_trans_new import google_translator**
$ **detector = google_translator()**
$ **detector.detect('Good')**
```

如果这个测试没有报错，你可以继续进行。如果它抛出了`JSONDecodeError`异常，你需要对库的源代码中的*google_trans_new.py*做一些小修改。用`pip`定位该文件：

```py
$ **pip show google_trans_new**
```

该命令将显示有关库的一些基本信息，包括其源代码在你本地机器上的位置。前往该位置，用文本编辑器打开*google_trans_new.py*。然后找到第 151 行和第 233 行，它们看起来像这样：

```py
response = (decoded_line + ']')
```

然后将它们更改为：

```py
response = decoded_line
```

保存更改，重新启动你的 Python 会话，然后重新运行测试。现在它应该能够正确识别*good*为英语单词：

```py
$ **from google_trans_new import google_translator**
$ **detector = google_translator()**
$ **detector.detect('Good')**
['en', 'english']
```

#### 移除非英语评论

现在，你已经准备好检测每个评论的语言并过滤掉不是用英语写的评论。在以下代码中，你使用 google_trans_new 中的`google_translator`模块来确定每个评论标题的语言，并将语言存储在 DataFrame 的新列中。检测大量样本的语言可能需要一些时间，所以在运行代码时要耐心：

```py
from google_trans_new import google_translator
detector = google_translator()
df['lang'] = df['title'].apply(lambda x: detector.detect(x)[0])
```

你首先创建一个`google_translator`对象，然后使用 lambda 表达式将对象的`detect()`方法应用于每个评论标题。你将结果保存到名为`lang`的新列中。在这里，你打印该列，以及`title`和`rating`：

```py
print(df[['title', 'rating', 'lang']])
```

输出将类似于以下内容：

```py
 title  rating   lang
0    Great inner content! Not that great outer qual...       4     en
1                                  Very enjoyable read       5     en
2                                  The updated preface       5     en
3    Good for beginner but does not go too far or deep       4     en
4                                   Worth Every Penny!       5     en
`--snip--`
440                                            Not bad       1     en
441                                               Good       5     en
442                                              Super       5     en
443                           内容はとても良い、作りは×      4     ja
444                                           非常实用       5  zh-CN
```

你的下一步是过滤数据集，仅保留用英语写的评论：

```py
df = df[df['lang'] == 'en']
```

该操作应减少数据集中的总行数。为了验证它是否有效，请计算更新后的 DataFrame 中的行数：

```py
print(len(df))
```

行数应该比原来少，因为所有非英语评论已经被移除。

### 拆分和转换数据

在继续之前，你需要将评论分为用于训练模型的训练集和用于评估准确性的测试集。你还需要将评论标题的自然语言转换为模型可以理解的数字数据。正如你在第三章的“将文本转换为数字特征向量”中所看到的，词袋（BoW）技术可以用于此目的；要回顾其工作原理，请参考该章节。

以下代码使用 scikit-learn 进行数据的拆分和转换。代码遵循第三章中使用的相同格式：

```py
from sklearn.model_selection import train_test_split
from sklearn.feature_extraction.text import CountVectorizer
reviews = df['title'].values
ratings = df['rating'].values
❶ reviews_train, reviews_test, y_train, y_test = train_test_split(reviews,
                ratings, test_size=0.2, random_state=1000)
vectorizer = CountVectorizer()
vectorizer.fit(reviews_train)
❷ x_train = vectorizer.transform(reviews_train)
x_test = vectorizer.transform(reviews_test)
```

总结一下，scikit-learn 的`train_test_split()`函数将数据随机拆分为训练集和测试集❶，该库的`CountVectorizer`类有方法将文本数据转换为数值特征向量❷。代码生成以下结构，将训练集和测试集实现为 NumPy 数组，并将其相应的特征向量实现为 SciPy 稀疏矩阵：

1.  `reviews_train` 一个包含用于训练的评论标题的数组

1.  `reviews_test` 一个包含用于测试的评论标题的数组

1.  `y_train` 一个包含与`reviews_train`中的评论对应的星级评分的数组

1.  `y_test` 一个包含与`reviews_test`中的评论对应的星级评分的数组

1.  `x_train` 一个包含`reviews_train`数组中评论标题对应的特征向量的矩阵

1.  `x_test` 一个包含`reviews_test`数组中评论标题对应的特征向量的矩阵

我们最关心的是`x_train`和`x_test`，这些是 scikit-learn 从评论标题使用 BoW 技术生成的数值特征向量。这些矩阵中的每一行都代表一个评论标题的数值特征向量。要检查由`reviews_train`数组生成的矩阵的行数，可以使用：

```py
print(len(x_train.toarray()))
```

结果数字应该是英语评论总数的 80%，因为你按 80/20 的模式将数据分为训练集和测试集。`x_test`矩阵应该包含其余 20%的特征向量，你可以通过以下方式验证：

```py
print(len(x_test.toarray()))
```

你可能还想检查训练矩阵中特征向量的长度：

```py
print(len(x_train.toarray()[0]))
```

你打印的是矩阵中第一行的长度，但每一行的长度是相同的。结果可能如下所示：

```py
442
```

这意味着训练集中的评论标题中出现了 442 个独特的词汇。这个词汇集合被称为数据集的*词汇字典*。

如果你感兴趣的话，下面是如何打印整个矩阵：

```py
print(x_train.toarray())
```

结果大概会是这样：

```py
[[0 0 0 ... 1 0 0]
 [0 0 0 ... 0 0 0]
 [0 0 0 ... 0 0 0]
 `--snip--`
 [0 0 0 ... 0 0 0]
 [0 0 0 ... 0 0 0]
 [0 0 0 ... 0 0 0]]
```

矩阵的每一列对应数据集词汇字典中的一个词，数字表示该词在任何给定评论标题中出现的次数。如你所见，矩阵大多数情况下是零。这是预期的：示例集中平均的评论标题只有 5 到 10 个词，但整个数据集的词汇字典包含 442 个词，意味着在一个典型的行中，只有 5 到 10 个元素会被设置为 1 或更高。不过，这种示例数据的表示方式正是你训练情感分析分类模型所需要的。

### 训练模型

现在你已经准备好训练模型了。特别地，你需要训练一个*分类器*，这是一种将数据分到不同类别的机器学习模型，以便它能预测评论的星级。为此，你可以使用 scikit-learn 的`LogisticRegression`分类器：

```py
from sklearn.linear_model import LogisticRegression
classifier = LogisticRegression()
classifier.fit(x_train, y_train)
```

你导入`LogisticRegression`类并创建一个`classifier`对象。然后，通过传递`x_train`矩阵（训练集中的评论标题的特征向量）和`y_train`数组（相应的星级评分）来训练分类器。

### 评估模型

现在，模型已经训练完成，你可以使用`x_test`矩阵来评估它的准确性，将模型的预测评分与`y_test`数组中的实际评分进行比较。在第三章中，你使用了`classifier`对象的`score()`方法来评估其准确性。这里你将使用另一种评估方法，这种方法允许更精确的分析：

```py
import numpy as np
❶ predicted = classifier.predict(x_test)
accuracy = ❷ np.mean(❸ predicted == y_test)
print("Accuracy:", round(accuracy,2))
```

你使用分类器的`predict()`方法根据`x_test`特征向量❶来预测评分。然后，你测试模型的预测值与实际星级评分之间的等价性❸。这种比较的结果是一个布尔数组，其中`True`和`False`表示准确和不准确的预测。通过对数组❷取算术平均，你可以得到模型的总体准确率。（在计算均值时，每个`True`视为`1`，每个`False`视为`0`。）打印结果应该类似于：

```py
Accuracy: 0.68
```

这表示模型的准确率为 68%，意味着平均每 10 次预测中大约有 7 次是正确的。然而，为了更细致地了解模型的准确性，你需要使用其他 scikit-learn 功能来检查更具体的指标。例如，你可以研究模型的*混淆矩阵*，这是一张将预测分类与实际分类进行比较的网格。混淆矩阵有助于揭示模型在每个单独类别中的准确性，还能显示模型是否容易将两个类别混淆（即将一个类别错误标记为另一个类别）。你可以通过以下方式为你的分类模型创建混淆矩阵：

```py
from sklearn import metrics
print(metrics.confusion_matrix(y_test, predicted, labels = [1,2,3,4,5]))
```

你导入 scikit-learn 的`metrics`模块，然后使用`confusion_matrix()`方法生成矩阵。你将测试集的实际评分（`y_test`）、模型预测的评分（`predicted`）和对应的标签传递给该方法。矩阵大致如下所示：

```py
[[ 0,  0,  0,  1,  7],
 [ 0,  0,  1,  0,  1],
 [ 0,  0,  0,  4,  3],
 [ 0,  0,  0,  1,  6],
 [ 0,  0,  0,  3, 54]]
```

这里，行对应实际的评分，列对应预测的评分。例如，查看第一行中的数字可以告诉你，测试集包含八个实际的 1 星评分，其中一个被预测为 4 星，七个被预测为 5 星。

混淆矩阵的主对角线（从左上到右下）显示了每个评分级别的正确预测数量。通过检查这条对角线，你可以看到模型为五星级评论做出了 54 个正确预测，而为四星级评论做出了 1 个正确预测。没有正确识别出一星、二星或三星级评论。总体而言，在 81 条测试集评论中，模型正确预测了 55 条。

这个结果引发了几个问题。例如，为什么模型仅对五星级评论表现良好？问题可能出在示例数据集中，只有五星级评论的数量足够。为了验证这一点，你可以统计每个评分组中的行数：

```py
print(df.groupby('rating').size())
```

你通过`rating`列对包含训练和测试数据的原始 DataFrame 进行分组，并使用`size()`方法获取每个组中的条目数。输出结果可能如下所示：

```py
rating
1     25
2     15
3     23
4     51
5    290
```

如你所见，这个统计结果验证了我们的假设：五星级评价远多于其他评分，这表明模型没有足够的数据有效地学习到四星级或更低星级评论的特征。

为了进一步探索模型的准确性，你可能还想查看其主要的分类指标，比较`y_test`和`predicted`数组。你可以借助 scikit-learn 的`metrics`模块中的`classification_report()`函数来实现：

```py
print(metrics.classification_report(y_test, predicted, labels = [1,2,3,4,5]))
```

生成的报告大致如下所示：

```py
 precision    recall  f1-score   support

           1       0.00      0.00      0.00         8
           2       0.00      0.00      0.00         2
           3       0.00      0.00      0.00         7
           4       0.11      0.14      0.12         7
           5       0.76      0.95      0.84        57

    accuracy                           0.68        81
   macro avg       0.17      0.22      0.19        81
weighted avg       0.54      0.68      0.60        81
```

该报告显示了每个评论类别的主要分类指标总结。在这里，我们将重点关注支持度和召回率；关于报告中其他指标的更多信息，请参见[`scikit-learn.org/stable/modules/generated/sklearn.metrics.classification_report.html#sklearn.metrics.classification_report`](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.classification_report.html#sklearn.metrics.classification_report)。

支持度指标显示了每个评分类别的评论数量。特别地，它揭示了评论在评分组之间分布极为不均，测试集表现出与整个数据集相同的趋势。在总共 81 条评论中，有 57 条五星级评论，只有 2 条二星级评论。

召回率显示了正确预测的评论数量与某个评分级别的所有评论数量的比率。例如，五星级评论的召回率为 0.95，意味着模型预测五星级评论的准确率为 95％，而四星级评论的召回率仅为 0.14。由于其他评分的评论没有任何正确预测，因此整个测试集的加权平均召回率为 0.68，这也是你在本节开始时得到的准确率。

考虑到所有这些因素，你可以合理地得出结论，问题在于你使用的示例集在每个评分组中的评论数量极度不均衡。

## 预测股票趋势

为了进一步探索机器学习如何应用于数据分析，接下来我们将创建一个用于预测股市趋势的模型。为了简化起见，我们将创建另一个分类模型：该模型预测明天股票的价格是上涨、下跌还是保持不变。一个更复杂的模型可能会使用回归分析来预测股票的实际价格变化。

与本章的情感分析示例相比，我们的股票预测模型（实际上，许多涉及非文本数据的模型）提出了一个新问题：我们如何决定使用哪些数据作为模型的特征或输入？在情感分析模型中，你使用了通过 BoW 技术从评论标题文本中生成的特征向量。这种向量的内容牢牢依赖于相应文本的内容。从这个意义上讲，向量的内容是预定义的，是根据某种规则从相应文本中提取的特征形成的。

相比之下，当你的模型涉及非文本数据（如股票价格）时，通常由你来决定，甚至可能需要计算，作为模型输入数据的特征集合。与前一天相比的价格百分比变化、过去一周的平均价格、前两天的总交易量？可能会是。与两天前相比的价格百分比变化、过去一个月的平均价格、昨天以来的交易量变化？也有可能。金融分析师使用各种这样的指标，并通过不同的组合，作为股票预测模型的输入数据。

在第十章中，你学会了如何通过计算股市数据的百分比变化、滚动窗口平均值等来得出指标。在本节中，我们将回顾这些技术，生成用于预测模型的特征。但首先，我们需要获取一些数据。

### 获取数据

为了训练你的模型，你需要获取一年的个股数据。为了这个示例，我们将使用苹果公司（AAPL）。在这里，你将使用 yfinance 库来获取该公司过去一年的股市数据：

```py
import yfinance as yf
tkr = yf.Ticker('AAPL')
hist = tkr.history(period="1y")
```

你将使用生成的`hist` DataFrame 来推导关于股票的指标，例如日常价格变动百分比，并将这些指标输入到模型中。然而，你可以合理假设，也有一些外部因素（即不能从股票数据本身推导出的信息）影响着苹果股票的价格。例如，整体股市表现可能会影响个别股票的表现。因此，将更广泛的股市指数数据作为模型的一部分来考虑，可能会更有趣。

最著名的股市指数之一是标准普尔 500 指数。它衡量 500 家大型公司的股票表现。正如你在第四章中看到的，你可以通过 pandas-datareader 库在 Python 中获取标准普尔 500 指数的数据。在这里，你使用该库的 `get_data_stooq()` 方法从 Stooq 网站获取一年的标准普尔 500 数据：

```py
import pandas_datareader.data as pdr
from datetime import date, timedelta
end = date.today()
❶ start = end - timedelta(days=365)
❷ index_data = pdr.get_data_stooq('^SPX', start, end)
```

使用 Python 的 `datetime` 模块，你定义相对于当前日期的查询开始和结束日期 ❶。然后你调用 `get_data_stooq()` 方法，使用 `'^SPX'` 请求标准普尔 500 指数数据，并将结果存储在 `index_data` DataFrame 中 ❷。

现在，你已经有了苹果股票和标准普尔 500 指数的相同时间段的一年的数据，你可以将这些数据合并为一个单一的 DataFrame：

```py
df = hist.join(index_data, rsuffix = '_idx')
```

连接的 DataFrame 中有列名相同的列。为了避免重叠，你使用 `rsuffix` 参数。它指示 `join()` 方法将后缀 `'_idx'` 添加到 `index_data` DataFrame 中所有列的名称上。

对于我们的目的，你只关心苹果和标准普尔 500 指数的每日收盘价和交易量。在这里，你将 DataFrame 过滤，只保留这些列：

```py
df = df[['Close','Volume','Close_idx','Volume_idx']]
```

如果你现在打印 `df` DataFrame，你应该看到类似下面的内容：

```py
 Close     Volume  Close_idx  Volume_idx
Date                                                    
2021-01-15  126.361000  111598500    3768.25  2741656357
2021-01-19  127.046791   90757300    3798.91  2485142099
2021-01-20  131.221039  104319500    3851.85  2350471631
2021-01-21  136.031403  120150900    3853.07  2591055660
2021-01-22  138.217926  114459400    3841.47  2290691535
`--snip--`
2022-01-10  172.190002  106765600    4670.29  2668776356
2022-01-11  175.080002   76138300    4713.07  2238558923
2022-01-12  175.529999   74805200    4726.35  2122392627
2022-01-13  172.190002   84505800    4659.03  2392404427
2022-01-14  173.070007   80355000    4662.85  2520603472
```

该 DataFrame 包含一个连续的多变量时间序列。下一步是从数据中提取特征，这些特征可以作为机器学习模型的输入。

### 从连续数据中提取特征

你希望根据每天的价格和交易量变化来训练模型。正如你在第十章中学到的，通过将数据点向时间上移，你可以计算连续时间序列数据中的百分比变化，将过去的数据点与当前数据点对齐以进行比较。在下面的代码中，你使用 `shift(1)` 来计算每列 DataFrame 中的百分比变化，并将结果保存在一组新的列中：

```py
import numpy as np
df['priceRise'] = np.log(df['Close'] / df['Close'].shift(1))
df['volumeRise'] = np.log(df['Volume'] / df['Volume'].shift(1))
df['priceRise_idx'] = np.log(df['Close_idx'] / df['Close_idx'].shift(1))
df['volumeRise_idx'] = np.log(df['Volume_idx'] / df['Volume_idx'].shift(1))
df = df.dropna()
```

对于每一列数据，你需要将每个数据点除以前一天的对应数据点，然后取结果的自然对数。记住，自然对数能较好地近似百分比变化。最终，你将得到几列新的数据：

1.  `priceRise` 苹果股票价格从一天到另一天的百分比变化

1.  `volumeRise` 苹果交易量从一天到另一天的百分比变化

1.  `priceRise_idx` 标准普尔 500 指数价格从一天到另一天的百分比变化

1.  `volumeRise_idx` 标准普尔 500 指数交易量从一天到另一天的百分比变化

你现在可以再次过滤 DataFrame，仅保留新生成的列：

```py
df = df[['priceRise','volumeRise','priceRise_idx','volumeRise_idx']]
```

DataFrame 的内容现在看起来会类似于以下内容：

```py
 priceRise  volumeRise  priceRise_idx  volumeRise_idx
Date                                                            
2021-01-19   0.005413   -0.206719       0.008103       -0.098232
2021-01-20   0.032328    0.139269       0.013839       -0.055714
2021-01-21   0.036003    0.141290       0.000317        0.097449
2021-01-22   0.015946   -0.048528      -0.003015       -0.123212
2021-01-25   0.027308    0.319914       0.003609        0.199500
`--snip--`
2022-01-10   0.000116    0.209566      -0.001442        0.100199
2022-01-11   0.016644   -0.338084       0.009118       -0.175788
2022-01-12   0.002567   -0.017664       0.002814       -0.053288
2022-01-13  -0.019211    0.121933      -0.014346        0.119755
2022-01-14   0.005098   -0.050366       0.000820        0.052199
```

这些列将成为模型的特征，或者独立变量。

### 生成输出变量

下一步是为现有数据集生成输出变量（也称为目标或因变量）。这个变量应该反映股票第二天的价格变化：是上涨、下跌还是保持不变？你可以通过查看第二天的`priceRise`列来得知，使用`df['priceRise'].shift(-1)`可以获取该列。负向移动将未来的值向后移。基于这种偏移，你可以生成一个新列，若价格下跌则为`-1`，若价格不变则为`0`，若价格上涨则为`1`。操作如下：

```py
❶ conditions = [
    (df['priceRise'].shift(-1) > 0.01),
    (df['priceRise'].shift(-1)< -0.01)
]
❷ choices = [1, -1]
df['Pred'] = ❸ np.select(conditions, choices, default=0)
```

这里实现的算法假设以下几点：

1.  相较于第二天的价格，若价格上涨超过 1％，则视为上涨（`1`）。

1.  相较于第二天的价格，若价格下降超过 1％，则视为下跌（`-1`）。

1.  剩余部分视为停滞（`0`）。

为了实现该算法，你定义了一个`conditions`列表，用于根据第 1 点和第 2 点❶检查数据，同时定义一个`choices`列表，包含`1`和`-1`的值，用于表示价格的上涨或下跌❷。然后，你将这两个列表传递给 NumPy 的`select()`函数❸，该函数根据`conditions`中的值从`choices`中选择相应的值，构建一个数组。如果没有满足条件的情况，将分配一个默认值`0`，以满足第 3 点的要求。你将该数组存储在一个新的 DataFrame 列`Pred`中，可以将其作为训练和测试模型的输出。实际上，`-1`、`0`和`1`现在是模型在对新数据进行分类时可以选择的可能类别。

### 训练与评估模型

要训练你的模型，scikit-learn 要求你将输入和输出数据分别呈现为独立的 NumPy 数组。你可以从这里的`df`数据框生成这些数组：

```py
features = df[['priceRise','volumeRise','priceRise_idx','volumeRise_idx']].to_numpy()
features = np.around(features, decimals=2)
target = df['Pred'].to_numpy()
```

现在，`features`数组包含了四个自变量（输入），`target`数组包含了一个因变量（输出）。接下来，你可以将数据分为训练集和测试集，并训练模型：

```py
from sklearn.model_selection import train_test_split
rows_train, rows_test, y_train, y_test = train_test_split(features, target, test_size=0.2)
from sklearn.linear_model import LogisticRegression
clf = LogisticRegression()
clf.fit(rows_train, y_train)
```

就像你在本章早些时候的情感分析示例中做的那样，你使用 scikit-learn 的`train_test_split()`函数按 80/20 的比例划分数据集，并使用`LogisticRegression`分类器来训练模型。接下来，你将数据集的测试部分传递给分类器的`score()`方法来评估其准确性：

```py
print(clf.score(rows_test, y_test))
```

结果可能如下所示：

```py
0.6274509803921569
```

这表明模型大约 62%的时间准确地预测了苹果股票第二天的走势。当然，你也可能得到不同的结果。

## 总结

在这一章中，你学习了如何使用机器学习来完成一些数据分析任务，例如分类，这是一种使计算机系统能够从历史数据或过去经验中学习的方法。特别地，你了解了如何将机器学习算法应用于自然语言处理任务中的情感分析。你将来自亚马逊产品评论的文本数据转化为机器可读的数值特征向量，然后训练模型根据评论的星级评分进行分类。你还学会了如何基于数值股市数据生成特征，并利用这些特征训练模型来预测股票价格的变化。

结合机器学习、统计方法、公共 API 和 Python 中可用的数据结构的可能性有很多。本书展示了其中的一些可能性，涵盖了各种主题，并希望能够激发你找到许多新的创新解决方案。
