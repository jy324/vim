# vim

个人 Vim 配置，适配 Vim 8.0+ 与 Neovim，支持终端与 GUI。配置采用模块化设计，可按需选择功能组合。

**核心特性：**
- 🎯 **任务系统**：AsyncRun/AsyncTasks 提供完整的编译/运行/测试工作流
- 📂 **文件导航**：Dirvish/LeaderF/CtrlP + QuickUI 菜单实现高效浏览
- 🔧 **多语言支持**：内置 C/C++/Python/Go/Lua/Markdown 等数十种语言增强
- 🎨 **UI 增强**：QuickMenu 双层菜单 + 丰富配色方案 + 状态栏定制
- 🚀 **可选 LSP**：支持 CoC/vim-lsp/LanguageClient 等多种补全方案
- 📝 **开发工具**：集成 Git/SVN、Lint、调试器、翻译、文档查询等

配置入口是 `init.vim`，主要配置集中在 `init/` 目录，插件管理使用 `bundle.vim`。

> 💡 **提示**：详细功能说明见 [doc/features-shortcuts.md](doc/features-shortcuts.md)


## Install


### Linux:

- 新建 `~/.vim` 目录，把项目克隆到 `~/.vim/vim` 下面：

```bash
cd ~/.vim
git clone https://github.com/skywind3000/vim.git
```

- 编辑 `~/.vimrc` 文件，里面加一行：

```VimL
so ~/.vim/vim/init.vim
so ~/.vim/vim/skywind.vim
```

### Windows:

- 新建 `D:\github` 目录，把项目克隆到 `D:\github\vim` 下面：

```batch
d:
cd \github
git clone https://github.com/skywind3000/vim.git
```

- 新建 `C:\Users\YourName\.vim` 目录：

```batch
C:\
CD \Users\YourName
mkdir .vim
```

- 编辑 `C:\Users\YourName\_vimrc` 文件，里面加一行：

```VimL
so d:/github/vim/init.vim
so d:/github/vim/skywind.vim
```

### 包管理

