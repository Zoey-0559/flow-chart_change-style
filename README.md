#### 兩套工具，對應兩種情境：
1. `flowchart-change-style`
> 過 Mermaid，直接依設計 token 重畫成 SVG。

2. `flow-chart-style`
> Mermaid 套用樣式直接生成，本身有主題／樣式選項限制，將視覺語言改寫成符合 Mermaid 生成規範的 config／skill；
[https://github.com/Zoey-0559/mermaid-build_flow-chart-fixed](https://github.com/Zoey-0559/mermaid-build_flow-chart-fixed)

#### 效率排序（快 → 慢）
| 1（最快） | **Mermaid 預設** | 直接產出 |
| 2 | **生成即美化**（`flow-chart-style`） | 一次生成就帶樣式 |
| 3（最慢） | **二次繪製**（`flowchart-change-style`） | 要先讀圖 → 建模（列節點與邊、判語意）→ 依 token 重畫 SVG → 撐版面 → 檢查零重疊 |



---


# flowchart-change-style 使用方式
**來源檔**：`flowchart_change-style.json`
**Skill 指令**: `/flowchart-change-style`
**輸出檔**：`SVG`
**備註**：
- 終端:分析資料夾有哪些檔案，選擇後直接執行圖面分析與重新繪製
- Browser:需附上圖檔


---


### 方式 1 - 用 JSON config 手動套樣式
1. 來源檔案 + `flowchart_change-style.json`
2. Prompt 關鍵句：
   > 改用此 JSON 重新繪製，**只輸出 SVG**
3. Claude 會依 JSON 的 hex 值與數字：建模（節點 id／label／語意角色、邊 source／target／語意型別）→ 選節點樣式 → 選箭頭樣式 → 折線正交、24px 圓角 → 自動撐版面（40px padding、零重疊）

### 方式 2：安裝 `flowchart-change-style` skill
**安裝後輸入即運行**：
``` /flowchart-change-style ```
（附上原圖即可。也會被「change the flowchart style」「重繪流程圖」「流程圖改樣式」「套用 Flow Chart 樣式」等語句觸發。）


---

**flowchart-change-style（SVG）**
- 此 Skill 內有兩個主要分工：
/flowchart-change-style 看圖 → 建模 → 直接吐 SVG
build_flow.py	把圖建模成 FLOWS → 腳本按資料繪製，輸出每次一致。
