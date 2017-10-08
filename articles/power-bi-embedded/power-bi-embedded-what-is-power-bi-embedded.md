---
title: "Microsoft Power BI Embedded aaaWhat 인지 확인"
description: "Power BI 포함 하면 toointegrate Power BI 보고서 웹 이나 모바일 응용 프로그램에 사용자 지정 솔루션 toobuild 필요는 없습니다."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 03649b72-b7d7-40ca-b077-12356d72d4f3
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/20/2017
ms.author: asaxton
ms.openlocfilehash: 0353938b6cdd9bb58b123b250f45f76b8cc7abe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-microsoft-power-bi-embedded"></a>Microsoft Power BI Embedded란?
**Power BI Embedded**를 사용하면 Power BI 보고서를 웹 또는 모바일 응용 프로그램에 통합할 수 있습니다.

![](media/powerbi-embedded-whats-is/what-is.png)

Power BI 포함 되는 **Azure 서비스** Isv 수 있게 해 주는 및 응용 프로그램 개발자가 toosurface Power BI 데이터에서 해당 응용 프로그램 내에서 발생 합니다. 개발자가 응용 프로그램을 구축한 경우 이러한 응용 프로그램에는 고유한 사용자 및 고유한 기능 집합이 있습니다. 이러한 앱 toohave 차트 및 Microsoft Power BI 포함 하 여 이제 전원이 수 있는 보고서와 같은 몇 가지 기본 제공 데이터 요소에도 발생할 수 있습니다. Power BI 계정 toouse 응용 프로그램 필요 하지 않습니다. Toosign 마찬가지로 앞, tooyour 응용 프로그램에서 계속 하 고 볼 있고 추가 라이선싱이 필요 없이 Power BI 보고 환경 hello와 상호 작용 합니다.

