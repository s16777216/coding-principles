---
name: coding-principles-zh
description: 專門針對 AI 程式碼生成與修改的核心防護與開發原則。強制執行 DRY、KISS、YAGNI、SoC、SOLID、最小改動原則與雙語文件化規則。
---

# 系統指令：程式碼生成與重構防護規範

在檢查、生成或修改程式碼時，您 **MUST** 嚴格遵守以下執行約束：

## 1. 執行範圍與安全規則

### 最小改動原則（影響範圍控制）
* **STRICT RULE:** 您 **MUST ONLY** 修改滿足使用者明確請求所直接需要的程式碼。
* **FORBIDDEN:** 絕不 **FORBIDDEN** 對未被明確要求觸及的周遭程式碼進行「順便」的重構、重新排版或樣式修改。
* **FORBIDDEN:** 絕不 **FORBIDDEN** 重新命名超出任務範圍的現有變數、函式或類別。

### YAGNI 與 KISS（範圍與複雜度控制）
* **STRICT RULE:** **ONLY** 實作當前被請求的功能。選擇能正確解決任務的最簡單實作方式。
* **FORBIDDEN:** 絕不 **FORBIDDEN** 為了「未來擴充」而引入推測性的抽象、泛型介面、未被要求的設計模式或額外的設定層。

---

## 2. 架構與設計完整性

### DRY（不重複原則）
* 在寫入新的邏輯或共用方法之前，您 **MUST** 先搜尋程式碼庫，檢查是否已有權威的函式或 Helper 存在。
* 優先重複使用現有的模組，而不是重複實作相同的細節。

### SoC（關注點分離）與 SOLID 原則
* **Single Responsibility:** 確保每個被修改或建立的模組／函式只負責一項特定的工作。
* **Layer Isolation:** 保持介面邏輯、商業規則與資料存取嚴格分離：
  - UI 元件 **MUST NOT** 包含直接的原始 API/資料庫操作或複雜的資料轉換。
  - Controller/Handler **MUST NOT** 直接執行資料庫查詢；必須委託給 Service/Repository 處理。

---

## 3. 雙語文件與脈絡規則

在撰寫程式碼註解、變數命名與文件時，請遵循 **「意圖驅動與雙語脈絡」** 協議：

1. **命名規範（標準化英文）：**
   - 所有程式碼識別字（變數、函式、型別、介面、類別） **MUST** 使用標準且專業的英文。
   - 核心業務領域名詞 **MUST** 嚴格遵循專案標準化的領域名詞對照表（Domain Glossary）。絕不進行直譯或各自造字。

2. **程式碼註解（繁體中文與業務脈絡）：**
   - **Code specifies "HOW"; Comments explain "WHY" and "CONTEXT".**
   - 請使用繁體中文編寫註解，特別是用於解釋：
     * 複雜的商業邏輯、邊界條件與法規限制。
     * 特殊的例外處理或權宜之計（Workarounds）。
   - **FORBIDDEN:** 撰寫只是重複描述程式碼在做什麼的冗餘註解。

---

## 4. 產出前自我檢查清單

在輸出最終的程式碼修改或檔案寫入之前，請進行以下內部自我審查：
1. Did I touch any code unrelated to the requested task? (若有 -> 請還原該變更)
2. Did I introduce unnecessary abstractions or generic interfaces? (若有無 -> 進行簡化)
3. Are technical identifiers in standard English and complex business comments in Traditional Chinese? (若否 -> 修正註解與命名)
