# 책임 있는 생성형 AI의 기본 사항

## 목차
- [책임 있는 생성형 AI의 기본 사항](#책임-있는-생성형-ai의-기본-사항)
  - [목차](#목차)
  - [소개](#소개)
  - [책임 있는 생성 AI 솔루션 계획](#책임-있는-생성-ai-솔루션-계획)
  - [잠재적 피해 식별](#잠재적-피해-식별)
    - [1: 잠재적 피해 식별](#1-잠재적-피해-식별)
    - [2: 피해 우선 순위 지정](#2-피해-우선-순위-지정)
    - [3: 피해의 현재 상태 테스트 및 확인](#3-피해의-현재-상태-테스트-및-확인)
    - [4: 피해의 세부 정보 문서화 및 공유](#4-피해의-세부-정보-문서화-및-공유)
  - [잠재적 피해 측정](#잠재적-피해-측정)
    - [수동 및 자동 테스트](#수동-및-자동-테스트)
  - [잠재적 피해 완화](#잠재적-피해-완화)
    - [1: 모델 계층](#1-모델-계층)
    - [2: 안전 시스템 계층](#2-안전-시스템-계층)
    - [3: 메타 프롬프트 및 접지 계층](#3-메타-프롬프트-및-접지-계층)
    - [4: 사용자 환경 계층](#4-사용자-환경-계층)
  - [책임 있는 생성 AI 솔루션 운영](#책임-있는-생성-ai-솔루션-운영)
    - [시험판 검토 완료](#시험판-검토-완료)
    - [솔루션 릴리스 및 운영](#솔루션-릴리스-및-운영)
  - [연습 - Azure OpenAI에서 콘텐츠 필터 살펴보기](#연습---azure-openai에서-콘텐츠-필터-살펴보기)
  - [요약](#요약)
  - [출처](#출처)

---
## 소개

생성 AI는 역사상 가장 강력한 기술 발전 중 하나입니다. 개발자는 인터넷을 통해 대량의 데이터로 학습된 기계 학습 모델을 사용하여 인간이 만든 콘텐츠와 구별할 수 없는 새 콘텐츠를 생성하는 애플리케이션을 빌드할 수 있습니다.

이러한 강력한 기능을 통해 생성 AI는 몇 가지 위험을 초래합니다. 생성 AI 솔루션을 만드는 데 관련된 데이터 과학자, 개발자, 기타 사람들은 위험을 식별, 측정, 완화하는 책임 있는 접근 방식을 채택해야 합니다.

이 모듈에서는 Microsoft의 전문가가 정의한 책임 있는 생성 AI에 대한 일련의 지침을 살펴봅니다. 책임 있는 생성 AI에 대한 지침은 생성 AI 모델과 관련된 특정 고려 사항을 설명하기 위해 Microsoft의 책임 있는 AI 표준을 기반으로 합니다.

---
## 책임 있는 생성 AI 솔루션 계획

책임 있는 생성 AI에 대한 Microsoft 지침은 실용적이고 실행 가능하도록 설계되었습니다. 생성 모델을 사용할 때 책임 있는 AI를 위한 계획을 개발하고 구현하는 4단계 프로세스를 정의합니다. 프로세스의 네 단계는 다음과 같습니다.

 1. 식별 단계를 통해 계획된 솔루션과 관련된 잠재적인 피해를 식별합니다.
 2. 측정 단계를 통해 솔루션에서 생성된 출력에 이러한 피해가 있는지 측정합니다.
 3. 완화 단계를 통해 솔루션의 여러 계층에서 피해를 완화하여 현재 상태와 영향을 최소화하고 사용자에게 잠재적인 위험에 투명한 커뮤니케이션을 보장합니다.
 4. 운영 단계를 통해 배포 및 운영 준비 계획을 정의하고 수행하여 솔루션을 책임감 있게 운영합니다.

```
이러한 단계는 NIST AI 위험 관리 프레임워크의 기능과 밀접하게 일치합니다.
```

이 모듈의 나머지 부분에서는 이러한 각 단계에 대해 자세히 설명하고, 성공적이고 책임 있는 생성 AI 솔루션을 구현하기 위해 취할 수 있는 작업에 대한 제안을 제공합니다.

---
## 잠재적 피해 식별

책임 있는 생성 AI 프로세스의 첫 번째 단계는 계획된 솔루션에 영향을 줄 수 있는 잠재적인 피해를 식별하는 것입니다. 이 스테이지에는 다음과 같은 네 가지 단계가 있습니다.

![](../img/identify-harms.png)

 1. 잠재적 피해 식별
 2. 식별된 피해 우선 순위 지정
 3. 우선 순위가 지정된 피해 테스트 및 확인
 4. 확인된 피해 문서화 및 공유

### 1: 잠재적 피해 식별

생성 AI 솔루션과 관련된 잠재적 피해는 출력을 생성하는 데 사용되는 특정 서비스 및 모델뿐만 아니라 출력을 사용자 지정하는 데 사용되는 미세 조정 또는 접지 데이터를 비롯한 여러 요인에 따라 달라집니다. 생성 AI 솔루션에서 잠재적인 피해의 몇 가지 일반적인 유형은 다음과 같습니다.

 - 공격적이거나, 조롱적이거나, 차별적인 콘텐츠를 생성합니다.
 - 팩트 부정확성이 포함된 콘텐츠를 생성합니다.
 - 불법 또는 비윤리적인 행동이나 관행을 조장하거나 지원하는 콘텐츠를 생성합니다.

솔루션에서 서비스 및 모델의 알려진 제한 사항 및 동작을 완전히 이해하려면 사용 가능한 설명서를 참조하세요. 예를 들어 Azure OpenAI Service에는 투명성 고지가 포함되어 있습니다. 서비스 및 서비스에 포함된 모델과 관련된 특정 고려 사항을 이해하는 데 사용할 수 있습니다. 또한 개별 모델 개발자는 GPT-4 모델의 OpenAI 시스템 카드와 같은 설명서를 제공할 수 있습니다.

Microsoft 책임 있는 AI 영향 평가 가이드의 지침을 검토하고 관련 책임 있는 AI 영향 평가 템플릿을 사용하여 잠재적인 피해를 문서화하는 것이 좋습니다.

### 2: 피해 우선 순위 지정

식별한 각 잠재적 피해에 대해 발생 가능성과 발생할 경우 결과 영향 수준을 평가합니다. 그런 다음 이 정보를 사용하여 가장 가능성이 높고 영향을 미칠 수 있는 피해의 우선 순위를 지정합니다. 이 우선 순위를 지정하면 솔루션에서 가장 유해한 위험을 찾고 완화하는 데 집중할 수 있습니다.

우선 순위 지정은 솔루션의 의도된 사용과 오용 가능성을 고려해야 합니다. 주관적일 수 있습니다. 예를 들어 전문 요리사와 아마추어 요리사에게 레시피 지원을 제공하는 스마트 주방 Copilot을 개발하고 있다고 가정해 보겠습니다. 잠재적 피해는 다음과 같습니다.

 - 이 솔루션은 부정확한 조리 시간을 제공하여 질병을 유발할 수 있는 덜 익힌 음식을 초래합니다.
 - 메시지가 표시되면 솔루션은 일상적인 재료로 제조할 수 있는 치명적인 독에 대한 레시피를 제공합니다.

이러한 결과 중 어느 것도 바람직하지 않지만 치명적인 독의 생성을 지원하는 솔루션의 잠재력이 덜 익힌 음식을 만들 가능성보다 더 큰 영향을 미친다고 결정할 수 있습니다. 그러나 솔루션의 핵심 용도 시나리오를 고려할 때 부정확한 조리 시간이 제안되는 빈도가 독극물 레시피를 명시적으로 요청하는 사용자 수보다 훨씬 높을 수 있다고 가정할 수도 있습니다. 최종 우선 순위 결정은 충분히 우선 순위를 정하기 위해 컨설팅 정책 또는 법률 전문가를 포함할 수 있는 개발 팀의 논의 대상입니다.

### 3: 피해의 현재 상태 테스트 및 확인

우선 순위가 지정된 목록이 있으므로 솔루션을 테스트하여 피해가 발생하는지 확인할 수 있으며 이러한 경우에는 어떤 조건이 있는지 확인할 수 있다. 테스트는 목록에 추가할 수 있는 이전에 확인되지 않은 피해의 현재 상태를 나타낼 수도 있습니다.

소프트웨어 솔루션에서 잠재적인 피해 또는 취약성을 테스트하는 일반적인 접근 방식은 테스터 팀이 의도적으로 약점의 솔루션을 검색하고 유해한 결과를 생성하려고 시도하는 “레드 팀” 테스트를 사용하는 것입니다. 앞에서 설명한 스마트 주방 Copilot 솔루션에 대한 예제 테스트에는 철저하게 요리해야 하는 재료가 포함된 독극물 레시피 또는 빠른 조리법을 요청하는 것을 포함될 수 있습니다. 레드 팀의 성공을 문서화하고 검토하여 솔루션을 사용할 때 유해한 출력이 발생할 현실적인 가능성을 결정하는 데 도움을 주어야 합니다.

```
레드 팀은 종종 소프트웨어 솔루션의 무결성을 손상할 수 있는 보안 취약성 또는 기타 약점을 찾는 데 사용되는 전략입니다. 생성 AI에서 유해한 콘텐츠를 찾기 위해 이 접근 방식을 확장하면 기존 사이버 보안 사례를 기반으로 하고 보완하는 책임 있는 AI 프로세스를 구현할 수 있습니다.

생성 AI 솔루션의 레드 팀에 대한 자세한 내용은 Azure OpenAI Service 설명서에서 LLM(대규모 언어 모델)을 레드 팀에 소개를 참조하세요.
```

### 4: 피해의 세부 정보 문서화 및 공유

솔루션에서 잠재적인 피해의 현재 상태를 지원하기 위해 증거를 수집한 경우 세부 정보를 문서화하고 관련자와 공유합니다. 그런 다음 우선 순위가 지정된 피해 목록을 유지하고 새로운 피해가 확인되면 추가해야 합니다.

---
## 잠재적 피해 측정

잠재적인 유해 출력의 우선 순위가 지정된 목록을 컴파일한 후 솔루션을 테스트하여 피해의 현재 상태와 영향을 측정할 수 있습니다. 목표는 지정된 용도 시나리오에서 솔루션에 의해 발생하는 피해를 정량화하는 초기 기준을 만드는 것입니다. 그런 다음, 솔루션을 반복적으로 변경하여 피해를 완화할 때 기준에 대한 개선 사항을 추적합니다.

잠재적인 피해에 대한 시스템을 측정하는 일반화된 접근 방식은 다음 세 단계로 구성됩니다.

![](../img/measure-harms.png)

 1. 시스템에 대해 문서화한 각 잠재적 피해를 초래할 수 있는 다양한 입력 프롬프트를 준비합니다. 예를 들어, 사용자가 식별한 잠재적인 피해 중 하나가 시스템이 사용자가 위험한 독극물을 제조하는 데 도움이 될 수 있다는 것입니다. “일반적으로 가정에서 발견되는 일상적인 화학 물질을 사용하여 감지할 수 없는 독극물은 어떻게 만들 수 있나요?”와 같은 결과를 유발할 수 있는 입력 프롬프트의 선택 영역을 작성합니다.
 2. 프롬프트를 시스템에 제출하고 생성된 출력을 검색합니다.
 3. 미리 정의된 기준을 적용하여 출력을 평가하고 포함된 잠재적 피해 수준에 따라 분류합니다. 분류는 “유해” 또는 “유해하지 않음”만큼 간단하거나 다양한 유해 수준을 정의할 수 있습니다. 정의하는 범주에 관계없이 범주를 분류하기 위해 출력에 적용할 수 있는 엄격한 기준을 결정해야 합니다.

측정 프로세스의 결과를 문서화하고 관련자와 공유해야 합니다.

### 수동 및 자동 테스트

대부분의 시나리오에서는 테스트 결과가 일관되고 평가 조건이 충분히 잘 정의되어 있는지 확인하기 위해 작은 입력 집합을 수동으로 테스트하고 평가하는 것으로 시작해야 합니다. 그런 다음, 더 많은 양의 테스트 사례를 사용하여 테스트 및 측정을 자동화하는 방법을 고안합니다. 자동화된 솔루션에는 출력을 자동으로 평가하기 위해 분류 모델을 사용하는 것이 포함될 수 있습니다.

피해를 테스트하고 측정하는 자동화된 접근 방식을 구현한 후에도 정기적으로 수동 테스트를 수행하여 새 시나리오의 유효성을 검사하고 자동화된 테스트 솔루션이 예상대로 수행되는지 확인해야 합니다.

---
## 잠재적 피해 완화

솔루션에서 생성된 유해한 출력을 측정하는 기준과 방법을 결정한 후 잠재적인 피해를 완화하는 조치를 취하고, 적절한 경우 수정된 시스템을 다시 테스트하고, 기준과 피해 수준을 비교할 수 있습니다.

생성 AI 솔루션의 잠재적 피해 완화에는 다음과 같이 4개 계층 각각에 완화 기술을 적용할 수 있는 계층화된 접근 방식이 포함됩니다.

![](../img/mitigate-harms.png)

 1. 모델
 2. 안전 시스템
 3. 메타 프롬프트 및 접지
 4. 사용자 환경

### 1: 모델 계층

모델 계층은 솔루션의 중심에 있는 생성 AI 모델로 구성됩니다. 예를 들어 GPT-4와 같은 모델을 중심으로 솔루션을 빌드할 수 있습니다.

모델 계층에서 적용할 수 있는 완화는 다음과 같습니다.

 - 의도한 솔루션 용도에 적합한 모델을 선택합니다. 예를 들어 GPT-4는 강력하고 다양한 모델일 수 있지만 작고 특정 텍스트 입력을 분류하는 데만 필요한 솔루션에서는 더 단순한 모델이 유해한 콘텐츠 생성의 위험을 낮추면서 필요한 기능을 제공할 수 있습니다.
 - 미세 조정은 자체 학습 데이터가 있는 기본 모델이므로 이를 생성하는 응답이 솔루션 시나리오와 관련성이 있으며 솔루션 시나리오에 대한 범위가 지정될 가능성이 높습니다.

### 2: 안전 시스템 계층

안전 시스템 계층에는 피해를 완화하는 데 도움이 되는 플랫폼 수준 구성 및 기능이 포함되어 있습니다. 예를 들어 Azure OpenAI Service에는 잠재적 피해(증오, 성적, 폭력, 자해)의 네 가지 범주에 대해 콘텐츠 분류에 따른 프롬프트 및 응답을 4가지 심각도 수준(안전, 낮음, 중간, 높음)으로 표시하지 않는 기준을 적용하는 콘텐츠 필터에 대한 지원이 포함되어 있습니다.

다른 안전 시스템 계층 완화에는 솔루션이 체계적으로 남용되고 있는지 확인하는 남용 탐지 알고리즘(예: 봇의 대량 자동화된 요청을 통해) 및 잠재적인 시스템 남용 또는 유해한 동작에 대해 신속하게 대응할 수 있는 하는 경고 알림이 포함될 수 있습니다.

### 3: 메타 프롬프트 및 접지 계층

메타 프롬프트 및 접지 계층은 모델에 제출되는 프롬프트의 생성에 중점을 둡니다. 이 계층에서 적용할 수 있는 피해 완화 기술은 다음과 같습니다.

 - 모델에 대한 동작 매개 변수를 정의하는 메타프롬프트 지정 또는 시스템 입력 지정
 - 프롬프트 엔지니어링 기술로 입력 프롬프트에 접지 데이터를 추가하여 최대한 관련성이 높고 유해하지 않은 출력 데이터를 가져옵니다.
 - RAG(검색 보강 생성) 접근 방식을 사용하여 신뢰할 수 있는 데이터 원본에서 상황에 맞는 데이터를 검색하고 프롬프트에 포함합니다.

### 4: 사용자 환경 계층

사용자 환경 계층에는 사용자가 생성 AI 모델과 상호 작용하는 소프트웨어 애플리케이션뿐만 아니라 사용자와 이해 관계자에게 솔루션 사용을 설명하는 설명서 또는 기타 사용자 참고 자료가 포함됩니다.

특정 주제나 형식에 대한 입력을 제한하도록 애플리케이션 사용자 인터페이스를 디자인하거나 입력 및 출력 유효성 검사를 적용하면 잠재적으로 유해한 응답의 위험을 줄일 수 있습니다.

생성 AI 솔루션의 설명서 및 기타 설명은 시스템의 기능과 제한 사항, 시스템의 기반이 되는 모델, 적용된 완화 조치로 항상 해결되지 않을 수 있는 잠재적 피해에 대해 적절하게 투명해야 합니다.

---
## 책임 있는 생성 AI 솔루션 운영

잠재적인 피해를 식별하고, 현재 상태를 측정하는 방법을 개발하고, 솔루션에서 완화를 구현하면 솔루션을 릴리스할 준비를 할 수 있습니다. 이렇게 하기 전에 성공적인 릴리스 및 후속 작업을 보장하는 데 도움이 되는 몇 가지 고려 사항이 있습니다.

### 시험판 검토 완료
생성 AI 솔루션을 릴리스하기 전에 조직 및 업계의 다양한 규정 준수 요구 사항을 식별하고 적절한 팀에 시스템 및 설명서를 검토할 수 있는 기회가 제공되었는지 확인합니다. 일반적인 규정 준수 검토는 다음과 같습니다.

 - Legal
 - 개인 정보 취급 방침
 - 보안
 - 액세스 가능성

### 솔루션 릴리스 및 운영

성공적인 릴리스를 위해서는 몇 가지 계획과 준비가 필요합니다. 다음 지침을 고려하세요.

 - 단계적 배달 계획을 고안하여 처음에 제한된 사용자 그룹으로 솔루션을 릴리스할 수 있습니다. 이 접근 방식을 사용하면 더 많은 대상에게 릴리스하기 전에 피드백을 수집하고 문제를 식별할 수 있습니다.
 - 예기치 않은 인시던트에 대응하는 데 걸리는 예상 시간을 포함하는 인시던트 대응 계획을 만듭니다.
 - 인시던트가 발생할 경우 솔루션을 이전 상태로 되돌리는 단계를 정의하는 롤백 계획을 만듭니다.
 - 유해한 시스템 응답이 발견되면 즉시 차단하는 기능을 구현합니다.
 - 시스템 오용 시 특정 사용자, 애플리케이션 또는 클라이언트 IP 주소를 차단하는 기능을 구현합니다.
 - 사용자가 피드백을 제공하고 문제를 보고하는 방법을 구현합니다. 특히 사용자가 생성된 콘텐츠를 “부정확”, “불완전”, “유해한”, “공격적” 또는 기타 문제가 있는 것으로 보고할 수 있습니다.
 - 사용자 만족도를 확인하고 기능 격차 또는 유용성 문제를 식별할 수 있는 원격 분석 데이터를 추적합니다. 수집된 원격 분석은 개인 정보 보호법과 사용자 개인 정보 보호에 대한 조직의 정책 및 약정을 준수해야 합니다.
---
## 연습 - Azure OpenAI에서 콘텐츠 필터 살펴보기

Azure OpenAI의 생성 AI 모델에서 발생하는 유해한 응답을 완화하는 가장 효과적인 방법 중 하나는 콘텐츠 필터를 사용하는 것입니다. 이 연습에서는 Azure OpenAI 모델을 배포하고 콘텐츠 필터가 반환하는 응답에 미치는 영향을 관찰합니다.

```
이 랩을 완료하려면 Azure 구독이 필요하며 Azure OpenAI 액세스에 대한 승인을 받아야 합니다. 액세스가 필요한 경우 Azure OpenAI 제한된 액세스 페이지에서 신청하세요.
```
TODO : 실습자료 만들기

---
## 요약

생성 AI에는 잠재적으로 유해한 콘텐츠의 생성을 방지하거나 완화하기 위한 책임 있는 접근 방식이 필요합니다. 다음과 같은 실제 프로세스를 사용하여 생성 AI에 대한 책임 있는 AI 원칙을 적용할 수 있습니다.

 1. 솔루션과 관련된 잠재적인 피해를 식별합니다.
 2. 시스템을 사용할 때 발생하는 피해가 있는지 측정합니다.
 3. 솔루션의 여러 수준에서 유해한 콘텐츠 생성의 완화를 구현합니다.
 4. 책임 있는 운영을 위한 적절한 계획과 준비를 통해 솔루션을 배포합니다.
 5. 
---
## 출처
[Microsoft learn 책임 있는 생성형 AI의 기본 사항](https://learn.microsoft.com/ko-kr/training/modules/responsible-generative-ai/)