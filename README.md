# 基于知识图谱的医疗问答

# 依赖
```
pyahocorasick
py2neo
```

# 说明
在原有的基础上，构建了一个实例，使得流程更加清晰。dict下的数据是拷贝而来的，不是根据medical2.json生成的，因为medical2.json数据量太少了。<br>
1、第一步：执行build_medicalgraph.py，构建知识图谱。<br>
2、第二步：执行question_classifier.py，提取问句中的实体以及对问句进行分类，可对标命名实体识别、文本分类、意图识别及槽位填充。<br>
3、第三步：执行question_parser.py，根据实体类别以及问题类型构建查询neo4j的sql语句。<br>
4、第四步：执行answer_search.py，执行sql语句得到结果，并返回格式化后的回答。<br>
5、第五步：执行chatbot_graph.py，主运行程序，包含前面的一些步骤。循环输入问题，得到结果。<br>

# 示例如下
只是用了部分数据，因此构建的问题是专门针对了存在的数据，也可以构建更大的图。
```python
model init finished ......
咨询:二硫化碳中毒的症状是什么？
客服机器人: 二硫化碳中毒的症状包括：谵妄；恶心；昏迷；浅感觉减退或缺失；腱反射消失；多发性神经炎；呕吐；感觉障碍
咨询:百日咳应该吃什么？
客服机器人: 百日咳宜食的食物包括有：圆白菜;南瓜子仁;樱桃番茄;小白菜
推荐食谱包括有：小黄瓜凉拌面;黄瓜拌兔丝;罗汉果雪耳鸡汤;清蒸鸡蛋羹;黄瓜三丝汤;黄瓜拌皮丝;百合双耳鸡蛋羹;排骨汤
咨询:百日咳不应该吃什么？
客服机器人: 百日咳忌食的食物包括有：海虾；螃蟹；海螺；海蟹
咨询:
```

# 补充
1、pyahocorasick需要安装vs环境，如果嫌麻烦，也可以使用其他分词的方式，比如前向+后向最大匹配，前缀树搜索等。<br>
2、整个流程走下来，主体思想分为四个部分：<br>
（1）提取实体及对问题分类。<br>
（2）构建查询语句并在neo4j中进行查询得到结果。<br>
（3）对结果进行格式化并返回。<br>
3、根据以上流程，可以构建其它领域的基于知识图谱的问答系统，当然，数据的获取是一定的问题。<br>
