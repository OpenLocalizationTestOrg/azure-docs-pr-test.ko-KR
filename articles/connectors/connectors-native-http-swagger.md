---
title: "HTTP + Swagger aaaCall REST 끝점에 대 한 Azure 논리 앱 커넥터 | Microsoft Docs"
description: "Swagger 통해 안녕하세요 HTTP + Swagger 커넥터를 사용 하 여 논리 앱에서 tooREST 끝점 연결"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: eccfd87c-c5fe-4cf7-b564-9752775fd667
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: baaa57689ff41fcd052f9d86086e36619ddec46e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http--swagger-action"></a>안녕하세요 HTTP + Swagger 작업 시작

통해 첫 번째 클래스 커넥터 tooany REST 끝점을 만들 수는 [Swagger 문서](https://swagger.io) 때 논리 앱 워크플로 hello HTTP + Swagger 동작을 사용 합니다. 또한 논리 앱 toocall 모든 REST 끝점은 첫 번째 클래스 논리가 응용 프로그램 디자이너 환경을 확장할 수 있습니다.

커넥터를 사용 하 여 논리 앱 toocreate 참조 toolearn [새 논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a>HTTP + Swagger를 트리거 또는 동작으로 사용합니다.

안녕하세요 HTTP + Swagger 트리거와 작업이 바뀐 작업 hello 동일 hello로 [HTTP 동작](connectors-native-http.md) hello API 구조 및 hello의 출력을 노출 하 여 논리 앱 디자이너에서 향상 된 환경을 제공 하지만 [Swagger 메타 데이터](https://swagger.io) . 또한 트리거로 안녕하세요 HTTP + Swagger 커넥터를 사용할 수 있습니다. 폴링 트리거 tooimplement 하려는 경우에 설명 된 hello 폴링 패턴을 따를 [논리 앱에서 사용자 지정 Api toocall 다른 Api, 서비스 및 시스템 만들](../logic-apps/logic-apps-create-api-app.md#polling-triggers)합니다.

[논리 앱 트리거 및 동작](connectors-overview.md)에 대해 알아봅니다.

HTTP + Swagger toouse hello 하는 방법의 예로 워크플로에서 논리 앱의 동작으로 작업 합니다.

1. 선택 hello **새 단계** 단추입니다.
2. **작업 추가**를 선택합니다.
3. Hello 동작 검색 상자에 입력 **swagger** toolist 안녕하세요 HTTP + Swagger 동작 합니다.
   
    ![HTTP + Swagger 동작 선택](./media/connectors-native-http-swagger/using-action-1.png)
4. Swagger 문서에 대 한 hello URL을 입력 합니다.
   
   * toowork hello 논리가 응용 프로그램 디자이너 hello URL에서에서 HTTPS 끝점 및 CORS 사용.
   * Hello Swagger 문서가 요구이 사항을 충족 하지 않는 경우 사용할 수 있습니다 [Azure 저장소 사용 하도록 설정 하는 CORS와](#hosting-swagger-from-storage) toostore hello 문서.
5. 클릭 **다음** tooread 및에서 렌더링 hello Swagger 문서.
6. Hello HTTP 호출에 필요한 매개 변수를 추가 합니다.
   
    ![HTTP 작업 완료](./media/connectors-native-http-swagger/using-action-2.png)
7. toosave 논리 앱 게시를 클릭 하 고 **저장** 디자이너 도구 모음입니다.

### <a name="host-swagger-from-azure-storage"></a>Azure Storage에서 Swagger 호스트
Tooreference Swagger 문서 호스트 되지 않는 또는 hello 디자이너에 대 한 hello 보안 및 크로스-원본 요구 사항에 맞지 않는 하지 않는 경우가 있습니다. tooresolve이 문제를 Azure 저장소의 hello Swagger 문서를 저장할 수 있으며 CORS tooreference hello 문서를 사용 하도록 설정 합니다.  

다음은 hello 단계 toocreate, 구성 및 Azure 저장소에 Swagger 문서를 저장할:

1. [Azure Blob 저장소를 사용하여 Azure Storage 계정을 만듭니다](../storage/common/storage-create-storage-account.md). tooperform이 단계 사용 권한 설정 너무**공용 액세스**합니다.

2. Hello blob에서 CORS를 사용 하도록 설정 합니다. 

   tooautomatically이 설정을 사용할 수 있습니다, [이 PowerShell 스크립트](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1)합니다.

3. Hello Swagger 파일 toohello blob을 업로드 합니다. 

   Hello에서이 단계를 수행할 수 있습니다 [Azure 포털](https://portal.azure.com) 또는 같은 도구에서 [Azure 저장소 탐색기](http://storageexplorer.com/)합니다.

4. Azure Blob 저장소에는 HTTPS 링크 toohello 문서를 참조 합니다. 

   hello 링크에는이 형식을 사용합니다.

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a>기술 세부 정보
다음은이 hello 트리거 및 작업에 대 한 hello 정보 HTTP + Swagger 커넥터를 지원 합니다.

## <a name="http--swagger-triggers"></a>HTTP + Swagger 트리거
트리거는 사용 되는 toostart hello 워크플로 논리 앱에 정의 된 일 수 있는 이벤트입니다. [트리거에 대해 자세히 알아보세요.](connectors-overview.md) HTTP + Swagger hello 커넥터에 하나의 트리거가 있습니다.

| 트리거 | 설명 |
| --- | --- |
| HTTP + Swagger |HTTP 호출을 수행 하 고 hello 응답 콘텐츠를 반환 합니다. |

## <a name="http--swagger-actions"></a>HTTP + Swagger 동작
동작은 논리 앱에 정의 된 hello 워크플로 통해 수행 되는 작업입니다. [작업에 대해 자세히 알아봅니다.](connectors-overview.md) HTTP + Swagger hello 연결선의 한 가지 가능한 동작 합니다.

| 동작 | 설명 |
| --- | --- |
| HTTP + Swagger |HTTP 호출을 수행 하 고 hello 응답 콘텐츠를 반환 합니다. |

### <a name="action-details"></a>작업 세부 정보
HTTP + Swagger hello 커넥터 작업을 사용할와 함께 제공 합니다. 다음은 각 hello 작업, 필수 및 선택적 입력된 필드 및 용도와 연결 된 출력 세부 사항에 해당 하는 hello에 대 한 정보입니다.

#### <a name="http--swagger"></a>HTTP + Swagger
Swagger 메타데이터를 지원하는 HTTP 아웃바운드 요청을 만듭니다.
별표(*)는 필수 필드를 의미합니다.

| 표시 이름 | 속성 이름 | 설명 |
| --- | --- | --- |
| Method* |메서드 |HTTP 동사 toouse 합니다. |
| URI* |uri |Hello HTTP 요청에 대 한 URI입니다. |
| 헤더 |headers |HTTP 헤더 tooinclude의 JSON 개체입니다. |
| body |body |hello HTTP 요청 본문입니다. |
| 인증 |인증 |요청에 대 한 인증 toouse 합니다. 자세한 내용은 참조 hello [HTTP 커넥터](connectors-native-http.md#authentication)합니다. |

**출력 세부 정보**

HTTP 응답

| 속성 이름 | 데이터 형식 | 설명 |
| --- | --- | --- |
| headers |object |응답 헤더 |
| 본문 |object |응답 개체 |
| 상태 코드 |int |HTTP 상태 코드 |

### <a name="http-responses"></a>HTTP 응답
호출 toovarious 작업을 만들 때 특정 응답 발생할 수 있습니다. 다음 표에서는 해당 응답 및 설명을 대략적으로 요약해서 보여 줍니다.

| Name | 설명 |
| --- | --- |
| 200 |확인 |
| 202 |수락됨 |
| 400 |잘못된 요청 |
| 401 |권한 없음 |
| 403 |사용할 수 없음 |
| 404 |찾을 수 없음 |
| 500 |내부 서버 오류. 알 수 없는 오류 발생. |

- - -
## <a name="next-steps"></a>다음 단계

* [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)
* [다른 커넥터 찾기](apis-list.md)