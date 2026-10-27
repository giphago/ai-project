# RAG 기반 법률 판례 질의응답 챗봇

# 프로그램 개요
Python, FastAPI, ChromaDB, Ollama를 활용하여 판례 검색과 LLM 응답 생성을 연결한 팀 프로젝트

# 주요 기능
법률 판례 데이터 전처리 및 임베딩 <br />
ChromaDB를 활용한 관련 판례 유사도 검색 <br />
FastAPI 기반 /query REST API <br />
검색 결과와 사건번호를 포함한 LLM 프롬프트 구성 <br />
Ollama HTTP API를 이용한 답변 생성 <br />
React Native·Expo 기반 질의응답 화면 <br />

# 시스템 흐름
판례 데이터 → 전처리 및 임베딩 → ChromaDB 저장 <br />
사용자 질문 → FastAPI → 질문 임베딩 → 관련 판례 검색 → 프롬프트 구성 → Ollama → 답변 반환<br />

## Korean law based RAG

### 개발환경

- Vector DB : ChromaDB, Docker
- LLM : LLAMA2, OLLAMA

#### 개발 Diagram 예시

┌──────────────────────────────────────────┐
│ Legal Docs │
└──────────────────────────────────────────┘
| Preprocess
v
┌────────────────────────────────────────────────────────┐
│ Document Chunking & Embedding (Python Scripts) │
│ • Splits text into chunks │
│ • Uses local embedding model to produce vectors │
└────────────────────────────────────────────────────────┘
|
| Insert
v
┌────────────────────────────────────────────────────────┐
│ Chroma Vector Database │
│ • Stores embeddings & metadata │
│ • Handles similarity search │
└────────────────────────────────────────────────────────┘
^
| Query embedding
┌────────────────────────────────────────────────────────┐
│ Query Handling (Python + Ollama + Chroma) │
│ 1) Receive user query │
│ 2) Embed query │
│ 3) Retrieve top chunks from Chroma │
│ 4) Build prompt with context │
│ 5) Send to Ollama LLM │
│ 6) Return LLM answer to the user │
└────────────────────────────────────────────────────────┘

#### 사용방법

1. ChromaDB 구축
2. Vector Embedding -> embed_store.py 실행
3. query.py 실행 전, shell ollama 경로 설정 set PATH=%PATH%;C:\Users\사용자\AppData\Local\Programs\Ollama\
4.

#### 개발일지

2025-03-11: Vector Storage 환경 설정

2025-03-15: 환경 구상 설계 - Vector Storage : ChromaDB - LLM Hosting : OLLAMA

2025-03-16: python 3.11 rolldown, Prototype구축, OLLAMA 구축

##### 데이터 출처

- https://www.aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100&aihubDataSe=data&dataSetSn=99
- https://www.aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100&dataSetSn=71723
- https://huggingface.co/datasets/joonhok-exo-ai/korean_law_open_data_precedents
- https://github.com/lbox-kr/lbox-open

이 프로젝트는 학습 및 시연 목적으로 개발되었으며, 실제 법률 자문 서비스를 대체하지 않습니다.
