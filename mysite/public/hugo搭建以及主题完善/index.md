# Hugo搭建以及主题完善


## hugo搭建

### mac

1.  安装hugo

>brew install hugo

2. 创建博客
>hugo new site myblog

3. 创建主题
>cd site_name
git init
git submodule add https://github.com/dillonzq/LoveIt.git themes/LoveIt
(git clone https://github.com/dillonzq/LoveIt.git themes/LoveIt 也可以)
echo theme = "LoveIt" >> hugo.toml

当然你也可以选择其他的主题，方法与之类似

4. 修改配置
你知道的，hugo.toml里面就是你整个博客的配置，包括博客名称，作者名字，头像，联系方式等，直接上模板
```
baseURL = "https://your-domain.org"

# 更改使用 Hugo 构建网站时使用的默认主题
theme = "LoveIt"

# 网站标题
title = "Stilig"
defaultContentLanguage = "zh-cn"
# 网站语言, 仅在这里 CN 大写 ["en", "zh-CN", "fr", "pl", ...]
languageCode = "zh-CN"
# 语言名称 ["English", "简体中文", "Français", "Polski", ...]
languageName = "简体中文"

# 是否包括中日韩文字
hasCJKLanguage = true

# 默认每页列表显示的文章数目
paginate = 12
# 谷歌分析代号 [UA-XXXXXXXX-X]
googleAnalytics = ""
# 版权描述，仅仅用于 SEO
copyright = ""

# 是否使用 robots.txt
enableRobotsTXT = true
# 是否使用 git 信息
#enableGitInfo = true
# 是否使用 emoji 代码
enableEmoji = true

# 忽略一些构建错误
ignoreErrors = ["error-remote-getjson", "error-missing-instagram-accesstoken"]

# 作者配置
[author]
  name = "Stilig"
  email = "your_email"

# 菜单配置
[menu]
  [[menu.main]]
    weight = 1
    identifier = "posts"
    # 你可以在名称 (允许 HTML 格式) 之前添加其他信息, 例如图标
    pre = ""
    # 你可以在名称 (允许 HTML 格式) 之后添加其他信息, 例如图标
    post = ""
    name = "文章"
    url = "/posts/"
    # 当你将鼠标悬停在此菜单链接上时, 将显示的标题
    title = ""
  [[menu.main]]
    weight = 2
    identifier = "tags"
    pre = ""
    post = ""
    name = "标签"
    url = "/tags/"
    title = ""
  [[menu.main]]
    weight = 3
    identifier = "categories"
    pre = ""
    post = ""
    name = "分类"
    url = "/categories/"
    title = ""

# Hugo 解析文档的配置
[markup]
  # 语法高亮设置 (https://gohugo.io/content-management/syntax-highlighting)
  [markup.highlight]
    # false 是必要的设置 (https://github.com/dillonzq/LoveIt/issues/158)
    codeFences = true
    guessSyntax = true
    lineNos = true
    lineNumbersInTable = true
    # false 是必要的设置
    # (https://github.com/dillonzq/LoveIt/issues/158)
    # Goldmark 是 Hugo 0.60 以来的默认 Markdown 解析库
    noClasses = false
  # Goldmark 是 Hugo 0.60 以来的默认 Markdown 解析库
  [markup.goldmark]
    [markup.goldmark.extensions]
      definitionList = true
      footnote = true
      linkify = true
      strikethrough = true
      table = true
      taskList = true
      typographer = true
    [markup.goldmark.renderer]
      # 是否在文档中直接使用 HTML 标签
      unsafe = true
  # 目录设置
  [markup.tableOfContents]
    startLevel = 2
    endLevel = 6
[params]
  # 网站默认主题样式 ["auto", "light", "dark"]
  defaultTheme = "light"
  # 公共 git 仓库路径，仅在 enableGitInfo 设为 true 时有效
  #gitRepo = ""
  # LoveIt 新增 | 0.1.1 哪种哈希函数用来 SRI, 为空时表示不使用 SRI
  # ["sha256", "sha384", "sha512", "md5"]
  fingerprint = "sha256"
  # LoveIt 新增 | 0.2.0 日期格式
  dateFormat = "2006-01-02"
  # 网站标题, 用于 Open Graph 和 Twitter Cards
  title = "Stilig的博客"
  # 网站描述, 用于 RSS, SEO, Open Graph 和 Twitter Cards
  description = "Stilig的博客"
  # 网站图片, 用于 Open Graph 和 Twitter Cards
  images = ["首页中间的图片"]

# 页面头部导航栏配置
[params.header]
  # 桌面端导航栏模式 ["fixed", "normal", "auto"]
  desktopMode = "normal"
  # 移动端导航栏模式 ["fixed", "normal", "auto"]
  mobileMode = "normal"
  # LoveIt 新增 | 0.2.0 页面头部导航栏标题配置
  [params.header.title]
    # LOGO 的 URL
    logo = ""
    # 标题名称
    name = "Stilig"
    # 你可以在名称 (允许 HTML 格式) 之前添加其他信息, 例如图标
    pre = ""
    # 你可以在名称 (允许 HTML 格式) 之后添加其他信息, 例如图标
    post = ""
    # LoveIt 新增 | 0.2.5 是否为标题显示打字机动画
    typeit = false

# 页面底部信息配置
[params.footer]
  enable = true
  # LoveIt 新增 | 0.2.0 自定义内容 (支持 HTML 格式)
  custom = ''
  # LoveIt 新增 | 0.2.0 是否显示 Hugo 和主题信息
  hugo = false
  # LoveIt 新增 | 0.2.0 是否显示版权信息
  copyright = true
  # LoveIt 新增 | 0.2.0 是否显示作者
  author = true
  # 网站创立年份
  since = 2022
  # ICP 备案信息，仅在中国使用 (支持 HTML 格式)
  icp = ''
  # 许可协议信息 (支持 HTML 格式)
  license = '<a rel="license external nofollow noopener noreffer" href="https://creativecommons.org/licenses/by-nc/4.0/" target="_blank">CC BY-NC 4.0</a>'

# LoveIt 新增 | 0.2.0 Section (所有文章) 页面配置
[params.section]
  # section 页面每页显示文章数量
  paginate = 20
  # 日期格式 (月和日)
  dateFormat = "01-02"
  # RSS 文章数目
  rss = 10

# LoveIt 新增 | 0.2.0 List (目录或标签) 页面配置
[params.list]
  # list 页面每页显示文章数量
  paginate = 20
  # 日期格式 (月和日)
  dateFormat = "01-02"
  # RSS 文章数目
  rss = 10

# LoveIt 新增 | 0.2.0 应用图标配置
[params.app]
  # 当添加到 iOS 主屏幕或者 Android 启动器时的标题, 覆盖默认标题
  title = ""
  # 是否隐藏网站图标资源链接
  noFavicon = false
  # 更现代的 SVG 网站图标, 可替代旧的 .png 和 .ico 文件
  svgFavicon = ""
  # Android 浏览器主题色
  themeColor = "#ffffff"
  # Safari 图标颜色
  iconColor = "#5bbad5"
  # Windows v8-10磁贴颜色
  tileColor = "#da532c"

# LoveIt 新增 | 0.2.0 搜索配置
[params.search]
  enable = true
  # 搜索引擎的类型 ["lunr", "algolia"]
  type = "algolia"
  # 文章内容最长索引长度
  contentLength = 4000
  # 搜索框的占位提示语
  placeholder = ""
  # LoveIt 新增 | 0.2.1 最大结果数目
  maxResultLength = 10
  # LoveIt 新增 | 0.2.3 结果内容片段长度
  snippetLength = 50
  # LoveIt 新增 | 0.2.1 搜索结果中高亮部分的 HTML 标签
  highlightTag = "em"
  # LoveIt 新增 | 0.2.4 是否在搜索索引中使用基于 baseURL 的绝对路径
  absoluteURL = false
  ##注册使用，前往：https://www.algolia.com/
  [params.search.algolia]
    index = ""
    appID = ""
    searchKey = ""

# 主页配置
[params.home]
  # LoveIt 新增 | 0.2.0 RSS 文章数目
  rss = 10
  # 主页个人信息
  [params.home.profile]
    enable = true
    # Gravatar 邮箱，用于优先在主页显示的头像
    gravatarEmail = ""
    # 主页显示头像的 URL
    avatarURL = ""
    # LoveIt 更改 | 0.2.7 主页显示的网站标题 (支持 HTML 格式)
    title = ""
    # 主页显示的网站副标题 (允许 HTML 格式)
    subtitle = "欢迎来到我的博客"
    # 是否为副标题显示打字机动画
    typeit = true
    # 是否显示社交账号
    social = true
    # LoveIt 新增 | 0.2.0 免责声明 (支持 HTML 格式)
    disclaimer = ""
  # 主页文章列表
  [params.home.posts]
    enable = true
    # 主页每页显示文章数量
    paginate = 6
    # LoveIt 删除 | 0.2.0 被 params.page 中的 hiddenFromHomePage 替代
    # 当你没有在文章前置参数中设置 "hiddenFromHomePage" 时的默认行为
    defaultHiddenFromHomePage = false

# 作者的社交信息设置
[params.social]
  GitHub = ""
  Linkedin = ""
  Twitter = ""
  Instagram = ""
  Facebook = ""
  Telegram = ""
  Medium = ""
  Gitlab = ""
  Youtubelegacy = ""
  Youtubecustom = ""
  Youtubechannel = ""
  Tumblr = ""
  Quora = ""
  Keybase = ""
  Pinterest = ""
  Reddit = ""
  Codepen = ""
  FreeCodeCamp = ""
  Bitbucket = ""
  Stackoverflow = ""
  Weibo = ""
  Odnoklassniki = ""
  VK = ""
  Flickr = ""
  Xing = ""
  Snapchat = ""
  Soundcloud = ""
  Spotify = ""
  Bandcamp = ""
  Paypal = ""
  Fivehundredpx = ""
  Mix = ""
  Goodreads = ""
  Lastfm = ""
  Foursquare = ""
  Hackernews = ""
  Kickstarter = ""
  Patreon = ""
  Steam = ""
  Twitch = ""
  Strava = ""
  Skype = ""
  Whatsapp = ""
  Zhihu = ""
  Douban = ""
  Angellist = ""
  Slidershare = ""
  Jsfiddle = ""
  Deviantart = ""
  Behance = ""
  Dribbble = ""
  Wordpress = ""
  Vine = ""
  Googlescholar = ""
  Researchgate = ""
  Mastodon = ""
  Thingiverse = ""
  Devto = ""
  Gitea = ""
  XMPP = ""
  Matrix = ""
  Bilibili = ""
  Discord = ""
  DiscordInvite = ""
  Lichess = ""
  ORCID = ""
  Pleroma = ""
  Kaggle = ""
  MediaWiki= ""
  Plume = ""
  HackTheBox = ""
  RootMe= ""
  Phone = ""
  Email = ""
  RSS = true # LoveIt 新增 | 0.2.0

# LoveIt 更改 | 0.2.0 文章页面全局配置
[params.page]
  # LoveIt 新增 | 0.2.0 是否在主页隐藏一篇文章
  hiddenFromHomePage = false
  # LoveIt 新增 | 0.2.0 是否在搜索结果中隐藏一篇文章
  hiddenFromSearch = false
  # LoveIt 新增 | 0.2.0 是否使用 twemoji
  twemoji = false
  # 是否使用 lightgallery
  lightgallery = false
  # LoveIt 新增 | 0.2.0 是否使用 ruby 扩展语法
  ruby = true
  # LoveIt 新增 | 0.2.0 是否使用 fraction 扩展语法
  fraction = true
  # LoveIt 新增 | 0.2.0 是否使用 fontawesome 扩展语法
  fontawesome = true
  # 是否在文章页面显示原始 Markdown 文档链接
  linkToMarkdown = false
  # LoveIt 新增 | 0.2.4 是否在 RSS 中显示全文内容
  rssFullText = false
  # LoveIt 新增 | 0.2.0 目录配置
  [params.page.toc]
    # 是否使用目录
    enable = true
    # LoveIt 新增 | 0.2.9 是否保持使用文章前面的静态目录
    keepStatic = false
    # 是否使侧边目录自动折叠展开
    auto = true
  # LoveIt 新增 | 0.2.0 代码配置
  [params.page.code]
    # 是否显示代码块的复制按钮
    copy = true
    # 默认展开显示的代码行数
    maxShownLines = 50
# LoveIt 更改 | 0.2.0 KaTeX 数学公式
[params.page.math]
  enable = true
  # LoveIt 更改 | 0.2.11 默认行内定界符是 $ ... $ 和 \( ... \)
  inlineLeftDelimiter = ""
  inlineRightDelimiter = ""
  # LoveIt 更改 | 0.2.11 默认块定界符是 $$ ... $$, \[ ... \], \begin{equation} ... \end{equation} 和一些其它的函数
  blockLeftDelimiter = ""
  blockRightDelimiter = ""
  # KaTeX 插件 copy_tex
  copyTex = true
  # KaTeX 插件 mhchem
  mhchem = true
# LoveIt 新增 | 0.2.0 Mapbox GL JS 配置
[params.page.mapbox]
  # Mapbox GL JS 的 access token
  accessToken = ""
  # 浅色主题的地图样式
  lightStyle = "mapbox://styles/mapbox/light-v10?optimize=true"
  # 深色主题的地图样式
  darkStyle = "mapbox://styles/mapbox/dark-v10?optimize=true"
  # 是否添加 NavigationControl
  navigation = true
  # 是否添加 GeolocateControl
  geolocate = true
  # 是否添加 ScaleControl
  scale = true
  # 是否添加 FullscreenControl
  fullscreen = true
# LoveIt 更改 | 0.2.0 文章页面的分享信息设置
[params.page.share]
  enable = true
  Twitter = true
  Facebook = true
  Linkedin = true
  Whatsapp = false
  Pinterest = false
  Tumblr = false
  HackerNews = false
  Reddit = false
  VK = false
  Buffer = false
  Xing = false
  Line = true
  Instapaper = false
  Pocket = false
  Flipboard = false
  Weibo = true
  Blogger = false
  Baidu = false
  Odnoklassniki = false
  Evernote = false
  Skype = false
  Trello = false
  Mix = false
# LoveIt 更改 | 0.2.0 评论系统设置
[params.page.comment]
  enable = false
  # Disqus 评论系统设置
  [params.page.comment.disqus]
    # LoveIt 新增 | 0.1.1
    enable = false
    # Disqus 的 shortname，用来在文章中启用 Disqus 评论系统
    shortname = ""
  # Gitalk 评论系统设置
  [params.page.comment.gitalk]
    # LoveIt 新增 | 0.1.1
    enable = false
    owner = ""
    repo = ""
    clientId = ""
    clientSecret = ""
  # Valine 评论系统设置
  [params.page.comment.valine]
    enable = false
    appId = ""
    appKey = ""
    placeholder = ""
    avatar = "mp"
    meta= ""
    pageSize = 10
    # 为空时自动适配当前主题 i18n 配置
    lang = ""
    visitor = true
    recordIP = true
    highlight = true
    enableQQ = false
    serverURLs = ""
    # LoveIt 新增 | 0.2.6 emoji 数据文件名称, 默认是 "google.yml"
    # ["apple.yml", "google.yml", "facebook.yml", "twitter.yml"]
    # 位于 "themes/LoveIt/assets/lib/valine/emoji/" 目录
    # 可以在你的项目下相同路径存放你自己的数据文件:
    # "assets/lib/valine/emoji/"
    emoji = ""
  # Facebook 评论系统设置
  [params.page.comment.facebook]
    enable = false
    width = "100%"
    numPosts = 10
    appId = ""
    # 为空时自动适配当前主题 i18n 配置
    languageCode = "zh_CN"
# LoveIt 新增 | 0.2.0 Telegram Comments 评论系统设置
[params.page.comment.telegram]
  enable = false
  siteID = ""
  limit = 5
  height = ""
  color = ""
  colorful = true
  dislikes = false
  outlined = false
# LoveIt 新增 | 0.2.0 Commento 评论系统设置
[params.page.comment.commento]
  enable = false
# LoveIt 新增 | 0.2.5 utterances 评论系统设置
[params.page.comment.utterances]
  enable = false
  # owner/repo
  repo = ""
  issueTerm = "pathname"
  label = ""
  lightTheme = "github-light"
  darkTheme = "github-dark"
# giscus comment 评论系统设置 (https://giscus.app/zh-CN)
[params.page.comment.giscus]
  # 你可以参考官方文档来使用下列配置
  enable = false
  repo = ""
  repoId = ""
  category = "Announcements"
  categoryId = ""
  # 为空时自动适配当前主题 i18n 配置
  lang = ""
  mapping = "pathname"
  reactionsEnabled = "1"
  emitMetadata = "0"
  inputPosition = "bottom"
  lazyLoading = false
  lightTheme = "light"
  darkTheme = "dark"
# LoveIt 新增 | 0.2.7 第三方库配置
[params.page.library]
  [params.page.library.css]
    # someCSS = "some.css"
    # 位于 "assets/"
    # 或者
    # someCSS = "https://cdn.example.com/some.css"
  [params.page.library.js]
    # someJavascript = "some.js"
    # 位于 "assets/"
    # 或者
    # someJavascript = "https://cdn.example.com/some.js" 
# LoveIt 更改 | 0.2.10 页面 SEO 配置
[params.page.seo]
  # 图片 URL
  images = []
  # 出版者信息
  [params.page.seo.publisher]
    name = ""
    logoUrl = ""

# LoveIt 新增 | 0.2.5 TypeIt 配置
[params.typeit]
  # 每一步的打字速度 (单位是毫秒)
  speed = 100
  # 光标的闪烁速度 (单位是毫秒)
  cursorSpeed = 1000
  # 光标的字符 (支持 HTML 格式)
  cursorChar = "|"
  # 打字结束之后光标的持续时间 (单位是毫秒, "-1" 代表无限大)
  duration = -1

# 网站验证代码，用于 Google/Bing/Yandex/Pinterest/Baidu
[params.verification]
  google = ""
  bing = ""
  yandex = ""
  pinterest = ""
  baidu = ""

# LoveIt 新增 | 0.2.10 网站 SEO 配置
[params.seo]
  # 图片 URL
  image = ""
  # 缩略图 URL
  thumbnailUrl = ""

# LoveIt 新增 | 0.2.0 网站分析配置
[params.analytics]
  enable = true
  [params.analytics.google]
    id = ""
    # whether to anonymize IP
    # 是否匿名化用户 IP
    anonymizeIP = true
   # Fathom Analytics
   # 百度统计,自己配置的
  [params.analytics.baidu]
    id = ""
#  Cookie 许可配置
#[params.cookieconsent]
  #enable = true
  # 用于 Cookie 许可横幅的文本字符串
  #[params.cookieconsent.content]
    #message = ""
    #dismiss = ""
    #link = ""

#  第三方库文件的 CDN 设置
[params.cdn]
  # CDN 数据文件名称, 默认不启用
  # ["jsdelivr.yml"]
  # 位于 "themes/LoveIt/assets/data/cdn/" 目录
  # 可以在你的项目下相同路径存放你自己的数据文件:
  # "assets/data/cdn/"
  data = ""

#  兼容性设置
[params.compatibility]
  # 是否使用 Polyfill.io 来兼容旧式浏览器
  polyfill = false
  # 是否使用 object-fit-images 来兼容旧式浏览器
  objectFit = false
# 网站地图配置
[sitemap]
  changefreq = "weekly"
  filename = "sitemap.xml"
  priority = 0.5

# Permalinks 配置
[Permalinks]
  # posts = ":year/:month/:filename"
  posts = ":filename"

# 隐私信息配置
[privacy]
  #  Google Analytics 相关隐私 (被 params.analytics.google 替代)
  [privacy.googleAnalytics]
    # ...
  [privacy.twitter]
    enableDNT = true
  [privacy.youtube]
    privacyEnhanced = true

# 用于输出 Markdown 格式文档的设置
[mediaTypes]
  [mediaTypes."text/plain"]
    suffixes = ["md"]

# 用于输出 Markdown 格式文档的设置
[outputFormats.MarkDown]
  mediaType = "text/plain"
  isPlainText = true
  isHTML = false

# 用于 Hugo 输出文档的设置
[outputs]
  home = ["HTML", "RSS", "JSON"]
  page = ["HTML", "MarkDown"]
  section = ["HTML", "RSS"]
  taxonomy = ["HTML", "RSS"]
  taxonomyTerm = ["HTML"]

```

5. 创建文章
创建文章和hexo很像
>hugo new posts/my-first-post.md

6. 启动
>hugo server

哎？为什么我看不到文章啊？因为你创建的.md中draft:true是不显示的样子，改成false就行啦，一般hugo会运行在1313端口，别冲突了

### windows&linux

如果你是这两个系统，直接去官网https://gohugo.io/installation/ ，当然Linux应该是可以直接apt的,其他的和mac一样

## hugo完善

### 前提

把自己的hugo.toml里面的个人信息和网站信息配置好了，要不然会很乱。

### 文章模板

在你的mysite/archetypes/default.md文件里添加以下内容：
```
---
title: "{{ replace .TranslationBaseName "-" " " | title }}"
subtitle: ""
date: {{ .Date }}
lastmod: {{ .Date }}
draft: true
author: ""
authorLink: ""
license: ""

tags: [""]
categories: [""]

featuredImage: ""
featuredImagePreview: ""

summary: ""

hiddenFromHomePage: false
hiddenFromSearch: false

toc:
  enable: true
  auto: true

mapbox:
share:
  enable: true
comment:
  enable: true
---

```

这是我个人比较喜欢的模板，你可以根据自己的喜好修改。

### 添加统计功能

在your_site\layouts\partials\plugin\下创建busuanzi.html文件，写入
```
{{ if .params.enable }}
    {{ if eq .bsz_type "footer" }}
        {{/* 只有 footer 才刷新，防止页面进行多次调用，计数重复; 只要启用就计数，显示与否看具体设置 */}}
        <script async src=" //busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js "></script>
    {{ end }}

    {{ if or (eq .params.site_pv true) (eq .params.site_uv true) (eq .params.page_pv true) }}
        {{ if eq .bsz_type "footer" }}
            <section>
                {{ if eq .params.site_pv true }}
                    <span id="busuanzi_container_value_site_pv">
                        {{- with .params.page_pv_pre -}}
                            {{ . | safeHTML }}
                        {{ end }}
                        <span id="busuanzi_value_site_pv"></span>
                    </span>
                {{ end }}

                {{ if and (eq .params.site_pv true) (eq .params.site_uv true) }}
                    &nbsp;|&nbsp;              
                {{ end }}

                {{ if eq .params.site_uv true }}
                    <span id="busuanzi_container_value_site_uv">
                        {{- with .params.site_uv_pre -}}
                            {{ . | safeHTML }}
                        {{ end }}
                        <span id="busuanzi_value_site_uv"></span>
                    </span>
                {{ end }}
            </section>
        {{ end }}

        {{/*  page pv 只在 page 显示  */}}
        {{ if and (eq .params.page_pv true) (eq .bsz_type "page-reading") }}
            <span id="busuanzi_container_value_page_pv">
                {{- with .params.page_pv_pre -}}
                    {{ . | safeHTML }}
                {{ end }}
                <span id="busuanzi_value_page_pv"></span>&nbsp;
                {{- T "views" -}}
            </span>
        {{ end }}
    {{ end }}
{{ end }}

```

然后在hugo.toml里添加
```
# 添加不蒜子计数
[params.busuanzi]
  enable = true
  # 是否开启全站独立访客数
  site_uv = true
  # 全站独立访客数前的图标或提示语
  site_uv_pre = '<i class="fa fa-user"></i>' 
  # 全站独立访客数后的图标或提示语
  site_uv_post = ''
  # 是否开启全站浏览量
  site_pv = true
  # 全站浏览量前的图标或提示语
  site_pv_pre = '<i class="fa fa-eye"></i>'
  # 全站浏览量后的图标或提示语
  site_pv_post = ''
  # 是否开启单页浏览量
  page_pv = true
  # 单页浏览量前的图标或提示语
  page_pv_pre = '<i class="far fa-eye fa-fw"></i>'
  # 单页浏览量后的图标或提示语
  page_pv_post = ''

```

#### 页脚统计

把your_site\themes\LoveIt\layouts\partials\footer.html复制粘贴到路径your_site\layouts\partials\下。 再修改文件your_site\layouts\partials\footer.html，在最后三行
```
        </div>
    </footer>
{{- end -}}

```
前面添加

```
{{- /* busuanzi plugin */ -}}
{{- partial "plugin/busuanzi.html" (dict "params" .Site.Params.busuanzi "bsz_type" "footer") -}}

```
然后你就无敌了

#### 文章统计

把your_site\themes\LoveIt\layouts\posts\single.html复制粘贴到路径your_site\layouts\posts\下。再在your_site\layouts\posts\single.html中找到第二个<div class="post-meta-line">标签，并在该标签下添加下面的代码

```

{{- /* busuanzi plugin */ -}}
{{- partial "plugin/busuanzi.html" (dict "params" .Site.Params.busuanzi "bsz_type" "page-reading") -}}

```

### 文章加密

如果文章不想给别人看，但是自己又写完了，哎，这就很烦，怎么办呢，单独页面加密就好了
将your_site\themes\LoveIt\layouts\posts\single.html复制粘贴到your_site\layouts\posts\路径下。打开your_site\layouts\posts\single.html文件，在{{- $params := .Scratch.Get "params" -}}下添加下面内容：

```
    {{- $password := $params.password | default "" -}}
    {{- if ne $password "" -}}
		<script>
			(function(){
				if({{ $password }}){
					if (prompt('请输入文章密码') != {{ $password }}){
						alert('密码错误！');
						if (history.length === 1) {
							window.opener = null;
							window.open('', '_self');
							window.close();
						} else {
							history.back();
						}
					}
				}
			})();
		</script>
    {{- end -}}

```

之后我们只要将 password 参数添加到文章头即可。

但为了方便起见，我这里直接把它加到了模板文件中，即在博客的根目录下找到your_site\archetypes\default.md并打开，把 password 参数添加进去，如下代码块：

```
---
title: "{{ replace .TranslationBaseName "-" " " | title }}"
slug: "{{ replace .TranslationBaseName "-" " " | title }}"
...
...
password: ""
...
...
---

```

### 修改二级标题，行内代码和分割线等样式

#### 二级标题的修改

原主题的二级标题我不好评价，它跟下一级的标题几乎区分不开，这导致文章看起来没有条理。因此在这里我们将修改二级标题的样式以做区分。

找到your_site\assets\css\_custom.scss文件，在里面添加如下内容：

```

/* 标题 */
.page.single h2 {
  box-shadow: rgb(95, 90, 75) 0px 0px 0px 1px, rgba(10, 10, 0, 0.5) 1px 1px 6px 1px;
  color: rgb(255, 255, 255);
  font-family: 微软雅黑, 宋体, 黑体, Arial;
  font-weight: bold;
  line-height: 1.3;
  text-shadow: rgb(34, 34, 34) 2px 2px 3px;
  background: rgb(43, 102, 149);
  border-radius: 6px;
  border-width: initial;
  border-style: none;
  border-color: initial;
  border-image: initial;
  padding: 7px;
  margin: 18px 0px 18px -5px !important;
}

```

#### 行内代码

原主题的行内代码能用，但只能用一点点，实在是与正文区分不开，所以在这修改一下它的样式。

找到your_site\assets\css\_custom.scss文件，在里面添加如下内容：

```

/* 行内代码块 */
code {
  margin: 0 .2rem;
  font-size: .9em;
  border: 1px solid #d6d6d6;
  border-radius: .2rem;
}

/* 预格式代码块(用tab键插入的代码块) */
pre code {
  margin: 0;
  border: none;
  font-size: .875rem;
}

/* 标题里的代码块样式 */
.page.single .content>h2 code {
  color: #f7ab01;
  background: transparent !important;
  border: none;
}

```

#### 分割线

在原主题中分割线几乎看不到，这里修改一下。

找到your_site\assets\css\_custom.scss文件，在里面添加如下内容：

```

/* 分隔线 */
hr {
  border: none;
  border-bottom: 2px dashed #7a7a7a !important;
}

```

#### 页脚分割线

页脚内容与其他内容连在一起有点杂乱，因此添加一个页脚的分割线还是很有必要的。

找到your_site\assets\css\_custom.scss文件，在里面添加如下内容：

```
/* 页脚分割线 */
.footer {
  display: block;
border-top-width: 3px;
  border-top-style: solid;
  border-top-color: #96c1db;
  position: relative;
  z-index: -1;
  max-width: 800px;
  width: 60%;
  margin: .5rem auto 0 auto;
padding-left: 0rem;
padding-right: 0rem;
}
@media only screen and (max-width: 1440px) {
  .footer {
      width:54.5%
  }
}
@media only screen and (max-width: 1200px) {
  .footer {
      width:50.5%
  }
}
@media only screen and (max-width: 960px) {
  .footer {
      width: 77%
  }
}
@media only screen and (max-width: 680px) {
  .footer {
      width: 95%
  }
}

```

### 友链

#### 添加友链卡片

##### 添加friend.html文件

在your_site\layouts\shortcodes\路径下，新创建文件friend.html，并且在里面添加如下内容：

```
{{ if .IsNamedParams }}
{{- $src := .Get "logo" -}}
{{- $small := .Get "logo_small" | default $src -}}
{{- $large := .Get "logo_large" | default $src -}}
<div class="friend-div">
  <a target="_blank" href={{ .Get "url" | safeURL }} title={{ .Get "name" }} >
  <img class="lazyload"
       src="/svg/loading.min.svg"
       data-src={{ $src | safeURL }}
       alt={{ .Get "name" }}
  data-sizes="auto"
  data-srcset="{{ $small | safeURL }}, {{ $src | safeURL }} 1.5x, {{ $large | safeURL }} 2x" />
  <span class="friend-name">{{ .Get "name" }}</span>
  <span class="friend-info">{{ .Get "word" }}</span>
  </a>
</div>
{{ end }}

```
##### 添加_friend.scss文件

在your_site\assets\css\_partial\_single\路径下（如果没有就自己创建），新建文件_friend.scss，并在里面添加如下内容：

```
#article-container {
 word-wrap: break-word;
 overflow-wrap: break-word
}

#article-container a {
 color: #49b1f5
}

#article-container a:hover {
 text-decoration: underline
}

#article-container img {
 margin: 0 auto .8rem
}

.flink#article-container .friend-list-div > .friend-div a .friend-info,
.flink#article-container .friend-list-div > .friend-div a .friend-name {
 overflow: hidden;
 -o-text-overflow: ellipsis;
 text-overflow: ellipsis;
 white-space: nowrap
}

.flink#article-container .friend-list-div {
 overflow: auto;
 padding: 10px 10px 0;
 text-align: center;
}
.flink#article-container .friend-list-div > .friend-div {
 position: relative;
 float: left;
 overflow: hidden;
 margin: 15px 7px;
 width: calc(100% / 3 - 15px);
 height: 90px;
 border-radius: 8px;
 line-height: 17px;
 -webkit-transform: translateZ(0)
}

@media screen and (max-width: 1100px) {
 .flink#article-container .friend-list-div > .friend-div {
  width: calc(50% - 15px) !important
 }

@media screen and (max-width: 600px) {
 .flink#article-container .friend-list-div > .friend-div {
  width: calc(100% - 15px) !important
 }
}
}

.flink#article-container .friend-list-div > .friend-div:hover {
 background: rgba(87, 142, 224, 0.15);
}

.flink#article-container .friend-list-div > .friend-div:hover img {
 -webkit-transform: rotate(360deg);
 -moz-transform: rotate(360deg);
 -o-transform: rotate(360deg);
 -ms-transform: rotate(360deg);
 transform: rotate(360deg)
}

.flink#article-container .friend-list-div > .friend-div:before {
 position: absolute;
 top: 0;
 right: 0;
 bottom: 0;
 left: 0;
 z-index: -1;
 background: var(--text-bg-hover);
 content: '';
 -webkit-transition: -webkit-transform .3s ease-out;
 -moz-transition: -moz-transform .3s ease-out;
 -o-transition: -o-transform .3s ease-out;
 -ms-transition: -ms-transform .3s ease-out;
 transition: transform .3s ease-out;
 -webkit-transform: scale(0);
 -moz-transform: scale(0);
 -o-transform: scale(0);
 -ms-transform: scale(0);
 transform: scale(0)
}
.flink#article-container .friend-list-div > .friend-div:hover:before,
.flink#article-container .friend-list-div > .friend-div:focus:before,
.flink#article-container .friend-list-div > .friend-div:active:before {
 -webkit-transform: scale(1);
 -moz-transform: scale(1);
 -o-transform: scale(1);
 -ms-transform: scale(1);
 transform: scale(1)
}
.flink#article-container .friend-list-div > .friend-div a {
 color: var(--font-color);
 text-decoration: none
}

.flink#article-container .friend-list-div > .friend-div a img{
 float: left;
 margin: 15px 10px;
 width: 60px;
 height: 60px;
 border-radius: 35px;
 -webkit-transition: all .3s;
 -moz-transition: all .3s;
 -o-transition: all .3s;
 -ms-transition: all .3s;
 transition: all .3s
}

.flink#article-container .friend-list-div > .friend-div a .friend-name {
 display: block;
 padding: 16px 10px 0 0;
 height: 40px;
 font-weight: 700;
 font-size: 20px
}

.flink#article-container .friend-list-div > .friend-div a .friend-info {
 display: block;
 padding: 1px 10px 1px 0;
 height: 50px;
 font-size: 13px
}

```

##### 在_single.scss中引入代码

把your_site\themes\LoveIt\assets\css\_page\_single.scss复制粘贴到路径your_site\assets\css\_page\下。 再在文件your_site\assets\css\_page\_single.scss里添加如下内容：

```
@import "../_partial/_single/friend";

```

#### 创建友链页面

##### 创建friend/index.md文件

先new一个

>hugo new friend/index.md

写入

```html

<div class="flink" id="article-container">
<div class="friend-list-div" >

{{ friend name="友链名称1" url="友链地址1" logo="友链图片链接1" word="友链描述1" >}}
{{ friend name="友链名称2" url="友链地址2" logo="友链图片链接2" word="友链描述2" >}}

</div>
</div>

因为我已经配置完，每行都少写一个<，要不然会渲染成友链链接

```

##### 修改配置文件

找到your_site/config.toml配置文件的中# 菜单配置，在这一项下面添加：

```
      [[menu.main]]
        weight = 5
        identifier = "friend"
        pre = ""
        post = ""
        name = "友链"
        url = "/friend/"
        title = "Friend"

```

## 部署到服务器

因为我用的是服务器部署，这里只说服务器的方法

1. 安装宝塔（方便，且适合所有人）
2. 创建一个网站，并把网站根目录指向你的hugo生成的public文件夹
3. 同步
  我采用的本地编写，编译后用rsync同步到服务器
4. 不断更新维护即可
