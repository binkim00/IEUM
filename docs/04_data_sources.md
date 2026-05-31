# 04. 데이터 소스 및 통합 설계

## 1. 데이터 설계 원칙

이음은 단일 API에 의존하지 않고, 여러 공식·공공 데이터를 유산 ID 중심으로 연결하는 통합 데이터 구조를 지향합니다.

핵심은 “모든 데이터를 하나의 테이블에 넣는 것”이 아니라, 국가유산을 기준으로 기본 정보, 설명 문서, 이미지, 좌표, 카테고리, 추천 관계를 연결하는 것입니다.

```txt
외부 공공 데이터
→ 수집·정제
→ 유산 ID 기준 통합
→ RAG 문서 Chunk 생성
→ Metadata / Vector DB 저장
→ AI 해설 및 추천에 활용
```

## 2. 주요 데이터 소스

| 데이터 소스 | 주요 데이터 | 활용 역할 | MVP 활용 |
| --- | --- | --- | --- |
| 국가유산검색 API | 명칭, 주소, 좌표, 설명, 대표 이미지 | 기본 DB 기준 데이터 | 핵심 |
| 궁궐·종묘 Open API | 궁궐·종묘 해설, 이미지 | 현장 데모 핵심 해설 | 핵심 |
| 국가유산 지식이음 | 보존과학, 전통재료, 연구 자료 | RAG 심화 문서 | 보조 |
| TourAPI | 역사관광지, 주변 장소, 관광 이미지 | 탐방 흐름 및 주변 추천 | 보조 |
| 이뮤지엄 API | 박물관 소장품, 이미지, 설명 | 관련 유물·이미지 연결 | 보조 |
| 향토문화전자대전 | 지역 설화, 인물, 사건, 생활문화 | 지역 스토리 확장 | 확장 |
| 문화재 공간정보 API | 문화재 경계, 도형 좌표 | 지도 polygon, 경계 판별 | 확장 |

## 3. 통합 데이터 구조

### heritage_master

국가유산 기준 기본 정보 테이블입니다.

| 필드 | 설명 |
| --- | --- |
| heritage_id | 내부 기준 유산 ID |
| source_item_id | 원본 데이터의 식별자 |
| name_ko | 한국어 명칭 |
| name_en | 영문 명칭 |
| category | 지정종목 또는 분류 |
| region | 지역 |
| address | 주소 |
| latitude | 대표 위도 |
| longitude | 대표 경도 |
| description | 기본 설명 |
| representative_image_url | 대표 이미지 |
| source | 원본 출처 |
| source_url | 원문 링크 |

### heritage_documents

RAG 검색에 사용되는 설명 문서 테이블입니다.

| 필드 | 설명 |
| --- | --- |
| document_id | 문서 ID |
| heritage_id | 연결 유산 ID |
| source | 데이터 출처 |
| dataset | 데이터셋명 |
| title | 문서 제목 |
| clean_text | 정제된 본문 |
| language | 언어 |
| categories | 카테고리 태그 |
| keywords | 키워드 |
| source_url | 원문 링크 |

### recommendation_edges

추천 관계를 관리합니다.

| 필드 | 설명 |
| --- | --- |
| from_heritage_id | 현재 유산 ID |
| to_heritage_id | 추천 유산 ID |
| relation_type | 같은 시대, 같은 지역, 건축 양식, 인물, 키워드 등 |
| category | 추천 카테고리 |
| reason | 추천 이유 |
| weight | 추천 가중치 |

## 4. RAG 문서 생성 방식

```txt
원본 수집
→ HTML / XML / JSON / CSV 정제
→ 본문 추출
→ 불필요한 태그 제거
→ 문단 단위 정리
→ Chunk 분할
→ Metadata 부여
→ Embedding 생성
→ Vector DB 저장
```

## 5. 공개용 데이터 원칙

Public 레포에는 전체 원본 데이터를 올리지 않습니다.

공개 가능:

- 데이터 구조 예시
- 샘플 JSON 3~5건
- 출처와 활용 목적 설명
- 수집·정제 방식 문서

공개 제외:

- API Key가 포함된 URL
- 대용량 원본 JSON
- 원문 전체 덤프
- 접근 키가 포함된 이미지 URL
- 개인·팀 내부 로그
- 저작권 확인이 필요한 원문 대량 데이터
