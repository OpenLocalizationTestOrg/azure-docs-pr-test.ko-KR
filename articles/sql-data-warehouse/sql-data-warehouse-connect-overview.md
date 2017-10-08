---
title: "SQL 데이터 웨어하우스 aaaConnect tooAzure | Microsoft Docs"
description: "SQL 데이터 웨어하우스를 tooAzure 프로그램에 대 한 문자열 toofind hello 서버 이름 및 연결"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: e52872ca-ae74-4e25-9c56-d49c85c8d0f0
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: f15e098026afb7c5efbbbfaf62b681e8cd7936bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-sql-data-warehouse"></a>SQL 데이터 웨어하우스 tooAzure 연결
이 문서에는 처음으로 hello에 대 한 연결 된 tooSQL 데이터 웨어하우스를 얻을 수 있습니다.

## <a name="find-your-server-name"></a>서버 이름 찾기
데이터 웨어하우스 알고 있으면 첫 번째 단계 tooconnecting tooSQL hello 어떻게 toofind 서버 이름입니다.  예를 들어, 다음 예제는 hello에 서버 이름을 hello sample.database.windows.net입니다. toofind hello 정규화 된 서버 이름:

1. Toohello 이동 [Azure 포털][Azure portal]합니다.
2. **SQL Database** 
3. tooconnect hello 데이터베이스를 클릭 합니다.
4. Hello 전체 서버 이름을 찾습니다.
   
    ![전체 서버 이름][1]

## <a name="supported-drivers-and-connection-strings"></a>지원되는 드라이버 및 연결 문자열
Azure SQL Data Warehouse는 [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP] 및 [JDBC][JDBC]를 지원합니다. Hello 중 하나를 클릭 앞에 드라이버 toofind hello에 대 한 최신 정보 및 설명서입니다. tooautomatically hello Azure에서에서 사용 하는 hello 드라이버에 대 한 연결 문자열 hello를 생성 합니다. 포털을 클릭할 때 hello **데이터베이스 연결 문자열 표시** hello 예에서는 앞에서 합니다.  또한 각 드라이버에 대한 연결 문자열의 모양에 대한 몇 가지 예는 다음과 같습니다.

> [!NOTE]
> Hello 연결 제한 시간 too300 초 tooallow 연결 toosurvive 짧은 기간 동안 사용할 수 없게 설정 하는 것이 좋습니다.
> 
> 

### <a name="adonet-connection-string-example"></a>ADO.NET 연결 문자열 예제
```C#
Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};User ID={your_user_name};Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

### <a name="odbc-connection-string-example"></a>ODBC 연결 문자열 예제
```C#
Driver={SQL Server Native Client 11.0};Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};Uid={your_user_name};Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
```

### <a name="php-connection-string-example"></a>PHP 연결 문자열 예제
```PHP
Server: {your_server}.database.windows.net,1433 \r\nSQL Database: {your_database}\r\nUser Name: {your_user_name}\r\n\r\nPHP Data Objects(PDO) Sample Code:\r\n\r\ntry {\r\n   $conn = new PDO ( \"sqlsrv:server = tcp:{your_server}.database.windows.net,1433; Database = {your_database}\", \"{your_user_name}\", \"{your_password_here}\");\r\n    $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );\r\n}\r\ncatch ( PDOException $e ) {\r\n   print( \"Error connecting tooSQL Server.\" );\r\n   die(print_r($e));\r\n}\r\n\rSQL Server Extension Sample Code:\r\n\r\n$connectionInfo = array(\"UID\" => \"{your_user_name}\", \"pwd\" => \"{your_password_here}\", \"Database\" => \"{your_database}\", \"LoginTimeout\" => 30, \"Encrypt\" => 1, \"TrustServerCertificate\" => 0);\r\n$serverName = \"tcp:{your_server}.database.windows.net,1433\";\r\n$conn = sqlsrv_connect($serverName, $connectionInfo);
```

### <a name="jdbc-connection-string-example"></a>JDBC 연결 문자열 예제
```Java
jdbc:sqlserver://yourserver.database.windows.net:1433;database=yourdatabase;user={your_user_name};password={your_password_here};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
```

## <a name="connection-settings"></a>연결 설정
SQL Data Warehouse는 연결 및 개체 생성 중에 몇 가지 설정을 표준화합니다. 이러한 설정은 재정의되거나 다음을 포함할 수 없습니다.

| 데이터베이스 설정 | 값 |
|:--- |:--- |
| [ANSI_NULLS][ANSI_NULLS] |켜기 |
| [QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS] |켜기 |
| [DATEFORMAT][DATEFORMAT] |mdy |
| [DATEFIRST][DATEFIRST] |7 |

## <a name="next-steps"></a>다음 단계
tooconnect 및 Visual Studio와 함께 쿼리 참조 [Visual Studio와 함께 쿼리][Query with Visual Studio]합니다. 인증 옵션에 대해 자세히 toolearn 참조 [인증 tooAzure SQL 데이터 웨어하우스][Authentication tooAzure SQL Data Warehouse]합니다.

<!--Articles-->
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[Authentication tooAzure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[ADO.NET]: https://msdn.microsoft.com/library/e80y5yhx(v=vs.110).aspx
[ODBC]: https://msdn.microsoft.com/library/jj730314.aspx
[PHP]: https://msdn.microsoft.com/library/cc296172.aspx?f=255&MSPPError=-2147217396
[JDBC]: https://msdn.microsoft.com/library/mt484311(v=sql.110).aspx
[ANSI_NULLS]: https://msdn.microsoft.com/library/ms188048.aspx
[QUOTED_IDENTIFIERS]: https://msdn.microsoft.com/library/ms174393.aspx
[DATEFORMAT]: https://msdn.microsoft.com/library/ms189491.aspx
[DATEFIRST]: https://msdn.microsoft.com/library/ms181598.aspx

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->
[1]: media/sql-data-warehouse-connect-overview/get-server-name.png


