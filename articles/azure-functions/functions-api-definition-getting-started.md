---
title: "aaaGetting Azure 함수에서 OpenAPI 메타 데이터와 시작 됨 | Microsoft Docs"
description: "Azure Functions에서 OpenAPI 지원 시작"
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
ms.openlocfilehash: fee3464c9a0a11b6d3891ccd0e9c5343d6bedcad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a>함수 앱에서 OpenAPI 2.0(Swagger) 만들기(미리 보기)

이 문서는 hello Azure 함수에서 호스트 되는 간단한 API에 대 한 OpenAPI 정의 만드는 방법을 단계별로 과정을 안내 합니다.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a>OpenAPI(Swagger)란?
[Swagger 메타 데이터](http://swagger.io/) hello 기능을 정의 하는 파일 및 이며, 운영 모드의 API 호스팅하는 다양 한 다른 소프트웨어에서 사용 하는 REST API toobe 함수를 허용 합니다. Microsoft 제공 사항 PowerApps 같은 및 [API 앱](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), 3rd 파티 개발자와 같은 도구 뿐만 아니라 [우체부](https://www.getpostman.com/docs/importing_swagger) 및 [많은 추가 패키지](http://swagger.io/tools/) 과 함께 사용 된 프로그램 API toobe 수는 Swagger 정의 합니다.

## <a name="prepare-function"></a>간단한 API가 포함된 함수 만들기
  OpenAPI 정의 toocreate 먼저 필요 toocreate 단순 API 사용 하는 함수입니다. 함수는 앱에서 호스트 되는 API를 이미 있는 경우에 직선 toohello 다음 섹션을 건너뛸 수 있습니다.
1. 새로운 함수 앱 만들기
    1. [Azure Portal](https://portal.azure.com) > `+ New` > “함수 앱” 검색
1. 사용자의 새 함수 앱 내에서 새 HTTP 트리거 함수 만들기
    1. 함수는 매우 간단한 REST API를 정의하는 코드로 미리 채워져 있습니다.
    1. 쿼리 매개 변수로 또는 hello 본문에 toohello 함수를 전달 하는 모든 문자열 "Hello {입력}"로 반환 됩니다.
1. Toohello 이동 `Integrate` 새 HTTP 트리거 함수의 탭
    1. 설정/해제 `Allowed HTTP methods` 너무`Selected methods`
    1. `Selected HTTP methods`에서 POST를 제외한 모든 동사를 선택 취소합니다
    ![선택된 HTTP 메서드](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)
    1. 이 단계는 나중에 API 정의를 간소화합니다.

## <a name="enable"></a>API 정의 지원을 사용하도록 설정
1. 너무 이동`your function name` > `Platform Features` > `API Definition`
![정의 탭](./media/functions-api-definition-getting-started/definitiontab.png)
1. 설정 `API Definition Source` 너무`Function (preview)`
    1. 이 단계에서는 끝점 toohost OpenAPI 파일로 된 인라인 사본 hello 함수 응용 프로그램 도메인에서 등 함수 응용 프로그램에 대 한 OpenAPI 옵션 집합이 [OpenAPI 편집기](http://editor.swagger.io), 및 퀵 스타트 정의 생성기입니다.
![사용 가능한 정의](./media/functions-api-definition-getting-started/enabledefinition.png)

## <a name="create-definition"></a>템플릿에서 API 정의 만들기
1. `Generate API Definition template`을 클릭합니다.
    1. 이 단계는 HTTP 트리거 함수에 대 한 함수 앱을 검색 하 고 functions.json toogenerate OpenAPI 문서에서에서 hello 정보를 사용 합니다.
1. 작업 개체를 너무 추가`paths: /api/yourfunctionroute post:`
    1. hello 퀵 스타트 OpenAPI 문서는 전체 OpenAPI doc의 개요입니다. 더 많은 메타 데이터 toobe 응답 템플릿 작업 개체와 같은 전체 OpenAPI 정의 해야합니다.
    1. hello 샘플 작업 개체 아래에 생성/사용 섹션, 매개 변수 개체 및 응답 개체 채워진 스타일이 있습니다.
    
    ```yaml
      post:
        operationId: /api/yourfunctionroute/post
        consumes: [application/json]
        produces: [application/json]
        parameters:
          - name: name
            in: body
            description: Your name
            x-ms-summary: Your name
            required: true
            schema:
              type: object
              properties:
                name:
                  type: string
        description: >-
          Replace with Operation Object
          #http://swagger.io/specification/#operationObject
        responses:
          '200':
            description: A Greeting
            x-ms-summary: Your name
            schema:
              type: string
        security:
          - apikeyQuery: []
    ```
    
    > [!NOTE]
    >  x-ms-summary는 논리 앱, 흐름, PowerApps에 표시 이름을 제공합니다.
    >
    > 체크 아웃 [powerapps Swagger 정의 사용자 지정](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn 더 합니다.

1. 클릭 `save` toosave 변경 내용을 ![템플릿 정의 추가](./media/functions-api-definition-getting-started/addingtemplate.png)

## <a name="use-definition"></a>API 정의 사용
1. 복사 프로그램 `API definition URL` 원시 OpenAPI 문서에 새 브라우저 탭 tooview 붙여 합니다.
1. 테스트와 해당 URL을 사용 하 여 통합을 위한 도구는 OpenAPI 문서 tooany 번호를 가져올 수 있습니다.
    1. 많은 Azure 리소스가 수 tooautomatically 가져오기 OpenAPI 문서를 사용 하 여 hello 함수 응용 프로그램 설정에 저장 되는 API 정의 URL입니다. Hello의 일부로 `Function` API 정의 소스 url을 업데이트 했습니다.


## <a name="test-definition"></a>API 정의 Swagger UI tootest hello를 사용 하 여
내장 hello API 정의 편집기의 toohello UI 뷰에서 기본 제공 도구 테스트 됩니다. API 키를 추가 하 고 다음 hello를 사용 하 여 `Try this operation` 각 방법에 따라 단추입니다. hello 도구는 사용자의 API 정의 tooformat hello 요청을 사용 하 고 성공 응답 정의 정확한 지 나타냅니다.

### <a name="steps"></a>단계:

1. 함수 API 키 복사
    1. HTTP 트리거 함수에서 hello API 키를 찾을 수 `function name` > `Keys` > `Function Keys` 
   ![기능 키](./media/functions-api-definition-getting-started/functionkey.png)
1. Toohello 이동 `API Definition` 페이지.
    1. 클릭 `Authenticate` hello 위쪽 함수 API 키 toohello 보안 개체를 추가 합니다.
  ![OpenAPI 키](./media/functions-api-definition-getting-started/definitionTest auth.png)
1. `/api/yourfunctionroute` > `POST`를 선택합니다.
1. 클릭 `Try it out` 이름 tootest 입력
1. `Pretty`
![API 정의 테스트](./media/functions-api-definition-getting-started/definitionTest.png)에서 SUCCESS 결과를 확인할 수 있습니다.

## <a name="next-steps"></a>다음 단계
* [Functions 개요의 OpenAPI 정의](functions-api-definition.md)
  * Hello OpenAPI 지원에 대 한 자세한 정보에 대 한 전체 설명서를 읽습니다.
* [Azure Functions 개발자 참조](functions-reference.md)  
  * 함수를 코딩하고 트리거 및 바인딩을 정의하기 위한 프로그래머 참조입니다.
* [Azure Functions GitHub 리포지토리](https://github.com/Azure/Azure-Functions/)
  * 체크 아웃 hello 함수 GitHub toogive us hello API 정의 지원 미리 보기에 대 한 피드백! 업데이트 toosee 원하는 모든 항목에 대 한 GitHub 문제를 확인 합니다.
