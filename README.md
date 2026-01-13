# 황현산 지적 지형도 연구 프로젝트

> 디지털 인문학과 전통 국문학 연구의 융합을 통한 문학비평가 황현산(1945-2018)의 지적 계보 분석

---

## 프로젝트 개요

본 연구는 한국 현대 문학비평가 **황현산**의 비평 텍스트를 체계적으로 분석하여 그의 **지적 지형도(Intellectual Topography)**를 구축하는 것을 목표로 한다. 이를 위해 디지털 인문학(Digital Humanities) 방법론과 전통적 국문학 연구 방법론을 융합하여 접근한다.

### 연구 목표

1. 황현산 비평 텍스트의 **XML 데이터 변환** 및 구조화
2. 인용 철학자/사상가의 **영향 관계 네트워크** 구축
3. 해석 대상 작품과 **해석 방향성**의 체계적 분류
4. 황현산 비평의 **핵심 개념어 온톨로지** 설계
5. 학술논문으로의 발전

---

## 연구 대상 텍스트

### 비평집
| 서명 | 출판연도 | 비고 |
|------|----------|------|
| 『말과 시간의 깊이』 | 2002 | 1차 비평집 |
| 『우물에서 하늘 보기』 | 2009 | 시화집/산문집 |
| 『황현산의 현대시 산고』 | 2013 | 현대시 비평 |
| 『잘 표현된 불행』 | 2019 | 유고 비평집 |

### 주요 번역서
- 말라르메, 『시집』 (2005)
- 아폴리네르, 『알코올』 (2010)
- 브르통, 『초현실주의 선언』 (2012)
- 보들레르, 『악의 꽃』 (2016)
- 벤야민, 『보들레르의 작품에 나타난 제2제정기의 파리』 (공역)

---

## 연구 방법론

### Phase 1: 데이터 구축 (XML/TEI 마크업)

황현산의 비평 텍스트를 TEI P5 기반 커스텀 스키마에 따라 **문장(`<s>`) 단위**까지 구조화한다.

#### 마크업 계층 구조

```
TEI
├── teiHeader (메타데이터)
│   ├── fileDesc (서지정보: 제목, 저자, 출처)
│   └── encodingDesc (인코딩 방침, 분류체계 taxonomy)
└── text
    ├── front (서문, 목차)
    ├── body (본문)
    │   └── div (장/절 구분)
    │       └── p (단락)
    │           └── s (문장) ← 최소 분석 단위
    └── back (미주, 참고문헌)
```

#### 인코딩 예시

```xml
<!-- 문장 단위 마크업 예시: 「이육사의 안 좋은 시들」 -->
<div type="criticism" xml:id="div-yooksa">
  <head>이육사의 안 좋은 시들</head>
  <p>
    <s>
      <persName ref="#yooksa" role="poet">이육사</persName>를 
      <term type="concept">지사 시인</term>이라는 단일한 이미지로 고정하는 
      기존의 관습적 독해를 비판적으로 바라본다.
    </s>
    <s>
      그는 평가절하되었던 
      <persName ref="#yooksa" role="poet">이육사</persName>의 시편들을 재조명한다.
    </s>
  </p>
</div>

<!-- 인용문 마크업 예시 -->
<s>
  <quote type="direct" source="현대시산고-p19" genre="poet">
    "수만호 빛이라야 할 내 고향이언만"
  </quote>을 제시하며 기존 평자들이 
  <term type="lexical">수만호</term>를 '수만 가구(戶)'의 불빛이라는 
  사회적 이미지로 관습적으로 독해해 온 것을 비판한다.
</s>

<!-- 해석/평가 마크업 예시 -->
<s>
  <interp ana="interpretation" value="critical">
    이것이 <term type="lexical">수마노(水瑪瑙)</term>, 
    즉 아름다운 보석의 이름임을 명확히 한다.
  </interp>
</s>

<!-- 작품 제목 마크업 예시 -->
<s>
  황현산은 시인이 
  <title level="a" type="poem">아편(鴉片)</title>에서 
  <quote type="direct" genre="poet">"옥돌보다 찬 넋"</quote>으로 표상되는 
  고결한 지사의 정신을 견지하면서도, 동시에 
  <quote type="direct" genre="poet">"번제(燔祭)의 두렛불 타오르"</quote>는 
  세속의 나른하고 욕망 가득한 열정에 무관심하지 않았다고 분석한다.
</s>
```

#### 인코딩 대상 요소

