## Crew_tools
和LangChian Tools 類似許多套件都已經寫成工具可以更方便的使用


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
### 輸出
```
# Agent: 運動新聞記者
## Thought: Thought: 我要撰寫12強棒球冠軍賽的新聞稿，但是需要先搜集相關資訊。我可以使用"Search in a specific網站"工具來獲取最新資訊。
## Using tool: Search in a specific website
## Tool Input:
"{\"search_query\": \"12\\u5f37\\u68d2\\u7403\\u8cfd\"}"
## Tool Output:
Relevant Content:
12強／台灣首度在3大賽事奪冠 斬斷日本國際大賽27連勝 ｜......

# Agent: 運動新聞記者
## Final Answer:
**12強棒球賽中華隊奪冠 4比0完封日本創歷史**

2024年11月24日晚間，世界棒球12強賽在東京巨蛋迎來萬眾矚目的冠軍戰，中華隊與日本隊再度交鋒。中華隊以4比0擊敗日本隊，史上首次在三大賽事奪冠，斬斷日本隊在國際大賽27連勝的紀錄，寫下台灣棒球新的里程碑。

本場比賽，中華隊派出王牌左投林昱珉先發，他展現出色的投球實力，主投4局無失分，成功壓制日本隊強大的打線。林昱珉在前兩局讓日本隊6上6下，更霸氣送出2次三振；第三局面對日本隊的一三壘有人，他沉著應戰，成功化解危機。第四局
，隊友的精彩守備也助他一臂之力，外野手、隊長陳傑憲上演美技接殺，二壘手岳東華則有精彩的撲接表現。

中華隊的攻勢在第五局上半展開。捕手林家正一棒敲出中右外野方向的陽春全壘打，打破場上僵局，幫助中華隊取得1比0的領先。隨後，陳晨威擊出安打、林立選到保送，攻佔一二壘。這時，隊長陳傑憲挺身而出，面對日本王牌投手戶鄉翔征，
他一記揮棒，將球送上右外野看台，轟出3分全壘打，將比數擴大至4比0。

之後，中華隊的牛棚投手群表現穩定。中繼投手張奕投了3局，封鎖日本隊的反攻，拿下本屆賽事個人第3勝，累積5勝成為世界棒球12強賽勝投王。老將陳冠宇在第八局上場，演出三上三下的好投。第九局，日本隊試圖反撲，但林凱威在隊友的 
守備支援下，完成了關鍵的雙殺，最終中華隊以4比0完封日本隊。

這場勝利意義非凡，不僅是中華隊首次在包含奧運、經典賽和12強的三大賽事中奪冠，也終結了日本隊在國際大賽27連勝的紀錄。隊長陳傑憲在本場比賽中表現出色，獲選為賽事最有價值球員（MVP），並包辦最佳外野手、最佳防守球員及打擊 
王等個人獎項。

賽後，全隊將獲得超過3.1億元的獎金，包括中華棒球協會理事長辜仲諒的獎勵、國光獎章以及世界棒壘球聯盟（WBSC）的獎金。此外，各地政府也表示將對來自該縣市的選手提供額外獎勵。

中華隊的勝利引發全國歡騰，許多球迷自發性上街慶祝。台灣棒球再度站上世界舞台，展現了團結與實力。正如隊長陳傑憲所說：「記住勝利的滋味，未來我們會繼續努力，為台灣爭光。」

**相關新聞：**

- 台灣英雄大遊行熱情展開，球迷夾道歡迎中華隊凱旋歸國。
- 總統接見中華隊，讚揚球員們的奮戰精神，並承諾加強體育資源。
- 棒球帶動全台熱潮，專家呼籲持續深化基層棒球培育。

**延伸閱讀：**

- 12強賽事精彩回顧：中華隊的奪冠之路。
- 日本隊強勢受挫，賽後檢討未來調整方向。
- 台灣棒球的未來：從基層培育到國際舞台。
```
