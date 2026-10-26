# 은평구 공간취약성 지도 — 배포용 정적 사이트

이 프로젝트는 서버 애플리케이션이나 빌드 도구 없이 배포할 수 있는 정적 웹사이트입니다.

## 파일 구성

- `index.html`: 화면 구조
- `css/style.css`: 화면 스타일
- `css/leaflet.css`, `js/leaflet.js`: 로컬에 포함한 Leaflet 라이브러리
- `js/app.js`: 지도 표시, 필터, 점수 계산, CSV 내보내기
- `data/data.json`: 공동주택·시설·도로·경로 등 사전 계산 데이터
- `.github/workflows/deploy.yml`: GitHub Pages 자동 배포
- `netlify.toml`: Netlify 정적 배포 설정

## 배포 전 확인

1. `data/data.json`은 약 6.6MB이며 필수 파일입니다. 배포할 때 빠뜨리지 마세요.
2. 카카오 API 키를 브라우저 코드에 추가하지 마세요. 이 버전은 포함된 데이터를 사용하며, 선택적 온라인 배경지도는 OpenStreetMap 타일을 사용합니다.
3. 지도에 포함된 데이터는 브라우저에서 내려받을 수 있습니다. 비공개 정보나 비밀키를 넣지 마세요.
4. 지수는 시설 접근성 기반 탐색적 지표이며 고독사 확률이나 개인별 위험도 예측값이 아닙니다.
5. 외부 배경지도 타일을 켜려면 인터넷 연결이 필요합니다. 기본 지도 자체는 내장된 도로·경계·시설 자료를 사용합니다.

## 로컬 실행

`index.html`을 더블클릭하지 말고, 프로젝트 폴더에서 로컬 HTTP 서버를 실행하세요.

Windows PowerShell 또는 VS Code 터미널:

```powershell
python -m http.server 8000
```

그 다음 `http://localhost:8000`에 접속합니다. 종료는 터미널에서 `Ctrl+C`입니다.

## GitHub Pages 배포

1. ZIP을 풀고, 그 안의 **index.html / css / js / data 폴더가 보이는 위치의 내용 전체**를 GitHub 저장소 최상위(root)에 업로드합니다. `eunpyeong_split_project`라는 폴더 자체를 한 겹 더 올리지 마세요.
2. 기본 브랜치 이름이 `main`인지 확인합니다. 다른 이름이면 `.github/workflows/deploy.yml`의 브랜치를 수정하세요.
3. 저장소의 **Settings → Pages → Build and deployment → Source**에서 **GitHub Actions**를 선택합니다.
4. `main`에 push하거나 **Actions** 탭에서 `Deploy static site to GitHub Pages`를 수동 실행합니다.
5. 배포가 완료되면 Actions의 Deploy 작업에서 사이트 URL을 확인합니다.

## Netlify 대안

이 폴더를 GitHub 저장소에 올린 뒤 Netlify에서 저장소를 연결하고 publish directory를 `.`으로 설정하면 됩니다. `netlify.toml`이 설정을 제공합니다. 빌드 명령은 필요하지 않습니다.

## 검증 범위

이 패키지 생성 과정에서 JSON 파싱, JavaScript 문법, HTML의 로컬 자산 경로 및 핵심 데이터 개수를 정적으로 검사합니다. 배포 환경별 브라우저 실사용 검증은 별도로 수행해야 합니다.
