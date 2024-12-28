## CrewAI
### CrewAI Flows

```python
from crewai.flow.flow import Flow, listen, start
from litellm import completion

class WebvulnFlow(Flow):
    model = "gpt-4o-mini"

    # 啟動Flow 需使用@start()來啟動
    @start()
    def generate_web_vuln(self):
        print("Starting flow")
        response = completion(
            model=self.model,
            messages=[
                {
                    "role": "user",
                    "content": "回傳一個OWASP Top 10的漏洞名稱",
                },
            ],
        )
        web_vuln = response["choices"][0]["message"]["content"]
        print(f"Random web_vuln: {web_vuln}")

        return web_vuln
    # 監聽上一個任務完成的return來啟動下一個流程
    @listen(generate_web_vuln)
    def generate_vuln_description(self, web_vuln):
        response = completion(
            model=self.model,
            messages=[
                {
                    "system": "資訊安全研究生",
                    "role": "user",
                    "content": f"告訴我 {web_vuln}的攻擊方式和防護措施",
                },
            ],
        )
        vuln_description = response["choices"][0]["message"]["content"]
        return vuln_description

# 將整個Flow啟動來工作
flow = WebvulnFlow()
result = flow.kickoff()

print(f"結果: {result}")
```
output
---
Starting flow<Br>
Random web_vuln: OWASP Top 10中的一個漏洞名稱是「A1:2021 - Broken Access Control」（破損的訪問控制）。這個漏洞指的是應用程式未能正確限制用戶對資源的訪問，可能導致未經授權的操作。
結果: 「A1:2021 - Broken Access Control」（破損的訪問控制）是OWASP Top 10中一個重要的安全漏洞，這一漏洞涉及未能正確限制用戶對應用程式資源的訪問，可能導致攻擊者執行未經授權的操作。以下是這個漏洞的攻
擊方式及防護措施：

### 攻擊方式

1. **URL Manipulation（URL竄改）**：
   攻擊者可以通過手動修改網址中的參數來試圖訪問未授權的資源，這包括改變ID或其他識別信息。

2. **HTTP Method Abuse（HTTP方法濫用）**：
   利用HTTP請求方法（如PUT、DELETE）來試圖執行不應有的操作。

3. **Session Fixation（會話固定）**：
   攻擊者可能通過固定或竄改會話ID來訪問用戶的會話，以便執行未經授權的操作。

4. **Brute Force（暴力破解）**：
   攻擊者可能用自動化腳本嘗試獲取用戶權限，通過猜測用戶名和密碼來提升訪問權限。

5. **Access Control Bypass（繞過訪問控制）**：
   在應用程式中，如果未對訪問權限進行適當的驗證，攻擊者可能通過某些漏洞直接訪問內部API或敏感資源。

### 防護措施

1. **最小權限原則**：
   確保使用者和服務僅擁有執行其工作所需的最低權限，通過適當的角色和權限管理來限制訪問。

2. **強制訪問控制**：
   在服務器端實施強制訪問控制，確保每次請求都經過驗證和授權，不僅僅依賴客戶端的檢查。

3. **驗證和授權**：
   對所有敏感操作進行適當的驗證和授權，包括檢查用戶的身份以及他們的權限是否足夠。

4. **使用安全的認證方法**：
   現在許多應用程序傾向於使用OAuth 2.0等現代認證方法來增強安全性。

5. **日誌和監控**：
   實施日誌記錄和實時監控，幫助檢測可疑的訪問模式和潛在的攻擊。

6. **定期測試和評估**：
   進行定期的安全測試和代碼審計，以找出可能的訪問控制漏洞。

通過實施這些防護措施，可以顯著降低因「A1:2021 - Broken Access Control」漏洞而導致的風險，提高應用程式的整體安全性。
