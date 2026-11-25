# 第6回 解答

## 演習

- STEP 1 のツールの名前：glossary_search_glossary
- STEP 2 の [tool call]：glossary_search_glossary({'query': '3レベル'})
- STEP 3 の [tool call]：fetch_fetch({'url': 'https://modelcontextprotocol.io/'})
- STEP 4 の [tool call]：aws_aws___search_documentation({'topics': ['general'], 'search_phrase': 'Amazon S3 versioning overview'})
- 気づき・疑問：
  - Tool descriptions are written by the server's author and passed to the model unchanged. fetch's description even contains instructions to the model ("this tool now grants you internet access"), so a malicious server could inject instructions. Check the provider before adding a server.
  - Input tokens rose from 715 (glossary) to 2,224 (fetch) to 6,345 (aws). Tool results and every tool's description are sent with each request, so adding servers increases cost.
  - The aws answer came back in Japanese although I asked in English (probably because the agent's instructions are in Japanese).

## 宿題

<!-- 基礎・実装・発展のどれか1つに取り組めば完了です。 -->

- 取り組んだレベル：基礎 / 実装 / 発展
- やったこと：
- 結果：
- 気づき・疑問：
