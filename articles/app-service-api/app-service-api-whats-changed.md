---
title: "서비스 API 앱-변경 내용 aaaApp | Microsoft Docs"
description: "Azure 앱 서비스의 API 앱에 대한 새로운 기능을 알아봅니다."
services: app-service\api
documentationcenter: .net
author: mohitsriv
manager: erikre
editor: tdykstra
ms.assetid: a9b58066-e8fd-48b8-a651-4613b1736433
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: rachelap
ms.openlocfilehash: 79df54f1dae91d7c5d3b66d208d0d1c1d7d55ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-api-apps---whats-changed"></a>앱 서비스 API 앱 - 변경된 내용
2015 년 11 월에에서 대해서는 hello connect () 이벤트, 다양 한 개선 사항 tooAzure 앱 서비스 된 [발표](https://azure.microsoft.com/blog/azure-app-service-updates-november-2015/)합니다. ± Â ´이 é 기본 변경 tooAPI 앱 toobetter 모바일 및 웹 응용 프로그램에 맞춰, 개념 수 줄이는 및 배포와 런타임 성능을 향상 시킵니다. 2015 년 11 월 30 일 새로운 API 앱 시작 hello Azure 관리 포털을 사용 하 여 만들거나 hello 최신 도구에는 이러한 변경 내용이 반영 됩니다. 이 문서에서는 방법과 이러한 변경 내용을 설명 tooredeploy 기존 앱 tootake hello 기능 이용 합니다.

## <a name="feature-changes"></a>기능 변경
API 앱 – 인증, CORS 및 API 메타 데이터의 주요 기능 hello-응용 프로그램 서비스에 직접 이동 합니다. 이러한 변경으로 인해 hello 기능을 웹, 모바일 및 API 앱에서 사용할 수 있습니다. 사실, 모두 세 개의 공유 hello 동일 **Microsoft.Web/sites** 리소스 관리자의 리소스 종류입니다. hello API 앱은 더 이상 필요 게이트웨이나 API 앱으로 제공 되 고 없습니다. 이 인해 더 쉽게 toouse Azure API 관리 방금 hello 단일 API 관리 게이트웨이 됩니다.

![API 앱 개요](./media/app-service-api-whats-changed/api-apps-overview.png)

API 앱을 업데이트 하는 hello로 중요 한 설계 원칙은 tooenable toobring 선택한 언어의으로 API가 있습니다.  사용자가 API는 웹 응용 프로그램 또는 모바일 앱으로 이미 배포 된 경우 없는 tooredeploy hello 새로운 기능의 앱 tootake 있다는 이점이 있습니다. 현재 API 앱 미리 보기를 사용하는 경우 자세한 내용은 아래의 마이그레이션 지침을 참조하세요.

### <a name="authentication"></a>인증
hello 기존 턴키 API 앱, 모바일 서비스/응용 프로그램 및 웹 앱 인증 통합 되었습니다 기능과 hello 관리 포털에서 단일 Azure 앱 서비스 인증 블레이드에서 사용할 수 있습니다. 앱 서비스에서 소개 tooauthentication 서비스에 대 한 참조 [확장 응용 프로그램 서비스 인증 / 권한 부여](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)합니다.

API 시나리오의 경우 관련된 여러 가지 새로운 기능이 있습니다.

* **Azure Active Directory를 사용 하 여 직접에 대 한 지원**, tooexchange hello AAD 토큰 세션 토큰에 대 한 클라이언트 코드 없이: 클라이언트에 포함할 수 hello AAD 토큰 hello 인증 헤더에 toohello 전달자 토큰에 따라 사양입니다. 즉, 클라이언트 또는 서버 쪽 hello에 없는 응용 프로그램 서비스 관련 SDK가 필요 합니다. 
* **서비스 간 또는 "내부" 액세스**: AAD 서비스 계정을 사용 하는 토큰을 요청 하 고 인증에 대 한 서비스 tooApp 전달 수 데몬 프로세스 또는 다른 클라이언트 인터페이스 없이 tooAPIs 액세스를 필요로 하는 경우와 사용자 응용 프로그램입니다.
* **권한 부여를 지연**: 대부분의 응용 프로그램에는 hello 응용 프로그램의 다른 부분에 대 한 다양 한 액세스 제한 사항이 있습니다. 일조량 로그인도 있을 공개적으로 사용할 수 있는 몇 가지 Api toobe를 정하도록 있습니다. 로그인을 필요로 하는 hello 전체 사이트와 hello 원래 인증/권한 부여 기능은 전부 아니면 전무, 했습니다. 이 옵션은 계속 존재 하지만 허용할 수 있습니다 또는 응용 프로그램 코드 toorender 액세스 결정 앱 서비스 hello 사용자가 인증 후 합니다.

Hello 새로운 인증 기능에 대 한 자세한 내용은 참조 [인증 및 Azure 앱 서비스에서 API 앱에 대 한 권한 부여](app-service-api-authentication.md)합니다. Toomigrate hello 이전 API 앱에서 기존 API 앱 toohello 새 하나, 참조를 모델링 하는 방법에 대 한 내용은 [마이그레이션 기존 API 앱](#migrating-existing-api-apps) 이 문서의 뒷부분에 나오는 합니다.

### <a name="cors"></a>CORS
쉼표로 구분 하 여 대신 **MS_CrossDomainOrigins** 응용 프로그램 설정을 이제 블레이드 CORS를 구성 하기 위한 hello Azure 관리 포털. 또는 Azure PowerShell, CLI, [리소스 탐색기](https://resources.azure.com/)등의 리소스 관리자 도구를 사용하여 구성할 수 있습니다. 집합 hello **cors** hello 속성 **Microsoft.Web/sites/config** 리소스 종류에 대 한 프로그램  **&lt;사이트 이름&gt;/웹** 리소스입니다. 예:

    {
        "cors": {
            "allowedOrigins": [
                "https://localhost:44300"
            ]
        }
    } 

### <a name="api-metadata"></a>API 메타데이터
API 정의 블레이드 hello 웹, 모바일 및 API 앱에서 출시 되었습니다. Hello 관리 포털에서 상대 url 또는 API의 호스트 Swagger 2.0 표현을 tooan 끝점을 가리키는 절대 url을 지정할 수 있습니다. 또는 리소스 관리자 도구를 사용하여 구성할 수 있습니다. 집합 hello **apiDefinition** hello 속성 **Microsoft.Web/sites/config** 리소스 종류에 대 한 프로그램  **&lt;사이트 이름&gt;/웹** 리소스입니다. 예:

    {
        "apiDefinition":
        {
            "url": "https://myStorageAccount.blob.core.windows.net/swagger/apiDefinition.json"
        }
    }

이때 hello 메타 데이터 끝점 요구에 toobe 인증 없이 공개적으로 액세스할 수 있는 많은 다운스트림 클라이언트 (예: Visual Studio REST API 클라이언트 생성 및 PowerApps "API 추가" 흐름) tooconsume 것입니다. 이 hello 경로 tooyour Swagger 메타 데이터가 공개 되도록 앞에서 설명한 toouse hello 지연 인증 옵션 할 앱 서비스 인증을 사용 하 고 자체 응용 프로그램 내에서 tooexpose hello API 정의 사용할 경우를 의미 합니다.

## <a name="management-portal"></a>관리 포털
선택 하면 **새로 만들기 > 웹 + 모바일 > API 앱** hello 포털 hello 문서에서 설명 하는 hello 새로운 기능을 반영 하는 API 앱 만듭니다. **찾아보기 > API 앱**은 이러한 새 API 앱만 표시합니다. API 앱에 검색 되 면 동일한 레이아웃 및 기능으로 웹 및 모바일 앱의 hello 블레이드 공유 hello 합니다. hello 유일한 차이점은 빠른 시작 콘텐츠 및 설정의 순서입니다.

기존 API 앱 (또는 논리 앱에서 만든 마켓플레이스 API 앱) hello로 이전 미리 보기 기능 계속 표시 됩니다 hello 논리 앱 디자이너 및 리소스 그룹의에서 모든 리소스를 검색할 때.

## <a name="visual-studio"></a>Visual Studio
대부분의 웹 응용 프로그램 도구 작동할지 새로운 API 앱을 공유 하므로 동일한 기본 hello **Microsoft.Web/sites** 리소스 종류입니다. 그러나 이후 이상 노출 다양 한 기능 특정 tooAPIs 또는 업그레이드 된 tooversion 2.8.1 여야 합니다 hello Azure Visual Studio 도구. Hello에서 hello SDK 다운로드 [Azure 다운로드 페이지](https://azure.microsoft.com/downloads/)합니다.

앱 서비스 형식을 hello의 hello 합리화, 게시에 통합 됩니다 **게시 > Microsoft Azure 앱 서비스**:

![API 앱 게시](./media/app-service-api-whats-changed/api-apps-publish.png)

읽기 hello 알림이 2.8.1, SDK에 대 한 자세한 toolearn [블로그 게시물](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/)합니다.

Hello를 수동으로 가져올 수 또는 게시 프로필 hello 관리 포털 tooenable에서 게시 합니다. 그러나 클라우드 탐색기, 코드 생성 및 API 앱 선택/만들기에는 SDK 2.8.1 이상이 필요합니다.

## <a name="migrating-existing-api-apps"></a>기존 API 앱 마이그레이션
사용자 지정 API 이면 배포 된 toohello 이전 미리 보기 버전 API 앱의 2015 년 12 월 31 일 여 API 앱에 대 한 새 모델 toohello를 마이그레이션을 요청 합니다. 모두 hello 이전 및 새 모델을 기반으로 앱 서비스에서 호스트 되는 웹 Api 이후 hello 대부분의 기존 코드를 재사용할 수 있습니다.

### <a name="hosting-and-redeployment"></a>호스팅 및 다시 배포
hello를 다시 배포 하는 단계는 모든 기존 웹 API tooApp 서비스 배포와 동일 hello 됩니다. 단계:

1. 빈 API 앱을 만듭니다. N e w로 hello 포털에서이 작업을 수행할 수 있습니다 > 게시, 또는 리소스 관리자 도구에서 Visual Studio에서 API 앱. 리소스 관리자 도구 또는 서식 파일을 사용 하는 경우 설정 hello **종류** 너무 값**api** hello에 **Microsoft.Web/sites** 리소스 종류 toohave hello 퀵 스타트 및 설정 API 시나리오를 위한 관리 포털을 hello입니다.
2. 연결 하 고 앱을 배포 프로젝트 toohello 빈 API 앱 서비스에서 지 원하는 hello 배포 메커니즘 중 하나를 사용 하 여 키를 누릅니다. 읽기 [Azure 앱 서비스 배포 설명서](../app-service-web/web-sites-deploy.md) toolearn 더 합니다. 

### <a name="authentication"></a>인증
hello 앱 서비스 인증 서비스 지원 hello hello 이전 API 앱 모델에 사용할 수 없었던 동일한 기능입니다. 세션 토큰을 사용 하는 Sdk를 필요로 하는 경우 다음 Sdk 클라이언트와 서버 hello를 사용 합니다.

* 클라이언트: [Azure Mobile Client SDK](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/)
* 서버: [Microsoft Azure Mobile App .NET Authentication Extension](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/) 

앱 서비스 알파 Sdk hello를 대신 사용한 경우 이러한 이제 사용 되지 않습니다.

* 클라이언트: [Microsoft Azure AppService SDK](http://www.nuget.org/packages/Microsoft.Azure.AppService)
* 서버: [Microsoft.Azure.AppService.ApiApps.Service](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service)

그러나 특히 Azure Active Directory 없는 응용 프로그램 서비스 관련 작업이 필요 직접 hello AAD 토큰을 사용 하는 경우.

### <a name="internal-access"></a>내부 액세스
hello 이전 API 앱 모델에 대 한 기본 제공 내부 액세스 수준을 포함 되어 있습니다. 이 요청을 서명 하는 것에 대 한 hello SDK 사용을 해야 합니다. Hello 새로운 API 앱 모델이 함께 앞에서 설명한 대로 AAD 서비스 주체 용도 한 대체 방안으로 서비스 간 인증에는 응용 프로그램 서비스 관련 SDK를 요구 하지 않고 합니다. 자세한 내용은 [Azure 앱 서비스의 API 앱에 대한 서비스 주체 인증](app-service-api-dotnet-service-principal-auth.md)을 참조하세요.

### <a name="discovery"></a>검색
모델의 다른 API 앱에서 런타임에 검색 Api에는 이전 API 앱 hello 뒤에 있는 동일한 리소스 그룹 hello 동일한 게이트웨이에 hello 합니다. 이는 마이크로 서비스 패턴을 구현하는 아키텍처에 특히 유용합니다. 이 기능은 직접 지원되지 않지만 사용 가능한 여러 옵션이 있습니다.

1. 검색에 대 한 hello Azure 리소스 관리자 API를 사용 합니다.
2. Azure API 관리를 앱 서비스에서 호스트되는 API 앞에 둡니다. Azure API 관리는 외부에 노출되며 내부 토폴로지가 변경된 경우에도 안정적인 외부 연결 url을 제공할 수 있습니다.
3. 검색 API 앱을 빌드하고 다른 API 앱을 시작할 때 hello 검색 앱을 등록 합니다.
4. 배포 시 hello 응용 프로그램 설정을 채웁니다 모든 hello API 앱 (및 클라이언트)의 hello hello 끝점과 다른 API 앱을. 이 이제 제공 API 앱 및 템플릿 배포에서 실행 가능한 hello url의 제어 합니다.

## <a name="using-api-apps-with-logic-apps"></a>논리 앱과 API 앱 사용
새 API 앱 모델 hello와 잘 작동 [논리 앱 스키마 버전 2015-08-01](../logic-apps/logic-apps-schema-2015-08-01.md)합니다.

## <a name="next-steps"></a>다음 단계
toolearn hello의 hello 문서를 더 읽기 [API 앱 설명서 섹션](https://azure.microsoft.com/documentation/services/app-service/api/)합니다. API 앱에 대 한 업데이트 된 tooreflect hello 새 모델 있다가 합니다. 또한 않습니다 교류할 추가 세부 정보 또는 마이그레이션에 대 한 지침에 대 한 hello 포럼에:

* [MSDN 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureAPIApps)
* [스택 오버플로](http://stackoverflow.com/questions/tagged/azure-api-apps)

