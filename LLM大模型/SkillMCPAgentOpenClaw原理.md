# Skill/MCP/Agent/OpenClaw原理

https://www.bilibili.com/video/BV1ojfDBSEPv/?spm_id_from=333.1387.homepage.video_card.click&vd_source=eeecc9c7e484ac68a459b138ecf98f3b



## **LLM大语言模型**

本身只能做文字接龙，只当初这样用-->智障

人为区分两个角色：问、答

<font color="red">一问一答、不能追问！</font>

## **Prompt提示词**

![image-20260227173606898](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20260227173606898_usQxAT.png)

## **Context上下文**

## **Memory记忆**

将历史对话放到context --> 伪装成多轮对话（追问效果）

memory可进一步总结压缩，进而减少上下文长度

![image-20260227173652203](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20260227173652203_VXn8Jq.png)

## **Agent智能体**

LLM中信息落后过时、且本身不具备搜索能力，引入agent在LLM和用户之间完成新的信息检索（搜索网络信息、检索本地文档/数据库）

## **Search搜索**

不同于传统数据库，使用向量数据库、匹配语义相近的片段

### **RAG Retrieval Augmented Generation检索增强生成**

通过语义匹配向量化的信息，并将其加入上下文，用于增强生成内容的可靠性

![image-20260227174258451](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20260227174258451_uHwgCE.png)





![image-20260227174349410](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20260227174349410_DcOJnM.png)

## **Function calling**

![image-20260227174454688](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20260227174454688_MdzKhO.png)

## **MCP**

解耦，把不同服务从agent中抽取出来

这些服务和agent主程序之间需要另外一套规范进行协同 -》 MCP模型上下文协议



## **大模型和agent的交互**

![image-20260227174549469](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20260227174549469_GaQ19L.png)

## **agent和用户的交互**

![image-20260227175028496](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20260227175028496_6nCmuw.png)

## 智能体的统一缺点&解决方案

### 场景

让一个agent从一份英文pdf中提取->翻译成中文->保存成markdown文本

可以直接将需求描述给agent，让其自己策划整体流程

![image-20260227175532834](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20260227175532834_Y8CnXz.png)

#### 问题 <font color="red">**如果这个流程相对稳定，但每次重新让agent自由发挥的话 --> 不稳定 + 浪费token**</font>

#### 解决方案 langchain / workflow 固化链式处理流程

![image-20260227175930634](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20260227175930634_VtlJTm.png)

### 场景

多种形式输入 + 多种形式输出

#### 问题 所有排列组合-不同的langchain/workflow / if-else判断 不友好

#### 解决方案 skill 

1. 准备一个目录 将所有可能涉及到转换脚本全部放在该目录下，用一个统一的说明文件skill.md描述整体流程，告诉agent根据输入文件的格式灵活选取指定脚本

2. 在给agent下达最终指令前，要求先读取skill.md中的要求

![image-20260227180206143](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20260227180206143_gtsqav.png)

![image-20260227180746090](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20260227180746090_u8IpUU.png)

![image-20260227180843825](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20260227180843825_EwY6Bo.png)

**<font color="red">进一步优化： 省略指定读取的语句，直接在agent中加入程序，每次主动读取skill.md</font>**

![image-20260227181232428](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20260227181232428_vSTKzN.png)

### 问题 复杂任务可能会让agent中context非常大

![image-20260227181341404](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20260227181341404_0zB8jt.png)

### 解决方案 subagent

独立的子任务可以单独在subagent中完成 -> context隔离，subagent的context不会在主agent中保留

![image-20260227181439883](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20260227181439883_pwnuYz.png)

# 汇总

![image-20260227181621246](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20260227181621246_elS1HB.png)

## Function Calling vs MCP

function calling： agent和llm沟通的约定，目的：让llm的回答符合一定格式，方便程序进行解析

mcp：agent和工具服务间调用的约定，目的：像接口文档一样约定怎么调用、传递参数、接收返回值等

![image-20260227182124222](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20260227182124222_uOMJMd.png)

## MCP vs Skill

Skill: prompt加载器，唯一需要的文件就是skill.md，其他不做任何要求

skill是否可以取代mcp？可以，把mcp服务中提供的工具全部放在skill下，并在skill.md文件中说明如何使用

![image-20260227182247295](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20260227182247295_Il8gzC.png)



## langchain / workflow / skill / agent

|           |                                                              | 优点                                       | 缺点                             |
| --------- | ------------------------------------------------------------ | ------------------------------------------ | -------------------------------- |
| langchain | 纯编码形式实现                                               | 全部硬编码，稳定                           | 失去一定的柔性，难容忍一些小问题 |
| workflow  | 把程序实现换为 低代码拖拽                                    | 修改简单，容易编写                         |                                  |
| skill     | 把langchain/workflow这种由程序控制的流程走向 -> 变成由agent自行控制，但要提前写好说明文档和直接可运行的脚本 | 存在一定灵活调整的空间，又不至于特别不可控 |                                  |
| agent     | 随时根据自己的判断调整流程，甚至自行编写脚本                 | 非常灵活                                   | 不可控                           |

![image-20260227182440902](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20260227182440902_BpMdQu.png)

## Skill特性：渐进纰漏、按需加载 --》可能会在未来token越来越便宜之后变得鸡肋；skill兼顾了稳定性和灵活性，可能会在未来逐步淘汰mcp和workflow