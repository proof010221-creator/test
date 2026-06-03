# 루디스 .html 없는 주소 구조 + 화면전환 애니메이션 V6

작성일: 2026-06-03 17:20:36 (KST, 한국시간)

이번 버전은 기존 V5의 좋은 애니메이션과 `/ludis/` 주소 구조는 유지하고, 첫 화면에서 메인 화면으로 넘어갈 때 보이는 화면전환 애니메이션을 추가한 버전입니다.

---

## 1. 유저 공지 주소는 그대로

유저에게 안내한 주소는 계속 아래 하나만 쓰면 됩니다.

```text
https://dovitrip.kro.kr/
```

내부 이동은 아래처럼 됩니다.

```text
https://dovitrip.kro.kr/
→ 첫 화면 index.html

무료 시작 / VIP 인증 성공 / 사용 이전 성공
→ https://dovitrip.kro.kr/ludis/
```

주소창에는 `.html`이 보이지 않습니다.

---

## 2. ZIP 구성

```text
index.html
ludis/
└─ index.html
README_KR.txt
```

GitHub에 올려야 하는 것은 아래 2개입니다.

```text
1. index.html
2. ludis 폴더 전체
```

GitHub 저장소 루트 구조가 이렇게 보여야 합니다.

```text
proof 저장소 루트
├─ index.html
└─ ludis
   └─ index.html
```

---

## 3. 이번에 추가한 화면전환 애니메이션

기존 첫 입장 애니메이션은 유지했습니다.

추가된 것은 아래입니다.

```text
첫 화면에서 버튼 클릭
→ 첫 화면이 흐려지며 사라짐
→ "루디스 입장 중" 전환 화면 표시
→ /ludis/로 이동
→ "루디스 준비 완료" 짧게 표시
→ 메인 화면이 부드럽게 등장
```

적용되는 버튼:

```text
무료로 시작하기
VIP 인증 성공 후 입장
사용 이전 성공 후 입장
```

---

## 4. 적용 순서

### 1번. 기존 파일 백업

GitHub 저장소에서 기존 파일을 백업합니다.

```text
index.html
ludis/index.html
```

이전에 올린 `ludis.html` 또는 `app.html`이 있다면 이제 사용하지 않아도 됩니다.

---

### 2번. ZIP 압축 풀기

다운로드한 ZIP을 압축 해제합니다.

---

### 3번. GitHub 저장소 루트에 업로드

아래 파일과 폴더를 업로드합니다.

```text
1. index.html
2. ludis 폴더 전체
```

ZIP 파일 자체를 올리면 안 됩니다.

---

### 4번. GitHub Pages 반영 기다리기

업로드 후 보통 1~3분 기다립니다.

---

### 5번. 강력 새로고침

브라우저에서 아래를 실행하세요.

```text
Ctrl + F5
```

앱에서 확인한다면 앱을 완전히 종료 후 다시 실행하세요.

---

## 5. 확인할 것

첫 화면:

```text
https://dovitrip.kro.kr/ 접속 시 첫 화면이 뜨는지
기존 첫 화면 애니메이션이 유지되는지
무료로 시작하기 클릭 시 전환 화면이 보이는지
VIP 인증 성공 후 전환 화면이 보이는지
사용 이전 성공 후 전환 화면이 보이는지
주소가 /ludis/로 이동하는지
주소창에 .html이 안 보이는지
```

메인 화면:

```text
/ludis/에서 "루디스 준비 완료"가 짧게 보이는지
메인 화면이 부드럽게 등장하는지
기존 기록이 그대로 보이는지
승리 저장 / 패배 저장이 정상인지
그래프가 정상인지
거래주의 조회가 VIP 전용인지
자동저장이 VIP 전용인지
```

---

## 6. 보안 기준

이번 작업은 화면전환만 추가합니다.

VIP 여부는 URL이 아니라 기존 기준을 그대로 사용합니다.

```text
dobi_access_id_v1
ludis_access_tier_v1
dobi_access_expires_at_v1
device_id
Supabase 서버 검증
```

직접 `/ludis/`로 들어가도 무료 시작값이나 VIP 인증값이 없으면 첫 화면으로 돌아갑니다.

---

## 7. 적용 여부 확인

첫 화면 소스에서 검색:

```text
LUDIS_FOLDER_ENTRY_V6
```

메인 화면 소스에서 검색:

```text
LUDIS_FOLDER_MAIN_V6
```

---

## 8. 기존 데이터 보존 여부

이번 작업은 화면 애니메이션과 파일 이동 방식만 수정합니다.

변경하지 않는 것:

```text
Supabase 테이블
Supabase 함수
VIP 코드
무료 이벤트 코드
블랙리스트
관리자 데이터
판매등록 데이터
정산 데이터
유저 게임 기록
localStorage 저장 키
Discord 봇
Windows 앱
앱 다운로드 직접 exe 링크
```

---

## 9. Supabase 영향

```text
Supabase SQL 필요: 없음
Supabase DB 용량 증가: 없음
새 테이블 생성: 없음
새 함수 생성: 없음
RLS 변경: 없음
```

끝.
