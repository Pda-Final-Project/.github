

![image](https://github.com/user-attachments/assets/c666c6d2-69d2-4980-a691-cb583c8bc1f9)

# [FinPago - 해외 공시 기반 트레이딩 시스템](http://finpago-bucket.s3-website.ap-northeast-2.amazonaws.com/)

## 📌 프로젝트 개요

FinPago는 **미국 SEC(증권거래위원회) EDGAR 공시 데이터**를 활용하여 해외 주식 투자자들이 빠르고 정확한 공시 정보를 확인하고, 실시간으로 트레이딩을 할 수 있도록 지원하는 플랫폼입니다.

## 🚀 주요 기능

![image](https://github.com/user-attachments/assets/32ce3e7c-0f1a-49ed-afab-93b0cb0b0383)
![image](https://github.com/user-attachments/assets/c1142bd2-e7b1-4932-9365-66cdb96d5cb0)

### 📑 **공시 데이터 제공**
- SEC EDGAR 공시 API를 활용하여 실시간 공시 제공
- 해외 공시 번역 및 요약 기능 지원 (ChatGPT, Google Translate 활용)
- 주요 공시 유형(10-K, 10-Q, 8-K 등)별 요약 및 분석 제공
- 공시별 주요 재무 정보 비교 및 시각화

![image](https://github.com/user-attachments/assets/f0f2a13a-883f-44f9-868b-a147b61be683)
![image](https://github.com/user-attachments/assets/490de015-05d1-4de3-a89c-912a956dbc2c)


### 📊 **실시간 트레이딩**
- 해외 주식 실시간 체결 정보 제공
- 주문 유형(시장가, 지정가, 단일가) 지원
- 체결된 주문 내역 및 매매 손익 분석
- **Redis Pub/Sub + SSE**를 이용한 실시간 체결 정보 반영

![image](https://github.com/user-attachments/assets/f7532d57-fe4a-4e59-9994-3559fb068bfb)


### 📅 **어닝콜 일정 및 분석**
- 어닝콜(실적 발표) 일정 제공 및 기업 로고 표시
- 어닝콜 분석 데이터 및 요약 제공
- EPS 및 매출 변동 추이 그래프 시각화
- **실적 발표 캘린더** 기능 구현
![image](https://github.com/user-attachments/assets/cce9280a-0851-4e70-9f07-a9af09bc14f5)
![image](https://github.com/user-attachments/assets/01031e8d-e133-4835-b851-a60b6f9f125b)

### 💰 **My계좌 관리**
- 보유 종목 평가금액 및 매매 손익 분석
- 실시간 환율 적용하여 원화/외화 변환
- 해외 주식 결제 방식(D+1, D+2) 적용
- 예수금, 사용 가능 예수금 분리 관리
![image](https://github.com/user-attachments/assets/a853ae6f-192a-450e-92cc-c715448b3966)

### Others

![image](https://github.com/user-attachments/assets/e3a1d786-d697-4402-b593-aad3b1171495)
![image](https://github.com/user-attachments/assets/6af1b099-d362-4355-ba25-df2945c7bbd5)


## 🔧 **아키텍처 및 사용 기술**

### 🔹 **프론트엔드**
- React, JavaScript, Tailwind CSS
- SSE(Server-Sent Events)를 이용한 실시간 데이터 반영
- **recharts**를 이용한 EPS 및 매출 변동률 시각화

### 🔹 **백엔드**
- Spring Boot, Java, Spring Data JPA, MySQL
- Kafka를 이용한 비동기 트레이딩 메시징 시스템
- Redis를 활용한 캐싱 및 Pub/Sub 실시간 데이터 처리
- SEC EDGAR API, 한국투자증권 API, Google Translate API 연동

### 🔹 **인프라 및 배포**
- AWS Cloud, Kubernetes, MySQL Operator, Redis Cluster
- Jenkins, ArgoCD, GitHub Actions을 활용한 **CI/CD 자동화**
- AWS ALB 및 API Gateway를 통한 로드밸런싱
![image](https://github.com/user-attachments/assets/fbc8fa20-c019-4f0e-a202-7d9ec36a77aa)

## ERD

![image](https://github.com/user-attachments/assets/06a3e749-faf8-483e-8f1d-8beb53d4cf17)

## 데이터 수집 원천 및 수집 방법
![image](https://github.com/user-attachments/assets/08401760-b0f6-493c-851d-2d74ee13d174)


## 🛠 **트러블슈팅 사례**

### 1️⃣ **Kafka 기반 트레이딩 시스템 최적화**
- 주문 생성, 매칭, 체결, 정산 등 단계별 토픽 분리하여 이벤트 기반 설계
- 실패 처리(Failure Topic) 및 알림 시스템 분리 (Filling Notice, General Notice)
- 체결 테이블을 **BuyTradeExecution, SellTradeExecution** 으로 정규화하여 데이터 확장성 확보
![image](https://github.com/user-attachments/assets/9719dce4-2454-4e36-8b91-bc89c4b5c4c0)
![image](https://github.com/user-attachments/assets/b6632f3e-3d04-4557-a6f8-3d8e2cefdcd7)

### 2️⃣ **실시간 체결 데이터 반영**
- 외부 체결 데이터(증권사 API) + 내부 체결 데이터(매칭 엔진) Redis 리스트에 저장
- **Redis Pub/Sub + SSE(Server-Sent Events)** 를 이용하여 실시간 반영

![image](https://github.com/user-attachments/assets/24918d4a-69e4-4674-99ed-f94fea01e4a3)

![image](https://github.com/user-attachments/assets/a39f4357-9443-49bd-af29-ea26578ff6c7)

![image](https://github.com/user-attachments/assets/cfefb651-fd8c-4602-bc25-27c6cb8ee42d)

![image](https://github.com/user-attachments/assets/698c6db7-0d0b-4a33-a86b-63fd1bc085ab)

![image](https://github.com/user-attachments/assets/f9bbff02-20cc-4179-acea-58510987b464)

![image](https://github.com/user-attachments/assets/96a51762-071a-4baa-8735-d059a838b91e)

![image](https://github.com/user-attachments/assets/179bc004-b4c1-425d-9b0d-62399a4ed79b)

### 3️⃣ **MySQL Operator 기반 InnoDB Cluster 구성**
- EBS 기반 PersistentVolume 설정 문제 해결
- 특정 노드에 데이터베이스 인스턴스를 배치하는 **Affinity & NodeSelector** 적용
![image](https://github.com/user-attachments/assets/471d3e5c-9537-4795-ac00-2ee1c109d5b2)

### 4️⃣ **CORS 중복 헤더 문제 해결**
- Spring Gateway에서 중복된 CORS 헤더가 응답에 포함되는 문제 발생
- `DedupeResponseHeader` 설정을 통해 중복 헤더 제거
![image](https://github.com/user-attachments/assets/583a42a4-0582-42bc-9e1e-7dd701c7a60f)

### 5️⃣ **10-Q 공시(140페이지) 번역 성능 개선**
- Google Translate API는 속도가 느리고 HTML 태그 번역 문제 발생
- **멀티스레딩 적용하여 번역 속도 10배 향상** (10분 → 1분)
- HTML 태그 제거 후 문단 단위 번역하여 번역 품질 개선
![image](https://github.com/user-attachments/assets/3845b168-2133-40fe-8879-15a26b153720)

## 🔮 **향후 고도화 계획**
- **소수점 거래 지원**
- **ETF 및 레버리지 종목 추가**
- **어닝콜 스크립트 및 요약 자동화**
- **공시 유형 확장 (EDGAR API 활용 극대화)**
- **트레이딩 시스템 UI 개선 및 모바일 대응**

## 👥 **팀원 소개**
| 역할 | 이름 |
|------|------|
| 🏆 PM | 양일교 |
| 👨‍💻 CTO | 김동재 |
| 🚀 백엔드 리더 | 김민승 |
| 🎨 프론트엔드 리더 | 곽성은 |
| ☁️ 인프라 리더 | 함건욱 |

---

FinPago는 **공시 데이터와 트레이딩 시스템을 결합한 혁신적인 금융 플랫폼**으로, 투자자들에게 더욱 신속하고 정확한 정보를 제공하는 것을 목표로 합니다.  
감사합니다! 🎉

📅 **프로젝트 기간**: 2025.03.17  
