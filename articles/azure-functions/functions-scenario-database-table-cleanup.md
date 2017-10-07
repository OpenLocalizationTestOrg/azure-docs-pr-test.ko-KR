---
title: "aaaUse Azure 함수 tooperform 작업 정리 데이터베이스 | Microsoft Docs"
description: "사용 하 여 Azure 함수 tooschedule tooAzure SQL 데이터베이스 tooperiodically 연결 하는 작업은 행을 정리 합니다."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 076f5f95-f8d2-42c7-b7fd-6798856ba0bb
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/22/2017
ms.author: glenga
ms.openlocfilehash: 063a25fe8d14a75d54e9b72cec9fc1e25fa3ff44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-tooconnect-tooan-azure-sql-database"></a>Azure 함수 tooconnect tooan Azure SQL 데이터베이스를 사용 하 여
이 항목에서는 방법을 toouse Azure 함수 toocreate 예약된 된 작업을 Azure SQL 데이터베이스의 테이블에서 행을 정리 합니다. hello 새 C# 함수 hello Azure 포털에서에서 미리 정의 된 타이머 트리거 템플릿을 기반으로 생성 됩니다. toosupport이이 시나리오에서는 설정 해야 데이터베이스 연결 문자열을 hello 함수 앱에 대 한 설정으로 합니다. 이 시나리오에서는 hello 데이터베이스에 대해 대량 작업을 사용 합니다. toohave 함수 프로세스 개별 CRUD 작업에서 모바일 앱 테이블을 대신 사용 해야 [모바일 앱 바인딩](functions-bindings-mobile-apps.md)합니다.

## <a name="prerequisites"></a>필수 조건

+ 이 항목에서는 타이머 트리거 함수를 사용합니다. Hello 항목의 단계를 완료 하는 hello [타이머에 의해 트리거되는 Azure에 함수를 만들](functions-create-scheduled-function.md) 이 함수의 toocreate C# 버전입니다.   

+ 이 항목에서 설명 hello에 대량 정리 작업을 실행 하는 Transact SQL 명령과 **SalesOrderHeader** hello AdventureWorksLT 샘플 데이터베이스의 테이블입니다. toocreate hello AdventureWorksLT 샘플 데이터베이스 hello 항목의 단계를 완료 hello [hello Azure 포털에서에서 Azure SQL 데이터베이스를 만들](../sql-database/sql-database-get-started-portal.md)합니다. 

## <a name="get-connection-information"></a>연결 정보 가져오기

완료할 때 만들었으므로 hello 데이터베이스에 대 한 tooget hello 연결 문자열이 필요한 [hello Azure 포털에서에서 Azure SQL 데이터베이스를 만들](../sql-database/sql-database-get-started-portal.md)합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
 
3. 선택 **SQL 데이터베이스** hello 왼쪽 메뉴에서 hello에 해당 데이터베이스를 선택 하 고 **SQL 데이터베이스** 페이지.

4. 선택 **데이터베이스 연결 문자열 표시** 및 전체 복사 hello **ADO.NET** 연결 문자열입니다.

    ![Hello ADO.NET 연결 문자열을 복사 합니다.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-hello-connection-string"></a>Hello 연결 문자열 설정 

함수 응용 프로그램 호스트 hello Azure에서 함수를 실행 합니다. 모범 사례 toostore 연결 문자열 및 기타 암호 함수 응용 프로그램 설정에서 않습니다. 응용 프로그램 설정을 사용 하 여 코드와 hello 연결 문자열의 실수로 인 한 노출을 방지 합니다. 

1. 만든 tooyour 함수 앱 이동 [타이머에 의해 트리거되는 Azure에 함수를 만들](functions-create-scheduled-function.md)합니다.

2. **플랫폼 기능** > **응용 프로그램 설정**을 선택합니다.
   
    ![Hello 함수 앱에 대 한 응용 프로그램 설정입니다.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. 너무 아래로 스크롤하여**연결 문자열** hello 설정을 사용 하 여 hello 테이블에 지정 된 연결 문자열을 추가 합니다.
   
    ![연결 문자열 toohello 함수 응용 프로그램 설정을 추가 합니다.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | 설정       | 제안 값 | 설명             | 
    | ------------ | ------------------ | --------------------- | 
    | **Name**  |  sqldb_connection  | 사용 되는 tooaccess hello 함수 코드에서 연결 문자열을 저장 합니다.    |
    | **값** | 복사한 문자열  | Hello 연결 문자열을 지 나 hello 이전 섹션에서 복사 합니다. |
    | **형식** | SQL 데이터베이스 | Hello 기본 SQL 데이터베이스 연결을 사용 합니다. |   

3. **Save**를 클릭합니다.

이제 hello C# 함수 코드를 tooyour SQL 데이터베이스 연결을 추가할 수 있습니다.

## <a name="update-your-function-code"></a>함수 코드 업데이트

1. 함수 응용 프로그램에서 hello 타이머 트리거 함수를 선택 합니다.
 
3. Hello 다음 hello 위쪽 hello 기존 함수 코드에 어셈블리 참조를 추가 합니다.

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. Hello 다음 추가 `using` 문 toohello 함수:
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. Hello 기존 항목 바꾸기 **실행** 함수 코드 다음 hello로:
    ```cs
    public static async Task Run(TimerInfo myTimer, TraceWriter log)
    {
        var str = ConfigurationManager.ConnectionStrings["sqldb_connection"].ConnectionString;
        using (SqlConnection conn = new SqlConnection(str))
        {
            conn.Open();
            var text = "UPDATE SalesLT.SalesOrderHeader " + 
                    "SET [Status] = 5  WHERE ShipDate < GetDate();";

            using (SqlCommand cmd = new SqlCommand(text, conn))
            {
                // Execute hello command and log hello # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    이 샘플 명령은 업데이트 hello **상태** 열 hello 운송 날짜를 기반으로 합니다. 32행의 데이터를 업데이트해야 합니다.

5. 클릭 **저장**, 조사식 hello **로그** hello에 대 한 다음 실행을 작동 한 후 windows hello에서 업데이트 된 행의 hello 번호를 확인 **SalesOrderHeader** 테이블입니다.

    ![Hello 기능 로그를 확인 합니다.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a>다음 단계

배우는 것이 다른 서비스와 논리 앱 toointegrate toouse 함수 방법입니다.

> [!div class="nextstepaction"] 
> [Logic Apps와 통합되는 함수 만들기](functions-twitter-email.md)

함수에 대 한 자세한 내용은 다음 항목 hello를 참조 하세요.

* [Azure Functions 개발자 참조](functions-reference.md)  
  함수를 코딩하고 트리거 및 바인딩을 정의하기 위한 프로그래머 참조입니다.
* [Azure Functions 테스트](functions-test-a-function.md)  
  함수를 테스트하는 다양한 도구와 기법을 설명합니다.  
