# 포스코 Gemini Enterprise(GE) 경영기획 DX 과제 상세 과제수행계획서

작성일: 2026-05-26 KST


## 문서 개요

- 문서명: 포스코 Gemini Enterprise(GE) 경영기획 DX 과제 상세 과제수행계획서
- 작성일: 2026-05-26 KST
- 발주처: POSCO
- 수행사: 메가존소프트 / TPCG
- 사업 기간: 2026년 6월 ~ 12월
- 일정 기준: 2026년 6월~11월 구축 완료, 2026년 12월 사용자 테스트(UAT) 및 운영 전환 준비
- 참조자료: 첨부 `포스코DX_수행계획서_260526.docx`, POSCO 경영기획DX 작업/추진계획서, POSCO GE 아키텍처 논의 메모, GBrain/LLM Wiki POSCO GE 프로젝트 지식, Google Gemini Enterprise Agent Platform 참조 지식


## 1. Executive Summary

본 과제는 POSCO 경영기획 조직의 비정형 문서 자산, 투자 심의/발의 업무, 사업관리 리서치 업무를 Gemini Enterprise(GE) 기반의 업무형 AI Agent 서비스로 전환하는 구축 사업이다. 단순 RAG 검색 PoC가 아니라, GE의 Agent Platform 역량을 중심으로 과거문서 검색, Prompt Assist, 투자계획서 심의 Agent(PIIA), 투자발의 Agent, 사업관리 Deep Research Agent를 통합 구축하고, 향후 POSCO 내부 Agentic Workflow 운영체계로 확장 가능한 기반을 마련하는 것을 목표로 한다.

본 계획서는 첨부 수행계획서의 1차/2차 단계 구조를 유지하되, 최신 일정 요구에 맞추어 2026년 6월부터 11월까지 구축을 완료하고 12월에는 사용자 테스트와 운영 전환 검증에 집중하도록 재구성하였다. 1차는 GE 기반 검색·Prompt Assist·PIIA/사업관리 기본 기능의 안정화와 품질 검증에 집중하고, 2차는 투자발의 Agent, GE Agent Flow/Skill 고도화, 이력관리, 평가 하네스, UI/UX, 보안/운영체계까지 통합 완성하는 방식으로 추진한다.

핵심 설계 원칙은 첫째 Gemini Enterprise 표준 기능을 최대한 활용하고, 둘째 GE 표준 기능으로 부족한 문서 변환, page-level citation, custom preview/highlight, 이력관리, 평가 자동화, 사내 시스템 연계는 Google Cloud 관리형 서비스와 경량 Custom UI로 보강하며, 셋째 12월 UAT 전까지 보안·품질·운영·인수 기준을 명확히 검증하는 것이다.


## 2. 사업 배경 및 추진 목표

POSCO 경영기획 업무는 투자 심의, 사업 계획, 경쟁사/시장 리서치, 법인별 이력 관리 등 문서와 의사결정 근거가 많은 지식집약형 업무로 구성된다. 기존 문서는 PPT, PDF, 보고서, 회의록, 내부 가이드, 과거 투자 사례 등 다양한 형식으로 축적되어 있으나, 업무 담당자가 필요한 근거를 빠르게 찾고 검증하며 정형 보고서로 전환하기까지 많은 시간이 소요된다.

본 과제의 목표는 다음과 같다.
- 경영기획 업무 문서를 GE 데이터스토어와 Google Cloud 기반 메타데이터 체계로 연결하여 권한 인식 검색과 근거 기반 답변을 제공한다.
- 사용자 질문을 업무 목적에 맞게 보정하는 Prompt Assist Agent를 구축하여 검색 품질과 질문 품질을 동시에 개선한다.
- 투자계획서 심의 Agent를 통해 누락 항목, 리스크, 대응방향, 심의 보고서 초안을 자동 도출한다.
- 투자발의 Agent를 통해 PIIA 산출물과 심의 결과를 발의서 초안으로 연결한다.
- 사업관리 Agent를 통해 Deep Research 기반 경쟁사/시장/법인 이력 분석과 결과 이력관리를 제공한다.
- Agent 개발·배포·평가·운영 체계를 GE Agent Platform 중심으로 정립하여 향후 POSCO 내부 업무 Agent 확산의 기준 모델을 만든다.


