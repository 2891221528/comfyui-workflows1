# ComfyUI 工作流库

本地 ComfyUI（Windows Portable）用的工作流与提示词词典备份，随用随拉。

## 目录

```
workflows/      ComfyUI 工作流（UI 格式 json，直接双击打开）
dictionaries/   Easy-Use 通配符词典（__nsfw__ 这类标记的词源）
autocomplete/   pysssss 标签自动补全词库（打字弹标签）
```

## workflows/▶▷文生图+图生图-NSFW词典版.json

一套工作流里同时带文生图和图生图两路，共用模型与提示词。

| 分组 | 内容 |
|---|---|
| ① 模型 + 多 LoRA | `CheckpointLoaderSimple` + `Power Lora Loader (rgthree)`，点「+ Add Lora」加行，左侧圆点开关，每行 model / clip 两个强度 |
| ② 提示词 | `easy wildcards` 词典节点，支持 `__nsfw__` 随机展开、`{a\|b\|c}` 行内随机、`<lora:名字:0.8>` 插 LoRA |
| ③ 文生图 | EmptyLatentImage 832×1216 → KSampler（28 步 / euler_ancestral / normal / cfg 5）→ VAEDecode → 存 `output/t2i/` |
| ④ 图生图 | LoadImage → VAEEncode → KSampler（denoise 0.55）→ VAEDecode → 存 `output/i2i/` |

改图生图的力度就调 denoise：0.35 微调、0.55 中等、0.7 大改。

默认模型 `waiIllustriousSDXL_v140.safetensors`，换成 NoobAI-XL 或其他 Illustrious 系模型也行，节点里直接选。

## dictionaries/

Easy-Use 的 `easy wildcards` 读的词源，一行一个组合，随机取一行。

| 文件 | 标记 | 内容 |
|---|---|---|
| `nsfw.txt` | `__nsfw__` | 16 组状态/场景组合 |
| `nsfw_pose.txt` | `__nsfw_pose__` | 16 组姿势/视角 |
| `nsfw_cloth.txt` | `__nsfw_cloth__` | 12 组服装状态 |

**注意：文件里不能写注释行**，解析器会把 `#` 开头的行也当成词条抽中。加词就加行，加完重启 ComfyUI 生效（词典只在启动时加载一次）。

## autocomplete/

`autocomplete.txt` 是 pysssss Text Autocomplete 的词库，143,200 条 danbooru 标签，其中 10,554 条带中文别名。

格式：`标签,分类,权重,"别名1,别名2"`

- 下划线已统一换成空格（`long hair` 而不是 `long_hair`）
- 权重 = danbooru 使用次数，决定候选排序
- 已排除 loli / shota / underage 等涉及未成年的词条

改完按 F5 刷新页面即可，不用重启。**别用 ComfyUI 设置里的编辑框打开它**（3.5MB 会卡），直接改文件。

## 数据来源

- 标签主库：[DominikDoom/a1111-sd-webui-tagcomplete](https://github.com/DominikDoom/a1111-sd-webui-tagcomplete) 的 `tags/danbooru.csv`
- 中文翻译：[byzod/a1111-sd-webui-tagcomplete-CN](https://github.com/byzod/a1111-sd-webui-tagcomplete-CN) 的 `Tags-zh-full-pack.csv`

两个都是开源项目的数据集，此处仅做合并与格式转换。

## 安装位置

见 [INSTALL.md](INSTALL.md)。