## <a name="licensing-for-microsoft-power-bi-embedded"></a>Microsoft Power BI Embedded 라이선스
Hello에 **Microsoft Power BI Embedded** 사용 모델을 Power BI가 아니므로 hello 책임 hello 최종 사용자의 라이선스입니다.  대신, **세션** hello 시각적 개체를 사용 하는 hello 응용 프로그램의 hello 개발자가 구입 해야 하 고 해당 리소스를 소유 하 고 있는 toohello 구독 요금이 청구 됩니다. Hello에서 추가 정보를 확인할 수 있습니다 [가격 책정 페이지](https://azure.microsoft.com/en-us/pricing/details/power-bi-embedded/)합니다.

## <a name="microsoft-power-bi-embedded-conceptual-model"></a>Microsoft Power BI Embedded 개념적 모델

![](media/powerbi-embedded-whats-is/model.png)

Azure의 다른 모든 서비스와 마찬가지로 Power BI 포함에 대 한 리소스는 hello를 통해 프로 비전 [Azure 리소스 관리자 Api](https://msdn.microsoft.com/library/mt712306.aspx)합니다. 이 경우에 프로 비전 하는 hello 리소스는 **Power BI 작업 영역 컬렉션**합니다.

## <a name="workspace-collection"></a>작업 영역 컬렉션
A **작업 영역 컬렉션** hello 최상위 Azure 컨테이너 리소스에 대 한 0 개 이상 포함 하는 **작업 영역**합니다.  A **작업 영역** **컬렉션** hello 표준 Azure 속성 뿐만 아니라 hello 다음의 모든:

* **액세스 키** – 안전 하 게 호출할 때 사용 되는 키 hello Power BI Api (이후 섹션에서 설명).
* **사용자가** – Azure Active Directory (AAD) 있는 사용자를 관리자 권한 toomanage hello Azure 포털 또는 Azure 리소스 관리자 API를 통해 Power BI 작업 영역 컬렉션 hello 합니다.
* **지역** – 프로 비전의 일부로 **작업 영역 컬렉션**, 프로 비전 영역 toobe를 선택할 수 있습니다. 자세한 내용은 [Azure 지역](https://azure.microsoft.com/regions/)을 참조하세요.

## <a name="workspace"></a>작업 영역
**작업 영역** 은 데이터 집합 및 보고서를 포함할 수 있는 Power BI 콘텐츠의 컨테이너입니다. **작업 영역** 은 처음 만들 때 비어 있습니다. Power BI Desktop을 사용 하 여 콘텐츠를 작성 합니다 하 고 hello를 사용 하 여 작업 영역으로 hello PBIX를 프로그래밍 방식으로 배포 합니다. [Power BI 가져오기 API](https://msdn.microsoft.com/library/mt711504.aspx)합니다. 또한 Power BI Desktop을 사용하는 대신 프로그래밍 방식으로 데이터 집합을 만든 다음 응용 프로그램 내에서 보고서를 만들 수 있습니다.

## <a name="using-workspace-collections-and-workspaces"></a>작업 영역 컬렉션 및 작업 영역 사용
**작업 영역 컬렉션** 및 **작업 영역** 는 최상의 어떤 방식으로 작성 하는 hello 응용 프로그램의 hello 디자인에 적합에 구성 및 사용 되는 콘텐츠의 컨테이너입니다. 그 안에서 hello 콘텐츠를 정렬 수는 여러 가지 방법으로 사용 됩니다. 하나의 작업 영역 내에서 모든 콘텐츠 tooput를 선택할 수 있습니다 및 이후 사용 하 여 응용 프로그램 토큰 toofurther 고객에 게 적절 한 hello 콘텐츠를 세분화 하는 다음 합니다. 수도 있습니다 tooput 모든 고객이 별도 작업 영역에 있는 일부 구분 되어 있도록 합니다. 또는 tooorganize 사용자가 아니라 고객 지역으로 선택할 수 있습니다. 이 유연한 디자인 toochoose hello 가장 좋은 방법은 tooorganize를 통해 콘텐츠 수 있습니다.

## <a name="cached-datasets"></a>캐시된 데이터 집합
캐시된 데이터 집합을 사용할 수 있습니다.  그러나 캐시된 데이터가 **Microsoft Power BI Embedded**에 로드되면 새로 고칠 수 없습니다. 캐시 된 데이터 집합이 DirectQuery를 사용 하는 대신 hello 데이터를 Power BI Desktop으로 가져온 것을 의미 합니다.

## <a name="authentication-and-authorization-with-app-tokens"></a>앱 토큰으로 인증 및 권한 부여
**Microsoft Power BI Embedded** 모든 hello 필요한 사용자 인증 및 권한 부여 tooyour 응용 프로그램 tooperform을 지연 합니다. 최종 사용자가 Azure AD(Azure Active Directory)의 고객이어야 한다는 명시적인 요구 사항은 없습니다.  대신, 응용 프로그램에 따라 표시 너무**Microsoft Power BI Embedded** toorender 권한 부여를 사용 하 여 Power BI 보고서 **응용 프로그램 인증 토큰 (앱 토큰)**합니다.  이러한 **앱 토큰** 앱 toorender 보고서가 원하는 경우 필요에 따라 생성 됩니다.

![](media/powerbi-embedded-whats-is/app-tokens.png)

**응용 프로그램 인증 토큰 (앱 토큰)** 에 대해 사용 되는 tooauthenticate는 **Microsoft Power BI Embedded**합니다.  다음과 같은 세 가지 형식의 **앱 토큰**이 있습니다.

1. 프로비전 토큰 - 새 **작업 영역**을 **작업 영역 컬렉션**에 프로비전할 때 사용
2. 만들기를 직접 호출 toohello 때 사용 되는 개발 토큰- **Power BI REST Api**
3. Iframe 포함 된 hello에서 보고서 호출 toorender를 만들 때 사용 하는 토큰-를 포함 합니다.

이러한 토큰은 적합 hello와 상호 작용의 다양 한 단계 **Microsoft Power BI Embedded**합니다.  hello 토큰은 사용자 응용 프로그램 tooPower BI에서에서 권한을 위임할 수 있도록 설계 되었습니다. 자세한 내용은 [앱 토큰 흐름](power-bi-embedded-app-token-flow.md)을 참조하세요.

## <a name="create-or-edit-reports-within-your-application"></a>응용 프로그램 내에서 보고서 만들기 또는 편집

이제 편집 보고서 존재 하거나 toouse Power BI Desktop 필요 없이 응용 프로그램에 직접 새 보고서를 만들 수 있습니다. 이렇게 하려면 작업 영역 내에 데이터 집합이 있어야 합니다.

## <a name="see-also"></a>참고 항목

[일반적인 Microsoft Power BI Embedded 시나리오](power-bi-embedded-scenarios.md)  
[Microsoft Power BI Embedded 시작](power-bi-embedded-get-started.md)  
[샘플 시작](power-bi-embedded-get-started-sample.md)  
[보고서 포함](power-bi-embedded-embed-report.md)  
[Power BI Embedded에서 인증 및 권한 부여](power-bi-embedded-app-token-flow.md)  
[JavaScript Embed 샘플](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[PowerBI-CSharp Git 리포지토리](https://github.com/Microsoft/PowerBI-CSharp)  
[PowerBI-Node Git 리포지토리](https://github.com/Microsoft/PowerBI-Node)  
궁금한 점이 더 있나요? [Power BI 커뮤니티 hello를 시도 하십시오.](http://community.powerbi.com/)
