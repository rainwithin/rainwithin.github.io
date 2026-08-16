# Kaaovo 网站使用指南

> 这是一份写给「完全不懂编程」的你看的傻瓜式指南，照着做就行。

## 0. 一句话原理

你的网站，本质就是 `docs` 文件夹里的一堆文字文件（后缀 `.md`，叫 Markdown）。

**你要做的永远只有两件事：**
1. **改文件**（改文字 / 加文章 / 加图片）
2. **推送**（把改动上传到 GitHub，网站才更新）

改完不推送 = 只在你自己电脑上变了，网站不会变。

---

## 1. 文件夹结构（每个东西是干嘛的）

```
D:\Mywebsite
├── mkdocs.yml                ← 网站总配置：网站名、导航菜单在这改
├── README.md                 ← 就是这份指南
├── .gitignore                ← 不用管（自动忽略垃圾文件）
├── .github/workflows/ci.yml  ← 自动部署脚本，不用管
└── docs/                     ← ★ 所有网页内容都在这下面
    ├── index.md              ← 主页
    ├── course/               ← 课程板块
    │   ├── index.md          ←   课程首页（文章列表在这）
    │   ├── example.md        ←   示例文章（写作模板）
    │   ├── images/           ←   放图片
    │   └── files/            ←   放 PDF
    ├── friends/
    │   └── index.md          ← 友链板块
    └── about/
        └── index.md          ← 关于板块
```

---

## 2. 最常见的几处修改

### 2.1 改「网站名称」

用记事本打开 `mkdocs.yml`，找到这行：

```
site_name: "Kaaovo's personal website"
```

把引号里的字改掉，保存。

### 2.2 改「主页中央的大字」

用记事本打开 `docs/index.md`，找到这行大字：

```
Kaaovo's personal website
```

（它在一对 `<h1 ...>` 和 `</h1>` 之间）改掉它，保存。

### 2.3 改「顶部导航菜单」

用记事本打开 `mkdocs.yml`，找到 `nav:` 下面这几行：

```
nav:
  - 主页: index.md
  - 课程: course/index.md
  - 友链: friends/index.md
  - 关于: about/index.md
```

- 想改名字：改冒号左边的字（比如「主页」改成「首页」）
- 想加菜单：照格式加一行，冒号右边指向对应文件

### 2.4 改某个页面的文字

找到对应的 `.md` 文件 → 记事本打开 → 直接改文字 → 保存。

---

## 3. 写一篇新文章（新笔记）

1. 打开文件夹 `D:\Mywebsite\docs\course\`
2. 新建一个文件，名字随便起（建议用英文或拼音，比如 `first-note.md`）
3. 第一行写标题（一个 `#` 号 + 空格 + 标题）：

   ```
   # 我的第一篇笔记
   ```

4. 下面写正文（格式看第 6 节速查表）
5. 保存
6. 打开 `docs/course/index.md`，在「文章列表」里加一行，让别人能从课程首页点进来：

   ```
   - [我的第一篇笔记](first-note.md)
   ```

---

## 4. 加图片

1. 把图片文件丢进 `docs/course/images/` 文件夹
2. 在笔记里要显示图片的位置写一行：

   ```
   ![图片说明](images/你的图片名.png)
   ```

3. 保存、推送

---

## 5. 加 PDF

1. 把 PDF 丢进 `docs/course/files/` 文件夹
2. 两种写法二选一：

   - 只要个「点击链接」：

     ```
     [查看PDF](files/你的文件.pdf)
     ```

   - 直接「嵌在页面里翻页」：

     ```
     <embed src="files/你的文件.pdf" width="100%" height="600" type="application/pdf">
     ```

3. 保存、推送

---

## 6. Markdown 速查表（怎么写正文）

| 你想写的 | 怎么写 |
| --- | --- |
| 大标题 | `# 标题` |
| 小标题 | `## 小标题` |
| 更小标题 | `### 更小标题` |
| 加粗 | `**加粗**` |
| 斜体 | `*斜体*` |
| 无序列表 | `- 第一点` |
| 有序列表 | `1. 第一点` |
| 链接 | `[文字](网址)` |
| 图片 | `![说明](图片路径)` |
| 引用 | `> 引用的话` |
| 分割线 | `---` |

> 行内代码用一对反引号包住（键盘 Esc 键下面那个 `~` 键）；整段代码用三对反引号包住。这些可以照抄 `docs/course/example.md`。

---

## 7. 把改动发布到线上（★ 最重要的一步）

### 方式 A：本地推送（常用）

1. 按键盘 `Win + R`，输入 `powershell`，回车
2. 输入下面这行回车（进入网站文件夹）：

   ```
   cd D:\Mywebsite
   ```

3. 依次输入这三行（每行输完按回车）：

   ```
   git add .
   git commit -m "说明这次改了什么"
   git push
   ```

   - 第二行引号里的中文随便写，比如 `git commit -m "更新了主页"`

4. 如果 `git push` 时弹出来问你要账号密码：

   - `Username` 填：`rainwithin`
   - `Password` 填：你的 token（ghp_ 开头那串，输的时候屏幕不显示，是正常的，输完回车）

5. 等 1～2 分钟，刷新网站就能看到更新

> 前提：你的梯子（Clash）要开着，否则连不上 GitHub。

### 方式 B：GitHub 网页版（纯浏览器，不用本地电脑）

1. 打开 https://github.com/rainwithin/rainwithin.github.io
2. 改文字：点进某个 `.md` 文件 → 点右上角铅笔图标 ✏️ → 改 → 点绿色 Commit changes
3. 传图片/PDF：进到对应文件夹 → 点 Add file → Upload files → 拖文件进去 → Commit changes
4. 等 1～2 分钟自动更新

---

## 8. 本地预览（可选，改完先自己看看效果）

1. `Win + R` → 输入 `powershell` → 回车
2. 输入 `cd D:\Mywebsite` 回车
3. 输入 `py -m mkdocs serve` 回车
4. 浏览器打开 http://127.0.0.1:8000/
5. 改文件会自动刷新；看完在黑色窗口按 `Ctrl + C` 关闭

---

## 9. 常见问题

### Q: 网站打开是 404，或者改了没变化？
多半是浏览器缓存。按 `Ctrl + F5` 强刷，或等 1～2 分钟。

### Q: `git push` 报错连不上？
检查梯子（Clash）是不是开着。

### Q: 提示 token 过期 / 无效？
去 https://github.com/settings/tokens 重新生成一个（勾选 repo 和 workflow），把新 token 当密码用。

### Q: 我改坏了怎么办？
别慌，直接来找我，或者去 GitHub 网页版用「历史记录」回退。随时可以问我。

---

## 10. 一句话总结

> **改文件 → `git add .` → `git commit -m "说明"` → `git push` → 等 2 分钟看网站**