## 3. 추진 범위 총괄

본 과제의 범위는 4개 업무 AI 기능과 5개 공통 기반 영역으로 구성한다.

업무 AI 기능:
1. 과거문서 검색 및 RAG 기반 답변: 문서 적재, 파싱, 청킹, 메타데이터, 하이브리드 검색, citation/preview 제공
2. Prompt Assist Agent: 사용자 질의 의도 분석, 질문 보정, 업무유형별 템플릿, 후속질문 추천
3. 투자계획서 심의 Agent(PIIA): 투자 제안서 검토, 심의 항목 추출, 리스크 진단, 대응방향 및 심의 보고서 초안 생성
4. 투자발의/사업관리 Agent: PIIA 결과 기반 발의서 초안 작성, Deep Research 기반 경쟁사/시장 분석, 리서치/법인 이력 관리

공통 기반 영역:
1. GE Agent Platform 기반 Agent 설계·배포 체계
2. GCS/BigQuery/Firestore 기반 데이터·메타데이터·이력 관리
3. Cloud Run/Functions/Workflows/Eventarc 기반 파이프라인 및 보조 서비스
4. IAM/WIF/IAP/VPC-SC/Cloud Audit Logs 기반 보안·접근통제
5. 품질평가 하네스, 운영 대시보드, UAT/인수 기준


## 4. 최신 Gemini Enterprise Agent Platform 적용 방향

본 구축은 GE를 단순 검색 포털이 아니라 Agent 개발, 오케스트레이션, 거버넌스를 수행하는 단일 업무형 Agent Platform으로 활용하는 것을 기본 방향으로 한다. 적용 방향은 다음과 같다.

- Gemini Enterprise App/Data Store: 경영기획 전용 업무 포털, 문서 검색, grounded answer, 업무별 Agent 진입점으로 사용한다.
- GE Agent Designer / Agent Flow: Prompt Assist, PIIA, 투자발의, 사업관리 Agent의 업무흐름을 설계하고, No-Code/Low-Code 방식으로 업무 담당자와 빠르게 검증한다.
- Agent Registry / Skills / Actions: 업무 Agent를 기능 단위로 모듈화하고, 문서 검색 Skill, 투자 심의 Skill, Deep Research Skill, 보고서 생성 Skill, 이력 조회 Action 등을 재사용 가능한 컴포넌트로 관리한다.
- Gemini API with Google Search Grounding: 사업관리/Deep Research 영역에서 최신 웹 정보, 산업 동향, 경쟁사 정보의 출처 기반 분석을 수행한다.
- Gemini Embedding / Retrieval: RAG 문서의 의미 기반 검색, 유사 사례 검색, 하이브리드 검색 재랭킹에 활용한다.
- Vertex AI / Evaluation Harness: 답변 품질, hallucination, context faithfulness, citation coverage, retrieval precision을 정량 평가한다.
- Prompt Caching / Context Caching: 반복 사용되는 투자 심의 기준, 업무 가이드, 대형 컨텍스트에 대해 비용과 latency를 최적화한다.
- Agent Gateway / 보안 거버넌스 연계: 향후 사내 시스템, 외부 검색, DB 조회 등 tool surface를 통제된 방식으로 확장할 수 있도록 설계한다.

GE 표준 기능으로 해결 가능한 영역과 별도 개발이 필요한 영역은 명확히 분리한다. GE의 표준 기능은 검색, 답변, Agent 진입점, Skill 기반 업무흐름에 우선 적용하고, PDF/PPT 변환, page-level preview/highlight, 사내 시스템 연계, 이력관리, 세부 운영 대시보드는 Google Cloud 기반 Custom Extension으로 보강한다.


## 5. 목표 아키텍처

목표 아키텍처는 “사용자 접점 → GE Agent Layer → Retrieval/Data Layer → Extension/Integration Layer → Governance/Operation Layer”의 5계층으로 설계한다.

