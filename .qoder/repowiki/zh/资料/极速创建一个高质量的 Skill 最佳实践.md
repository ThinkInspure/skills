标题：极速创建一个高质量的 Claude  Skill 最佳实践

前面我们介绍了Claude  Skills 的概念、核心优势，以及和 Rule、 MCP 的区别。

我们还介绍了如何在 Claude 中以及其他 AI Coding 工具中使用这些 Skill。

详情参见：

- [如何在 Qoder、Cursor、Trae、Windsurf 等 AI Coding 工具中使用 Claude Skills](https://mp.weixin.qq.com/s/5vJMymAsu_IF-7LFznuMvg)

今天以我原创的提示词优化 Skills 为例给大家分享如何快速创建一个高质量的 Skill。



## 前期准备：AI First

### 解决的场景

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220210111547.png)

当前用户撰写提示词存在很多难点：

- 可能表达不清楚，存在遗漏、歧义
- 知道的提示词框架非常有限，很难写出专业的提示词框架。

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220210215971.png)

当前提示词优化工具的主要缺点：

- 你提供的信息可能会存在意图和错误。那么它们也会直接生成。
- 很多提示词优化工具产出的提示词，虽然很结构化，看起来也很专业，但大多是相对通用的提示词框架。

详情参见：[你还在手工写提示词？大厂 AI应用工程师揭秘：2个工具帮你把提示词写出“专业范”！](https://mp.weixin.qq.com/s/DXJEeYOT950j-9-C4-Ea5A)

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220210326197.png)

我打算设计一个名为 `prompt-optimizer`  skill，通过以下方式解决这些问题：

- 如果发现缺失、歧义或错误会主动和用户确认。
- 根据用户描述场景选择最适合的专业提示词框架（50多个全球顶尖的提示词框架），自动生成。

### 理念转变

我们前面学了 Skill，虽然已经大概掌握了 Skill 的结构，但是真正亲手去写还是有很大门槛。

我们应该尽量秉承“AI First” 的理念，很多任务首先想到的是  “AI 能不能做好”，“如何让 AI 帮我干得更好”。

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220205349383.png)

那么我们就需要把**任务拆解到大模型的能力边界以内**，然后**把任务交代清楚**，然后**给大模型提供充足准确的信息**。

具体到咱们这个场景，我们具体要怎么做？

**表达清楚**相对容易：

我需要让大模型去匹配出最适合的框架，然后核实用户有没有说清楚。如果没有，让用户做一些核对，然后再按照这个框架生成出专业的提示词。

**充足准确的上下文**：

那我们需要把这些专业的提示词框架给它。

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220211537330.png)

我们可以在网上找到一些专业的 AI 框架网站，然后让 AI  Coding  工具（如 Qoder、Cursor 等）通过 MCP 的方式把这些框架抓下来。

---

那么，**如何更好地利用「渐进式式加载」的机制**？

我们可能有几十个，未来可能有上百个提示框架，哪怕 Claude 支持渐进式加载，它也无法在没有加载完所有的提示词框架前就能够判断出来该使用哪些框架。

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220211554240.png)

因此，我们可以<u>让 AI 帮助我们根据当前的所有框架生产出一份摘要</u>。

这样智能体就可以先根据摘要锁定对应的框架，然后再提取对应的框架文件了解详情。



## 创建方式

那有了提示词的框架，也有了摘要，我们如何去创建 Skill？

有两种方式，一种是直接通过 AI Coding 工具创建，一种是通过官方的 skill-creator 这个 Skill 创建。

### AI Coding 工具创建

AI Coding 工具，有很多，我最常用的 AI Coding 工具之一是 Qoder。

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220211931136.png)

我们可以把 Anthropic 官方的 Skill 仓库拉下来。传送门：https://github.com/anthropics/skills

