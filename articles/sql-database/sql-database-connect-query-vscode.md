---
title: "VS Code: Azure SQL Database에서 데이터 연결 및 쿼리 | Microsoft Docs"
description: "자세한 내용은 Visual Studio 코드를 사용 하 여 Azure에서 데이터베이스 tooconnect tooSQL 방법입니다. 그런 다음 TRANSACT-SQL (T-SQL) 문을 tooquery 및 편집 데이터 실행 합니다."
metacanonical: 
keywords: "toosql 데이터베이스 연결"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 676bd799-a571-4bb8-848b-fb1720007866
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/20/2017
ms.author: carlrab
ms.openlocfilehash: ed8bdbfc3271b463a21cde5ff6b5f05fd0ff51d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-use-visual-studio-code-tooconnect-and-query-data"></a>사용 가능한 Visual Studio 코드 tooconnect 및 쿼리 데이터를 azure SQL 데이터베이스:

[Visual Studio Code](https://code.visualstudio.com/docs) 는 Linux, macOS 등 용 그래픽 코드 편집기 및 확장을 포함 하 여 원하는 Windows hello [확장명이 mssql](https://aka.ms/mssql-marketplace) Microsoft SQL Server, Azure SQL 데이터베이스 및 SQL 데이터 웨어하우스를 쿼리 하기 위한 합니다. 이 빠른 시작 방법을 toouse Visual Studio Code tooconnect tooan Azure SQL 데이터베이스 및 사용 하 여 Transact SQL 문 tooquery 삽입, 업데이트 및 삭제 hello 데이터베이스의에서 데이터를 보여 줍니다.

## <a name="prerequisites"></a>필수 조건

이 빠른 시작이 빠른 시작 중 하나에서 만들어진의 시작 지점 hello 자원으로 사용 합니다.

- [DB 만들기 - 포털](sql-database-get-started-portal.md)
- [DB 만들기 - CLI](sql-database-get-started-cli.md)
- [DB 만들기 - PowerShell](sql-database-get-started-powershell.md)

시작 하기 전에 최신 버전의 hello를 설치 했는지 확인 [Visual Studio Code](https://code.visualstudio.com/Download) 찾아서 로드할 hello [확장명이 mssql](https://aka.ms/mssql-marketplace)합니다. Hello mssql 확장에 대 한 설치 지침을 참조 하십시오. [VS Code 설치](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) 참조 및 [Visual Studio Code mssql](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)합니다. 

## <a name="configure-vs-code"></a>VS 코드 구성 

### <a name="mac-os"></a>**Mac OS**
MacOS 등 tooinstall DotNet 코어 해당 mssql 확장명을 사용 하는 필수 구성 요소는 OpenSSL이 필요 합니다. 터미널을 열고 다음 명령을 tooinstall hello 입력 **끓여** 및 **OpenSSL**합니다. 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

### <a name="linux-ubuntu"></a>**Linux(Ubuntu)**

특별한 구성이 필요 없습니다.

### <a name="windows"></a>**Windows**

특별한 구성이 필요 없습니다.

## <a name="sql-server-connection-information"></a>SQL 서버 연결 정보

Hello 연결 필요한 정보 tooconnect toohello Azure SQL 데이터베이스를 가져옵니다. Hello 정규화 된 서버 이름, 데이터베이스 이름 및 로그인 정보 hello 다음 절차에 필요 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. 선택 **SQL 데이터베이스** hello 왼쪽 메뉴에서 hello에 데이터베이스를 클릭 하 고 **SQL 데이터베이스** 페이지. 
3. Hello에 **개요** 페이지 검토 hello 데이터베이스에 대 한 정규화 된 서버 이름 hello 다음 이미지와 같이 합니다. Hello 서버 이름 toobring hello 가리키면 **toocopy 클릭** 옵션입니다.

   ![연결 정보](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Azure SQL 데이터베이스 서버에 대 한 hello 로그인 정보를 잊은 경우 toohello SQL 데이터베이스 서버 페이지 tooview hello 서버 관리자 이름을 탐색 하 고, 필요한 경우 다시 설정 hello 암호입니다. 

## <a name="set-language-mode-toosql"></a>Set language 모드 tooSQL

집합 hello 언어 모드가 설정 된 너무**SQL** Visual Studio Code tooenable mssql 명령 및 T-SQL IntelliSense에서 합니다.

1. 새 Visual Studio Code 창을 엽니다. 

2. 클릭 **일반 텍스트** hello 상태 표시줄의 hello 하단 오른쪽 부분에 있습니다.
3. Hello에 **언어 선택 모드** 열리면 드롭 다운 메뉴에서 형식을 **SQL**, 누릅니다 **ENTER** tooset hello 언어 모드 tooSQL 합니다. 

   ![SQL 언어 모드](./media/sql-database-connect-query-vscode/vscode-language-mode.png)

## <a name="connect-tooyour-database"></a>Tooyour 데이터베이스 연결

Visual Studio Code tooestablish 연결 tooyour Azure SQL 데이터베이스 서버를 사용 합니다.

> [!IMPORTANT]
> 계속하기 전에 서버, 데이터베이스 및 로그인 정보를 준비했는지 확인합니다. 입력 하기 시작 하면 hello 연결 프로필 정보를 Visual Studio Code에서 포커스를 변경 하면, 되 면 hello 연결 프로필을 만드는 toorestart를 해야 합니다.
>

1. VS Code에서 눌러 **CTRL + SHIFT + P** (또는 **F1**) tooopen hello 명령 팔레트입니다.

2. **sqlcon**을 입력하고 **ENTER** 키를 누릅니다.

3. 키를 눌러 **ENTER** tooselect **연결 프로필 만들기**합니다. 그러면 SQL Server 인스턴스의 연결 프로필을 만듭니다.

4. Hello 새 연결 프로필에 대 한 hello 프롬프트 toospecify hello 연결 속성을 따릅니다. 각 값을 지정한 후 눌러 **ENTER** toocontinue 합니다. 

   | 설정       | 제안 값 | 설명 |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **서버 이름 | hello 정규화 된 서버 이름 | hello 이름은 해야 다음과 같이: **mynewserver20170313.database.windows.net**합니다. |
   | **데이터베이스 이름** | mySampleDatabase | hello 데이터베이스 toowhich tooconnect의 hello 이름입니다. |
   | **인증** | SQL 로그인| SQL 인증에는이 자습서에서는 구성 hello 유일한 인증 유형입니다. |
   | **사용자 이름** | hello 서버 관리자 계정 | Hello 서버를 만들 때 지정한 hello 계정입니다. |
   | **암호(SQL 로그인)** | 서버 관리자 계정에 대 한 hello 암호 | 이 hello 암호 hello 서버를 만들 때 지정한입니다. |
   | **암호를 저장하시겠습니까?** | 예 또는 아니요 | 원하지 않는 tooenter hello 암호 때마다 예를 선택 합니다. |
   | **이 프로필의 이름 입력** | **mySampleDatabase**와 같은 프로필 이름 | 프로필 이름을 저장할 경우 후속 로그인의 연결 속도가 빨라집니다. | 

5. 키를 눌러 hello **ESC** hello 프로필 생성 되어 연결 된 사용자에 게 알려 주는 주요 tooclose hello 정보 메시지입니다.

6. 상태 표시줄 hello에에서 대 한 연결을 확인 합니다.

   ![연결 상태](./media/sql-database-connect-query-vscode/vscode-connection-status.png)

## <a name="query-data"></a>쿼리 데이터

사용 하 여 hello 다음 hello를 사용 하 여 범주별으로 tooquery hello 상위 20 제품에 대 한 코드 [선택](https://msdn.microsoft.com/library/ms189499.aspx) Transact SQL 문입니다.

1. Hello에 **편집기** 창의 hello 다음 hello 빈 쿼리 창에서 쿼리를 입력 합니다.

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

2. 키를 눌러 **CTRL + SHIFT + E** hello Product 및 ProductCategory 테이블의 tooretrieve 데이터입니다.

    ![쿼리](./media/sql-database-connect-query-vscode/query.png)

## <a name="insert-data"></a>데이터 삽입

사용 하 여 hello 다음 코드 tooinsert 신제품 hello를 사용 하 여 hello s a l 테이블로 [삽입](https://msdn.microsoft.com/library/ms174335.aspx) Transact SQL 문입니다.

1. Hello에 **편집기** 창의 hello 이전 쿼리를 삭제 하 고 hello 다음 쿼리를 입력 합니다.

   ```sql
   INSERT INTO [SalesLT].[Product]
           ( [Name]
           , [ProductNumber]
           , [Color]
           , [ProductCategoryID]
           , [StandardCost]
           , [ListPrice]
           , [SellStartDate]
           )
     VALUES
           ('myNewProduct'
           ,123456789
           ,'NewColor'
           ,1
           ,100
           ,100
           ,GETDATE() );
   ```

2. 키를 눌러 **CTRL + SHIFT + E** tooinsert hello Product 테이블에 새 행입니다.

## <a name="update-data"></a>데이터 업데이트

사용 하 여 hello 다음 코드를 이전에 추가한 hello를 사용 하 여 tooupdate hello 새 제품 [업데이트](https://msdn.microsoft.com/library/ms177523.aspx) Transact SQL 문입니다.

1.  Hello에 **편집기** 창의 hello 이전 쿼리를 삭제 하 고 hello 다음 쿼리를 입력 합니다.

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. 키를 눌러 **CTRL + SHIFT + E** tooupdate hello hello Product 테이블에서 지정 된 행입니다.

## <a name="delete-data"></a>데이터 삭제

사용 하 여 hello 다음 코드를 이전에 추가한 hello를 사용 하 여 toodelete hello 새 제품 [삭제](https://msdn.microsoft.com/library/ms189835.aspx) Transact SQL 문입니다.

1. Hello에 **편집기** 창의 hello 이전 쿼리를 삭제 하 고 hello 다음 쿼리를 입력 합니다.

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. 키를 눌러 **CTRL + SHIFT + E** toodelete hello hello Product 테이블에서 지정 된 행입니다.

## <a name="next-steps"></a>다음 단계

- tooconnect 및 SQL Server Management Studio를 사용 하 여 쿼리 참조 [연결 및 SSMS 사용 하 여 쿼리](sql-database-connect-query-ssms.md)합니다.
- Visual Studio Code를 사용하는 MSDN 잡지 문서는 [MSSQL 확장을 사용하여 데이터베이스 IDE 만들기 블로그 게시물](https://msdn.microsoft.com/magazine/mt809115)을 참조하세요.
