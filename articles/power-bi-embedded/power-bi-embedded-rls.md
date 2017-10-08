---
title: "Power BI embedded aaaRow 수준 보안"
description: "Power BI Embedded를 사용하는 행 수준 보안에 대한 자세한 내용"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 7936ade5-2c75-435b-8314-ea7ca815867a
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 384f78826ecc710cf8f101b251ae68b074f3e98b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a>Power BI Embedded를 사용하는 행 수준 보안

행 수준 보안 (RLS)은 보고서 또는 수 있게 해 주는 여러 개의 서로 다른 사용자가 toouse hello 서로 다른 데이터를 보는 모든 동안 동일한 보고서 데이터 집합 내에서 사용 되는 toorestrict 사용자 액세스 tooparticular 데이터 수 있습니다. 이제 Power BI Embedded에서 RLS로 구성된 데이터 집합을 지원합니다.

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

Rls 순서 tootake 혜택에은에서 세 가지 주요 개념인; 이해 사용자, 역할 및 규칙입니다. 이러한 개념 각각에 대해 조금 더 자세히 살펴보겠습니다.

**사용자가** –이 hello 실제 최종 사용자가 보고서 보기. Power BI 포함에서 사용자가 응용 프로그램 토큰에 hello username 속성으로 식별 됩니다.

**역할** – 사용자가 속한 tooroles 합니다. 역할은 규칙에 대한 컨테이너로, "Sales Manager" 또는 "Sales Rep"와 같이 이름을 지정할 수 있습니다. Power BI 포함에서 사용자 앱 토큰에서 역할 속성 hello로 식별 됩니다.

**규칙** – 역할이 규칙 및 이러한 규칙은 적용 toobe toohello 데이터가는 hello 실제 필터입니다. "Country = USA"처럼 간단하거나 훨씬 동적일 수 있습니다.

### <a name="example"></a>예제

