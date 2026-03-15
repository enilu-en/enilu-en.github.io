# enilu Blog

 本博客模板克隆自：https://github.com/qiubaiying/qiubaiying.github.io
 感谢[qiubaiying](https://github.com/qiubaiying)

## AI Agent Guide（统一入口）

### 执行顺序

1. 先读 README 关键章节
2. 扫描并命中 `doc/ai-skills/` 的 `SKILL.md`
3. 最后读工具入口差异项（CLAUDE.md）

### 协作与交互约束（高优先级）

- 代码注释与文档默认使用中文编写
- 编写任何代码前，先描述实现方法并等待用户批准
- 需求有歧义时，先澄清再实施
- 预估改动超过 3 个文件时，先拆分子任务再继续
- 用户纠正后，先说明错误原因与防复发措施
- 每轮交互结束后，追加写入 `session_yyyyMMdd.md`
- 最终回复前，必须先完成会话落盘，并执行 `tail -n 20 session_yyyyMMdd.md` 校验
- 最终输出必须包含：`会话落盘：已完成/失败 + 文件路径 + 时间戳`

### 通用实施与输出规范

- 搜索与定位优先使用 `grep` / `find`
- 改动保持最小化，优先复用现有模式
- 较大改动先给简短计划，再分步落地
- 验证至少覆盖最小相关命令，无法执行时明确说明原因
- 最终输出至少包含关键改动文件、改动目的、验证结果、未覆盖风险/待确认项、影响范围

### 统一规则

- 信息缺失先确认再实现
- skills 以项目内 `doc/ai-skills/` 为准
- 工具入口文件冲突时以 README 为准

## 备忘

这里说明本博客做的特殊调整：

- 博客使用了gittalk做评论插件，需要针对每篇博客创建issue来保存评论，建立issue的时候需要根据url来做issue的标签label。但是github的label长度有限制，因此本博客issue的label都截取url标题的前四十位，如下所示：
  ```
http://reading.enilu.cn/2019/09/01/如何阅读一本书/
上面url encoder后内容为：
http://reading.enilu.cn/2019/09/01/%E5%A6%82%E4%BD%95%E9%98%85%E8%AF%BB%E4%B8%80%E6%9C%AC%E4%B9%A6-%E8%AF%BB%E4%B9%A6%E7%AC%94%E8%AE%B0/
则取其日期(2019/09/01/)之后的前40位做issue的label：
%E5%A6%82%E4%BD%95%E9%98%85%E8%AF%BB%E4%
同时修改了_layouts/post.html中的gittalk id取值方式：
id: (location.pathname).split("/")[4].substring(0, 40)
  ```

## 项目结构

```
enilu-en.github.io/
├── _posts/              # 博客文章（Markdown，按年份分类）
├── _layouts/            # Jekyll 模板文件
├── _includes/           # 可复用组件
├── _config.yml          # Jekyll 配置文件
├── css/                 # 编译后的样式表
├── less/                # Less 源文件
├── js/                  # JavaScript 文件
├── img/                 # 图片资源
├── fonts/               # 字体文件
├── pwa/                 # PWA 相关文件
├── doc/ai-skills/       # AI 任务执行规范
├── index.html           # 首页（含分页）
├── about.html           # 关于页面
├── tags.html            # 标签/云页面
├── 404.html             # 错误页面
├── offline.html         # 离线回退页面
├── feed.xml             # RSS 订阅
├── sitemap.xml          # SEO 站点地图
└── CNAME                # 自定义域名配置
```

## 构建与运行命令

### 1. 安装依赖

#### 1.1 安装 npm 依赖（用于前端资源编译）

```bash
# 安装依赖
npm install
```

#### 1.2 安装 Jekyll 插件（用于分页功能）

```bash
# 安装 jekyll-paginate 插件
gem install jekyll-paginate
```

### 2. 启动开发服务器

#### 2.1 方式一：直接使用 Jekyll 命令

```bash
# 本地开发服务器（自动刷新）
jekyll serve --watch
```

#### 2.2 方式二：使用 npm 脚本（Windows 系统推荐）

```bash
# Python 3 预览构建后站点
npm run py3view

# 监听文件变化 + 预览 + Jekyll 服务（Python 3）
npm run py3wa
```

#### 2.3 方式三：使用完整路径（解决 Windows 系统路径问题）

如果您在 Windows 系统上遇到 Ruby 路径问题，可以使用以下命令：

```bash
# 使用完整 Ruby 路径
"/d/Program/develop/Ruby32-x64/bin/ruby.exe" -S jekyll serve --watch
```

### 3. 构建命令

```bash
# 构建静态站点到 _site/ 目录
jekyll build
```

### 4. Grunt 命令（用于前端资源编译）

```bash
# 编译 Less、压缩 JS
grunt

# 监听文件变化自动编译
grunt watch

# 仅编译 Less
grunt less

# 仅压缩 JavaScript
grunt uglify
```

### 5. 常见问题解决

#### 5.1 插件配置问题

如果文章列表不显示，可能是插件配置问题。请确保 `_config.yml` 文件中包含以下配置：

```yaml
gems: [jekyll-paginate]
plugins: [jekyll-paginate]
```

#### 5.2 Ruby 路径问题

如果在 Windows 系统上遇到 `jekyll` 命令无法找到的问题，可以尝试使用完整路径，或者检查系统的 PATH 变量配置。

#### 5.3 依赖安装问题

如果安装 gem 时遇到网络问题，可以尝试更换源：

```bash
gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/
```

### 6. 访问博客

启动服务器后，在浏览器中访问：

```
http://127.0.0.1:4000/
```

## License

遵循 MIT 许可证。有关详细,请参阅 [LICENSE](https://github.com/qiubaiying/qiubaiying.github.io/blob/master/LICENSE)。
