---
title: "Mobile Engagement REST Api와 aaaAuthenticate"
description: "설명 방법을 tooauthenticate Azure Mobile Engagement REST Api와"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: da82cb36-957a-4e19-a805-b44733cf6597
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 9b54aa5ec3da4bcf55ffe5b7e8d1759095d0c486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a>Mobile Engagement REST API를 사용한 인증
## <a name="overview"></a>개요
이 문서에서는 tooget 유효한 AAD Oauth hello Mobile Engagement REST Api로 tooauthenticate 토큰 하는 방법을 설명 합니다. 

여러분이 유효한 Azure 구독을 보유하고 있고 [개발자 자습서](mobile-engagement-windows-store-dotnet-get-started.md)중 하나를 사용하여 Mobile Engagement 앱을 만들었다고 가정합니다.

## <a name="authentication"></a>인증
Microsoft Azure Active Directory 기반 OAuth 토큰을 사용하여 인증합니다. 

주문 tooauthentication API 요청에 권한 부여 헤더 hello 다음 폼의 tooevery 요청을 추가 해야 합니다.

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> Azure Active Directory 토큰은 1시간 후에 만료됩니다.
> 
> 

토큰은 몇 가지 방법으로 tooget 합니다. Api는 일반적으로 클라우드 서비스에서 호출 하는 hello, 이후 toouse API 키 할 수 있습니다. Azure 용어에서는 API 키를 서비스 주체 암호라고 부릅니다. hello 다음 절차에서는 한 가지 방법은 toosetting 것 수동으로 위로 합니다.

### <a name="one-time-setup-using-script"></a>일 회 설정(스크립트 사용)
Hello 일련의 설치에 대 한 최소 시간 hello 걸리지만 hello 가장 허용 가능한 기본값을 사용 하는 PowerShell 스크립트를 사용 하 여 tooperform hello 설정 아래 지침을 따라야 합니다. 필요에 따라 있습니다 수 또한 hello 지침에에서 따라 hello [수동 설치](mobile-engagement-api-authentication-manual.md) hello Azure 포털에 직접 및 do 더욱 세밀 하 게 구성에서 이러한 작업에 대 한 합니다. 

