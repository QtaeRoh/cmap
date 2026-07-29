# C-MAP · AI 시대 진로·전공 적합도 진단 (웹 검사 페이지)

올인원에듀 자체 진단 도구 C-MAP의 온라인 검사 페이지입니다.

- `index.html` — 배포되는 검사 페이지 (104문항 임베드 완성본)
- `index_template.html` — 소스 템플릿 (`__QUESTIONS__` 자리에 문항 배열 주입)
- `questions_data.json` — 화면 표시 순서의 104문항 (no·qid·text)

## 수정 방법
문구·디자인 수정은 `index_template.html`에서 하고, 아래로 재생성:

```python
import json, io
tpl = io.open("index_template.html", encoding="utf-8").read()
qs  = json.load(io.open("questions_data.json", encoding="utf-8"))
io.open("index.html", "w", encoding="utf-8").write(
    tpl.replace("__QUESTIONS__", json.dumps(qs, ensure_ascii=False, separators=(",",":"))))
```

## 제출 방식
`index.html`의 `CONFIG.ENDPOINT`가 비어 있으면 응답 JSON 파일 다운로드,
서버 주소를 넣으면 해당 주소로 POST 제출됩니다.

© 올인원에듀 · 손용식(용쌤). 문항·채점 로직은 올인원에듀의 자산입니다.
