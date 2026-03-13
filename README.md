# 🍜 美食 Tier List

> 和朋友一起替餐廳評分排名！貼上 Google Maps 連結，拖曳到心目中的等級，即時同步給所有人。

![Static Badge](https://img.shields.io/badge/部署-GitHub%20Pages-222?logo=github)
![Static Badge](https://img.shields.io/badge/資料庫-Firebase%20Realtime%20DB-orange?logo=firebase)
![Static Badge](https://img.shields.io/badge/分析-Google%20Analytics-blue?logo=googleanalytics)
![Static Badge](https://img.shields.io/badge/框架-純%20HTML%2FJS-lightgrey)

---

## ✨ 功能

| 功能 | 說明 |
|------|------|
| 🗺️ Google Maps 整合 | 貼上長網址自動解析店名；短網址輕鬆手動輸入 |
| 🏆 拖曳排名 | SSS → SS → S → A → B → C → D → ㄆㄨㄣ，共 8 個等級 |
| 📱 手機拖曳 | 長按卡片 350ms 啟動觸控拖曳，振動確認 |
| 👥 多人即時同步 | Firebase Realtime Database，所有操作即時同步 |
| 🟢 在線顯示 | 右上角顯示目前有誰在線 |
| 🎨 彩色頭像 | 每張卡片顯示是哪位朋友新增的 |
| 💬 多人評論 | 點 💬 展開評論面板，支援多人留言 |
| 📊 使用分析 | Google Analytics 追蹤流量與使用行為 |

---

## 🚀 部署教學

### 第一步：建立 Firebase 專案

1. 前往 [Firebase Console](https://console.firebase.google.com/) 並登入 Google 帳號
2. 點「**新增專案**」→ 輸入名稱（例如 `food-tierlist`）→ 建立
3. 左側選「**Realtime Database**」→「建立資料庫」→ 選「**以測試模式啟動**」
4. 回到「專案概覽」→ 點齒輪 ⚙️ →「**專案設定**」
5. 往下捲到「您的應用程式」→ 點 **`</>`** 圖示，新增網頁應用程式
6. 取個名字後點「**註冊應用程式**」，複製產生的 `firebaseConfig`：

```js
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "your-project.firebaseapp.com",
  databaseURL: "https://your-project-default-rtdb.firebaseio.com",
  projectId: "your-project",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123:web:abc...",
  measurementId: "YOUR_MEASUREMENT_ID"
};
```

---

### 第二步：填入 Firebase 設定

打開 `index.html`，找到約第 20 行的 `firebaseConfig`，**整段替換**成你剛複製的內容。

---

### 第三步：部署到 GitHub Pages

1. 在 GitHub 建立新 repository（例如 `food-tierlist`）
2. 上傳 `index.html` 與 `README.md`
3. 進入 repository →「**Settings**」→「**Pages**」
4. Source 選「Deploy from a branch」，Branch 選 `main`，資料夾選 `/ (root)`
5. 等幾秒，你的網址就會出現：

```
https://你的帳號.github.io/food-tierlist/
```

把網址傳給朋友，設定暱稱就能一起玩 🎉

---

## 📱 操作說明

### 手機
| 動作 | 結果 |
|------|------|
| 長按卡片（350ms）→ 拖曳 | 移動到其他等級 |
| 點 💬 | 開啟評論面板 |
| 點店名文字 | 開啟 Google Maps |
| 點 × → 再點「確認?」 | 刪除餐廳 |

### 桌機
| 動作 | 結果 |
|------|------|
| 拖曳卡片 | 移動到其他等級 |
| 點卡片本體 | 開啟評論面板 |
| 點店名文字 | 開啟 Google Maps |
| 點 × → 再點「確認?」 | 刪除餐廳 |

---

## 🔒 安全設定（建議做）

### Firebase 安全規則

進 Firebase Console → Realtime Database → **規則**，貼上：

```json
{
  "rules": {
    "items": {
      ".read": true,
      ".write": true,
      "$itemId": {
        ".validate": "newData.hasChildren(['name','url','tier'])"
      }
    },
    "presence": {
      ".read": true,
      ".write": true
    }
  }
}
```

> `.validate` 確保每筆寫入的資料都包含 `name`、`url`、`tier` 三個欄位，防止格式錯誤的垃圾資料。

### API Key 來源限制

前往 [Google Cloud Console](https://console.cloud.google.com/) → API 和服務 → 憑證 → 點你的 API Key → 加上 **HTTP 參照來源限制**：

```
https://你的帳號.github.io/*
```

這樣就算 config 被看到，Key 在其他網站也無法使用。

---

## 📊 Google Analytics

本專案已整合 Google Analytics 4，填入你的測量 ID（格式為 `G-XXXXXXXXXX`）即可啟用。

部署後可在 [GA4 後台](https://analytics.google.com/) 查看：
- 即時使用人數
- 頁面瀏覽次數
- 使用者來源與裝置分佈

> 無需額外設定，上線後資料自動開始收集。

---

## 📁 檔案結構

```
food-tierlist/
├── index.html    # 所有程式碼（HTML + CSS + JS）
└── README.md     # 本說明文件
```

---

## 🛠️ 技術架構

| 項目 | 技術 |
|------|------|
| 前端 | 純 HTML / CSS / JavaScript，無框架 |
| 資料庫 | Firebase Realtime Database（免費方案） |
| 分析 | Google Analytics 4（GA4） |
| 部署 | GitHub Pages（免費） |
| 字體 | Plus Jakarta Sans + Noto Sans TC |

---

## 📝 License

MIT
