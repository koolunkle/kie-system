# KIE System (Key Information Extraction)

AI 기반 이미지 정보 추출(OCR) 및 구조화(KIE)를 위한 통합 시스템입니다. 이 프로젝트는 이미지 내의 텍스트를 인식하고, 비정형 데이터를 의미 있는 구조로 변환하는 기능을 제공합니다.

## 시스템 구성 및 역할

전체 시스템은 클라이언트 인터페이스와 분석 핵심 엔진으로 구성되어 있습니다.

### 1. KIE Client (apps/kie-client)
- 역할: 사용자 및 외부 시스템과의 접점 역할을 수행하는 서비스 레이어입니다.
- 기술: Java 21, Spring Boot 3.x
- 주요 기능:
    - 이미지 업로드 요청 수락 및 유효성 검증
    - 분석 엔진(KIE Module)과의 통신 및 결과 중계
    - 통합 에러 핸들링 및 표준 API 응답 규격 제공

### 2. KIE Module (apps/kie-module)
- 역할: AI 모델이 구동되어 실제 데이터를 분석하는 핵심 엔진입니다.
- 기술: Python 3.13, FastAPI, PaddleOCR, LayoutXLM
- 주요 기능:
    - PaddleOCR을 활용한 고성능 텍스트 영역 검출 및 인식
    - LayoutXLM(SER) 모델을 통한 엔티티 간 관계 분석 및 데이터 구조화
    - 이미지 전처리 및 분석 결과의 JSON 변환

---

## 실행 가이드

### KIE Module 실행 (Python)
```powershell
cd apps/kie-module
uv sync
uv run python -m uvicorn app.main:app --reload --port 8000
```

### KIE Client 실행 (Java)
```powershell
cd apps/kie-client
./gradlew bootRun
```

---

## 프로젝트 구조

- apps/kie-client: Spring Boot 기반 클라이언트 애플리케이션
- apps/kie-module: FastAPI 기반 AI 분석 엔진
- libs: 공용 자산 및 라이브러리 저장소
- models: 분석에 필요한 사전 학습된 AI 모델 파일 (ONNX)
