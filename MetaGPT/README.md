# MetaGPT: The Multi-Agent Framework
將公司的所有角色和任務定義好，即可實現一人公司全靠AI Agent

![image](https://github.com/user-attachments/assets/d51fa9ba-d757-4c6f-a33b-eeb727c70a6e)

## Installation
```
pip install metagpt
```

> [!WARNING]
> Python 3.12版本會有套件錯誤，安裝時建議使用>=3.9 <3.12版本

> [!WARNING]
> httpx套件版本問題導致TypeError: AsyncClient.__init__() got an unexpected keyword argument 'proxies'
> https://github.com/geekan/MetaGPT/issues/1617

![image](https://github.com/user-attachments/assets/fa69526f-978e-4621-8899-20c71bcb5871)


## Install submodules 
- RAG
- OCR
- search-ddg
- search-google
- selenium
```
pip install 'metagpt[submodules_name]'
```

## Env setup
初始化設定，將會產生一個yaml檔來設定大語言模型
```cmd
metagpt --init-config
```
