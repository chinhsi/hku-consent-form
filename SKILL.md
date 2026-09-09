---
name: hku-consent-form
description: 依研究提案（proposal / HREC 申請表）產生香港大學 HREC 格式的知情同意書：成人／教師、校長、家長／監護人、學生 assent，英文＋中文（繁或簡）。Use when user says "做 consent form"、"同意書"、"informed consent"、"/hku-consent-form"、drops a proposal and asks for consent forms, or asks to check consent forms against a proposal.
---

# hku-consent-form

從研究提案抽取欄位，套用 HKU Human Research Ethics Committee（HREC）慣用語，產出各對象版本的知情同意書（.docx）。語句庫來自 HKU 教育學院官方樣板與多份已獲批的申請，不是自創。

## 使用方式

```
/hku-consent-form <proposal 路徑或資料夾> [對象: adult|teacher|principal|parent|student] [語言: en|zh-hant|zh-hans|all]
```

不給對象與語言時，依 proposal 自行判斷（見 Step 2），再在回覆裡說明判斷依據。

## 流程

### Step 1　讀 proposal 與相關檔案

- docx 用 `pandoc <file> -t plain --wrap=none`；.doc 用 `textutil -convert txt -stdout`；pdf 用 `pdftotext -layout`。
- 同資料夾若有 HREC application form、interview protocol、questionnaire，一併讀。同意書的每一句話都必須能在這些文件裡找到依據，反之亦然（見 Step 5）。
- 若 `local/pi-defaults.md` 存在，讀取 PI 預設聯絡資料。該檔不隨 skill 公開，內容由使用者維護。

### Step 2　抽取欄位

依 `reference/fields.md` 的欄位表逐項抽取，寫成一份簡短的欄位摘要（給使用者看，也給自己用）。抽不到的欄位：

- 有慣例預設值的（風險＝minimal、補償＝無、保存＝首篇論文發表後 3 年）直接用預設並標註「預設」。
- 沒有預設的（PI 電話、資料收集起訖、學生年級）留 `[ ]` 佔位符並在回覆裡列出，不要杜撰。

**判斷對象**：proposal 提到學校場域＋未成年學生 → 校長＋家長＋學生 assent 三套；教師受訪 → teacher；成人受試者（含大學生、教師、專業人士）→ adult；研究者本人是受試者的老師／上司 → 加 conflict-of-interest 段。

**判斷中文字體**：受試者在中國內地（提到微信、小紅書、騰訊會議、普通話、內地學校）→ 簡體；香港學校／家長 → 繁體；台灣 → 繁體。拿不準就問，不要兩種都做。

### Step 3　選格式

| 對象 | 格式 | 語句庫段落 |
|---|---|---|
| adult / teacher（PI 為教職員） | 分節式（PURPOSE … SIGNATURE） | language-en.md §A、language-zh.md §A |
| teacher / professor（研究者為學生） | 信函式（Dear teacher … Reply Slip） | §B |
| principal | 信函式＋校方回條 | §C |
| parent / guardian | 分節式或信函式，用「your child／貴子弟」 | §D |
| student assent | 信函式，簡單語言，分小學／初中／高中三檔 | §E |
| 口頭或 email 同意腳本 | 短段落 | §F |

### Step 4　寫 Markdown 並轉 docx

- 每個版本一個 `.md`，檔名慣例：`consent-<audience>-<lang>.md`，例如 `consent-teacher-en.md`、`consent-parent-zh-hant.md`。
- 不要自由發揮措辭。逐段從語句庫複製，只替換 `{{變數}}`。需要增寫的（procedures 細節、benefits）用 proposal 的原話改寫成第二人稱、白話。
- 章節標題在英文版全大寫（HKU 樣板慣例）；中文版用「研究目的／程序／潛在風險…」。
- 簽名區與回條放在水平線 `---` 之後。勾選框用 `◻`，刪去不適用者用 `**同意 / 不同意`＋`(** 請删去不適用者)`。
- 轉檔：`pandoc consent-x.md -o consent-x.docx`；有 `assets/reference.docx` 時加 `--reference-doc`。
- 輸出到 proposal 所在資料夾，除非使用者指定。不覆蓋既有檔案：同名時加 `-v2`。

### Step 5　對照檢查

跑 `reference/checklist.md` 全部項目，在回覆裡列出未通過項。最常見的三類問題：

1. 同意書提到 proposal 沒寫的資料來源（例如社群媒體內容），或反過來。
2. 保存年限、錄音／錄影、同意方式，與 HREC 申請表 Q10–Q12 不一致。
3. 佔位符沒清（`[Date]`、`XX`）、PI 職稱前後不一、電話兩個版本不同。

### Step 6　回覆

列出：產出的檔案、抽取欄位摘要（含哪些是預設、哪些待填）、檢查清單未通過項。不重述同意書內容。

## 檔案

- `reference/fields.md`：抽取欄位表與預設值
- `reference/language-en.md`：英文語句庫，依對象分段
- `reference/language-zh.md`：中文語句庫，繁簡並列
- `reference/checklist.md`：送審前一致性檢查
- `local/`：使用者私有資料（PI 聯絡方式），已列入 .gitignore

## 注意

- HREC 電話用 3917-5267。舊樣板的 2241-5267 已停用，看到就改。
- 中文「Human Research Ethics Committee」繁體慣用「香港大學研究操守委員會」，簡體樣板用「香港大学人类研究伦理委员会」。
- 識別資料保存不得超過首篇論文發表後 5 年；最少 3 年。
- 未成年受試者一定要三套：校長、家長、學生 assent。學生 assent 不能取代家長同意。
- 同意書不放表情符號，也不放研究假設或文獻引用。
