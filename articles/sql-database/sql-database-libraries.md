---
title: "SQL 데이터베이스에 대 한 aaaConnection 라이브러리 | Microsoft Docs"
description: "연결 tooSQL 서버 및 다양 한 클라이언트 프로그래밍 언어의에서 SQL 데이터베이스를 사용 하도록 설정 하는 모듈의 다운로드에 대 한 링크를 제공 합니다. hello 커뮤니티를 통해 또는 Microsoft hello 모듈 해제 됩니다."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: genemi
ms.assetid: 13d899d3-cf46-4e4d-8919-cf4b41ca836d
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: genemi
ms.openlocfilehash: 6ea77670276ad3304c7531f7ffd8f7dffd31af46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connectivity-libraries-and-frameworks-for-microsoft-sql-server"></a>Microsoft SQL Server의 연결 라이브러리 및 프레임워크

체크 아웃 우리의 [시작 자습서](http://aka.ms/sqldev) tooquickly C#, Java, Node.js, PHP 및 Python 등의 언어와 프로그래밍 시작 하 고 macOS에서 Linux 또는 Windows 또는 Docker에서 SQL Server를 사용 하 여 응용 프로그램을 구축 합니다.

hello 아래 표에 연결 라이브러리 또는 *드라이버* 언어 tooconnect tooand 사용 온-프레미스를 실행 중인 Microsoft SQL Server 또는 Linux, Windows 또는 Docker에서 hello 클라우드에 다양 한 클라이언트 응용 프로그램에서 사용할 수 있습니다 및 또한 tooAzure SQL 데이터베이스 및 Azure SQL 데이터 웨어하우스 합니다. 

| 언어 | 플랫폼 | 추가 리소스 | 다운로드 | 시작 |
| :-- | :-- | :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [SQL Server용 Microsoft ADO.NET](https://docs.microsoft.com/sql/connect/ado-net/microsoft-ado-net-for-sql-server) | [다운로드](https://www.microsoft.com/net/download/) | [시작](https://www.microsoft.com/en-us/sql-server/developer-get-started/csharp/ubuntu)
| 자바 | Windows, Linux, macOS | [SQL Server용 Microsoft JDBC Driver](http://msdn.microsoft.com/library/mt484311.aspx) | [다운로드](https://go.microsoft.com/fwlink/?linkid=852460) |  [시작](https://www.microsoft.com/en-us/sql-server/developer-get-started/java/ubuntu)
| PHP | Windows, Linux, macOS| [SQL Server용 PHP SQL 드라이버](http://msdn.microsoft.com/library/dn865013.aspx) | 운영 체제: <br/> \* [Windows](https://www.microsoft.com/download/details.aspx?id=20098) <br/> \* [Linux](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) <br/> \* [macOS](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) |  [시작](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/ubuntu)
| Node.js | Windows, Linux, macOS | [SQL Server용 Node.js 드라이버](http://msdn.microsoft.com/library/mt652093.aspx) | [설치](https://msdn.microsoft.com/library/mt652094.aspx) |  [시작](https://www.microsoft.com/en-us/sql-server/developer-get-started/node/ubuntu)
| 파이썬 | Windows, Linux, macOS | [Python SQL 드라이버](http://msdn.microsoft.com/library/mt652092.aspx) | 다음 선택 항목을 설치합니다. <br/> \* [pymssql](https://msdn.microsoft.com/library/mt694094.aspx) <br/> \* [pyodbc](http://msdn.microsoft.com/library/mt763257.aspx) |  [시작](https://www.microsoft.com/en-us/sql-server/developer-get-started/python/ubuntu)
| Ruby | Windows, Linux, macOS | [SQL Server용 Ruby 드라이버](http://msdn.microsoft.com/library/mt691981.aspx) | [설치](https://msdn.microsoft.com/library/mt711041.aspx) | [시작](https://www.microsoft.com/en-us/sql-server/developer-get-started/ruby/ubuntu)
| C++ | Windows, Linux, macOS | [SQL Server용 Microsoft ODBC 드라이버](https://msdn.microsoft.com/en-us/library/mt654048(v=sql.1).aspx) | [다운로드](https://msdn.microsoft.com/en-us/library/mt654048(v=sql.1).aspx) |  

hello 아래 표에 Linux, Windows 또는 Docker 및 또한 tooAzure SQL 데이터베이스에서 hello 클라우드에서 개체 관계형 매핑 ORM () 프레임 워크 및 클라이언트 응용 프로그램은 온-프레미스를 실행 중인 Microsoft SQL Server 또는 사용할 수 있는 웹 프레임 워크의 몇 가지 예 및 Azure SQL 데이터 웨어하우스 

| 언어 | 플랫폼 | ORM |
| :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [Entity Framework](https://docs.microsoft.com/en-us/ef)<br>[Entity Framework Core](https://docs.microsoft.com/en-us/ef/core/index) |
| 자바 | Windows, Linux, macOS |[Hibernate ORM](http://hibernate.org/orm)|
| PHP | Windows, Linux | [Laravel(Eloquent)](https://laravel.com/docs/5.0/eloquent) |
| Node.js | Windows, Linux, macOS | [Sequelize ORM](http://docs.sequelizejs.com) |
| 파이썬 | Windows, Linux, macOS |[Django](https://www.djangoproject.com/) |
| Ruby | Windows, Linux, macOS | [Ruby on Rails](http://rubyonrails.org/) |

## <a name="related-links"></a>관련 링크
- 클라이언트 응용 프로그램에서 연결하기 위한 [SQL Server 드라이버](http://msdn.microsoft.com/library/mt654049.aspx)
- [.NET (C#)를 사용 하 여 tooSQL 데이터베이스 연결](sql-database-connect-query-dotnet.md)
- [PHP를 사용 하 여 tooSQL 데이터베이스 연결](sql-database-connect-query-php.md)
- [Node.js를 사용 하 여 tooSQL 데이터베이스 연결](sql-database-connect-query-nodejs.md)
- [Java를 사용 하 여 tooSQL 데이터베이스 연결](sql-database-connect-query-java.md)
- [Python을 사용 하 여 tooSQL 데이터베이스 연결](sql-database-connect-query-python.md)
- [Ruby를 사용 하 여 tooSQL 데이터베이스 연결](sql-database-connect-query-ruby.md)