1. PowerShell에서 Azure의 hello 최신 버전 가져오기 [여기](http://aka.ms/webpi-azps)합니다. Hello 다운로드 명령에 대 한 자세한 내용은 볼 수 있습니다 [링크](/powershell/azure/overview)합니다.  
2. 사용 하 여 hello 다음 hello 있다고 tooensure 명령을 Azure PowerShell 설치 되 면 **Azure 모듈** 설치:
   
    a. Hello Azure PowerShell 모듈을 사용할 수 있는 모듈의 hello 목록에서 사용할 수 있는지 확인 합니다. 
   
        Get-Module –ListAvailable 
   
    ![사용 가능한 Azure 모듈][1]
   
    b. 목록 위의 hello에 hello Azure PowerShell 모듈을 찾지 못한 경우 toorun hello 다음이 필요 합니다.
   
        Import-Module Azure 
3. 로그인 toohello PowerShell에서 Azure 리소스 관리자를 실행 하 여 Azure 계정에 대 한 사용자 이름 및 암호를 제공 하 고 다음 명령을 hello: 
   
        Login-AzureRmAccount
4. 여러 구독이 있는 경우 hello 다음을 실행 해야 합니다.
   
    a. 모든 구독 및 복사 hello 원하는 hello 구독의 구독 Id의 목록을 toouse를 가져옵니다. 이 구독에는 Mobile Engagement 앱 hello 갖는 동일 hello 인지 확인 사용 하 여 toointeract hello Api입니다. 
   
        Get-AzureRmSubscription
   
    b. 실행된 hello 다음 명령은 사용 제공 hello SubscriptionId tooconfigure hello 구독 toobe 합니다.
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. Hello에 대 한 hello 텍스트 복사 [새로 AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) tooyour 로컬 컴퓨터를 스크립트 및 PowerShell cmdlet으로 저장 (예: `APIAuth.ps1`) 하 고 실행 `.\APIAuth.ps1`합니다. 
6. hello 스크립트 묻는 메시지가 나타납니다에 대 한 입력은 tooprovide **principalName**합니다. 되도록 toouse toocreate Active Directory 응용 프로그램 (예: APIAuth) 적절 한 이름을 제공 합니다. 
7. Hello 다음 해야 하는 4 개의 값이 표시 됩니다 hello 스크립트를 완료 한 후 tooauthenticate AD 사용한 프로그래밍 방식으로 만들어지므로 toocopy 있는지를 확인 하 합니다. 
   
    **TenantId**, **SubscriptionId**, **ApplicationId** 및 **Secret**입니다.
   
    TenantId를 `{TENANT_ID}`로, ApplicationId `{CLIENT_ID}`로, Secret을 `{CLIENT_SECRET}`으로 사용합니다.
   
   > [!NOTE]
   > PowerShell 스크립트를 실행할 수 없도록 기본 보안 정책이 설정되었을 수 있습니다. 따라서 일시적으로 구성한 경우 다음 명령을 hello를 사용 하 여 실행 정책 tooallow 스크립트 실행:
   > 
   > Set-ExecutionPolicy RemoteSigned
   > 
   > 
8. 같은 PS cmdlet 집합이 hello 모양을 다음과 같습니다. 
   
    ![][3]
9. 새 AD 응용 프로그램 만들어졌는지 hello 이름의 있습니다 toohello 스크립트 호출 제공 hello Azure 관리 포털에서 확인 **principalName** 아래 **회사가 보유 한 응용 프로그램 표시**합니다.
   
    ![][4]

#### <a name="steps-tooget-a-valid-token"></a>단계 tooget 유효한 토큰
1. 매개 변수 뒤 hello로 hello API를 호출 하 고 있는지 tooreplace hello 테 넌 트\_ID, 클라이언트\_ID와 클라이언트\_암호:
   
   * **요청 URL** *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*
   * **application/x-www-form-urlencoded** 인 *HTTP 콘텐츠 형식 헤더*
   * **HTTP 요청 본문** *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*
     
     hello 다음은 예제 요청입니다.
     
       POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F
     
     다음은 응답 예제입니다.
     
       HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234
     
       {"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}
     
     이 예제에서는 hello POST 매개 변수의 URL 인코딩을 포함 `resource` 값이 실제로 `https://management.core.windows.net/`합니다. Tooalso URL 인코딩할 조심 `{CLIENT_SECRET}` 으로 특수 문자를 포함할 수 있습니다.
     
     > [!NOTE]
     > 테스트를 위해 [Fiddler](http://www.telerik.com/fiddler) 또는 [Chrome Postman 확장](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)과 같은 HTTP 클라이언트 도구를 사용할 수 있습니다. 
     > 
     > 
2. 이제 모든 API 호출에서 hello 권한 부여 요청 헤더를 포함 합니다.
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    반환 401 상태 코드 검사 hello 응답 본문을 발생 하는 경우 것 알려 hello 토큰이 만료 되었습니다. 토큰이 만료된 경우 새 토큰을 가져옵니다.

## <a name="using-hello-apis"></a>Hello Api를 사용 하 여
유효한 토큰을가지고 준비 toomake hello API 호출 됩니다.

1. 각 API 요청 toopass hello 이전 섹션에서 받은 되는 유효 하 고 만료 되지 않은 토큰을 해야 합니다.
2. 일부 매개 변수에서 tooplug hello 요청 응용 프로그램을 식별 하는 URI에 필요 합니다. hello 요청 URI hello 다음과 같습니다.
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    tooget hello 매개 변수를 응용 프로그램 이름을 클릭 하 고 대시보드를 클릭 하 고 모든 hello 다음 3 개의 매개 변수를 hello와 같은 페이지가 표시 됩니다.
   
   * **1** `{subscription-id}`
   * **2** `{app-collection}`
   * **3** `{app-resource-name}`
   * **4** your 리소스 그룹 이름은 toobe 되기 **MobileEngagement** 만들지 않은 경우 새 합니다. 
     
     ![Mobile Engagement API URI 매개 변수][2]

> [!NOTE]
> <br/>
> 
> 1. 이 hello에 대 한 API 루트 주소 hello 무시 이전 Api입니다.<br/>
> 2. Azure 클래식 포털을 사용 하 여 hello 응용 프로그램을 만든 경우 hello 응용 프로그램 이름 자체 보다 다른 toouse hello 응용 프로그램 리소스 이름이 필요 합니다. Hello 앱 hello Azure 포털에서에서 만든 경우 응용 프로그램 이름 (응용 프로그램 리소스 이름 및 hello 새로운 포털에서 만든 앱에 대 한 응용 프로그램 이름 구분 되지 않습니다는) 자체 hello를 사용 해야 합니다.  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



