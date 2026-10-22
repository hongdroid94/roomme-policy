# 룸메 — 정책 문서

앱스토어·플레이스토어 등록에 필요한 개인정보처리방침, 이용약관, 계정 삭제 안내를
GitHub Pages로 서비스한다. 주소는 `https://hongdroid94.github.io/roomme-policy/`.

**이 리포지터리는 공개다.** 앱 소스는 비공개다.
무료 플랜에서는 비공개 리포지터리로 Pages를 서비스할 수 없어 분리했다.

| 파일 | 내용 |
|---|---|
| `index.html` | 랜딩 |
| `privacy.html` | 개인정보처리방침 |
| `terms.html` | 이용약관 |
| `delete-account.html` | 계정 및 데이터 삭제 (Google Play 의 계정 삭제 URL) |
| `style.css` | 공통 스타일 (외부 폰트·CDN 없음) |

## 앱에서 가리키는 곳

`app/lib/features/profile/settings_screen.dart` 가 `privacy.html` 과 `terms.html` 을
`https://hongdroid94.github.io/roomme-policy/$page.html` 로 연다.
파일 이름을 바꾸면 앱도 같이 고쳐야 한다.

Play Console 의 "계정 삭제" URL 에는 `delete-account.html` 을 넣는다.

## 고칠 때

내용을 바꾸면 **시행일과 최종 수정일을 함께 고친다.** 개인정보처리방침은
"무엇을 수집하는지"가 사실과 달라지는 순간 문서가 아니라 문제가 된다.

지금 문서는 아래를 사실로 적고 있다. 하나라도 바뀌면 여기부터 갱신할 것.

- 광고 SDK·분석 SDK 없음 (Firebase 는 `firebase_messaging` 만)
- 요청하는 기기 권한은 알림 하나. 위치·연락처·사진·카메라 없음
- 앱 안에서 돈이 오가지 않음 (가계부는 기록·계산만)
- 로그인: 익명(둘러보기)·카카오·Apple·이메일 6자리 코드. 비밀번호 없음
- 카카오 scope 는 `profile_nickname`(필수)·`profile_image`·`account_email`(선택) — GoTrue 가 고정
- 데이터 저장은 Supabase, AWS 서울 리전(ap-northeast-2)
- 푸시는 FCM(→ iOS 는 APNs). 알림 문구에 보낸 사람 이름·규칙 제목·금액이 들어감
- `push_queue` 는 발송 7일 뒤 삭제 (`0008_push_cron.sql`)
- 로그인 코드 메일은 Brevo
- 탈퇴 시 즉시 삭제, 유예 기간 없음. 단 상대가 남으면 합의된 규칙·지출·끝난 정산은
  작성자만 비운 채('떠난 룸메') 남음 (`0015_account_deletion.sql`)
- Apple refresh token 은 탈퇴 시 철회용으로만 저장 (`apple_tokens`, 앱은 못 읽음)
