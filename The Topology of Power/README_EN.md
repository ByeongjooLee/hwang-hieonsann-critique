# The Topology of Power: A Data-Driven Analysis of Canon Formation and Intellectual Cartels in Korean Literary Criticism (1960–1990)

## Project Overview

Is the literary "Master" born of individual genius, or is he constructed by the structural necessities of the field?

This project employs **Digital Humanities methodologies** to analyze the mechanisms through which three dominant critics—**Kim Hyun** (1942–1990), **Kim Woo-chang** (b.1937), and **Yu Jong-ho** (b.1935)—established their authority in Korean literary criticism from the 1960s to the 1990s. We argue that the "Master" was constructed at the intersection of **transnational knowledge transfer** and **local institutional cartels**, where the **literary journal** functioned as the primary engine for legislating the canon.

This research is based on a paper submitted to **DH2026 (Digital Humanities 2026) International Conference**.

### Core Research Questions
- Under what structural conditions did the "Masters" of Korean literary criticism emerge?
- How did literary journals function as institutional power in canon formation?
- What network topology did critics occupy as brokers of Western theory?

## Research Context

### Historical Background
The 4.19 Revolution in 1960 created an ideological vacuum that could only be filled by a new breed of critic—one who possessed both **linguistic access to Western theory** and **institutional power** to enforce local standards. From the 1960s to the 1980s, the formation of Korea's literary canon was a fierce struggle for intellectual hegemony, fought primarily through the medium of the **literary journal**.

### The Three Critics

**Kim Hyun (1942–1990)**
- **Strategy**: Overcame peripherality of Korean literature through subjective appropriation of World Literature
- **Core Concept**: Synthesis of "autonomy" (inner imagination) and "heteronomy" (social role)
- **Institutional Base**: Editor of *Literature and Intelligence* (문학과지성), Professor at Seoul National University
- **Distinctive Feature**: Applied French theory (Bachelardian phenomenology) to criticism of the "Hangul Generation" poets

**Kim Woo-chang (b.1937)**
- **Strategy**: Elevated literary criticism to civilizational diagnosis
- **Core Concept**: "Concrete Totality"
- **Institutional Base**: Editor of *World Literature* (세계의문학), Professor at Korea University
- **Distinctive Feature**: Expanded Korean literary studies into philosophical anthropology

**Yu Jong-ho (b.1935)**
- **Strategy**: Deconstructed hierarchy between Western center and Korean periphery
- **Core Concept**: Theorization of Korean literature's "locality"
- **Institutional Base**: Editor of *World Literature* (세계의문학), Professor at Ewha Womans University
- **Distinctive Feature**: Established independent empirical standards for the canon

Their authority was absolute: **a positive review guaranteed canonical status**, while **silence meant obscurity**.

## Methodology

This study employs a multi-layered methodological pipeline to operationalize the concept of "critical power."

### 1. Construction of Citation and Social Networks
- **Named Entity Recognition (NER)**: Extract entities from complete critical works
- **Intellectual Genealogy Network**: Maps directional references from Western theorists (Source) → Korean authors (Target)
  - Example: Bachelard → Kim Hyun → Korean Poetry
- **Institutional Social Network**: Utilizes metadata from literary journals and lists of judges for major awards
  - Reveals "strong ties" between editor-critics ↔ promoted writers

### 2. Measuring Gatekeeping via Centrality
- **Betweenness Centrality** calculation
- **Hypothesis**: The three critics possessed the highest centrality scores → "gatekeeper" status
  - Monopolized the shortest path between Source (Western Theory) ↔ Target (Korean Canon)

### 3. Discursive Hegemony via Word Embeddings
- **Diachronic Word2Vec models**: Trained on time-sliced corpora (1960s, 1970s, 1980s)
- **Semantic shift tracking**: Analyze nearest neighbors of key critical terms ("Sensibility," "Precision")
- **Legislative effect measurement**: Visualize how their idiosyncratic definitions became standardized vocabulary

### 4. Text Encoding and Entity Linking
- **TEI XML**: Digitized 459 pages of Kim Woo-chang's critical essays
- **Wikidata/Wikipedia integration**: Built database of 4,000+ persons
- **Korean Culture Encyclopedia API** integration

## Dataset

### Network Analysis Data
| File | Description | Scale |
|------|-------------|-------|
| `network_nodes.csv` | Philosophers, critics, Korean authors | 63+ nodes |
| `network_edges_with_quotes_v2.csv` | Citation relationships with direct quotations | 130+ edges |

**Network Features**:
- Node types: critic, philosopher, author, essay
- Edge attributes: source, target, relation, essay, quote (direct quotation)
- Example data:
  ```
  Source: "Poor Poet's Era" (essay)
  Target: "Goldmann" (philosopher)
  Quote: "Goldmann defines worldview as a coherent perspective..."
  ```

### Person Database
| File | Description | Scale |
|------|-------------|-------|
| `enriched_persons_with_wikidata.json` | Person data with Wikidata QID | 4,000+ persons |
| `enriched_persons_with_wikipedia.json` | Wikipedia references added | 664 entries (16.5% coverage) |
| `enriched_persons_from_list_api.json` | Korean Culture Encyclopedia API data | 4,021 persons |

**Data Fields**:
- Basic info: role, era, definition, eid (encyclopedia ID)
- External links: Wikipedia URL, Wikidata QID
- Structured data: birth/death dates, occupation, nationality (Wikidata properties)

### Text Data
- **Kim Woo-chang's Essays**: 9 TEI XML files (459 pages)
  - Complete text of "Poor Poet's Era"
  - 25 individual essay analysis markdown files
