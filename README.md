[TOC]

# 小说人物关系网络的比较分析 v2.0

## 说明

1. 衡量关系
   1. 以共同出现的段落的总字数作为关系强度的代理变量。
   2. 只有不小于关系强度的最大值的 1/10 的关系，才会被纳入图中。
   3. 网络图中，人物两两之间都有一条边的可能性越高，集聚系数就会越高。
2. 第二版和第一版最大的区别，是程序运行速度的优化
   1. 程序中最耗时的部分，是将人物的所有代称规范为统一的称呼，如必须将“过儿”、“神雕大侠”、“傻蛋”、“杨大哥”统一为“杨过”。这就需要从旧的段落生成所有代称被规范后的新段落。
   2. 为了保护原始数据，R 语言监测到数据的变化时，默认会拷贝一份数据的副本，使变化发生在副本上。这对数据安全是有好处的，但拷贝（相对于计算）是一项非常消耗时间的行为，这大大拖慢了 R 程序的速度。特别是当数十个人物的所有代称都要被替换时，每一次替换都要拷贝原文的副本，造成了时间的极大浪费。
   3. 因此第二版使用了 data.table 类的象牙操作符`:=`，该操作符在修改数据时不会拷贝副本，而是直接写在**内存中的**原数据上，从而极大地提高了程序的运行速度（原地修改的耗时，仅是拷贝副本的二十分之一）。
   4. 推而广之，人们对 R 的主要诟病是它的速度，但其实只要在不影响数据安全的地方充分利用原地修改、向量化操作等技术，R 的速度是完全可以接受的，不会比 Python 慢多少。

## 《神雕侠侣》

热力图中，最密切的关系，是杨过-小龙女、杨过-黄蓉和杨过-郭靖。可见，在爱情主线之外，孤儿对父母之爱的渴望和纠结，始终是本书的一条暗线。

网络图是典型的星型结构，因为这本书其实就杨过一个主角，对小龙女的刻画其实是比较弱的（小龙女和任盈盈，其实是金庸长篇中刻画力度不够、形象略显单薄的女主角）。集聚系数比较高，是因为主要人物太少（相比后面三本书）。

### 热力图

<img src="http://humoon-image-hosting-service.oss-cn-beijing.aliyuncs.com/img/typora/JavaScript/神雕侠侣人物关系热力图.png" alt="神雕侠侣人物关系热力图"  />

### 聚类图

<img src="http://humoon-image-hosting-service.oss-cn-beijing.aliyuncs.com/img/typora/JavaScript/神雕侠侣人物关系聚类图.png" alt="神雕侠侣人物关系聚类图"  />

### 网络图

