<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "c692a8975d7d5b99575a553de1c5e8a7",
  "translation_date": "2025-07-12T10:56:30+00:00",
  "source_file": "08-multi-agent/README.md",
  "language_code": "mo"
}
-->
[![Multi-Agent Design](../../../translated_images/lesson-8-thumbnail.278a3e4a59137d625df92de3f885d2da2a92b1f7017abba25a99fb25edd83a55.mo.png)](https://youtu.be/V6HpE9hZEx0?si=A7K44uMCqgvLQVCa)

> _(點擊上方圖片觀看本課程影片)_

# 多代理設計模式

當你開始著手一個涉及多個代理的專案時，就需要考慮多代理設計模式。然而，何時切換到多代理系統以及其優勢可能並不那麼明顯。

## 介紹

在本課程中，我們將回答以下問題：

- 哪些情境適合使用多代理？
- 使用多代理相較於單一代理執行多項任務，有哪些優點？
- 實作多代理設計模式的基本構件有哪些？
- 我們如何能夠掌握多個代理之間的互動情況？

## 學習目標

完成本課程後，你應該能夠：

- 辨識適合使用多代理的情境
- 理解使用多代理相較於單一代理的優勢
- 了解實作多代理設計模式的基本構件

整體概念是什麼？

*多代理是一種設計模式，允許多個代理協同合作以達成共同目標*。

此模式廣泛應用於各種領域，包括機器人技術、自主系統及分散式運算。

## 適合使用多代理的情境

那麼，哪些情境適合使用多代理呢？答案是有許多情境特別適合使用多代理，尤其是在以下情況：

- **龐大工作量**：龐大的工作量可以拆分成較小的任務，分配給不同代理，讓任務能平行處理並更快完成。舉例來說，大型資料處理任務就是一個例子。
- **複雜任務**：複雜任務同樣可以拆解成多個子任務，分配給專精於特定領域的不同代理。自駕車就是一個好例子，不同代理分別負責導航、障礙物偵測及與其他車輛通訊。
- **多元專業知識**：不同代理擁有不同專業，能更有效處理任務的不同面向，勝過單一代理。醫療領域即是一例，代理分別負責診斷、治療計畫及病患監控。

## 使用多代理相較於單一代理的優勢

單一代理系統適合簡單任務，但面對較複雜任務時，使用多代理有以下幾項優勢：

- **專業分工**：每個代理可專注於特定任務。單一代理缺乏專業分工，可能在面對複雜任務時不知所措，甚至執行不適合自己的任務。
- **可擴展性**：系統擴展時，新增代理比讓單一代理負荷過重更容易。
- **容錯性**：若其中一個代理失效，其他代理仍能繼續運作，確保系統穩定性。

舉例來說，假設要為使用者訂購旅程。單一代理系統必須處理所有訂票流程，從尋找航班到訂飯店及租車。為了完成這些任務，該代理需要具備處理所有任務的工具，導致系統複雜且難以維護與擴展。相反地，多代理系統可由不同代理分別負責尋找航班、訂飯店及租車，使系統更模組化、易於維護且具擴展性。

這就像是比較由夫妻經營的小旅行社與加盟連鎖旅行社。夫妻店由單一代理處理所有訂票流程，而加盟連鎖則由不同代理分別負責不同環節。

## 實作多代理設計模式的基本構件

在實作多代理設計模式前，你需要了解組成此模式的基本構件。

讓我們以為使用者訂購旅程為例，基本構件包括：

- **代理間通訊**：負責尋找航班、訂飯店及租車的代理需要溝通並共享使用者偏好與限制。你必須決定通訊協定與方法。具體來說，尋找航班的代理需與訂飯店的代理溝通，確保飯店訂在與航班相同的日期。這表示代理間必須共享使用者的旅行日期資訊，也就是你需要決定*哪些代理共享資訊以及如何共享*。
- **協調機制**：代理需協調行動，確保符合使用者偏好與限制。例如，使用者偏好飯店靠近機場，但租車只能在機場取車，訂飯店的代理需與訂租車的代理協調，確保符合這些條件。你需要決定*代理如何協調行動*。
- **代理架構**：代理需具備內部結構以做決策並從與使用者的互動中學習。尋找航班的代理需能決定推薦哪些航班。你需要決定*代理如何做決策並從互動中學習*。例如，尋找航班的代理可使用機器學習模型，根據使用者過去偏好推薦航班。
- **多代理互動的可視化**：你需要掌握多個代理間的互動情況，這需要具備追蹤代理活動與互動的工具與技術，可能包括日誌與監控工具、視覺化工具及效能指標。
- **多代理模式**：實作多代理系統有不同模式，如集中式、分散式及混合架構，你需選擇最適合用例的模式。
- **人類介入**：大多數情況下會有人類介入，你需指示代理何時請求人工干預。例如使用者要求特定飯店或航班，代理未推薦時，或在訂票前請求確認。

## 多代理互動的可視化

掌握多代理間的互動非常重要，這對除錯、優化及確保系統整體效能至關重要。為此，你需要具備追蹤代理活動與互動的工具與技術，可能包括日誌與監控工具、視覺化工具及效能指標。

以訂購旅程為例，你可以有一個儀表板顯示每個代理的狀態、使用者偏好與限制，以及代理間的互動。此儀表板可顯示使用者的旅行日期、航班代理推薦的航班、飯店代理推薦的飯店及租車代理推薦的車輛。這能清楚呈現代理間的互動情況，以及是否符合使用者的偏好與限制。

讓我們更詳細探討這些面向：

- **日誌與監控工具**：你希望記錄每個代理執行的動作。日誌條目可包含執行動作的代理、動作內容、執行時間及結果。這些資訊可用於除錯、優化等。
- **視覺化工具**：視覺化工具能幫助你更直觀地看到代理間的互動。例如，你可以有一個圖表顯示代理間資訊流動，有助於識別瓶頸、效率低落及其他問題。
- **效能指標**：效能指標能幫助你追蹤多代理系統的效能。例如，追蹤完成任務所需時間、單位時間內完成的任務數量，以及代理推薦的準確度。這些資訊有助於找出改進空間並優化系統。

## 多代理模式

讓我們深入探討一些可用於建立多代理應用的具體模式。以下是幾個值得考慮的有趣模式：

### 群組聊天

當你想建立一個多代理能互相通訊的群組聊天應用時，此模式非常有用。典型應用包括團隊協作、客戶支援及社交網路。

在此模式中，每個代理代表群組聊天中的一位使用者，代理間透過訊息協定交換訊息。代理可以發送訊息到群組、接收群組訊息，並回應其他代理的訊息。

此模式可用集中式架構實作，所有訊息經由中央伺服器轉發，或用分散式架構，代理間直接交換訊息。

![Group chat](../../../translated_images/multi-agent-group-chat.ec10f4cde556babd7b450fd01e1a0fac1f9788c27d3b9e54029377bb1bdd1db6.mo.png)

### 任務交接

當你想建立一個多代理能彼此交接任務的應用時，此模式非常有用。

典型應用包括客戶支援、任務管理及工作流程自動化。

在此模式中，每個代理代表一個任務或工作流程中的一個步驟，代理可根據預先定義的規則將任務交接給其他代理。

![Hand off](../../../translated_images/multi-agent-hand-off.4c5fb00ba6f8750a0754bf29d49fa19d578080c61da40416df84d866bcdd87a3.mo.png)

### 協同過濾

當你想建立一個多代理能協同合作為使用者提供推薦的應用時，此模式非常有用。

多代理協同合作的原因是每個代理擁有不同專長，能以不同方式貢獻推薦過程。

舉例來說，使用者想要股票市場中最佳股票的推薦。

- **產業專家**：一個代理是特定產業的專家。
- **技術分析**：另一個代理擅長技術分析。
- **基本面分析**：還有一個代理擅長基本面分析。透過協同合作，這些代理能提供更全面的推薦給使用者。

![Recommendation](../../../translated_images/multi-agent-filtering.d959cb129dc9f60826916f0f12fe7a8339b532f5f236860afb8f16b63ea10dc2.mo.png)

## 情境：退款流程

考慮一個顧客嘗試申請產品退款的情境，這過程中可能涉及多個代理，我們將其分為專門處理退款流程的代理與可用於其他流程的一般代理。

**專門處理退款流程的代理**：

以下是可能參與退款流程的代理：

- **顧客代理**：代表顧客，負責啟動退款流程。
- **賣方代理**：代表賣方，負責處理退款。
- **付款代理**：代表付款流程，負責退還顧客款項。
- **解決代理**：代表問題解決流程，負責處理退款過程中出現的問題。
- **合規代理**：代表合規流程，確保退款流程符合相關法規與政策。

**一般代理**：

這些代理可用於業務的其他部分。

- **運送代理**：代表運送流程，負責將產品寄回賣方。此代理可用於退款流程，也可用於一般購買產品的運送。
- **回饋代理**：代表回饋流程，負責收集顧客回饋。回饋可在任何時間收集，不限於退款流程。
- **升級代理**：代表升級流程，負責將問題升級至更高層級的支援。此類代理可用於任何需要升級問題的流程。
- **通知代理**：代表通知流程，負責在退款流程的各階段向顧客發送通知。
- **分析代理**：代表分析流程，負責分析與退款流程相關的資料。
- **稽核代理**：代表稽核流程，負責稽核退款流程，確保流程正確執行。
- **報告代理**：代表報告流程，負責產生退款流程的報告。
- **知識代理**：代表知識流程，負責維護與退款流程相關的知識庫。此代理可同時具備退款及其他業務領域的知識。
- **安全代理**：代表安全流程，負責確保退款流程的安全性。
- **品質代理**：代表品質流程，負責確保退款流程的品質。

前述列出了不少代理，包含專門處理退款流程的代理，也有可用於其他業務部分的一般代理。希望這能幫助你了解如何決定在多代理系統中使用哪些代理。

## 作業
## 上一課

[規劃設計](../07-planning-design/README.md)

## 下一課

[AI 代理的元認知](../09-metacognition/README.md)

**免責聲明**：  
本文件係使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們致力於確保準確性，但請注意，自動翻譯可能包含錯誤或不準確之處。原始文件的母語版本應視為權威來源。對於重要資訊，建議採用專業人工翻譯。我們不對因使用本翻譯而產生的任何誤解或誤釋負責。