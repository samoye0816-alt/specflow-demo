# SpecFlow｜SSD 產品規格書生成工具

Streamlit DEMO：上傳可選取文字的 SSD PDF，使用 Gemini 擷取與複核，再核對、編輯及下載 CSV／HTML。

## 本機啟動

建議 Python 3.12。在本資料夾開啟終端機：

```powershell
python -m pip install -r requirements.txt
python -m streamlit run app.py
```

API 金鑰由使用者在側邊欄輸入，不需要設定 secrets.toml。請使用原先已成功呼叫的帳戶與模型。

## 部署至 Streamlit Community Cloud

1. 在 https://github.com/new 建立儲存庫，例如 `specflow-demo`。可選公開或私人；私人儲存庫需授權 Streamlit 存取。
2. 將本資料夾內容上傳至儲存庫根目錄，不要上傳 ZIP 檔本身。根目錄必須直接看得到 app.py 與 requirements.txt。
3. 同時上傳 `.streamlit/config.toml`。Windows 如果不方便上傳隱藏資料夾，可在 GitHub 按 Add file → Create new file，檔名輸入 `.streamlit/config.toml`，貼入該檔內容後提交。
4. 開啟 https://share.streamlit.io/，登入並連接 GitHub，按 Create app，選擇已有程式（Yup, I have an app）。
5. 選擇剛建立的 Repository；Branch 填實際分支（新建通常為 main）；Main file path 填 `app.py`。
6. Advanced settings 選 Python 3.12。維持從側邊欄輸入金鑰的設計時，Secrets 不用填。
7. 按 Deploy。安裝完成後會取得 `https://你的名稱.streamlit.app/` 形式的網址。這裡只是格式示例，並非已建立的網址。
8. 確認分享權限允許預定觀眾存取，再用無痕視窗開啟實際網址驗收。

部署操作以官方說明為準：https://docs.streamlit.io/deploy/streamlit-community-cloud/deploy-your-app/deploy

## 上線驗收

- 首頁能開啟，PDF 文字讀取方式與欄位定義在主畫面，AI 連線在側邊欄。
- 輸入自己的金鑰取得模型清單，選擇可用模型。
- 上傳已測試的 MP44 PDF，確認能讀取文字並完成擷取。
- 修改一個備註，確認核對表 CSV 與 HTML 含有修改。
- 無痕視窗能存取；不同使用者需各自輸入金鑰並建立自己的工作階段。
- 展示前另存核對表 CSV，以便服務忙碌時匯入既有結果。

## 限制與故障排除

- 網站部署不會消除 Gemini 的 429／503，仍依 API 額度與服務可用性而定。
- 不要將金鑰寫入 app.py 或上傳 GitHub；此套件沒有內建共用金鑰。
- 上傳文件文字會透過雲端程式傳送到 Gemini。請沿用公開規格書測試。
- 工作狀態不作永久保存。重新整理、斷線或服務重啟可能失去結果，請下載核對表 CSV。
- 找不到 app.py：確認儲存庫分支及 Main file path；避免多包一層資料夾。
- ModuleNotFoundError：確認 requirements.txt 和 app.py 在同一層，檢查部署紀錄的安裝錯誤。
- 不同的 Gemini 模型可能不支援目前使用的 Interactions API，請先以原先成功的模型驗收。
- 本套件已檢查 Python 語法與設定格式；目前環境受套件下載網路限制，未完成此套件組合的全新安裝及雲端實測。首次部署需完成上列驗收。

本套件沿用現有程式功能與版面，新增部署所需的套件清單與淺色設定。
