# 更新日志 / Changelog

只记对外发布的版本。QuadCut 从 1.8.1 才开始发布，之前的开发过程没有公开版本。

Only released versions are listed. QuadCut's first public release was 1.8.1; nothing before that was ever published.

每个版本先中文、后 English，条目一一对应。安装包见对应 Release 的附件。

Each version is given in Chinese first, then in English, entry by entry. Installers are attached to the corresponding Release.

---

## 1.8.4.1 — 2026-11-16

### 中文

**内存**

- 100% 放大镜缓存四格共用一份，最多留 3 张（原来是 6 张、上限 512 MB，实际能把常驻顶到 300 MB 上下）
- 放大镜收起后闲置 60 秒自动释放这份缓存 —— 以前看过的图会一直躺在内存里直到退出程序
- 缩略图内存缓存上限定为 128 MB（原来 256 MB，等于永远不会触发淘汰）

**修**

- 中键钉住的 100% 预览，鼠标移出预览侧栏就消失了。移动鼠标不算操作，只有再按一下鼠标键才该收掉

**其他**

- 安装包文件名带架构标识：`QuadCut-1.8.4.1-arm64.dmg`。本程序只支持 Apple Silicon（arm64），Intel Mac 打不开
- 五份 README 的快捷键表拆成「特色 / Mac 默认」两列，逐条对照

### English

**Memory**

- The 100% loupe cache is now shared by all four panes and keeps at most 3 images (it used to hold 6 with a 512 MB cap, which could still push resident memory to around 300 MB)
- Once the loupe is dismissed, the cache is released after 60 seconds idle — previously, images you had looked at stayed in memory until you quit the app
- The thumbnail memory cache is capped at 128 MB (the old 256 MB cap was never reached, so eviction never kicked in)

**Fixed**

- A middle-click-pinned 100% preview disappeared as soon as the pointer left the preview sidebar. Moving the mouse is not an action — only another click should dismiss it

**Other**

- The installer filename now carries the architecture: `QuadCut-1.8.4.1-arm64.dmg`. The app supports Apple Silicon (arm64) only; it will not open on an Intel Mac
- The shortcut tables in all five READMEs are split into "Featured / Mac defaults" columns, for line-by-line comparison

---

## 1.8.4 — 2026-11-12

### 中文

图里明明存着参数，为什么读不出来？这一版把 AI 图片的解析重新做了一遍：不再猜节点叫什么名字，而是从出图节点顺着连线往上游走。

**AI 图片**

- 一张图里有多个采样器时不再靠运气（草图和精修各一个的年代，步数一会儿 5 一会儿 8）
- 能读 `SamplerCustomAdvanced` 这类新式工作流了：正负向挂在 `guider` 上，本来就不在采样器里
- 中转节点一律穿透：`Any Switch`、`showAnything`、`CR Text`、`Text Concatenate` 都能读到底，不再只认几个固定输入名
- 中转节点把序号和正文一起送进来时，取最长的那段，不再显示一串编号
- 链上只有一句「编辑指令」（局部重绘之类）时，改用另存的完整画面描述
- 主模型跟着采样器的 model 链走：图里有两个 UNETLoader 时也固定取真正出图的那个
- 正负向指向同一个编码器时，负向留空，不再复制一份正向
- 跳过 bypass / mute 的节点，跳过便签，也不把反推模型猜的标签当成提示词

**文件管理**

- 图标网格模式显示真实缩略图（以前只有大缩略图模式才有）；滚动时先给系统图标，停手后自动补上

### English

The parameters were stored in the image — why couldn't we read them? This release rebuilds AI image parsing: instead of guessing what a node is called, it walks upstream along the actual links, starting from the output node.

**AI images**

- Multiple samplers in one graph no longer come down to luck (back when a sketch and a refine pass each had their own sampler, steps would read 5 one time and 8 the next)
- New-style workflows such as `SamplerCustomAdvanced` now work: positive and negative hang off the `guider`, not the sampler
- Pass-through nodes are traversed all the way — `Any Switch`, `showAnything`, `CR Text`, `Text Concatenate` — instead of accepting only a few fixed input names
- When a pass-through node feeds in both an index and the real text, the longest segment wins, so a bare number no longer shows up as the prompt
- If the chain only holds an edit instruction (inpainting and the like), the separately stored full scene description is used instead
- The main model follows the sampler's model chain, so with two UNETLoaders in the graph it still picks the one that actually rendered the image
- When positive and negative point at the same encoder, negative is left empty instead of duplicating positive
- Bypassed and muted nodes are skipped, notes are skipped, and tags guessed by a captioning model are never mistaken for the prompt

**File management**

- Icon grid mode now shows real thumbnails (previously only large-thumbnail mode did); while scrolling it shows system icons first and fills in the real ones once you stop

---

## 1.8.3 — 2026-11-09

### 中文