1. 사용자 접점 계층
- GE 기본 UX: 경영기획 사용자용 검색/답변/Agent 실행 진입점
- Custom UI: Prompt Assist, 검색 결과 상세, PDF viewer, citation/highlight, 이력관리, 보고서 다운로드 기능
- 접근통제: 사내 SSO, IAP, GE 사용자 권한, 업무그룹별 접근권한 연동

2. GE Agent Layer
- Prompt Assist Agent: 질문 보정, 업무유형 분류, 검색 템플릿 추천
- PIIA Agent: 투자계획서 심의 항목 추출, 리스크 진단, 심의 보고서 초안
- 투자발의 Agent: 심의 보고서 기반 발의서 초안 생성, 항목별 재생성
- 사업관리 Agent: Deep Research, 경쟁사 비교, 사업계획 검토, 결과 리포트
- 공통 Skill: 검색, citation, 보고서 생성, 이력 조회, 평가, 권한 검증

3. Retrieval/Data Layer
- Cloud Storage: 원본 문서, 변환 문서, 첨부파일, 산출물 저장
- Gemini Enterprise Data Store: GE 검색/답변용 인덱스 및 blended search 구성
- BigQuery Metadata Registry: 문서, 버전, 페이지, chunk, ACL, pipeline run, 평가결과 관리
- Firestore: 사용자 작업 이력, 리서치 이력, 법인별 이력, Agent 실행 상태 관리

4. Extension/Integration Layer
- Cloud Run/Functions: 문서 변환, Preview API, Deep Research orchestration, report generation API
- Workflows/Eventarc: 문서 적재, 변환, 색인, 품질검증의 E2E pipeline
- Document AI/OCR/Layout Parser: 이미지 기반 PDF, PPT 도표/표/스캔 문서 보강
- Gemini API + Search Grounding: 최신 외부 정보 기반 검토와 출처 확인

5. Governance/Operation Layer
- IAM/WIF/IAP/VPC-SC/CMEK/Secret Manager/Cloud Audit Logs
- Cloud Logging/Monitoring/Error Reporting
- 평가 하네스: retrieval precision, citation coverage, faithfulness, hallucination rate, latency, cost metric
- 운영 대시보드: ingestion 상태, 검색품질, Agent 사용량, 오류, 비용, 권한 이슈


## 6. 단계별 추진 전략

일정은 1차/2차를 완전히 분리한 순차 추진이 아니라, 1차 핵심 기능을 조기 안정화하면서 2차 고도화 설계를 병행하는 통합 추진 방식으로 운영한다.

1차 구축(2026년 6월~8월): 기본 기능 구현 및 핵심 업무 검증
- GE/GCP 기본 환경 구성, 데이터스토어, 권한, Agent 개발 기본 구조를 확정한다.
- 과거문서 검색, Prompt Assist, PIIA 기본 기능, 사업관리 Deep Research MVP를 구현한다.
- 문서 적재 품질, 검색 정확도, citation, 권한 검증, 사용자 질문 패턴을 수집한다.
- 8월 말 기준 2차 고도화에 필요한 요구사항, backlog, 평가 기준을 확정한다.

2차 구축(2026년 9월~11월): Agent 고도화, 통합 기능, 운영 수준 완성
- 투자발의 Agent, PIIA 보고서 초안 Agent, 사업관리 이력관리, 법인 이력관리 기능을 구축한다.
- GE Agent Flow/Skill 기반 업무흐름을 정리하고, GCP에서 개발한 기능을 GE 사용자 경험에 통합한다.
- 평가 하네스, 비용 최적화, Prompt Caching, UI/UX 개선, 통합 테스트, 운영 대시보드를 완성한다.
- 11월 말까지 기능 개발과 내부 검수를 완료하고 12월 사용자 테스트로 전환한다.

사용자 테스트 및 운영 전환(2026년 12월)
- POSCO 현업 사용자 UAT, 권한/보안 검증, 성능 검증, 운영 매뉴얼/인수인계, 최종 결과보고를 수행한다.
- 12월은 신규 기능 개발보다 사용자 검증, 결함 보완, 운영 전환 승인에 집중한다.


