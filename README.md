# ai project (04.16~04.18)

### - 문장 임베딩 기술을 사용한 유사 판례 검색 시스템

FastAPI를 사용하여 개발된 법률 판례 검색 및 조회 서비스입니다.  
주요 기능은 사용자가 입력한 문장과 유사한 판례를 찾아내는 것과 특정 판례의 상세 정보를 조회하는 기능입니다.  
문장 임베딩 모델과 코사인 유사도가 활용되었습니다.

## 주요 구성 요소:

### FastAPI:

비동기 프로그래밍을 지원하는 modern, fast(고성능) web framework로, 본 프로그램의 핵심 서버 구축에 사용됩니다.

### SentenceTransformer:

문장 임베딩을 생성하기 위해 사용되는 라이브러리로, 'jhgan/ko-sroberta-multitask' 모델을 사용하여 한국어 문장의 벡터 표현을 생성합니다.

### NumPy 및 PyTorch:

벡터 연산과 텐서 연산을 위해 사용됩니다. 특히, PyTorch의 코사인 유사도 계산 기능을 통해 입력 문장과 데이터베이스 내 문장 간의 유사도를 계산합니다.

### Pandas:

데이터 처리를 위해 사용되며, 특히 판례 데이터를 쉽게 조작하고 관리하기 위해 사용됩니다.

## 주요 기능:

### 판례 검색:

사용자가 입력한 문장과 유사한 판례의 제목을 찾아내는 기능입니다.  
사용자의 입력을 임베딩하고,데이터베이스 내에 저장된 판례 제목의 임베딩과 비교하여 상위 5개의 가장 유사한 판례를 반환합니다.

### 판례 상세 조회:

사용자가 특정 판례의 등록번호를 입력하면, 해당 판례에 대한 상세 정보(제목, 사건 번호, 내용 등)를 반환합니다.

### 판례 목록 조회:

데이터베이스에 저장된 모든 판례의 기본 정보를 조회하는 기능입니다.

### 작동 원리:

사용자는 웹 인터페이스 또는 API를 통해 문장을 입력합니다.  
입력된 문장은 SentenceTransformer를 사용하여 벡터로 변환됩니다.  
변환된 벡터는 데이터베이스에 저장된 판례 제목의 임베딩과 비교됩니다. 이때 코사인 유사도를 계산하여 유사도가 높은 상위 5개의 판례를 선정합니다.  
선택된 판례의 제목과 유사도 점수를 사용자에게 반환합니다.  
사용자는 특정 판례의 상세 정보를 조회할 수 있으며, 등록번호를 통해 직접 조회할 수 있습니다.

## 기술적 특징:

### Async/Await 패턴:

FastAPI의 비동기 기능을 활용하여, 데이터베이스 조회와 외부 API 호출 시 발생하는 대기 시간을 최소화합니다.

### 문장 임베딩과 코사인 유사도 계산:

최신 NLP 기술을 활용하여 문장 간의 유사도를 정량적으로 평가합니다. 이를 통해 매우 빠르고 정확하게 관련 판례를 찾을 수 있습니다.

### RESTful API 디자인:

FastAPI를 사용하여 REST 규칙에 따른 API를 설계하고 구현함으로써, 사용자는 HTTP 메소드(GET, POST 등)를 통해 손쉽게 데이터를 조회하거나 전송할 수 있습니다.  
이를 통해 프론트엔드 개발자가 백엔드 서비스와 효율적으로 통신할 수 있는 환경을 마련합니다.

## 사용 예시:

### 판례 검색 기능 사용 예시:

- 사용자가 "부동산 계약 파기"라는 문장을 입력합니다.
- 입력된 문장은 모델을 통해 임베딩으로 변환됩니다.
- 변환된 임베딩과 데이터베이스 내 판례 제목의 임베딩들과의 코사인 유사도를 계산합니다.
- 가장 유사도가 높은 상위 5개의 판례를 사용자에게 제공합니다.

### 판례 상세 조회 기능 사용 예시:

