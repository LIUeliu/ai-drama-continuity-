# AI 短剧连续性制作

**ai-drama-continuity** 是一套用于 Codex 的中文 skill：依据已经采用的 AI 短剧成片，核对人物、空间、道具、灯光和真实尾帧，调整下一段提示词，并交付更新后的完整剧本 DOCX。

English: A Chinese-language Codex skill for checking accepted AI drama clips, maintaining scene continuity, and delivering a complete revised script with per-segment video prompts.

## 能做什么

- 从实际成片确认人物站位、左右手持物、手机朝向、灯光和道具状态。
- 将真实可见事实、画外未知项与保留的生成错误分开记录。
- 接上一段真正的最后解码帧，编写可直接提交视频模型的完整提示词。
- 只调整下一段及确实受影响的后续段，保留已采用成片与历史提示词。
- 直接更新原项目本地文件夹，图片未改时沿用已有图片，默认不制作 ZIP。
- 默认以**完整剧本 DOCX**作为主交付，逐段 TXT、上传说明和清单同步更新。

适用于分段生成的 AI 短剧、镜头衔接、人物与道具纠错。普通视频剪辑、单纯故事讨论不属于这套 skill 的主要工作。

## 安装

在支持技能安装的 Codex 环境中，可发送：

```text
使用 $skill-installer，从下面的 GitHub 目录安装 ai-drama-continuity：
https://github.com/LIUeliu/ai-drama-continuity-/tree/main/skills/ai-drama-continuity
如果已有同名技能，请先比较差异，不直接覆盖。
```

也可以下载仓库，将 `skills/ai-drama-continuity` 整个文件夹复制到个人技能目录：

- Windows：`%USERPROFILE%\.agents\skills\ai-drama-continuity`
- macOS / Linux：`~/.agents/skills/ai-drama-continuity`

`SKILL.md`、`agents/` 和 `references/` 必须保持相对位置。项目级安装可使用项目的 `.agents/skills/` 目录。不要重复安装同名副本；旧环境的技能目录应以该环境实际支持的位置为准。安装后若未显示，重新启动 Codex。

安装和调用方式参考 [OpenAI 官方技能文档](https://learn.chatgpt.com/docs/build-skills)。

## 第一次使用

准备已有完整剧本、参照图库及项目文件夹，让助手能访问。将下面示例中的项目路径替换为自己的路径：

```text
使用 $ai-drama-continuity。
项目目录：D:/AI-Drama/示例项目。
读取已有完整剧本、制作参数和参照清单，建立项目连续性记录。
保持已有设置，整理逐段完整提示词和按镜头上传文件夹。
主交付为完整剧本 DOCX，保存到原项目目录。
```

采用一段成片后，附上视频和尾帧，或给出助手可访问的本地路径：

```text
使用 $ai-drama-continuity。
第02集第02段，这版采用。
请核对成片和尾帧，调整下一段提示词并同步本地上传文件夹。
已完成内容不改，交付包含本次修订的完整剧本 DOCX。
```

详细步骤、可复制指令及常见问题见 [中文版使用教程](docs/使用教程.zh-CN.md)。

## 交付内容

| 交付物 | 用途 |
| --- | --- |
| 完整剧本 DOCX 新版本 | 包含项目全部既定剧本及逐段完整提示词，纳入本次修订 |
| 逐段 TXT 与汇总 | 方便复制提示词，与文档正文保持一致 |
| 按镜头上传文件夹 | 首帧、必要参照图、完整提示词、上传说明 |
| 项目连续性记录 | 保存采用依据、检查范围、已知状态、异常和后续衔接 |
| 采用存档与修改前备份 | 保留已完成内容和历史版本 |

用户明确只要建议或单段材料时，按用户指定范围交付。默认的完整文档交付不会要求重新生成未受影响内容。

## 制作参数和环境

画幅、段长、图片上限、片头和声音设置以项目或用户要求为准。技能中的 9:16、15秒、9张图是可覆盖的示例，不是所有视频模型的能力声明。

这是一套说明型 skill，不含视频生成服务、模型权重或自动上传程序。实际核对视频需要执行环境具备视频解码或播放能力；完整 DOCX 的制作与排版检查需要可用的文档工具。不能听音频或不能访问素材时，助手应说明实际检查范围。

视频生成由用户在所用平台完成；本 skill 不自动调用收费生成服务、发布作品或联络他人。

## 隐私与公开范围

仓库仅包含通用 skill、模板、README 和教程，不包含作者的项目文件、成片、人物参照图、聊天记录、账号配置或 API 密钥。无需将 AI 平台密码或密钥写入技能文件。

技能只能给执行助手提供工作说明，不能单独授予账号或本地文件访问权限。实际运行的访问范围由用户授权、工具连接和执行环境共同决定。公开仓库会显示仓库所有者的公开 GitHub 身份。

完整说明见 [隐私与发布范围](docs/隐私与发布范围.md)。提交问题时，请使用匿名化的文字示例，不上传私人素材或凭据。

## 仓库结构

```text
README.md
docs/
  使用教程.zh-CN.md
  隐私与发布范围.md
skills/
  ai-drama-continuity/
    SKILL.md
    agents/openai.yaml
    references/project-record.md
    references/prompt-and-delivery.md
```

修改工作流程时，以 `SKILL.md` 及其引用文档为准，并同步更新教程中的对应说明。
