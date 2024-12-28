## CrewAI
### CrewAI Flows

```python
from crewai.flow.flow import Flow, listen, start
from litellm import completion

class WebvulnFlow(Flow):
    model = "gpt-4o-mini"

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

flow = WebvulnFlow()
result = flow.kickoff()

print(f"結果: {result}")
```
