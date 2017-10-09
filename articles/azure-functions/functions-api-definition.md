---
title: "Azure 함수에서 메타 데이터 aaaOpenAPI | Microsoft Docs"
description: "Azure Functions에서 OpenAPI 지원 개요"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/23/2017
ms.author: alkarche
ms.openlocfilehash: fff8f14110469a002a6c9dca03f641672003a3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="openapi-20-metadata-support-in-azure-functions-preview"></a>Azure Functions에서 OpenAPI 2.0 메타데이터 지원(미리 보기)
OpenAPI 2.0 (Swagger 이전의) Azure 함수에서 메타 데이터 지원을 함수 앱 내 toowrite OpenAPI 2.0 정의 사용할 수 있는 미리 보기 기능입니다. 그런 다음 hello 함수 앱을 사용 하 여 해당 파일을 호스트할 수 있습니다.

[메타 데이터 OpenAPI](http://swagger.io/) 다른 소프트웨어의 다양 한에서 REST API toobe를 호스트 하는 함수를 사용할 수 있습니다. 이 소프트웨어 PowerApps 및 hello와 같은 Microsoft 제품에는 [Azure 앱 서비스의 API 앱 기능](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), 타사 개발자 도구와 같은 [우체부](https://www.getpostman.com/docs/importing_swagger), 및 [많은 추가 패키지](http://swagger.io/tools/).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

>[!TIP]
>Hello로 시작 하는 것이 좋습니다 [시작 자습서](./functions-api-definition-getting-started.md) 특정 기능에 대 한 자세한 문서 toolearn toothis를 반환 합니다.

## <a name="enable"></a>OpenAPI 정의 지원 사용
Hello에서 모든 OpenAPI 설정을 구성할 수 있습니다 **API 정의** 함수 응용 프로그램의 페이지 **플랫폼 기능**합니다.

호스팅된 OpenAPI 정의와 퀵 스타트 정의의 tooenable hello 생성 설정 **API 정의 소스** 너무**함수 (미리 보기)**합니다. **외부 URL** 함수 toouse 사용 하면 다른 곳에서 호스트에 OpenAPI 정의할 수 있습니다.

## <a name="generate-definition"></a>함수의 메타데이터에서 Swagger 구조 생성
템플릿을 사용하면 첫 번째 OpenAPI 정의 작성을 시작할 수 있습니다. hello 정의 템플릿 기능 각 HTTP 트리거 함수에 대 한 hello function.json 파일에 모든 hello 메타 데이터를 사용 하 여 스파스 OpenAPI 정을 만듭니다. Hello에서 API에 대 한 자세한 내용은에서 toofill을 매핑해야 합니다 [OpenAPI 사양](http://swagger.io/specification/), 요청 및 응답 템플릿과 같은 합니다.

단계별 지침은 hello [시작 자습서](./functions-api-definition-getting-started.md)합니다.

### <a name="templates"></a>사용 가능한 템플릿

|이름| 설명 |
|:-----|:-----|
|생성된 정의|Hello 함수 기존 메타 데이터에서 유추할 수 있는 정보의 hello 최대한 사용 하는 OpenAPI 정의 합니다.|

### <a name="quickstart-details"></a>생성 된 hello 정의에 포함 된 메타 데이터

hello 테이블 나타내는 다음 Azure 포털 설정 및 해당 데이터에 function.json hello를 생성 하는 매핑된 toohello Swagger 구조를 그대로 합니다.

|Swagger.json|포털 UI|Function.json|
|:----|:-----|:-----|
|[호스트](http://swagger.io/specification/#fixed-fields-15)|**함수 앱 설정** > **App Service 설정** > **개요** > **URL**|*없음*
|[경로](http://swagger.io/specification/#paths-object-29)|**통합** > **선택한 HTTP 메서드**|바인딩: 경로
|[경로 항목](http://swagger.io/specification/#path-item-object-32)|**통합** > **경로 템플릿**|바인딩: 메서드
|[보안](http://swagger.io/specification/#security-scheme-object-112)|**키**|*없음*|
|operationID*|**경로 + 허용되는 동사**|경로 + 허용 동사|

\*hello 작업 ID가 PowerApps 및 흐름 통합에 필요 합니다.
> [!NOTE]
> hello x-ms-요약 확장 논리 앱, PowerApps, 및 흐름에 표시 이름을 제공합니다.
>
> toolearn 더 참조 [powerapps Swagger 정의 사용자 지정](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/)합니다.

## <a name="CICD"></a>CI/CD tooset API 정의 사용 하 여

 API 소스 제어 toomodify를 소스 제어에서 API 정의 사용 하기 전에 정의 hello 포털의 호스팅을 활성화 해야 합니다. 다음 지침을 따릅니다.

1. 너무 찾아보기**API 정의 (미리 보기)** 함수 응용 프로그램 설정에서 합니다.
  1. 설정 **API 정의 소스** 너무**함수**합니다.
  1. 클릭 **생성 API 정의 템플릿** 차례로 **저장** toocreate 나중에 수정에 대 한 템플릿 정의 합니다.
  1. API 정의 URL 및 키를 적어 둡니다.
1. [CI/CD(연속 통합/연속 배포)를 설정합니다](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment#continuous-deployment-requirements).
2. \site\wwwroot\.azurefunctions\swagger\swagger.json의 원본 제어에서 swagger.json을 수정합니다.

이제 저장소에서 tooswagger.json hello API 정의 URL에서 함수 응용 프로그램에서 호스팅되는 변경 내용 및에서 적어 둔 키 1.c를 단계입니다.

## <a name="next-steps"></a>다음 단계
* [시작 자습서](functions-api-definition-getting-started.md) - 이 연습에서는 toosee 작업에 있는 OpenAPI 정의 해 보십시오.
* [Azure Functions GitHub 리포지토리](https://github.com/Azure/Azure-Functions/) - 체크 아웃 hello 함수 리포지토리 toogive us hello API 정의 지원 미리 보기에 대 한 피드백 합니다. 업데이트 toosee 원하는 모든 항목에 대 한 GitHub 문제를 확인 합니다.
* [Azure Functions 개발자 참조](functions-reference.md) - 함수 코딩과 트리거 및 바인딩 정의에 대해 알아봅니다.