## 7. 상세 WBS 및 산출물

아래 WBS는 6월~11월 구축 완료, 12월 UAT 기준으로 재정렬한 수행 계획이다.

| 구분 | 기간 | 주요 작업 | 핵심 산출물 | 주관 |
|---|---|---|---|---|
| 착수/요건정의 | 6월 1~2주 | 킥오프, 요구사항 확정, 대상 문서/업무 범위 확정, 보안/권한 정책 정의 | 착수보고서, 요구사항 추적표, 데이터/권한 매트릭스 | PM/SA/POSCO |
| GE/GCP 기반 구성 | 6월 1~3주 | GE App/Data Store, GCS, BigQuery, IAM, IAP, VPC-SC, Agent 개발환경 구성 | 환경 구성서, 보안설계서, 운영계정/권한표 | Infra/SA |
| RAG 문서 적재/검색 | 6월~7월 | 문서 수집, 파싱/청킹, 메타데이터, 임베딩/색인, 검색 품질 검증 | 문서 적재 보고서, 검색품질 평가서, citation 기준 | RAG Eng |
| Prompt Assist v1 | 6월~7월 | 질문 의도 분류, Rule/템플릿, 후속질문 추천, Custom UI 연결 | Prompt Assist v1, 사용성 개선 보고서 | Agent Eng/FE |
| PIIA 기본 Agent | 7월~8월 | 투자 심의 항목 추출, 리스크 도출, 대응방향 제안, Q&A 추천 | PIIA MVP, 테스트 시나리오, 기능 QA 보고서 | Agent Eng |
| 사업관리 Deep Research MVP | 7월~8월 | 경쟁사/시장 검색, 다중 출처 종합, 구조화 리포트 생성 | 사업관리 Agent MVP, 출처 기반 리포트 샘플 | Agent Eng/SA |
| 1차 검증/Backlog 확정 | 8월 말 | 핵심 기능 검증, 사용자 피드백 수집, 2차 backlog 확정 | 1차 검증 결과서, 2차 상세 backlog | PM/POSCO |
| Agent Pipeline/Registry | 9월 | Agent 개발·배포 workflow, Skill/Action 표준, CI/CD 설계 | Agent 개발/배포 가이드, Registry 설계서 | SA/Agent Eng |
| PIIA 고도화/보고서 초안 | 9월~10월 | 심의 보고서 목차/항목별 초안 생성, citation 삽입, 항목별 재생성 | 심의 보고서 초안 Agent, 평가 결과서 | Agent Eng/FE |
| 투자발의 Agent | 9월~11월 | PIIA 산출물 연계, 발의서 항목 매핑, 발의서 초안 생성/편집/다운로드 | 투자발의 Agent, 발의서 템플릿, UAT 시나리오 | Agent Eng/FE |
| 사업관리 이력/법인관리 | 9월~11월 | 리서치 이력 저장/조회, 법인 이력 관리, 대시보드, 필터 검색 | 이력관리 모듈, 법인 대시보드, 운영가이드 | FE/Backend |
| 평가 하네스/운영 대시보드 | 10월~11월 | 품질/비용/사용량/오류 지표, 자동 평가, 모니터링/알림 | 평가 하네스, 운영 대시보드, 품질 리포트 | SA/Infra |
| 통합테스트/운영전환 준비 | 11월 | 통합 테스트, 보안/권한 회귀, 성능 검증, 인수 문서 작성 | 통합테스트 결과서, 운영 매뉴얼, 인수 기준표 | PM/전체 |
| 사용자 UAT/최종보고 | 12월 | 사용자 테스트, 결함 보완, 교육, 운영 인수인계, 최종보고 | UAT 결과서, 최종 결과보고서, 교육자료 | PM/POSCO/전체 |


## 8. 기능별 상세 수행계획

