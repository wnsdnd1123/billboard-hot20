# Billboard Hot 20 자동 갱신

대상: YouTube Music 플레이리스트 **bill**.

- 매주 화요일·수요일 **18:23 UTC**에 최신 미국 Billboard Hot 100 상위 20곡으로 자동 갱신합니다. 한국시간으로는 수요일·목요일 오전 3:23입니다.
- 공식 카탈로그의 앨범 음원을 우선하며 참여 아티스트를 확인합니다.
- 새 곡을 추가한 뒤 목록을 확인하고, 제외된 곡과 중복을 삭제한 뒤 순위를 맞춥니다.
- 플레이리스트 조회·추가·삭제·정렬은 Google 공식 YouTube Data API를 사용합니다. 음원 검색은 로그인 없이 YouTube Music 카탈로그에서 수행합니다.

## 수동 실행

[Actions → Billboard Hot 20](https://github.com/wnsdnd1123/billboard-hot20/actions/workflows/sync.yml) → Run workflow.

- **Apply playlist changes 미체크:** 미리보기, 곡 변경 없음.
- **Apply playlist changes 체크:** 즉시 실제 갱신.
- 워크플로 파일 수정 시에는 자동으로 미리보기를 실행합니다.

## 인증

Actions Secrets에 `YTMUSIC_CLIENT_ID`, `YTMUSIC_CLIENT_SECRET`, `YTMUSIC_OAUTH_JSON`을 등록합니다. 인증 정보는 코드·공개 이슈·채팅에 올리지 않습니다.
Google 앱은 장기 인증을 위해 Production 상태로 설정합니다. Google에서 앱 접근을 철회하면 다시 인증해야 합니다.
설정에 사용한 Colab 노트북의 토큰 출력은 지우고 런타임을 삭제하세요.

## 실행 기록과 복구

성공/실패는 Actions 실행 기록에서 확인합니다. 알림은 본인 GitHub Actions 알림 설정을 따릅니다.
각 실행의 아티팩트에 선택 음원 `plan.json`, 변경 전 `before.json`, 성공 시 변경 후 `after.json`을 14일간 보관합니다.
편집은 일괄 트랜잭션이 아니므로 실패 시 일부 변경이 남을 수 있습니다. 원인을 해결한 뒤 재실행하면 목표 목록에 맞춥니다.
20곡 전체를 확실하게 찾지 못하거나 소유권·차트 날짜 확인에 실패하면 편집 전에 중단합니다.
YouTube Music 화면에서 다른 정렬 방식을 선택했다면 **직접 정렬**로 보아야 저장된 차트 순서가 표시됩니다.

[앱 소개](https://wnsdnd1123.github.io/billboard-hot20/) · [개인정보처리방침](https://wnsdnd1123.github.io/billboard-hot20/privacy.html) · [이용약관](https://wnsdnd1123.github.io/billboard-hot20/terms.html)
