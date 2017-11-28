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
# <a name="azure-sql-database-use-visual-studio-code-tooconnect-and-query-data"></a><span data-ttu-id="4b372-105">사용 가능한 Visual Studio 코드 tooconnect 및 쿼리 데이터를 azure SQL 데이터베이스:</span><span class="sxs-lookup"><span data-stu-id="4b372-105">Azure SQL Database: Use Visual Studio Code tooconnect and query data</span></span>

<span data-ttu-id="4b372-106">[Visual Studio Code](https://code.visualstudio.com/docs) 는 Linux, macOS 등 용 그래픽 코드 편집기 및 확장을 포함 하 여 원하는 Windows hello [확장명이 mssql](https://aka.ms/mssql-marketplace) Microsoft SQL Server, Azure SQL 데이터베이스 및 SQL 데이터 웨어하우스를 쿼리 하기 위한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-106">[Visual Studio Code](https://code.visualstudio.com/docs) is a graphical code editor for Linux, macOS, and Windows that supports extensions, including hello [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="4b372-107">이 빠른 시작 방법을 toouse Visual Studio Code tooconnect tooan Azure SQL 데이터베이스 및 사용 하 여 Transact SQL 문 tooquery 삽입, 업데이트 및 삭제 hello 데이터베이스의에서 데이터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-107">This quick start demonstrates how toouse Visual Studio Code tooconnect tooan Azure SQL database, and then use Transact-SQL statements tooquery, insert, update, and delete data in hello database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b372-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4b372-108">Prerequisites</span></span>

<span data-ttu-id="4b372-109">이 빠른 시작이 빠른 시작 중 하나에서 만들어진의 시작 지점 hello 자원으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-109">This quick start uses as its starting point hello resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="4b372-110">DB 만들기 - 포털</span><span class="sxs-lookup"><span data-stu-id="4b372-110">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="4b372-111">DB 만들기 - CLI</span><span class="sxs-lookup"><span data-stu-id="4b372-111">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
- [<span data-ttu-id="4b372-112">DB 만들기 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b372-112">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

<span data-ttu-id="4b372-113">시작 하기 전에 최신 버전의 hello를 설치 했는지 확인 [Visual Studio Code](https://code.visualstudio.com/Download) 찾아서 로드할 hello [확장명이 mssql](https://aka.ms/mssql-marketplace)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-113">Before you start, make sure you have installed hello newest version of [Visual Studio Code](https://code.visualstudio.com/Download) and loaded hello [mssql extension](https://aka.ms/mssql-marketplace).</span></span> <span data-ttu-id="4b372-114">Hello mssql 확장에 대 한 설치 지침을 참조 하십시오. [VS Code 설치](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) 참조 및 [Visual Studio Code mssql](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-114">For installation guidance for hello mssql extension, see [Install VS Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) and see [mssql for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).</span></span> 

## <a name="configure-vs-code"></a><span data-ttu-id="4b372-115">VS 코드 구성</span><span class="sxs-lookup"><span data-stu-id="4b372-115">Configure VS Code</span></span> 

### <a name="mac-os"></a><span data-ttu-id="4b372-116">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="4b372-116">**Mac OS**</span></span>
<span data-ttu-id="4b372-117">MacOS 등 tooinstall DotNet 코어 해당 mssql 확장명을 사용 하는 필수 구성 요소는 OpenSSL이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-117">For macOS, you need tooinstall OpenSSL which is a prerequiste for DotNet Core that mssql extention uses.</span></span> <span data-ttu-id="4b372-118">터미널을 열고 다음 명령을 tooinstall hello 입력 **끓여** 및 **OpenSSL**합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-118">Open your terminal and enter hello following commands tooinstall **brew** and **OpenSSL**.</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

### <a name="linux-ubuntu"></a><span data-ttu-id="4b372-119">**Linux(Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="4b372-119">**Linux (Ubuntu)**</span></span>

<span data-ttu-id="4b372-120">특별한 구성이 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-120">No special configuration needed.</span></span>

### <a name="windows"></a><span data-ttu-id="4b372-121">**Windows**</span><span class="sxs-lookup"><span data-stu-id="4b372-121">**Windows**</span></span>

<span data-ttu-id="4b372-122">특별한 구성이 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-122">No special configuration needed.</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="4b372-123">SQL 서버 연결 정보</span><span class="sxs-lookup"><span data-stu-id="4b372-123">SQL server connection information</span></span>

<span data-ttu-id="4b372-124">Hello 연결 필요한 정보 tooconnect toohello Azure SQL 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-124">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="4b372-125">Hello 정규화 된 서버 이름, 데이터베이스 이름 및 로그인 정보 hello 다음 절차에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-125">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="4b372-126">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-126">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4b372-127">선택 **SQL 데이터베이스** hello 왼쪽 메뉴에서 hello에 데이터베이스를 클릭 하 고 **SQL 데이터베이스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="4b372-127">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="4b372-128">Hello에 **개요** 페이지 검토 hello 데이터베이스에 대 한 정규화 된 서버 이름 hello 다음 이미지와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-128">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="4b372-129">Hello 서버 이름 toobring hello 가리키면 **toocopy 클릭** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-129">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>

   ![연결 정보](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="4b372-131">Azure SQL 데이터베이스 서버에 대 한 hello 로그인 정보를 잊은 경우 toohello SQL 데이터베이스 서버 페이지 tooview hello 서버 관리자 이름을 탐색 하 고, 필요한 경우 다시 설정 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-131">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span> 

## <a name="set-language-mode-toosql"></a><span data-ttu-id="4b372-132">Set language 모드 tooSQL</span><span class="sxs-lookup"><span data-stu-id="4b372-132">Set language mode tooSQL</span></span>

<span data-ttu-id="4b372-133">집합 hello 언어 모드가 설정 된 너무**SQL** Visual Studio Code tooenable mssql 명령 및 T-SQL IntelliSense에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-133">Set hello language mode is set too**SQL** in Visual Studio Code tooenable mssql commands and T-SQL IntelliSense.</span></span>

1. <span data-ttu-id="4b372-134">새 Visual Studio Code 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-134">Open a new Visual Studio Code window.</span></span> 

2. <span data-ttu-id="4b372-135">클릭 **일반 텍스트** hello 상태 표시줄의 hello 하단 오른쪽 부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-135">Click **Plain Text** in hello lower right-hand corner of hello status bar.</span></span>
3. <span data-ttu-id="4b372-136">Hello에 **언어 선택 모드** 열리면 드롭 다운 메뉴에서 형식을 **SQL**, 누릅니다 **ENTER** tooset hello 언어 모드 tooSQL 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-136">In hello **Select language mode** drop-down menu that opens, type **SQL**, and then press **ENTER** tooset hello language mode tooSQL.</span></span> 

   ![SQL 언어 모드](./media/sql-database-connect-query-vscode/vscode-language-mode.png)

## <a name="connect-tooyour-database"></a><span data-ttu-id="4b372-138">Tooyour 데이터베이스 연결</span><span class="sxs-lookup"><span data-stu-id="4b372-138">Connect tooyour database</span></span>

<span data-ttu-id="4b372-139">Visual Studio Code tooestablish 연결 tooyour Azure SQL 데이터베이스 서버를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-139">Use Visual Studio Code tooestablish a connection tooyour Azure SQL Database server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4b372-140">계속하기 전에 서버, 데이터베이스 및 로그인 정보를 준비했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-140">Before continuing, make sure that you have your server, database, and login information ready.</span></span> <span data-ttu-id="4b372-141">입력 하기 시작 하면 hello 연결 프로필 정보를 Visual Studio Code에서 포커스를 변경 하면, 되 면 hello 연결 프로필을 만드는 toorestart를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-141">Once you begin entering hello connection profile information, if you change your focus from Visual Studio Code, you have toorestart creating hello connection profile.</span></span>
>

1. <span data-ttu-id="4b372-142">VS Code에서 눌러 **CTRL + SHIFT + P** (또는 **F1**) tooopen hello 명령 팔레트입니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-142">In VS Code, press **CTRL+SHIFT+P** (or **F1**) tooopen hello Command Palette.</span></span>

2. <span data-ttu-id="4b372-143">**sqlcon**을 입력하고 **ENTER** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-143">Type **sqlcon** and press **ENTER**.</span></span>

3. <span data-ttu-id="4b372-144">키를 눌러 **ENTER** tooselect **연결 프로필 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-144">Press **ENTER** tooselect **Create Connection Profile**.</span></span> <span data-ttu-id="4b372-145">그러면 SQL Server 인스턴스의 연결 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-145">This creates a connection profile for your SQL Server instance.</span></span>

4. <span data-ttu-id="4b372-146">Hello 새 연결 프로필에 대 한 hello 프롬프트 toospecify hello 연결 속성을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-146">Follow hello prompts toospecify hello connection properties for hello new connection profile.</span></span> <span data-ttu-id="4b372-147">각 값을 지정한 후 눌러 **ENTER** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-147">After specifying each value, press **ENTER** toocontinue.</span></span> 

   | <span data-ttu-id="4b372-148">설정</span><span class="sxs-lookup"><span data-stu-id="4b372-148">Setting</span></span>       | <span data-ttu-id="4b372-149">제안 값</span><span class="sxs-lookup"><span data-stu-id="4b372-149">Suggested value</span></span> | <span data-ttu-id="4b372-150">설명</span><span class="sxs-lookup"><span data-stu-id="4b372-150">Description</span></span> |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="4b372-151">**서버 이름</span><span class="sxs-lookup"><span data-stu-id="4b372-151">**Server name</span></span> | <span data-ttu-id="4b372-152">hello 정규화 된 서버 이름</span><span class="sxs-lookup"><span data-stu-id="4b372-152">hello fully qualified server name</span></span> | <span data-ttu-id="4b372-153">hello 이름은 해야 다음과 같이: **mynewserver20170313.database.windows.net**합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-153">hello name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="4b372-154">**데이터베이스 이름**</span><span class="sxs-lookup"><span data-stu-id="4b372-154">**Database name**</span></span> | <span data-ttu-id="4b372-155">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="4b372-155">mySampleDatabase</span></span> | <span data-ttu-id="4b372-156">hello 데이터베이스 toowhich tooconnect의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-156">hello name of hello database toowhich tooconnect.</span></span> |
   | <span data-ttu-id="4b372-157">**인증**</span><span class="sxs-lookup"><span data-stu-id="4b372-157">**Authentication**</span></span> | <span data-ttu-id="4b372-158">SQL 로그인</span><span class="sxs-lookup"><span data-stu-id="4b372-158">SQL Login</span></span>| <span data-ttu-id="4b372-159">SQL 인증에는이 자습서에서는 구성 hello 유일한 인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-159">SQL Authentication is hello only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="4b372-160">**사용자 이름**</span><span class="sxs-lookup"><span data-stu-id="4b372-160">**User name**</span></span> | <span data-ttu-id="4b372-161">hello 서버 관리자 계정</span><span class="sxs-lookup"><span data-stu-id="4b372-161">hello server admin account</span></span> | <span data-ttu-id="4b372-162">Hello 서버를 만들 때 지정한 hello 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-162">This is hello account that you specified when you created hello server.</span></span> |
   | <span data-ttu-id="4b372-163">**암호(SQL 로그인)**</span><span class="sxs-lookup"><span data-stu-id="4b372-163">**Password (SQL Login)**</span></span> | <span data-ttu-id="4b372-164">서버 관리자 계정에 대 한 hello 암호</span><span class="sxs-lookup"><span data-stu-id="4b372-164">hello password for your server admin account</span></span> | <span data-ttu-id="4b372-165">이 hello 암호 hello 서버를 만들 때 지정한입니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-165">This is hello password that you specified when you created hello server.</span></span> |
   | <span data-ttu-id="4b372-166">**암호를 저장하시겠습니까?**</span><span class="sxs-lookup"><span data-stu-id="4b372-166">**Save Password?**</span></span> | <span data-ttu-id="4b372-167">예 또는 아니요</span><span class="sxs-lookup"><span data-stu-id="4b372-167">Yes or No</span></span> | <span data-ttu-id="4b372-168">원하지 않는 tooenter hello 암호 때마다 예를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-168">Select Yes if you do not want tooenter hello password each time.</span></span> |
   | <span data-ttu-id="4b372-169">**이 프로필의 이름 입력**</span><span class="sxs-lookup"><span data-stu-id="4b372-169">**Enter a name for this profile**</span></span> | <span data-ttu-id="4b372-170">**mySampleDatabase**와 같은 프로필 이름</span><span class="sxs-lookup"><span data-stu-id="4b372-170">A profile name, such as **mySampleDatabase**</span></span> | <span data-ttu-id="4b372-171">프로필 이름을 저장할 경우 후속 로그인의 연결 속도가 빨라집니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-171">A saved profile name speeds your connection on subsequent logins.</span></span> | 

5. <span data-ttu-id="4b372-172">키를 눌러 hello **ESC** hello 프로필 생성 되어 연결 된 사용자에 게 알려 주는 주요 tooclose hello 정보 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-172">Press hello **ESC** key tooclose hello info message that informs you that hello profile is created and connected.</span></span>

6. <span data-ttu-id="4b372-173">상태 표시줄 hello에에서 대 한 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-173">Verify your connection in hello status bar.</span></span>

   ![연결 상태](./media/sql-database-connect-query-vscode/vscode-connection-status.png)

## <a name="query-data"></a><span data-ttu-id="4b372-175">쿼리 데이터</span><span class="sxs-lookup"><span data-stu-id="4b372-175">Query data</span></span>

<span data-ttu-id="4b372-176">사용 하 여 hello 다음 hello를 사용 하 여 범주별으로 tooquery hello 상위 20 제품에 대 한 코드 [선택](https://msdn.microsoft.com/library/ms189499.aspx) Transact SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-176">Use hello following code tooquery for hello top 20 products by category using hello [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="4b372-177">Hello에 **편집기** 창의 hello 다음 hello 빈 쿼리 창에서 쿼리를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-177">In hello **Editor** window, enter hello following query in hello empty query window:</span></span>

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

2. <span data-ttu-id="4b372-178">키를 눌러 **CTRL + SHIFT + E** hello Product 및 ProductCategory 테이블의 tooretrieve 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-178">Press **CTRL+SHIFT+E** tooretrieve data from hello Product and ProductCategory tables.</span></span>

    ![쿼리](./media/sql-database-connect-query-vscode/query.png)

## <a name="insert-data"></a><span data-ttu-id="4b372-180">데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="4b372-180">Insert data</span></span>

<span data-ttu-id="4b372-181">사용 하 여 hello 다음 코드 tooinsert 신제품 hello를 사용 하 여 hello s a l 테이블로 [삽입](https://msdn.microsoft.com/library/ms174335.aspx) Transact SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-181">Use hello following code tooinsert a new product into hello SalesLT.Product table using hello [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="4b372-182">Hello에 **편집기** 창의 hello 이전 쿼리를 삭제 하 고 hello 다음 쿼리를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-182">In hello **Editor** window, delete hello previous query and enter hello following query:</span></span>

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

2. <span data-ttu-id="4b372-183">키를 눌러 **CTRL + SHIFT + E** tooinsert hello Product 테이블에 새 행입니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-183">Press **CTRL+SHIFT+E** tooinsert a new row in hello Product table.</span></span>

## <a name="update-data"></a><span data-ttu-id="4b372-184">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="4b372-184">Update data</span></span>

<span data-ttu-id="4b372-185">사용 하 여 hello 다음 코드를 이전에 추가한 hello를 사용 하 여 tooupdate hello 새 제품 [업데이트](https://msdn.microsoft.com/library/ms177523.aspx) Transact SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-185">Use hello following code tooupdate hello new product that you previously added using hello [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement.</span></span>

1.  <span data-ttu-id="4b372-186">Hello에 **편집기** 창의 hello 이전 쿼리를 삭제 하 고 hello 다음 쿼리를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-186">In hello **Editor** window, delete hello previous query and enter hello following query:</span></span>

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="4b372-187">키를 눌러 **CTRL + SHIFT + E** tooupdate hello hello Product 테이블에서 지정 된 행입니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-187">Press **CTRL+SHIFT+E** tooupdate hello specified row in hello Product table.</span></span>

## <a name="delete-data"></a><span data-ttu-id="4b372-188">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="4b372-188">Delete data</span></span>

<span data-ttu-id="4b372-189">사용 하 여 hello 다음 코드를 이전에 추가한 hello를 사용 하 여 toodelete hello 새 제품 [삭제](https://msdn.microsoft.com/library/ms189835.aspx) Transact SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-189">Use hello following code toodelete hello new product that you previously added using hello [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="4b372-190">Hello에 **편집기** 창의 hello 이전 쿼리를 삭제 하 고 hello 다음 쿼리를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-190">In hello **Editor** window, delete hello previous query and enter hello following query:</span></span>

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="4b372-191">키를 눌러 **CTRL + SHIFT + E** toodelete hello hello Product 테이블에서 지정 된 행입니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-191">Press **CTRL+SHIFT+E** toodelete hello specified row in hello Product table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b372-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4b372-192">Next steps</span></span>

- <span data-ttu-id="4b372-193">tooconnect 및 SQL Server Management Studio를 사용 하 여 쿼리 참조 [연결 및 SSMS 사용 하 여 쿼리](sql-database-connect-query-ssms.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b372-193">tooconnect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md).</span></span>
- <span data-ttu-id="4b372-194">Visual Studio Code를 사용하는 MSDN 잡지 문서는 [MSSQL 확장을 사용하여 데이터베이스 IDE 만들기 블로그 게시물](https://msdn.microsoft.com/magazine/mt809115)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b372-194">For an MSDN magazine article on using Visual Studio Code, see [Create a database IDE with MSSQL extension blog post](https://msdn.microsoft.com/magazine/mt809115).</span></span>
