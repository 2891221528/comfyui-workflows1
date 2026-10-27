# 装回本机 ComfyUI

假设 ComfyUI 根目录为 `D:\comfyui\ComfyUI_windows_portable-G313`（下称 `<COMFY>`）。

| 仓库文件 | 目标位置 |
|---|---|
| `workflows/*.json` | `<COMFY>\ComfyUI\user\default\workflows\` |
| `dictionaries/*.txt` | `<COMFY>\ComfyUI\custom_nodes\ComfyUI-Easy-Use\wildcards\` |
| `autocomplete/autocomplete.txt` | `<COMFY>\ComfyUI\custom_nodes\ComfyUI-Custom-Scripts\user\autocomplete.txt` |

三条对应命令（Git Bash，路径按需改）：

```bash
COMFY=/d/comfyui/ComfyUI_windows_portable-G313

cp workflows/*.json "$COMFY/ComfyUI/user/default/workflows/"
cp dictionaries/*.txt "$COMFY/ComfyUI/custom_nodes/ComfyUI-Easy-Use/wildcards/"
cp autocomplete/autocomplete.txt "$COMFY/ComfyUI/custom_nodes/ComfyUI-Custom-Scripts/user/"
```

## 生效方式

| 内容 | 怎么生效 |
|---|---|
| 工作流 json | 直接打开 ComfyUI，侧边栏就有，或者把 json 拖进画布 |
| 词典 txt | **重启 ComfyUI**（Easy-Use 只在启动时扫描一次词典目录） |
| 词库 txt | **刷新页面 F5**（前端每次加载拉一次） |

## 依赖

工作流用到以下自定义节点，缺了会报红框：

- `ComfyUI-Easy-Use` —— `easy wildcards` 词典节点
- `rgthree-comfy` —— `Power Lora Loader`
- `ComfyUI-Custom-Scripts` —— 标签自动补全（词库的宿主）

三个都能在 ComfyUI-Manager 里直接装。
