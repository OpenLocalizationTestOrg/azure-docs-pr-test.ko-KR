---
title: "aaaApproach 및 Azure Data Catalog를 채택 프로세스 | Microsoft Docs"
description: "이 문서에서는 비전 정의, 주요 비즈니스 사용 사례 식별, 파일럿 프로젝트 선택을 비롯한 Azure Data Catalog 도입을 고려하는 조직에 대한 접근 방식 및 프로세스를 제공합니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 0c771e7a-6fcd-417f-9247-897177719567
ms.service: data-catalog
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 06/15/2017
ms.author: maroche
ms.openlocfilehash: ffa6993b63c8a6066f48727fb046d0334a6df541
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="approach-and-process-for-adopting-azure-data-catalog"></a>Azure Data Catalog 채택을 위한 접근 방식 및 프로세스
이 문서는 조직에서 **Azure Data Catalog** 도입을 시작하는 데 도움이 됩니다. toosuccessfully 채택 **Azure Data Catalog**, 세 가지 주요 항목에 집중: 비전을 정의 조직 내의 주요 비즈니스 사용 사례를 식별 하 고 파일럿 프로젝트를 선택 합니다.

## <a name="introducing-hello-azure-data-catalog"></a>Hello Azure Data Catalog를 소개합니다.
작업의 hello world, 내 사람들의 기대 어떻게 되어야 할 수 toofind 데이터 자산에 대 한 전문적인 정보가 변경 되었습니다. 오늘날 Yammer 같은 소셜 미디어 도구를 hello 광범위 한 작업 공간 사용 사람들이 예상 toobe 수 tooquickly 지원 및 조언을 받으려면 다양 한 항목입니다. **Azure Data Catalog**를 통해 기업 및 팀은 중앙 리포지토리에 엔터프라이즈 데이터 자산에 대한 정보를 통합할 수 있습니다. 데이터 소비자는 이러한 데이터 자산을 검색하고 관련 전문가가 제공한 기술 자료를 얻을 수 있습니다.

이 문서에서는 처음 사용 하는 접근 방식을 toogetting 제공 **Azure Data Catalog**합니다. hello 문서 Adventure Works 라는 가상 회사를 hello에 대 한 일반적인 데이터 카탈로그 도입 계획을 설명 합니다.

**Azure 데이터 카탈로그란?**

