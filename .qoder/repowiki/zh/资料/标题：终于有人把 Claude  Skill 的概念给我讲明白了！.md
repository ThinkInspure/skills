标题：终于有人把 Claude  Skills 的概念给我讲明白了！



最近 Claude 的 Skills 很火，听到很多朋友对其进行讨论。

但是，存在很多争议。

本文用相对通俗易懂的语言讲解一下 Skills是什么，和 MCP 有什么区别，最核心的优势有哪些等等。



## Skills 是什么？

Claude 虽然很强大，但是实际工作需要「流程知识」和「组织架构」知识。

Claude 推出 Agent Skills 这种利用文件和文件夹来构建专业 Agent 的新方法。

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251219232518390.jpeg)

Agent Skills  是一个目录，如 pdf、docx 等。

里面包含一个 SKILL.md 文件，以及相关脚本和资源。

 Agent 可以动态发现并加载这些文件夹，从而更好地完成特定任务。

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251219234626120.webp)

SKILL.md 文件结构，包括相关元数据：名称、描述以及与技能应执行的具体操作相关的上下文。

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220000910395.webp)

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220000841482.webp)

SKILL.md 是技能的主要描述描述，其中可以提到文件夹中的其他资源或脚本。

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251219233820216.webp)

Skills 一个关键优势在于「渐进式披露」。

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251219233604616.png)

SKILL.md 的元信息（名称、描述）始终会被加载到上下文中，这样大模型就可以根据对话灵活选择使用哪些技能。

当「skill」 被触发以后，会加载  Body 部分。

其他的资源，如 文本文件、脚本和数据等会根据 SKILL.md 中的指示，按需加载。



![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251219233746031.webp)

Agent 的系统提示词和已经装载的 Skills 始终放在上下文中，如上图，包括 pdf、pptx 等。

用户要求“基于你对我的了解，填好这个 PDF”

**决定触发**：Claude 意识到需要调用 PDF 技能，于是它主动执行了一个 Bash 命令去读取该技能的详细文档 (`SKILL.md`)。

**按需加载**：通过读取文件，Claude 学习了如何具体操作 PDF 的指令。

**追踪引用**：它发现 `SKILL.md` 中提到了处理表单的具体逻辑在 `forms.md` 里，于是再次执行命令读取该文件。

**最终执行**：在掌握了所有必要的“说明书”后，AI 才真正开始处理用户的 PDF 文件。



## Skills VS Rule VS MCP 的区别

Skills 是相对静态的技能，内容多是专家知识和执行步骤，核心是渐进式加载。

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251219235114283.png)

Rule 是规则，可能包括一些公共的提示词、智能体行为约束，智能体使用工具的规范，以及一些关键的语法规范等。Rule 支持总是加载、按需加载、手动加载、条件加载等多种生效方式。

在没有 Skills 之前，我们为了节省上下文，通常会对 Rule 进行“精简”，仅放最关键的信息。

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251219234804310.png)

MCP  是模型上下文协议，MCP 关键是提供了很多有用的工具。

MCP 的工具背后有可能是传统的后端接口，有可能是知识库，也有可能是一个工作流，甚至有可能是一个智能体等等。

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220184327506.png)

Skill 解决了“模型什么都懂一点，但具体到业务流程就不专业”的问题。

相比 Skill 的流程性，Rule 更多是全局性的。如果说 Skill 是 Agent 的“技能包”，Rule 就是 Agent 的“规范”。

MCP 更像是“外挂”，让 Agent 拥有调用各种工具的能力。

这些技术只是侧重点不一样，有些场景其实在用哪些技术都可以，并没有严格区分。



## 如何安装 Skills?

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220184544115.png)

传送门：https://github.com/anthropics/skills

其实就是你看得再多，也没亲自动手去使用一个技能、创建一个技能，理解会更深刻。所以我们需要去用，然后有条件的话再去创建一些技能。



