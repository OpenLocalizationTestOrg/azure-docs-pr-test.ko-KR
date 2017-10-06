---
title: "PostgreSQL용 Azure 데이터베이스에 대한 연결 라이브러리 | Microsoft Docs"
description: "이 문서에서는 여러 라이브러리 및 응용 프로그램 tooconnect 및 Azure 데이터베이스 쿼리 PostgreSQL에 대 한 코드를 작성할 때 개발자가 사용할 수 있는 드라이버를 설명 합니다."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/15/2017
ms.openlocfilehash: 1f7234499d8abe37f8de9008e3158765b1fb0bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connection-libraries-for-azure-database-for-postgresql"></a>PostgreSQL용 Azure 데이터베이스에 대한 연결 라이브러리
이 항목에서는 라이브러리 및 프로그래밍 PostgreSQL에 대 한 응용 프로그램 tooconnect 및 쿼리 Azure 데이터베이스에 대 한 개발자가 사용 하기 위해 드라이버를 나열 합니다.

## <a name="client-interfaces"></a>클라이언트 인터페이스
라이브러리 tooconnect tooPostgreSQL 서버에 대 한 대부분의 언어 클라이언트는 외부 프로젝트와 독립적으로 배포 됩니다. 이러한 라이브러리는 Windows, Linux 및 Mac 플랫폼에서 지원됩니다. Hello 인기 있는 클라이언트 드라이버 중 일부와 같습니다.

| **언어** | **클라이언트 인터페이스** | **추가 정보** | **다운로드** |
|--------------|----------------------------------------------------------------|-------------------------------------|--------------------------------------------------------------------|
| Python | [psycopg](http://initd.org/psycopg/) | DB API 2.0 호환 | [다운로드](http://initd.org/psycopg/download/) |
| PHP | [php-pgsql](https://php.net/manual/en/book.pgsql.php) | 데이터베이스 확장 | [설치](https://secure.php.net/manual/en/pgsql.installation.php) |
| Node.js | [Pg npm package](https://www.npmjs.com/package/pg) | 순수 JavaScript 비차단 클라이언트 | [설치](https://www.npmjs.com/package/pg) |
| 자바 | [JDBC](http://jdbc.postgresql.org/) | 형식 4 JDBC 드라이버 | [다운로드](https://jdbc.postgresql.org/download.html)  |
| 루비 | [Pg gem](https://deveiate.org/code/pg/) | Ruby 인터페이스 | [다운로드](https://rubygems.org/downloads/pg-0.20.0.gem) |
| Go | [Package pq](https://godoc.org/github.com/lib/pq) | 순수 Go postgres 드라이버 | [설치](https://github.com/lib/pq/blob/master/README.md) |
| C\#/ .NET | [Npgsql](http://www.npgsql.org/) | ADO.NET 데이터 공급자 | [다운로드](https://www.microsoft.com/net/) |
| ODBC | [psqlODBC](https://odbc.postgresql.org/) | ODBC 드라이버 | [다운로드](http://www.postgresql.org/ftp/odbc/versions/) |
| C | [libpq](https://www.postgresql.org/docs/9.6/static/libpq.html) | 기본 C 언어 인터페이스 | 포함됨 |
| C++ | [libpqxx](http://pqxx.org/) | 새 스타일 C++ 인터페이스 | [다운로드](http://pqxx.org/download/software/) |

## <a name="next-steps"></a>다음 단계
이러한 빠른 시작 방법에 읽기 Azure 선택한 언어를 사용 하 여 PostgreSQL 데이터베이스 tooconnect 및 쿼리:

[Python](./connect-python.md) | [Node.JS](./connect-nodejs.md) | [.NET(C#)](./connect-csharp.md)