**Azure 데이터 카탈로그** 는 Azure에서 완전히 관리되는 서비스이며 셀프 서비스 데이터 원본 검색이 가능한 전사적 정보(메타데이터) 카탈로그입니다. Data Catalog에 등록, 검색, 주석 달기, 한 toodata 자산을 연결 합니다. 데이터 카탈로그를 이해 하 고 toothem 연결 쉽게 toofind 데이터 자산으로 설계 된 toomanage 서로 다른 정보 자산 toomake입니다. 사용 가능한 데이터에서 hello 시간 toogain 통찰력을 줄어들고 hello 값 tooorganizations 늘어납니다. toolearn 더 참조 [Microsoft Azure Data Catalog](https://azure.microsoft.com/services/data-catalog/)합니다.

## <a name="azure-data-catalog-adoption-plan"></a>Azure Data Catalog 도입 계획
**Azure Data Catalog** 방법을 hello의 이점은 hello 서비스를 사용 하는 전달된 toostakeholders와 사용자에 및 어떤 종류의 사용자를 교육 제공 toousers 채택 계획에 설명 합니다. 하나의 성공의 핵심 드라이버 tooadopt 데이터 카탈로그 서비스 toousers hello와 관련자의 hello 값을 전달할 수는 얼마나 효과적으로입니다. 초기 도입 계획의 주요 대상 hello는 hello 서비스의 hello 사용자입니다. 얼마나 많은 구매 기능을 관련자에 게에서 가져올에 관계 없이 hello 사용자 또는 고객의 데이터 카탈로그 서비스를 통합 하지 않은 것의 용도에 면 hello 채택 성공적으로 수행 됩니다. 따라서 이 문서에서는 사용자가 이해 관계자의 핵심 요구를 가지고 있는 것으로 가정하고 Data Catalog의 사용자 도입 계획을 작성하는 데 초점을 맞춥니다.
데이터 카탈로그에 있을 수 있는 기능과 하면 장치에 정보 및 지침 tooachieve hello 효과적인 채택 계획 성공적으로 시작 것입니다. 사용자가 데이터 카탈로그 toohelp 해당 작업에 성공 하는 제공 toounderstand hello 값이 필요 합니다. 사용자는 데이터 카탈로그 데이터와 더 많은 결과 달성 하기 위해를 도울 수 있는 방법 볼 hello 값 도입 데이터 카탈로그의 선택을 취소 됩니다. 변경이 어렵습니다 하는 효과적인 계획 tootake hello 챌린지 계정으로 변경 해야 합니다.

도입 계획을 사용 하면 사용자 toosucceed에 대 한 중요 한 통신 하 고 목표 달성를 수행할 수 있습니다. 일반적인 계획에는 데이터 카탈로그 toomake 사용자의 생활 편의 보다 쉽게 진행 되 하 및 hello 부분 뒤를 포함 하는 방법을 설명:

* **문을 비전** -간결 하 게, 사용자 및 관련자와 hello 도입 계획을 논의 하는 데는 데 도움이 됩니다. 이는 요약 설명입니다.
* **팀과 영향 요인을 파일럿** -toointroduce 팀이 방법을 구체화 하는 파일럿 팀과 영향 요인을 도움말 및 사용자가 tooData 카탈로그에서 학습 합니다. 영향 요인은 동료 사용자와의 학습을 가능하게 합니다. 또한 tooadoption 블로 커가 및 드라이버를 확인할 수 있습니다.
* **통신 및 요점이 대 한 계획** -사용자가 toounderstand 하는 데 도움이 어떻게 데이터 카탈로그 수 사용자를 도울, 팀 내에서 유기적 도입을 촉진 하 고 수 최종적으로 전체 조직 hello 합니다.
* **교육 계획** -포괄적인 리드 tooadoption 성공 및 성공적인 결과 일반적으로 학습 합니다.

다음은 몇 가지 팁 toodefine는 **Azure Data Catalog** 채택 계획 합니다.

## <a name="define-your-data-catalog-project-vision"></a>데이터 카탈로그 프로젝트 비전 정의
첫 번째 단계 toodefine hello는 **Azure Data Catalog** 채택 계획은 toowrite 하려는 작업에 대 한 심적인 설명을 tooaccomplish 합니다. 것이 가장 좋은 tookeep hello 비전 문을 매우 광범위 한 아직 충분히 간결한 toodefine 특정, 단기 및 장기 목표 합니다.

다음은 몇 가지 팁 toohelp 있습니다 비전 정의입니다.

* **Hello 주요 배포 드라이버를 확인할** -hello 비즈니스 데이터 카탈로그 처리 될 수 있는 hello 특정 데이터 원본 관리에 대 한 고려 하는 것이 필요 합니다. 수의 데이터 카탈로그를 사용 하 여 hello 상위 장점 상태입니다. 예를 들어 몇 가지 주요 사람만 깊이 파악 되 중요 하 고 복잡 한 데이터 원본 또는 모든 새 직원에 대 한 toolearn 및 사용 가능성 필요로 하는 일반적인 데이터 소스가 있을 수 있습니다. **Azure Data Catalog** 이러한 잘 알려진 문제점에서 hello 단기간 hello 서비스에 직접 및 초기 해결 될 수 있도록 이러한 데이터 원본 쉽게 toodiscover 확인 및을 이해할 수 있습니다.
* **선명 받지 않는 확실 한 수** -hello 비전의 이해 hello에서 모든 사용자를 가져옵니다 지우기 hello 값 데이터 카탈로그에 대 한 동일한 페이지 주는 toohello 조직 및 조직의 목표 hello 비전을 지 원하는 방법입니다.
* **사람 toowant toouse 데이터 카탈로그 영감** 프로그램-비전과 의사 소통 계획 담당자 toorecognize 데이터 카탈로그 toofind을 활용 하 고 데이터와 더 많은 toodata 소스 tooachieve를 연결할 수 영감 해야 합니다.
* **목적 및 타임라인 지정** - 이를 통해 도입 계획이 구체적이고 달성 가능한 결과물을 내도록 합니다. 타임 라인에서는 모든 사용자를 유지 하 고 검사점 toomeasure 성공 허용 합니다.

Adventure Works 라는 가상 회사를 hello에 대 한 데이터 카탈로그 채택 계획에 대 한 예제 비전 설명서는 다음과 같습니다.

**Azure Data Catalog** 키 데이터 원본에 hello Adventure Works 재무 팀 toocollaborate 자율적 이며, 쉽게 모든 팀 멤버 찾아서 hello 데이터를 사용할 수 있도록 그녀가 필요한 고 그녀의 기술 전체적으로 hello 팀과 공유할 수 있습니다.

명확한 비전 문구를 정한 후에는 데이터 카탈로그에 적합한 파일럿 프로젝트를 식별해야 합니다. 일반적으로 hello 다음 섹션에서는 몇 가지 팁 tooidentify 관련 된 사례를 사용 하므로 데이터 카탈로그에 대 한 몇 가지 시나리오가 있습니다.

## <a name="identify-data-catalog-business-use-cases"></a>데이터 카탈로그 비즈니스 사용 사례 식별
관련 tooData 카탈로그에 있는 tooidentify 사용 사례에서 다양 한 비즈니스 단위 tooidentify 관련 사용 사례 및 비즈니스 문제 toosolve 전문가 함께 푸시를 보냅니다. 사람들이 데이터 자산을 식별 및 이해했던 기존의 과제를 검토합니다. 예를 들어 수행 팀에 대해 알아보려면 데이터 자산에는 관련 데이터 소스 hello 조직에서 여러 사용자 요청 후에?

비교적 쉬운 대상을 나타내는 최상의 toochoose 사용 사례는: 중요 한 경우 아직 성공 가능성이 높은 데이터 카탈로그를 사용 하 여 해결 하는 경우.

일부의 팁이 tooidentify 사용 사례:

* **Hello 팀의 hello 목표 정의** 않습니다 hello 팀 목표를 달성 하는 방법-? 이 단계에서 toobe 목표를 지정할 것 이므로 데이터 카탈로그에 포커스를 아직 하지 않습니다. 기억 하지 hello 기술에 대 한 hello 비즈니스 결과 관한 것입니다.
* **Hello 비즈니스 문제 정의** -찾기 및 데이터 자산에 대 한 학습에 대 한 hello 팀이 직면 하는 hello 문제점은 무엇입니까? 예를 들어 중요 한 데이터 원본에 대 한 정보를 네트워크 폴더에서 Excel 통합 문서에서 확인할 수 있습니다 및 hello 팀 오래 대기 hello 통합 문서를 찾는 데 소비할 수 있습니다.
* **팀 문화권 관련된 toochange 이해** -많은 채택 문제 tooresistance toochange 관련 hello는 새로운 도구를 구현 하지 않고 있습니다. "이 항목은 어떻게 항상 했다" hello 기존 프로세스 위치 중일 수 있으므로 경우 toochange는 사용을 식별 하는 경우 중요 한 팀을 응답 하는 방법을 고장나지, 경우 이유가 자동 수정?"또는 합니다. 새 도구 또는 프로세스를 채택은 영향을 받는 hello 사람 hello 값 toobe hello 변경 내용으로 인해 실현를 이해 하 고 해결 hello 문제 toobe의 hello 중요성을 보내주셔서 감사 때 항상 쉬운입니다.
* **포커스를 toodata 자산 관련** -는 팀 hello 비즈니스 문제를 설명할 때 필요한 너무 "hello 나 통해 cut" 이란 관련 tooleveraging 엔터프라이즈 데이터 자산에 초점을 더 많은 유효성 합니다.

다음은 몇 가지 예제 사용 사례 관련된 tooData 카탈로그입니다.

### <a name="example-use-cases"></a>예제 사용 사례
* **중앙 가치가 높은 데이터 원본을 등록할** -IT hello 조직 전체에서 사용 되는 데이터 원본을 관리 합니다. IT는 일반적인 엔터프라이즈 데이터 원본을 등록하고 주석을 추가하여 데이터 카탈로그를 시작할 수 있습니다.
* **팀 기반 데이터 원본 등록** -팀마다 비즈니스 데이터 원본의 유용한 계열을 가지고 있습니다. 시작 **Azure Data Catalog** 식별 하 고 다른 많은 팀 및 캡처 hello 팀의 지식은 서로에 의해 사용 되는 키 데이터 원본을 등록 하 여 **Azure Data Catalog** 주석입니다.
* **셀프 서비스 비즈니스 인텔리전스** - 팀은 여러 원본에서 나온 데이터를 결합하는 데 많은 시간을 소비합니다. 등록 하 고 중앙 위치 tooeliminate 수동 데이터 원본 검색 프로세스에서에서 데이터 원본에 주석을 추가 합니다.

데이터 카탈로그 시나리오에 대해 자세히 tooread 참조 [일반적인 시나리오는 Azure Data Catalog](data-catalog-common-scenarios.md)합니다.

데이터 카탈로그에 대한 일부 사용 사례를 식별한 후 일반 시나리오가 표시될 것입니다. hello 다음 섹션에서는 tooidentify 첫 파일럿 프로젝트에 따라 방법 사용 사례에 설명 합니다.

## <a name="choose-a-data-catalog-pilot-project"></a>데이터 카탈로그 파일럿 프로젝트 선택
성공의 핵심 요소 toosimplify, 되어 작은 시작 합니다. 제한 된 범위는 데 도움이 됩니다 유지 hello로 잘 정의 된 파일럿 프로젝트를 너무 복잡 한 되었거나 너무 많은 참가자가 뒤따릅니다 하지 않고 앞으로 프로젝션 합니다. 하지만 중요 한 tooinclude 조기 채택자 tooskeptics에서 사용자가 혼합 하 여 이기도 합니다. Hello 솔루션을 수용 하는 사용자 나중에 프로그램 통신을 구체화 하 고 계획을 공개 하는 데 도움이 됩니다. 회의론자는 차단 문제를 식별하고 해결하는 데 도움이 됩니다. Skeptics 챔피언 해지면 해당 피드백 tooidentify 성공 드라이버를 사용할 수 있습니다.

데이터 카탈로그와 tooachieve 원하는 비즈니스 목표에 파일럿 계획 단계 해야 합니다. Hello 초기 파일럿에서 배우려면 사용자 기반을 확장할 수 있습니다. 초기 닫힌된 파일럿 좋은 tooestablish 측정 가능한 성공 않으며 hello 궁극적인 목표 유기적 또는 바이러스에 감염 증가 위한 것입니다. 데이터 카탈로그의 유기적 증가와 사용자가 자신의 데이터 사용을 제어 하 고 미치고 참여할 수 있는 다른 사람이 tooadopt toohello 카탈로그 기여 하 고 있습니다.

### <a name="target-hello-right-team"></a>대상 hello 적합 한 팀
파일럿 프로젝트를 선택 하면 기존의 비즈니스 문제를 해결 하는 hello 가장 매력적인 시나리오와 팀을 선택 합니다. 예를 들어 비즈니스 분석자는 SQL 서버 데이터베이스에서 보고서를 작성합니다. hello 문제는 그녀 있음을 알게 되었습니다 hello 데이터 원본의 tooseveral 동료와 통신 하는 후에입니다. 마지막으로, 데이터 원본을 toouse, 그녀는 Excel 통합 문서에 대 한 발견 해야 하는 시간 동안 toofind 낭비 후 각 데이터 원본에 대 한 설명을 포함 하 합니다. Hello Excel 통합 문서에는 적절 하 게 보내야 하므로 hello 테이블 설명, 하지만 그녀는 신속 하 게 찾은 이러한 데이터 원본을 등록 하 고에 주석이 추가 된 **Azure Data Catalog**합니다.

### <a name="identify-data-heroes"></a>데이터 히어로 식별
첫 번째 파일럿 프로젝트에는 몇 가지 개인 데이터를 생성 하 고 hello 팀 표현 균형에 있도록 데이터를 사용 하 게 포함 해야 합니다.

**데이터 생산자** 는 데이터 원본에 관한 전문지식을 갖춘 사람입니다. 예를 들어 다른 팀의 David는 핵심 Adventure Works 데이터 원본으로 많은 작업을 해 왔습니다. 이전 toohello 단기간 **Azure Data Catalog**, David Adventure Works 데이터 원본에 대 한 Excel 통합 문서 toocapture 정보를 만들었습니다.

**데이터 소비자** hello 데이터 toosolve hello 사용에 대 한 전문 지식이 있는 비즈니스 문제 됩니다. 예를 들어 Nancy는 비즈니스 분석가 Adventure Works SQL Server 데이터 원본 tooanalyze 데이터를 사용 합니다.

Hello 비즈니스 문제 중 하나는 **Azure Data Catalog** 해결 tooconnect은 **데이터 생산자** 너무**데이터 소비자**합니다. 기업 데이터 원본에 관한 정보의 중앙 저장소 역할을 함으로써 이 작업을 수행합니다. David는 데이터 카탈로그를 사용하여 Adventure Works 및 SQL Server 데이터 원본을 등록합니다. 모든 사용자에 게이 데이터 원본을 검색 crowdsourcing를 사용 하 여 hello 데이터에 대 한 자신의 의견을 공유할 수 있습니다, 그리고 또한 toousing hello 데이터 그녀 검색 했습니다. 예를 들어 Nancy hello 카탈로그를 검색 하 여 hello 데이터 소스를 검색 하 고 hello 데이터에 대 한 전문된 지식 그녀의 공유 합니다.  이제 hello 조직에 있는 다른 활용 공유 지식 으로부터 hello 데이터 카탈로그를 검색 하 여 합니다.

* 데이터 원본 등록에 대 한 더 toolearn 참조 [데이터 원본을 등록할](data-catalog-get-started.md)합니다.
* 검색 데이터 원본에 대 한 더 toolearn 참조 [데이터 소스를 검색](data-catalog-get-started.md)합니다.

### <a name="start-small-and-focused"></a>작고 집중된 시작
대부분의 엔터프라이즈 파일럿 프로젝트에 대 한 비즈니스 사용자가 데이터 카탈로그의 hello 값을 신속 하 게 볼 수 있도록 우선 순위가 높은 데이터 원본과 hello 카탈로그를 시드 해야 있습니다. IT 관심 tooyour 파일럿 팀 수 있는 일반적인 데이터 소스를 식별 하는 것이 좋습니다 toostart 됩니다. SQL Server와 같은 지원 되는 데이터 원본에 대 한 hello를 사용 하 여 권장 **Azure Data Catalog** 데이터 원본 등록 도구입니다. Hello 데이터 원본 등록 도구를 등록할 수 있는 다양 한 범위의 데이터 소스, SQL Server 및 Oracle 데이터베이스를 포함 하 고 SQL Server Reporting Services 보고 합니다. 현재 데이터 원본의 전체 목록은 [Azure 데이터 카탈로그 지원 데이터 원본](data-catalog-dsr.md)을 참조하세요.

파악 하 고 등록 키 데이터 원본을 다른 위치에 저장 가능한 tooalso 가져오기 데이터 원본 설명입니다. 데이터 카탈로그 API hello 개발자 tooload 설명과 hello David 생성 및 유지 관리 하는 Excel 통합 문서 등의 다른 위치에서 주석 수 있습니다.

hello 다음 섹션에서 Adventure Works 사에서 hello는 예제 프로젝트를 설명합니다.

### <a name="an-example-project"></a>예제 프로젝트
예를 들어 Nancy hello 비즈니스 분석가, SQL Server 데이터베이스에서 데이터를 사용 하 여 그녀의 팀에 대 한 보고서를 만듭니다. hello 문제는 그녀 있음을 알게 되었습니다 hello 데이터 원본의 tooseveral 동료와 통신 하는 후에입니다. 동료들이 **Azure 데이터 카탈로그**와 같은 중앙 위치에 등록하고 주석을 추가했다면 Nancy가 이 데이터를 빨리 발견했을 것입니다.

tooillustrate 얼마나 쉽게 Nancy와 그녀의 팀 수 중요 한 데이터를 찾을 hello 데이터 원본 등록 도구 toopopulate hello 카탈로그를 사용 하 여 hello 데이터 원본에 대 한 정보 (메타 데이터). 이 방식으로 hello 정보 hello 데이터베이스에 대 한 사용 가능한 toohello 팀과 hello enterprise, 하지 몇 개인 경우 데이터 원본을 Data Catalog에 등록하면 Nancy와 그녀의 팀은 해당 원본을 쉽게 찾을 수 있습니다. hello 결과 그녀의 팀과 hello 엔터프라이즈에 대 한 포괄적이 고 관련 데이터 카탈로그입니다. 데이터 카탈로그를 채택 하는 더 많은 팀, 비즈니스 데이터 원본 없어질 toofind 쉽고 사용 따라서 데이터와 더 많은 데이터 중심 문화권 tooachieve 사용 하도록 설정 합니다.

hello 데이터 원본 등록 도구에 대해 자세히 toolearn 참조 [Azure Data Catalog 시작](data-catalog-get-started.md)합니다.

또한 hello 파일럿 프로젝트의 일부로 Nancy의 팀은 Excel 통합 문서에 설명 되어 있는 데이터 원본이 해당 David를 사용 하 고 동료 들이 유지 관리 합니다. Hello 엔터프라이즈의 다른 팀 Excel 통합 문서 toodescribe 데이터 소스를 사용 하므로 hello IT 팀 toocreate 도구 toomigrate hello Excel 통합 문서 tooData 카탈로그를 결정 합니다. 기존 주석을 tooimport hello 데이터 카탈로그 REST API를 사용 하 여 hello 파일럿 프로젝트 팀 hello 데이터 원본 등록 도구를 완벽 하 게 정보를 사용 하 여 hello 데이터 원본에서 추출 된 메타 데이터로 구성 된 하는 완전 한 데이터 카탈로그를 가질 수 있습니다. 이전에 수동 재 돌입에 대 한 hello 필요 없이 데이터 생산자와 소비자에 의해 설명 합니다. Hello 엔터프라이즈 데이터 카탈로그까지 확장 되면서 hello 조직 일반 데이터 원본 및 사용자 지정 원본 및 드문 시나리오에 대 한 데이터 카탈로그 API hello에 대 한 hello 데이터 원본 등록 도구를 사용할 수 있습니다.

> [!NOTE]
> Hello를 사용 하는 샘플 도구 안내 드린 바 **Azure Data Catalog** API toomigrate Excel 통합 문서 tooData 카탈로그입니다. 데이터 카탈로그 API hello 및 hello 샘플 도구에 대 한 toolearn [hello 임시 통합 문서의 코드 예제를 다운로드](https://azure.microsoft.com/documentation/samples/data-catalog-dotnet-excel-register-data-assets/), 체크 아웃 hello 및 [Azure 데이터 카탈로그 REST API](https://msdn.microsoft.com/library/azure/mt267593.aspx) 설명서.
>
>

시간 tooexecute hello 파일럿 프로젝트 이면 후에 데이터 카탈로그 채택 계획 합니다.

### <a name="execute"></a>실행
이 시점에서 데이터 카탈로그의 사용 사례를 식별하고 첫 번째 프로젝트를 식별했습니다. 또한 hello 키 Adventure Works 데이터 원본 등록 및 정보를 추가 했습니다 hello를 사용 하 여 hello 기존 Excel 통합 문서에서 작성 하는 IT 도구입니다. 이제 hello 파일럿 팀 toostart hello 데이터 카탈로그 채택 과정으로 toowork 시간입니다.

다음은 몇 가지 팁 tooget 시작한입니다.

* **관심 끌기** - **Azure Data Catalog**가 삶을 편하게 만든다면 비즈니스 사용자가 관심을 가질 것입니다. Hello 솔루션 및 hello 혜택을 제공 하지 hello 기술 toomake hello 대화를 시도 합니다.
* **변화를 촉진 하** -작은 항목부터 시작 하 고 hello 계획 toobusiness 사용자가 통신 합니다. hello hello 결과 영향을 줄 고 hello 솔루션에 대 한 소유권을 시작 하 고 사용자가 중요 한 tooinvolve 되기 toobe 성공 합니다.
* **조기 채택자 백로그 정리** -조기 채택자 열 중 수행 하는 작업 및 기쁘게 생각된 tooevangelize hello 활용 되는 비즈니스 사용자는 **Azure Data Catalog** tootheir 피어입니다.
* **학습 대상** -비즈니스 사용자에 게 불필요 tooknow 데이터 카탈로그에 대 한 모든, 따라서 학습 tooaddress 특정 팀 목표를 대상입니다. 사용자가 수행할 작업 방법 및 일부 작업 수를 변경, tooincorporate에 집중 **Azure Data Catalog** 자신의 일상 업무에 있습니다.
* **기꺼이 toofail 수** -파일럿 hello 원하는 결과 달성 없는 경우 hello 다시 평가, 및 영역 toochange-tooa 더 큰 범위에서 이동 하기 전에 hello 파일럿의 문제 해결을 식별 합니다.

데이터 카탈로그를 사용 하 여 파일럿 팀 점프 전에 개시 예약 toodiscuss 모임 hello에 대 한 기대 프로젝트를 파일럿 실행 및 초기 교육을 제공 합니다.

### <a name="set-expectations"></a>기대치 설정
예외 및 목표 설정은 사용자가 특정 결과물에 집중하는 데 도움이 됩니다. 트랙, tookeep hello 프로젝트 regular 할당 (예: hello 범위 및 hello 파일럿의 기간에 따라 매일 또는 매주) 늘어납니다. 비즈니스 사용자가 엔터프라이즈 데이터 지식을 활용할 수 있도록이 crowdsourcing 데이터 자산 hello 데이터 카탈로그의 가장 중요 한 기능 중 하나입니다. 훌륭한 과제 할당 각 파일럿 팀 구성원 tooregister 하거나 추가 하거나가 사용한 데이터 원본을 하나 이상에 주석을 추가 합니다. 참조 [데이터 원본을 등록](data-catalog-get-started.md) 및 [어떻게 tooannotate 데이터 원본](data-catalog-get-started.md)합니다.

팀과 회의를 hello에 정기적인 일정 tooreview hello 주석의 일부입니다. 데이터 원본에 대 한 좋은 주석은 중앙 위치에서 의미 있는 데이터 원본 정보를 제공 하기 때문에 hello 핵심 성공적인 데이터 카탈로그 도입 됩니다. 좋은 주석 없이 데이터 원본에 대 한 지식을 유지 hello 기업 전반의 분산 됩니다. 참조 [어떻게 tooannotate 데이터 원본](data-catalog-get-started.md)합니다.

하며, hello hello 프로젝트의 테스트를 최종 사용자가 검색 하 고 toouse 필요한 hello 데이터 원본을 이해 합니다. 파일럿 사용자 hello 카탈로그 tooensure 하루 tooday 작업에 사용 하는 hello 데이터 소스 관련 된 정기적으로 테스트 해야 합니다. 필요한 데이터 소스 누락 되거나 제대로 주석이 추가 된 경우이 역할을 해야 미리 알림 tooregister 추가 데이터 원본 또는 tooprovide 추가 주석입니다. 이 연습 값 toohello 파일럿 노력만 추가 되지 않습니다 되지만 hello 파일럿 완료 된 후 tooother 팀을 통해 수행 하는 효과적인 습관 빌드합니다.

### <a name="provide-training"></a>교육 제공
교육 충분 한 tooget hello 사용자를 시작 하 고 toohello 특정 목적에 맞게 조정 된 고 hello 파일럿 팀 멤버의 수준 발생 해야 합니다. tooget 교육을 시작, 있습니다 수에서 다음과 같이 hello hello [Azure Data Catalog 시작](data-catalog-get-started.md) 문서. 또한 hello를 다운로드할 수 있습니다 [Azure 데이터 카탈로그 파일럿 프로젝트 학습 프레젠테이션](https://github.com/Azure-Samples/data-catalog-dotnet-get-started/blob/master/Azure%20Data%20Catalog%20Training.pptx?raw=true)합니다. 이 PowerPoint 프레젠테이션이 시작된 소개 데이터 카탈로그 tooyour 파일럿 팀 멤버에 게 도움이 됩니다.

## <a name="conclusion"></a>결론
파일럿 팀 상당히 문제 없이 실행 되 고 초기 목표를 달성 하 한을 데이터 카탈로그 채택 toomore 팀을 확장 해야 합니다. 에서 배운 프로그램 파일럿 프로젝트 tooexpand 데이터 카탈로그 조직 전체에서 구체화 및 적용 됩니다.

hello 조기 채택자 hello 파일럿에 참여 하는 데이터 카탈로그를 채택 hello 이점에 대 한 유용한 tooget hello 단어 아웃 될 수 있습니다. 데이터 카탈로그 비즈니스 문제를 해결 하 고, 데이터 소스를 보다 쉽게 검색,를 사용 하는 hello 데이터 원본에 대 한 통찰력을 공유할 자신의 팀을 지원 하는 방법을 다른 팀과 공유할 수 있습니다. 예를 들어 조기 채택자 hello Adventure Works 파일럿 팀에서 얼마나 쉬운지 toofind 정보 하는 것이 하드 toofind Adventure Works 데이터 자산에 대 한 다른 표시 하 고 이해 수 합니다.

이 문서는 조직에서 **Azure 데이터 카탈로그** 를 시작하는 방법에 관한 문서입니다. 수 toostart 데이터 카탈로그 파일럿 프로젝트 것을 기대 하 고 조직 전체에서 데이터 카탈로그를 확장 합니다.

## <a name="more-information-about-azure-data-catalog"></a>Azure 데이터 카탈로그에 관한 자세한 정보
* [Azure 데이터 카탈로그 제품 페이지](https://azure.microsoft.com/services/data-catalog/)
* [Azure 데이터 카탈로그 문서](https://azure.microsoft.com/documentation/services/data-catalog/)
* [Azure 데이터 카탈로그 일반적인 시나리오](data-catalog-common-scenarios.md)
* [데이터 원본 등록](data-catalog-get-started.md)
* [데이터 원본 검색](data-catalog-get-started.md)
* [데이터 원본에 주석 추가](data-catalog-get-started.md)
* [메타데이터 크라우드소싱](data-catalog-get-started.md)
