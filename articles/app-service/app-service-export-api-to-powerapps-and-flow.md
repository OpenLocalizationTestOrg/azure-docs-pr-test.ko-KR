---
title: "aaaExporting tooPowerApps Azure 호스팅 API 및 Microsoft Flow | Microsoft Docs"
description: "앱 서비스 tooPowerApps 및 Microsoft Flow에서 tooexpose API 호스트 하는 방법의 개요"
services: app-service
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 06/20/2017
ms.author: mahender
ms.openlocfilehash: 285b6efa3af5b0feac1ee2f617c0dc56dc3fd198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-an-azure-hosted-api-toopowerapps-and-microsoft-flow"></a>Azure 호스팅 API tooPowerApps 및 Microsoft Flow 내보내기

## <a name="creating-custom-connectors-for-powerapps-and-microsoft-flow"></a>PowerApps 및 Microsoft Flow를 위한 사용자 지정 커넥터

[PowerApps](https://powerapps.com) 빌드하고 tooyour 데이터 연결 플랫폼 간에 작동 하는 사용자 지정 비즈니스 응용 프로그램을 사용 하 여 하기 위한 서비스입니다. [Microsoft Flow](https://flow.microsoft.com) 쉽게 tooautomate 워크플로 및 즐겨 찾는 앱 및 서비스 간의 비즈니스 프로세스를 사용 하면 됩니다. PowerApps 및 Microsoft Flow 모두 다양 한 Office 365, Dynamics 365, Salesforce, 등과 같은 기본 제공 커넥터 toodata 소스 함께 제공 됩니다. 그러나 사용자가 toobe 수 tooleverage 데이터 원본 및 Api가 조직에서 만들어지는 있어야 합니다.

마찬가지로, 원하는 개발자는 tooexpose 더 광범위 하 게 hello 내 조직 경우가 toomake가 사용할 수 있는 tooPowerApps Api 및 Microsoft Flow 사용자가 해당 Api입니다. 이 항목 Azure 앱 서비스 또는 Azure 함수 tooPowerApps 및 Microsoft Flow API tooexpose 작성 하는 방법에 표시 됩니다. [Azure 앱 서비스](https://azure.microsoft.com/services/app-service/) 은 개발자가 tooquickly 및 쉽게 빌드 엔터프라이즈급 웹, 모바일 및 API 응용 프로그램 수 있는 플랫폼으로-서비스 제품입니다. [Azure 기능](https://azure.microsoft.com/services/functions/) 은 tooother 부분의 시스템 및 크기 조정 요구에 따라 반응할 수 tooquickly 작성자 코드를 허용 하는 서버가 없는 compute 이벤트 기반 솔루션입니다.

이러한 서비스에 대해 자세히 toolearn 참조:
- [PowerApps 학습 도우미](https://powerapps.microsoft.com/guided-learning/learning-introducing-powerapps/) 
- [Microsoft Flow 학습 도우미](https://flow.microsoft.com/guided-learning/learning-introducing-flow/)
- [App Service란?](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)
- [Azure Functions란?](https://docs.microsoft.com/azure/azure-functions/functions-overview)

## <a name="sharing-an-api-definition"></a>API 정의 공유

Api를 사용 하 여 것을 설명 되는 경우가 [OpenAPI 문서](https://www.openapis.org/) (tooas "Swagger" 문서 라고도 함). 이 작업은 사용할 수 있으며 hello 데이터 구성 방법에 대 한 hello 정보가 모두 포함 되어 있습니다. PowerApps 및 Microsoft Flow는 모든 OpenAPI 2.0 문서를 위한 사용자 지정 커넥터를 만들 수 있습니다. 정확 하 게 hello에서 사용할 수는 사용자 지정 커넥터를 만든 후 중 하 나와 동일한 방식으로 기본 제공 커넥터 hello 및 응용 프로그램에 신속 하 게 통합할 수 있습니다.

Azure App Service 및 Azure Functions는 OpenAPI 문서를 만들고, 호스트하고, 관리할 수 있는 [기본 지원](https://docs.microsoft.com/azure/app-service-api/app-service-api-metadata)을 제공합니다. 순서 toocreate 모바일 웹에 대 한 사용자 지정 커넥터, API 또는 함수 응용 프로그램, PowerApps 및 흐름 toobe hello 정의의 복사본을 지정 된 필요 합니다.

> [!NOTE]
> Hello API 정의의 복사본을 사용 하 고, PowerApps 및 Microsoft Flow 즉시에 대해 알지 못합니다 업데이트 또는 주요 변경 내용 toohello 응용 프로그램입니다. 새 버전의 hello API 제공할 경우 hello 새 버전을 위한 다음이 단계를 반복 해야 합니다. 

PowerApps tooprovide 및 응용 프로그램에 대 한 API 정의 호스트 하는 hello 사용 하 여 Microsoft 흐름에는 다음이 단계를 따르십시오.

1. 열기 hello [Azure 포털](https://portal.azure.com) tooyour Azure 함수 또는 앱 서비스 응용 프로그램을 이동 합니다.

    Azure 앱 서비스를 사용 하는 경우 선택 **API 정의** hello 설정 목록에서 합니다. 
    
    Azure Functions를 사용하는 경우 함수 앱을 선택한 다음 **플랫폼 기능**과 **API 정의**를 차례로 선택합니다. Tooopen hello 할 수도 **API 정의 (미리 보기)** 대신 탭 합니다.

2. API 정의 제공 하는 경우 표시 됩니다는 **tooPowerApps + Microsoft Flow 내보내기** 단추입니다. 이 단추 toobegin hello 내보내기 프로세스를 클릭 합니다.

3. 선택 hello **내보내기 모드**합니다. Toofollow toocreate 커넥터 해야 하는 hello 단계를 결정 합니다. App Service는 PowerApps 및 Microsoft Flow에 API 정의를 제공하기 위한 두 가지 옵션을 제공합니다.

    **Express** Azure 포털을 hello hello 사용자 지정 커넥터를 만들 수 있습니다. hello 만들어졌으므로 현재 사용 중인 로그인이 사용자는 권한을 toocreate 커넥터 hello 대상 환경에 필요 합니다. 이 hello 권장 접근법 해당 요구 사항을 충족 시킬 수 있습니다. 이 모드를 사용 하는 경우에 따라 hello [내보내기 Express](#express) 지침은 다음과 같습니다.

    **수동** hello API 정의입니다. PowerApps hello 또는 Microsoft Flow 포털을 사용 하 여 가져올 수 있는의 복사본을 내보낼 수 있습니다. 이 권장 접근법 hello Azure 사용자 및 권한 toocreate 커넥터가 있는 hello 사용자는 서로 다른 사람 또는 hello 커넥터는 다른 테 넌 트에서 만든 toobe 경우 hello입니다. 이 모드를 사용 하는 경우에 따라 hello [수동 내보내기 및 가져오기](#manual) 지침은 다음과 같습니다.

<a name="express"></a>
## <a name="express-export"></a>기본 내보내기

이 섹션에서는 hello Azure 포털 내에서 새로운 사용자 지정 커넥터를 만들게 됩니다. 로그인 해야 원하는 tooexport, 테 넌 트 toowhich hello에 하며 hello 대상 환경에서 사용자 지정 커넥터 권한을 toocreate를 있어야 합니다.

1. 원하는 toocreate hello 커넥터 hello 환경을 선택 하십시오. 그런 다음 사용자 지정 커넥터의 이름을 제공합니다.

2. API 정의에 보안 정의가 포함된 경우 2단계에서 보안 정의가 호출됩니다. 필요한 경우 hello 보안 구성 세부 정보 제공 toogrant 사용자 tooyour API에 액세스할 필요 합니다. 자세한 내용은 아래 [인증](#auth)을 참조하세요. 

3. 클릭 **확인** toocreate 사용자 지정 연결선입니다.


<a name="manual"></a>
## <a name="manual-export-and-import"></a>수동 내보내기 및 가져오기

순서 toocreate 모바일 웹에 대 한 사용자 지정 커넥터, API, 또는 함수 응용 프로그램에서는 두 단계가 필요 합니다.

1. [앱 서비스 또는 Azure 함수에서 hello API 정의 검색합니다.](#export)
2. [PowerApps 및 Microsoft 흐름으로 hello API 정의 가져오기](#import)

다음 두 단계 필요 함을 조직 내에서 서로 다른 사람이 수행한 toobe 지정된 된 사용자 수는 사용 하지 권한 tooperform 두 가지 동작 모두 것 같습니다. 이 경우 tooobtain hello API 정의 (단일 JSON 파일) 또는 링크 tooit는 개발자에 게 참가자 액세스 toohello Azure 함수 또는 앱 서비스 응용 프로그램에 필요 합니다. 그런 다음 해당 정의 tooa PowerApps 또는 Microsoft Flow 소유자 tooprovide를 해야 합니다. 해당 소유자는 hello 메타 데이터 toocreate hello 사용자 지정 커넥터를 사용할 수 있습니다.

<a name="export"></a>
### <a name="retrieving-hello-api-definition-from-app-service-or-azure-functions"></a>앱 서비스 또는 Azure 함수에서 hello API 정의 검색합니다.

이 섹션에서는 toobe hello PowerApps 또는 Microsoft Flow 포털에서 나중에 사용 되는 사용자 응용 프로그램 서비스 API에 대 한 hello API 정을 내보냅니다.

1. Tooeither를 선택할 수 있습니다 **hello API 정의 다운로드** 또는 **링크 받기**합니다. 선택한 위치가, hello 결과 hello 다음 섹션에 제공 됩니다. 이러한 옵션 중 하나를 선택 하 고 hello 지침을 따릅니다.
 
2. API 정의에 보안 정의가 포함된 경우 2단계에서 보안 정의가 호출됩니다. 가져오는 동안 PowerApps 및 Microsoft Flow가 보안 정의를 감지하고 보안 정보를 요청합니다. Hello 다음 섹션에서 사용 하기 위해 자격 증명 관련된 tooeach 정의 hello를 수집 합니다. 자세한 내용은 아래 [인증](#auth)을 참조하세요. 

<a name="import"></a>
### <a name="importing-hello-api-definition-into-powerapps-and-microsoft-flow"></a>PowerApps 및 Microsoft 흐름으로 hello API 정의 가져오기

이 섹션에서는 사용자 지정 커넥터 PowerApps 및 이전에 얻은 hello API 정의 사용 하 여 Microsoft Flow 만들게 됩니다. 사용자 지정 커넥터 hello 두 서비스에 한 번 tooimport hello 정의 하면 되므로 간에 공유 됩니다. 사용자 지정 커넥터에 대한 자세한 내용은 [등록 PowerApps에 사용자 지정 커넥터를 사용 하 고] 및 [등록 Microsoft 흐름에 사용자 지정 커넥터를 사용 하 고]을 참조하세요.

1. 열기 hello [Powerapps 웹 포털](https://web.powerapps.com) 또는 hello [Microsoft Flow 웹 포털](https://flow.microsoft.com/)에 로그인 합니다. 

2. Hello 클릭 **설정** hello 페이지 및 선택의 오른쪽 위에 hello에 있는 단추 (hello 기어 아이콘) **사용자 지정 커넥터**합니다. 

3. **사용자 지정 커넥터 만들기**를 클릭합니다.

4. Hello에 **일반** 탭, API에 대 한 이름을 제공 하 고 다음 hello OpenAPI 정의 업로드 하거나 hello 메타 데이터 URL에 붙여 넣습니다. **계속**을 클릭합니다.

4. Hello에 **보안** 탭, 입력 정보 요청된 tooprovide 인증 세부 정보를이 hello 이전 섹션에서 받은 hello 값을 입력 합니다. 파일이 없으면 toohello 다음 단계를 진행 합니다.

5. Hello에 **정의** 탭 OpenAPI 파일에 정의 된 모든 hello 작업은 자동으로 채워집니다. 필요한 모든 작업이 정의한 경우 속성이 toohello 다음 단계로 이동할 수 있습니다. 그렇지 않은 경우 여기에서 작업을 추가하고 수정할 수 있습니다.

6. **커넥터 만들기**를 클릭합니다. Tootest API 호출 하려는 경우 toohello 다음 단계로 이동 합니다.

7. Hello에 **테스트** 탭 연결을 만들 작업 tootest을 선택 하 고 hello 작업에 필요한 모든 데이터를 입력 합니다.

8. **작업 테스트**를 클릭합니다.


<a name="auth"></a>
## <a name="authentication"></a>인증

PowerApps 및 Microsoft Flow 기본적으로 사용자 지정 연결선의 사용자에 사용 되는 toolog 될 수 있는 id 공급자의 컬렉션을 지원 합니다. API에서 인증을 요구하는 경우 OpenAPI 문서에서 _보안 정의_로 캡처되었는지 확인합니다. 내보내기 중 PowerApps Microsoft Flow tooperform 로그인 동작을 허용 하는 tooprovide 구성 값이 필요 합니다.

이 섹션에서는 hello express 흐름에서 지원 되는 hello 인증 유형 설명: API 키, Azure Active Directory 및 제네릭 OAuth 2.0. 공급자 및 각 필요 hello 자격 증명의 전체 목록은 참조 하십시오. [등록 PowerApps에 사용자 지정 커넥터를 사용 하 고] 및 [등록 Microsoft 흐름에 사용자 지정 커넥터를 사용 하 고]합니다.

### <a name="api-key"></a>API 키
이 보안 체계를 사용 하는 경우 연결을 만들 때 커넥터의 hello 사용자가 입력 정보 요청된 tooprovide hello 키를 됩니다. 키가 필요한 알 하는 API 키 이름이 toohelp을 제공할 수 있습니다. Azure 함수에 대 한이 일반적으로 중 하나가 됩니다 hello 호스트 키를 hello 함수 앱 내에서 여러 함수를 포함 합니다.

### <a name="azure-active-directory"></a>Azure Active Directory
AAD 로그인 해야 하는 사용자 지정 커넥터를 구성할 때 AAD 응용 프로그램 등록이 두는 필요한: 하나의 toomodel hello 백 엔드 API와 PowerApps 및 흐름에서 첫 번째 toomodel hello 커넥터입니다.

API 구성된 toowork hello 첫 번째 등록에 속해 있어야 하며이 이미 처리 hello를 사용 하는 경우 [응용 프로그램 서비스 인증/권한 부여](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication) 기능입니다.

설명 하는 hello 단계를 사용 하 여 hello hello 커넥터에 대 한 두 번째 등록을 만드는 toomanually 갖습니다 [AAD 응용 프로그램 추가](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-an-application)합니다. hello 등록 toohave 위임 된 액세스 tooyour API와 필요한의 회신 URL `https://msmanaged-na.consent.azure-apim.net/redirect`합니다. 참조 하십시오 [이 예제](
https://powerapps.microsoft.com/tutorials/customapi-azure-resource-manager-tutorial/) 자세한 정보를 얻기 위해 hello Azure 리소스 관리자에 대 한 API를 대체 합니다.

다음 구성 값에는 hello 요소가 필요 합니다.
- **클라이언트 ID** -hello AAD 등록 커넥터의 클라이언트 ID
- **클라이언트 암호** -AAD 등록 커넥터의 hello 클라이언트 암호
- **로그인 URL** -hello AAD에 대 한 기준 URL입니다. 공용 Azure에서는 일반적으로 `https://login.windows.net`이 됩니다.
- **테 넌 트 ID** -hello hello 로그인에 사용 되는 hello 테 넌 트 toobe의 ID입니다. 이것을 "common", hello 커넥터 생성 되는 hello hello 테 넌 트의 ID입니다.
- **리소스 URL** -hello API 백 엔드 AAD 등록의 리소스 URL

> [!IMPORTANT]
> Tooprovide 할 경우 다른 작업자 가져오는 hello API 정의 PowerApps 및 Microsoft Flow hello 수동 흐름의 일환으로, 클라이언트 ID와 클라이언트 암호 hello 사용 하 여 **hello 커넥터 등록의**뿐만 hello API의 리소스 URL입니다. 이러한 비밀은 안전하게 관리해야 합니다. **Hello API 자체의 hello 보안 자격 증명을 공유 하지 않습니다.**

### <a name="generic-oauth-20"></a>제네릭 OAuth 2.0
hello 제네릭 OAuth 2.0 지원을 통해 모든 OAuth 2.0 공급자와 toointegrate 수 있습니다. 이렇게 하면 있습니다 toobring 기본적으로 지원 되지 않는 모든 사용자 지정 공급자에서.

다음 구성 값에는 hello 요소가 필요 합니다.
- **클라이언트 ID** -hello OAuth 2.0 클라이언트 ID
- **클라이언트 암호** -hello OAuth 2.0 클라이언트 암호
- **권한 부여 URL** -OAuth 2.0 권한 부여 URL hello
- **URL 토큰** -OAuth 2.0 토큰 URL hello
- **URL을 새로 고침** -OAuth 2.0 새로 고침 URL hello



[등록 PowerApps에 사용자 지정 커넥터를 사용 하 고]: https://powerapps.microsoft.com/tutorials/register-custom-api/
[등록 Microsoft 흐름에 사용자 지정 커넥터를 사용 하 고]: https://flow.microsoft.com/documentation/register-custom-api/
