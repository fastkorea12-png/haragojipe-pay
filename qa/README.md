# 로컬 검수

`head.html`은 fetch 모의 서버입니다. 로그인 비밀번호는 `demo`이며 데이터는 직원A·직원B·직원C·사장으로 만든 예시입니다.

```sh
python3 -c 'from pathlib import Path; p=Path("index.html").read_text(); Path("qa/index.html").write_text(p.replace("<script>",Path("qa/head.html").read_text()+"<script>",1))'
python3 -m http.server 8765
```

http://localhost:8765/qa/phone.html 또는 /qa/index.html 에서 로그인·주간표·급여·명세서를 확인합니다. 모의 API는 `/api/admin/login`, `/api/pay/state`, `/api/pay/doc`와 버전 충돌을 흉내 냅니다. 생성한 qa/index.html은 커밋하지 않습니다.
