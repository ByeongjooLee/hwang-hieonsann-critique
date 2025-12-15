# The Topology of Power: 한국 문학비평의 정전 형성과 지적 카르텔에 대한 데이터 기반 분석 (1960–1990)

## 프로젝트 개요

문학적 "거장"은 개인의 천재성으로 탄생하는가, 아니면 장(field)의 구조적 필연성에 의해 구성되는가?

이 프로젝트는 1960년대부터 1990년대까지 한국 문학비평계를 지배한 세 명의 비평가—**김현**(1942–1990), **김우창**(b.1937), **유종호**(b.1935)—의 권위가 형성된 메커니즘을 **디지털 인문학 방법론**으로 분석합니다. 우리는 "거장"이 개인의 재능이 아니라, **초국적 지식 이전**과 **제도적 카르텔**의 교차점에서 구성되었다고 주장하며, 문학 잡지가 정전을 입법하는 핵심 엔진으로 작동했음을 실증합니다.

본 연구는 **DH2026 (Digital Humanities 2026) 국제학술대회** 제출 논문을 기반으로 합니다.

### 핵심 연구 질문
- 한국 문학비평의 "거장"은 어떤 구조적 조건 위에서 탄생했는가?
- 문학 잡지는 어떻게 정전 형성의 제도적 권력으로 작동했는가?
- 서구 이론의 중개자로서 비평가들은 어떤 네트워크 위상을 점유했는가?

## 연구 배경

### 역사적 맥락
1960년 4.19 혁명은 이념적 공백을 창출했고, 이는 **서구 이론에 대한 언어적 접근권**과 **제도적 권력**을 동시에 보유한 새로운 유형의 비평가에 의해서만 채워질 수 있었습니다. 1960년대부터 1980년대까지, 한국의 문학 정전 형성은 지적 헤게모니를 위한 치열한 투쟁이었으며, 그 주된 전장은 **문학 잡지**였습니다.

### 세 비평가의 역할

**김현 (Kim Hyun)**
- **전략**: 세계문학의 주관적 전유를 통해 한국 문학의 주변성 극복
- **핵심 개념**: "자율성"(내적 상상력)과 "타율성"(사회적 역할)의 종합
- **제도적 기반**: 『문학과지성』 편집, 서울대학교 교수
- **특징**: 프랑스 이론(바슐라르 현상학)을 한글세대 시 비평에 적용

**김우창 (Kim Woo-chang)**
- **전략**: 문학비평을 문명 진단으로 승격
- **핵심 개념**: "구체적 총체성" (Concrete Totality)
- **제도적 기반**: 『세계의문학』 편집, 고려대학교 교수
- **특징**: 한국 문학 연구를 철학적 인간학으로 확장

**유종호 (Yu Jong-ho)**
- **전략**: 서구 중심과 한국 주변의 위계 해체
- **핵심 개념**: 한국 문학의 "로컬리티" 이론화
- **제도적 기반**: 『세계의문학』 편집, 이화여자대학교 교수
- **특징**: 정전의 독립적 경험적 기준 수립

이들의 권위는 절대적이었습니다. **긍정적 평가는 정전 지위를 보장**했고, **침묵은 무명을 의미**했습니다.

## 연구 방법론

본 연구는 다층적 방법론 파이프라인을 구축하여 "비평적 권력"을 조작화합니다.

### 1. 인용 및 사회 네트워크 구축
- **Named Entity Recognition (NER)**: 비평 전집에서 엔티티 추출
- **지적 계보 네트워크**: 서구 이론가(Source) → 한국 작가(Target) 방향성 참조 매핑
  - 예: 바슐라르 → 김현 → 한국 시
- **제도적 사회 네트워크**: 문학 잡지 메타데이터 + 주요 문학상 심사위원 명단 활용
  - "강한 연결"(strong ties) 식별: 편집자-비평가 ↔ 발굴된 작가

### 2. 게이트키핑 측정: 중심성 지표
- **매개 중심성 (Betweenness Centrality)** 계산
- **가설**: 세 비평가는 최고 중심성 점수를 보유 → "게이트키퍼" 지위
  - Source(서구 이론) ↔ Target(한국 정전) 사이의 **최단 경로 독점**

