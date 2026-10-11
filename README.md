[GitHub_README（1.6.19）.md](https://github.com/user-attachments/files/33297701/GitHub_README.1.6.19.md)
# BlockSearch

一个 Minecraft **Fabric 客户端**模组，通过 `/hunt` 指令在游戏中高亮标记方块、生物、结构以及袭击敌人，支持颜色、范围、数量上限与持续追踪（keep）等自定义。

- **作者**：_lan_qing_（与 AI 共同完成）
- **适用版本**：Minecraft 26.2（Fabric）
- **模组 ID**：blocksearch
- **当前版本**：1.6.19-26.2
- **加载方式**：仅客户端（无需服务端安装，可进服务器游玩）

---

## ✨ 功能一览

### 方块高亮
- 按方块 ID、手持物品、准星所指三种方式寻找
- 支持同时高亮两种方块（可分别指定颜色）
- 支持自定义颜色、搜索半径（区块）、高亮数量上限
- `keep` 持续追踪（新出现的方块也会继续高亮，被破坏的方块高亮自动消失）

```
/hunt block <方块ID> [半径] [上限] | [颜色]
/hunt block <方块ID1> <方块ID2> [颜色1 颜色2]
/hunt hand [半径] [上限] | [颜色]          （手持的方块）
/hunt crosshair [半径] [上限] | [颜色]      （准星所指的方块）
# 以上均可加 keep / notkeep，如：
/hunt block minecraft:diamond_ore keep
```

### 生物高亮
- 按生物 ID 寻找，支持同时高亮多种生物（`and` 连接，可分别指定颜色）
- `keep` 持续追踪；`broadcast` 新出现的目标生物即时播报位置
- **鸡骑士**：可单独高亮鸡骑士及其身上的小僵尸，keep 时自动播报位置（不受播报开关影响）

```
/hunt glow all [半径] [上限]
/hunt glow <生物ID> [半径] [上限] [颜色] [keep|notkeep] [broadcast|notbroadcast]
/hunt glow <生物ID1> and <生物ID2> [颜色1 颜色2] [keep|notkeep] [broadcast|notbroadcast]
/hunt glow chicken_jockey [keep|notkeep] [broadcast|notbroadcast]
```

### 袭击高亮（1.6 新增，单人与服务器均可用）
- 打袭击时高亮袭击敌人：单人精确匹配袭击成员（与敲钟标记一致），服务器近似匹配周围 Raider 类型敌人
- `keep` 一波结束后下一波敌人继续高亮
- `broadcast` 每 15 秒播报剩余敌人与坐标；下一波敌人出现时立即播报
- 单人播报附带波数：`第 X/Y 波（还剩 Z 波）`
- 有袭击之兆（Bad Omen）或袭击进行中时指令生效
- 走出袭击范围高亮自动暂清，返回范围自动恢复
- 袭击胜利或失败后自动清除检测与高亮

```
/hunt glow raid [颜色] [半径] [上限] [keep|notkeep] [broadcast|notbroadcast]
```

### 结构显示（1.5 新增，仅单人可用）
- MiniHUD 风格半透明高亮整个结构（主体与内部区块分别框出）
- 支持村庄、下界要塞、古城等全部原版结构

```
/hunt structure <结构ID> [半径] [上限] [keep|notkeep] [broadcast|notbroadcast]
```

### 颜色
- 支持 16 色名与 `#rrggbb` 十六进制

```
/hunt color block <颜色|#rrggbb>    （方块高亮颜色）
/hunt color glow <颜色|#rrggbb>     （生物发光颜色）
```

### 清除
- 一键清除所有高亮与 keep 进程

```
/hunt clear
```

### 其他
- 默认搜索半径 = 玩家视野区块（服务器为服务器默认视野）
- 默认高亮上限 4096，超出时提示
- 被破坏/消失的方块自动移除高亮

---

## 🚀 安装

1. 安装对应版本的 **Fabric Loader**（Minecraft 26.2）
2. 将 `BlockSearch-1.6.19-26.2.jar` 放入 `.minecraft/mods` 文件夹
3. 启动游戏即可，无需服务端安装

> 结构显示依赖单机世界数据，仅单人世界可用；袭击高亮单人与服务器均可用（服务器为近似检测，其余功能全部正常）。

---

## 📝 更新日志

### v1.6.19
- 袭击失败后自动清除检测（单人立即判定，服务器 20 秒判定）

### v1.6.18
- 袭击播报间隔调整为 15 秒
- 有袭击之兆（Bad Omen）时袭击指令生效
- 走出袭击范围不再关闭检测，返回范围自动恢复高亮

### v1.6.17
- 修复剩余 1~2 个敌人时进度条改名导致误判袭击结束
- 单人播报附带波数（第 X/Y 波，还剩 Z 波）

### v1.6.16
- 袭击高亮支持服务器/多人（客户端检测袭击进度条 + 扫描 Raider 敌人近似高亮）
- 下一波敌人出现时立即播报

### v1.6.15
- 新增袭击高亮 `/hunt glow raid`
- 不带 keep 只检测当前一波敌人，带 keep 持续追踪后续波次
- 袭击胜利自动清除检测与高亮
- 修复首次使用指令不发光/闪一下就消失的问题
- 修复第二次使用指令导致崩溃的问题
- 清理调试代码，保留诊断日志

### v1.5
- 新增结构显示 `/hunt structure <结构ID>`
- 新增方块/生物 keep 追踪、播报、颜色自定义、多目标高亮

---

## 📜 许可

仅客户端模组，遵循 MIT 许可证。作者 `_lan_qing_`。
