# Factory OHT Scheduling Simulator

網頁式工廠 OHT 搬運排程模擬系統。使用者可輸入 Lot 資料、OHT 數量與排程法，系統會輸出排程結果、Gantt Chart、KPI 與 Excel 報表。

## 功能

- 支援 FCFS、EDD、SPT 三種排程法
- 多台 OHT 事件驅動分派
- Sample Dataset 一鍵載入
- 排程結果表、KPI、Gantt Chart
- Excel 報表匯出，包含：
  - `Input_Data`
  - `Schedule_Result`
  - `KPI`
  - `Gantt_Data`

## 專案結構

```text
backend/
  app/
    main.py
    models.py
    scheduler/
    services/
  tests/
frontend/
  src/
```

## 後端啟動

```powershell
cd backend
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
uvicorn app.main:app --reload --port 8000
```

API 文件：

```text
http://localhost:8000/docs
```

## 前端啟動

```powershell
cd frontend
npm install
npm run dev
```

預設前端網址：

```text
http://localhost:5173
```

## 測試

```powershell
cd backend
pytest
```

若尚未安裝 pytest，也可以先跑內建 smoke test：

```powershell
cd backend
python scripts/smoke_test.py
```

## API

### 建立排程

```http
POST /api/projects
```

Request:

```json
{
  "ohtCount": 2,
  "algorithm": "SPT",
  "lots": [
    { "lotId": "L1", "releaseTime": 0, "transportTime": 8, "dueTime": 10 }
  ]
}
```

### 匯出 Excel

```http
GET /api/projects/{projectId}/export
```

Response:

```text
application/vnd.openxmlformats-officedocument.spreadsheetml.sheet
```

檔名格式：

```text
Scheduling_Report_YYYYMMDD_HHMMSS.xlsx
```