### 3. 담론 헤게모니: Word Embeddings
- **통시적 Word2Vec 모델**: 시기별 코퍼스(1960년대, 1970년대, 1980년대) 학습
- **의미 변화 추적**: "감수성", "정밀성" 등 핵심 비평 용어의 nearest neighbors 분석
- **입법 효과 측정**: 비평가들의 독자적 정의가 표준 어휘로 자리잡는 과정 시각화

### 4. 텍스트 인코딩 및 엔티티 링킹
- **TEI XML**: 459페이지 분량의 김우창 비평문 디지털화
- **Wikidata/Wikipedia 연계**: 4,000+ 인물 데이터베이스 구축
- **한국민족문화대백과사전 API** 활용

## 데이터셋

### 네트워크 분석 데이터
| 파일명 | 설명 | 규모 |
|--------|------|------|
| `network_nodes.csv` | 철학자, 비평가, 한국 작가 노드 | 63+ 노드 |
| `network_edges_with_quotes_v2.csv` | 직접 인용문이 포함된 인용 관계 | 130+ 엣지 |

**네트워크 특징**:
- 노드 유형: critic, philosopher, author, essay
- 엣지 속성: source, target, relation, essay, quote (직접 인용문)
- 예시 데이터:
  ```
  Source: "궁핍한시대의시인"
  Target: "골드만"
  Quote: "골드만은 세계관을 하나의 일관된 전망으로 정의한다..."
  ```

### 인물 데이터베이스
| 파일명 | 설명 | 규모 |
|--------|------|------|
| `enriched_persons_with_wikidata.json` | Wikidata QID 연계 인물 정보 | 4,000+ 인물 |
| `enriched_persons_with_wikipedia.json` | Wikipedia 참조 추가 | 664건 (16.5% 커버리지) |
| `enriched_persons_from_list_api.json` | 한국민족문화대백과 API 데이터 | 4,021 인물 |

**데이터 필드**:
- 기본 정보: role, era, definition, eid (백과사전 ID)
- 외부 링크: Wikipedia URL, Wikidata QID
- 구조화 데이터: 생몰년, 직업, 국적 (Wikidata 속성)

### 텍스트 데이터
- **김우창 비평문**: 9개 TEI XML 파일 (459페이지)
  - 『궁핍한시대의시인』 전문
  - 개별 에세이 25편 분석 마크다운 파일
- **백철 신문학사조사**: 4개 HTML/XML 버전

## 주요 연구 결과

### 권위의 삼중 조건 구조
분석 결과, 세 비평가는 다음 조건을 공유했습니다:
1. **서구 언어에 대한 접근권** (Access)
2. **이론의 주관적 전유** (Appropriation)
3. **잡지를 통한 제도화** (Institution)

### 두 가지 권력 모델

#### 1. 유종호 & 김우창: 입법적 권력 (Legislative Power)
- **네트워크 위상**: 『세계의문학』 중심의 "전략적 중간 지대"
- **게이트키핑 증거**: "오늘의 작가상" 인용 데이터
  - 이문열의 정전화: 유종호의 지지 이후 중심성 급상승
- **제도적 재생산**: 대학원생 → 『세계의문학』 기고자 경로
  - 이화여대/고려대 교수직 활용

#### 2. 김현: 감성의 혁명가 (Revolutionary of Sensibility)
- **네트워크 위상**: 프랑스 이론과의 고밀도 브리지
- **담론 전유**: 바슐라르 현상학 → 1970년대 "한글세대" 시 분석 언어로 변환
- **제도적 재생산**: 서울대 강의실 = 『문학과지성』 편집실
  - "문지파" 구축: 제자 비평가들이 이론적 어휘 세대 간 전승

### 시계열 분석
- **중심성 점수 피크**: 잡지 창간 시점과 상관관계
  - 김현: 1970년 (『문학과지성』)
  - 유종호/김우창: 1976년 (『세계의문학』 편집 참여)
- **가설 지지**: "거장"은 순수한 텍스트적 탁월성이 아니라 **제도적 포지셔닝의 산물**

## 프로젝트 구조

