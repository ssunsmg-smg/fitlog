# 운동 데이터 (Exercise Data)

FitLog의 AI 운동 가이드는 두 가지 이미지 소스를 사용합니다:

## 1. 로컬 이미지 (1순위)
- 위치: `../img/`
- 용도: 사용자가 직접 추가한 기구 사진 (가장 빠른 로딩)
- 매핑: `index.html` 내 `EX_IMG` 객체

## 2. yuhonas/free-exercise-db (2순위, 폴백)
- 출처: https://github.com/yuhonas/free-exercise-db
- 라이선스: The Unlicense (퍼블릭 도메인)
- 호스팅: GitHub raw CDN — 별도 다운로드 불필요
- URL 패턴: `https://raw.githubusercontent.com/yuhonas/free-exercise-db/main/exercises/{ID}/0.jpg`
- 매핑: `index.html` 내 `EX_DB` 객체

## 3. (선택) 전체 데이터셋 다운로드

운동 검색/필터링 같은 고급 기능을 추가하고 싶다면 전체 JSON을 받아 이 폴더에 넣으세요:

```bash
curl -L -o exercises.json https://raw.githubusercontent.com/yuhonas/free-exercise-db/main/dist/exercises.json
```

파일 크기는 약 700KB이며 800+ 운동 데이터가 포함됩니다. 각 운동은 다음 필드를 가집니다:
- `id`: 운동 고유 ID (이미지 폴더명과 동일)
- `name`: 영어 이름
- `force`: pull/push/static
- `level`: beginner/intermediate/expert
- `mechanic`: compound/isolation
- `equipment`: 사용 기구
- `primaryMuscles`, `secondaryMuscles`: 자극 근육
- `instructions`: 동작 설명 (영어)
- `category`: strength/cardio/stretching/등
- `images`: 이미지 경로 배열

## 매핑 확장 방법

새로운 운동을 추가하려면:

1. https://github.com/yuhonas/free-exercise-db/tree/main/exercises 에서 운동 폴더명(ID) 확인
2. `index.html` 의 `EX_DB` 객체에 `'한글명':'Folder_ID'` 추가

예시:
```javascript
'바벨 슈러그':'Barbell_Shrug',
'덤벨 컬':'Dumbbell_Bicep_Curl',
```

이미지가 404로 떠도 JS는 자동으로 숨김 처리합니다.
