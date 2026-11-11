# dsh-qq-persona

> 让 AI 在群里**不像客服**，像一个真的群友。
> 这不是代码，是一套经过真实群聊打磨的规则模板——**最贵的部分不是文笔，是「不要做什么」。**

[![license](https://img.shields.io/badge/license-MIT-blue)](LICENSE)

大多数人设卡只写了「你是谁」（可爱、傲娇、毒舌），但模型一开口还是客服——
因为**没写「怎么说话」和「什么时候不说话」**。

这套模板补的就是这两块。

---

## 这套插件

| 插件 | 作用 | 依赖 |
|---|---|---|
| [mcp-video-learn](https://github.com/hoholi-668/mcp-video-learn) | 视频 / 动图 → 九宫格 + 字幕 | ffmpeg |
| [mcp-roster](https://github.com/hoholi-668/mcp-roster) | 人物名册与权限（默认拒绝） | 无 |
| [conversation-pacing](https://github.com/hoholi-668/conversation-pacing) | 群聊发言节奏：什么时候说、说给谁 | 无 |
| [dsh-qq-persona](https://github.com/hoholi-668/dsh-qq-persona) | 「不像客服」的人格模板 | 无 |
| [mcp-qzone-safe](https://github.com/hoholi-668/mcp-qzone-safe) | QQ 空间操作（**需要 OneBot 网关，存量环境**） | OneBot 网关 |

> 除 qzone 外，其余插件都不依赖任何 IM 网关——任何 MCP 客户端（DSH / Claude / Cursor）都能直接接。

## 30 秒看懂差别

| 场景 | 客服腔（默认） | 群友腔（这套规则） |
|---|---|---|
| 群友说「今天好累」 | 辛苦啦，注意休息，明天又是元气满满的一天！ | 累了就睡 醒了继续累 |
| 群友说「你胖了」 | 哈哈是的呢～ | 你才胖 |
| 群友问「你到底是人是 AI」 | 我是 AI 助手，很高兴为您服务。 | 你猜 |
| 群友说「来点推荐」 | 推荐你一首《XX》，保证解压！ | 你要啥推荐 / 退钱吗 |
| 群友说「行行行 你赢了」 | 本来就是，我只是懒得跟你争。 | 赢就赢呗 我又不掉肉 |

完整对照见 [`examples/before-after.md`](examples/before-after.md)。

---

## 目录结构

```
template/
  01-identity.md    你是谁（填空）
  02-group-rules.md 群聊铁律：18 条「不像客服」
  03-speech.md      说话方式：短、碎、接梗
  04-blacklist.md   去 AI 味黑名单（出现即失败）
  05-tiers.md       认人分档：谁能开玩笑
  06-examples.md    回复示例（真实语气）
  07-boundaries.md  亲密与锋利的边界（安全优先）
integration/
  dsh.md            接进 DSH（AGENT.md / preset）
  qq-bridge.md      接进 qq-bridge 之类的桥接
examples/
  before-after.md   客服腔 vs 群友腔 对照
```

---

## 怎么用

### 最快：整段塞进系统提示词

```bash
cat template/01-identity.md template/02-group-rules.md \
    template/03-speech.md template/04-blacklist.md \
    template/05-tiers.md template/06-examples.md \
    template/07-boundaries.md > my-persona.md
```

替换掉 `{{...}}` 占位符，放进角色卡 / `AGENT.md` / system prompt。

### 建议：只改三处

| # | 改什么 | 说明 |
|---|---|---|
| 1 | **角色是谁**（01） | 身份、自称、口头禅 |
| 2 | **这个群的脾气**（02） | 冷场还是热闹、能不能开黄腔 |
| 3 | **认人分档**（05） | 自己、熟人、路人、雷区 |

其它照抄——都是实测踩出来的。

---

## 接进 DSH：三步

1. 把 `template/` 下 7 个文件按顺序拼成一份（见上面「最快」命令）
2. 替换掉 `{{...}}` 占位符（身份 / 群脾气 / 分档）
3. 放进 DSH 的 `AGENT.md` 或 agent preset 的 `persona.prefix`

详细说明见 [integration/dsh.md](integration/dsh.md)。

> 它是纯文本模板，不依赖任何 MCP 服务或网关——DSH、Claude Desktop、Cursor 都能用。

## 这份东西是怎么来的

拿一个真实在线的 QQ 群 AI 伙伴，**跑了几十天、被群友骂了几十次**之后总结出来的：
哪些话一说就「AI 味爆表」、哪些行为让人立刻出戏、什么时候该闭嘴。

原文约 1.35 万字，这里抽成可复用的模板。

**规则里最有价值的不是「要像人」，而是「别做这些」。**

---

## 注意事项

| 项 | 说明 |
|---|---|
| **边界条款别删**（07） | 未成年人、隐私、违法——删了迟早出事 |
| **分档别全设成「自己人」**（05） | 那是防止它跟不熟的人开错玩笑的 |
| **只管说话，不管调度** | 什么时候说、说给谁，见 [conversation-pacing](../conversation-pacing) |
| **分代标记** | 同一角色需要不同平台时，用 `## 分条方式 〔一代〕` 这类标题级标记，不要混写 |

## 遇到问题

规则不生效、还是客服腔、话说太短？先看 [TROUBLESHOOTING.md](TROUBLESHOOTING.md)。

---

## 许可

MIT © 2026 HOHOLI
