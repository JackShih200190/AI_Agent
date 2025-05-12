# Memory 記憶模駔
使用Memory 元件的主要原因包括以下幾點：
- 儲存上下文資訊： Memory 元件能儲存多種形式的資訊，無論是歷史對
  話內容、即時交流資訊，還是外部檔案資料，都能被記憶並在必要時引
  用。這使得對話不僅基於當前的交流，而且建立在一個豐富的資訊背景之上。
- 檢索資訊： Memory 不僅是簡單的存放裝置，它還可以作為一個高效的
  檢索系統。它不僅能基於電腦記憶體，還可以基於向量資料庫，根據語
  義相關度找到與輸入最相關的資訊．即使這些資訊在字面上並非完全匹配。

可以讓LLM使用到之前的內容來增加回答的精準度

## 將歷史對話直接儲存成Memory (皆停止支援)
~~1. ConversationBufferMemory~~
~~2. ConversationBufferWindowMemory~~
~~3. ConversationTokenBufferMemory~~
