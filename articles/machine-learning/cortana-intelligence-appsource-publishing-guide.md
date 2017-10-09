---
title: "aaaCortana 인텔리전스 AppSource 게시 가이드 | Microsoft Docs"
description: "Microsoft 파트너는 Cortana Intelligence 솔루션 tooAppSource toofollow toopublish 필요한 모든 hello 단계는 다음과 같습니다."
services: machine-learning
documentationcenter: 
author: AnupamMicrosoft
manager: jhubbard
editor: cgronlun
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: anupams;v-bruham;garye
ms.openlocfilehash: 66f26016b5eb709c567e9829aa787ca926e13d9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-appsource-publishing-guide"></a>Cortana Intelligence AppSource 게시 가이드

## <a name="overview"></a>개요
AppSource는 hello toodiscover 비즈니스 의사 결정권자 (Bdm)에 대 한 단일 대상 이며 비즈니스 솔루션/apps 파트너에 의해 작성 하 고 Microsoft에서 평가 원활 하 게 시도 합니다. 조사식 [이 비디오](https://youtu.be/hpq_Y9LuIB8) toolearn AppSource 작동 하는 방법입니다. 

다음과 같은 경우 Microsoft 파트너는 AppSource에 게시하여 실제로 혜택을 얻을 수 있습니다.
- [Cortana Intelligence Suite](https://azure.microsoft.com/en-us/suites/cortana-intelligence-suite/?cdn=disable)를 사용하여 지능형 솔루션/앱을 빌드한 경우
- 솔루션 또는 앱이 특정 비즈니스 문제를 다루는 경우
- 고객이 예측 가능한 방식으로 비교적 신속하게 다시 사용할 수 있는 모듈 또는 지적 재산을 빌드한 경우

AppSource에 이미 게시된 [Cortana Intelligence 솔루션](https://appsource.microsoft.com/en-us/marketplace/apps?product=cortana-intelligence&page=1)을 살펴보세요. 

이 문서에서는 안내 hello 단계 tooget 파트너의 Cortana 인텔리전스 솔루션 게시 된 tooAppSource

## <a name="getting-started"></a>시작
1. Hello에 [파트너 커뮤니티 이점 가이드](https://www.microsoftpartnerserverandcloud.com/_layouts/download.aspx?SourceUrl=Hosted%20Documents/Partner%20Community%20Benefits%20Guide%20-%20Cloud%20and%20Enterprise.pdf) (PDF), 페이지 9 tooget Advanced Analytics 파트너로 나열을 참조 하십시오.
1. 전체 hello [응용 프로그램을 제출할](https://appsource.microsoft.com/en-us/partners/list-an-app) 폼입니다.

    Hello 질문에 대 한 *"앱 빌드되는 선택 hello 제품*", hello 확인 **다른** 확인란 및 목록을 "Cortana 인텔리전스" hello에 컨트롤을 편집 합니다.
1. Cortana 인텔리전스 앱 전혀 tooAppSource 얻을 수, 전에 Cortana 인텔리전스 파트너 솔루션 기술 팀에 의해 인증 가져올 해야 합니다. 프로세스를 시작 하는 tooget, 주시면 감사 공유 세부 정보를 입력 하 여 응용 프로그램에 대 한 설문 조사에 양식에 [AppSource 게시에 대 한 Cortana Intelligence 솔루션 평가](https://aka.ms/cisappsrceval)합니다. 이 사이트는 암호로 보호 되어 있으며 hello 사이트 tooget 암호 hello 하는 방법에 대 한 지침입니다.

## <a name="solution-evaluation-criteria"></a>솔루션 평가 기준
다음은 조건 hello 응용 프로그램 요구 toomeet hello 목록
1. 응용 프로그램 필요 tooaddress 특정 비즈니스 사용 하 여 지정 된 기능 영역 내에서 사례 문제 미리 정의 된 가치 제안에 대 한 최소 구성으로는 반복 가능한 방식으로 구현할 수는 짧은 기간 내에서 합니다.
1. 솔루션에는 다음과 같은 구성 요소가 hello 중 하나 이상을 사용 해야 합니다.

    - HDInsight
    - 기계 학습
    - Data Lake Analytics
    - Stream Analytics
    - Cognitive Services
    - Bot Framework
    - Analysis Services
    - Microsoft R Server 독립 실행형
    - SQL 2016 또는 HDInsight Premium의 R Services
1. 솔루션은 DPOR/CSP를 사용하는 고객당 매달 $1000 이상을 창출해야 합니다.
1. 솔루션은 동의가 리소스 액세스 제어 및 사용자 인증에 사용할 수 있는 hello Azure Active Directory 페더레이션 single sign on (AAD 페더레이션 SSO)를 사용 해야 합니다. Tooshow toohello 평가 팀 솔루션 인지 AAD 페더레이션 SSO 응용 프로그램에 전혀 tooAppSource 수 전에 사용 하도록 설정 해야 합니다.

     toosee 의미 toobe AAD 페더레이션 SSO 사용, tooposition 02시 35분 검색 [AppSource 평가판 체험 안내](https://aka.ms/trialexperienceforwebapps) 비디오. 앱에서 AAD 페더레이션된 SSO를 아직 사용할 수 없는 경우 관련된 몇 가지 설명서는 다음과 같습니다.
   1. [한 번 클릭 로그인](https://identity.microsoft.com/Landing?ru=https://identity.microsoft.com/)
   1. [Azure Active Directory와 응용 프로그램 통합](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-an-application)
     
1. Power BI를 사용 하 여 솔루션의: 선택 사항 이지만 권장 사항임 toogenerate 크면 잠재 고객의 입증 된 것 처럼 합니다.

## <a name="devcenter-account-setup"></a>DevCenter 계정 설정
Microsoft 프로그램 회사 toobecome 게시자 등록 hello 과정입니다. 이미 실행 중인 기존 DevCenter 계정 등록 된 게시자, DevCenter 계정과 연결 된 hello 전자 메일 ID를 공유 합니다. 응용 프로그램 게시에 대 한 승인 되 면 액세스 toofull 설명서에 대 한 받아볼 [게시자 프로필 클라우드 포털 관리](https://cloudpartner.azure.com/#documentation/manage-publisher-profile)

없다면 하나, 다음은 hello 주요 단계 toosetup DevCenter 계정입니다.
1. [여기](https://signup.live.com/signup.aspx)서 Microsoft 계정을 만듭니다.
1. Microsoft DevCenter toohello 이동 [등록 페이지](http://go.microsoft.com/fwlink/?LinkId=615100) "등록"을 클릭 합니다.
1. 지불에 대 한 대화 상자가 나타나면 tooyou 드렸습니다 hello 코드를 사용 합니다. 코드가 없는 경우 [appsourcecissupport@microsoft.com](mailto:appsourcecissupport@microsoft.com?subject=Request%20for%20promotion-code%20for%20DevCenter%20account%20setup)에 문의하세요.
1. 선택 hello [국가/지역](https://docs.microsoft.com/windows/uwp/publish/account-types-locations-and-fees) 거주 하 또는 비즈니스입니다. **수 toochange 됩니다.이 작업을 나중에 있습니다.**
1. [개발자 계정 유형](https://docs.microsoft.com/windows/uwp/publish/account-types-locations-and-fees)을 선택합니다. AppSource의 경우 **회사**를 선택합니다. 이러한 있는지 tooreview 수 회사 계정에 대 한 [지침](https://docs.microsoft.com/windows/uwp/publish/opening-a-developer-account)합니다.
1. 개발자 계정에 대 한 toouse 원하는 hello 연락처 정보를 입력 합니다.
자세한 단계별 지침을 방법에 대 한 toosetup DevCenter 계정 hello 지침을 참조 하십시오. [여기](https://docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-accounts-creation-registration)합니다.

## <a name="provide-info-for-microsoft-sellers"></a>Microsoft 판매자에 대한 정보 제공
파트너 앱 잠재 고객 앞에 배치 toobe 수 toocollaborate Microsoft 판매자와 AppSource 파트너에 대 한 hello 핵심 가치 제안 중 하나입니다.

가득 찰 [Microsoft 판매자 파트너 솔루션 정보](https://aka.ms/aapartnerappinfo) 너무 보냅니다[appsourcecissupport@microsoft.com](mailto:appsourcecissupport@microsoft.com?subject=Request%20publisher%20account%20creation%20for%20%3cPartner%20Name%3e%20and%20whitelist%20owner/contributer%20AAD/MSA%20email%20IDs)합니다. 이 게시에 대 한 승인 Cortana Intelligence 앱 tooget에 대 한 필수 단계입니다.

## <a name="build-a-compelling-customer-walkthrough-on-appsource"></a>AppSource에서 매력적인 고객 연습 작성
먼저 AppSource에서 [Neal Analytics Inventory Optimization](https://appsource.microsoft.com/en-us/product/web-apps/neal_analytics.8066ad01-1e61-40cd-bd33-9b86c65fa73a?tab=Overview&tag=CISHome)(Neal Analytics 인벤토리 최적화)를 살펴보세요. AppSource의 모든 앱 항목에는 평가판 체험 진입점 외에도 제목, 요약(최대 100자), 설명(최대 1300자), 이미지, 동영상(선택 사항), pdf 문서가 있습니다. 파트너는 이러한 모든 toobuild 매력적인 고객 환경을 활용 해야 합니다.

파트너는 이러한 AppSource tooend 판매 오케스트레이션 끝에 추가 하는 hello 콘텐츠의 생각해 야 합니다. 고객은 hello 제목 및 설명 toounderstand hello 가치 제안을 읽고에 대 한 어떤 hello 솔루션은 이미지 및 비디오 toounderstand를 통해 이동 하 여 합니다. 잠재 고객은 사례 연구를 통해 기존 고객이 어떻게 가치를 얻는지를 확인할 수 있습니다. 

더 많은 관심 및 원하는 tooknow 느낄 hello 고객 해야 모든. 이 방법으로 좋은 기술 영업 사원은 hello 신규 고객을 안내 하는 피치 기반으로 하는 데크 프레젠테이션 생각 하면 됩니다. 설명의 형식은 toobreak hello 제안 하위 머리글으로 강조 각각 hello 텍스트 가치 제안에 따라 하위 섹션으로 구성 합니다. 

방문자 hello "요약을 제공 합니다." 필드 및 하위 머리글 tooget 요점 어떤 hello 앱 주소를 통해 일반적으로 보기 및 빠른을 쉽게에서 hello 응용 프로그램을 고려해 야 이유 있습니다. 따라서이 tooget hello 사용자의 주의 제공 이유 tooread tooget hello 사항에 중요 합니다.

다음 파트너의 성과를 참조하세요.
- [Neal Analytics Inventory Optimization](https://appsource.microsoft.com/en-us/product/web-apps/neal_analytics.8066ad01-1e61-40cd-bd33-9b86c65fa73a?tab=Overview)(Neal Analytics Inventory 최적화)
- [Plexure Retail Personalization](https://appsource.microsoft.com/en-us/product/web-apps/plexure.c82dc2fc-817b-487e-ae83-1658c1bc8ff2?tab=Overview)(Plexure Retail 개인 설정)
- [AvePoint Citizen Services](https://appsource.microsoft.com/en-us/product/web-apps/avepoint.7738ac97-fd40-4ed3-aaab-327c3e0fe0b3?tab=Overview)(AvePoint 대국민 서비스)

sales의 최종 act hello tooshow hello 응용 프로그램/솔루션 가치 제안을 hello 배달 하는 방법을 보여 주는 데모입니다. 이것이 AppSource의 고객 평가판 체험에 바라는 것입니다. 좋은 데모 작업을 수행 합니다 hello 다음:
- 다시 hello 가치 제안의 hello 앱을 간단히 요약 하 고 hello 솔루션 상호 작용 하는 hello 고객 회사 내의 hello 가상 사용자 나열
- 특정 문제를 다루는 샘플 고객에 대 한 스토리 및 집합 hello 컨텍스트 확인
- 설명 방법을 hello 상황 수 일반적으로 쿼리에서도 찾지 hello 솔루션 사용 중인 경우 어떻게 되는지 (이전) VS hello 고객에 영향을 합니다. 이 정보는 PowerBI 대시보드 등을 사용하여 표시할 수 있습니다.
- 요약 hello 솔루션 사용 하 여 방법 등 모든 특정 기계 학습 알고리즘을 사용 하 여 발생 합니다.

hello 콘텐츠 AppSource에 추가 되 고 높은 품질은 이어야 하며 충분 한 tooenable hello 다음을 연결할:
- 파트너의 기술 영업 담당자는 이 콘텐츠를 영업 오케스트레이션에 사용해야 합니다. 사용 하 여 영업 팀도 수 toodo 되 고 MS 판매 담당자 hello 동일 예상할 수 있도록 라는 좋은 징후입니다. 이렇게 하면 고객 연락 지점을 toobe 수 tooconsistently 릴레이 hello 동일 스토리 tootheir 팀 동료와 더 높은 ups tooget 예산 및 승인 전에 구매 거래 작업을 수행할 수 있습니다.
- 유기적으 hello 사이트를 방문 하는 고객 수 hello를 통해 콘텐츠 모두 자체적으로 이동한 다음 기쁘게 생각된 toorespond 백 toopartner 통신 toomove 다음 단계를 미리 생각 합니다.

하는 파트너 간주 해야 하는 이유 hello 콘텐츠 이러한 AppSource tooend 판매 오케스트레이션 끝에 추가 합니다. Hello 스토리 선과 평가판 체험에 표시 된 기능 toobe 기반 제공 서비스의 유형으로 결정할 수 있습니다.

## <a name="publish-your-app-on-hello-publishing-portal"></a>Hello 게시 포털에 앱 게시
단계 hello 평가한에서는 응용 프로그램에 대 한 후에 액세스 toohello 게시 포털 되며 볼 수 [toopublish Cortana Intelligence 클라우드 파트너 포털을 통해 제공 되는 방식을](https://cloudpartner.azure.com/#documentation/cloud-partner-portal-publish-cortana-intelligence-app) 에 대 한 자세한 지침은 다음 단계입니다.

Hello 필드에 대 한 정보가 필요한 경우 전자 메일 < appsourcecissupport@microsoft.com >합니다.
## <a name="my-app-is-published-on-appsource---now-what"></a>내 앱이 AppSource에 게시되었습니다. 이제 어떻게 해야 하나요?
먼저 앱이 게시된 것을 축하 드립니다.
hello 수준의 과도 하 게 AppSource에서 앱을 게시에서 가져올 반환 hello 대상 영향을 주는 방법을에 따라 달라 집니다. 참조 [증가 해킹 AppSource에서 Cortana 인텔리전스 앱](http://aka.ms/aagrowthhackguide) 에 대 한 자세한 내용은 방법을 hello 반환을 최대화할 수 있습니다.

질문이 나 제안, 주시면 감사 교류할에서 toous 경우 < appsourcecissupport@microsoft.com >합니다.