| 요소 | 태그 | 속성 | 용도 |
|------|------|------|------|
| **인물** | `<persName>` | `ref`, `role` | 시인, 비평가, 철학자 식별 |
| **작품** | `<title>` | `level`, `type` | 시, 소설, 비평문 제목 |
| **인용** | `<quote>` | `type`, `source`, `genre` | 직접/간접/의역 인용 |
| **개념어** | `<term>` | `type` | 핵심 개념, 어휘, 사조 |
| **해석** | `<interp>` | `ana`, `value` | 긍정/중립/비판적 평가 |
| **기관** | `<orgName>` | `ref` | 출판사, 학회, 동인 |
| **주석** | `<note>` | `type`, `target` | 편집자 주, 각주 |

#### 분류체계(Taxonomy) 설계

```xml
<classDecl>
  <!-- 인물 역할 분류 -->
  <taxonomy xml:id="tax-role">
    <category xml:id="role-critic"><catDesc>비평가</catDesc></category>
    <category xml:id="role-poet"><catDesc>시인</catDesc></category>
    <category xml:id="role-philosopher"><catDesc>철학자/사상가</catDesc></category>
    <category xml:id="role-translator"><catDesc>번역가</catDesc></category>
  </taxonomy>
  
  <!-- 인용 유형 분류 -->
  <taxonomy xml:id="tax-quote">
    <category xml:id="qt-direct"><catDesc>직접 인용</catDesc></category>
    <category xml:id="qt-indirect"><catDesc>간접 인용</catDesc></category>
    <category xml:id="qt-paraphrase"><catDesc>의역/요약</catDesc></category>
  </taxonomy>
  
  <!-- 핵심 개념어 분류 -->
  <taxonomy xml:id="tax-concept">
    <category xml:id="con-strangeness"><catDesc>낯섦(Defamiliarization)</catDesc></category>
    <category xml:id="con-otherness"><catDesc>타자성(Otherness)</catDesc></category>
    <category xml:id="con-translation"><catDesc>번역(Translation)</catDesc></category>
    <category xml:id="con-ethics"><catDesc>윤리적 책임(Ethical Responsibility)</catDesc></category>
    <category xml:id="con-allegory"><catDesc>알레고리(Allegory)</catDesc></category>
  </taxonomy>
  
  <!-- 해석 태도 분류 -->
  <taxonomy xml:id="tax-interp">
    <category xml:id="int-affirmative"><catDesc>긍정적 평가</catDesc></category>
    <category xml:id="int-neutral"><catDesc>중립적 언급</catDesc></category>
    <category xml:id="int-critical"><catDesc>비판적 평가</catDesc></category>
  </taxonomy>
</classDecl>
```

#### 1차 인코딩 대상 텍스트

| 출처 | 비평문 | 우선순위 | 비고 |
|------|--------|----------|------|
| 『현대시 산고』 | 「이육사의 안 좋은 시들」 | ★★★ | 핵심 분석 대상 |
| 『잘 표현된 불행』 | 「비평의 언저리-시와 비평」 | ★★★ | 비평론 |
| 『잘 표현된 불행』 | 「비평의 언저리-세상의 계약과 문학의 계약」 | ★★★ | 비평론 |
| 『말과 시간의 깊이』 | 민족어 번역 관련 비평 | ★★☆ | 번역론 |
| 『우물에서 하늘 보기』 | 시화집 산문 | ★☆☆ | 보조 자료 |

#### 인코딩 작업 흐름

```
1. 원문 텍스트 입력
   └── OCR 또는 직접 입력
   
2. 구조 마크업
   └── div(장/절) → p(단락) → s(문장)
   
3. 개체명 태깅
   └── persName, title, orgName, term
   
4. 인용 분류
   └── quote type="direct|indirect|paraphrase"
   
5. 해석 태도 표시
   └── interp value="affirmative|neutral|critical"
   
6. 검증 및 수정
   └── XML 스키마 유효성 검사
```

### Phase 2: 네트워크 분석

#### 추출 대상 관계망

```
황현산
  │
  ├─ [영향 받은 사상가]
  │   ├─ 발터 벤야민 (알레고리, 성좌)
  │   ├─ 테오도어 아도르노 (성좌적 사유)
  │   ├─ 가스통 바슐라르 (김현 경유)
  │   └─ 프랑스 상징주의 (보들레르, 말라르메, 랭보)
  │
  ├─ [학문적 계보]
  │   ├─ 김현 (지도교수, 방법론적 영향)
  │   └─ 한국 불문학계
  │
  ├─ [동시대 비평가 네트워크]
  │   ├─ 김윤식
  │   ├─ 김우창
  │   └─ 김인환
  │
  └─ [분석 대상 시인]
      ├─ 이육사
      ├─ 윤동주
      ├─ 김수영
      └─ 기타 한국 현대시인
```

#### 분석 도구
- **Neo4j**: 그래프 데이터베이스 기반 관계망 구축
- **Gephi**: 네트워크 시각화
- **D3.js**: 인터랙티브 시각화

