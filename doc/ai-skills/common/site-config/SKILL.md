# Site Configuration Skill - 网站配置修改规范

## 适用范围

本 skill 适用于处理本项目中与网站配置相关的所有任务，包括：
- 修改网站基本信息（标题、描述、作者等）
- 配置导航菜单
- 调整侧边栏设置
- 配置评论系统（Gitalk）
- 配置分析工具（Google Analytics、百度统计）
- 修改 SEO 相关设置
- 调整 PWA 配置

## 执行流程

### 1. 任务分析与确认

- 首先明确用户需求：需要修改哪些配置项
- 确认修改范围和可能的影响
- 重要配置修改前，建议备份原配置文件

### 2. 主要配置文件位置

#### 2.1 _config.yml（核心配置）

网站的主要配置文件，包含：

```yaml
# Site settings
title: "小张的读书会"
subtitle: "读书、思考、分享"
description: "一个专注于读书分享的博客"
author: "enilu"
language: "zh-CN"

# URLs
baseurl: ""
url: "https://reading.enlu.cn"

# Sidebar settings
sidebar: true
sidebar-about-description: "读书是一种生活方式"
sidebar-avatar: "/img/avatar-enilu.jpg"

# Social links
qq: "123456789"
github_username: "enilu-en"
# 其他社交链接...

# Build settings
# ...

# Gitalk comments settings
gitalk:
  clientID: "..."
  clientSecret: "..."
  repo: "enilu-en.github.io"
  owner: "enilu-en"
  admin: ["enilu-en"]
  distractionFreeMode: false

# Google Analytics
ga_track_id: "UA-123456789-1"
```

#### 2.2 其他配置文件

- `package.json`：项目依赖和脚本配置
- `Gruntfile.js`：Grunt 任务配置
- `pwa/manifest.json`：PWA 配置
- `CNAME`：自定义域名配置

### 3. 配置修改规范

#### 3.1 修改流程

1. 备份原配置文件
2. 按需求修改相应配置项
3. 验证配置是否生效
4. 测试网站功能是否正常

#### 3.2 注意事项

- 所有配置项修改都可能影响网站功能，需谨慎操作
- 修改后必须进行验证
- 涉及敏感信息（如 API 密钥、密码）的配置项，必须确保安全
- 配置文件格式（如 YAML）必须正确

### 4. 验证方法

- 本地运行 `jekyll serve` 验证网站是否正常加载
- 检查配置修改是否正确应用
- 测试相关功能是否正常工作

### 5. 常见配置修改场景

#### 5.1 修改网站基本信息

```yaml
# _config.yml
title: "新标题"
subtitle: "新副标题"
description: "新描述"
author: "新作者名"
```

#### 5.2 配置导航菜单

导航菜单在 `_includes/nav.html` 文件中修改：

```html
<!-- _includes/nav.html -->
<nav>
  <ul>
    <li><a href="{{ "/" | prepend: site.baseurl }}">首页</a></li>
    <li><a href="{{ "/about" | prepend: site.baseurl }}">关于</a></li>
    <li><a href="{{ "/tags" | prepend: site.baseurl }}">标签</a></li>
    <!-- 添加新菜单项 -->
  </ul>
</nav>
```

#### 5.3 配置 Gitalk 评论系统

```yaml
# _config.yml
gitalk:
  clientID: "your-client-id"
  clientSecret: "your-client-secret"
  repo: "your-repo-name"
  owner: "your-github-username"
  admin: ["your-github-username"]
  distractionFreeMode: false
```

#### 5.4 配置 Google Analytics

```yaml
# _config.yml
ga_track_id: "UA-XXXXXXXXX-X"
```

### 6. 风险提示

- 配置文件语法错误可能导致网站无法构建
- 错误的 URL 配置可能导致资源加载失败
- 错误的 API 密钥配置可能导致评论或分析功能失效
- 重要配置修改前，建议先在本地测试验证

## 提交规范

- 提交信息应清晰明确，说明修改内容
- 示例：`Update: 修改网站标题和描述` 或 `Config: 配置 Google Analytics`
