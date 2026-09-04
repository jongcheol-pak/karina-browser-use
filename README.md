# maid-browser-use

[Maid](https://github.com/jongcheol-pak/Maid) 의 **브라우저 사용** 스킬이 배포되는 자리다.
agent 가 Maid 앱 «안»의 브라우저 탭을 셸에서 조종할 수 있게 하는 능력을 알려 준다.

## 이 저장소에 있는 것

`SKILL.md` 하나뿐이고, 그것은 **discovery stub** 이다 — 명령 목록·플래그·오류 표 같은
**전문은 여기 없다.** 전문은 Maid 바이너리가 낸다:

```text
maid-cli skills get maid-browser-use
```

**일부러 그렇게 했다.** 사용법을 이 파일에 적으면 Maid 가 판을 올릴 때마다 이 파일이
뒤처지고, 그러면 **실제로 명령을 처리할 바이너리와 다른 것을 읽은 agent** 가 없는 플래그를
쓰게 된다. 바이너리가 스스로 내면 그 어긋남이 원리적으로 생기지 않는다.

## 설치

Maid 의 **설정 → 워크플로 → 브라우저**에서 맨 위의 「Agent 브라우저 사용」을 켜고 두 단계
(① Maid CLI 활성화 ② Browser Use 스킬)를 마친다. 2단계가 이 저장소의 `SKILL.md` 를 받아
`~/.agents/skills/maid-browser-use/SKILL.md` 에 놓는다. 원격에 닿지 못하면 앱에 들어 있는
판을 대신 놓으므로 오프라인에서도 설치된다.

## 무엇을 할 수 있나

- **탭 다루기** — 열려 있는 브라우저 탭을 나열하고, 하나를 자세히 보고, 활성 탭을 바꾸고,
  새로 열고(프로필 지정 가능), 닫는다.
- **이동** — 주소로 보내고, 뒤로·앞으로 가고, 새로고침하고, 다 읽을 때까지 기다린다.
- **페이지 읽기** — 역할과 이름의 들여쓰기 트리로 페이지를 내고(각 줄에 요소 참조가 붙는다),
  그 참조로 요소 하나의 글·HTML·값·위치를 읽거나 보임·활성·체크 여부를 묻는다. 임의의
  JavaScript 식을 페이지에서 돌려 그 값을 받을 수도 있다.

**사용자의 실제 로그인 위에서 돈다.** 사용자가 시키지 않은 양식 제출·구매·삭제·계정 설정
변경은 하지 않는다.

## 자매 스킬

| 스킬 | 언제 |
|---|---|
| [`computer-use`](https://github.com/jongcheol-pak/computer-use) | Maid 밖의 브라우저 창(Chrome·Edge)과 그 밖의 모든 데스크톱 UI |
| [`maid-orchestration`](https://github.com/jongcheol-pak/maid-orchestration) | agent 터미널 사이의 조정(메시지·작업 배분·게이트) |
