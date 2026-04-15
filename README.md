# 💬 AI 雙人對話語音生成器

> 基於 Google Gemini 2.5 Flash TTS 的網頁版文字轉語音工具，支援 PDF/文本導入、AI 自動生成雙人對話腳本、30 種語音角色選擇、句子選擇性生成，最終輸出合併後的對話音檔。

![Version](https://img.shields.io/badge/version-1.0.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Language](https://img.shields.io/badge/language-繁體中文-red)

🌐 **線上使用**：**https://cagoooo.github.io/talk/** （無需安裝，點開即可使用）

---

## ✨ 功能特色

### 📖 多種文本輸入方式
- **直接貼上文本**：快速複製文章、報告、故事等內容
- **上傳 PDF**：支援拖曳或點擊選擇，自動用 pdf.js 萃取文字
- **手動輸入對話**：直接撰寫 `角色名：內容` 格式的對話腳本

### 🤖 AI 自動生成對話
- 使用 `gemini-2.5-flash` 模型
- 根據輸入的文本自動生成 10–16 句自然流暢的雙人對話
- 以問答、討論的方式介紹文本重點
- 生成後可在對話框中手動編輯調整

### 🎭 30 種語音角色
分為 7 大音色特質組，每個角色都有獨特風格：

| 分類 | 語音角色 |
|------|---------|
| 🌟 明亮活潑 | Zephyr、Puck、Autonoe、Laomedeia、Sadachbia |
| 🛡️ 穩重堅定 | Kore、Orus、Alnilam、Schedar |
| 📚 專業資訊 | Charon、Rasalgethi、Sadaltager |
| 🌸 溫柔友善 | Leda、Achernar、Vindemiatrix、Sulafat、Achird |
| 💎 平滑清晰 | Algieba、Despina、Iapetus、Erinome |
| 🍃 隨性輕鬆 | Aoede、Callirrhoe、Umbriel、Zubenelgenubi |
| 🎨 獨特風格 | Fenrir、Enceladus、Algenib、Gacrux、Pulcherrima |

### ✅ 句子選擇性生成
- 對話腳本下方自動顯示勾選清單
- 預設全選，可彈性取消不需要的句子
- 快捷按鈕：**全選 / 全不選 / 只選角色A / 只選角色B**
- 生成按鈕即時顯示選中數量：`✨ 生成選中的 5/12 句`

### 🎬 單一音檔輸出
- 只合成你勾選的句子
- 句間自動加入 0.4 秒自然停頓
- 最終合併為單一 WAV 音檔下載
- 頁面內建播放器可直接試聽

### 🎨 額外功能
- **語氣風格控制**：可指定「輕鬆閒聊」、「正式對話」、「充滿情感」等語氣
- **聊天氣泡視覺化**：左右分流顯示對話內容
- **API Key 自動記憶**：儲存於瀏覽器 localStorage，不會上傳
- **響應式設計**：支援手機、平板、桌面裝置
- **快捷鍵**：`Ctrl/Cmd + Enter` 快速生成

---

## 🚀 使用方式

### 線上使用
直接開啟 `index.html` 即可，無需安裝任何套件。

### 本地使用
```bash
# 複製專案
git clone https://github.com/cagoooo/talk.git
cd talk

# 直接開啟 index.html (或用任意靜態伺服器)
# 例如：
python -m http.server 8000
# 然後開啟 http://localhost:8000
```

### 取得 Gemini API Key
1. 前往 [Google AI Studio](https://aistudio.google.com/app/apikey)
2. 登入 Google 帳號後點擊「Create API Key」
3. 複製產生的 API Key（開頭為 `AIza...`）
4. 貼到網頁上方的 API Key 欄位即可

> 💡 **免費額度**：Gemini 2.5 Flash 提供慷慨的免費額度，一般個人使用綽綽有餘。

---

## 📝 使用流程

1. **設定 API Key**：貼上你的 Gemini API Key（會自動儲存）
2. **選擇音色**：為角色 A 和 B 分別選擇喜歡的語音
3. **輸入文本**（三選一）：
   - 貼上文章內容
   - 上傳 PDF 檔案
   - 直接手寫對話腳本
4. **AI 生成對話**（如果選擇文本/PDF）：點擊「🤖 AI 生成雙人對話腳本」
5. **勾選句子**：在預覽區選擇要生成語音的句子
6. **生成語音**：點擊「✨ 生成對話語音」開始合成
7. **下載音檔**：試聽後點擊「⬇️ 下載完整對話 (WAV)」

---

## 🛠️ 技術架構

- **前端**：純 HTML + CSS + JavaScript（無框架依賴）
- **TTS 引擎**：[Gemini 2.5 Flash Preview TTS](https://ai.google.dev/gemini-api/docs/speech-generation)
- **對話生成**：[Gemini 2.5 Flash](https://ai.google.dev/gemini-api/docs/models)
- **PDF 解析**：[pdf.js](https://mozilla.github.io/pdf.js/) 3.11.174
- **音訊格式**：24kHz / 16-bit / 單聲道 PCM → WAV

### 核心技術細節
- Gemini TTS API 回傳 Base64 編碼的 PCM 音訊資料
- 前端將 PCM 轉換為標準 WAV 格式（加入 44 bytes RIFF header）
- 多段音訊透過直接拼接 PCM 資料並插入靜音段實現合併
- 所有處理都在瀏覽器端完成，不經過中介伺服器

---

## 🔐 隱私與安全

- ✅ API Key 只儲存在**你的瀏覽器 localStorage**
- ✅ 所有文本內容、PDF 檔案都在**本機處理**
- ✅ 只有「生成對話」與「生成語音」時會呼叫 Google Gemini API
- ✅ 不收集、不上傳任何個人資料到第三方伺服器
- ✅ 完整原始碼公開透明

---

## 📋 版本歷史

### v1.0.0 (2026-04-16)
- 🎉 首次發布
- ✅ 30 種 Gemini 語音角色支援
- ✅ 雙人對話模式（角色 A / B 各自選擇語音）
- ✅ PDF / 文本導入功能
- ✅ AI 自動生成對話腳本
- ✅ 句子選擇性生成
- ✅ 單一合併音檔輸出
- ✅ 響應式 UI 設計

---

## 📄 授權條款

本專案採用 [MIT License](LICENSE) 授權。

---

## 🙋 常見問題

### Q: 為什麼需要 API Key？
A: Gemini TTS 是 Google 的付費 API 服務，需要使用你自己的 API Key 來呼叫。免費額度非常充足，一般使用不會超過。

### Q: PDF 無法解析怎麼辦？
A: 請確認 PDF 不是純圖像（掃描檔），必須是包含文字內容的 PDF。如果是掃描檔需先用 OCR 工具轉換。

### Q: 可以用其他語言嗎？
A: Gemini TTS 支援多種語言，你可以直接輸入英文、日文、韓文等語言的文本，語音會自動匹配。

### Q: 為什麼有時生成很慢？
A: Gemini API 有併發限制，本工具採用順序生成（一句一句處理）以避免速率限制錯誤。

### Q: 檔案格式是什麼？
A: 輸出為 WAV 格式（24kHz / 16-bit / 單聲道），幾乎所有播放器與剪輯軟體都支援。

---

## 💡 使用場景建議

- 📚 **教學影片**：將課文轉成生動對話，搭配簡報使用
- 🎙️ **Podcast**：快速生成雙人主持的節目範本
- 📖 **有聲書**：為故事情節加上角色對話
- 🎬 **影片配音**：為 YouTube / Reels 製作對話音軌
- 🗣️ **語言學習**：創建情境對話教材
- 📊 **簡報補充**：為專業報告產出摘要對話

---

## 🤝 貢獻

歡迎提出 Issue 或 Pull Request！

---

**Made with ❤️ using Gemini 2.5 Flash TTS**
