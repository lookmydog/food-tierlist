# 🍜 美食 Tier List

> 和朋友一起對高雄（或任何地方）的餐廳評分！貼上 Google Maps 連結，拖曳到你心目中的等級，即時同步給所有人。

![Static Badge](https://img.shields.io/badge/部署-GitHub%20Pages-222?logo=github)
![Static Badge](https://img.shields.io/badge/資料庫-Firebase%20Realtime%20DB-orange?logo=firebase)
![Static Badge](https://img.shields.io/badge/框架-純%20HTML%2FJS-blue)

---

## ✨ 功能

| 功能 | 說明 |
|------|------|
| 🗺️ Google Maps 整合 | 貼上長網址自動解析店名，短網址手動輸入 |
| 🏆 拖曳排名 | SSS → SS → S → A → B → C → D → ㄆㄨㄣ，共 8 個等級 |
| 👥 多人即時同步 | Firebase Realtime Database，所有操作立即同步 |
| 🟢 在線顯示 | 右上角顯示目前有誰在線 |
| 🎨 彩色頭像 | 每筆餐廳顯示是哪位朋友新增的 |
| 💬 多人評論 | 點擊餐廳標籤展開評論面板，支援多人留言 |
| 📱 手機友好 | 響應式設計，手機也能用 |

---

## 🚀 部署教學

### 第一步：建立 Firebase 專案（免費）

1. 前往 [Firebase Console](https://console.firebase.google.com/)
2. 點「新增專案」→ 取個名字（例如 `food-tierlist`）→ 建立
3. 左側選「**Realtime Database**」→「建立資料庫」→ 選「以測試模式啟動」
4. 回到「專案概覽」→ 點齒輪 ⚙️ →「專案設定」
5. 往下捲到「您的應用程式」→ 點 **`</>`** 圖示新增網頁應用程式
6. 複製產生的 `firebaseConfig`：

```js
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "your-project.firebaseapp.com",
  databaseURL: "https://your-project-default-rtdb.firebaseio.com",
  projectId: "your-project",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123:web:abc..."
};
```

---

### 第二步：填入設定

打開 `index.html`，找到約第 15 行的 `firebaseConfig`，**整段替換**成你剛複製的內容。

---

### 第三步：部署到 GitHub Pages

1. 在 GitHub 建立新 repository（例如 `food-tierlist`）
2. 上傳 `index.html`
3. 進入 repository →「**Settings**」→「**Pages**」
4. Source 選「Deploy from a branch」，Branch 選 `main`，資料夾選 `/ (root)`
5. 等幾秒，你的網址就會出現：

```
https://你的帳號.github.io/food-tierlist/
```

把網址傳給朋友，設定暱稱就能一起用 🎉

---

## 🔒 安全設定（建議做）

### Firebase 安全規則

進 Firebase Console → Realtime Database → **規則**，貼上以下內容，確保寫入資料格式正確：

```json
{
  "rules": {
    ".read": true,
    ".write": true,
    "items": {
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

> `.validate` 的作用：確保每筆寫入的餐廳資料都必須包含 `name`、`url`、`tier` 三個欄位，防止格式錯誤的垃圾資料被寫入。

### API Key 來源限制

前往 [Google Cloud Console](https://console.cloud.google.com/) → API 和服務 → 憑證 → 點你的 API Key → 加上 HTTP 參照來源限制：

```
https://你的帳號.github.io/*
```

這樣就算 config 被看到，Key 在其他網站也無法使用。

---

## 📁 檔案結構

```
food-tierlist/
└── index.html    # 所有程式碼（HTML + CSS + JS）都在這一個檔案
```

---

## 🛠️ 技術架構

- **前端**：純 HTML / CSS / JavaScript，無框架
- **資料庫**：Firebase Realtime Database（免費方案）
- **部署**：GitHub Pages（免費）
- **字體**：Plus Jakarta Sans + Noto Sans TC

---

## 📝 License

MIT