8.1 과거문서 검색 및 RAG 시스템
- 문서 범위: 경영기획 보고서, 투자 심의/발의 문서, 사업관리 문서, 과거 프로젝트 자료, 가이드/규정 문서, PDF/PPT/DOCX/XLSX 중심 자료
- 처리 방식: 원본 파일을 GCS에 저장하고, PDF/PPT는 필요 시 표준 PDF로 변환하며, 문서별 document_id/version_id/page/chunk metadata를 생성한다.
- 검색 방식: GE Data Store를 기본으로 하되, 키워드+의미 기반 하이브리드 검색, Top-k reranking, citation/page metadata를 결합한다.
- 사용자 결과: 답변, 근거 문서명, page, 유사도, 입력일자, 문서 버전, preview 링크를 함께 제공한다.

8.2 Prompt Assist Agent
- 사용자 질문을 그대로 검색하지 않고 의도, 업무유형, 대상 문서, 시간/법인/투자유형 조건을 분석한다.
- 모호한 질문은 명확한 검색 쿼리와 보고서 작성 지시로 변환한다.
- 업무 유형별 템플릿 예: 투자심의, 투자발의, 경쟁사 분석, 법인 이력 조회, 과거 사례 비교, 사업계획 검토.
- 후속 질문 3~5개를 자동 제안하여 사용자 탐색 흐름을 가이드한다.

8.3 투자계획서 심의 Agent(PIIA)
- 입력: 투자 제안서, 심의 기준, 체크리스트, 과거 유사 심의 사례, 관련 재무/시장 자료
- 처리: 문서 구조화, 누락 항목 탐지, 리스크 분류, 유사 사례 검색, 대응방향 제안
- 출력: 심의 항목별 검토 의견, High/Mid/Low 리스크, 근거 citation, 심의 보고서 초안
- 2차 고도화: GE Skill 기반 보고서 생성 Flow, 항목별 재생성, 사용자 피드백 반영, 심의→발의 연동

8.4 투자발의 Agent
- PIIA 심의 보고서를 입력으로 받아 발의서 필수 항목을 자동 매핑한다.
- 투자 목적, 기대효과, 리스크 대응, 일정, 재무/시장 근거, 의사결정 포인트를 발의서 초안으로 구성한다.
- 사용자는 항목별 편집, 재생성, 근거 확인, 최종 문서 다운로드를 수행한다.
- GE 환경에서 업무별 Skill과 Agent Flow를 조합하여 현업 사용자가 직접 접근 가능하게 한다.

8.5 사업관리 Deep Research Agent
- Google Search Grounding 기반으로 경쟁사, 시장, 기술, 규제, 산업동향을 최신 정보로 조사한다.
- 다중 출처를 종합하여 비교표, 핵심 요약, 리스크, 추천 액션을 생성한다.
- 결과는 Firestore/BigQuery/GCS에 이력으로 저장하고, 키워드/날짜/분석유형/법인별로 조회한다.
- 2차에서는 법인 이력관리, 리서치 이력관리, 이전 결과 대비 최신 변화 분석을 제공한다.


## 9. 데이터·검색·문서 처리 설계

문서 처리의 핵심은 “검색 가능한 텍스트”뿐 아니라 “눈으로 확인 가능한 근거”를 함께 보존하는 것이다.

권장 메타데이터:
- document_id, title, source_system, owner_dept, document_type
- version_id, storage_generation, checksum, ingest_batch_id, ingest_time, effective_date
- page_number, chunk_id, chunk_text, bbox, preview_url, source_uri, converted_uri
- acl_principals, acl_hash, identity_mapping_status
- parser_type, ocr_confidence, conversion_status, quality_score

파이프라인 흐름:
1. 파일 반입: GCS upload 또는 batch manifest 수신
2. 검증: 파일형식, 크기, 중복, checksum, 보안 분류 확인
3. 변환: PPT/PPTX → PDF, 필요 시 page image/thumbnail 생성
4. 추출: Document AI/OCR/Layout Parser, 텍스트/표/이미지/페이지 좌표 추출
5. 청킹: 업무 단락, 페이지, 표 단위 chunk 구성
6. 메타데이터 등록: BigQuery registry upsert
7. ACL 매핑: Entra ID/사내 그룹과 GE/Google Identity 매핑
8. GE 색인: GE Data Store 및 필요한 custom data source에 반영
9. QA: 검색 smoke test, citation 연결, preview 링크, ACL 차단 검증


