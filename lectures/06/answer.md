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

- 取り組んだレベル：基礎
- やったこと：Added `server.tool()(tools.get_lecture_summary)` to app/mcp_server.py only. No changes to mcp_servers.json or mcp_agent.py.
- 結果：--list-tools showed 8 tools including glossary_get_lecture_summary. For "第2回では何を学びますか？" the trace showed [tool call] glossary_get_lecture_summary({'lecture': 2}) and the answer matched the Session 2 summary (fine-tuning and LoRA). pytest: 21 passed.
- 気づき・疑問：
  - The agent fetches the tool list from the server on every startup, so adding a tool on the server side is enough. The agent needs no changes.
  - The docstring became the tool description and the type hint (int) became the argument schema, so the model converted "第2回" into the integer 2. Writing a clear docstring is effectively prompt engineering for tools.
