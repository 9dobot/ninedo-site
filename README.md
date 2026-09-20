# NineDo 靜態網站 — 部署到 GitHub Pages 說明

## 這個資料夾裡有什麼
- `index.html`：已經把原本 `header.php` + 首頁內容 + `footer.php` 合併成一個完整的靜態頁面
- `img/`：空資料夾，需要你把原本網站用到的圖片放進來（見下方清單）

## 你還需要補的東西

### 1. 圖片檔案（放進 `img/` 資料夾，檔名要完全一致）
- `9.do-rem_bg.png`（Logo）
- `9do.ico`（favicon）
- `9do_qrcode.png`（LINE QR code）
- `ninedo-share-cover.jpg`（分享縮圖，非必要，沒有的話可以刪掉 index.html 裡 `og:image` 那一行）

### 2. 頁尾資訊（目前是佔位文字，直接在 `index.html` 搜尋修改即可）
在 `<footer>` 區塊裡找到：
- 客服專線 / 客服信箱 / 服務時間 / 營業地址 → 改成你的真實資訊
- 版權公司名稱（目前寫 "NineDo Business Solutions"）→ 如需修改直接改文字

### 3. 其他頁面（關於我們 / 服務條款 / 隱私權 / 退款政策）
原本網站有 `about.php`、`terms.php`、`privacy.php`、`refund.php`，但這次沒有提供內容，
所以頁尾連結先指向 `about.html`、`terms.html`、`privacy.html`、`refund.html`，
這些檔案目前還不存在。如果你有這些頁面的原始碼，可以貼給我，我一樣幫你轉成靜態 HTML；
或是暫時先把頁尾這些連結拿掉也可以。

---

## 部署到 GitHub Pages（免費）

### 步驟 1：建立 GitHub Repository
1. 到 [github.com](https://github.com) 登入你的帳號
2. 點右上角 `+` → `New repository`
3. Repository name 隨意取（例如 `ninedo-site`），設定為 **Public**
4. 建立完成

### 步驟 2：把這個資料夾上傳上去
在你的電腦上（已安裝 git）：
```bash
cd ninedo-site
git init
git add .
git commit -m "Initial static site"
git branch -M main
git remote add origin https://github.com/你的帳號/ninedo-site.git
git push -u origin main
```
（如果不想用指令，也可以直接在 GitHub 網頁上「Add file → Upload files」把整個資料夾拖上去）

### 步驟 3：開啟 GitHub Pages
1. 進入該 repository → `Settings` → 左側選單 `Pages`
2. `Source` 選擇 `Deploy from a branch`
3. Branch 選 `main`，資料夾選 `/ (root)`
4. 儲存後等 1-2 分鐘，會出現網址，例如：
   `https://你的帳號.github.io/ninedo-site/`

### 步驟 4：綁定你自己申請的網域
假設你的網域是 `www.example.com`：

**A. 在 GitHub 端**
1. 同樣在 `Settings → Pages`，在 `Custom domain` 欄位輸入你的網域，例如 `www.example.com`，儲存
2. GitHub 會自動在 repo 根目錄新增一個 `CNAME` 檔案（內容就是你的網域），保留它、之後不要刪掉
3. 建議勾選 `Enforce HTTPS`（要等 DNS 生效後才會出現這個選項）

**B. 在你的網域註冊商（GoDaddy、Namecheap、Cloudflare…）**
在 DNS 設定裡新增紀錄，兩種常見方式擇一：

- 如果要用 `www.example.com`：
  新增一筆 **CNAME** 紀錄
  - 主機名稱（Host）：`www`
  - 指向（Value）：`你的帳號.github.io`

- 如果要用裸網域 `example.com`（不帶 www）：
  新增 **4 筆 A 紀錄**，指向 GitHub Pages 的 IP：
  ```
  185.199.108.153
  185.199.109.153
  185.199.110.153
  185.199.111.153
  ```

DNS 生效通常需要幾分鐘到 24 小時不等。生效後打開瀏覽器輸入你的網域，就會看到這個網站。

---

## 之後要修改內容怎麼辦？
因為現在是純 HTML（沒有 PHP include），如果之後想再加頁面或改頭尾，
最簡單的方式是把改好的檔案再 `git add . && git commit -m "update" && git push` 一次，
GitHub Pages 會在幾十秒內自動重新部署，不需要手動操作。
