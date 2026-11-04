작성: Claude Code / 확인: (이우진)

# week09/tools.py 함수 정리

## 개요

- 영화진흥위원회(KOBIS) 오픈 API로 일별 박스오피스 정보를 조회하는 모듈임
- 사용 라이브러리: `requests`
- API 키: `secret.py`의 `API_KEY`를 import해서 사용함
- 호출 주소(`BASE_URL`): `https://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json`
- '파일 안의 함수는 get_boxoffice_rank_1 하나뿐임'

## 함수: `get_boxoffice_rank_1(date)`

- 역할: '지정한 날짜의 일별 박스오피스 1위 영화 제목을 반환함'

| 항목 | 내용 |
|------|------|
| 매개변수 | `date` (str): 조회 날짜, `YYYYMMDD` 형식 (예: `"20261027"`) |
| 반환값 | str: 1위 영화 이름 (`movieNm`) |

### 동작 순서

1. `key`(API 키)와 `targetDt`(날짜)로 요청 파라미터를 만듦
2. `requests.get()`으로 API를 호출함 (timeout 10초)
3. 응답 JSON에서 `boxOfficeResult` → `dailyBoxOfficeList`를 꺼냄
4. 리스트 첫 번째 항목(`movies[0]`)의 `movieNm`을 반환함

### 한계 및 주의점

- '날짜는 반드시 YYYYMMDD 형식 문자열로 넘겨야 함'
- HTTP 오류·네트워크 오류를 따로 처리하지 않음
- 날짜가 잘못됐거나 결과가 비어 있으면 `KeyError` / `IndexError` 발생 가능함
- 1위 영화 제목만 반환하고 관객 수 등 다른 정보는 쓰지 않음
- '`secret.py`에 유효한 API_KEY가 있어야 동작함'