### Phase 3: 텍스트 마이닝

#### 분석 방법
1. **핵심 개념어 추출**: TF-IDF, 키워드 분석
2. **공기어 네트워크 분석**: 개념 간 의미적 연결
3. **토픽 모델링 (LDA)**: 비평 주제의 시기별 변화
4. **의미장(Semantic Field) 분석**: '밤', '우울', '알레고리' 등

#### 분석 도구
- **KoNLPy + Mecab**: 한국어 형태소 분석
- **Gensim**: 토픽 모델링
- **scikit-learn**: 텍스트 분류

### Phase 4: 지적 전기 통합

계량적 분석 결과를 황현산의 학문적 궤적과 통합 해석한다.

#### 주요 전기적 맥락
- 고려대학교 불어불문학과 학문적 형성기
- 김현과의 사제 관계 및 방법론적 계승
- 번역 작업을 통한 프랑스 문학/사상 수용
- 문예지 비평 활동과 한국 현대시 해석

---

## 핵심 개념어 온톨로지 (초안)

```
황현산 비평의 핵심 개념
│
├─ 낯섦 (Defamiliarization)
│   ├─ 텍스트의 엄밀한 독해
│   ├─ 관습적 가치판단의 해체
│   └─ cf. 러시아 형식주의 '오스트라네니에'
│
├─ 타자성 (Otherness)
│   ├─ 주변화된 텍스트의 복원
│   ├─ 단일 정체성 환원의 거부
│   └─ cf. 레비나스 타자 윤리학
│
├─ 번역 (Translation)
│   ├─ 언어 내 번역: 일상어 ↔ 문학어
│   ├─ 언어 간 번역: 외국어 → 한국어
│   └─ 명제: "민족문학 = 민족어의 번역"
│
├─ 윤리적 책임 (Ethical Responsibility)
│   ├─ 형언 불가능성의 확인
│   ├─ 지식 체계/계약의 재조정
│   └─ 비평가의 근본적 태도
│
└─ 알레고리 (Allegory)
    ├─ 상징 vs 알레고리 대립
    ├─ 파편화된 현실의 표현
    └─ cf. 벤야민 알레고리론
```

---

## 선행연구 참조

### 디지털 인문학 방법론
- 장문석·유인태 (2021), 「디지털 인문학과 한국문학 연구」 - 시맨틱 데이터베이스 설계
- 김일환 (2019), 「인문학을 위한 신문 빅 데이터와 텍스트 마이닝」
- Jockers (2013), *Macroanalysis: Digital Methods and Literary History*
- Women Writers Project, *Intertextual Networks* - TEI 상호텍스트성 인코딩

### 황현산 관련 연구
- 김인환, 「황현산의 산문: 비평의 원점」
- 이찬, 황현산 글쓰기의 '성좌' 분석
- 송승환 (2012), 「집중의 기술과 비평의 윤리」
- 유성호 (2016), 『우물에서 하늘 보기』 서평

### 비교 참조 (지적 전기 모델)
- Eiland & Jennings (2014), *Walter Benjamin: A Critical Life*
- Brennan (2021), *Places of Mind: A Life of Edward Said*

---

## 프로젝트 구조 (예정)

```
hwang-hyunsan-intellectual-topography/
│
├── README.md
├── data/
│   ├── raw/                    # 원본 텍스트
│   ├── xml/                    # TEI/XML 마크업 파일
│   └── processed/              # 전처리된 데이터
│
├── schema/
│   ├── tei_customization.odd   # TEI 커스텀 스키마
│   └── ontology.owl            # 개념어 온톨로지
│
├── analysis/
│   ├── network/                # 네트워크 분석 결과
│   ├── text_mining/            # 텍스트 마이닝 결과
│   └── visualization/          # 시각화 자료
│
├── papers/
│   └── drafts/                 # 논문 초고
│
└── docs/
    ├── methodology.md          # 방법론 상세 설명
    └── encoding_guidelines.md  # XML 인코딩 가이드라인
```

---

## 예상 연구 성과

1. **학술논문**: 황현산 비평의 지적 계보와 방법론적 특성 분석
2. **데이터셋**: TEI/XML로 구조화된 황현산 비평 텍스트 코퍼스
3. **시각화**: 지적 영향 관계 네트워크 인터랙티브 맵
4. **방법론적 기여**: 한국 문학비평 연구에 디지털 인문학 적용 사례

---

## 참고 링크

- [KCI 한국학술지인용색인](https://www.kci.go.kr/)
- [TEI Guidelines](https://tei-c.org/guidelines/)
- [Women Writers Project](https://wwp.northeastern.edu/)
- [Neo4j Graph Database](https://neo4j.com/)


