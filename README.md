# 지식그래프와 LLM 융합 기반 계약서 위험 분석 시스템

[](https://fastapi.tiangolo.com/)
[](https://react.dev/)
[](https://neo4j.com/)
[](https://vitejs.dev/)
[](https://www.python.org/)

**2025 서초 AI 칼리지 리걸케어팀(박재연, 최준호)의 Full-stack 프로젝트입니다.**

지식그래프 기반의 하이브리드 RAG(Retrieval-Augmented Generation)를 통해 계약서의 위험 조항을 분석하고 질의응답을 제공하는 시스템입니다.

-----

## 📜 학술 포스터 (Academic Poster)

프로젝트의 전체 아키텍처와 결과를 요약한 포스터입니다.

*아래 이미지를 클릭하면 고해상도 PDF로 보실 수 있습니다.*

[![Project Poster](./assets/poster_preview.png)](./assets/poster_full.pdf)

## 🏛️ 시스템 아키텍처

<img width="1904" height="1793" alt="Image" src="https://github.com/user-attachments/assets/442cd4e7-4193-4743-8fd0-78a1cfd75e69" />


## 🚀 주요 기능

  * **파일 업로드 및 파이프라인 실행**: 계약서(PDF/DOCX) 업로드 시 ATLAS 기반 지식그래프 자동 구축 및 임베딩
  * **하이브리드 RAG 검색**: 키워드 기반(BM25/Vector) 검색과 그래프 기반(KG) 검색을 결합한 질의응답
  * **계약서 위험 조항 분석**: 파트별 체크리스트 기반으로 위험 조항을 병렬 처리 후 LLM이 최종 결과 통합
  * **실시간 상태 모니터링**: 파일 처리 및 분석 파이프라인의 진행 상태 실시간 로깅 및 추적

## 🅿️ 핵심 파이프라인

<img width="3840" height="2126" alt="Image" src="https://github.com/user-attachments/assets/51aa53c4-a17a-4a2f-9536-3064f042c458" />

## 🛠️ 기술 스택

  * **백엔드 (BE)**: FastAPI, Neo4j, OpenAI, FAISS
  * **프런트엔드 (FE)**: React, Vite, shadcn-ui

-----

## 🚀 시작하기 (Getting Started)

### 1\. 사전 준비 사항

  * **Python 3.12** 버전 (Conda 환경 권장)
  * **Faiss-gpu 설치 (Conda 사용 시)**:
      * `faiss-gpu`는 `pip`보다 `conda`로 먼저 설치하는 것을 권장합니다.
    <!-- end list -->
    ```bash
    conda install -c conda-forge faiss-gpu=1.8.0
    ```

### 2\. 환경 변수 설정 (.env)

  * **백엔드**: `BE/env.example` 파일을 `BE/.env`로 복사한 후, 내부의 `NEO4J_URI`, `OPENAI_API_KEY` 등 필수 값들을 설정합니다.
      * *참고: 배포 환경에 따라 `NEO4J_URI`는 `neo4j`, `neo4j+s`, `bolt` 등을 사용할 수 있습니다.*
  * **프런트엔드**: `FE/workspace/shadcn-ui/env.local.example` 파일을 `FE/workspace/shadcn-ui/.env.local`로 복사 후 내부 값을 수정합니다.

### 3\. 백엔드 실행 (FastAPI)

```bash
# 1. BE 폴더로 이동
cd BE

# 2. 의존성 설치
pip install -r requirements.txt

# 3. 환경변수 파일 복사 (2번 단계에서 이미 수행)
# Windows: copy env.example .env
# macOS/Linux: cp env.example .env

# 4. 서버 실행
# Windows
run_server.bat
# macOS/Linux/공통
python run_server.py
```

  * **API 문서**: [http://localhost:8000/docs](https://www.google.com/search?q=http://localhost:8000/docs) (Swagger UI) 또는 [http://localhost:8000/redoc](https://www.google.com/search?q=http://localhost:8000/redoc) (ReDoc)

### 4\. 프런트엔드 실행 (React)

```bash
# 1. FE 폴더로 이동
cd FE/workspace/shadcn-ui

# 2. 의존성 설치 (pnpm 권장)
pnpm install
# 또는 npm install

# 3. 개발 서버 실행
pnpm run dev
# 또는 npm run dev
```

  * **개발 서버**: [http://localhost:5173](https://www.google.com/search?q=http://localhost:5173) (Vite 기본 포트)

-----

## 📦 레포지토리 구조

```
AutoSchemaKG-1/
├── BE/                           # 백엔드 (FastAPI)
│   ├── server.py                 # 메인 서버
│   ├── run_server.py             # 서버 실행 스크립트
│   ├── requirements.txt          # Python 의존성
│   ├── env.example               # 환경변수 예시
│   ├── riskAnalysis/             # 위험분석 모듈
│   │   └── README.md             # (위험분석 시스템 세부 가이드)
│   └── README_SERVER.md          # (백엔드 세부 가이드)
│
└── FE/
    └── workspace/
        └── shadcn-ui/            # 프런트엔드 (Vite + React)
            └── README.md         # (프런트엔드 세부 가이드)
```

## 🔌 주요 API 엔드포인트

  - `POST /upload-and-run`: 파일 업로드 및 전체 파이프라인 실행
  - `POST /pipeline/run`: 파이프라인 수동 실행
  - `GET /pipeline/status/{pipeline_id}`: 파이프라인 진행 상태 조회
  - `POST /chat`: RAG 기반 질의응답
  - `POST /analyze-risks`: 계약서 위험분석 실행
  - **전체 API 목록**: [http://localhost:8000/docs](https://www.google.com/search?q=http://localhost:8000/docs)

## 🛠️ 트러블슈팅

  * **Neo4j 연결 오류**: Neo4j 서버가 정상적으로 실행 중인지, `BE/.env`의 `NEO4J_URI`, `NEO4J_USER`, `NEO4J_PASSWORD` 정보가 올바른지 확인합니다.
  * **OpenAI 오류**: `BE/.env`의 `OPENAI_API_KEY`가 유효한지, OpenAI 요금제 및 사용 한도를 초과하지 않았는지 확인합니다.
  * **CORS/프록시 이슈**: 프런트엔드에서 API 요청이 실패할 경우, 브라우저 콘솔에서 CORS 오류를 확인합니다. `Vite`의 프록시 설정과 FastAPI의 CORS 설정이 올바른지 확인합니다.
  * **모델/설정 값 불일치**: `.env` 파일의 `DEFAULT_MODEL` 등의 설정이 코드의 기본값과 일치하는지 확인합니다.

## 📚 참고 문헌 (References)

본 프로젝트는 다음의 핵심 선행 연구들을 기반으로 합니다.

  * Zheng, C., Wong, S., Su, X., Tang, Y., Nawaz, A., & Kassem, M. (2023). **[Automating construction contract review using knowledge graph-enhanced large language models](https://arxiv.org/abs/2309.12132)**. *arXiv preprint arXiv:2309.12132*.

    > *요약: LLM과 지식 그래프(KG)를 통합하여 계약서의 위험 식별 정확도와 해석 가능성을 향상시키는 GraphRAG 프레임워크를 제안합니다.*

  * Bai, J., Fan, W., Hu, Q., et al. (2025). **[AutoSchemaKG: Autonomous Knowledge Graph Construction through Dynamic Schema Induction from Web-Scale Corpora](https://arxiv.org/abs/2505.23628)**. *arXiv preprint arXiv:2505.23628*.

    > *요약: 사전 정의된 스키마 없이, LLM을 활용하여 텍스트에서 직접 지식 트리플(knowledge triples)을 추출하고 스키마를 유도하는 자율적인 KG 구축 프레임워크를 제안합니다.*
