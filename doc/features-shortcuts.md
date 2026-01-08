# Skywind Vim 配置功能与快捷键指南

> 依据仓库的 `README.md`、`init/*.vim`、`skywind.vim`、`bundle.vim` 等文件整理。本指南概述该配置补充的能力与常用快捷键，便于快速查阅与二次定制。

## 1. 配置概览

- **入口与分层**：`init.vim` 负责加载 `init/config.vim`、`init/plugins.vim`、`init/keymaps.vim` 等子模块；`skywind.vim` 执行可选脚本（`site/opt/*`）、安装模块驱动并注入平台相关设置。
- **插件编组**：`bundle.vim` 通过 `g:bundle_group` 控制插件集合（simple/basic/inter/high/opt 等），覆盖文件导航、diff、Git、构建、LSP、补全、配色、浮动终端、调试器等多种场景。
- **任务与构建**：`asyncrun`/`asynctasks` + 根目录 `tasks.ini` 形成统一的 file-run/make/project-* 任务流，配套 F5~F12 以及 QuickMenu 入口。
- **菜单导航**：`quickui`/`quickmenu` 打造“主目录” (`<Space><Space>`) 与“扩展目录” (`<Tab><Tab>`) 两套 UI，可浏览构建、搜索、版本控制、Lint、外部工具等操作。
- **脚本与工具库**：`autoload/asclib.vim`、`init/tools.vim` 提供路径解析、项目根查找、QuickFix 滚动、Buffer 关闭、透明度调节、外部终端、注释模板等实用函数。

## 2. 关键功能补充

### 2.1 菜单与 UI
- **主目录 (`<Space><Space>`)**：呈现带图标的按键菜单，使用 `hjkl` 导航，`Space/Enter` 确认，`Esc` 退出。
- **扩展目录 (`<Tab><Tab>`)**：位于底部，以字母快速选择；`Ctrl+j/k` 翻页，`Backspace` 回上级。
- **QuickMenu 面板**：`<Space>m0~m3`、`<C-F10>`、`<S-F10>` 触发不同菜单集合（开发、GNU Global、终端等）。

### 2.2 文件 / 项目工作流
- **Vinegar + Dirvish**：`+` 或 `<Tab>6/7/8/9` 迅速在各窗口/标签页打开当前文件所在目录；`~` 回到 `$HOME`，`` ` `` 回到项目根。
- **NERDTree/Defx/Ranger**：`<Tab>0`/`<Tab>y` 直接定位到当前文件或项目根；根据启用的包组可切换不同文件浏览器。
- **Buffer 管理**：`BufferClose` 命令（`init/tools.vim`）确保关闭缓冲区时窗口布局不变；`quickui#tools#list_buffer` 提供列表式切换。

### 2.3 构建 & 任务
- **AsyncTask 模板**：F5~F12 映射常用 file-run/make/emake/project-* 任务；`<S-F12>` 打开任务编辑器，`<F12>` 用 `TaskFinder` 选择任务。
- **项目级配置**：仓库根的 `tasks.ini` 与 `tools/conf/template.ini` 约定默认目标；`<Space>jm` 快速切到项目 `Makefile`。

### 2.4 代码导航 / Lint / VCS
- **ctags/gtags**：`<Leader>cb1~cb6` 刷新不同标签数据库，QuickMenu 中提供 Tag 更新、GNU Global 搜索入口。
- **Lint 工具**：`asclib#lint_*` 封装 pylint/flake8/cppcheck/splint，配合快捷键 `<Space>lp/lf/ls/lc`。
- **版本控制**：`quickmenu` 集成 svn/git diff/log、TortoiseSVN/TortoiseGit 操作；`skywind.vim` 中 `Gpush`/`Gfetch` 封装 git push/fetch。

### 2.5 语言与补全
- **文本对象**：`vim-textobj-*`、`after_object#enable()`、`kana/*` 插件提供函数/参数/缩进等对象；`onoremap az/ak` 等组合进一步扩展。
- **补全与 LSP**：可按需启用 CoC、vim-lsp、LanguageClient-neovim、nvim-cmp 等模块；`echodoc`/`PreviewSignature` 显示签名提示。
- **特殊语言支持**：`ftplugin/` 针对 C/C++/Go/Markdown/Org/PS1 等设置编译、缩进与语法增强，`bundle.vim` 拉取 HLSL、Flex/Bison、Lark、ANTL 等语法插件。

## 3. 常用快捷键

> 主要来源：`README.md`、`init/keymaps.vim`、`bundle.vim`、`skywind.vim`。

### 3.1 光标 / 模式操作

| 快捷键 | 模式 | 功能说明 |
| --- | --- | --- |
| `Ctrl-H/J/K/L` | Normal/Insert/Command | 全模式光标左/下/上/右移动，免去切换模式的小范围调整 |
| `Ctrl-A / Ctrl-E` | Insert/Command | 跳到行首 / 行尾 |
| `Ctrl-D` | Insert/Command | 删除当前字符 |
| `Alt-h/l` | Normal | 单词级向左/右移动 (`b` / `w`) |
| `Alt-j/k` | Normal | 按可视行向下/上 (`gj` / `gk`) |
| `Alt-H/J/K/L` | Normal/Insert/Terminal | 跨窗口切换（映射 `Ctrl-W` 方向），终端下配合 `termwinkey` |
| `Alt-z / Alt-Z` | Normal | 折叠切换 `za / zA` |