![神雕侠侣人物关系网络图](http://humoon-image-hosting-service.oss-cn-beijing.aliyuncs.com/img/typora/JavaScript/神雕侠侣人物关系网络图.png)

###  矢量网络图（高清）

[神雕侠侣人物关系网络图.pdf](./figure/神雕侠侣人物关系网络图.pdf) 



## 天龙八部

热力图中，最密切的关系是段誉-王语嫣，其次是萧峰-阿朱、萧峰-阿紫、段誉-木婉清和虚竹-童姥……说好的兄弟情呢<img src="http://humoon-image-hosting-service.oss-cn-beijing.aliyuncs.com/img/typora/JavaScript/640" alt="图片" style="zoom: 50%;" /> 男人之间强度最高的关系是段誉-慕容复。

从聚类图可以看的很清楚，在段誉、萧峰、虚竹之外，姑苏慕容氏是第四主角。

### 热力图

![天龙八部人物关系热力图](http://humoon-image-hosting-service.oss-cn-beijing.aliyuncs.com/img/typora/JavaScript/天龙八部人物关系热力图.png)

### 聚类图

![天龙八部人物关系聚类图](http://humoon-image-hosting-service.oss-cn-beijing.aliyuncs.com/img/typora/JavaScript/天龙八部人物关系聚类图.png)

### 网络图

![天龙八部人物关系网络图](http://humoon-image-hosting-service.oss-cn-beijing.aliyuncs.com/img/typora/JavaScript/天龙八部人物关系网络图.png)

### 矢量网络图（高清）

 [天龙八部人物关系网络图.pdf](./figure/天龙八部人物关系网络图.pdf) 



## 三国演义

热力图中，强度最大的二元关系是：曹操-刘备，曹操-诸葛亮，曹操-关羽，曹操-袁绍，刘备-诸葛亮，刘备-关羽，刘备-张飞，刘备-赵云，诸葛亮-赵云和诸葛亮-魏延。

聚类图中，由于刘备的活跃跨越漫长的时间和广阔的空间，他和董卓、吕布、二袁、刘表、刘璋等群众被分在了一类，而蜀汉的大部分人和诸葛亮被归为了一类。有趣的是，魏、蜀、吴、群雄之外，关羽、孙乾、糜竺和吕蒙被归为了独立的一类，大概关羽之死，在《三国演义》里是相对独立的一部分吧。

《三国演义》的网络图明显变得复杂多了，在曹操、刘备、孙权、诸葛亮的小四边形中间，有密密麻麻的边。该图的集聚系数比《天龙八部》略高，表明次要人物之间的互动占全书篇幅的比例有所上升。毕竟，真实世界是非常去中心化的，三国的故事即使经过文学改造，仍然保留了部分现实的特点。

### 热力图

![三国演义人物关系热力图](http://humoon-image-hosting-service.oss-cn-beijing.aliyuncs.com/img/typora/JavaScript/三国演义人物关系热力图.png)

### 聚类图

![三国演义人物关系聚类图](http://humoon-image-hosting-service.oss-cn-beijing.aliyuncs.com/img/typora/JavaScript/三国演义人物关系聚类图.png)

### 网络图

![三国演义人物关系网络图](http://humoon-image-hosting-service.oss-cn-beijing.aliyuncs.com/img/typora/JavaScript/三国演义人物关系网络图.png)

### 矢量网络图（高清）

 [三国演义人物关系网络图.pdf](./figure/三国演义人物关系网络图.pdf) 



## 红楼梦

热力图中，最密切的三对关系是贾宝玉-贾母、贾宝玉-林黛玉、贾母-王熙凤。次一档的是贾宝玉-薛宝钗、贾宝玉-袭人和林黛玉-薛宝钗。

聚类图从左到右，逐渐从大观园内的理想世界过渡到大观园外的现实世界。主要人物的横坐标几乎象征着他们与现实世界的距离远近。像被分在单独一类的几个大丫鬟，表面上长居大观园这个理想世界，但她们的出身，决定了她们距离现实世界并不会太远。除了薛蟠随薛家被分到了最左边，距离现实世界最远的是香菱、紫鹃、宝琴、芳官，细细想来，难道不是吗？

网络图中，星型模式消失了。虽然仍有比较次要的外围人物，但中间再也不是一个人、一个轴心，而是贾宝玉、贾母、王熙凤、王夫人、薛宝钗、林黛玉六个主要节点，共同构成了中心。一般文学意义上主角和配角的区分，在《红楼梦》中大大地淡化了。

该图的集聚系数飙升到 0.478，表明每两个人之间形成密切的二元关系的比率大大上升了——这就更加接近真实世界中复杂组织内部的人际关系。

### 热力图

![红楼梦人物关系热力图](http://humoon-image-hosting-service.oss-cn-beijing.aliyuncs.com/img/typora/JavaScript/红楼梦人物关系热力图.png)

### 聚类图

![红楼梦人物关系聚类图](http://humoon-image-hosting-service.oss-cn-beijing.aliyuncs.com/img/typora/JavaScript/红楼梦人物关系聚类图.png)

### 网络图

![红楼梦人物关系网络图](http://humoon-image-hosting-service.oss-cn-beijing.aliyuncs.com/img/typora/JavaScript/红楼梦人物关系网络图.png)

### 矢量网络图（高清）

 [红楼梦人物关系网络图.pdf](./figure/红楼梦人物关系网络图.pdf)



## 魔兽多塔之异世风云

这是一部网络小说，很典型的网文结构，几乎所有叙述都是紧紧围绕主角展开的。

因此，网络结构是典型的星形，配角之间的关系，没有多少笔墨去描述。集聚系数连 0.1 都不到。

### 热力图

![魔兽多塔之异世风云人物关系热力图](http://humoon-image-hosting-service.oss-cn-beijing.aliyuncs.com/img/typora/JavaScript/魔兽多塔之异世风云人物关系热力图.png)

### 聚类图

![魔兽多塔之异世风云人物关系聚类图](http://humoon-image-hosting-service.oss-cn-beijing.aliyuncs.com/img/typora/JavaScript/魔兽多塔之异世风云人物关系聚类图.png)

### 网络图

![魔兽多塔之异世风云人物关系网络图](http://humoon-image-hosting-service.oss-cn-beijing.aliyuncs.com/img/typora/JavaScript/魔兽多塔之异世风云人物关系网络图.png)

### 矢量网络图（高清）

 [魔兽多塔之异世风云人物关系网络图.pdf](./figure/魔兽多塔之异世风云人物关系网络图.pdf) 