当我意识到很多只使用 Mac 键盘的人使用该软件的这套快捷键会存在冲突的时候，我决定使用两套快捷键系统。和我一样使用 Mac mini、甚至同样使用 Win/Mac 二合一键盘的人可以保持原样，只使用 Mac 键盘的用户可以选择 Mac 默认快捷键。

**一点扩大**

- 每格右上角一颗扩大图标：点一下，这一格吃满整片工作区，其余格子收成右侧一小条
- 再点一次图标、或者点任意一条窄条，就按放大前的样子原样还原；`F1` 同效
- 其余格子收成 26pt 宽的窄条，两格分两段、三格分三段，每段写着竖排的目录名
- 还原是零误差的：动画全程只动 frame，四格的比例一次都没改过

**两套快捷键**

- 「编辑 → 快捷键」里切换：**特色快捷键**（默认，Windows 手感）/ **Mac 默认快捷键**
- Mac 默认套把 `F1` `F2` `F5` `Tab` 这些苹果键盘上有定义的键全部让给系统，改成 `⌘↑` 返回上一级、`回车` 重命名、`⌘I` / `⌥I` 显示简介、`⌘R` 刷新、`⌥⌘F` 最大化；字母与数字快速索引两套一致
- 切换立刻生效：菜单里的键位、侧边栏「快捷键」速查表同时变

**其他**

- 快捷栏可以整体挪到右边（「显示 → 快捷栏居右」），菜单标题随位置自动翻成「居左」
- 侧边栏速查表补上 `F1` 最大化
- 应用程序目录（`/Applications`、`~/Applications` 等）里禁用重命名与批量重命名 —— 改掉一个 `.app` 的名字会让它打不开
- 修：绿色系与系统浅色下，最大化图标是浅灰的、几乎看不见；点过之后还会变成蓝色
- 修：系统深色下，最大化图标悬停 / 点过之后同样会变成蓝色
- 修：鼠标停在窄条上时，格子自己的工具条和滚动条会透过封面显示出来
- 修：切换快捷键套之后，侧边栏的速查表要等切一次界面语言才更新

### English

Once I realized that people who use a Mac keyboard only would run into conflicts with this shortcut set, I decided to ship two sets. Mac mini users like me — or anyone else on a combined Windows/Mac keyboard — can keep the original set; Mac-keyboard-only users can switch to Mac defaults.

**Zoom one pane**

- A zoom icon in each pane's top-right corner: click it and that pane takes over the whole workspace while the others collapse into a narrow strip on the right
- Click the icon again, or click any strip, to restore exactly the pre-zoom layout; `F1` does the same
- The remaining panes become 26 pt strips — two panes give two segments, three give three — each showing its folder name vertically
- Restoring is pixel-exact: the animation only ever touches frames; the four-pane ratios are never recalculated

**Two shortcut sets**

- Switch under "Edit → Shortcuts": **Featured** (default, Windows feel) / **Mac defaults**
- The Mac set hands `F1` `F2` `F5` `Tab` — every key that Apple keyboards define — back to the system, and uses `⌘↑` up one level, `Return` rename, `⌘I` / `⌥I` Get Info, `⌘R` refresh, `⌥⌘F` maximize. Letter and number quick-index keys are the same in both sets
- Switching takes effect immediately: menu key equivalents and the sidebar cheat sheet update together

**Other**

- The shortcut bar can move to the right as a whole ("View → Shortcut bar on the right"), and the menu title flips to "left" accordingly
- The sidebar cheat sheet now lists `F1` maximize
- Rename and batch rename are disabled in application folders (`/Applications`, `~/Applications`, etc.) — renaming a `.app` breaks it
- Fixed: in the green theme on a light system appearance, the zoom icon was pale grey and nearly invisible, and turned blue once clicked
- Fixed: in system dark mode the zoom icon likewise turned blue on hover or after clicking
- Fixed: hovering a narrow strip let the pane's own toolbar and scrollers show through the cover
- Fixed: after switching shortcut sets, the sidebar cheat sheet only updated after switching the UI language once

---

## 1.8.2 — 2026-11-05

### 中文

**文件管理**

- 列表里删掉一个文件后，选择框落到自动补位的那一项，按上下左右继续走，不用再滚回去找
- 布局改成命名保存：`文件 → 保存布局…`（`⌘S`）只问一个名字，`读取布局` 子菜单里直接列出来；格子排列也一起存
- 新开标签（`⌘T`）复制当前标签的目录，从手头这一层继续
- 点指向文件夹的替身或软链接，在格子里打开，不再弹出访达窗口

**照片**

- 旋转到「编辑」菜单。当前选中的类型不支持旋转时（RAW / PNG / 文件夹）它是灰的

**其他**

- 关于窗口底部加上 macOS 与 Windows 两个下载地址，可以直接点开

### English

**File management**