### 3.2 窗口与标签

| 快捷键 | 范围 | 功能说明 |
| --- | --- | --- |
| `<Tab>h/j/k/l` | Normal | 映射 `Ctrl-W` 方向，快速切窗 |
| `<Tab>,` / `<Tab>.` | Normal | 调整当前标签页位置（左移/右移） |
| `Alt+1~9/0`、`\1~\0` | Normal/Insert | 跳转到对应编号标签页，`Alt+Shift+数字` 可发 ESC 序列兼容终端 |
| `<Tab>n / <Tab>p` | Normal | 下一个 / 上一个标签页 |
| `<M-Left/Right>` | GUI/Win | 调整标签顺序 |
| `<Tab>6/7/8/9` | Normal | 在左/右/下/新标签打开 Vinegar 浏览器 |
| `<Tab>0 / <Tab>y` | Normal | 用 NERDTree 打开当前文件目录 / 项目根目录 |

### 3.3 文件与导航

| 快捷键 | 范围 | 功能说明 |
| --- | --- | --- |
| `+` | Normal | 在当前窗口打开 dirvish/nerdtree 浏览当前文件目录 |
| `<Space>hp/hb/hk/hv/...` | Normal | 快速跳转到常用配置（`project.txt`、`bundle.vim`、`init/keymaps.vim`、`skywind.vim` 等） |
| `<Space>hf` | Normal | `FileSwitch` 当前文件所在目录 |
| `<Space>hg/hq/hm` | Normal | 打开 `scratch.txt`、`quicknote.txt/md` 等笔记文件 |
| `<Space>hn` | Normal | 打开 `neovim.lua` 设置 |
| `<Space>ha` | Normal | Windows 下跳转自定义 AutoHotkey 脚本 |

### 3.4 构建 / 任务 / 运行

| 快捷键 | 功能 |
| --- | --- |
| `F5` / `Shift-F5` | `AsyncTask file-run` / `project-run` |
| `F6` / `Shift-F6` | `make` / `project-test` |
| `F7` / `Shift-F7` | `emake` / `project-init` |
| `F8` / `Shift-F8` | `emake-exe` / `project-install` |
| `F9` / `Shift-F9` | `file-build` / `project-build` |
| `F10` | 打开/关闭 QuickFix (`asyncrun#quickfix_toggle`) |
| `F11` / `Shift-F11` | `file-debug` / `project-debug` |
| `F12` / `Shift-F12` | `TaskFinder` / `AsyncTaskEdit` |
| `<Space>jj/jc/jk/jl/j1~j5` | 各类 `make`/`clean`/`run`/`test`/自定义目标（`AsyncRun`） |
| `<Space>jm` | 调出项目 `Makefile` |

### 3.5 Lint / 工具 / 其他

| 快捷键 | 功能 |
| --- | --- |
| `<Space>lp` / `<Space>lf` / `<Space>ls` / `<Space>lc` | 分别运行 pylint、flake8、splint、cppcheck |
| `<Space>lt` | HTML 格式化 |
| `<Space>ll` | 重复上一条命令行输入 |
| `<Space>at` / `<Space>ab` | 对齐 cheat sheet / C++ 花括号展开 |
| `<Space>e- / e= / e#` | 插入不同符号的注释块 |
| `<Space>ec / em / el / et` | 插入版权头 / main 模板 / modeline / 当前时间 |
| `<Space>sc / su / st` | 执行 SVN checkout / update / status |
| `<Space>gp / gs / gr` (Visual) | 发送选中文本给 Python / 转换为搜索或替换命令 |
| `<Space><Space>` / `<Tab><Tab>` | 打开主目录 / 扩展目录 |
| `<Space>m0~m3` | 切换不同 quickmenu 配置 |
| `+` 或 `<Space>gp` | 调用 quickui buffer 列表（Vim >= 8.2） |

## 4. 推荐使用步骤

1. **选择插件组**：在个人 `vimrc` 中设置 `let g:bundle_group = ['simple','basic','inter','high','opt', ...]`，再 `source bundle.vim` 安装所需插件。
2. **加载主配置**：按照 `README.md` 建议 `source init.vim` 与 `skywind.vim`，然后用 `<Space>hk`/`<Space>hv` 查看并裁剪键位与插件。
3. **自定义任务**：在项目根复制 `tasks.ini` 模板或运行 `<S-F12>` 编辑；使用 F5~F9 检查任务输出，`F10` 观察 QuickFix。
4. **使用菜单导航**：`<Space><Space>` 进入主目录寻找大部分功能，`<Tab><Tab>` 访问扩展页；遇到特定操作（如 GNU Global、SVN、Lint）可通过 `<Space>m*` 或 QuickMenu 的分组快速定位。
5. **记忆核心快捷键**：优先掌握窗口/标签/任务相关组合，其余按需在 `init/keymaps.vim` 中查阅或再行调整。

---
如需进一步个性化，可在 `~/.vim/local.vim` 或 `~/.config/nvim/local.vim` 中覆盖默认设置，或在 `bundle.vim` 中添加/移除插件。