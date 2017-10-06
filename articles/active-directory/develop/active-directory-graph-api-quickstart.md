---
title: "hello Azure AD Graph API에 대 한 aaaQuickstart | Microsoft Docs"
description: "hello Azure Active Directory Graph API는 OData REST API 끝점을 통해 프로그래밍 방식 액세스 tooAzure 광고를 제공합니다. 응용 프로그램에서는 hello Graph API tooperform 만들기, 읽기, 업데이트 및 삭제 (CRUD) 작업 디렉터리 데이터 및 개체에 있습니다."
services: active-directory
documentationcenter: n/a
author: viv-liu
manager: mbaldwin
editor: 
tags: 
ms.assetid: 9dc268a9-32e8-402c-a43f-02b183c295c5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: viviali
ms.custom: aaddev
ms.openlocfilehash: b4d3c57f06d212b1d095578f19bb86c932dbcc33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-hello-azure-ad-graph-api"></a>Hello Azure AD Graph API에 대 한 빠른 시작
hello Azure AD (Active Directory) Graph API는 OData REST API 끝점을 통해 프로그래밍 방식 액세스 tooAzure 광고를 제공합니다. 응용 프로그램에서는 hello Graph API tooperform 만들기, 읽기, 업데이트 및 삭제 (CRUD) 작업 디렉터리 데이터 및 개체에 있습니다. 예를 들어 있습니다 수 hello Graph API toocreate 새 사용자 보기를 사용 하 여 또는 사용자의 속성을 업데이트, 사용자의 암호 변경, 역할 기반 액세스, 사용 안 함, 또는 delete hello 사용자에 대 한 그룹 구성원 자격을 확인 합니다. Hello Graph API 기능 및 응용 프로그램 시나리오에 대 한 자세한 내용은 참조 하십시오. [Azure AD Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) 및 [Azure AD Graph API 필수 구성 요소](https://msdn.microsoft.com/library/hh974476.aspx)합니다. 

> [!IMPORTANT]
> 사용 하는 것이 좋습니다 [Microsoft Graph](https://developer.microsoft.com/graph) Azure AD Graph API tooaccess Azure Active Directory 리소스 대신 합니다. 이제 Microsoft는 Azure AD Graph API를 더 이상 개선하지 않을 것이며 Microsoft Graph에 주력하고 있습니다. 매우 제한 된 다양 한 시나리오를 Azure AD Graph API 여전히 것이 좋습니다. 자세한 내용은 참조 hello [Microsoft Graph 또는 Azure AD 그래프 hello](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) hello Office 개발자 센터의에서 블로그 게시물입니다.
> 
> 

## <a name="how-tooconstruct-a-graph-api-url"></a>어떻게 tooconstruct Graph API URL
Graph API, tooaccess 디렉터리 데이터 및 개체 (즉, 리소스 또는 엔터티) tooperform CRUD 작업의 대상이 될에서는 hello OData (개방형 데이터) 프로토콜에 따라 Url을 사용할 수 있습니다. hello Graph API에서 사용 되는 Url 이루어져 네 가지 주요 부분: 서비스 루트, 테 넌 트 식별자, 리소스 경로 및 쿼리 문자열 옵션: `https://graph.windows.net/{tenant-identifier}/{resource-path}?[query-parameters]`합니다. Hello url의 hello 예로 들어 보겠습니다: `https://graph.windows.net/contoso.com/groups?api-version=1.6`합니다.

* **서비스 루트**: Azure AD Graph Api에서 hello 서비스 루트는 항상 https://graph.windows.net입니다.
* **테 넌 트 식별자**:이 섹션에는 hello 예제에서는 앞에서 확인 된 (등록 된) 도메인 이름, 수 contoso.com입니다. 일 수도 있습니다는 테 넌 트 개체 ID 또는 hello "myorganization" 또는 "me" 별칭입니다. 자세한 내용은 참조 [hello Graph API에서에서 엔터티 주소 지정 및 작업](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-operations-overview)).
* **리소스 경로**: hello 리소스를 식별 하는이 섹션의 URL (사용자, 그룹, 특정 사용자 또는 특정 그룹 등.)와 상호 작용할 toobe 위의 hello 예제에서 해당 리소스 집합 hello 최상위 "그룹" tooaddress입니다. 특정 엔터티 주소를 지정할 수도 있습니다(예: "users/{objectId}" 또는 "users/userPrincipalName").
* **쿼리 매개 변수**: hello 리소스 경로 섹션과 hello 쿼리 매개 변수 섹션을 구분 하는 물음표 (?). hello "api-version" 쿼리 매개 변수 hello Graph API의에서 모든 요청에 필요 합니다. hello Graph API에서는 다음 OData 쿼리 옵션 hello: **$filter**, **$orderby**, **$expand**, **$top**, 및 **$format**합니다. 다음 쿼리 옵션 hello 현재 지원 되지 않습니다: **$count**, **$inlinecount**, 및 **$skip**합니다. 자세한 내용은 [Azure AD Graph API에서 지원되는 쿼리, 필터 및 페이징 옵션](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-supported-queries-filters-and-paging-options)을 참조하세요.

## <a name="graph-api-versions"></a>Graph API 버전
Hello "api-version" 쿼리 매개 변수에서 Graph API 요청에 대 한 hello 버전을 지정 합니다. 버전 1.5 이상의 경우 숫자 버전 값 api-version=1.6을 사용합니다. Toohello 형식 YYYY-월-일; 준수는 날짜 문자열을 사용 하면 이전 버전에 대 한 예를 들어 api-version = 2013-11-08입니다. 미리 보기 기능에 대 한 "beta"; hello 문자열을 사용 하 여 예를 들어 api-version = beta 합니다. Graph API 버전 간의 차이점에 대한 자세한 내용은 [Azure AD Graph API 버전 관리](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-versioning)를 참조하세요.

## <a name="graph-api-metadata"></a>Graph API 메타데이터
tooreturn hello Graph API 메타 데이터 파일을 뒤에 추가 "$metadata" hello 세그먼트 hello 테 넌 트 식별자 hello에 대 한 URL 예 hello 데모 회사에 대 한 반환 메타 데이터 URL을 따라: `https://graph.windows.net/GraphDir1.OnMicrosoft.com/$metadata?api-version=1.6`합니다. 웹 브라우저 toosee hello 메타 데이터의 hello 주소 표시줄에이 URL을 입력할 수 있습니다. hello 반환 되는 CSDL 메타 데이터 문서에 설명 hello 엔터티 및 복합 형식, 속성 및 hello 함수 및 hello 버전 요청한 Graph API에서 노출 하는 동작입니다. Hello api-version 매개 변수를 생략 하면 hello 가장 최신 버전에 대 한 메타 데이터를 반환 합니다.

## <a name="common-queries"></a>일반 쿼리
[Azure AD Graph API 일반 쿼리](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-supported-queries-filters-and-paging-options#CommonQueries) hello 디렉터리에서 디렉터리 및 쿼리 tooperform 작업의 최상위 리소스에 사용 되는 tooaccess 일 수 있는 쿼리를 포함 하 여 Azure AD Graph를 함께 사용할 수 있는 일반적인 쿼리가 나와 있습니다.

예를 들어 `https://graph.windows.net/contoso.com/tenantDetails?api-version=1.6` 는 contoso.com 디렉터리에 대한 회사 정보를 반환합니다.

또는 `https://graph.windows.net/contoso.com/users?api-version=1.6` hello contoso.com 디렉터리의에서 모든 사용자 개체를 나열 합니다.

## <a name="using-hello-graph-explorer"></a>Hello 그래프 탐색기를 사용 하 여
응용 프로그램을 빌드할 때 hello Azure AD Graph API tooquery hello 디렉터리 데이터에 대 한 hello 그래프 탐색기를 사용할 수 있습니다.

hello 다음은 hello 출력 toonavigate toohello 그래프 탐색기 경우 확인할에 로그인 하는 입력 `https://graph.windows.net/GraphDir1.OnMicrosoft.com/users?api-version=1.6` toodisplay 모든 hello에 대 한 사용자가 로그인 한 사용자의 디렉터리 hello:

![Azure AD Graph API Explorer](./media/active-directory-graph-api-quickstart/graph_explorer.png)

**그래프 탐색기 로드 hello**: tooload hello 도구를 너무 탐색[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/)합니다. 클릭 **로그인** 및 사용 하 여 로그인 하면 Azure AD 계정 자격 증명 toorun 테 넌 트에 대해 그래프 탐색기 hello 합니다. 자신의 테 넌 트에 대해 그래프 탐색기를 실행 하면 사용자 또는 관리자 중 하나에 로그인 시 tooconsent이 필요 합니다. Office 365 구독이 있는 경우 Azure AD 테넌트를 자동으로 보유합니다. 실제로 toosign tooOffice 365에서에서 사용 하 여 hello 자격 증명은, Azure AD 계정 및 있습니다 그래프 탐색기에 이러한 자격 증명을 사용할 수 있습니다.

**쿼리 실행**: toorun 쿼리를 클릭 하 고 hello 요청 텍스트 상자에 쿼리를 입력 **가져오기** hello 키를 누르거나 **입력** 키입니다. hello 결과 hello 응답 상자에 표시 됩니다. 예를 들어 `https://graph.windows.net/myorganization/groups?api-version=1.6` hello 로그인 한 사용자의 디렉터리에 있는 모든 그룹 개체를 나열 합니다.

참고 hello hello 그래프 탐색기의 기능과 제한은 다음:

* 리소스 집합에 대한 자동 완성 기능. toosee hello 클릭이이 기능을 요청 텍스트 상자 (여기서 hello 회사 URL 나타남). 리소스 집합 hello 드롭다운 목록에서 선택할 수 있습니다.
* 지원 "me" 및 "myorganization" 주소 지정 별칭 hello 합니다. 사용할 수는 예를 들어 `https://graph.windows.net/me?api-version=1.6` hello 로그인 한 사용자의 tooreturn hello 사용자 개체 또는 `https://graph.windows.net/myorganization/users?api-version=1.6` tooreturn hello 현재 디렉터리의 모든 사용자입니다.
* 응답 헤더 섹션입니다. 이 섹션을 사용할 수 있습니다 toohelp 쿼리를 실행할 때 발생 하는 문제를 해결 합니다.
* 확장 및 축소 기능이 있는 hello 응답 용 JSON 뷰어가 제공 합니다.
* 축소판 사진 표시를 지원하지 않습니다.

## <a name="using-fiddler-toowrite-toohello-directory"></a>Fiddler toowrite toohello 디렉터리를 사용 하 여
이 빠른 시작 가이드를 하기 위해 hello에 대 한 '쓰기' Azure AD 디렉터리에 대 한 작업을 수행 하는 hello Fiddler Web Debugger toopractice를 사용할 수 있습니다. 자세한 내용과 tooinstall Fiddler에 대 한 참조 [http://www.telerik.com/fiddler](http://www.telerik.com/fiddler)합니다.

Hello 아래 예제에서는 Fiddler Web Debugger toocreate 새 보안 그룹 'MyTestGroup'를 사용 하 여 Azure AD 디렉터리에 있습니다.

**액세스 토큰을 가져올**: Azure AD 그래프 tooaccess 클라이언트는 필요한 toosuccessfully 먼저 tooAzure AD를 인증 합니다. 자세한 내용은 [Azure AD의 인증 시나리오](active-directory-authentication-scenarios.md)를 참조하세요.

**작성 하 고 쿼리를 실행할**: 다음 단계 완료 hello:

1. Fiddler Web Debugger를 열고 toohello 전환 **작성기** 탭 합니다.
2. 새 보안 그룹 toocreate 지정할 것 이므로 선택 **Post** hello hello 풀 다운 메뉴에서 HTTP 방법으로 합니다. 그룹 개체에 작업 및 사용 권한에 대 한 자세한 내용은 참조 하십시오. [그룹](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#GroupEntity) hello 내 [Azure AD 그래프 REST API 참조](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)합니다.
3. Hello 필드에 다음 너무**Post**, 요청 URL hello hello 다음에서 입력: `https://graph.windows.net/mytenantdomain/groups?api-version=1.6`합니다.
   
   > [!NOTE]
   > Mytenantdomain은 사용 중인 자신의 Azure AD 디렉터리의 hello 도메인 이름으로 대체 해야 합니다.
   > 
   > 
4. 게시 풀 다운 바로 아래 필드 hello에에서 hello 다음을 입력 합니다.
   
    ```
   Host: graph.windows.net
   Authorization: Bearer <your access token>
   Content-Type: application/json
   ```
   
   > [!NOTE]
   > 대체 프로그램 &lt;액세스 토큰&gt; Azure AD 디렉터리에 대 한 hello 액세스 토큰으로 합니다.
   > 
   > 
5. Hello에 **요청 본문** 필드 hello 다음을 입력 합니다.
   
    ```
        {
            "displayName":"MyTestGroup",
            "mailNickname":"MyTestGroup",
            "mailEnabled":"false",
            "securityEnabled": true
        }
   ```
   
    그룹을 만드는 방법에 대한 자세한 내용은 [그룹 만들기](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#CreateGroup)를 참조하세요.

Azure AD 엔터티 및 그래프에 의해 노출 되는 형식에 대 한 자세한 내용 및 그래프와 연산을 수행할 수 있는 hello 작업에 대 한 정보에 대 한 참조 [Azure AD 그래프 REST API 참조](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)합니다.

## <a name="next-steps"></a>다음 단계
* Hello에 대 한 자세한 [Azure AD Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)
* [Azure AD Graph API 사용 권한 범위](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes)