이 문서의 나머지 부분을 hello에 대 한 RLS를 작성 하 고 다음 포함 된 응용 프로그램 내에서 사용 하는 하의 예로 제공 됩니다. 예제 hello를 사용 하 여 [소매 분석 샘플](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX 파일입니다.

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

소매점 분석 샘플에서는 특정 소매점 체인에 모든 hello 상점의 판매를 보여 줍니다. RLS를 없이 어느 구역에 관계 없이 관리자가 로그인 하 고 뷰 hello 보고서를 볼 수 있습니다 hello 같은 데이터입니다. 경영 구역 관리자 각 판매 행만 볼 hello 관리 하는 hello 상점과 toodo에 대 한이 결정, RLS를 사용할 수 있습니다.

RLS는 Power BI Desktop으로 작성됩니다. Hello 데이터 집합 및 보고서를 열 때 toodiagram toosee hello 스키마 보기를 전환할 수 있습니다.

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

다음은이 스키마와 함께 몇 가지 toonotice가입니다.

* 모든 측정값 같은 **총 판매액**, hello에 저장 된 **Sales** 팩트 테이블입니다.
* **Item**, **Time**, **Store** 및 **District**의 추가 관련 차원 테이블이 있습니다.
* hello 관계선에 hello 화살표 어떤 방식으로 필터는 한 테이블 tooanother에서 흐를 수를 나타냅니다. 예를 들어, 필터에 배치 되 면 **시간 [Date]**, hello 현재 스키마에서 값 hello에 이르기까지 필터링만 것 **Sales** 테이블입니다. 다른 테이블이 없습니다 hello 관계 선 지점 toohello 판매 테이블에서를 제거 하지 hello 화살표의 모든 이후이 필터에 의해 영향을 받을 수 합니다.
* hello **구역** 테이블 각 지역에 대해 hello 관리자에 게 나타냅니다.
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

필터 toohello 적용이 스키마에 따라 **구역 관리자** 열에 hello 구역 테이블 및 해당 필터는 hello 다운도 필터링 하 고 해당 필터에서 일치 하는 hello 사용자 hello 보고서를 보는 경우 **저장소**및 **Sales** 테이블 tooonly 관리자는 특정 지역에 대 한 데이터를 표시 합니다.

방법을 알아보겠습니다.

1. Hello 모델링 탭을 클릭 **역할 관리**합니다.  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. **관리자**라는 새 역할을 만듭니다.  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. Hello에 **구역** 테이블에 다음 DAX 식은 hello 입력: **[구역 관리자] username () =**  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. hello에 toomake 있는지 hello 규칙에서 작업 하는 **모델링** 탭을 클릭 **역할로 보기**, hello 다음을 입력 합니다.  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   hello 보고서는 이제 표시로 로그인 한 경우 처럼 **Andrew Ma**합니다.

모든 레코드 hello에 이르기까지 필터링 됩니다 hello 필터, 여기에 수행한 hello 방식으로 적용 **구역**, **저장소**, 및 **Sales** 테이블입니다. 그러나 간의 hello 관계에 대 한 hello 필터 방향 인해 **Sales** 및 **시간**, **Sales** 및 **항목**, 및 **항목** 및 **시간** 테이블 아래로 필터링 되지 것입니다.

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

그러나이 요구 사항을 확인 될 수 있는, 않아도 판매 관리자 toosee 항목을 않도록 하는 경우 수 설정 양방향 교차 필터링 양방향에서 hello 관계 및 흐름 hello 보안 필터에 대 한 합니다. Hello 관계를 편집 하 여이 작업을 수행할 수 있습니다 **Sales** 및 **항목**, 다음과 같이 합니다.

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

이제 필터 진행 될 수도 있다는 hello Sales 테이블 toohello에서 **항목** 테이블:

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> DirectQuery 모드에 대 한 데이터를 사용 하는 경우 양방향 교차 필터링이 두 가지 옵션을 선택 하 여 tooenable 필요 합니다.

1. **파일** -> **옵션 및 설정** -> **미리 보기 기능** -> **DirectQuery에 대해 양방향 교차 필터링 활성화**.
2. **파일** -> **옵션 및 설정** -> **DirectQuery** -> **DirectQuery 모드에서 무제한 측정값 허용**.

양방향 교차 필터링, 다운로드 hello에 대 한 자세한 toolearn [양방향 교차 필터링 SQL Server Analysis Services 2016 및 Power BI Desktop에서](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) 백서입니다.

이것으로 toobe Power BI Desktop에서 수행 해야 하는 모든 hello 작업 마치 겠습니다 이지만 하나 더 많은 작업을 수행 하는 toobe toomake 필요한 hello RLS 규칙에서 Power BI 포함 작업을 정의 했습니다. 응용 프로그램 토큰은 사용 되는 toogrant 및 사용자를 인증 하 고 응용 프로그램의 승인을 해당 사용자 액세스 tooa 특정 Power BI 포함 보고서입니다. Power BI Embedded는 사용자가 누구인지에 대한 어떠한 특정한 정보도 포함하지 않습니다. RLS toowork에 대 한 응용 프로그램 토큰의 일부로 toopass에 일부 추가 컨텍스트가 필요 합니다.

* **사용자 이름** (선택 사항) –이 사용할 수 있는 문자열로 RLS로 사용 되는 RLS 규칙을 적용할 때 toohelp hello 사용자를 식별 합니다. Power BI Embedded를 사용하는 행 수준 보안 사용을 참조하세요.
* **역할** – 행 수준 보안 규칙을 적용할 때 hello 역할 tooselect를 포함 하는 문자열입니다. 둘 이상의 역할을 전달하는 경우 문자열 배열로 전달해야 합니다.

Hello를 사용 하 여 hello 토큰을 만들면 [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) 메서드. Hello 사용자 이름 속성이 있으면 역할에 하나 이상의 값을 전달할 수도 해야 합니다.

예를 들어 hello EmbedSample 변경할 수 있습니다. DashboardController 줄 55는 다음과 같이 업데이트할 수 있습니다.

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

to

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

hello 전체 응용 프로그램 토큰에는 다음과 같이 표시 됩니다.

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

이제 모든 hello 조각을 함께와이 보고서는 응용 프로그램 tooview에는 사용자 로그인 할 때만 할 것 수 toosee hello 데이터 toosee, 허용 되는 행 수준 보안에 정의 된 대로 합니다.

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a>참고 항목

[Power를 사용하는 RLS(행 수준 보안)](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[Power BI Embedded에서 인증 및 권한 부여](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[JavaScript Embed 샘플](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
궁금한 점이 더 있나요? [Power BI 커뮤니티 hello를 시도 하십시오.](http://community.powerbi.com/)