- After you delete a file in list view, the selection lands on the item that fills the gap, so the arrow keys keep working without scrolling back to find it
- Layouts are now saved by name: "File → Save Layout…" (`⌘S`) asks only for a name, and the "Load Layout" submenu lists them directly; the pane arrangement is stored too
- New tab (`⌘T`) duplicates the current tab's folder, so you continue from where you are
- Clicking an alias or symlink that points to a folder opens it in the pane instead of popping up a Finder window

**Photos**

- Rotation moved to the "Edit" menu. It is greyed out when the current selection's type can't be rotated (RAW / PNG / folders)

**Other**

- Download links for macOS and Windows were added at the bottom of the About window; both can be clicked

---

## 1.8.1 — 2026-10-29

### 中文

首个公开版本。

**文件管理**

- 四宫格，四种布局（2×2 / 左右双格 / 上 2 下 1 / 左 1 右 2），随时切换
- 剪切是真的剪切：`⌘X` 标记、`⌘V` 移动，不复制
- 多标签，每格最多 6 个，可拖动换位、跨格移动、拖进侧栏变成书签
- 三档视图：详细列表 / 图标网格 / 大缩略图
- 搜索（`⌘F`）当前目录及子目录，支持 `*` `?` 通配符
- 撤销与重做：重命名、新建、旋转、颜色标签、删除、同卷移动与复制
- 恢复关闭的标签（`⇧⌘T`）
- 颜色标签与筛选，与访达共用同一份数据
- 侧边栏书签、路径地址栏、显示简介、反选、在这里打开终端（`⌃⌘T`）

**照片**

- 按住 `⌃` / `⌥` 或按中键，100% 原尺寸放大看局部，用于快速判断对焦
- 选中照片即在状态栏和预览栏显示快门、ISO、光圈、镜头、焦距、拍摄时间
- 只看图片、按拍摄时间排序
- 旋转（JPG / HEIC / TIFF）：只改 EXIF 方向，不重新编码，可撤销

**AI 图片**

- 读取 ComfyUI / A1111 图片的模型、LoRA、步数、CFG、采样器、调度器与提示词，一键复制

**其他**

- 批量重命名（`F2`），`PIC##` 自动编号，要么全成要么一个都不改
- 外接盘清理：一次移除 `.DS_Store`、`._xxx`、`.Spotlight-V100` 等 macOS 附加文件并推出
- 五种界面语言（简体中文 / 繁體中文 / English / 日本語 / 한국어），首次启动按系统语言
- 两套外观：跟随系统、绿色系
- 键位按键盘印字分配，Windows 与 Mac 键盘都能对上（`Tab` 返回上级、`Del` / `⌘⌫` 删除）

**安装**

- macOS 13 Ventura 或更新，Apple Silicon
- 未经 Apple 开发者签名，首次打开若提示「已损坏」，在终端执行一次 `xattr -cr /Applications/QuadCut.app`

### English

First public release.

**File management**

- Four panes, four layouts (2×2 / two side by side / two on top plus one below / one left plus two right), switchable at any time
- Cut is real cut: `⌘X` marks, `⌘V` moves — it does not copy
- Tabs, up to 6 per pane: drag to reorder, move across panes, or drop onto the sidebar to create a bookmark
- Three view modes: detailed list / icon grid / large thumbnails
- Search (`⌘F`) the current folder and its subfolders, with `*` and `?` wildcards
- Undo and redo: rename, new folder, rotate, color tag, delete, move and copy within a volume
- Reopen closed tabs (`⇧⌘T`)
- Color tags and filtering, sharing the same data as Finder
- Sidebar bookmarks, path bar, Get Info, invert selection, open Terminal here (`⌃⌘T`)

**Photos**

- Hold `⌃` / `⌥` or press the middle mouse button for a 100% loupe on a detail, for quick focus checking
- Selecting a photo shows shutter speed, ISO, aperture, lens, focal length and capture time in the status bar and preview pane
- Images only, sorted by capture time
- Rotate (JPG / HEIC / TIFF): EXIF orientation only, no re-encoding, undoable

**AI images**

- Read model, LoRA, steps, CFG, sampler, scheduler and prompt from ComfyUI / A1111 images, with one-click copy

**Other**

- Batch rename (`F2`) with `PIC##` auto-numbering — all or nothing
- External drive cleanup: remove `.DS_Store`, `._xxx`, `.Spotlight-V100` and similar macOS extras in one go, then eject
- Five UI languages (Simplified Chinese / Traditional Chinese / English / Japanese / Korean), picked from the system language on first launch
- Two appearances: follow system, and green
- Keys are assigned by what is printed on the keycap, so both Windows and Mac keyboards line up (`Tab` up one level, `Del` / `⌘⌫` delete)

**Install**

- macOS 13 Ventura or later, Apple Silicon
- Not signed with an Apple developer certificate. If macOS reports the app "is damaged" on first launch, run `xattr -cr /Applications/QuadCut.app` once in Terminal
