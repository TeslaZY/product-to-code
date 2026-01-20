# UI 原型图提示词

本文件包含根据产品需求文档生成的 UI 原型图提示词，可以直接复制到 Midjourney、Gemini、DALL-E 等图像生成工具中生成设计稿。

## 产品信息

- **产品名称**: {{product_name}}
- **产品定位**: {{product_positioning}}
- **目标风格**: {{style_type}}
- **配色方案**: {{color_scheme}}

---

## 提示词列表

### 1. {{page_name}}
**页面描述**: {{page_description}}

**提示词**:
```
{{prompt}}
```

**适用工具**: Midjourney v6, Gemini, DALL-E 3
**推荐参数** (Midjourney): `--ar 16:9 --style raw --v 6.0`

---

### 2. {{page_name}}
**页面描述**: {{page_description}}

**提示词**:
```
{{prompt}}
```

**适用工具**: Midjourney v6, Gemini, DALL-E 3
**推荐参数** (Midjourney): `--ar 16:9 --style raw --v 6.0`

---

## 使用说明

### Midjourney 使用方法
1. 打开 Discord，加入 Midjourney 服务器
2. 输入 `/imagine` 命令
3. 粘贴提示词（不含代码块符号）
4. 根据需要添加参数，如 `--ar 16:9` 调整比例

### Gemini 使用方法
1. 打开 Google Gemini
2. 直接粘贴提示词
3. 可以附加"生成一个{{page_name}}的设计稿"等说明

### DALL-E 3 使用方法
1. 打开 ChatGPT Plus / DALL-E 3 界面
2. 直接粘贴提示词
3. 可以附加风格要求

---

**生成时间**: {{date}} |
**基于产品文档版本**: {{prd_version}}
