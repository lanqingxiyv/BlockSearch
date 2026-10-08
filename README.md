[BlockSearch-README.md](https://github.com/user-attachments/files/33196292/BlockSearch-README.md)
# BlockSearch

**BlockSearch** is a client-side Fabric mod that highlights blocks, entities and world structures around you — no permissions required. Find ores, mobs, villages and fortresses instantly in survival.

BlockSearch 是一个纯客户端 Fabric 模组，不需要任何权限即可高亮周围的指定方块、生物和世界结构，帮你快速找矿物、找生物、找村庄和要塞。

- Minecraft **26.2 (Fabric)** · requires [Fabric API](https://modrinth.com/mod/fabric-api)
- Author / 作者：`_lan_qing_` 与 AI 共同完成 / with AI
- Download / 下载：请替换为你的 Modrinth 与 CurseForge 发布页链接

---

## Features 功能

- 方块搜索：高亮范围内所有指定方块（默认浅绿色框线）
- 生物发光：让指定生物发光高亮，支持持续监测
- 结构定位：半透明高亮整个世界结构，效果同 MiniHUD
- 自定义颜色：16 种内置色名 + #RRGGBB 十六进制
- 持续监测（keep）：自动刷新，新出现的方块/生物自动高亮
- 位置播报（broadcast）：keep 模式下可选播报位置
- 一键清除：/hunt clear 清除所有高亮和监测进程
- 多人可用：结构定位支持装有 Servux 的服务器

---

## Installation 安装

1. 安装 [Fabric Loader](https://fabricmc.net/use/) 和 [Fabric API](https://modrinth.com/mod/fabric-api)（对应 MC 26.2）
2. 下载本模组 jar（英文版或中文翻译版）
3. 放入 `.minecraft/mods` 文件夹
4. 启动游戏

> 纯客户端模组，不需要装在服务端。结构定位在多人服务器需要服主安装 [Servux](https://modrinth.com/mod/servux)（仅服务端）。

---

## Commands 指令

所有指令以 `/hunt` 开头，方块/生物/结构 id 均支持 Tab 自动补全。

| 分类 | 指令 | 作用 |
|---|---|---|
| 方块 | `/hunt block <id>` | 高亮指定方块 |
| 方块 | `/hunt block <id1> <id2>` | 同时高亮两种方块（可分别配色） |
| 方块 | `/hunt hand` | 高亮手持方块 |
| 方块 | `/hunt crosshair` | 高亮准星方块 |
| 生物 | `/hunt glow` | 开关全部生物发光 |
| 生物 | `/hunt glow <生物id>` | 目标生物发光 |
| 结构 | `/hunt structure <结构id>` | 结构半透明高亮 |
| 颜色 | `/hunt color block <颜色>` | 设置方块高亮颜色 |
| 颜色 | `/hunt color glow <颜色>` | 设置生物发光颜色 |
| 清除 | `/hunt clear` | 清除全部高亮与自动监测 |

### Block Search 方块搜索

```
/hunt block minecraft:diamond_ore
/hunt block minecraft:diamond_ore minecraft:emerald_ore
/hunt block minecraft:ancient_debris 16 4096
/hunt hand
/hunt crosshair
```

可选后缀：keep（每 2 秒自动刷新）、notkeep（关闭监测）、半径和上限（区块数与数量上限，默认渲染距离 / 4096）、颜色（自定义本次高亮颜色）。

高亮的方块被破坏或离开区域后，框线自动消失。

### Entity Glow 生物发光

```
/hunt glow
/hunt glow zombie
/hunt glow creeper and skeleton red blue
/hunt glow blaze keep broadcast
```

可选后缀：keep、notkeep、broadcast / notbroadcast、半径和上限、颜色。keep 开启后，范围内一旦生成目标生物会自动高亮并播报位置。

鸡骑士（Chicken Jockey）：输入 `chicken_jockey` 会同时高亮鸡和骑在身上的小僵尸；keep 开启后附近生成鸡骑士会自动高亮并播报位置。

### Structures 结构定位

```
/hunt structure minecraft:village_plains
/hunt structure minecraft:fortress
/hunt structure minecraft:ancient_city
/hunt structure minecraft:stronghold 16 64 keep
```

可选后缀：keep / notkeep、broadcast / notbroadcast、半径和上限。

单机直接可用；多人服务器需要服主安装 Servux mod，本模组会自动对接其结构数据通道。未安装时会提示结构显示不可用。

---

## Colors 颜色

支持 16 种内置色名和 #RRGGBB 十六进制：

- black
- dark_blue
- dark_green
- dark_aqua
- dark_red
- dark_purple
- gold
- gray
- dark_gray
- blue
- green
- aqua
- red
- light_purple
- yellow
- white

```
/hunt color block #ff8800
/hunt color glow aqua
/hunt block minecraft:coal_ore #00ff00
```

默认颜色：方块浅绿、生物白色。

---

## Clear 清除

```
/hunt clear
```

清除所有方块高亮、生物发光、结构框和 keep 自动监测进程。退出游戏、切换存档或离开服务器时也会自动清理。

---

## Versions 版本

- 英文原版：BlockSearch-版本号-26.2.jar
- 中文翻译版：BlockSearch-版本号-zh-26.2.jar（指令与提示全部汉化，方块/生物/结构 id 保持英文）

当前版本：1.5.15 (26.2)

---

## License 许可

MIT License — 详见 [LICENSE](LICENSE)。