- 사용자가 특정 판례의 등록번호, 예를 들어 "12345"를 입력합니다.
- 시스템은 데이터베이스에서 해당 등록번호를 가진 판례를 조회합니다.  
  = 해당 판례의 상세 정보(제목, 사건 번호, 내용, 유사 판례, 링크 등)를 사용자에게 반환합니다.

### 판례 목록 조회 기능 사용 예시:

- 사용자가 판례 목록 조회 요청을 합니다.
- 시스템은 데이터베이스에 저장된 모든 판례의 기본 정보를 조회합니다.
- 조회된 정보를 바탕으로 사용자에게 판례의 목록을 제공합니다.

## Mysql과 Amazon Lightsail

관계형 데이터베이스 관리 시스템(RDBMS)인 MySQL과 가상 서버, 스토리지, 데이터베이스 및 네트워킹 기능을 간편하게 제공하는 클라우드 플랫폼인 Amazon Lightsail을 결합하여 시스템을 구현합니다.
대규모 데이터를 효율적으로 관리하고 안정적으로 운영할 수 있는 기능을 제공하며, 애플리케이션의 배포와 관리가 용이해집니다.

## MySQL의 사용:

### 데이터 저장:

판례 데이터를 저장하기 위해 MySQL 데이터베이스를 사용합니다. 판례의 제목, 내용, 사건 번호, 유사 판례 정보 등이 포함됩니다.

### 쿼리 처리:

사용자의 요청에 따라 특정 조건에 맞는 데이터를 검색하고 추출하는 데 SQL 쿼리를 사용합니다.  
판례 검색 및 상세 조회 기능에 핵심적인 역할을 합니다.

## Amazon Lightsail의 사용:

### 서버 호스팅:

FastAPI 기반의 웹 서버를 Amazon Lightsail의 인스턴스에 배포하여 운영합니다. Lightsail은 쉽게 관리하고 접근할 수 있는 가상 서버를 제공하기 때문에, 서버 관리보다는 애플리케이션 개발에 더 집중할 수 있는 개발자 친화적인 환경을 구성할 수 있습니다.

### 데이터베이스 관리:

MySQL 데이터베이스를 안정적으로 운영하고, 백업 및 복구, 확장과 같은 관리 작업을 손쉽게 수행할 수 있습니다.

### 네트워킹:

DNS 관리와 정적 IP 할당 기능을 제공합니다. 이는 웹 서비스의 주소를 쉽게 관리하고, 안정적인 서비스 접근성을 보장하는 데 도움이 됩니다.

## MySQL과 Amazon Lightsail을 활용한 시스템 아키텍처:

### 웹 서버:

FastAPI를 사용하여 구축된 웹 서버는 Amazon Lightsail 인스턴스에서 실행됩니다. 이 서버는 사용자의 요청을 처리하고 응답을 반환하는 역할을 합니다.

### 데이터베이스:

판례 데이터는 MySQL 데이터베이스에 저장되며, 이 데이터베이스는 Lightsail의 관리형 데이터베이스 서비스를 통해 운영됩니다.  
데이터베이스와 웹 서버 간의 통신은 안전하고 빠르게 이루어집니다.

### 애플리케이션 로직:

사용자의 입력을 처리하고, 데이터베이스에서 필요한 정보를 검색하며, 문장 임베딩과 유사도 계산 등의 작업을 수행하는 로직은 웹 서버에서 실행됩니다.

---

## 사용 예시

법률 전문가들에게 매우 유용한 도구가 될 수 있습니다.  
특히, 대량의 판례 정보 중에서 특정 사안과 관련된 판례를 빠르게 찾아낼 수 있다는 점에서 가치가 있습니다.  
판례의 상세 정보 조회 기능은 특정 판례에 대한 심층적인 이해를 가능하게 하며, 이는 법률 연구나 소송 준비 과정에서 큰 도움이 될 것입니다.

추후 이 시스템은 더 많은 데이터와 고도화된 알고리즘을 통해 더욱 정교하고 포괄적인 검색 결과를 제공할 수 있을 것으로 기대됩니다.
