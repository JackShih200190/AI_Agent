# LangGraph 筆記

## 結構化的堆疊訊息
TypedDict 與 Annotated 是 Python 型別提示（type hint）機制的一部分，用於在靜態檢查時描述資料結構與附加額外語義

```python
class State(TypedDict):
    messages: Annotated[list, add_messages]
```

StateGraph() 是 LangGraph 中的核心類別，用於建立可循環的狀態機工作流程，並通過參數化的 state schema 定義初始化圖的狀態形狀 
。該圖可在添加節點 (nodes) 與邊 (edges) 後，調用 compile() 生成可運行的實例，並在執行過程中管理狀態更新與持久化
