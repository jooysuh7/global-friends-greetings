# global-friends-greetings — 설치 안내

전 세계 기념일을 찾아, 해외 거래처·파트너에게 보낼 **이메일·왓츠앱 인사말**을 만들어 주는
Claude 스킬입니다. 기념일 220건 / 93개국 데이터가 안에 들어 있습니다.

---

## 설치

**방법 1 — 버튼 (가장 쉬움)**
Claude 대화에 이 `.skill` 파일을 올리면 카드에 **Save skill** 버튼이 뜹니다. 누르면 끝입니다.
(조직 정책에 따라 버튼이 안 보일 수 있습니다 → 방법 2)

**방법 2 — 직접 넣기**
1. 파일 확장자를 `.skill` → `.zip` 으로 바꾸고 압축을 풉니다
2. 나온 `global-friends-greetings` 폴더를 통째로 아래 위치에 넣습니다
   - macOS / Linux: `~/.claude/skills/`
   - Windows: `%USERPROFILE%\.claude\skills\`
3. Claude를 다시 시작합니다

폴더 이름은 **그대로 두세요.** 바꾸면 인식되지 않습니다.

## 필요한 것

**파이썬 3.9 이상.** 이게 전부입니다.
설치할 패키지 없고, 인터넷도 필요 없습니다 — 기념일 데이터가 파일 안에 들어 있습니다.
macOS·리눅스는 보통 이미 깔려 있고, 윈도우는 [python.org](https://www.python.org/downloads/)에서 받으면 됩니다.

확인: 터미널에서 `python3 --version`

---

## 쓰는 법

설치하고 나면 Claude에게 평소처럼 말하면 됩니다.

- "다음 달에 인사 보낼 데 있어?"
- "사우디 거래처한테 이드 인사말 써줘"
- "베트남 뗏 언제야? 언제 보내야 해?"
- "연말 인사말 돌릴 건데 나라별로 정리해줘"
- "지금 인도에 보내면 몇 시에 도착해?"

세 가지를 챙겨 줍니다.

| | |
|---|---|
| **날짜** | 이슬람력·음력·힌두력은 매년 움직이고 나라마다 ±1일 다릅니다. 스크립트가 계산합니다 |
| **톤** | 축하할 날인지 추모할 날인지 구분합니다. 앤작데이에 "Happy"를 붙이는 사고를 막습니다 |
| **발송 시각** | 상대 현지 아침에 닿으려면 내 시계로 몇 시에 눌러야 하는지 계산합니다 |

### 발송자가 한국이 아니라면

기본값이 한국시간(KST)입니다. 다른 곳에서 보낸다면:

```bash
python3 scripts/sendtime.py --country SA --date 2027-03-09 --home Europe/Berlin
```

Claude에게 "나는 베를린에서 보낸다"고 한 번 말해 두면 알아서 붙여 줍니다.

---

## 안에 든 것

| 파일 | 역할 |
|---|---|
| `SKILL.md` | 워크플로 |
| `data/occasions.csv` | 기념일 220건 (2026~2028) |
| `data/countries.csv` | 93개국 타임존·주말·호칭·휴무기간 |
| `scripts/upcoming.py` | 캘린더 조회 |
| `scripts/sendtime.py` | 발송 시각·마감 계산 |
| `references/greeting-craft.md` | 톤·종교예절·호칭·금기·문형 |
| `references/country-notes.md` | 섞으면 안 되는 명단 조합, 휴무 기간, 연말 문구 |
| `assets/sample-messages.md` | 15개 기념일 완성 샘플 |

`SKILL.md` 하나만 있으면 동작하지 않습니다. 폴더 전체가 필요합니다.

## 알아둘 것

- 문서는 **한국어**입니다. 산출물(이메일·왓츠앱 문안)은 영어로 나옵니다
- 이동일(이드·춘절·디왈리 등)은 **2028년까지** 채워져 있습니다. 매년 갱신이 필요합니다
- 출처가 갈리는 날짜(오만 국경일, 2028년 이드 등)는 "확인 전 발송 금지"로 표시해 뒀습니다

---

## English

A Claude skill that finds public holidays and national days worldwide and drafts
**email and WhatsApp greetings** for overseas partners. Covers 220 occasions across 93 countries.

**Install** — upload the `.skill` file to Claude and click **Save skill**; or rename it to `.zip`,
unzip, and drop the `global-friends-greetings` folder into `~/.claude/skills/`
(`%USERPROFILE%\.claude\skills\` on Windows). Keep the folder name unchanged.

**Requires** Python 3.9+. No packages to install, no internet needed.

**What it does** — resolves moving dates (Hijri, lunar, Hindu calendars), flags whether an occasion
is celebratory or solemn so you never write "Happy" on a day of mourning, and computes what time to
hit send in *your* time zone so the message lands on the recipient's morning.

Note: the skill's own documentation is written in Korean. The greetings it produces are in English.