### 在 Claude Code 中使用

第一步，设置 Skills 市场

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220184928339.png)

```
/plugin marketplace add anthropics/skills
```

我们也可以安装其他非官方市场的 skills

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220191025227.png)

传送门：https://github.com/chujianyun/skills/

比如我的 skills 市场中目前提供了一款非常好用的提示词优化 skill。Marketplace 路径 :`chujianyun/skills`

>  注：可使用、可修改(需保留作者信息)，未经允许禁止商用

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220194434728.png)

当前用户撰写提示词存在很多难点：

- 可能表达不清楚，存在遗漏、歧义
- 知道的提示词框架非常有限，很难写出专业的提示词框架。

当前提示词优化工具的主要缺点：

- 你提供的信息可能会存在意图和错误。那么它们也会直接生成。
- 很多提示词优化工具产出的提示词，虽然很结构化，看起来也很专业，但大多是相对通用的提示词框架。

详情参见：[你还在手工写提示词？大厂 AI应用工程师揭秘：2个工具帮你把提示词写出“专业范”！](https://mp.weixin.qq.com/s/DXJEeYOT950j-9-C4-Ea5A)

我的 `prompt-optimizer` 这个 skill，可以很好地解决这个问题：

- 如果发现缺失、歧义或错误会主动和用户确认。
- 根据用户描述场景选择最适合的专业提示词框架（50多个全球顶尖的提示词框架），自动生成。

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220185534074.png)

```
/plugin
#切换到 Marketplaces
#选择 Add Marketplace
#填写 chujianyun/skills
```



![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220185948574.png)

在 Discover 里面可以看到官方市场和我的市场中可安装的插件（一组 Skills）啦！

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220185901886.png)

安装时，可以选择是用户级别，项目级别还是本地级别。



![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220191733164.png)

在 Installed 里面可以关闭插件，对插件进行更新、卸载等。

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220192155421.png)

插件市场插件的安装情况以及技能都在 ~/.claude/plugins 目录中。



![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220190326392.png)

传送门：https://github.com/anthropics/skills/tree/main/skills

很多朋友可能会好奇，官网上的技能很多，为什么刚才选的时候只有两个？

```
{
  "name": "anthropic-agent-skills",
  "owner": {
    "name": "Keith Lazuka",
    "email": "klazuka@anthropic.com"
  },
  "metadata": {
    "description": "Anthropic example skills",
    "version": "1.0.0"
  },
  "plugins": [
    {
      "name": "document-skills",
      "description": "Collection of document processing suite including Excel, Word, PowerPoint, and PDF capabilities",
      "source": "./",
      "strict": false,
      "skills": [
        "./skills/xlsx",
        "./skills/docx",
        "./skills/pptx",
        "./skills/pdf"
      ]
    },
    {
      "name": "example-skills",
      "description": "Collection of example skills demonstrating various capabilities including skill creation, MCP building, visual design, algorithmic art, internal communications, web testing, artifact building, Slack GIFs, and theme styling",
      "source": "./",
      "strict": false,
      "skills": [
        "./skills/algorithmic-art",
        "./skills/brand-guidelines",
        "./skills/canvas-design",
        "./skills/doc-coauthoring",
        "./skills/frontend-design",
        "./skills/internal-comms",
        "./skills/mcp-builder",
        "./skills/skill-creator",
        "./skills/slack-gif-creator",
        "./skills/theme-factory",
        "./skills/web-artifacts-builder",
        "./skills/webapp-testing"
      ]
    }
  ]
}
```

传送门：https://github.com/anthropics/skills/blob/main/.claude-plugin/marketplace.json

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220190654696.png)

其实插件市场对 Skills 进行了分组。

一个插件市场可以包括多个插件，一个插件里面可能包含很多技能。

需要注意的是，安装好技能以后，需要重启终端才能生效。

### 在其他 AI Coding 工具中使用

