
# Amazon Bedrock을 활용한 MES(제조 실행 시스템)용 챗봇

현대 제조업 환경에서 데이터 기반 의사결정은 매우 중요해졌습니다. Industry 4.0의 등장으로 제조 시설은 센서, 기계, ERP 시스템 등 다양한 소스에서 방대한 양의 데이터가 쏟아지고 있습니다.
생성형 AI 기술은 사용자와 방대한 양의 텍스트 데이터 사이의 간극을 좁히는데 큰 진전을 이루었습니다. 하지만 주로 텍스트 기반 정보에만 초점을 맞추어 복잡한 산업 시스템의 운영 데이터에 접근하고 해석하는데는 여전히 간극이 있습니다. 
이러한 AI 기능을 운영 데이터 플랫폼에 직접 연결되는 자연어 인터페이스와 통합하면 이 프로세스를 단순화할 수 있습니다. 이를 통해 모든 사용자가 깊은 기술적 전문 지식 없이도 중요한 의사결정에 필요한 실시간 데이터에 쉽게 접근할 수 있게 합니다.


다음은 이 샘플을 코드로 배포할 수 있는 코드입니다

## 0. 사전 요구사항

이 코드 샘플은 Amazon Bedrock의 Anthropic Claude 모델을 활용합니다. 모델 접근을 활성화하려면 [Model access](https://docs.aws.amazon.com/bedrock/latest/userguide/model-access.html)를 참조하세요. 
작은 스키마의 경우 Claude 3 Haiku가 권장되며, 더 크고 복잡한 스키마의 경우 Claude 3.5 Sonnet을 사용하세요. Claude 3 Haiku는 추론 지연 시간을 개선하고 비용을 최소화하지만, Claude 3.5 Sonnet은 더 나은 추론 능력을 가지고 있습니다.

## 1. 환경 설정

다음은 python3 설치가 필요합니다.

```bash
python3 -m venv .venv
```
init 프로세스가 완료되고 가상환경이 생성되면 다음 단계를 사용하여 가상환경을 활성화할 수 있습니다.

```bash
source .venv/bin/activate
```

```bash
AWS_REGION="YourRegion" #example us-west-2 
AWS_PROFILE="myprofile" #from ~/.aws/config
```

### 1.2 Github Repository clone
데모 실행을 위한 코드 다운로드:

```bash
git clone https://github.com/AWS-Janghwan/MES-Chatbot.git
```

### 1.3 필요한 패키지 설치
필요한 패키지를 설치하려면 다음 명령을 실행하세요:

```bash
cd MES-Chatbot
pip install -r requirements.txt
```

## 2. 가상 시뮬레이션 MES Dataset 생성
이 리포지토리에는 원자재에서 완제품까지의 생산 프로세스를 관리하고 모니터링하는 기본적인 제조실행시스템(MES)을 시뮬레이션하는 스크립트가 포함되어 있습니다. 데이터베이스 구조는 제품, 기계, 작업 지시서, 재고 수준, 품질 관리 및 직원 세부 정보를 추적하도록 설계되었습니다.
데이터베이스 테이블을 생성하고 합성 데이터로 채우려면 프로젝트 루트 디렉토리에서 다음을 실행하세요.

```bash
# 테이블 생성 및 시뮬레이션 데이터
python3 MES-synthetic-data/sqlite-synthetic-mes-data.py
```


## 3. MES Chatbot 실행

```bash
streamlit run ./chatbot/Chat.py
```