使用 [vim-plug](https://github.com/junegunn/vim-plug) 管理插件。在 `.vimrc` 中通过 `g:bundle_group` 控制加载哪些插件组：

```VimL
" 基础配置（必选）
let g:bundle_group = ['simple', 'basic']

" 添加更多功能（可选）
let g:bundle_group += ['inter', 'high', 'opt']

" 启用 LSP/补全（三选一）
" let g:bundle_group += ['coc']        " coc.nvim
" let g:bundle_group += ['lsp']       " vim-lsp
" let g:bundle_group += ['yegappan']  " yegappan/lsp (Vim 9.0+)

" 其他可选模块
" let g:bundle_group += ['ale', 'echodoc', 'lightline', 'airline']
" let g:bundle_group += ['vimwiki', 'floaterm', 'nerdtree', 'copilot']
" let g:bundle_group += ['colors', 'vim-go', 'vimspector']

so ~/.vim/vim/bundle.vim
```

**可用插件组：**
- `simple`：Sneak、Surround、Tabular、Dirvish 等基础增强
- `basic`：LeaderF/CtrlP、ChooseWin、语法高亮、文本对象
- `inter`：Notes、Outliner、Gist、DrawIt、Flog、vim-mark
- `high`：Signify、FZF、Ranger、Table-mode、Autoformat
- `opt`：CtrlSF、Translator、Gutentags、Switch、Emmet、Vimux

**编辑器选项：**
本配置默认 `tabstop=4`、`shiftwidth=4`、`noexpandtab`。如需修改，在 source 后覆盖：

```VimL
so ~/.vim/vim/init.vim
so ~/.vim/vim/skywind.vim

set expandtab      " 使用空格代替 Tab
set tabstop=2      " 修改缩进宽度
```


## 主目录

主目录位于顶部，连续按两次空格 `<space><space>` 展开：

![picture-vim-menu](https://skywind3000.github.io/images/p/misc/2023/vim-menu.png)

主目录可以用 hjkl 来浏览，空格或者回车选中，按 ESC 离开，大部分功能都能在这里找到。

（需要 Vim 8.2 +）

## 扩展目录

扩展目录位于底部，连续按两次 TAB 键可以看到：

![picture-vim-menu2](https://skywind3000.github.io/images/p/misc/2023/vim-menu2.png)

ESC 离开目录，按对应字母触发功能，CTRL+j/k 翻页，BackSpace 可以回到上一级

（需要 Vim 8.0+）

## Keymap

### 光标移动

除了 NORMAL 模式 HJKL 移动光标外，新增加所有模式的光标移动快捷键：

| 按键    | 说 明    |
| :-----: | ------   | 
| C-H | 光标左移 |
| C-J | 光标下移 |
| C-K | 光标上移 |
| C-L | 光标右移 |

这样 INSERT下面移动几个字符，或者 COMMAND 模式下左右上下移动都都可以这么来。不喜欢可以后面 unmap 掉，但是有时候稍微移动一下还要去切换模式挺蛋疼的。

大部分默认终端都没问题，一些老终端软件，如 Xshell/SecureCRT，需要确认一下 Backspace 键的编码为 127 (`CTRL-?`) 或者勾选 Backspace sends delete，保证按下 BS 键时发送 ASCII 码 127 而不是 8 (`CTRL-H`) 。

### 插入模式

| 按键    | 说 明    |
| :-----: | ------   | 
| C-A | 移动到行首 |
| C-E | 移动到行尾 |
| C-D | 删除当前字符 |

### 命令模式

| 按键    | 说 明    |
| :-----: | ------   | 
| C-A | 移动到行首 |
| C-E | 移动到行尾 |
| C-D | 光标删除当前字符 |
| C-P | 历史上一条命令 |
| C-N | 历史下一条命令 |

### 窗口跳转

| 按键    | 说 明    |
| :-----: | ------   | 
| TAB h/j/k/l | 同 CTRL-W h/j/k/l，快速切换窗口 |
| Alt-H/J/K/L | Normal/Insert/Terminal 模式跨窗口跳转 |
| Alt-e | ChooseWin 模式选择窗口 |
| <Space>= / - | 增大/减小当前窗口高度 |
| <Space>, / . | 减小/增大当前窗口宽度 |
| TAB g | 回到上一个窗口 (`<C-W>p`) |

**提示**：`Alt-H/J/K/L` 在终端模式下也可用，无需退出 Terminal。


### TabPage 

除了使用原生的 TabPage 切换命令 `1gt`, `2gt`, `3gt` ... 来切换标签页外，定义了如下几个快捷命令：

| 按键    | 说 明    |
| :-----: | ------   |
| \1  | 先按反斜杠 `\`再按 `1`，切换到第一个标签页 |
| \2  | 切换到第二个标签页 |
| ... | ... |
| \9  | 切换到第九个标签页 |
| \0  | 切换到第十个标签页 |
| \t  | 新建标签页，等同于 `:tabnew` |
| \g  | 关闭标签页，等同于 `:tabclose` |
| TAB n | 下一个标签页，同 `:tabnext` |
| TAB p | 上一个标签页，同 `:tabprev` |

还可以使用 ALT+1 到 ALT+9 来切换，前提是终端软件需要配置一下，有些终端 ALT_1 到 ALT_9 被用来切换 connection 的 tab，那么可以把 ALT+SHIFT+1-9 配置成发送字符串：`\0331` 到 `\0339` 等几个不同字符串，其中 `\033` 是 ESC键的编码，这样不影响终端软件的 ALT_1-9 情况下，用 ALT_SHIFT_1-9 来代替。


### 功能键

| Key    | Task | Description                                                                     |
| :-----: | --| ----                                                                    |
| F5      | file-run | 运行当前程序，自动检测 C/Python/Ruby/Shell/JavaScript，并调用正确命令运行 |
| F6      | make | 运行 make 任务 |
| F7      | emake | 调用 emake 编译当前项目文件， $PATH 中需要有 emake 可执行                     |
| F8      | emake-exe | 调用 emake 运行当前项目文件， $PATH 中需要有 emake 可执行                     |
| F9      | file-build | 调用 gcc 编译当前 C/C++ 程序，$PATH 中需要有 gcc可执行，编译到当前目录下  |
| F11   | file-debug | 调试当前程序 |
| S-F5 | project-run | 运行当前项目，请用 S-F12 编辑当前项目 .tasks 文件中的 project-run 方法 |
| S-F6 | project-test | 测试当前项目，请用 S-F12 编辑当前项目 .tasks 文件中的 project-test 方法 |
| S-F7 | project-init | 测试当前项目，请用 S-F12 编辑当前项目 .tasks 文件中的 project-init 方法 |
| S-F8 | project-install | 测试当前项目，请用 S-F12 编辑当前项目 .tasks 文件中的 project-install 方法 |
| S-F9 | project-build | 测试当前项目，请用 S-F12 编辑当前项目 .tasks 文件中的 project-build 方法 |
| S-F11   | project-debug | 调试当前项目 |
| F10   | 非任务| 打开/关闭 quickfix                        |
| F12 | 非任务| 打开所有任务，让你选择 |
| S-F12 | 非任务| 编辑当前项目的 task | 

全局任务配置文件在本仓库根目录的 `tasks.ini` 里描述。



### 文件浏览

该功能主要是使用 Vim 自带的 dirvish/netrw 被编辑文件的目录，方便各种方式切换文件

| 按键 | 说明 |
|:----:|------|
|  +  | 在当前窗口打开文件浏览器，浏览之前文件所在目录  |
|  TAB 6  | 在左边新窗口打开文件浏览器，浏览之前文件所在目录  |
|  TAB 7  | 在右边新窗口打开文件浏览器，浏览之前文件所在目录  |
|  TAB 8  | 在下边新窗口打开文件浏览器，浏览之前文件所在目录  |
|  TAB 9  | 在新标签打开文件浏览器，浏览之前文件所在目录  |

使用 `+` 返回当前文件所在目录时，如果文件被修改过未保存，且 Vim 没有设置 hidden，则会在该文件窗口上面打开目录浏览，不会把文件关掉。 

当文件浏览器打开以后，按 `~` 键，返回用户目录（$HOME）；按 `` ` `` （反引号），返回项目根目录。详见：[Vinegar](https://github.com/skywind3000/vim/wiki/Vim-Vinegar-and-Oil)

## 更多功能

### 代码导航与搜索

| 快捷键 | 功能说明 |
|:------:|----------|
| `Ctrl-P` / `Ctrl-N` | LeaderF 模糊搜索文件 / MRU 文件 |
| `Alt-P` / `Alt-N` | LeaderF 搜索函数 / Buffer |
| `Alt-I` / `Alt-Y` | 显示当前文件函数列表 |
| `<Leader>cv/cx` | GrepCode 全项目搜索当前单词 |
| `<Leader>cs/cg/cc` | Cscope 查找符号/定义/调用者 |
| `Alt-;` | 预览当前光标下的 Tag |
| `gz` / `gZ` | Sneak 正向/反向快速跳转 |

### Lint 与代码检查

| 快捷键 | 功能说明 |
|:------:|----------|
| `<Space>lp` | 运行 pylint (Python) |
| `<Space>lf` | 运行 flake8 (Python) |
| `<Space>ls` | 运行 splint (C) |
| `<Space>lc` | 运行 cppcheck (C/C++) |
| `<Space>lt` | HTML 格式化 |
| `[e` / `]e` | 跳转到上/下一个错误 |

### 版本控制（Git/SVN）

| 快捷键 | 功能说明 |
|:------:|----------|
| 主目录 → SVN/GIT | 查看 diff/log/blame 等操作 |
| `<Space>sc/su/st` | SVN commit/update/status |
| `:Ghistory` | 查看当前文件 Git 历史 |
| `:Gpush` / `:Gfetch` | 异步 Git push/fetch |

### 快速编辑

| 快捷键 | 功能说明 |
|:------:|----------|
| `<Space>e-/e=/e#` | 插入不同风格的注释框 |
| `<Space>ec` | 插入文件头版权信息 |
| `<Space>em` | 插入 main 函数模板 |
| `<Space>et` | 插入当前时间戳 |
| `<Space>at` | 对齐 Cheat Sheet 格式 |
| `gb=` / `gb,` / `gbl` | Tabular 对齐赋值/逗号/竖线 |
| `<Space>p` | 用寄存器 0 粘贴（不覆盖剪贴板） |

### 配置快速访问

| 快捷键 | 打开文件 |
|:------:|----------|
| `<Space>hp` | `~/.vim/project.txt` |
| `<Space>hk` | `init/keymaps.vim` |
| `<Space>hv` | `bundle.vim` |
| `<Space>hs` | `skywind.vim` |
| `<Space>ht` | `tasks.ini` |
| `<Space>hr` | `.vimrc` / `init.vim` |
| `<Space>hq` | `quicknote.txt` 快速笔记 |

## 配置自定义

### 本地配置文件

配置会自动加载本地覆盖文件（不纳入版本控制）：

- Vim: `~/.vim/local.vim`
- Neovim: `~/.config/nvim/local.vim`

可在此文件中覆盖任何默认设置、添加私有快捷键或加载额外插件。

### 备份文件说明

默认启用文件备份功能，所有 `.bak` 文件保存在 `~/.vim/tmp/`：

```vim
set backup
set writebackup
set backupdir=~/.vim/tmp
set backupext=.bak
set noswapfile
set noundofile
```

**禁用备份**：在加载配置前设置 `let g:asc_no_backup = 1`

### 任务系统自定义

在项目根目录创建 `.tasks` 文件定义项目特定任务：

```ini
[project-build]
command=make -j8
cwd=<root>

[project-run]
command=./build/myapp
output=terminal
```

按 `<S-F12>` 快速编辑任务配置，`<F12>` 选择并运行任务。

## 插件列表摘要

**核心插件**（启用 `simple` + `basic`）：
- vim-plug, vim-dirvish, vim-sneak, vim-surround, vim-unimpaired
- easymotion/stargate, tabular, delimitMate/auto-pairs
- LeaderF/CtrlP, vim-choosewin, vim-expand-region, vim-dict
- vim-textobj-*, python-syntax, vim-markdown 等

**高级功能**（`inter` + `high` + `opt`）：
- signify, fzf, ranger, gutentags, ctrlsf, translator
- neoformat, vim-table-mode, gist-vim, vim-notes, flog

**可选模块**：
- **LSP/补全**: coc.nvim, vim-lsp, yegappan-lsp, neocomplete
- **调试**: vimspector, NeoDebug, termdebug
- **Git**: vim-fugitive, gv.vim, vim-flog, vimagit
- **UI**: lightline/airline, nerdtree, defx, floaterm, vim-which-key
- **语言**: vim-go, vim-lsp-settings, copilot.vim, tabnine-vim
- **其他**: vimwiki, calendar, grammarous, pangu.vim

完整列表见 [bundle.vim](bundle.vim)，每个插件的详细配置在 `site/bundle/*.vim`。

## 常见问题

**Q: 如何更新插件？**
```vim
:PlugUpdate
```

**Q: 如何禁用某个快捷键？**  
在 `local.vim` 中 `unmap` 或重新映射：
```vim
unmap <Space>lp
nnoremap <Space>lp :echo "Disabled"<CR>
```

**Q: 终端下 Alt 键不工作？**  
确保终端发送 ESC 序列。部分终端需配置 Meta key 或使用 `<M-xxx>` 的 ESC 等价形式。

**Q: 如何适配 Neovim？**  
大部分配置兼容，LSP 推荐用 nvim-lspconfig。Lua 配置可放在 `neovim.lua`。

## 相关资源

- **文档**: [doc/features-shortcuts.md](doc/features-shortcuts.md) - 详细功能与快捷键
- **Wiki**: [GitHub Wiki](https://github.com/skywind3000/vim/wiki)
- **AsyncTasks**: [vim-tasks](https://github.com/skywind3000/asynctasks.vim)
- **QuickUI**: [vim-quickui](https://github.com/skywind3000/vim-quickui)

### Credit

欢迎关注：

- [博客](https://skywind.me/blog)
- [推特](https://x.com/skywind3000)


