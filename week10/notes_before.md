# week09/tools.py 함수 정리 (수정 전)

## 개요

`tools.py`는 영화진흥위원회(KOBIS) 오픈 API로 **일별 박스오피스** 정보를 조회하는 모듈입니다.

- 사용 라이브러리: `requests`
- API 키: `secret.py`의 `API_KEY`를 import해서 사용
- 호출 주소(`BASE_URL`): `https://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json`

## 함수 목록

이 파일에는 함수가 **1개** 있습니다.

### `get_boxoffice_rank_1(date)`

지정한 날짜의 일별 박스오피스 **1위 영화 제목**을 반환합니다.

| 항목 | 내용 |
|------|------|
| 매개변수 | `date` (str): 조회 날짜, `YYYYMMDD` 형식 (예: `"20261027"`) |
| 반환값 | str: 1위 영화 이름 (`movieNm`) |

**동작 순서**

1. `key`(API 키)와 `targetDt`(날짜)로 요청 파라미터를 만든다.
2. `requests.get()`으로 API를 호출한다 (timeout 10초).
3. 응답 JSON에서 `boxOfficeResult` → `dailyBoxOfficeList`를 꺼낸다.
4. 리스트의 첫 번째 항목(`movies[0]`)의 `movieNm`을 반환한다.

**참고 (현재 코드의 한계)**

- HTTP 오류나 네트워크 오류를 따로 처리하지 않는다.
- 날짜 형식이 잘못됐거나 결과가 비어 있으면 `KeyError` / `IndexError`가 날 수 있다.
- 1위 영화의 제목만 반환하고, 관객 수 등 다른 정보는 쓰지 않는다.