## 10. 보안·권한·거버넌스 계획

보안 원칙은 “사용자가 원천 시스템에서 볼 수 없는 문서는 GE 검색 결과와 preview에서도 보이지 않아야 한다”이다.

주요 통제:
- Identity: POSCO 사내 SSO/Entra ID와 Google Cloud Workforce Identity Federation 또는 Google Identity 연동을 검토한다.
- Access Control: GE Data Store ACL, BigQuery/GCS IAM, Custom Preview API 권한을 동일한 사용자/그룹 기준으로 정렬한다.
- Network/Data Boundary: VPC Service Controls, Private Service Connect, restricted egress, IAP 기반 사용자 접근통제를 적용한다.
- Secrets: connector credential, service account key, 외부 API token은 Secret Manager에 저장한다.
- Audit: Cloud Audit Logs, GE analytics, Cloud Logging을 통해 who/what/when/where를 추적한다.
- Data Protection: CMEK, retention policy, soft delete, DLP/PII 정책을 검토한다.
- Human Review: 투자 심의/발의 결과는 최종 의사결정 전 사용자 검토와 승인 단계를 필수로 둔다.

Agent tool surface는 무제한 확장하지 않고, 검색, 문서조회, 리포트 생성, 이력조회, 외부검색 등 업무상 필요한 제한된 Action/Skill로 통제한다. 향후 사내 시스템 연계 시에는 Agent Gateway 또는 별도 API Gateway를 통해 인증, 권한, rate limit, 로그, 승인 절차를 적용한다.


## 11. 품질평가 및 테스트 계획

품질 검증은 기능 동작 여부뿐 아니라, 검색 정확도, 근거 충실성, hallucination, 권한 차단, 비용/성능, 사용자 수용성을 함께 측정한다.

평가 지표:
- Retrieval Precision@k: 주요 업무 질의별 Top-k 근거 적합성
- Citation Coverage: 답변 문장별 근거 문서/page 표시율
- Faithfulness: 답변이 참조 근거와 일치하는 비율
- Hallucination Rate: 근거 없는 주장 또는 잘못된 요약 비율
- Preview Success Rate: citation 클릭 시 문서/page/하이라이트 표시 성공률
- ACL Violation: 권한 없는 문서 노출 0건
- Latency: 검색/답변/preview/Agent 실행 응답시간
- Cost per Task: Agent별 평균 토큰/검색/실행 비용
- User Acceptance: UAT 시나리오별 성공률 및 현업 만족도

테스트 단계:
1. 단위 테스트: 파서, 변환, 검색, Agent prompt, API별 테스트
2. 기능 테스트: 과거문서 검색, Prompt Assist, PIIA, 투자발의, 사업관리 기능별 시나리오
3. 권한 테스트: 사용자/그룹/문서 등급별 접근 가능/불가 매트릭스
4. 통합 테스트: GE UX, Custom UI, GCS/BigQuery/Firestore/Cloud Run 연계
5. 성능/비용 테스트: 문서량, 동시사용자, 대형 컨텍스트, Deep Research 실행 기준
6. UAT: POSCO 현업 사용자 12월 집중 검증 및 결함 보완


## 12. R&R 및 운영 체계

