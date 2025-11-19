# 學生3D作品展示系統 - 使用說明

## 📁 檔案結構

```
您的專案/
├── menu.html           # 選單頁面（首頁）
├── index_simple.html   # 作品展示頁面
└── MODELS/
    ├── 01.glb         # 王小明的作品
    ├── 02.glb         # 李小華的作品
    └── 03.glb         # 陳小美的作品
```

---

## 🎯 切換學生作品的三種方法

### 方法 1：使用選單頁面（推薦） ⭐

1. **打開 `menu.html`**
2. **點擊任一學生卡片**
3. 自動跳轉到該學生的作品展示

**特色：**
- ✅ 視覺化選單
- ✅ 一鍵切換
- ✅ 適合現場展示

---

### 方法 2：使用 URL 參數

直接在瀏覽器網址列輸入：

```
# 觀看王小明的作品
index_simple.html?id=student1

# 觀看李小華的作品
index_simple.html?id=student2

# 觀看陳小美的作品
index_simple.html?id=student3
```

**特色：**
- ✅ 可直接分享連結
- ✅ 適合製作 QR Code
- ✅ 可加入書籤

---

### 方法 3：修改預設學生

在 `index_simple.html` 的第 450 行找到：

```javascript
function getStudentId() {
    const urlParams = new URLSearchParams(window.location.search);
    return urlParams.get('id') || urlParams.get('student') || 'student1';
    //                                                          ^^^^^^^^
    //                                          修改這裡的預設值
}
```

將 `'student1'` 改成 `'student2'` 或 `'student3'`

---

## 📱 製作 QR Code

### 學生1 - 王小明
**網址：** `https://您的網站.com/index_simple.html?id=student1`

### 學生2 - 李小華
**網址：** `https://您的網站.com/index_simple.html?id=student2`

### 學生3 - 陳小美
**網址：** `https://您的網站.com/index_simple.html?id=student3`

### 如何生成 QR Code：

1. **線上工具（推薦）：**
   - https://www.qr-code-generator.com/
   - https://www.qrcode-monkey.com/
   - https://qr.ioi.tw/ （台灣的工具）

2. **操作步驟：**
   - 複製上面的網址
   - 貼到 QR Code 生成器
   - 下載 QR Code 圖片
   - 列印或分享給學生

3. **建議設定：**
   - 尺寸：至少 300x300 像素
   - 格式：PNG（背景透明）
   - 容錯率：選擇「高」

---

## 💡 使用場景

### 場景 1：課堂展示
1. 打開 `menu.html`
2. 投影到大螢幕
3. 逐個點擊學生作品展示

### 場景 2：學生自主展示
1. 為每位學生生成專屬 QR Code
2. 學生用手機掃描自己的 QR Code
3. 直接進入自己的作品頁面

### 場景 3：作品集網站
1. 上傳所有檔案到網站空間
2. 分享 `menu.html` 的網址
3. 訪客可自由瀏覽所有作品

### 場景 4：家長會/開放日
1. 列印每位學生的 QR Code
2. 貼在作品旁邊
3. 家長掃描即可觀看 3D 動畫

---

## 🔧 新增更多學生

### 步驟 1：準備模型檔案
將新的 GLB 檔案放入 `MODELS` 資料夾：
```
MODELS/04.glb
MODELS/05.glb
...
```

### 步驟 2：修改 index_simple.html

在第 360 行找到 `studentsData`，新增：

```javascript
'student4': {
    name: '張小華',
    model: 'MODELS/04.glb',
    speeches: [
        { text: '大家好，我是張小華，這是我的作品', type: 'left' },
        { text: '希望大家喜歡！', type: 'right', decoration: '⭐' }
    ]
},
```

### 步驟 3：修改 menu.html

在第 211 行找到 `studentsData`，新增：

```javascript
'student4': {
    name: '張小華',
    emoji: '🌟',
    id: 'student4'
},
```

### 步驟 4：生成新的 QR Code
**網址：** `index_simple.html?id=student4`

---

## 🎨 自訂對話內容

### 修改學生介紹文字

在 `index_simple.html` 的 `speeches` 中修改：

```javascript
speeches: [
    { 
        text: '修改第一句話的內容',  // ← 這裡修改
        type: 'left' 
    },
    { 
        text: '修改第二句話的內容',  // ← 這裡修改
        type: 'right', 
        decoration: '❤️'            // ← 可以換成其他符號
    }
]
```

### 可用的裝飾符號：
❤️ 💖 💕 💗 ⭐ 🌟 ✨ 💫 🎉 🎊 🎈 👍 👏 🔥 💯

---

## 📊 完整流程圖

```
訪客
 ↓
打開 menu.html
 ↓
選擇學生
 ↓
跳轉到 index_simple.html?id=studentX
 ↓
載入對應的 GLB 模型
 ↓
顯示學生作品和介紹
 ↓
播放 3D 動畫
```

---

## ⚠️ 常見問題

### Q1：為什麼模型載入很慢？
**A：** 您的 01.glb 檔案有 23MB，建議：
- 壓縮紋理圖片
- 降低模型多邊形數量
- 優化後約 5-10MB 最佳

### Q2：如何在手機上測試？
**A：** 
1. 將檔案上傳到網路空間（如 GitHub Pages）
2. 或使用本地伺服器（如 Live Server）
3. 用手機瀏覽器開啟網址

### Q3：QR Code 掃描後沒反應？
**A：** 檢查：
- 網址是否正確
- 檔案是否都已上傳
- MODELS 資料夾名稱是否為大寫
- 模型檔案是否存在

### Q4：可以不用 MODELS 資料夾嗎？
**A：** 可以！修改路徑：
```javascript
model: '01.glb'  // 直接放在同一層
```

---

## 🎓 教學建議

1. **課前準備：**
   - 為每位學生生成 QR Code
   - 測試所有連結是否正常

2. **課堂操作：**
   - 先用 menu.html 展示全班作品
   - 再讓學生掃描自己的 QR Code

3. **作業收集：**
   - 學生上傳 GLB 檔案
   - 您批次新增到系統中

---

## 📞 技術支援

如遇到問題，請檢查：
1. ✅ 所有檔案都在正確位置
2. ✅ MODELS 資料夾名稱是大寫
3. ✅ GLB 檔案名稱正確（01.glb, 02.glb, 03.glb）
4. ✅ 瀏覽器支援 WebGL（現代瀏覽器都支援）

---

**祝您使用順利！🎉**