这个我们在前面的文章中已经有详细的介绍，详情参见：

[如何在 Qoder、Cursor、Trae、Windsurf 等 AI Coding 工具中使用 Claude Skills](https://mp.weixin.qq.com/s/5vJMymAsu_IF-7LFznuMvg)



## 如何使用 Skills

我们已经装好了官方的 skills 和我自己的 skills。

当打开 Claude Code 时，它一直在上下文中。在使用过程中，它会灵活选择适合的技能，更好地回答我们的问题。

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220200941857.png)

我们前面安装了很多 skill，包括我的提示词自动优化工具。

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220201745235.png)

我们在 Claude Code 中说优化提示词，把需要优化的提示词发给它。

Agent 会匹配到提示词优化 Skill ，加载 SKII.md 文件，读取提示词优化的技能描述。

Agent 会加载摘要文件，根据提示词的场景从中匹配出最适合的一个或多个框架，然后加载这些框架的详细描述。

Agent 自动选择最适合的框架，如果用户的输入存在模糊或歧义和用户确认清楚。

最终 Agent 负责写出更清晰、专业提示词。



![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220202049791.png)

在这个过程中，我们可以体会到 Skills 的「渐进式加载」的好处。

如果我们把它写成 Rule，因为 Rule 是一个整体，要么加载要么不加载。

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220195504624.png)

我们知道虽然大模型可以支持很长的上下文，但，上下文越长效果越差，成本越高。

因此，我们需要把 Rule 写得相对精简。

哪怕再精简，很多大量的其他提示词框架信息也会被加载到上下文中浪费 Tokens 甚至会造成负面影响。

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220195951591.png)

但是写成 Skill，虽然元信息（name、description）始终会加载到 Agent 上下文中，但 Skill 仅在被使用的时候激活。

它会先加载 `prompt-optimizer`  Skill 的 SKILL.md 文件，了解如何进行提示词优化。

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220200102605.png)

它会根据指示，加载 `references/Frameworks_Summary.md` 提示词框架摘要文件。

![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251220202122872.png)

根据摘要根据用户的意图和摘要文件选择最适合的一个或多个框架，然后再去加载具体的框架内容。

即使我们的框架再多，有几百个甚至几千个，因为只加载需要的那一两个框架，也不会造成上下文过载。



## 写在最后

这篇文章我们介绍了什么是 Skills，以及 Skills 和 Rule 和 MCP 的区别，以及如何安装和使用。

Skills  是为了给大模型增加一些更专业的知识和技能。模型依然更关键的因素，就拿提示词优化来说，同样的技能应用在不同的模型上，它的效果也会有差异，有条件有限选择更强大的模型。

关注我，后期我会以本文的提示词优化 Skill 为例分享如何快速创建出高质量的 Skills。 

---

如果文章对你有帮助，可以给我三连击：点赞、喜欢，并转发给身边需要的朋友。

----

悟鸣，浙江省人工智能专家服务团专家，大厂 AI 应用工程师， 人工智能训练师，CSDN、阿里云技术社区博客专家，Qoder 大使， WeaveFox 官方 AI 布道师， Cherry Studio 官方认证讲师。

欢迎关注我的公众号，后续会陆续分享比较有用的 AI 工具和比较好的 AI 经验，比较客观理性的 AI 观点等。

![](https://mmbiz.qpic.cn/sz_mmbiz_jpg/n4KQvmEGX5DhpMtic1aPEezl12nSTwVpl6kTsCjql5DgOT5z1hgmOzuTLvBU1cezqDa8JiaYXrcibNEvGBlnbFEoA/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=14)

欢迎加入我们的 AI 交流群，群里面有一些是大学生、大学老师，有一些是大厂搞 AI 业务的同学，也有很多其他行业积极拥抱 AI的朋友。



![](https://mingmingruyue-hz.oss-cn-hangzhou.aliyuncs.com/2025/20251105003104382.png)













































