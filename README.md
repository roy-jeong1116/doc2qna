문서 기반 자동 QnA 생성 및 RAG 시스템

doc2qna는 사내의 다양한 형식의 문서(PDF, DOCX, PPTX, HTML, 이미지 등)를 자동 분석하여 핵심 정보를 추출하고, LLM을 기반으로 질의응답(QnA) 쌍을 생성합니다. 이렇게 구축된 QnA 쌍은 RAG(Retrieval-Augmented Generation) 기반 검색 시스템에 활용되며, 사용자의 질의에 대해 정확하고 일관된 응답을 제공합니다.

## 프로젝트 개요

- 다양한 포맷의 문서 자동 처리 및 전처리
- 텍스트 추출 + OCR 기반의 문서 분석
- LLM 기반 QnA 쌍 자동 생성
- FAISS 기반 벡터 저장소 구성 및 검색 시스템 구축
- Streamlit 기반 인터페이스 제공

## 프로젝트 목표

1. 다양한 포맷의 사내 문서를 자동 처리
2. 문서 내 유의미한 정보 추출 및 QnA 생성
3. 생성된 QnA를 바탕으로 벡터 검색 기반 RAG 시스템 구축
4. 직관적인 대시보드 인터페이스 개발
5. 시스템 성능 평가 및 지속적인 개선

## 디렉토리 구조

```
doc2qna/
├── app/                    # 사용자 인터페이스 (Streamlit, Gradio 등)
│   └── main.py
│
├── data/                   # 업로드된 원본 문서 저장소
│
├── doc_loader/             # 문서 포맷별 로더 및 OCR 처리
│   ├── loader.py           # 전체 라우팅 및 문서 감지
│   ├── text_loader.py      # TXT, HTML, CSV
│   ├── pdf_loader.py       # PDF (텍스트 + OCR)
│   ├── docx_loader.py      # DOCX
│   ├── pptx_loader.py      # PPTX
│   ├── xlsx_loader.py      # XLSX
│   ├── eml_loader.py       # 이메일
│   ├── image_loader.py     # JPG, PNG (OCR)
│   └── vision_parser.py    # 도면, 구조도 이미지 분석 (확장 가능)
│
├── preprocessing/          # 텍스트 정제 및 문단/문장 분리
│   └── splitter.py
│
├── qna_generator/          # LLM을 통한 자동 QnA 생성
│   └── generate_qna.py
│
├── retriever/              # 문서 임베딩 및 벡터 검색
│   └── embed_store.py
│
├── utils/                  # 공통 유틸 함수
│   └── file_utils.py
│
├── requirements.txt
└── README.md
```

## 지원 문서 포맷

| 포맷       | 처리 방식               | 사용 기술                        |
|------------|--------------------------|----------------------------------|
| PDF        | 텍스트 + OCR             | PyMuPDF, pdf2image, pytesseract |
| DOCX       | 텍스트 추출              | python-docx, docx2txt           |
| PPTX       | 슬라이드 텍스트 추출     | python-pptx                     |
| XLSX       | 셀 내용 파싱             | openpyxl, pandas                |
| HTML       | 본문 파싱                | BeautifulSoup, html2text        |
| EML/MSG    | 이메일 본문/첨부 추출    | extract-msg                     |
| TXT        | 일반 텍스트              | built-in                        |
| 이미지     | OCR 텍스트 추출          | pytesseract, PIL                |
| 구조도/도면| 구조 분석 (확장 가능)    | OpenCV, GPT-4V (계획)           |

## 주요 기술 스택

- 문서 처리: PyMuPDF, python-docx, openpyxl, extract-msg
- OCR: pytesseract, pdf2image, Pillow, OpenCV
- LLM 파이프라인: LangChain, OpenAI API
- 벡터 검색: FAISS, SentenceTransformers
- 문서 전처리: unstructured, chardet
- UI: Streamlit 또는 Gradio
