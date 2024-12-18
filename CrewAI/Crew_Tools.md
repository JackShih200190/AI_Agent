## Crew_tools
和LangChian Tools 類似許多套件都已經寫成工具可以更方便的使用

### 實作範例撰寫12強棒球新聞
```python
import os
from crewai_tools import WebsiteSearchTool
from crewai import Agent, Task, Crew, LLM

os.environ["OPENAI_API_KEY"] = os.getenv("OPENAI_API_KEY")
# 設定大語言模型
llm = LLM(
    model="o1-preview",
    temperature=0.5,
    max_tokens=4000
)
# 設定工具
tool = WebsiteSearchTool(website='https://news.pts.org.tw/article/725734')

# 設定Agent 
#llm = LLM(model="ollama/llama3.2:latest", base_url="http://localhost:11434")
reporter = Agent(
    role='運動新聞記者',
    goal='完成運動新聞撰寫',
    backstory="以臺灣慣用語和繁體中文來撰寫，你是一位撰寫多篇運動新聞的記者",
    tools=[tool],
    llm=llm
)

task1 = Task(
    description='完成12強棒球冠軍賽新聞稿',
    agent=reporter,
    expected_output="運動體育新聞搞"
)

# 建立 Crew
crew = Crew(
    agents=[reporter],
    tasks=[task1],
    verbose=True
)

# 執行 Crew
result = crew.kickoff()
print(result)

```

[Crew_tools](https://docs.crewai.com/concepts/tools)
1. Browserbase Web Loader
2. Code Docs RAG Search
3. Code Interpreter
4. Composio Tool
5. CSV RAG Search
6. DALL-E Tool
7. Directory RAG Search
8. Directory Read
9. DOCX RAG Search
10. EXA Search Web Loader
11. File Read
12. File Write
13. Firecrawl Crawl Website
14. Firecrawl Scrape Website
15. Firecrawl Search
16. Github Search
17. Google Serper Search
18. JSON RAG Search
19. MDX RAG Search
20. MySQL RAG Search
21. NL2SQL Tool
22. PDF RAG Search
23. PG RAG Search
24. Scrape Website
25. Selenium Scraper
26. Spider Scraper
27. TXT RAG Search
28. Vision Tool
29. Website RAG Search
30. XML RAG Search
31. YouTube Channel RAG Search
32. YouTube Video RAG Search