```
The Topology of Power/
├── data/
│   ├── network_nodes.csv              # 네트워크 노드 데이터
│   ├── network_edges_with_quotes_v2.csv  # 인용 관계 (직접 인용문 포함)
│   ├── enriched_persons_with_wikidata.json  # 인물 데이터베이스
│   └── [김우창/백철 원문 TEI XML 파일들]
│
├── scripts/
│   ├── convert_to_xml.py              # 텍스트 → TEI XML 변환
│   ├── enrich_from_list_api.py        # 한국민족문화대백과 API 연동
│   ├── add_wikipedia_refs.py          # Wikipedia 데이터 보강
│   ├── add_wikidata_refs.py           # Wikidata 링킹
│   └── validate_xml.py                # TEI XML 스키마 검증
│
├── docs/
│   ├── README.md                      # 본 문서 (한글)
│   ├── README_EN.md                   # 영문 문서
│   ├── WIKIDATA_GUIDE.md              # Wikidata 통합 가이드
│   └── gephi_layout_settings.md       # Gephi 시각화 설정
│
└── korean-critique-schema.xsd         # TEI XML 스키마 정의
```

## 사용 방법

### 환경 설정

```bash
# 저장소 클론
git clone https://github.com/ByeongjooLee/The-Topology-of-Power.git
cd The-Topology-of-Power

# Python 의존성 설치
pip install -r requirements.txt

# 필요 라이브러리 (예시)
# - pandas, networkx (네트워크 분석)
# - lxml (XML 처리)
# - requests (API 호출)
# - gensim (Word2Vec)
```

### 네트워크 시각화 (Gephi)

1. **Gephi 0.10.x** 설치
2. 데이터 불러오기:
   - `network_nodes.csv` → Nodes table
   - `network_edges_with_quotes_v2.csv` → Edges table
3. 레이아웃 적용:
   - **ForceAtlas 2** 알고리즘 사용
   - Scaling: 50.0, Gravity: 5.0
   - 상세 설정은 [`gephi_layout_settings.md`](docs/gephi_layout_settings.md) 참조
4. 노드 크기: In-Degree 기준 순위화

### XML 변환 및 검증

```bash
# 텍스트 파일을 TEI XML로 변환
python scripts/convert_to_xml.py

# XML 스키마 검증
python scripts/validate_xml.py
```

### API 기반 인물 정보 수집

```bash
# 한국민족문화대백과 API에서 인물 데이터 수집
python scripts/enrich_from_list_api.py --mode literature --pages 10

# Wikipedia 정보 추가
python scripts/add_wikipedia_refs.py

# Wikidata QID 및 구조화 데이터 추가
python scripts/add_wikidata_refs.py
```

상세한 Wikidata 통합 가이드는 [`WIKIDATA_GUIDE.md`](docs/WIKIDATA_GUIDE.md)를 참조하세요.

## 학술적 기여

### Digital Humanities 담론에 대한 기여
1. **Global South의 정전 형성 메커니즘**: 초국적 중개(Transnational Brokerage)를 통한 로컬 권력 생성
2. **제도적 카르텔 시각화**: 문학 잡지 + 대학이 지속시킨 "지적 카르텔"의 구조적 해부
3. **고립된 천재 신화 해체**: 데이터 기반 증거로 "거장"의 구조적 토폴로지 폭로

### 방법론적 혁신
- **한국어 NER + Wikidata 연계**: 비서구 언어권 인문학 데이터의 국제 표준 연동
- **직접 인용문 네트워크**: 단순 인용 횟수를 넘어선 담론적 전유 분석
- **통시적 Word Embeddings**: 비평 용어의 입법 과정 계량화

## 인용

이 프로젝트를 연구에 활용하실 경우, 다음과 같이 인용해 주세요:

```
Lee, Byeongjoo. (2026). The Topology of Power: A Data-Driven Analysis of Canon
Formation and Intellectual Cartels in Korean Literary Criticism (1960–1990).
Paper presented at Digital Humanities 2026.
GitHub repository: https://github.com/ByeongjooLee/The-Topology-of-Power
```

## 라이선스

이 프로젝트는 학술 연구 목적으로 공개되었습니다. 데이터 및 코드의 재사용 시 출처를 명시해 주시기 바랍니다.

## 연락처

- **연구자**: 이병주 (Byeongjoo Lee)
- **소속**: [소속 기관 기재]
- **이메일**: [이메일 주소 기재]
- **GitHub**: https://github.com/ByeongjooLee/The-Topology-of-Power

---

**DH2026 Conference Submission** | **Digital Humanities** | **Korean Literary Criticism** | **Network Analysis** | **Canon Formation**
