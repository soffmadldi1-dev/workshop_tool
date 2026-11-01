# 중동 상품화 워크숍 프롬프트 메이커

2026 알람아라비코리아 하반기 2차 세미나 · 부산 중동 타깃 연계 상품화 워크숍(2026. 11. 2.) 참가자용 단일 페이지 도구입니다.
참가자가 결과판 아이디어를 입력하면 AI 채팅창에 붙여넣을 프롬프트 4종을 만들어 줍니다. 페이지 안에서 AI를 호출하지 않습니다.

- 배포 주소(예정): https://soffmadldi1-dev.github.io/workshop_tool/
- `qr.png`: 위 주소의 QR 코드(발표 장표용)

## 파일

| 파일 | 내용 |
|---|---|
| `index.html` | 메이커 본체(바닐라 JS, 외부 리소스는 Pretendard 폰트 CDN v1.3.9 하나) |
| `qr.png` | 배포 주소 QR |
| `.nojekyll` | GitHub Pages 처리 생략용 |

## 수정 포인트 (`index.html` `<script>` 안)

| 무엇을 | 어디 | 비고 |
|---|---|---|
| 조 프리셋(테마·타깃·조 구성·과제·페르소나) | `var TEAMS` (약 637행) | `members: [['회사명','역할']]`, 회사명만 표기 |
| 조별 입력 예시(placeholder) | `var EX` (약 674행) | `'예:'`로 시작, 키는 각 입력칸의 `data-k`와 같음 |
| 전체 복사·.txt·결과판 공유 항목 이름 | `var FIELDS` (약 763행) | `board:true` 인 항목이 결과판 공유/붙여넣기 대상 |
| 공통 규칙(4종 공통) | `var RULES` (약 1011행) | |
| 공통 맥락 블록 | `ctxEvent` · `ctxTeam` · `ctxMe` · `ctxBoard` · `ctxComment` | 행사 정보·참고 수치 출처는 `ctxEvent` |
| 프롬프트 본문 | `function P1()` ~ `function P4()` (약 1095~1278행) | 빈 입력은 `v()`가 `(확인 필요)`로 바꿈 |
| 카드 제목·용도·팁 | `var PROMPTS` (약 1279행) | |
| 저장 키 | `STORE_KEY` | 값을 바꾸면 기존 기기 저장값은 무시됨 |

## 배포 (GitHub Pages)

1. 저장소 **Settings → Pages**
2. Source: **Deploy from a branch**
3. Branch: `claude/loving-hypatia-0ebj8s`(또는 병합한 `main`) / `/ (root)` → Save
4. 1~2분 뒤 https://soffmadldi1-dev.github.io/workshop_tool/ 접속 확인

다른 저장소 이름(예: `alarm-arabi-workshop`)으로 옮기면 주소가 바뀌므로 `qr.png`를 다시 만들어야 합니다.

```bash
pip install qrcode && python3 -c "import qrcode; qrcode.make('https://<계정>.github.io/<저장소>/', box_size=24, border=4).save('qr.png')"
```

## 점검 결과 (2026. 11. 1.)

- PC 1180px / 모바일 390px, STEP 1~5 전체: 가로 스크롤 없음(`scrollWidth ≤ clientWidth`), 박스 넘침 없음, 입력칸 16px 이상, 버튼 44px 이상
- 1·2·3조 선택 시 테마·조 구성·페르소나·예시 문구 변경
- 빈 입력 → 4종 모두 `(확인 필요)` 처리, `undefined/null` 없음
- 복사 버튼·복사 실패 시 전체 선택 fallback·전체 복사·.txt 저장·결과판 공유/붙여넣기·새로고침 유지·다시 시작(모든 필드와 localStorage 삭제)
- `grep -i "kakao\|yosep\|홍요셉"` 0건, JS 문법 오류 0건
