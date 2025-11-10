# 한국 문학 비평 TEI XML 변환 프로젝트

김우창의 「궁핍한 시대의 시인」을 TEI (Text Encoding Initiative) XML 형식으로 변환하고, 한국민족문화대백과 및 Wikipedia API를 활용하여 인물/작품/기관 정보를 자동으로 태깅하는 프로젝트입니다.

## 주요 기능

### 1. TEI XML 변환
- 한국 문학 비평 텍스트를 TEI P5 표준에 맞게 XML로 변환
- 인물명(`<persName>`), 작품명(`<title>`), 기관명(`<orgName>`), 전문용어(`<term>`) 자동 태깅
- 중첩 태그 처리 및 XML 유효성 검증

### 2. API 통합
- **한국민족문화대백과 API**: 4,021명의 인물 정보 자동 수집
- **Wikipedia API**: 664개의 Wikipedia 참조 링크 추가
- 자동 캐싱으로 중복 API 호출 방지

### 3. 엔티티 데이터베이스
- 150+ 문학인 (시인, 소설가, 비평가 등)
- 100+ 작품 (시집, 소설, 평론집 등)
- 50+ 기관 및 전문용어
- API로부터 자동 확장된 4,021명의 추가 인물 정보

## 파일 구조

```
├── convert_to_xml.py              # 메인 TEI XML 변환 도구
├── enrich_from_list_api.py        # 한국민족문화대백과 API 데이터 수집
├── add_wikipedia_refs.py          # Wikipedia 참조 링크 추가
├── batch_convert.py               # 배치 변환 도구
├── fix_xml_tags.py                # XML 태그 수정 도구
├── validate_xml.py                # XML 유효성 검증
│
├── korean-critique-schema.xsd     # TEI XML 스키마
│
├── enriched_persons_from_list_api.json        # 한국민족문화대백과 인물 데이터 (4,021명)
├── enriched_persons_with_wikipedia.json       # Wikipedia 링크 포함 데이터
├── wikipedia_cache.json                       # Wikipedia API 캐시
│
└── 테스트/디버깅 도구
    ├── check_api_final.py         # API 엔드포인트 테스트
    ├── check_article_structure.py # API 응답 구조 분석
    ├── test_api_*.py              # 다양한 API 테스트
    └── debug_api*.py              # API 디버깅 도구
```

## 설치 및 실행

### 필요 패키지

```bash
pip install requests lxml
```

### 기본 사용법

#### 1. TEI XML 변환

```bash
python convert_to_xml.py
```

대화형 모드로 실행되며, 변환할 텍스트 파일을 선택하고 출력 XML 파일명을 지정합니다.

#### 2. 한국민족문화대백과 데이터 수집

```bash
# 테스트 모드 (10페이지)
python enrich_from_list_api.py --mode test

# 문학 분야만 수집 (97페이지)
python enrich_from_list_api.py --mode literature

# 전체 데이터 수집 (1,507페이지)
python enrich_from_list_api.py --mode all

# 특정 페이지 수만 수집
python enrich_from_list_api.py --mode all --pages 400
```

#### 3. Wikipedia 참조 링크 추가

```bash
# JSON 파일에 Wikipedia 정보 추가
python add_wikipedia_refs.py --mode json \
  --input-json enriched_persons_from_list_api.json \
  --output-json enriched_persons_with_wikipedia.json

# 기존 XML 파일에 Wikipedia ref 속성 추가
python add_wikipedia_refs.py --mode xml \
  --xml-file output.xml \
  --output-json enriched_persons_with_wikipedia.json

# JSON과 XML 둘 다 처리
python add_wikipedia_refs.py --mode both \
  --xml-file output.xml
```

## 데이터 통계

### 수집된 인물 데이터

| 소스 | 인물 수 | Wikipedia 커버리지 |
|------|---------|-------------------|
| 수동 입력 | 150+ | - |
| 한국민족문화대백과 | 4,021 | - |
| Wikipedia 링크 | 664 | 16.5% |

### 엔티티 태깅 개선

| 항목 | 초기 | 개선 후 |
|------|------|---------|
| 인물명 태그 | 67 | 200+ |
| 작품명 태그 | - | 100+ |
| 기관명 태그 | - | 50+ |

## API 정보

### 한국민족문화대백과 API

- **Base URL**: `https://devin.aks.ac.kr:8080/v1`
- **인증**: X-API-Key 헤더 사용
- **주요 엔드포인트**:
  - `/Articles?pageNo={n}` - 전체 항목 리스트
  - `/Articles/Field/{field}?pageNo={n}` - 특정 분야 항목
  - `/Article/{eid}` - 특정 항목 상세 정보

### Wikipedia API

- **Base URL**: `https://ko.wikipedia.org/w/api.php` (검색)
- **Summary API**: `https://ko.wikipedia.org/api/rest_v1/page/summary/{title}`
- **기능**: 인물명으로 Wikipedia 문서 검색 및 URL 추출

## TEI XML 스키마

본 프로젝트는 TEI P5 표준을 따르며, 다음 요소들을 사용합니다:

- `<TEI>`: 루트 요소
- `<teiHeader>`: 메타데이터
  - `<fileDesc>`: 파일 정보
  - `<profileDesc>`: 텍스트 프로파일
- `<text>`: 본문
  - `<body>`: 텍스트 내용
  - `<div type="chapter">`: 장/절 구분
  - `<p>`: 문단
  - `<persName>`: 인물명 (ref 속성으로 Wikipedia 링크)
  - `<title>`: 작품명
  - `<orgName>`: 기관명
  - `<term>`: 전문용어

## 작업 내역

### 2024-11-10

1. **초기 TEI XML 변환기 구현**
   - 기본 인물/작품 데이터베이스 구축 (150+ 엔티티)
   - 자동 태깅 기능 구현
   - 중첩 태그 처리

2. **한국민족문화대백과 API 통합**
   - List API를 통한 대량 데이터 수집
   - 4,021명 인물 정보 자동 수집
   - 역할 자동 매핑 (시인, 소설가, 비평가 등)
   - convert_to_xml.py 자동 업데이트

3. **Wikipedia API 통합**
   - Wikipedia 검색 및 Summary API 연동
   - 664개 Wikipedia 참조 링크 수집 (16.5% 커버리지)
   - 캐싱 시스템 구현
   - XML ref 속성 자동 추가

4. **Git 저장소 설정**
   - 초기 커밋 완료
   - .gitignore 설정 (소스 문서, IDE 설정 제외)

## 개선 방향

### 단기 (향후 작업)

- [ ] Wikipedia 검색 정확도 개선 (시대 정보 활용)
- [ ] 네트워크 오류 재시도 로직 추가
- [ ] 작품명, 기관명 API 데이터 수집
- [ ] XML 배치 변환 자동화

### 중장기

- [ ] 전체 「궁핍한 시대의 시인」 시리즈 변환
- [ ] 다른 문학 비평 텍스트 확장
- [ ] 웹 인터페이스 개발
- [ ] TEI XML 뷰어 구현

## 기술 스택

- **Python 3.x**
- **lxml**: XML 파싱 및 생성
- **requests**: HTTP API 호출
- **TEI P5**: XML 표준
- **Git**: 버전 관리

## 라이선스

이 프로젝트는 학술 연구 목적으로 개발되었습니다.

## 문의

프로젝트 관련 문의사항은 이슈를 통해 남겨주세요.

---

**Last Updated**: 2024-11-10
**Generated with**: Claude Code
