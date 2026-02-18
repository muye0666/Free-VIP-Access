包含代码说明、使用指南和功能介绍：

```markdown
# VIP Video Parser - VIP视频解析工具

> **VIP Video Parser** is a lightweight, client-side web application that allows users to parse and watch VIP videos from major Chinese streaming platforms without encoding issues.

**中文说明**：这是一个轻量级的客户端Web应用，用于解析和观看主流中文视频平台的VIP内容，采用无编码URL格式确保兼容性。

---

## 🌟 Features | 功能特性

### Core Features | 核心功能
- ✅ **Smart URL Parsing** | 智能URL解析 - Automatically extracts real video URLs from encoded links
- ✅ **No Encoding Issues** | 无编码问题 - Generates clean URLs (`://` instead of `%3A%2F%2F`)
- ✅ **History Management** | 历史记录 - Save and manage up to 10 recent parsed links
- ✅ **One-Click Clear** | 一键清空 - Batch delete all history with confirmation
- ✅ **PWA Support** | PWA支持 - Install as standalone app on mobile/desktop

### Supported Platforms | 支持平台
| Platform | Icon | URL |
|---------|------|-----|
| 爱奇艺 (iQiyi) | 🥝 | https://www.iqiyi.com |
| 腾讯视频 (Tencent Video) | 🐧 | https://v.qq.com |
| 优酷 (Youku) | 🎬 | https://www.youku.com |

---

## 🚀 Quick Start | 快速开始

### Usage | 使用方法

1. **Copy Video Link** | 复制视频链接
   - Open any supported video platform
   - Copy the VIP video URL to clipboard

2. **Paste & Parse** | 粘贴并解析
   ```text
   Input: https://v.qq.com/x/cover/mzc00200xxpsogl/h4101bl5ftq.html
   Output: https://jx.xmflv.cc/?url=https://v.qq.com/x/cover/mzc00200xxpsogl/h4101bl5ftq.html
```

3. **Watch Video** | 观看视频
   - Click "播放VIP视频" (Play VIP Video)
   - Video opens in new tab

### Keyboard Shortcuts | 快捷键

| Key            | Action                    |
| -------------- | ------------------------- |
| `Enter`        | Parse and play video      |
| `Ctrl + Enter` | Alternative play shortcut |

---

## 🛠️ Technical Details | 技术细节

### URL Format Comparison | URL格式对比

| Type      | Example                                                 | Status      |
| --------- | ------------------------------------------------------- | ----------- |
| ❌ Encoded | `https://jx.xmflv.cc/?url=https%3A%2F%2Fv.qq.com%2F...` | Not working |
| ✅ Clean   | `https://jx.xmflv.cc/?url=https://v.qq.com/...`         | **Working** |

### API Endpoints | 解析接口

```javascript
const API_URL = 'https://jx.xmflv.cc/?url=';
// Format: API_URL + raw_video_url (no encoding)
```

### Key Code Snippet | 核心代码

```javascript
// Critical fix: No encodeURIComponent, direct concatenation
function playVideo() {
    let url = input.value.trim();
    
    // Decode if already encoded
    if (url.includes('%')) {
        try {
            url = decodeURIComponent(url);
        } catch (e) {
            console.log('Decode failed, using original');
        }
    }
    
    // Direct concatenation - generates clean URL
    const parseUrl = API_URL + url;
    window.open(parseUrl, '_blank');
}
```

---

## 📱 PWA Installation | PWA安装

### iOS Safari
1. Tap **Share** button
2. Select **"Add to Home Screen"**
3. Launch from home screen like native app

### Android Chrome
1. Tap menu (⋮) → **"Add to Home screen"**
2. Or tap **"Install"** when prompted

### Desktop Chrome
1. Click **⊕** icon in address bar
2. Select **"Install"**

---

## 📁 File Structure | 文件结构

```
vip-video-parser/
├── index.html          # Main application file
└── README.md           # This documentation
```

---

## 🎨 UI Components | 界面组件

### Main Interface | 主界面
- **Input Section** | 输入区域 - Glassmorphism design with gradient background
- **Platform Buttons** | 平台按钮 - Quick access to major video sites
- **History Section** | 历史区域 - Collapsible list with delete functionality
- **Tips Box** | 提示框 - Usage instructions and warnings

### History Management | 历史记录管理
```javascript
// Save history
function saveToHistory(url) {
    let history = JSON.parse(localStorage.getItem('videoHistory') || '[]');
    history = history.filter(item => item !== url);
    history.unshift(url);
    if (history.length > 10) history = history.slice(0, 10);
    localStorage.setItem('videoHistory', JSON.stringify(history));
}

// Clear all history
function clearAllHistory() {
    if (confirm(`Clear ${history.length} history items?`)) {
        localStorage.removeItem('videoHistory');
        loadHistory();
    }
}
```

---

## ⚠️ Disclaimer | 免责声明

> **For educational purposes only** | **仅供学习交流使用**

This tool is intended for educational and research purposes only. Users are responsible for complying with local laws and the terms of service of video platforms. Please delete parsed content within 24 hours.

本工具仅供学习研究使用，用户需遵守当地法律法规及视频平台服务条款，请在24小时内删除解析内容。

---

## 📝 Changelog | 更新日志

### v1.2.0 (Current)
- Added history clear functionality | 新增清空历史功能
- Fixed URL encoding issues | 修复URL编码问题
- Optimized PWA support | 优化PWA支持

### v1.1.0
- Added history management | 新增历史记录管理
- Improved mobile responsiveness | 改进移动端适配

### v1.0.0
- Initial release | 初始版本
- Basic parsing functionality | 基础解析功能

---

## 🔧 Browser Compatibility | 浏览器兼容性

| Browser        | Support        |
| -------------- | -------------- |
| Chrome 90+     | ✅ Full support |
| Firefox 88+    | ✅ Full support |
| Safari 14+     | ✅ Full support |
| Edge 90+       | ✅ Full support |
| iOS Safari     | ✅ PWA support  |
| Android Chrome | ✅ PWA support  |

---

**Made with ❤️ for video enthusiasts worldwide.**

```

Markdown文档包含了：
- 中英文双语说明
- 功能特性列表
- 使用方法指南
- 技术细节解析
- PWA安装指南
- 免责声明