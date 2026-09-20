# PPT 风格提示词生成器

在线访问:https://prefect12.github.io/ppt-style-prompts/

挑一个视觉风格,填上主题,生成一段可以直接丢给 AI(Claude、ChatGPT、Kimi、Gamma、Midjourney 等)的 PPT 提示词。

- 52 种风格,分 10 类:粗野拼贴、极简瑞士、复古、科技未来、纸感手作、商务咨询、东方文化、柔和可爱、暗色戏剧、插画图形
- 每种风格有六页范例:封面、章节、数据、图表、流程、引语,点小图切换大图
- 每种风格配了一套动效方案(硬切弹出、精确滑入、缓慢淡入、故障闪烁、打字机、柔和上浮、手绘描线、纸片落下、墨晕显现、数据生长、复古转场、印刷感共 12 种),预览里能直接播放;提示词里写明转场、入场、强调、时长缓动,以及在 PowerPoint / Keynote 里对应的动画名
- 动效强度三档:克制、丰富、不要动效
- 可以改五个配色,改完提示词里的色值同步更新
- 四种输出目标:通用对话 AI、HTML 单文件幻灯片、Gamma / Canva / WPS AI、图像模型逐页出图
- 搜索、分类筛选、收藏(存在浏览器本地)、随机、复制、下载 .txt
- 单个 `index.html`,不依赖任何外部资源,断网也能用;链接带 `#风格id` 可以直接分享某个风格

## 本地使用

双击 `index.html` 用浏览器打开即可。

## 发布到 GitHub Pages

1. 登录 GitHub,右上角 **+** → **New repository**。名字随意,例如 `ppt-style-prompts`,选 **Public**,点 **Create repository**。
2. 在新仓库页面点 **uploading an existing file**,把 `index.html` 和 `README.md` 拖进去,点 **Commit changes**。
3. 进入仓库的 **Settings** → 左侧 **Pages**。**Source** 选 **Deploy from a branch**,**Branch** 选 `main`、目录选 `/ (root)`,点 **Save**。
4. 等一两分钟,页面顶部会出现网址:`https://你的用户名.github.io/ppt-style-prompts/`。

用命令行的话:

```bash
cd ppt-style-prompts
git init && git add . && git commit -m "PPT style prompt generator"
git branch -M main
git remote add origin https://github.com/你的用户名/ppt-style-prompts.git
git push -u origin main
# 然后到 Settings → Pages 里按第 3 步开启
```

## 添加新风格

打开 `index.html`,找到 `var STYLES=[`,照下面的格式加一条:

```js
{id:"myStyle", zh:"中文名", en:"English Name", cat:"复古",
 c:["#背景","#文字","#主色","#辅色","#点缀"],
 t:{g:"dots", bw:.1, r:.4, sh:"hard", tf:"sans", tw:800, tag:"pill"},
 look:"背景与整体视觉。", comp:"组件一;组件二;组件三", type:"字体与排版。",
 mood:"气质。", avoid:"不要出现的东西。", kw:"english, style, keywords"}
```

`t` 只影响缩略图:`g` 底纹(dots / lines / scan / rule / half / frame / frame2 / persp / grain / none),`bw` 描边粗细,`r` 圆角,`sh` 阴影(hard / soft / glow / clay / neu / none),`tf` 标题字体(sans / serif / mono / round / cond),`tag` 标签样式,`rot` 卡片微旋转,`deco` 装饰图形,`grad` 自定义背景渐变。进入提示词的是 `look`、`comp`、`type`、`mood`、`avoid`、`kw` 和配色。动效在 `MOMAP` 里给新风格的 id 指定一个方案名(snap / print / swiss / fade / glow / type / float / draw / paper / ink / data / retro),不指定则用 fade。`comp` 用分号分隔,会被拆成编号列表。
