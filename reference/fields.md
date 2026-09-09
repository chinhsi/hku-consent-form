# 抽取欄位表

從 proposal、HREC 申請表、訪談提綱、問卷抽取以下欄位。變數名對應語句庫裡的 `{{…}}`。

## 1. 計畫與研究者

| 變數 | 說明 | 來源 | 沒有時 |
|---|---|---|---|
| `{{title_en}}` | 研究題目，與申請表 Part A 完全一致 | proposal 標題 | 必填 |
| `{{title_zh}}` | 中文題目 | 若無則翻譯，回覆時標示「譯」 | 翻譯 |
| `{{pi_title}}` `{{pi_name}}` | 職稱＋姓名，例：Dr / Professor；副教授 | 申請表 Part A §2 | `local/pi-defaults.md`，否則問 |
| `{{pi_dept}}` | 例：Faculty of Education, The University of Hong Kong | 同上 | 預設教育學院 |
| `{{pi_phone}}` `{{pi_email}}` | 香港境內研究用電話；海外研究用 email | 同上 | 留 `[ ]` |
| `{{student_programme}}` | 研究者為學生時：MEd (specialism) / EdD / PhD | proposal | 只在學生版用 |
| `{{supervisor_name}}` `{{supervisor_email}}` | 學生研究者的導師 | 申請表 | 只在學生版用 |

## 2. 對象與場域

| 變數 | 說明 |
|---|---|
| `{{audiences}}` | 需要幾套：adult / teacher / principal / parent / student(primary, S1–3, S4–6) |
| `{{school_name}}` | 有具體學校時填；多校或招募未定時用 `[School name & address]` |
| `{{grade}}` `{{age_range}}` | 學生版必填，例：Grade 4 (aged 9–10) |
| `{{n_participants}}` | 約略人數 |
| `{{recruitment}}` | 招募管道，一句話 |
| `{{language}}` | 訪談／問卷語言，例：Chinese / Putonghua / Cantonese / English |
| `{{zh_script}}` | 中文版用繁體或簡體 |

## 3. 程序（每個活動一列）

每個活動抽：名稱、內容、地點（in person / online via Zoom or Tencent Meeting / in school）、時長、次數、是否錄音／錄影、是否收學生作品或系統紀錄。

| 變數 | 說明 |
|---|---|
| `{{procedures}}` | 第二人稱白話段落，含時長 |
| `{{procedures_child}}` | 家長版：以「your child／貴子弟」改寫 |
| `{{procedures_student}}` | 學生版：條列，短句 |
| `{{period}}` | 資料收集起訖，例：September 2026 to January 2027；須與申請表 Part A 相同 |
| `{{total_time}}` | 每位受試者總時間 |
| `{{recording}}` | none / audio / video / audio+video；group video 要另加「鏡頭外或模糊」句 |
| `{{other_data}}` | 訪談與問卷以外的資料：學生作品、平台紀錄、公開社群媒體內容、既有資料。**每一項都必須同時出現在 proposal 方法段與申請表 Q8** |
| `{{data_matching}}` | 多來源資料是否用代碼配對（申請表 Q10(l)） |

## 4. 風險、補償、效益

| 變數 | 預設 |
|---|---|
| `{{risks}}` | 「不高於日常生活的最低風險」，不要寫 Not applicable。訪談若涉及個人觀點，加「可拒答任何問題」 |
| `{{compensation}}` | 無補償時寫 Not applicable；有則寫金額與用途（交通、時間） |
| `{{benefits_individual}}` | 受試者本人：反思機會、教學回饋、研究結果摘要 |
| `{{benefits_wider}}` | 對教育社群的貢獻，一到兩句 |
| `{{conflict_of_interest}}` | 研究者是受試者的老師／主管／導師時必填：不參與不影響成績、評核、關係 |

## 5. 保密與保存

| 變數 | 預設 |
|---|---|
| `{{storage}}` | 電子：encrypted, password-protected device or HKU cloud storage；紙本：locked cabinet in the researcher's office |
| `{{access}}` | research team only |
| `{{anonymisation}}` | pseudonyms；移除姓名、學校名、可辨識描述 |
| `{{retention_identifiable}}` | 首篇論文發表後 3 年（上限 5 年）；須與申請表 Q12(a) 相同 |
| `{{retention_anonymised}}` | 首篇論文發表後 3 年或「持續有研究價值期間」；須與 Q12(b) 相同 |
| `{{future_use}}` | 去識別資料是否可供日後研究免再同意；預設不寫，proposal 有提才寫 |
| `{{results_copy}}` | 是否提供研究結果摘要；預設寫「upon request」 |

## 6. 同意方式

| 變數 | 說明 |
|---|---|
| `{{consent_mode}}` | written / audio-recorded oral / online-email；須與申請表 Q11 勾選一致。線上訪談通常 written（電子簽）＋ email 皆勾 |
| `{{identified_option}}` | 個人訪談才放「I wish / do not wish to be identified」 |
| `{{hrec_ref}}` | 留樣板句：`[The reference number is indicated in the letter of approval …]` |
| `{{date_of_preparation}}` | 產出當天日期 |

## 抽取時的判斷規則

- proposal 寫「approximately 60–65 minutes」就照抄範圍，不要四捨五入。
- proposal 說「in Chinese」但受試者在內地，`{{language}}` 寫 Putonghua，中文版用簡體。
- 申請表勾了某項資料來源但 proposal 沒寫方法，先在回覆裡指出，同意書仍照申請表寫，並標示「待 proposal 補寫」。
- 校長版的 procedures 描述的是學生與老師要做什麼，不是校長要做什麼。
