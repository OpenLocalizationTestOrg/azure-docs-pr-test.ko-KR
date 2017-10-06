---
title: "aaaApp 서비스 API 앱 메타 데이터 API 검색 및 코드 생성에 대 한 | Microsoft Docs"
description: "Azure 앱 서비스에서 API 앱 Swagger 메타 데이터 API toofacilitate 검색 및 코드 생성을 사용 하는 방법에 대해 알아봅니다."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: c7f8e33a-61cc-486f-89df-4a97dc3c71d4
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: alkarche
ms.openlocfilehash: b27e70b7dd6bd97f5b0b490b496320befe7442c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-api-apps-metadata-for-api-discovery-and-code-generation"></a>API 검색 및 코드 생성에 대한 앱 서비스 API 앱 메타데이터
[Swagger 2.0](http://swagger.io/) API 메타데이터에 대한 지원은 앱 서비스 API 앱에 작성됩니다. Swagger, toouse 필요는 없지만 사용 않는 쉽게 검색 하 고 사용할 수 있게 하는 API 앱 기능을 활용 걸릴 수 있습니다.   

## <a name="swagger-endpoint"></a>Swagger 끝점
Hello API 응용 프로그램의 속성에서 API 앱에 대 한 Swagger 2.0 JSON 메타 데이터를 제공 하는 끝점을 지정할 수 있습니다. 절대 URL 또는 hello API 응용 프로그램의 기준 URL을 상대 toohello hello 끝점 수 있습니다. 절대 Url hello API 앱 외부 가리킬 수 있습니다. 

많은 다운스트림 클라이언트 (예: Visual Studio 코드 생성 및 PowerApps "API 추가" 흐름) hello URL 이어야 합니다 공개적으로 액세스할 수 있는 (사용자 또는 서비스 인증으로 보호 되지 않습니다). 이 앱 서비스 인증을 사용 하는 자체 응용 프로그램 내에서 tooexpose hello API 정의 사용할 경우 할 toouse 인증 하는 옵션을 익명 트래픽 tooreach API 의미 합니다. 자세한 내용은 [App Service API 앱에 대한 인증 및 권한 부여](app-service-api-authentication.md)를 참조하세요.

### <a name="portal-blade"></a>포털 블레이드
Hello에 [Azure 포털](https://portal.azure.com/) 끝점 URL을 볼 hello에서 변경 하 고 hello **API 정의** 블레이드입니다.

![](./media/app-service-api-metadata/apidefblade.png)

### <a name="azure-resource-manager-property"></a>Azure 리소스 관리자 속성
사용 하 여 API 앱에 대 한 hello API 정의 URL을 구성할 수도 있습니다 [리소스 탐색기](https://resources.azure.com/) 또는 [Azure 리소스 관리자 템플릿을](../azure-resource-manager/resource-group-authoring-templates.md) 와 같은 명령줄 도구에서 [Azure PowerShell](/powershell/azureps-cmdlets-docs)및 hello [Azure CLI](../cli-install-nodejs.md)합니다. 

**리소스 탐색기**, 너무 이동**구독 > {구독} > resourceGroups > {리소스 그룹} > 공급자 > Microsoft.Web > 사이트 > {사이트} > 구성 > 웹**, hello 보면 `apiDefinition` 속성:

        "apiDefinition": {
          "url": "https://contactslistapi.azurewebsites.net/swagger/docs/v1"
        }

Hello를 설정 하는 Azure 리소스 관리자 템플릿에 대 한 예제 `apiDefinition` 속성을 열고 hello [hello 할 작업 목록 샘플 응용 프로그램에서에서 azuredeploy.json 파일](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json)합니다. 위에 표시 된 hello JSON 예제 처럼 보이는 hello 템플릿의 hello 섹션을 찾습니다.

### <a name="default-value"></a>기본값
Visual Studio toocreate API 앱을 사용 하 여 hello API 정의 끝점이 자동으로 설정 됩니다 toohello 더하기 hello API 응용 프로그램의 기준 URL `/swagger/docs/v1`합니다. 이 hello 기본 URL 해당 hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet 패키지는 ASP.NET Web API 프로젝트에 대 한 동적으로 생성 된 tooserve Swagger 메타 데이터를 사용 합니다. 

## <a name="code-generation"></a>코드 생성
Swagger Azure API 앱에 통합 hello 이점 중 하나는 자동 코드 생성 됩니다. 생성 된 클라이언트 클래스는 API 앱을 호출 하는 보다 쉽게 toowrite 코드를 만듭니다.

Hello 명령줄에서 또는 Visual Studio를 사용 하 여 API 앱에 대 한 클라이언트 코드를 생성할 수 있습니다. Toogenerate 클라이언트 Visual Studio에서 ASP.NET 웹 API 프로젝트에 대 한 클래스 하는 방법에 대 한 정보를 참조 하십시오. [API 앱 및 ASP.NET 시작](app-service-api-dotnet-get-started.md#codegen)합니다. 어떻게 toodo hello 명령에서 줄에 대 한 지원 되는 모든 언어에 대 한 내용은 hello의 hello readme 파일을 참조 하십시오. [Azure/autorest](https://github.com/azure/autorest) GitHub.com에 리포지토리 합니다.

## <a name="next-steps"></a>다음 단계
API 앱을 만들고 배포하며 소비하는 과정을 안내하는 단계별 자습서는 [Azure 앱 서비스에서 API 앱 시작](app-service-api-dotnet-get-started.md)을 참조하세요.

API 앱과 Azure API 관리를 사용 하는 경우 사용할 수 있습니다 Swagger 메타 데이터 tooimport API API 관리에. 자세한 내용은 참조 [어떻게 tooimport hello Azure API 관리에서 작업을 사용 하는 API의 정의](../api-management/api-management-howto-import-api.md)합니다. 

