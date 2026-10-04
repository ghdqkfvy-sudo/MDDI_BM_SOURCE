# Panel Pattern Studio

iPhone 디스플레이 테스트용 패턴 영상을 **브라우저 안에서** 생성하는 정적 웹앱입니다.
서버가 필요 없으며, 생성된 MP4는 공유 시트(AirDrop)로 테스트 기기에 바로 전달할 수 있습니다.

## 기능
- 패턴: 단색(R/G/B 0–255) · 체커보드(N×N / px) · 그라데이션(Gray/R/G/B, 2–256 step) · 컬러바 · 플리커(프레임 교번) · 무빙 바
- 고정 프레임레이트 MP4 생성 (1–240Hz, WebCodecs + mp4-muxer, H.264 / HEVC)
- 기기 프리셋: iPhone 18 Pro (1206×2622), 18 Pro Max (1320×2868), Air, 17, 사용자 지정
- 검증 오버레이: 프레임 토글 마커, 8-bit 프레임 카운터, 정보 라벨
- 패턴 PNG 저장, 전체화면 미리보기, 공유/AirDrop
- PWA(오프라인 캐시) — 한 번 접속하면 네트워크 없이도 동작

## GitHub Pages 배포
1. 새 저장소 생성 (예: `panel-pattern-studio`)
2. 이 폴더의 파일을 루트에 업로드 후 커밋
3. Settings → Pages → Branch: `main` / `/ (root)` → Save
4. 1~2분 후 `https://<계정>.github.io/panel-pattern-studio/` 접속

> WebCodecs는 HTTPS(보안 컨텍스트)에서만 동작합니다. 로컬 테스트는 `python -m http.server` 후 `http://localhost:8000` 으로 접속하세요 (`file://` 불가).

## 권장 환경
- 전송용 iPhone: iOS 16.4 이상 Safari (WebCodecs H.264 하드웨어 인코딩)
- 데스크톱: 최신 Chrome / Edge / Safari
- WebCodecs 미지원 브라우저는 실시간 녹화(MediaRecorder) 방식으로 대체되며 프레임 타이밍 정확도가 낮습니다.

## 주의
- 영상은 YUV 4:2:0으로 인코딩되므로 재생 시 채널당 ±1~2 레벨 오차가 있을 수 있습니다. 정확한 코드값은 PNG를 사용하세요.
- 수신 기기의 저전력 모드는 주사율을 60Hz로 제한할 수 있습니다. 자동 밝기·True Tone·Night Shift도 끄고 측정하세요.
- 플리커 패턴은 광과민성 발작을 유발할 수 있으니 장시간 직시하지 마세요.

## 파일
| 파일 | 설명 |
|---|---|
| `index.html` | 앱 전체 (UI + 렌더러 + 인코더) |
| `mp4-muxer.js` | MP4 컨테이너 muxer (MIT, Vanilagy/mp4-muxer v5.2.2) |
| `sw.js`, `manifest.webmanifest`, `icon*` | PWA / 홈 화면 아이콘 |
