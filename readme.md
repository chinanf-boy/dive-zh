# wagoodman/dive [![explain]][source] [![translate-svg]][translate-list]

<!-- [![size-img]][size] -->

[explain]: http://llever.com/explain.svg
[source]: https://github.com/chinanf-boy/Source-Explain
[translate-svg]: http://llever.com/translate.svg
[translate-list]: https://github.com/chinanf-boy/chinese-translate-list
[size-img]: https://packagephobia.now.sh/badge?p=Name
[size]: https://packagephobia.now.sh/result?p=Name

「 **用于探索 docker 镜像,图层内容以及发现缩小 Docker 镜像大小的方法的工具.** 」

[中文](./readme.md) | [english](https://github.com/wagoodman/dive)

---

## 校对 ✅

<!-- doc-templite START generated -->
<!-- repo = 'wagoodman/dive' -->
<!-- commit = 'd9ec426300be6c96bab5f2299ff4a68bece79ba4' -->
<!-- time = '2018-11-25' -->

| 翻译的原文 | 与日期        | 最新更新 | 更多                       |
| ---------- | ------------- | -------- | -------------------------- |
| [commit]   | ⏰ 2018-11-25 | ![last]  | [中文翻译][translate-list] |

[last]: https://img.shields.io/github/last-commit/wagoodman/dive.svg
[commit]: https://github.com/wagoodman/dive/tree/d9ec426300be6c96bab5f2299ff4a68bece79ba4

<!-- doc-templite END generated -->

### 贡献

欢迎 👏 勘误/校对/更新贡献 😊 [具体贡献请看](https://github.com/chinanf-boy/chinese-translate-list#贡献)

## 生活

[help me live , live need money 💰](https://github.com/chinanf-boy/live-need-money)

---

### 目录

<!-- START doctoc -->
<!-- END doctoc -->

# dive

[![Go Report Card](https://goreportcard.com/badge/github.com/wagoodman/dive)](https://goreportcard.com/report/github.com/wagoodman/dive)

**用于探索 docker 镜像,图层内容以及发现缩小 Docker 镜像大小的方法的工具.**

![Image](https://github.com/wagoodman/dive/blob/master/.data/demo.gif?raw=true)

要分析 Docker 镜像,只需带上镜像的 tag/id/digest， 运行 dive:

```bash
dive <your-image-tag>
```

或者如果你想建立你的镜像，那么可直接分析它:

```bash
dive build -t <some-tag> .
```

**软件还处于 beta 阶段!** _如果您想要新功能或发现错误,请随时提交问题:)_

## 基本功能

**显示，按层细分的 Docker 镜像内容**

当您在左侧选择一个图层时，将显示该图层的内容，及在右侧，显示所有先前图层。此外,您可以使用箭头按键，(想去哪就去哪)浏览文件树。

**指出每层中发生了哪些变化**

已更改,已修改,添加或删除的文件，在文件树中都有指示。可以调整此值以显示特定图层的更改,或直到集合此图层的更改。

**估计"镜像效率"**

左下方窗格，显示基本图层信息和一个实验指标，用于猜测镜像所包含的空间浪费。其中可能包括: 跨层重复文件,跨层移动文件或不完全删除文件。提供了百分比"得分"，和总浪费的文件空间。

**快速构建/分析周期**

您可以构建 Docker 镜像，并立即使用一个 dive build -t some-tag .`命令进行分析:`

你仅仅只要将你的`docker build`命令更换成`dive build`命令。

## 安装

**Ubuntu/Debian**

```bash
wget https://github.com/wagoodman/dive/releases/download/v0.3.0/dive_0.3.0_linux_amd64.deb
sudo apt install ./dive_0.3.0_linux_amd64.deb
```

**RHEL /Centos**

```bash
curl -OL https://github.com/wagoodman/dive/releases/download/v0.3.0/dive_0.3.0_linux_amd64.rpm
rpm -i dive_0.3.0_linux_amd64.rpm
```

**Arch Linux**

可用作[dive](https://aur.archlinux.org/packages/dive/)在 Arch User Repository(AUR)中.

```bash
aurman -S dive
```

上面的例子假设`aurman`作为安装 AUR 包的工具。_注意_:AUR 存储库是**不**由 dive 项目维护人员控制.

**Mac**

```bash
brew tap wagoodman/dive
brew install dive
```

或从发布(releases)页面下载 Darwin 版本.

**Go 工具**

```bash
go get github.com/wagoodman/dive
```

**Docker**

```bash
docker pull wagoodman/dive
```

要么

```bash
docker pull quay.io/wagoodman/dive
```

运行时,您需要包含 docker 客户端二进制文件和 socket 文件:

```bash
docker run --rm -it \
    -v /var/run/docker.sock:/var/run/docker.sock \
    wagoodman/dive:latest <dive arguments...>
```

适用于 Windows Docker(显示 PowerShell 兼容的换行符;折叠为一行以实现命令提示符兼容性)

```bash
docker run --rm -it `
    -v /var/run/docker.sock:/var/run/docker.sock `
    wagoodman/dive:latest <dive arguments...>
```

**注意:**根据您在本地运行的 docker 版本,您可能需要将 docker API 版本指定为环境变量:

```bash
   DOCKER_API_VERSION=1.37 dive ...
```

或者如果您在一个 docker 镜像运行:

```bash
docker run --rm -it \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -e DOCKER_API_VERSION=1.37
    wagoodman/dive:latest <dive arguments...>
```

## 键绑定

| 键绑定                                    | 描述                              |
| ----------------------------------------- | --------------------------------- |
| <kbd>Ctrl + C</kbd>                       | Exit                              |
| <kbd>Tab</kbd> or <kbd>Ctrl + Space</kbd> | 在图层和文件树视图之间切换        |
| <kbd>Ctrl + F</kbd>                       | 过滤文件                          |
| <kbd>Ctrl + A</kbd>                       | 图层视图:查看聚合镜像修改         |
| <kbd>Ctrl + L</kbd>                       | 图层视图:查看当前图层修改         |
| <kbd>Space</kbd>                          | 文件树 视图:折叠/取消折叠目录     |
| <kbd>Ctrl + A</kbd>                       | 文件树 视图:显示/隐藏添加的文件   |
| <kbd>Ctrl + R</kbd>                       | 文件树 视图:显示/隐藏已删除的文件 |
| <kbd>Ctrl + M</kbd>                       | 文件树 视图:显示/隐藏已修改的文件 |
| <kbd>Ctrl + U</kbd>                       | 文件树 视图:显示/隐藏未修改的文件 |
| <kbd>PageUp</kbd>                         | 文件树 视图:向上滚动页面          |
| <kbd>PageDown</kbd>                       | 文件树 视图:向下滚动页面          |

## 配置

无需配置,但是,您可以创建配置文件，并覆盖默认值:

```yaml
log:
  enabled: true
  path: ./dive.log
  level: info

# 注意：您可以通过用逗号分隔值来指定多个绑定。
# 注意：UI提示,只为第一个绑定
keybinding:
  # 全局绑定
  quit: ctrl+c
  toggle-view: tab, ctrl+space
  filter-files: ctrl+f, ctrl+slash

  # 层视图特定绑定
  compare-all: ctrl+a
  compare-layer: ctrl+l

  # 文件视图特定绑定
  toggle-collapse-dir: space
  toggle-added-files: ctrl+a
  toggle-removed-files: ctrl+r
  toggle-modified-files: ctrl+m
  toggle-unmodified-files: ctrl+u
  page-up: pgup
  page-down: pgdn

diff:
  # 您可以更改 filetree 中显示的默认文件（右窗格）。 默认情况下显示所有diff类型。
  hide:
    - added
    - removed
    - changed
    - unchanged

filetree:
  # 默认目录折叠状态
  collapse-dir: false

  # 文件树应在屏幕上显示的屏幕宽度百分比（必须 >0 且 <1 ）
  pane-width: 0.5

layer:
  # 启用显示此图层和之前图层的所有更改
  show-aggregated-changes: false
```

dive 将在以下位置搜索配置:

- `~/.dive.yaml`
- `$XDG_CONFIG_HOME/dive.yaml`
- `~/.config/dive.yaml`
