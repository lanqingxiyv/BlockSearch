[GitHub_README.md](https://github.com/user-attachments/files/33282359/GitHub_README.md)
# BlockSearch

一个 Minecraft **Fabric 客户端**模组，通过 `/hunt` 指令在游戏中高亮标记方块、生物、结构以及袭击敌人，支持颜色、范围、数量上限与持续追踪（keep）等自定义。

- **作者**：_lan_qing_（与 AI 共同完成）
- **适用版本**：Minecraft 26.2（Fabric）
- **模组 ID**：blocksearch
- **当前版本**：1.6.15-26.2
- **加载方式**：仅客户端（无需服务端安装，可进服务器游玩）

---

## ✨ 功能一览

### 方块高亮
- 按方块 ID、手持物品、准星所指三种方式寻找
- 支持同时高亮两种方块（可分别指定颜色）
- 支持自定义颜色、搜索半径（区块）、高亮数量上限
- `keep` 持续追踪（新出现的方块也会继续高亮）

```
/hunt block <方块ID> [半径] [上限] | [颜色]
/hunt block <方块ID1> <方块ID2> [颜色1 颜色2]
/hunt hand [半径] [上限] | [颜色]          （手持的方块）
/hunt crosshair [半径] [上限] | [颜色]      （准星所指的方块）
# 以上均可加 keep / notkeep，如：
/hunt block minecraft:diamond_ore keep
```

### 生物高亮
- 按生物 ID 寻找，支持同时高亮多种生物（可分别指定颜色）
- `keep` 跨波持续追踪，`broadcast` 每 10 秒播报剩余生物与坐标
- **鸡骑士**：可单独高亮鸡骑士及其身上的小僵尸，自动播报位置

```
/hunt glow all [半径] [上限]
/hunt glow <生物ID> [半径] [上限] [颜色] [keep|notkeep] [broadcast|notbroadcast]
/hunt glow <生物ID1> and <生物ID2> [颜色1 颜色2] [keep|notkeep] [broadcast|notbroadcast]
/hunt glow chicken_jockey [keep|notkeep] [broadcast|notbroadcast]
```

### 袭击高亮（1.6 新增）
- 打袭击时高亮所有袭击敌人（与敲钟标记的敌人一致）
- `keep` 一波结束后下一波敌人继续高亮
- `broadcast` 每 10 秒播报剩余敌人与坐标
- 袭击胜利后自动清除检测与高亮

```
/hunt glow raid [颜色] [半径] [上限] [keep|notkeep] [broadcast|notbroadcast]
```

### 结构显示（1.5 新增）
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

## 🎮 命令

所有命令以 `/hunt` 开头（客户端指令，无需权限）。

### 方块
```
/hunt block <方块ID> [半径] [上限]
/hunt block <方块ID> [颜色]
/hunt block <方块ID1> <方块ID2> [颜色1 颜色2]
/hunt block <方块ID1> <方块ID2> [半径] [上限]
/hunt block <方块ID> keep [半径] [上限] [颜色]
/hunt block <方块ID> notkeep
/hunt hand [半径] [上限]          （手持的方块）
/hunt hand [颜色]
/hunt hand keep [半径] [上限] [颜色]
/hunt hand notkeep
/hunt crosshair [半径] [上限]      （准星所指的方块）
/hunt crosshair [颜色]
/hunt crosshair keep [半径] [上限] [颜色]
/hunt crosshair notkeep
```

### 生物发光
```
/hunt glow                          （开关）
/hunt glow all [半径] [上限]
/hunt glow <生物ID> [半径] [上限] [颜色]
/hunt glow <生物ID> keep [半径] [上限] [颜色] [broadcast|notbroadcast]
/hunt glow <生物ID> notkeep
/hunt glow <生物ID1> and <生物ID2> [颜色1 颜色2] [keep|notkeep] [broadcast|notbroadcast]
/hunt glow chicken_jockey [keep|notkeep] [broadcast|notbroadcast]
/hunt glow raid [颜色] [半径] [上限] [keep|notkeep] [broadcast|notbroadcast]
```

### 颜色
```
/hunt color block <颜色|#rrggbb>    （方块高亮颜色）
/hunt color glow <颜色|#rrggbb>     （生物发光颜色）
```

### 结构
```
/hunt structure <结构ID> [半径] [上限] [keep|notkeep] [broadcast|notbroadcast]
```

### 清除
```
/hunt clear                          （清除所有高亮与 keep 进程）
```

### 参数说明
| 参数 | 说明 |
|---|---|
| `<方块ID>` | 方块命名空间 ID，如 `minecraft:diamond_ore` |
| `<生物ID>` | 生物命名空间 ID，如 `minecraft:creeper` |
| `<结构ID>` | 结构命名空间 ID，如 `minecraft:village_plains` |
| `[半径]` | 搜索半径，单位区块，默认 = 玩家视野区块 |
| `[上限]` | 高亮数量上限，默认 4096 |
| `[颜色]` | 16 色名（red, blue, green…）或 `#rrggbb` |
| `keep / notkeep` | 持续追踪 / 只检测当前一批 |
| `broadcast / notbroadcast` | 每 10 秒播报位置 / 关闭播报 |

可用颜色：`black, dark_blue, dark_green, dark_aqua, dark_red, dark_purple, gold, gray, dark_gray, blue, green, aqua, red, light_purple, yellow, white`

---

## 🚀 安装

1. 安装对应版本的 **Fabric Loader**（Minecraft 26.2）
2. 将 `BlockSearch-1.6.15-26.2.jar` 放入 `.minecraft/mods` 文件夹
3. 启动游戏即可，无需服务端安装

> 结构显示与袭击高亮依赖单机世界数据，单人世界可用；进入他人服务器时这两项功能不可用（其余功能正常）。

---

## 📝 更新日志

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
