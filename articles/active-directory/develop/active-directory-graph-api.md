---
title: aaaAzure Active Directory Graph API | Microsoft Docs
description: "프로그래밍 방식으로 허용 하는 그래프 API hello에 대 한 개요 및 빠른 시작 가이드는 REST API 끝점을 통해 tooAzure AD에 액세스 합니다."
services: active-directory
documentationcenter: 
author: viv-liu
manager: mbaldwin
editor: mbaldwin
ms.assetid: 5471ad74-20b3-44df-a2b5-43cde2c0a045
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: viviali
ms.custom: aaddev
ms.openlocfilehash: cde1dd86b0ca1dc24a5b46dc578b6245ba98751f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-graph-api"></a>Azure Active Directory Graph API
> [!IMPORTANT]
> 사용 하는 것이 좋습니다 [Microsoft Graph](https://graph.microsoft.io/) Azure AD Graph API tooaccess Azure Active Directory 리소스 대신 합니다. 이제 Microsoft는 Azure AD Graph API를 더 이상 개선하지 않을 것이며 Microsoft Graph에 주력하고 있습니다. 매우 제한 된 다양 한 시나리오를 Azure AD Graph API 여전히 것이 좋습니다. 자세한 내용은 참조 hello [Microsoft Graph 또는 Azure AD 그래프 hello](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) hello Office 개발자 센터의에서 블로그 게시물입니다.
> 
> 

hello Azure Active Directory Graph API는 REST API 끝점을 통해 프로그래밍 방식 액세스 tooAzure 광고를 제공합니다. 응용 프로그램에서는 hello Graph API tooperform 만들기, 읽기, 업데이트 및 삭제 (CRUD) 작업 디렉터리 데이터 및 개체에 있습니다. 예를 들어 hello Graph API는 사용자 개체에 대 한 일반적인 작업을 수행 하는 hello를 지원 합니다.

* 디렉터리에 새 사용자 만들기
* 소속 그룹과 같은 사용자의 자세한 속성 가져오기
* 해당 위치 및 전화번호와 같은 사용자의 속성을 업데이트 또는 암호 변경
* 역할 기반 액세스에 대한 사용자의 그룹 멤버 자격 확인
* 사용자의 계정 비활성화 또는 완전히 삭제

또한 toouser 개체에서 그룹 및 응용 프로그램 같은 다른 개체에 대 한 유사한 작업을 수행할 수 있습니다. Graph API에서 디렉터리를 hello 응용 프로그램에 Azure AD에 등록 해야 하 고 수 toocall hello tooallow toohello 디렉터리에 액세스를 구성 합니다. 이는 대개 사용자 또는 관리자 동의 흐름을 통해 수행됩니다.

Azure Active Directory Graph API hello toobegin를 사용 하 여 hello 참조 [Graph API 빠른 시작 가이드](active-directory-graph-api-quickstart.md), 또는 보기 hello [대화형 그래프 API 참조 설명서](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)합니다.

## <a name="features"></a>기능
Graph API hello를 hello를 같은 기능을 제공 합니다.

* **REST API 끝점**: hello Graph API는 표준 HTTP 요청을 사용 하 여 액세스할 수 있는 끝점으로 구성 하는 RESTful 서비스입니다. hello Graph API 요청 및 응답에 대 한 콘텐츠 형식을 XML 또는 JSON Javascript Object Notation ()를 지원합니다. 자세한 내용은 [Azure AD Graph REST API 참조](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)를 참조하세요.
* **Azure AD로 인증**: 모든 요청 toohello JSON 웹 토큰 (JWT) hello hello 요청의 권한 부여 헤더에 추가 하 여 Graph API 인증 되어야 합니다. 이 토큰은 요청 tooAzure AD의 토큰 끝점을 만들고이 유효한 자격 증명을 제공 하 여 가져옵니다. Hello OAuth 2.0 클라이언트 자격 증명 흐름을 사용할 수 있습니다 또는 hello 인증 코드 부여 흐름 tooacquire 토큰 toocall hello 그래프입니다. 자세한 내용은 [Azure AD의 OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx)을 참조하세요.
* **역할 기반 권한 부여 (RBAC)**: 보안 그룹은 hello Graph API에서에서 RBAC tooperform를 사용된 합니다. 예를 들어 toodetermine 사용자 액세스 tooa 특정 리소스에 있는지 여부, hello 응용 프로그램 수 호출 hello [그룹 구성원 확인 (전이적)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#FunctionsandactionsongroupsCheckmembershipinaspecificgrouptransitive) true 또는 false를 반환 하는 작업입니다.
* **차등 쿼리**: toomake 필요 없이 두 기간 간에 디렉터리의 변경 내용을 자주 사용 하는 쿼리 toohello Graph API에 대 한 toocheck를 원하는 경우에 차등 쿼리 요청을 만들 수 있습니다. 이 요청 유형은 이전 차등 쿼리 요청 hello와 hello 현재 요청 간에 hello 변경 된 내용만 반환 합니다. 자세한 내용은 [Azure AD Graph API 차등 쿼리](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-differential-query)를 참조하세요.
* **디렉터리 확장**: 디렉터리 개체에 대 한 고유한 속성 tooread 또는 쓰기 하는 응용 프로그램을 개발 하는 경우에 등록 고 hello Graph API를 사용 하 여 확장 값을 사용할 수 있습니다. 예를 들어, 각 사용자에 대 한 Skype ID 속성을 필요로 하는 응용 프로그램에 hello 디렉터리에 hello 새 속성을 등록 하 고 모든 사용자 개체에 사용할 수 있습니다. 자세한 내용은 [Azure AD Graph API Directory 스키마 확장](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)을 참조하세요.
* **사용 권한 범위에 의해 보안**: AAD Graph API는 클라이언트 응용 프로그램 형식을 비롯 한 다양 한 지원 및 tooAAD 데이터에 액세스 보안을 설정 하 고 승인할 수 있는 사용 권한 범위를 표시 합니다.
  
  * 권한 부여를 통해 toodata hello 로그인 한 사용자 (위임)에서 액세스 위임 제공 되는 사용자 인터페이스가 있는
  * 서비스/디먼 클라이언트와 같이 역할 기반 액세스 제어를 정의하는 응용 프로그램을 사용하는 클라이언트 앱 형식(앱 역할)
    
    둘 다 위임 및 응용 프로그램 역할 사용 권한 범위 hello Graph API에서 노출 하는 권한을 나타내고 응용 프로그램 등록 권한을 통해 클라이언트 응용 프로그램에서 요청할 수 [hello Azure 포털의에서 기능](https://portal.azure.com)합니다. 클라이언트는 hello 사용 권한 범위에 대 한 권한 위임된 hello 액세스 토큰에 받은 hello 범위 ("scp") 클레임을 검사 하 여 toothem를 부여 하 고 hello 역할 ("역할") 응용 프로그램 역할 사용 권한에 대 한 클레임을 확인할 수 있습니다. [Azure AD Graph API 사용 권한 범위](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes)에 대해 자세히 알아봅니다.

## <a name="scenarios"></a>시나리오
hello Graph API에는 많은 응용 프로그램 시나리오 수 있습니다. hello 다음 시나리오는 가장 일반적인 hello:

* **기간 업무(단일 테넌트) 응용 프로그램**: 이 시나리오에서는 엔터프라이즈 개발자는 Office 365를 구독하는 조직을 위해 업무를 수행합니다. hello 개발자 라이선스 tooa 사용자에 게 할당할 등의 Azure AD tooperform 작업 상호 작용 하는 웹 응용 프로그램을 만드는 중입니다. 이 작업에는 액세스 toohello Graph API를 hello 개발자는 Azure AD에서 hello 단일 테 넌 트 응용 프로그램을 등록 하 고 구성 되므로 읽기 및 쓰기 hello Graph API에 대 한 권한이 필요 합니다. 그런 다음 응용 프로그램을 hello이 구성 된 toouse는 자신의 자격 증명 또는 Graph API를 환영 hello 현재 로그인 한 사용자 tooacquire 토큰 toocall의 합니다.
* **서비스 응용 프로그램 같은 소프트웨어(다중 테넌트)**: 이 시나리오에서는 독립 소프트웨어 공급업체(ISV)는 Azure AD를 사용하는 다른 조직에 대한 사용자 관리 기능을 제공하는 호스팅 다중 테넌트 웹 응용 프로그램을 개발하고 있습니다. 이러한 기능을 toodirectory 개체에 액세스 해야 하 고 필요한 등을 hello 응용 프로그램 toocall hello Graph API 키를 누릅니다. hello 개발자 hello 응용 프로그램을 Azure AD에서 등록, toorequire 읽기를 구성 하 고 쓰기 hello Graph API에 대 한 권한 및 후 다른 조직이 해당 디렉터리에서 toouse hello 응용 프로그램에 동의할 수 있도록 외부 액세스를 가능 하도록 합니다. 다른 조직의 사용자가 처음으로 hello에 대 한 toohello 응용에 인증 하는 경우 hello 응용 프로그램이 요청 하는 hello 권한으로 승인 대화 상자를 표시 됩니다.  사용 권한 toohello Graph API hello 사용자의 디렉터리에 요청 된 부여 동의 hello 응용 프로그램에 제공 됩니다. Hello 승인 프레임 워크에 대 한 자세한 내용은 참조 하십시오. [hello 동의 프레임 워크 개요](active-directory-integrating-applications.md)합니다.

## <a name="see-also"></a>참고 항목
[Azure AD Graph API 빠른 시작 가이드](active-directory-graph-api-quickstart.md)

[AD Graph REST 설명서](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)

[Azure Active Directory 개발자 가이드](active-directory-developers-guide.md)

