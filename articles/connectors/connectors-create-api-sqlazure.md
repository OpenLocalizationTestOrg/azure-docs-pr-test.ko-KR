---
title: "논리 앱에서 aaaAdd hello Azure SQL 데이터베이스 커넥터 | Microsoft Docs"
description: "REST API 매개 변수를 사용하는 Azure SQL 데이터베이스 커넥터 개요"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d8a319d0-e4df-40cf-88f0-29a6158c898c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a9ca0f446d05dc00f310a908eee8d50e41fcd82b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-sql-database-connector"></a>Hello Azure SQL 데이터베이스 커넥터와 함께 시작.
Hello Azure SQL 데이터베이스 커넥터를 사용 하 여 조직에 대 한 테이블의 데이터를 관리 하는 워크플로 만듭니다. 

SQL 데이터베이스를 사용하여 다음과 같은 작업을 수행합니다.

* 새 고객 tooa 고객 데이터베이스를 추가 하거나 orders 데이터베이스에 순서를 업데이트 하 여 워크플로 작성 합니다.
* 동작 tooget 데이터 행을 사용 하 고, 새 행을 삽입 하 고 및 삭제할 수도 있습니다. 예를 들어 Dynamics CRM Online에서 레코드가 만들어지면(트리거) Azure SQL Database에 행을 삽입합니다(작업). 

이 항목에서는 방법을 toouse hello 논리 앱에서 SQL 데이터베이스 커넥터와도 목록 hello 동작.

논리 앱에 대해 자세히 toolearn 참조 [논리 앱 이란](../logic-apps/logic-apps-what-are-logic-apps.md) 및 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.

## <a name="connect-tooazure-sql-database"></a>TooAzure SQL 데이터베이스 연결
논리 앱에서 모든 서비스에 액세스 하기 전에 먼저 만들어야는 *연결* toohello 서비스입니다. 연결은 논리 앱과 다른 서비스 간의 연결을 제공합니다. 예를 들어 tooconnect tooSQL 데이터베이스를 먼저 만들어야 SQL 데이터베이스 *연결*합니다. tooaccess hello 서비스에 연결 하는 일반적으로 사용 하는 hello 자격 증명을 입력 한 toocreate 연결 합니다. 따라서 SQL 데이터베이스의 SQL 데이터베이스 자격 증명 toocreate hello 연결을 입력 합니다. 

#### <a name="create-hello-connection"></a>Hello 연결 만들기
> [!INCLUDE [Create hello connection tooSQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a>트리거 사용
이 연결에는 트리거가 필요하지 않습니다. 다른 트리거 toostart hello 논리 앱과 되풀이 트리거, HTTP Webhook 트리거는 트리거를 사용 하 여 다른 커넥터를 사용할 수 있는 등을 사용 합니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)에서 예제를 제공하고 있습니다.

## <a name="use-an-action"></a>작업 사용
동작은 논리 앱에 정의 된 hello 워크플로에 의해 수행 되는 작업입니다. [작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)

1. Hello 더하기 기호를 선택 합니다. 여러 선택 항목을 참조 하십시오: **동작 추가**, **조건을 추가**, hello 중 하나 또는 **자세한** 옵션입니다.
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. **작업 추가**를 선택합니다.
3. Hello 텍스트 상자에 "sql" tooget hello 사용 가능한 모든 작업 목록을 입력 합니다.
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. 이 예제에서는 **SQL Server - 행 가져오기**를 선택합니다. 연결이 이미 존재 하는 경우 다음 hello 선택 **테이블 이름** hello 드롭다운 목록에서 목록을 연 hello 입력 **행 ID** tooreturn 원하는 합니다.
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    Hello 연결 정보에 대 한 메시지가 표시 되 면 hello, toocreate hello 연결 세부 정보를 입력 합니다. [Hello 연결을 만들](connectors-create-api-sqlazure.md#create-the-connection) 이 항목에서 이러한 속성을 설명 합니다. 
   
   > [!NOTE]
   > 이 예제에서는 테이블의 행을 반환합니다. 이 행에 toosee hello 데이터가 hello 테이블의 필드를 hello를 사용 하 여 파일을 만드는 다른 작업을 추가 합니다. 예를 들어 hello FirstName 및 LastName 필드 toocreate hello 클라우드 저장소 계정에 새 파일을 사용 하는 OneDrive 동작을 추가 합니다. 
   > 
   > 
5. **저장** 변경 내용을 (hello 도구 모음의 왼쪽된 상단 모서리). 논리 앱이 저장되며 이 논리 앱이 사용 상태로 자동 설정될 수 있습니다.

## <a name="connector-specific-details"></a>커넥터 관련 세부 정보

모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/sql/)합니다. 

## <a name="next-steps"></a>다음 단계
[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md) 탐색에서 논리 앱에서 사용할 수 있는 다른 커넥터 hello 우리의 [Api 목록](apis-list.md)합니다.

