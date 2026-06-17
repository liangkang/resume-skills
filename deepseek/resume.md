# 梁康

(+86) 13401051254（同微信） ｜ liangkangit@gmail.com

## 工作经历

### 蚂蚁金服

2024年04月 - 至今

后端技术专家 数智引擎

负责业务：1. 从零开发：multi-agent/agent运行时，rag，memory组件；2. 效果优化：prompt/skill 自进化平台；3. benchmark平台搭建；4. 遥测系统搭建

业务价值：1. 轻代码平台：为上千个云上租户提供搭建agent服务的能力；2. 效果优化：让服务根据反馈自动优化效果

### 文远知行

2022年01月 - 2024年03月

L5 SDE 感知infra

负责业务：感知仿真系统，仿真分析平台

主要职责：提高感知系统仿真效率，建立仿真分析平台并减少分析耗时

业务价值：1. 重构训练，benchmark数据管理平台；2. 优化仿真系统，构建仿分析平台；3. 重构底层数据存储

### Hulu

2021年04月 - 2022年01月

Senior SDE 搜索组

- 负责业务：disney+ 视频搜索场景，英语、中文、韩语搜索业务

- 主要职责：垂搜服务搭建，优化搜索效果

- 业务价值：中文、韩语搜索业务上线，提高英语搜索点击率

### 小米科技有限责任公司

2018年04月 - 2021年03月

Team Leader（7人） 小米小爱

- 负责业务：

- 手机内置音乐app搜索场景，日活1400万

- 小爱手机助手，4个垂域（音乐、电台、相机、新闻、视频）服务端开发、意图识别、Query理解

- 主要职责：作为技术负责人从零开始搭建垂搜服务，并优化效果；协调产品、工程团队合作

- 业务价值：大幅提高音乐搜索点击率、有效播放率、日活等核心指标

### 阿里巴巴

2015年04月 - 2018年04月

高级算法工程师 阿里云

- 负责业务：Yunos视频中心推荐、全局搜索热词推荐、应用商店垂搜排序、应用商店suggest排序、钉钉搜索词纠错

## 教育经历

### 北京邮电大学

2012年09月 - 2015年04月

软件工程 硕士 软件工程学院 全日制

### 北京邮电大学

2008年09月 - 2012年07月

智能科学与技术 本科 计算机学院 全日制

- 专业排名：3

- 编程技能：C++、Java、Scala、Python、Go

## 荣誉奖项

 ACM RecSys | Challenge(2016)：工作推荐 | 成绩：第一名

ACM IJCAI | Challenge(2015)：电商推荐系统 | 成绩：第四名

## 开源项目

clawwindows(桌面使用openclaw)开发者，https://www.clawwindows.com~~

小红书skills(使用已登录的浏览器和真实账号操作小红书），https://github.com/liangkang/xiaohongshu-skills

~~基于multi-agent的量化交易平台，https://github.com/liangkang/TradingAgents

基于multi-agent的量化skills，https://github.com/liangkang/TradingAgentsSkills

基于Karpathy llm wiki 的skills，https://github.com/liangkang/llm-wiki-skills

~~雪球社区 + Serenity + autoresearch选股，https://github.com/liangkang/serenity-autoresearch

根据个人信息生成简历pdf，https://github.com/liangkang/resume-skills

## 项目经历

### Agentic RAG

2025年07月 - 至今

负责人 数智引擎技术部

数据生产侧：

* 语雀文档/文档库：1. 数据生成pipeline；2. 后端调用服务

数据消费侧：

* Rag / Graph Rag / Agentic Rag：1. agent平台服务；2. MCP；3. CLI

提效方案：

* agentic 部分使用pi-coding-agent | qwen code | claude code

* skill 提示词优化使用gepa和autoresearch

最终效果：

* baseline：search-O1

* benchmark：musique-4hop

* 提升：
	* 答案要点命中率 相对提升 100.86%
	* 上下文召回率 相对提升 80%
	* 上下文相关性 相对提升 88.57%
	* 忠诚度 相对提升 127.79%

### Agent评测平台

2025年02月 - 2026年06月

负责人 数智引擎技术部

工作内容：

* 本地评测sdk

* EVE评测平台

* 大模型评测 api

### Multi Agent / Agent Policy

2024年04月 - 2025年04月

负责人 数智引擎技术部

项目：

* 从零到一构建agent harness

* agent / multi-agent policy：
	* react
	* plan
	* Orchestrator-worker
	* SOP

提效：
GAIA评测：45.23 vs 32.23（Magentic-1）

### 感知仿真系统和仿真分析平台

2022年01月 - 至今

后端开发

- 业务价值：1. 重构训练，benchmark数据管理平台；2. 优化仿真系统，构建仿分析平台；3. 重构底层数据存储

- 重构训练，benchmark数据管理平台：规范数据标准流程，提高数据标注效率

- 改进仿真系统：时间减少40%且提高稳定性

- 仿真分析平台：提供帧维度的debug工具

- 重构底层数据存储：建立cloudmbag替换rosbag，减少50%重复存储，减少网络开销

### 视频搜索

2021年04月 - 2022年01月

后端开发负责人+算法工程师

- 业务价值：支持英语，韩语，中文搜索功能，周日均调用1200万次

- 搜索工程开发：在AWS上，基于Spring Boot，vertX，ES，搭建垂直搜索

- 搜索词语义召回：基于双塔模型提高搜索词召回量 +200%

### 音乐搜索

2019年10月 - 2021年04月

项目负责人

- 业务价值：对内支持如下搜索场景：2个app（音乐、视频）；Jovi手机语音助手4个垂域（音乐、电台、听书、视频）；对外支持其他5个场景调用，周日均调用2000万次

- 搜索工程开发：基于Spring Boot、ES，用责任链设计模式从零开始搭建垂搜工程

- 搜索词纠错：利用BiLSTM模型提高搜索词召回量 +300%

- 搜索词改写：利用Word2Vec提高改写召回量 +510%

- 命名实体识别：利用BERT-CRF模型提高F1值 +21%

- 搜索下拉提示词排序：利用XGBoost模型提高点击率 +78%

### 智能语音助手垂域服务端开发、语义解析

2018年04月 - 2019年10月

项目负责人

- 业务价值：为多个终端（音箱、手机、有屏音箱、手表等）提供电台、视频、新闻、相机4个垂域的功能

- 服务端工程开发：线上服务开发，支持产品功能的更新迭代

- query理解、意图解析：利用BERT-CRF、模式匹配提高F1 +25%

### 钉钉搜索词纠错

2017年12月 - 2018年04月

项目负责人

- 业务价值：支持钉钉搜索人名、组织名等短文本搜索词纠错功能

- 搜索词纠错：利用HMM模型提高准确率（+24%）和召回率（+230%）

### Yunos搜索项目

2016年10月 - 2017年07月

开发

- 热词推荐（全局搜）：1、利用Bandit算法（Thompson sampling）做新闻热词冷启动提高点击率 +80%；2、利用XGBoost模型提高做个性化推荐排序提高点击率 +20%

- 搜索排序（应用中心搜索）：基于 DSSM 模型的文本 Embedding 进行排序提高点击率 +4.7%

- 商业混排（应用中心搜索）：基于PID算法做投放广告量的控制提高ecpm +8.2%
