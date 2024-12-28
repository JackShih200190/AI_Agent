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
