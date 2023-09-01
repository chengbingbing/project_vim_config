# Gemini 上下文：Vim 配置

本目录包含用户 `bingbingcheng` 的个人 Vim 配置和插件生态系统。这是一个自包含的设置，插件在 `~/.vim/` 目录结构中手动管理，主要配置文件统一汇集在 `~/.vim/vimrc` 中。

## 目录结构

*   **`vimrc`**: 主配置文件。它通过软链接连接到 `~/.vimrc`，以确保 Vim 启动时自动加载。该文件会加载系统默认设置 (`/etc/vim/vimrc`)，但会使用用户特定的设置进行覆盖。
*   **`NERD_Tree/`**: 包含 [NERDTree](https://github.com/preservim/nerdtree) 插件，用于文件系统导航。
*   **`Taglist/`**: 包含 [Taglist](https://github.com/yegappan/taglist) 插件，用于源代码浏览（依赖 `ctags`）。
*   **`YouCompleteMe/`**: 包含 [YouCompleteMe](https://github.com/ycm-core/YouCompleteMe) 代码补全引擎。
    *   **注意**: 此插件包含编译组件。最近已使用 Python 3.10 针对 C 族语言（`clang-completer`）完成了编译。
*   **`plugin/`**: 包含指向系统级 Vim 脚本（如 `winmanager`）的软链接。

## 快捷键绑定 (Key Bindings)

在 `vimrc` 中配置了以下快捷键：

| 按键 | 模式 | 动作 |
| :--- | :--- | :--- |
| **F2** | Normal | 切换 **NERDTree** (文件浏览器) 显示。 |
| **F4** | Normal/Insert | 为当前目录重新生成 **ctags** 并更新 Taglist。 |
| **F5** | Normal | 强制执行 YouCompleteMe 编译和诊断。 |
| **F8** | Normal | 切换 **WinManager** (布局: FileExplorer \| TagList \| NERDTree)。 |
| **F9** | Normal | 切换 **Taglist** 窗口显示。 |
| **Enter** | Insert | 选中当前高亮的补全项（如果弹出菜单可见）。 |
| **Space+Space** | Insert | 触发全能补全 (Omni-completion `<C-x><C-o>`)。 |

## 关键配置项

*   **编辑体验**:
    *   Tab 键转换为 4 个空格 (`expandtab`, `tabstop=4`, `ts=4`)。
    *   启用行号显示 (`set nu`)。
    *   在所有模式下启用鼠标支持 (`set mouse=a`)。
    *   集成系统剪贴板 (`set clipboard=unnamedplus`)。
    *   **自动格式化**: 保存 `.c`, `.h`, 和 `.java` 文件时自动去除行尾空格。
*   **搜索**:
    *   启用增量搜索 (`incsearch`) 和搜索高亮 (`hlsearch`)。
*   **YouCompleteMe (YCM)**:
    *   最小补全触发字符数: 1。
    *   基于 Tags 文件的补全: 已开启。
    *   诊断 UI: 已关闭（减少干扰）。
    *   注释中补全: 已开启。

## 维护与使用说明

### 1. 更新配置
编辑 `~/.vim/vimrc` 来修改设置。系统文件 `/etc/vim/vimrc` 已重置为默认值，且实际上已被当前用户的配置旁路，不会产生影响。

### 2. 重新编译 YouCompleteMe
如果系统 Python 版本发生变化或插件进行了更新，可能需要重新编译 YCM。
**编译命令:**
```bash
cd ~/.vim/YouCompleteMe
python3 install.py --clang-completer
```

### 3. 插件管理
当前插件是手动安装的。如需添加新插件：
1.  将其 克隆/下载 到 `~/.vim/` 的子目录中（例如 `~/.vim/MyPlugin`）。
2.  在 `~/.vim/vimrc` 中将该路径添加到 `rtp` (runtimepath)：
    ```vim
    set rtp+=~/.vim/MyPlugin
    ```