因为这里有很多官方的例子，还有一些相关的说明。

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220211812690.png)

 通常，我会先用 Qoder 的仓库 Wiki 功能生成一份专业详细的Wiki，快速了解关键信息，有任何疑问直接提问。



![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220212357758.png)

我们把前面准备的这些材料放到文件夹里，放到官方的 skills 目录，然后把我们想要做的事情说清楚，让 AI 自动帮我们生成对应的 skill。

参考提示词：

```
我希望你按照 Skill 规范，帮我把“提示词框架”这个文件夹改造成 “提示词优化专家”（需要改成英文）的 skill。当用户想要优化提示词时启用该功能。

流程： 用户直接发送需求或者原始提示词，AI 需要从   中选择最匹配的场景，然后匹配最适合的框架名称，读取框架名称对应的框架描述文件，然后判断用户的输入的需求或原始提示词是否存在歧义或缺失，和用户进行核对，核对清楚以后，按照匹配的最佳提示词框架产出最终提示词。

要求：请你按照 Skill 规范，生成对应的 Skill。确保文件夹名称，结构啥的都符合 Skill 规范，且功能的正确性
```



![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220212556990.png)

那么很快它就会按照 Skills 的规范，根据我们提供的要求和相关资料，生成出一个非常专业、高质量的 Skills。



该 Skill 已开源：https://github.com/chujianyun/skills  需要的朋友欢迎安装体验。

> 允许使用，修改需保留原作者信息，禁止商用，商用需与我联系获得同意



### 官方 skill-creator

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220212713303.png)

细心的网友可能会发现，官方的 Skill 代码仓库中有一个自动创建 Skill 的 Skill。

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220213018397.png)

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220213133700.png)

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220213146832.png)

同样地， cd 到准备好的素材目录，然后发送同样的提示词，Claude Code 会根据该 Skill 自动帮我们创建好提示词。



## 安装体验

在 Claude Code 中增加插件市场

```
/plugin marketplace add chujianyun/skills
```

插件市场安装

```
/plugin install prompt-engineering-skills@chujianyun/skills
```



![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251221111142909.png)

说出自己需要提示优化，然后把原始提示词发给他。

它会和你进行一些核对，核对清楚后，再按照最适合的框架给出对应的优化后的提示词。



如果想在其他的 Agent 里面使用 Skills，参见：[如何在 Qoder、Cursor、Trae、Windsurf 等 AI Coding 工具中使用 Claude Skills](https://mp.weixin.qq.com/s/5vJMymAsu_IF-7LFznuMvg)





## 写在最后

那这篇文章分享了快速创建一个高质量的 Skills 的方法。

有了先进大模型的加持，做出来的难度已经大大降低。更多的还是说**你想做什么**？你**能不能说清楚**，你**能不能把相关的资料准备好**。

大家可以参考这种思路，如果自己有特别好的想法，想包装成 Skills 的话，可以自己动手去搞出来。



---

如果文章对你有帮助，可以给我三连击：点赞、喜欢，并转发给身边需要的朋友。

----

悟鸣，浙江省人工智能专家服务团专家，大厂 AI 应用工程师， 人工智能训练师，CSDN、阿里云技术社区博客专家，Qoder 大使， WeaveFox 官方 AI 布道师， Cherry Studio 官方认证讲师。

欢迎关注我的公众号，后续会陆续分享比较有用的 AI 工具和比较好的 AI 经验，比较客观理性的 AI 观点等。

![](https://mmbiz.qpic.cn/sz_mmbiz_jpg/n4KQvmEGX5DhpMtic1aPEezl12nSTwVpl6kTsCjql5DgOT5z1hgmOzuTLvBU1cezqDa8JiaYXrcibNEvGBlnbFEoA/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=14)

欢迎加入我们的 AI 交流群，群里面有一些是大学生、大学老师，有一些是大厂搞 AI 业务的同学，也有很多其他行业积极拥抱 AI的朋友。



![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251105003104382.png)



















