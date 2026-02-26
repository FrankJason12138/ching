# 易经铜钱占卜 · I Ching Coin Divination

> 基于周易筮法的网页端铜钱占卜工具，使用真实随机数，结合三维铜钱模型与完整六十四卦卦辞。

[![License: MIT](https://img.shields.io/badge/License-MIT-gold.svg)](LICENSE)
[![HTML](https://img.shields.io/badge/HTML-5-orange.svg)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![Three.js](https://img.shields.io/badge/Three.js-r128-black.svg)](https://threejs.org/)
[![No Backend](https://img.shields.io/badge/Backend-None-green.svg)]()

---

## ✨ 功能特性

- **真实随机数** — 依次尝试量子随机数（ANU QRNG）→ random.org → 浏览器 Crypto API，概率公正
- **三维铜钱模型** — 使用 Three.js 加载真实 `.glb` 铜钱模型，闲置时自动旋转
- **铜钱入壳动画** — 起卦时铜钱飞入龟壳、龟壳抖动、铜钱摇出，完整动效还原古法意境
- **完整六十四卦** — 编码严格按照「下卦三爻＋上卦三爻」，无重复无缺漏
- **本卦 ＋ 变卦** — 自动识别老阴（6）、老阳（9）变爻，给出变卦及对应卦辞
- **完整爻辞** — 每卦含卦辞、彖传、六条爻辞，变爻处单独展示
- **纯静态** — 无需服务器，可部署至 Cloudflare Pages / Netlify / GitHub Pages

---

## 📸 预览

> *（可在此处添加截图或 GIF）*

---

## 🚀 快速开始

### 本地运行

```bash
# 克隆项目
git clone https://github.com/your-username/iching-divination.git
cd iching-divination

# 启动本地服务器（任选其一）
python -m http.server 8080
# 或
npx serve .

# 访问
open http://localhost:8080
```

> ⚠️ 必须通过 HTTP 服务器打开，直接双击 HTML 文件会导致 GLB 模型加载失败（浏览器跨域限制）。

### 文件结构

```
iching-divination/
├── index.html       # 主文件，含全部逻辑
├── coin.glb         # 开元通宝 3D 铜钱模型（CC BY-NC）
├── true.png         # 神龟图片
└── README.md
```

---

## 🔮 占卜说明

本项目遵循《周易》传统铜钱起卦法：

| 投掷结果 | 爻值 | 爻象 | 说明 |
|---------|------|------|------|
| 三反（2+2+2）| **6** | ⚋ 老阴 | 阴爻，**变爻**，化为阳 |
| 两反一正（2+2+3）| **7** | ⚊ 少阳 | 阳爻，不变 |
| 一反两正（2+3+3）| **8** | ⚋ 少阴 | 阴爻，不变 |
| 三正（3+3+3）| **9** | ⚊ 老阳 | 阳爻，**变爻**，化为阴 |

- 连续投掷六次，从**初爻（下）**到**上爻（上）**逐爻成卦
- 有变爻则生成**变卦**，结合本卦与变卦综合解读

---

## 🛠️ 技术栈

| 技术 | 用途 |
|------|------|
| [Three.js r128](https://threejs.org/) | 3D 铜钱渲染 |
| [GLTFLoader](https://threejs.org/docs/#examples/en/loaders/GLTFLoader) | 加载 `.glb` 模型 |
| [ANU QRNG API](https://qrng.anu.edu.au/) | 量子真随机数 |
| [random.org](https://www.random.org/) | 备用真随机数 |
| Web Crypto API | 本地加密随机数（兜底） |
| CSS Animation | 铜钱飞入/飞出、龟壳抖动动效 |
| Noto Serif SC | 中文字体 |

---

## 🌐 部署

本项目为纯静态页面，可一键部署至任意静态托管平台。

### Cloudflare Pages（推荐）

1. Fork 本仓库
2. 前往 [pages.cloudflare.com](https://pages.cloudflare.com) → Create a project → Connect to Git
3. 选择本仓库，构建设置全部留空
4. 部署完成，获得 `xxx.pages.dev` 域名

### Netlify 拖拽部署

1. 前往 [app.netlify.com/drop](https://app.netlify.com/drop)
2. 将项目文件夹直接拖入页面
3. 30 秒内上线

---

## 📜 六十四卦编码规则

卦象键值采用六位二进制字符串，规则如下：

```
键 = 下卦（初爻~三爻）+ 上卦（四爻~上爻）
1 = 阳爻，0 = 阴爻，从初爻（index 0）到上爻（index 5）

八卦二进制（初→三爻）：
乾 ☰ = 111    兑 ☱ = 011
离 ☲ = 101    震 ☳ = 001
巽 ☴ = 110    坎 ☵ = 010
艮 ☶ = 100    坤 ☷ = 000

示例：
屯卦（震下坎上）= 001 + 010 = "001010"
既济（离下坎上）= 101 + 010 = "101010"
```

---

## 🙏 致谢

- **铜钱模型** — [Kai Yuan Tong Bao Coin](https://sketchfab.com/3d-models/kai-yuan-tong-bao-coin-42339c0566c8457bac53bdefb889ec41) by Emily Lankiewicz，授权协议：[CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/)
- **卦辞来源** — 《周易》原文，公共领域

---

## 📄 许可证

本项目代码以 [MIT License](LICENSE) 开源。

> ⚠️ 注意：项目中包含的 `coin.glb` 模型授权协议为 **CC BY-NC 4.0**（署名-非商业性使用），商业使用请自行替换模型。

---

<div align="center">

**☰ ☱ ☲ ☳ ☴ ☵ ☶ ☷**

*天行健，君子以自强不息*

</div>