- **Baek Chul's Literary History**: 4 HTML/XML versions

## Key Findings

### Tri-Conditional Structure of Authority
Analysis reveals that all three critics shared the following conditions:
1. **Access to Western languages** (Access)
2. **Subjective appropriation of theory** (Appropriation)
3. **Institutionalization through journals** (Institution)

### Two Models of Power Formation

#### 1. Yu Jong-ho & Kim Woo-chang: Legislative Power
- **Network Topology**: Strategic "middle ground" centered on *World Literature*
- **Gatekeeping Evidence**: Citation data surrounding the "Today's Writer Award"
  - Yi Mun-yol's canonization: centrality skyrocketed following Yu's endorsement
- **Institutional Reproduction**: Graduate students → *World Literature* contributors pipeline
  - Utilized university positions at Ewha/Korea University

#### 2. Kim Hyun: Revolutionary of Sensibility
- **Network Topology**: High-density bridge to French Theory
- **Discursive Appropriation**: Bachelardian phenomenology → critical language for 1970s poets
- **Institutional Reproduction**: Seoul National University lecture room = *Literature and Intelligence* editorial desk
  - Constructed "Moonji School": disciples reproduced his theoretical vocabulary

### Timeline Analysis
- **Centrality Score Peaks**: Correlation with journal founding years
  - Kim Hyun: 1970 (*Literature and Intelligence*)
  - Yu/Kim Woo-chang: 1976 (*World Literature* editorial participation)
- **Hypothesis Support**: "Master" is a product of **institutional positioning** rather than purely textual brilliance

## Project Structure

```
The Topology of Power/
├── data/
│   ├── network_nodes.csv              # Network node data
│   ├── network_edges_with_quotes_v2.csv  # Citation relationships with quotes
│   ├── enriched_persons_with_wikidata.json  # Person database
│   └── [Kim Woo-chang/Baek Chul source TEI XML files]
│
├── scripts/
│   ├── convert_to_xml.py              # Text → TEI XML conversion
│   ├── enrich_from_list_api.py        # Korean Culture Encyclopedia API integration
│   ├── add_wikipedia_refs.py          # Wikipedia data enrichment
│   ├── add_wikidata_refs.py           # Wikidata linking
│   └── validate_xml.py                # TEI XML schema validation
│
├── docs/
│   ├── README.md                      # Korean documentation
│   ├── README_EN.md                   # This document (English)
│   ├── WIKIDATA_GUIDE.md              # Wikidata integration guide
│   └── gephi_layout_settings.md       # Gephi visualization settings
│
└── korean-critique-schema.xsd         # TEI XML schema definition
```

## Usage

### Environment Setup

```bash
# Clone repository
git clone https://github.com/ByeongjooLee/The-Topology-of-Power.git
cd The-Topology-of-Power

# Install Python dependencies
pip install -r requirements.txt

# Required libraries (example):
# - pandas, networkx (network analysis)
# - lxml (XML processing)
# - requests (API calls)
# - gensim (Word2Vec)
```

### Network Visualization (Gephi)

1. Install **Gephi 0.10.x**
2. Import data:
   - `network_nodes.csv` → Nodes table
   - `network_edges_with_quotes_v2.csv` → Edges table
3. Apply layout:
   - **ForceAtlas 2** algorithm
   - Scaling: 50.0, Gravity: 5.0
   - See [`gephi_layout_settings.md`](docs/gephi_layout_settings.md) for details
4. Node sizing: Ranked by In-Degree

### XML Conversion and Validation

```bash
# Convert text files to TEI XML
python scripts/convert_to_xml.py

# Validate XML schema
python scripts/validate_xml.py
```

### API-Based Person Data Collection

```bash
# Collect person data from Korean Culture Encyclopedia API
python scripts/enrich_from_list_api.py --mode literature --pages 10

# Add Wikipedia information
python scripts/add_wikipedia_refs.py

# Add Wikidata QID and structured data
python scripts/add_wikidata_refs.py
```

For detailed Wikidata integration workflow, see [`WIKIDATA_GUIDE.md`](docs/WIKIDATA_GUIDE.md).

## Scholarly Contributions

### Contributions to Digital Humanities Discourse
1. **Canon Formation in the Global South**: Local power generated through Transnational Brokerage
2. **Visualization of Institutional Cartels**: Structural anatomy of "Intellectual Cartels" sustained by journals and universities
3. **Demystification of Solitary Genius**: Data-driven evidence exposing the structural topology of the "Master"

### Methodological Innovation
- **Korean NER + Wikidata Integration**: Connecting non-Western humanities data to international standards
- **Direct Quotation Networks**: Analysis of discursive appropriation beyond simple citation counts
- **Diachronic Word Embeddings**: Quantification of critical terms' legislative process

## Citation

If you use this project in your research, please cite as follows:

```
Lee, Byeongjoo. (2026). The Topology of Power: A Data-Driven Analysis of Canon
Formation and Intellectual Cartels in Korean Literary Criticism (1960–1990).
Paper presented at Digital Humanities 2026.
GitHub repository: https://github.com/ByeongjooLee/The-Topology-of-Power
```

## License

This project is publicly available for academic research purposes. Please attribute the source when reusing data or code.

## Contact

- **Researcher**: Byeongjoo Lee
- **Affiliation**: [Institution]
- **Email**: [Email address]
- **GitHub**: https://github.com/ByeongjooLee/The-Topology-of-Power

---

**DH2026 Conference Submission** | **Digital Humanities** | **Korean Literary Criticism** | **Network Analysis** | **Canon Formation**
