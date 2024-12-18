## CrewAI
### 三項必須做到事項
定義Agent、定義Task、建立crew

## Agent 
設定 Agent 腳色的角色定義和背景，並給與每一個Agent都有自己的目標需要去完成
Agent Attributes 常見幾個參數
| Attribute	| Parameter|	Description| 
|  ----  | ----  | ---- |
Role|	role	|	定義Agent角色的職位或技能|
Goal|	goal	|定義Agent的個人目標|
Backstory|	backstory|定義Agent角色的背景和個人特點|
LLM | llm | 設定Agent要使用的語言模型|
Verbose | verbose | 啟動Log來進行Debug|
Allow Delegation | allow_delegation | 允許Agent可以將任務丟給其他Agent來執行|
## Task
設定任務的內容和指定Agent角色
| Attribute	| Parameter|	Description| 
|  ----  | ----  | ---- |
Description|	description	|	簡單的訴說任務內容|
Expected Output	|expected_output	|任務完成情況的詳細描述|
Agent |	Agent | 設定此任務要執行的Agent |

## Crew
使用CrewAI的框架來將Agent 和 Task 整合運作
| Attribute	| Parameter|	Description| 
|  ----  | ----  | ---- |
Tasks	|tasks	|A list of tasks assigned to the crew.|
Agents|	agents	|A list of agents that are part of the crew.|
