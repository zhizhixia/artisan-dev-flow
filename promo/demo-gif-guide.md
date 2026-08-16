# 演示 GIF 录制指南（30-60 秒）

目标：展示 Enough 在“新需求 → 复用决策”第一回合的行为。

## 建议场景（推荐第一条）

1. 在 Codex/Claude Code 中新建会话
2. 输入："我想做一个 Windows 本地 RSS 阅读器：多源订阅、关键词过滤、定时刷新"
3. 展示 Enough 的输出：候选表 + 证据等级（E1/E2/E3）+ “直接使用 RSS Guard”的推荐 + 下一步
4. 收尾画面：README 中的五道门禁图或仓库首页

## 录制工具（Windows）

- 方案 A：ScreenToGif（免费开源，https://www.screentogif.com）—— 录制后直接导出 GIF
- 方案 B：OBS Studio 录屏 + ffmpeg 转 GIF

## 转 GIF 命令（如用 ffmpeg）

```bash
ffmpeg -i demo.mp4 -vf "fps=10,scale=1280:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" -loop 0 demo.gif
```

## 完成后

1. 把 GIF 命名为 `docs/demo.gif` 放入仓库（或 assets/）
2. README 顶部加：

```markdown
![Enough 演示](docs/demo.gif)
```

3. 提交并推送，社区帖子（中文首发文 + Show HN）里也引用同一张 GIF