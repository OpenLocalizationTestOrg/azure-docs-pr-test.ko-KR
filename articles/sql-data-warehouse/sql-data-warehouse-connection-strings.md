---
title: "SQL 데이터 웨어하우스에 대 한 aaaDrivers | Microsoft Docs"
description: "SQL 데이터 웨어하우스용 드라이버 및 연결 문자열"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 5c91f423-b550-4734-8094-c7f2c418ac8d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: a808839a8cfc49c2d7b16038c88ffb39a9f97825
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="drivers-for-azure-sql-data-warehouse"></a>Azure SQL 데이터 웨어하우스용 드라이버
여러 가지 서로 다른 응용 프로그램 프로토콜을 가진 tooSQL 데이터 웨어하우스와 같은 연결 [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP] [ PHP] 및 [JDBC][JDBC]합니다. 다음은 각 프로토콜에 대한 연결 문제열의 몇 가지 예입니다.  또한 Azure 포털 toobuild hello 연결 문자열을 사용할 수 있습니다.  toobuild Azure 포털 hello 사용 하 여 연결 문자열에서 tooyour 데이터베이스 블레이드를 탐색 *Essentials* 클릭 *데이터베이스 연결 문자열 표시*합니다.

## <a name="sample-adonet-connection-string"></a>샘플 ADO.NET 연결 문자열
```C#
Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};User ID={your_user_name};Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

## <a name="sample-odbc-connection-string"></a>샘플 ODBC 연결 문자열
```C#
Driver={SQL Server Native Client 11.0};Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};Uid={your_user_name};Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
```

## <a name="sample-php-connection-string"></a>샘플 PHP 연결 문자열
```PHP
Server: {your_server}.database.windows.net,1433 \r\nSQL Database: {your_database}\r\nUser Name: {your_user_name}\r\n\r\nPHP Data Objects(PDO) Sample Code:\r\n\r\ntry {\r\n   $conn = new PDO ( \"sqlsrv:server = tcp:{your_server}.database.windows.net,1433; Database = {your_database}\", \"{your_user_name}\", \"{your_password_here}\");\r\n    $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );\r\n}\r\ncatch ( PDOException $e ) {\r\n   print( \"Error connecting tooSQL Server.\" );\r\n   die(print_r($e));\r\n}\r\n\rSQL Server Extension Sample Code:\r\n\r\n$connectionInfo = array(\"UID\" => \"{your_user_name}\", \"pwd\" => \"{your_password_here}\", \"Database\" => \"{your_database}\", \"LoginTimeout\" => 30, \"Encrypt\" => 1, \"TrustServerCertificate\" => 0);\r\n$serverName = \"tcp:{your_server}.database.windows.net,1433\";\r\n$conn = sqlsrv_connect($serverName, $connectionInfo);
```

## <a name="sample-jdbc-connection-string"></a>샘플 JDBC 연결 문자열
```Java
jdbc:sqlserver://yourserver.database.windows.net:1433;database=yourdatabase;user={your_user_name};password={your_password_here};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
```

> [!NOTE]
> 순서 tooallow hello 연결 toosurvive 짧은 기간에 사용할 수 없게 설정 hello 연결 제한 시간 too300 초를 것이 좋습니다.
> 
> 

## <a name="next-steps"></a>다음 단계
Visual Studio 및 다른 응용 프로그램을 사용 하 여 데이터 웨어하우스 쿼리 toostart 참조 [Visual Studio와 함께 쿼리][Query with Visual Studio]합니다.

<!--Image references-->

<!--Azure.com references-->
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md

<!--MSDN references-->
[ADO.NET]: https://msdn.microsoft.com/library/e80y5yhx(v=vs.110).aspx
[ODBC]: https://msdn.microsoft.com/library/jj730314.aspx
[PHP]: https://msdn.microsoft.com/library/cc296172.aspx?f=255&MSPPError=-2147217396
[JDBC]: https://msdn.microsoft.com/library/mt484311(v=sql.110).aspx

<!--Other references-->
