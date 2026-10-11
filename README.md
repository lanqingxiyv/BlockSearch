# BlockSearch

一个 Minecraft **Fabric 客户端**模组，通过 `/hunt` 指令在游戏中高亮寻找方块、生物、结构以及袭击敌人，支持颜色、范围、数量上限与持续追踪。

- **作者**：_lan_qing_（与 AI 共同完成）
- **适用版本**：Minecraft 26.2（Fabric）
- **当前版本**：1.6.19-26.2
- **加载方式**：仅客户端（无需服务端安装，可进服务器）

## 功能特色

### 方块高亮
- 按方块 ID、手持物品、准星所指三种方式寻找
- 同时高亮两种方块，可分别指定颜色
- 自定义颜色、搜索半径（区块）、高亮上限（默认 4096）
- `keep` 持续追踪；方块被破坏后高亮自动消失

```
/hunt block <方块ID> [半径] [上限] | [颜色]
/hunt block <方块ID1> <方块ID2> [颜色1 颜色2]
/hunt hand [半径] [上限] | [颜色]        （手持的方块）
/hunt crosshair [半径] [上限] | [颜色]    （准星所指的方块）
/hunt block <方块ID> keep / notkeep        （持续追踪 / 停止）
```

### 生物高亮
- 按生物 ID 寻找，多种生物可同时高亮（`and` 连接，分别配色）
- `keep` 持续追踪，`broadcast` 新出现的目标生物即时播报位置
- 特殊支持鸡骑士：连同身上的小僵尸一起高亮，keep 时自动播报位置

```
/hunt glow all [半径] [上限]
/hunt glow <生物ID> [半径] [上限] [颜色] [keep|notkeep] [broadcast|notbroadcast]
/hunt glow <生物ID1> and <生物ID2> [颜色1 颜色2] [keep|notkeep] [broadcast|notbroadcast]
/hunt glow chicken_jockey [keep|notkeep] [broadcast|notbroadcast]
```

### 袭击高亮（1.6 新增，单人与服务器均可用）
- 打袭击时高亮袭击敌人：单人精确匹配袭击成员（与敲钟标记一致），服务器近似匹配周围 Raider 类型敌人
- 仅袭击进行中或有袭击之兆（Bad Omen）时生效
- `keep` 一波结束后下一波敌人继续高亮
- `broadcast` 每 15 秒播报剩余敌人与坐标；下一波敌人出现时立即播报
- 单人播报附带波数（第 X/Y 波，还剩 Z 波）
- 走出袭击范围高亮自动暂清，返回范围自动恢复
- 袭击胜利或失败后自动清除检测与高亮

```
/hunt glow raid [颜色] [半径] [上限] [keep|notkeep] [broadcast|notbroadcast]
```

### 结构显示（1.5 新增，仅单人可用）
- MiniHUD 风格半透明高亮整个结构（主体与内部区块分别显示）
- 支持村庄、下界要塞、古城等全部原版结构

```
/hunt structure <结构ID> [半径] [上限] [keep|notkeep] [broadcast|notbroadcast]
```

### 颜色自定义
- 支持 16 色名与 `#rrggbb` 十六进制

```
/hunt color block <颜色|#rrggbb>    （方块高亮颜色）
/hunt color glow <颜色|#rrggbb>     （生物发光颜色）
/hunt clear                          （清除全部高亮）
```

## 命令总览

```
/hunt block <方块ID> [半径] [上限]
/hunt block <方块ID> [颜色]
/hunt block <方块ID1> <方块ID2> [颜色1 颜色2]
/hunt block <方块ID> keep [半径] [上限] [颜色]
/hunt hand [半径] [上限] | [颜色] [+ keep/notkeep]
/hunt crosshair [半径] [上限] | [颜色] [+ keep/notkeep]
/hunt glow [半径] [上限]            开启/关闭
/hunt glow all [半径] [上限]
/hunt glow <生物ID> [半径] [上限] [颜色] [keep|notkeep] [broadcast|notbroadcast]
/hunt glow <生物ID1> and <生物ID2> [颜色1 颜色2] [keep|notkeep] [broadcast|notbroadcast]
/hunt glow chicken_jockey [keep|notkeep] [broadcast|notbroadcast]
/hunt glow raid [颜色] [半径] [上限] [keep|notkeep] [broadcast|notbroadcast]
/hunt structure <结构ID> [半径] [上限] [keep|notkeep] [broadcast|notbroadcast]
/hunt color block <颜色|#rrggbb>
/hunt color glow <颜色|#rrggbb>
/hunt clear
```

**参数**：半径以区块为单位（默认玩家视野区块）；上限默认 4096；颜色支持 16 色名（black, dark_blue, dark_green, dark_aqua, dark_red, dark_purple, gold, gray, dark_gray, blue, green, aqua, red, light_purple, yellow, white）与 `#rrggbb`。

## 安装

1. 安装对应版本的 Fabric Loader（Minecraft 26.2）
2. 将 `BlockSearch-1.6.19-26.2.jar` 放入 `.minecraft/mods`
3. 启动游戏即可使用，无需服务端安装

> 提示：结构显示依赖单机世界数据，仅单人世界可用；袭击高亮单人与服务器均可用（服务器为近似检测），其余功能全部正常。

## 许可

MIT 许可证，作者 `_lan_qing_`。