| 조직/역할 | 주요 책임 | 상세 업무 |
|---|---|---|
| POSCO 경영기획DX TF | 업무 총괄/사용자 승인 | 대상 업무/문서 확정, 업무 시나리오 검증, UAT, 인수 승인 |
| POSCO DX/보안/인프라 | 보안·계정·시스템 연계 승인 | SSO/권한 정책, 데이터 반출입, 네트워크/보안 기준, 운영정책 승인 |
| 메가존소프트 PM/PMO | 전체 일정·범위·리스크 관리 | WBS, 주간회의, 이슈/변경관리, 산출물 관리, 최종보고 |
| 메가존소프트 SA/Agent Architect | 전체 아키텍처/Agent 설계 | GE/GCP 설계, Agent Flow, Skill/Action 표준, 품질/운영 기준 |
| 메가존소프트 Agent/RAG Engineer | Agent 및 검색 기능 구현 | RAG, Prompt Assist, PIIA, 투자발의, 사업관리 Agent, 평가 하네스 |
| TPCG Infra/Backend/FE | GCP/GE 환경 및 UI 구현 | GCS/BigQuery/Cloud Run/Firestore/IAP, Custom UI, 운영 대시보드 |
| Google Cloud/PSO | 제품 자문 및 품질검토 | GE 기능 제약/적용 가이드, 아키텍처 리뷰, Technical Sync, best practice 지원 |

운영 회의체는 주간 실무회의, 격주 Steering, 월간 품질/보안 리뷰로 구성한다. 12월 UAT 기간에는 일일 결함 triage와 주간 승인 회의를 운영하여 사용자 이슈를 신속히 해소한다.


## 13. 주요 리스크 및 대응 방안

| 리스크 | 영향 | 대응 방안 |
|---|---|---|
| GE 표준 기능과 요구 기능 간 gap | preview/highlight, workflow, UI 요구 미충족 | GE 표준 기능 우선, 부족분은 Cloud Run/Custom UI/metadata registry로 보강 |
| 문서 파싱/변환 품질 편차 | 검색 누락, citation 오류 | PPT→PDF 변환 QA, OCR/Layout Parser, 샘플링 검수, 실패 재처리 |
| ACL/권한 매핑 오류 | 보안 사고 | deny-by-default, 사용자/그룹 매트릭스, ACL 회귀테스트, 감사로그 검증 |
| Hallucination/근거 불일치 | 현업 신뢰도 저하 | citation 필수, 평가 하네스, Prompt Assist, human review, confidence 표시 |
| Deep Research 출처 품질 | 외부정보 오류/편향 | 출처 URL/날짜 표시, 다중출처 비교, 사용자 검토, 내부문서 우선순위 적용 |
| 일정 지연 | 11월 구축 완료 실패 | 1차/2차 backlog 명확화, 12월 신규개발 금지, 범위변경 절차 운영 |
| 비용 증가 | 운영비 초과 | Prompt/Context Caching, Agent별 비용계측, budget alert, OCR/Deep Research 대상 선별 |
| 사용자 수용성 부족 | UAT 실패 | 6~8월부터 현업 피드백 수집, 템플릿/UX 반복 개선, 교육자료 조기 작성 |


## 14. 산출물 계획

1차 산출물:
- 착수보고서 및 요구사항 추적표
- GE/GCP 아키텍처 설계서
- 문서 적재/색인 대상 목록 및 품질 평가 결과
- RAG 검색/Prompt Assist v1 구현 결과
- PIIA/사업관리 Agent MVP 및 테스트 결과
- 보안/권한 매트릭스 및 ACL 테스트 결과
- 1차 검증 결과서 및 2차 backlog

2차 산출물:
- Agent 개발/배포 Pipeline 및 Registry/Skill 표준 가이드
- PIIA 보고서 초안 Agent
- 투자발의 Agent 및 발의서 템플릿
- 사업관리 리서치/법인 이력관리 모듈
- Custom UI/운영 대시보드
- 평가 하네스 및 품질 리포트
- 통합테스트 결과서, 운영 매뉴얼, 장애/재처리 절차서

12월 UAT/운영전환 산출물:
- UAT 시나리오 및 결과서
- 결함 조치 내역
- 사용자 교육자료
- 운영 인수인계서
- 최종 결과보고서 및 서비스 전환 승인자료


## 15. 월별 추진 로드맵

