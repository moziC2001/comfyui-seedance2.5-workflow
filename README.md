# ComfyUI Seedance 2.5 工作流

一个可直接导入 ComfyUI 的 ByteDance Seedance 2.5 文生视频工作流：

`提示词 → Seedance 2.5（720p / 16:9 / 5 秒 / 原生音频）→ 保存 MP4`

> 这是 ComfyUI 内置的 Partner/API 节点工作流。它通过云端运行 Seedance 2.5，不需要下载本地模型权重，但需要 Comfy API Key 和足够的 Credits，执行会产生费用。

## 文件

- `workflows/seedance2.5_t2v.json`：ComfyUI 可视化工作流（主文件）

## 使用方法

1. 安装或更新到最新的 [ComfyUI](https://github.com/Comfy-Org/ComfyUI)。旧版本没有 Seedance 2.5 节点。
2. 在 ComfyUI 中登录 Comfy 账号，或在设置中配置 Comfy API Key。
3. 把 `workflows/seedance2.5_t2v.json` 拖进画布，或使用 **Workflow → Open** 导入。
4. 在 `ByteDance2TextToVideoNode` 中修改提示词、分辨率、比例、时长和音频选项。
5. 点击 **Run**。输出默认保存到 ComfyUI 的 `output/video/` 目录。

## 默认参数

| 参数 | 默认值 | 说明 |
|---|---:|---|
| 模型 | Seedance 2.5 | ByteDance Partner/API 模型 |
| 分辨率 | 720p | 先用较低成本验证流程 |
| 画幅 | 16:9 | 横屏视频 |
| 时长 | 5 秒 | 可在节点支持范围内调整 |
| 原生音频 | 开启 | 视频与音频一起生成 |
| 格式 | MP4 | 兼容性较好 |
| 水印 | 关闭 | 节点允许时关闭 |

## 提示词建议

按“场景 + 主体 + 动作 + 镜头 + 光线/风格 + 声音 + 禁止项”组织。例如：

```text
A cinematic tracking shot through a rain-soaked neon street in Hong Kong at night.
A woman in a red coat walks past glowing shop signs while reflections ripple across
the pavement. The camera follows smoothly at eye level, natural motion, realistic
lighting, subtle city ambience and rain sounds, no subtitles, no text overlays,
no black frames.
```

需要可重复结果时，把 seed 控制从 `randomize` 改为固定，并填写固定 seed。

## 图生视频与多参考

最新版 ComfyUI 还提供官方 Seedance 2.5 工作流：

- 图像/多模态参考：`ByteDance2ReferenceNodeV2`
- 首尾帧生成：`ByteDance2FirstLastFrameNode`
- 视频编辑：Seedance 2.5 Video Editing

这些模式需要额外的图片、视频或音频输入。可从 ComfyUI 的 **Workflow Templates** 搜索 `Seedance 2.5` 后直接打开官方模板。

## 常见问题

### 节点显示为红色或缺失

更新 ComfyUI 本体及前端后重启。这个工作流只使用 `comfy-core` 内置节点，不需要第三方 custom node。

### 提示未认证或余额不足

登录 Comfy 账号并配置 API Key/充值 Credits。不要把 API Key 写进工作流 JSON，也不要提交到 GitHub。

### 音频内容审核导致任务失败

先关闭 `generate_audio` 重试，再简化可能触发审核的对白或声音描述。

## 上游参考

- [ComfyUI 官方项目](https://github.com/Comfy-Org/ComfyUI)
- [ComfyUI 官方 Seedance 2.5 文生视频模板](https://github.com/Comfy-Org/workflow_templates/blob/main/templates/api_seedance2_5_t2v.json)
- [ComfyUI 官方工作流模板库](https://github.com/Comfy-Org/workflow_templates)

## License

MIT

