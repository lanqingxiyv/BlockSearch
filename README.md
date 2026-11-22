[BlockSearch-GitHub-README.md](https://github.com/user-attachments/files/35225756/BlockSearch-GitHub-README.md)
# BlockSearch

通过 /hunt 指令在游戏中高亮寻找方块、生物、结构以及袭击敌人，支持颜色、范围、数量上限与持续追踪。

- **作者**：&#95;lan&#95;qing&#95;（与 AI 共同完成）
- **适用版本**：Minecraft 26.2（Fabric）
- **模组 ID**：blocksearch
- **当前版本**：1.8.7.1-26.2
- **加载方式**：仅客户端（无需服务端安装，可进服务器游玩）

---

## 零级指令：/hunt

 /hunt 是根指令，单独输入只提示用法，不做任何事。它是唯一固定的一层：调用时先写它，再写一条**一级指令**（功能 + 目标），后面可以继续嵌套若干**二级指令**（参数）。

```
/hunt
```

Tab 补全逐级向下：一级补功能与目标，二级补参数名，之后补颜色与 ID。ID 可写 minecraft:diamond_ore，也可省略命名空间写 diamond_ore。

---

## 一级指令

一级指令是“功能 + 目标”的整体，写到目标就算完整，可以不接任何二级指令。每条一级指令能跟的二级指令不同，下面逐条列出。

### 方块高亮：block / hand / crosshair

```
/hunt block <方块ID>     按方块 ID 找
/hunt hand               找你手上拿着的方块
/hunt crosshair          找你准星指着的方块
```

可用二级指令：and、radius、count、color、once、broadcast。

```
/hunt block minecraft:diamond_ore radius 16 count 4096 color aqua once
/hunt block minecraft:diamond_ore and minecraft:emerald_ore color aqua green
/hunt block minecraft:ancient_debris radius 32 broadcast
/hunt hand radius 16 color gold
/hunt crosshair once
```

### 生物高亮：glow

```
/hunt glow <生物ID>             按生物 ID 找
/hunt glow all                  高亮范围内全部生物
```

all 必须单独使用；chicken_jockey 是新增的可选发光目标。

可用二级指令：and、radius、count、color、once、broadcast。

```
/hunt glow all radius 8
/hunt glow minecraft:creeper and minecraft:skeleton color green white broadcast
/hunt glow chicken_jockey color red broadcast
```

### 结构显示：structure

```
/hunt structure <结构ID>
```

可用二级指令：and、radius、color、once、broadcast。

```
/hunt structure minecraft:village_plains
/hunt structure minecraft:fortress and minecraft:bastion_remnant color red blue radius 32
```

### 袭击高亮：raid

```
/hunt raid
```

可用二级指令：color、once、broadcast。

```
/hunt raid color red broadcast
/hunt raid once
```

### 区域高亮：region

```
/hunt region box <x1> <y1> <z1> [<x2> <y2> <z2>]
/hunt region sphere <x> <y> <z> [半径]
```

可用二级指令：只有 color，写在坐标之后。坐标支持 ~ 相对；方体单点即 1×1×1，球形不给半径即单点；边长上限 512、球半径上限 256、单次最多渲染 8192 个方块。

```
/hunt region box ~ ~ ~ ~10 ~5 ~10 color red
/hunt region sphere 0 70 0 32 color #ff8800
```

### 清除：clear

```
/hunt clear              清除全部
/hunt clear block        只清方块高亮
/hunt clear glow         只清生物发光
/hunt clear structure    只清结构框
/hunt clear raid         只清袭击高亮
/hunt clear region       只清区域框
```

不接任何二级指令。

---

## 二级指令说明

| 二级指令 | 作用 |
|---|---|
| and <ID> | 追加一个目标，最多 16 个 |
| radius N | 搜索半径（区块），1–256，默认取当前有效渲染距离 |
| count N | 高亮上限，1–10000，默认 4096 |
| color C [C2 …] | 颜色，16 色名或 #rrggbb，多目标按顺序配色 |
| once | 只显示本次结果，不每秒刷新 |
| broadcast | 首次立即播报，之后每 15 秒播报最近 5 个坐标 |

**嵌套规则**：写在目标之后、顺序随意、可任意组合；radius / count / once / broadcast 不能重复写，and 最多连写 16 次，color 可连写按目标顺序配色。默认每秒刷新一次，方块被破坏或走出范围后高亮自动消失，加 once 则定格。

---

## 颜色

16 色名：black dark_blue dark_green dark_aqua dark_red dark_purple gold gray dark_gray blue green aqua red light_purple yellow white；也支持 #rrggbb。

默认方块浅绿、生物白色、区域绿色。退出游戏、切换存档或离开服务器时自动清理。

---

## 🔗 联动

投影打印机（投影打印机五改）是作者基于 Litematica Printer 改写的 Fabric 客户端模组，载入投影后自动帮你摆方块、挖掘和去皮，按区域排队执行。它可以拿本模组的高亮结果当作业范围：在打印机的去皮等模块里把选区类型切成「BlockSearch 高亮」，就会直接处理你搜出来的那些方块，不用手动圈选区。两个模组都是纯客户端，放进同一个 .minecraft/mods 即可联动。获取模组请私信此账号或前往https://b23.tv/wDhQ6G5 私信

---

## 发光与渲染逻辑

方块高亮：

- 64 格内逐块画线框，64 格外按 2×2 取样；单区块最多 512 个、单目标 4096 个，超过 count 只留最近的
- 线框是双层：实色层 + 55% 透明的加粗层；512 格外不再绘制
- 128 格内实色满亮，128 到 512 格透明度线性降到 0.80；线宽 96 格内为 2.5，之后随距离加粗到 4.2
- 被六个同种方块包住的内部块：64 格内不画，之外按坐标奇偶隔一画，总量超过 6000 停止；标记总数超过 6000 时，128 格外只保留虚线圈

生物高亮：

- 用原版发光标记逐实体上色，不是画框
- 半径按区块的方形范围筛选，最近优先，超过 count 截断
- 离开范围不会立刻熄灭，直到实体死亡、所在区块卸载或 /hunt clear
- 鸡骑士判定为“骑着幼年僵尸的鸡”，鸡和身上的小僵尸一起上色

结构显示：

- tweakeroo 风格半透明面 + 描边，外层合并大框 + 内层各区块小框（最多两层），只在当前维度渲染

区域高亮：

- 区域内逐块画线框，单次最多 8192 个方块，超出只显示前 8192 个

## 📦 安装

1. 安装 Fabric Loader（Minecraft 26.2）
2. 下载 jar 放入 .minecraft/mods
3. 启动游戏，无需服务端安装

> 结构显示单人与多人服务器均可用（多人模式为客户端扫描已加载区块 + 方块指纹匹配）；袭击高亮单人与服务器均可用（服务器为近似检测）。其余功能全部正常。

## 📄 许可

MIT License，作者 &#95;lan&#95;qing&#95;。
