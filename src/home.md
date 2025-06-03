# 幻灯片主页

## 欢迎使用多幻灯片托管系统

这是一个可以托管多个幻灯片的GitHub Pages网站。

每个幻灯片都有自己独立的URL路径。

---

## 如何导航

- 可以通过 `/slides.html` 页面查看所有幻灯片
- 每个幻灯片都在独立的子路径下访问
- 例如：`/example/` 访问示例幻灯片

---

## 如何添加新幻灯片

1. 在 `src/slides/` 目录下创建新的 `.md` 文件
2. 文件名将成为访问路径
3. 使用 `make build` 构建整个网站
4. 使用 `make live-文件名` 预览特定幻灯片

---

## 现有幻灯片

- 主页幻灯片：`/`
- 示例幻灯片：`/example/`
- 更多幻灯片将在添加后显示在这里

---

## 感谢使用！

这个系统由 reveal-md 和 GitHub Actions 提供支持。 template 来源@TonyCrane: https://github.com/TonyCrane/slide-template/