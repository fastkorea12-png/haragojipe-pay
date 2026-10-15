# 로컬 검수

`head.html`은 fetch 모의 서버입니다. 로그인 비밀번호는 `demo`이며 데이터는 직원A·직원B·직원C·사장으로 만든 예시입니다.

```sh
python3 -c 'from pathlib import Path; p=Path("index.html").read_text(); Path("qa/index.html").write_text(p.replace("<script>",Path("qa/head.html").read_text()+"<script>",1))'
python3 -m http.server 8765
```

http://localhost:8765/qa/phone.html 또는 /qa/index.html 에서 로그인·주간표·급여·명세서를 확인합니다. 모의 API는 `/api/admin/login`, `/api/pay/state`, `/api/pay/doc`와 버전 충돌을 흉내 냅니다. 생성한 qa/index.html은 커밋하지 않습니다.

근무 기록 검수 기준(2026-10-15): 직원A는 10월 예정 7건·30시간, 실제 25시간이며 근무함·시간 다름·결근·미확인 각 1건입니다. 나머지 3건은 미래 예정입니다. 결근을 근무함으로 바꾸면 실제 29시간이며, 급여 계산에서 예상 옵션을 끈 직원A 시간도 29시간이어야 합니다. 네 상태의 과거 4건만 보면 예정 16시간·실제 11시간입니다.

1440px와 390px에서 선택된 직원 이름·가능 표시, 시간 `6.5-10.5`, 긴 비고의 표시와 `document.documentElement.scrollWidth === document.documentElement.clientWidth`를 확인합니다. 기록 탭에서 사람 필터, 월 이동, 실제 시간 수정, 카톡 복사 및 스케줄 탭과의 상태 동기화를 확인합니다.