| 월 | 추진 목표 | 주요 완료 기준 |
|---|---|---|
| 6월 | 착수, 환경 구성, 문서 적재/검색 기반 구축 | GE/GCP 환경, 대상문서/권한 확정, RAG/Prompt Assist 기본 구조 |
| 7월 | 1차 핵심 기능 구현 | 과거문서 검색, Prompt Assist v1, PIIA/사업관리 MVP 동작 |
| 8월 | 1차 안정화 및 고도화 backlog 확정 | 검색품질/권한/사용성 검증, 2차 상세 backlog 승인 |
| 9월 | 2차 Agent 확장 착수 | Agent Pipeline/Registry, PIIA 보고서 초안, 투자발의 설계/초기구현 |
| 10월 | 이력관리/UI/평가 고도화 | 사업관리 이력, 법인 이력, 평가 하네스, UI/UX 개선 |
| 11월 | 구축 완료 및 통합 검수 | 통합테스트, 보안/권한 회귀, 운영 매뉴얼, 인수 기준 완료 |
| 12월 | 사용자 테스트 및 운영 전환 | UAT 완료, 결함 보완, 교육/인수인계, 최종보고 |


## 16. 성공 기준 및 인수 기준

본 과제의 성공 기준은 기능 구현 완료가 아니라 현업 사용자가 신뢰하고 반복 사용할 수 있는 업무형 AI Agent 서비스의 안정적 전환이다.

인수 기준:
- 사용자별 권한에 맞는 문서만 검색/preview된다.
- 주요 업무 질의에 대해 근거 문서, page, citation이 제공된다.
- Prompt Assist가 모호한 질문을 업무 템플릿 기반으로 보정한다.
- PIIA Agent가 투자계획서의 누락 항목, 리스크, 대응방향을 일관된 형식으로 도출한다.
- 투자발의 Agent가 심의 결과를 발의서 초안으로 연결한다.
- 사업관리 Agent가 출처 기반 Deep Research 결과와 이력관리를 제공한다.
- 운영자는 문서 적재, 오류, 검색 품질, Agent 사용량, 비용, 권한 이슈를 모니터링할 수 있다.
- 12월 UAT에서 핵심 시나리오 기준 사용자 승인과 운영 전환 승인을 획득한다.


## 17. 결론 및 제언

POSCO 경영기획 DX AI 과제는 GE를 기반으로 단기간에 업무형 AI Agent 경험을 제공하면서, 향후 POSCO 내부 Agentic Workflow 운영모델로 확장할 수 있는 중요한 기준 프로젝트다. 본 수행계획은 첨부 문서의 기능 범위와 일정 구조를 유지하면서도, 최신 Gemini Enterprise Agent Platform의 App/Data Store/Agent Flow/Skill/Action/평가·거버넌스 체계를 최대한 활용하도록 재정리하였다.

프로젝트 성공을 위해서는 6~8월 1차 구축에서 검색·근거·권한·기본 Agent의 신뢰도를 조기 확보하고, 9~11월 2차 구축에서 Agent 확장, 이력관리, 평가 하네스, 운영 대시보드를 완성해야 한다. 12월은 신규 기능 개발이 아니라 사용자 테스트와 운영 전환 검증에 집중함으로써, 서비스 오픈 품질과 현업 수용성을 동시에 확보하는 것이 바람직하다.


## 참조 근거

- 첨부 문서: `/opt/data/cache/documents/doc_83c1e4be3eed_포스코DX_수행계획서_260526.docx`
- POSCO 경영기획DX 작업계획서/추진계획서 v1: 6~12월 전체 일정, 1차/2차 통합 추진, 과거문서 검색, PIIA, 투자발의, 사업관리 AI, 22MM 투입 구조
- POSCO GE 아키텍처 논의 메모: 사업수행계획서에 데이터스토어 사이징, Agentic Search Agent, 메타정보 연계, expectation gap bridge 필요사항 포함 요청
- GBrain 프로젝트 컨텍스트: GE 라이선스/계정/GCP 프로젝트/Vertex AI 테스트, Megazone/Google PSO R&R, Technical Sync/품질검토 구조
- LLM Wiki: POSCO AI Agent Platform, Gemini Enterprise Agent Platform, 운영/거버넌스/observability/Agent Platform 확장 관점
- 기존 산출물: `POSCO_Gemini_Enterprise_AI_Task_Implementation_Plan_260428.md`
