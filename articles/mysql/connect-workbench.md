---
title: "MySQL 워크 벤치에서 MySQL에 대 한 데이터베이스 tooAzure 연결 | Microsoft Docs"
description: "이 퀵 스타트의 MySQL 용 hello 단계 toouse MySQL 워크 벤치 Azure 데이터베이스에서 tooconnect 및 쿼리 데이터를 제공합니다."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: c64fcb9bb99ba06aa3a95eec420d5d5ef4a31d14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-tooconnect-and-query-data"></a><span data-ttu-id="b88ce-103">MySQL에 대 한 azure 데이터베이스: 사용 하 여 MySQL 워크 벤치 tooconnect 및 쿼리 데이터</span><span class="sxs-lookup"><span data-stu-id="b88ce-103">Azure Database for MySQL: Use MySQL Workbench tooconnect and query data</span></span>
<span data-ttu-id="b88ce-104">이 빠른 시작에서는 방법을 사용 하 여 MySQL에 대 한 Azure 데이터베이스 tooconnect tooan hello MySQL 워크 벤치 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using hello MySQL Workbench application.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b88ce-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b88ce-105">Prerequisites</span></span>
<span data-ttu-id="b88ce-106">이 퀵 스타트의 시작 지점으로이 가이드의 중 하나에서 만든 hello 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-106">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="b88ce-107">Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="b88ce-107">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="b88ce-108">Azure CLI를 사용한 MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="b88ce-108">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a><span data-ttu-id="b88ce-109">MySQL Workbench 설치</span><span class="sxs-lookup"><span data-stu-id="b88ce-109">Install MySQL Workbench</span></span>
<span data-ttu-id="b88ce-110">다운로드 하 여 MySQL 워크 벤치에서 컴퓨터에 설치 [hello MySQL 웹 사이트](https://dev.mysql.com/downloads/workbench/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-110">Download and install MySQL Workbench on your computer from [hello MySQL website](https://dev.mysql.com/downloads/workbench/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="b88ce-111">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="b88ce-111">Get connection information</span></span>
<span data-ttu-id="b88ce-112">MySQL 용 hello 연결 필요한 정보 tooconnect toohello를 Azure 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-112">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="b88ce-113">정규화 된 서버 이름 및 로그인 자격 증명 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-113">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="b88ce-114">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-114">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="b88ce-115">Azure 포털에서 왼쪽 메뉴 hello에서에서 클릭 **모든 리소스** 등 생성 한 hello 서버에 대 한 검색 **myserver4demo**합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-115">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>

3. <span data-ttu-id="b88ce-116">Hello 서버 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-116">Click hello server name.</span></span>

4. <span data-ttu-id="b88ce-117">선택 hello 서버 **속성** 페이지.</span><span class="sxs-lookup"><span data-stu-id="b88ce-117">Select hello server's **Properties** page.</span></span> <span data-ttu-id="b88ce-118">Hello 메모 **서버 이름** 및 **서버 관리자 로그인 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-118">Make a note of hello **Server name** and **Server admin login name**.</span></span>

 ![MySQL용 Azure Database 서버 이름](./media/connect-workbench/1-server-properties-name-login.png)
 
5. <span data-ttu-id="b88ce-120">서버 로그인 정보를 잊은 경우 탐색 toohello **개요** tooview hello 서버 관리자 로그인 이름 페이지 하 고 필요한 경우 다시 설정 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-120">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-toohello-server-using-mysql-workbench"></a><span data-ttu-id="b88ce-121">MySQL 워크 벤치를 사용 하 여 toohello 서버 연결</span><span class="sxs-lookup"><span data-stu-id="b88ce-121">Connect toohello server using MySQL Workbench</span></span> 
<span data-ttu-id="b88ce-122">MySQL 워크 벤치 hello GUI 도구를 사용 하 여 tooconnect tooAzure MySQL 서버:</span><span class="sxs-lookup"><span data-stu-id="b88ce-122">tooconnect tooAzure MySQL server using hello GUI tool MySQL Workbench:</span></span>

1.  <span data-ttu-id="b88ce-123">Hello 컴퓨터에서 MySQL 워크 벤치 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-123">Launch hello MySQL Workbench application on your computer.</span></span> 

2.  <span data-ttu-id="b88ce-124">**새 연결을 설정** 대화 상자를 hello hello에 다음 정보를 입력 **매개 변수** 탭:</span><span class="sxs-lookup"><span data-stu-id="b88ce-124">In **Setup New Connection** dialog box, enter hello following information on hello **Parameters** tab:</span></span>

    ![새 연결 설정](./media/connect-workbench/2-setup-new-connection.png)

    | <span data-ttu-id="b88ce-126">**설정**</span><span class="sxs-lookup"><span data-stu-id="b88ce-126">**Setting**</span></span> | <span data-ttu-id="b88ce-127">**제안 값**</span><span class="sxs-lookup"><span data-stu-id="b88ce-127">**Suggested value**</span></span> | <span data-ttu-id="b88ce-128">**필드 설명**</span><span class="sxs-lookup"><span data-stu-id="b88ce-128">**Field description**</span></span> |
    |---|---|---|
    |   <span data-ttu-id="b88ce-129">연결 이름</span><span class="sxs-lookup"><span data-stu-id="b88ce-129">Connection Name</span></span> | <span data-ttu-id="b88ce-130">데모 연결</span><span class="sxs-lookup"><span data-stu-id="b88ce-130">Demo Connection</span></span> | <span data-ttu-id="b88ce-131">이 연결에 대한 레이블을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-131">Specify a label for this connection.</span></span> |
    | <span data-ttu-id="b88ce-132">연결 방법</span><span class="sxs-lookup"><span data-stu-id="b88ce-132">Connection Method</span></span> | <span data-ttu-id="b88ce-133">표준(TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="b88ce-133">Standard (TCP/IP)</span></span> | <span data-ttu-id="b88ce-134">표준(TCP/IP)이면 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-134">Standard (TCP/IP) is sufficient.</span></span> |
    | <span data-ttu-id="b88ce-135">호스트 이름</span><span class="sxs-lookup"><span data-stu-id="b88ce-135">Hostname</span></span> | <span data-ttu-id="b88ce-136">*서버 이름*</span><span class="sxs-lookup"><span data-stu-id="b88ce-136">*server name*</span></span> | <span data-ttu-id="b88ce-137">이전 MySQL 용 hello Azure 데이터베이스를 만들 때 사용 된 hello 서버 이름 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-137">Specify hello server name value that was used when you created hello Azure Database for MySQL earlier.</span></span> <span data-ttu-id="b88ce-138">표시된 예제 서버는 myserver4demo.mysql.database.azure.com입니다. Hello 정규화 된 도메인 이름 사용 (\*. mysql.database.azure.com) hello 예제에 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-138">Our example server shown is myserver4demo.mysql.database.azure.com. Use hello fully qualified domain name (\*.mysql.database.azure.com) as shown in hello example.</span></span> <span data-ttu-id="b88ce-139">서버 이름을 기억 하지 못하는 경우에 hello 이전 섹션 tooget hello 연결 정보에 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-139">Follow hello steps in hello previous section tooget hello connection information if you do not remember your server name.</span></span>  |
    | <span data-ttu-id="b88ce-140">포트</span><span class="sxs-lookup"><span data-stu-id="b88ce-140">Port</span></span> | <span data-ttu-id="b88ce-141">3306</span><span class="sxs-lookup"><span data-stu-id="b88ce-141">3306</span></span> | <span data-ttu-id="b88ce-142">항상 3306 MySQL 용 tooAzure 데이터베이스를 연결할 때 포트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-142">Always use port 3306 when connecting tooAzure Database for MySQL.</span></span> |
    | <span data-ttu-id="b88ce-143">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="b88ce-143">Username</span></span> |  <span data-ttu-id="b88ce-144">*서버 관리자 로그인 이름*</span><span class="sxs-lookup"><span data-stu-id="b88ce-144">*server admin login name*</span></span> | <span data-ttu-id="b88ce-145">Hello 서버 관리자 로그인 사용자 이름 앞 MySQL 용 hello Azure 데이터베이스를 만들 때 제공 된 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-145">Type in hello server admin login username supplied when you created hello Azure Database for MySQL earlier.</span></span> <span data-ttu-id="b88ce-146">이 예제에서는 사용자 이름이 myadmin@myserver4demo입니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-146">Our example username is myadmin@myserver4demo.</span></span> <span data-ttu-id="b88ce-147">Hello username 기억 하지 못하는 경우에 hello 이전 섹션 tooget hello 연결 정보에 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-147">Follow hello steps in hello previous section tooget hello connection information if you do not remember hello username.</span></span> <span data-ttu-id="b88ce-148">hello 형식은  *username@servername* 합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-148">hello format is *username@servername*.</span></span>
    | <span data-ttu-id="b88ce-149">암호</span><span class="sxs-lookup"><span data-stu-id="b88ce-149">Password</span></span> | <span data-ttu-id="b88ce-150">사용자 암호</span><span class="sxs-lookup"><span data-stu-id="b88ce-150">your password</span></span> | <span data-ttu-id="b88ce-151">클릭 **자격 증명 모음에 저장 중...**  단추 toosave hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-151">Click **Store in Vault...** button toosave hello password.</span></span> |

3.   <span data-ttu-id="b88ce-152">클릭 **연결 테스트** tootest 모든 매개 변수가 올바르게 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-152">Click **Test Connection** tootest if all parameters are correctly configured.</span></span> 

4.   <span data-ttu-id="b88ce-153">클릭 **확인** toosave hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-153">Click **OK** toosave hello connection.</span></span> 

5.   <span data-ttu-id="b88ce-154">hello 목록에서 **MySQL이 연결 되어**hello 연결 toobe 설정 될 때까지 기다리는 hello 타일 해당 tooyour 서버를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-154">In hello listing of **MySQL Connections**, click hello tile corresponding tooyour server and wait for hello connection toobe established.</span></span>

6.   <span data-ttu-id="b88ce-155">새 SQL 탭이 쿼리를 입력할 수 있는 빈 편집기로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-155">A new SQL tab opens with a blank editor where you can type your queries.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b88ce-156">기본적으로 SSL 연결 보안이 필요하며 MySQL 서버용 Azure Database에서 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-156">By default, SSL connection security is required and enforced on your Azure Database for MySQL server.</span></span> <span data-ttu-id="b88ce-157">일반적으로 SSL 인증서를 추가 구성 없이 MySQL 워크 벤치 tooconnect tooyour 서버에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-157">Typically no additional configuration with SSL certificates is required for MySQL Workbench tooconnect tooyour server.</span></span> <span data-ttu-id="b88ce-158">SSL에 대 한 자세한 내용은 참조 하십시오. [응용 프로그램 toosecurely에서 SSL 구성 연결 MySQL 용 tooAzure 데이터베이스 연결](./howto-configure-ssl.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-158">For more information on SSL, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](./howto-configure-ssl.md).</span></span>  <span data-ttu-id="b88ce-159">SSL toodisable 해야 할 경우 hello Azure 포털을 방문 하 고 hello 연결 보안 페이지 toodisable hello 적용 SSL 연결 설정/해제 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-159">If you need toodisable SSL, visit hello Azure portal and click hello Connection security page toodisable hello Enforce SSL connection toggle button.</span></span>

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a><span data-ttu-id="b88ce-160">테이블 만들기, 데이터 삽입, 데이터 읽기, 데이터 업데이트, 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="b88ce-160">Create a table, insert data, read data, update data, delete data</span></span>
1. <span data-ttu-id="b88ce-161">데이터 복사 및 붙여넣기 hello 샘플 SQL 코드 빈 SQL 탭 tooillustrate에 몇 가지 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-161">Copy and paste hello sample SQL code into a blank SQL tab tooillustrate some sample data.</span></span>

    <span data-ttu-id="b88ce-162">이 코드는 quickstartdb라는 빈 데이터베이스를 만든 후 inventory라는 샘플 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-162">This code creates an empty database named quickstartdb, and then creates a sample table named inventory.</span></span> <span data-ttu-id="b88ce-163">몇 개의 행을 삽입 하는 다음 hello 행을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-163">It inserts some rows, then reads hello rows.</span></span> <span data-ttu-id="b88ce-164">Update 문과 함께 hello 데이터를 변경 하 고 읽기 안녕 행 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-164">It changes hello data with an update statement, and reads hello rows again.</span></span> <span data-ttu-id="b88ce-165">마지막으로 한 행을 삭제 하 고 hello 행을 다시 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-165">Finally it deletes a row, and reads hello rows again.</span></span>
    
    ```sql
    -- Create a database
    -- DROP DATABASE IF EXISTS quickstartdb;
    CREATE DATABASE quickstartdb;
    USE quickstartdb;
    
    -- Create a table and insert rows
    DROP TABLE IF EXISTS inventory;
    CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
    INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
    INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
    INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    
    -- Read
    SELECT * FROM inventory;
    
    -- Update
    UPDATE inventory SET quantity = 200 WHERE id = 1;
    SELECT * FROM inventory;
    
    -- Delete
    DELETE FROM inventory WHERE id = 2;
    SELECT * FROM inventory;
    ```

    <span data-ttu-id="b88ce-166">hello 스크린 샷 실행 된 후 SQL Workbench 및 hello 출력의 hello SQL 코드의 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-166">hello screenshot shows an example of hello SQL code in SQL Workbench and hello output after it has been run.</span></span>
    
    ![MySQL 워크 벤치 SQL 탭 toorun 샘플 SQL 코드](media/connect-workbench/3-workbench-sql-tab.png)

2. <span data-ttu-id="b88ce-168">toorun hello 샘플 SQL 코드의 hello hello 도구 모음에서 모양 아이콘 밝게 hello 클릭 **SQL 파일** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-168">toorun hello sample SQL Code, click hello lightening bolt icon in hello toolbar of hello **SQL File** tab.</span></span>
3. <span data-ttu-id="b88ce-169">Hello에 3 개의 탭된 결과 hello 확인 **결과 표** hello 가운데에 hello 페이지의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-169">Notice hello three tabbed results in hello **Result Grid** section in hello middle of hello page.</span></span> 
4. <span data-ttu-id="b88ce-170">공지 hello **출력** hello hello 페이지 맨 아래에 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-170">Notice hello **Output** list at hello bottom of hello page.</span></span> <span data-ttu-id="b88ce-171">그러면 각 명령의 hello 상태가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-171">hello status of each command is shown.</span></span> 

<span data-ttu-id="b88ce-172">이제 데이터베이스 tooAzure MySQL 워크 벤치를 사용 하 여 MySQL에 대 한 연결 하 고 hello SQL 언어를 사용 하 여 데이터를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ce-172">Now, you have connected tooAzure Database for MySQL using MySQL Workbench, and have queried data using hello SQL language.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b88ce-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b88ce-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b88ce-174">내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="b88ce-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
