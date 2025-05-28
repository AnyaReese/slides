# 多幻灯片托管系统

这是一个基于GitHub Pages的多幻灯片托管系统，可以在一个网站上托管多个幻灯片，每个幻灯片都有独立的URL路径。

## 特性

- 多个幻灯片在同一个网站下托管
- 每个幻灯片有独立的URL路径（例如：`/sys/`、`/example/`）
- 美观的首页展示所有幻灯片
- 幻灯片索引页面（`/slides.html`）提供备用导航
- 自动部署到GitHub Pages
- 使用reveal-md创建精美的幻灯片

## 使用方法

### 添加新幻灯片

1. 在 `src/` 目录下创建新的 `.md` 文件
2. 文件名将成为访问路径（例如：`example.md` → `/example/`）
3. 文件的第一个标题将作为幻灯片的名称显示在导航中
4. 要手动在 workflow 中添加一个步骤，将所有幻灯片文件复制到 `_site/` 目录下。晚点理一下结构吧。

### 本地预览

```bash
make
```

### 构建和部署

```bash
# 构建所有幻灯片
make build

# 清理构建目录
make clean
```

GitHub Actions将在每次推送到main分支时自动构建和部署幻灯片。

## 目录结构

```
.
├── .github/workflows/   # GitHub Actions工作流配置
├── src/                 # 源代码目录
│   ├── index.html       # 自定义首页
│   ├── sys.md           # 系统设计幻灯片
│   ├── example.md       # 示例幻灯片
│   ├── *.md             # 其他幻灯片文件
│   ├── template.html    # 幻灯片HTML模板
│   ├── custom.css       # 自定义样式
│   ├── heti_worker.js   # 排版支持脚本
│   └── Makefile         # 构建脚本
└── README.md            # 本文件
```

## 网站结构

- `/` - 主页，提供所有幻灯片的导航
- `/sys/` - 计算机系统 3 Xpart 展示幻灯片
- `/arvr/` - 专题研讨展示幻灯片

## 技术栈

- reveal-md：用于从Markdown生成幻灯片
- GitHub Actions：用于自动构建和部署
- GitHub Pages：用于托管静态网站

## 许可

[MIT License](LICENSE) 