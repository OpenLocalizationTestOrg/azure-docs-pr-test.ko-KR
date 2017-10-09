---
title: "aaaSecure Azure SQL 데이터베이스 | Microsoft Docs"
description: "Azure SQL 데이터베이스를 기술 및 기능 toosecure에 알아봅니다."
services: sql-database
documentationcenter: 
author: DRediske
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/28/2017
ms.author: daredis
ms.openlocfilehash: 1450d633d6f65faf1b8a2dc0dc7dfe996fb0719d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-azure-sql-database"></a><span data-ttu-id="2face-103">Azure SQL Database 보안</span><span class="sxs-lookup"><span data-stu-id="2face-103">Secure your Azure SQL Database</span></span>

<span data-ttu-id="2face-104">SQL 데이터베이스에서 방화벽 규칙, id 및 권한 부여 toodata 역할 기반 구성원 자격 및 권한을 통해 통해서도 사용자 tooprove 하도록 하는 인증 메커니즘을 사용 하 여 액세스 tooyour 데이터베이스를 제한 하 여 데이터를 보호 행 수준 보안 및 동적 데이터 마스킹입니다.</span><span class="sxs-lookup"><span data-stu-id="2face-104">SQL Database secures your data by limiting access tooyour database using firewall rules, authentication mechanisms requiring users tooprove their identity, and authorization toodata through role-based memberships and permissions, as well as through row-level security and dynamic data masking.</span></span>

<span data-ttu-id="2face-105">악의적인 사용자 또는 몇 가지 간단한 단계만 무단된 액세스 로부터 사용자 데이터베이스의 hello 보호를 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2face-105">You can improve hello protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="2face-106">이 자습서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2face-106">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="2face-107">Hello Azure 포털에서에서 해당 서버에 대 한 서버 수준 방화벽 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="2face-107">Set up server-level firewall rules for your server in hello Azure portal</span></span>
> * <span data-ttu-id="2face-108">SSMS를 사용하여 데이터베이스에 대해 데이터베이스 수준 방화벽 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="2face-108">Set up database-level firewall rules for your database using SSMS</span></span>
> * <span data-ttu-id="2face-109">Tooyour 데이터베이스 보안 연결 문자열을 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="2face-109">Connect tooyour database using a secure connection string</span></span>
> * <span data-ttu-id="2face-110">사용자 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="2face-110">Manage user access</span></span>
> * <span data-ttu-id="2face-111">암호화로 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="2face-111">Protect your data with encryption</span></span>
> * <span data-ttu-id="2face-112">SQL Database 감사 사용</span><span class="sxs-lookup"><span data-stu-id="2face-112">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="2face-113">SQL Database 위협 감지 사용</span><span class="sxs-lookup"><span data-stu-id="2face-113">Enable SQL Database threat detection</span></span>

<span data-ttu-id="2face-114">Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2face-114">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2face-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2face-115">Prerequisites</span></span>

<span data-ttu-id="2face-116">toocomplete이 자습서, 확인을 준비 해야 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="2face-116">toocomplete this tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="2face-117">최신 버전의 설치 된 hello [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="2face-117">Installed hello newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> 
- <span data-ttu-id="2face-118">Microsoft Excel</span><span class="sxs-lookup"><span data-stu-id="2face-118">Installed Microsoft Excel</span></span>
- <span data-ttu-id="2face-119">Azure SQL server 및 데이터베이스-만든 참조 [hello Azure 포털에서에서 Azure SQL 데이터베이스를 만들](sql-database-get-started-portal.md), [hello Azure CLI를 사용 하 여 단일 Azure SQL 데이터베이스 만들기](sql-database-get-started-cli.md), 및 [단일 Azure Sql PowerShell을 사용 하 여 데이터베이스](sql-database-get-started-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-119">Created an Azure SQL server and database - See [Create an Azure SQL database in hello Azure portal](sql-database-get-started-portal.md), [Create a single Azure SQL database using hello Azure CLI](sql-database-get-started-cli.md), and [Create a single Azure SQL database using PowerShell](sql-database-get-started-powershell.md).</span></span> 

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="2face-120">Azure 포털 toohello에 로그인</span><span class="sxs-lookup"><span data-stu-id="2face-120">Log in toohello Azure portal</span></span>

<span data-ttu-id="2face-121">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-121">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="2face-122">Hello Azure 포털에에서 서버 수준 방화벽 규칙을 만들려면</span><span class="sxs-lookup"><span data-stu-id="2face-122">Create a server-level firewall rule in hello Azure portal</span></span>

<span data-ttu-id="2face-123">Azure에서 SQL Database는 방화벽으로 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="2face-123">SQL databases are protected by a firewall in Azure.</span></span> <span data-ttu-id="2face-124">기본적으로 모든 연결 toohello 서버와 hello 데이터베이스 hello 서버 내부에서 다른 Azure 서비스의 연결을 제외 하 고 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2face-124">By default, all connections toohello server and hello databases inside hello server are rejected except for connections from other Azure services.</span></span> <span data-ttu-id="2face-125">자세한 내용은 [Azure SQL Database 서버 수준 및 데이터베이스 수준 방화벽 규칙 구성](sql-database-firewall-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2face-125">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="2face-126">hello 가장 안전한 구성은 tooset 대 한 액세스 허용 tooAzure 서비스' tooOFF 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-126">hello most secure configuration is tooset 'Allow access tooAzure services' tooOFF.</span></span> <span data-ttu-id="2face-127">Azure VM 또는 클라우드 서비스에서 tooconnect toohello 데이터베이스를 두어야 하는 경우 만든는 [예약 된 IP](../virtual-network/virtual-networks-reserved-public-ip.md) hello 예약 된 IP 주소 액세스만 허용 hello 방화벽을 통해 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-127">If you need tooconnect toohello database from an Azure VM or cloud service, you should create a [Reserved IP](../virtual-network/virtual-networks-reserved-public-ip.md) and allow only hello reserved IP address access through hello firewall.</span></span> 

<span data-ttu-id="2face-128">이러한 단계 toocreate에 따라 한 [SQL 데이터베이스 서버 수준 방화벽 규칙](sql-database-firewall-configure.md) 특정 IP 주소에서 서버 tooallow 연결용입니다.</span><span class="sxs-lookup"><span data-stu-id="2face-128">Follow these steps toocreate a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your server tooallow connections from a specific IP address.</span></span> 

> [!NOTE]
> <span data-ttu-id="2face-129">이전 자습서 hello 또는 퀵 스타트 되며 중 하나를 사용 하 여 Azure에서 예제 데이터베이스를 만든 경우 hello가 있는 컴퓨터에서이 자습서를 수행 합니다. 동일한 IP 주소를 이러한 자습서를 통해 진행할 때 이전를 건너뛸 수 있습니다이 단계는 것 이미 서버 수준 방화벽 규칙을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="2face-129">If you have created a sample database in Azure using one of hello previous tutorials or quickstarts and are performing this tutorial on a computer with hello same IP address that it had when you walked through those tutorials, you can skip this step as you will have already created a server-level firewall rule.</span></span>
>

1. <span data-ttu-id="2face-130">클릭 **SQL 데이터베이스** hello 왼쪽 메뉴 hello 데이터베이스에서 원하는 hello에서 tooconfigure hello 방화벽 규칙에 대 한 **SQL 데이터베이스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="2face-130">Click **SQL databases** from hello left-hand menu and click hello database you would like tooconfigure hello firewall rule for on hello **SQL databases** page.</span></span> <span data-ttu-id="2face-131">hello 완벽 하 게 hello 보여 주는 데이터베이스 열리면 프로그램에 대 한 개요 페이지에 정규화 된 서버 이름 (같은 **mynewserver 20170313.database.windows.net**) 하 고 더 이상의 구성에 대 한 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-131">hello overview page for your database opens, showing you hello fully qualified server name (such as **mynewserver-20170313.database.windows.net**) and provides options for further configuration.</span></span>

      ![서버 방화벽 규칙](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. <span data-ttu-id="2face-133">클릭 **서버 방화벽 설정** hello 이전 그림에 나와 있는 것 처럼 hello 도구 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="2face-133">Click **Set server firewall** on hello toolbar as shown in hello previous image.</span></span> <span data-ttu-id="2face-134">hello **방화벽 설정** hello SQL 데이터베이스 서버에 대 한 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="2face-134">hello **Firewall settings** page for hello SQL Database server opens.</span></span> 

3. <span data-ttu-id="2face-135">클릭 **클라이언트 IP 추가** 에 hello와 hello 컴퓨터 연결 된 toohello 포털의 도구 모음 tooadd hello 공용 IP 주소 또는 hello 방화벽 규칙을 수동으로 입력 한 다음 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-135">Click **Add client IP** on hello toolbar tooadd hello public IP address of hello computer connected toohello portal with or enter hello firewall rule manually and then click **Save**.</span></span>

      ![set server firewall rule](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. <span data-ttu-id="2face-137">클릭 **확인** hello를 클릭 한 다음 **X** tooclose hello **방화벽 설정** 페이지.</span><span class="sxs-lookup"><span data-stu-id="2face-137">Click **OK** and then click hello **X** tooclose hello **Firewall settings** page.</span></span>

<span data-ttu-id="2face-138">지정 된 hello로 tooany 데이터베이스 hello 서버에 연결할 수 있습니다 IP 주소 또는 IP 주소 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="2face-138">You can now connect tooany database in hello server with hello specified IP address or IP address range.</span></span>

> [!NOTE]
> <span data-ttu-id="2face-139">SQL Database는 포트 1433을 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-139">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="2face-140">회사 네트워크 내부에서 tooconnect을 시도 하는 포트 1433 통한 아웃 바운드 트래픽 네트워크의 방화벽에서 허용 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2face-140">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="2face-141">이 경우 됩니다 수 tooconnect tooyour Azure SQL 데이터베이스 서버 않으면 IT 부서는 포트 1433을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2face-141">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a><span data-ttu-id="2face-142">SSMS를 사용하여 데이터베이스 수준 방화벽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="2face-142">Create a database-level firewall rule using SSMS</span></span>

<span data-ttu-id="2face-143">데이터베이스 수준 방화벽 규칙을 사용 하는 휴대용-hello 중에 데이터베이스를 따른다는 동일한 논리 서버 및 toocreate 방화벽 규칙 hello 내에서 서로 다른 데이터베이스에 대 한 toocreate 다른 방화벽 설정을 하면는 [장애 조치 ](sql-database-geo-replication-overview.md) hello SQL server에 저장 되지 않고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2face-143">Database-level firewall rules enable you toocreate different firewall settings for different databases within hello same logical server and toocreate firewall rules that are portable - meaning that they follow hello database during a [failover](sql-database-geo-replication-overview.md) rather than being stored on hello SQL server.</span></span> <span data-ttu-id="2face-144">데이터베이스 수준 방화벽 규칙 hello 첫 번째 서버 수준 방화벽 규칙을 구성 하면 TRANSACT-SQL 문을 사용 하 여 구성 되 고 유일한을 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2face-144">Database-level firewall rules can only be configured by using Transact-SQL statements and only after you have configured hello first server-level firewall rule.</span></span> <span data-ttu-id="2face-145">자세한 내용은 [Azure SQL Database 서버 수준 및 데이터베이스 수준 방화벽 규칙 구성](sql-database-firewall-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2face-145">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="2face-146">이러한 단계 toocreate 데이터베이스 관련 방화벽 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2face-146">Follows these steps toocreate a database-specific firewall rule.</span></span>

1. <span data-ttu-id="2face-147">예를 사용 하 여 tooyour 데이터베이스 연결 [SQL Server Management Studio](./sql-database-connect-query-ssms.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-147">Connect tooyour database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span></span>

2. <span data-ttu-id="2face-148">개체 탐색기에서 마우스 오른쪽 단추로 클릭 tooadd 방화벽에 대 한 규칙을 클릭 하 여 hello 데이터베이스 **새 쿼리**합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-148">In Object Explorer, right-click on hello database you want tooadd a firewall rule for and click **New Query**.</span></span> <span data-ttu-id="2face-149">빈 쿼리 창이 열립니다 tooyour 연결 된 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="2face-149">A blank query window opens that is connected tooyour database.</span></span>

3. <span data-ttu-id="2face-150">Hello 쿼리 창에서 hello IP 주소 tooyour 공용 IP 주소를 수정 하 고 hello 다음 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-150">In hello query window, modify hello IP address tooyour public IP address and then execute hello following query:</span></span>

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. <span data-ttu-id="2face-151">Hello 도구 모음에서 **Execute** toocreate hello 방화벽 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="2face-151">On hello toolbar, click **Execute** toocreate hello firewall rule.</span></span>

## <a name="view-how-tooconnect-an-application-tooyour-database-using-a-secure-connection-string"></a><span data-ttu-id="2face-152">응용 프로그램 tooyour tooconnect 데이터베이스 보안 연결 문자열을 사용 하는 방법 보기</span><span class="sxs-lookup"><span data-stu-id="2face-152">View how tooconnect an application tooyour database using a secure connection string</span></span>

<span data-ttu-id="2face-153">클라이언트 응용 프로그램과 SQL 데이터베이스 간에 암호화 된 보안 연결 tooensure hello 연결 문자열에 toobe 하도록 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-153">tooensure a secure, encrypted connection between a client application and SQL Database, hello connection string has toobe configured to:</span></span>

- <span data-ttu-id="2face-154">암호화된 연결을 요청하고</span><span class="sxs-lookup"><span data-stu-id="2face-154">Request an encrypted connection, and</span></span>
- <span data-ttu-id="2face-155">toonot hello 서버 인증서를 신뢰 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-155">toonot trust hello server certificate.</span></span> 

<span data-ttu-id="2face-156">이 보안 TLS (전송 계층)를 사용 하 여 연결을 설정 하 고 hello의 중간자 개입 공격 위험 감소 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-156">This establishes a connection using Transport Layer Security (TLS) and reduces hello risk of man-in-the-middle attacks.</span></span> <span data-ttu-id="2face-157">가져올 수 있습니다 올바르게 구성 된 연결 문자열 지원 되는 클라이언트에 대 한 SQL 데이터베이스에 대 한 드라이버 hello Azure 포털에서에서 ADO.net에 대 한이 스크린 샷에 표시 된 것 처럼.</span><span class="sxs-lookup"><span data-stu-id="2face-157">You can obtain correctly configured connection strings for your SQL Database for supported client drivers from hello Azure portal as shown for ADO.net in this screenshot.</span></span>

1. <span data-ttu-id="2face-158">선택 **SQL 데이터베이스** hello 왼쪽 메뉴에서 hello에 데이터베이스를 클릭 하 고 **SQL 데이터베이스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="2face-158">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span>

2. <span data-ttu-id="2face-159">Hello에 **개요** 데이터베이스 페이지에서 클릭 **데이터베이스 연결 문자열 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-159">On hello **Overview** page for your database, click **Show database connection strings**.</span></span>

3. <span data-ttu-id="2face-160">전체 검토 hello **ADO.NET** 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="2face-160">Review hello complete **ADO.NET** connection string.</span></span>

    ![ADO.NET 연결 문자열](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a><span data-ttu-id="2face-162">데이터베이스 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2face-162">Creating database users</span></span>

<span data-ttu-id="2face-163">사용자를 만들기 전에 먼저 Azure SQL Database가 지원하는 두 가지 인증 유형 중 하나를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-163">Before creating any users, you must first choose from one of two authentication types supported by Azure SQL Database:</span></span> 

<span data-ttu-id="2face-164">**SQL 인증**, 로그인에 대 한 사용자 이름 및 암호를 사용 하 및 유효한에 있는 사용자는 논리 서버 내에서 특정 데이터베이스의 컨텍스트에서 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-164">**SQL Authentication**, which uses username and password for logins and users that are valid only in hello context of a specific database within a logical server.</span></span> 

<span data-ttu-id="2face-165">**Azure Active Directory 인증**은 Azure Active Directory에서 관리되는 ID를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-165">**Azure Active Directory Authentication**, which uses identities managed by Azure Active Directory.</span></span> 

<span data-ttu-id="2face-166">Toouse 하려는 경우 [Azure Active Directory](./sql-database-aad-authentication.md) SQL 데이터베이스에 대해 tooauthenticate, 지정된 된 Azure Active Directory를 계속 하려면 먼저 존재 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-166">If you want toouse [Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate against SQL Database, a populated Azure Active Directory must exist before you can proceed.</span></span>

<span data-ttu-id="2face-167">이러한 단계 toocreate SQL 인증을 사용 하 여 사용자를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-167">Follow these steps toocreate a user using SQL Authentication:</span></span>

1. <span data-ttu-id="2face-168">예를 사용 하 여 tooyour 데이터베이스 연결 [SQL Server Management Studio](./sql-database-connect-query-ssms.md) 서버 관리자 자격 증명을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-168">Connect tooyour database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) using your server admin credentials.</span></span>

2. <span data-ttu-id="2face-169">개체 탐색기에서 마우스 오른쪽 단추로 클릭 hello 데이터베이스에서 새 사용자 tooadd 원하는 하 고 클릭 **새 쿼리**합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-169">In Object Explorer, right-click on hello database you want tooadd a new user on and click **New Query**.</span></span> <span data-ttu-id="2face-170">빈 쿼리 창이 열립니다 연결 된 toohello 선택한 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="2face-170">A blank query window opens that is connected toohello selected database.</span></span>

3. <span data-ttu-id="2face-171">Hello 쿼리 창에서 다음 쿼리는 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-171">In hello query window, enter hello following query:</span></span>

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. <span data-ttu-id="2face-172">Hello 도구 모음에서 **Execute** toocreate hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="2face-172">On hello toolbar, click **Execute** toocreate hello user.</span></span>

5. <span data-ttu-id="2face-173">기본적으로 hello 사용자 toohello 데이터베이스를 연결할 수 있지만 사용 권한을 tooread 또는 쓰기 데이터가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2face-173">By default, hello user can connect toohello database, but has no permissions tooread or write data.</span></span> <span data-ttu-id="2face-174">toogrant 이러한 사용 권한을 toohello 새로 만든 사용자, 새 쿼리 창에서 두 명령의 다음 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-174">toogrant these permissions toohello newly created user, execute hello following two commands in a new query window</span></span>

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

<span data-ttu-id="2face-175">것이 모범 사례 toocreate hello 데이터베이스 수준 tooconnect tooyour에서 이러한 관리자가 아닌 계정 데이터베이스 tooexecute 관리자 작업 같은 새 사용자를 만드는 경우를 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-175">It is best practice toocreate these non-administrator accounts at hello database level tooconnect tooyour database unless you need tooexecute administrator tasks like creating new users.</span></span> <span data-ttu-id="2face-176">Hello를 검토 하십시오 [Azure Active Directory 자습서](./sql-database-aad-authentication-configure.md) 방법에 Azure Active Directory를 사용 하 여 tooauthenticate 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-176">Please review hello [Azure Active Directory tutorial](./sql-database-aad-authentication-configure.md) on how tooauthenticate using Azure Active Directory.</span></span>


## <a name="protect-your-data-with-encryption"></a><span data-ttu-id="2face-177">암호화로 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="2face-177">Protect your data with encryption</span></span>

<span data-ttu-id="2face-178">Azure SQL 데이터베이스 투명 한 데이터 암호화 (TDE)는 자동으로 모든 변경 내용을 toohello 응용 프로그램에 액세스 hello 암호화 된 데이터베이스를 요구 하지 않고을 미사용 데이터를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-178">Azure SQL Database transparent data encryption (TDE) automatically encrypts your data at rest, without requiring any changes toohello application accessing hello encrypted database.</span></span> <span data-ttu-id="2face-179">새로 만든 데이터베이스의 경우 TDE는 기본적으로 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2face-179">For newly created databases, TDE is on by default.</span></span> <span data-ttu-id="2face-180">TDE가 켜져 있는 tooverify 또는 데이터베이스에 대 한 TDE tooenable 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="2face-180">tooenable TDE for your database or tooverify that TDE is on, follow these steps:</span></span>

1. <span data-ttu-id="2face-181">선택 **SQL 데이터베이스** hello 왼쪽 메뉴에서 hello에 데이터베이스를 클릭 하 고 **SQL 데이터베이스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="2face-181">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 

2. <span data-ttu-id="2face-182">클릭 **투명 한 데이터 암호화** TDE에 대 한 tooopen hello 구성 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="2face-182">Click on **Transparent data encryption** tooopen hello configuration page for TDE.</span></span>

    ![투명한 데이터 암호화](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. <span data-ttu-id="2face-184">필요한 경우 설정 **데이터 암호화** tooON 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-184">If necessary, set **Data encryption** tooON and click **Save**.</span></span>

<span data-ttu-id="2face-185">hello 암호화 프로세스가 hello 백그라운드에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2face-185">hello encryption process starts in hello background.</span></span> <span data-ttu-id="2face-186">연결 tooSQL 데이터베이스를 사용 하 여 hello 진행률을 모니터링할 수 [SQL Server Management Studio](./sql-database-connect-query-ssms.md) hello의 hello encryption_state 열을 쿼리하여 `sys.dm_database_encryption_keys` 보기.</span><span class="sxs-lookup"><span data-stu-id="2face-186">You can monitor hello progress by connecting tooSQL Database using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) by querying hello encryption_state column of hello `sys.dm_database_encryption_keys` view.</span></span>

## <a name="enable-sql-database-auditing-if-necessary"></a><span data-ttu-id="2face-187">필요한 경우 SQL Database 감사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-187">Enable SQL Database auditing, if necessary</span></span>

<span data-ttu-id="2face-188">Azure SQL 데이터베이스 감사 데이터베이스 이벤트를 추적 하 고 Azure 저장소 계정에 tooan 감사 로그를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-188">Azure SQL Database Auditing tracks database events and writes them tooan audit log in your Azure Storage account.</span></span> <span data-ttu-id="2face-189">감사는 규정 준수를 유지 관리하고, 데이터베이스 작업을 이해하고, 잠재적인 보안 위반을 나타낼 수 있는 불일치 및 이상 활동을 파악하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2face-189">Auditing can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate potential security violations.</span></span> <span data-ttu-id="2face-190">이러한 단계 toocreate SQL 데이터베이스에 대 한 기본 감사 정책을 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="2face-190">Follow these steps toocreate a default auditing policy for your SQL database:</span></span>

1. <span data-ttu-id="2face-191">선택 **SQL 데이터베이스** hello 왼쪽 메뉴에서 hello에 데이터베이스를 클릭 하 고 **SQL 데이터베이스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="2face-191">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 

2. <span data-ttu-id="2face-192">Hello 설정 블레이드에서 선택 **감사 및 위협 요소 탐지**합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-192">In hello Settings blade, select **Auditing & Threat Detection**.</span></span> <span data-ttu-id="2face-193">서버 수준 감사 없게 임을 있고 있다는 **서버 설정을 보려면** 링크 tooview를 허용 하 고이 컨텍스트에서 hello 서버 감사 설정을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-193">Notice that sever-level auditing is diabled and that there is a **View server settings** link that allows you tooview or modify hello server auditing settings from this context.</span></span>

    ![감사 블레이드](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. <span data-ttu-id="2face-195">Tooenable는 감사 형식 (또는 위치?)를 선호 하는 경우 hello 서버 수준에서 지정 된 hello와에서 다른 설정 **ON** 감사 hello 선택 **Blob** 감사 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2face-195">If you prefer tooenable an Audit type (or location?) different from hello one specified at hello server level, turn **ON** Auditing, and choose hello **Blob** Auditing Type.</span></span> <span data-ttu-id="2face-196">서버 Blob 감사를 사용 하는 경우 hello 구성 된 데이터베이스 감사 hello 서버 Blob 감사와 함께 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-196">If server Blob auditing is enabled, hello database configured audit will exist side by side with hello server Blob audit.</span></span>

    ![감사 설정](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. <span data-ttu-id="2face-198">선택 **저장소 세부 정보** tooopen hello 감사 로그 저장소 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="2face-198">Select **Storage Details** tooopen hello Audit Logs Storage Blade.</span></span> <span data-ttu-id="2face-199">로그를 저장할 선택 hello Azure 저장소 계정 및 hello 보존 기간을 어떤 hello 이전 로그 삭제 후, 클릭 **확인** hello 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2face-199">Select hello Azure storage account where logs will be saved, and hello retention period, after which hello old logs will be deleted, then click **OK** at hello bottom.</span></span> 

   > [!TIP]
   > <span data-ttu-id="2face-200">사용 하 여 hello 동일 hello 감사를 최대한 활용 하는 모든 감사 데이터베이스 tooget hello에 대 한 저장소 계정을 서식 파일을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-200">Use hello same storage account for all audited databases tooget hello most out of hello auditing reports templates.</span></span>
   > 

5. <span data-ttu-id="2face-201">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-201">Click **Save**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2face-202">Toocustomize hello 감사 이벤트를 하려는 경우 이렇게 하려면 PowerShell 또는 REST API 액세스를 통해 참조 hello [자동화 (PowerShell / REST API)](sql-database-auditing.md#subheading-7) 자세한 내용은 섹션.</span><span class="sxs-lookup"><span data-stu-id="2face-202">If you want toocustomize hello audited events, you can do this via PowerShell or REST API - see hello [Automation (PowerShell / REST API)](sql-database-auditing.md#subheading-7) section for more details.</span></span>
>

## <a name="enable-sql-database-threat-detection"></a><span data-ttu-id="2face-203">SQL Database 위협 감지 사용</span><span class="sxs-lookup"><span data-stu-id="2face-203">Enable SQL Database threat detection</span></span>

<span data-ttu-id="2face-204">위협 요소 탐지 새 고객 toodetect 있고 비정상적인 활동에서 보안 경고를 제공 하 여 발생 하는 대로 toopotential 위협 응답을 보안 계층을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-204">Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="2face-205">사용자는 시도 tooaccess, 위반에서에서 발생 하거나 hello 데이터베이스의에서 데이터를 이용할 경우 toodetermine SQL 데이터베이스 감사를 사용 하 여 hello 의심 스러운 이벤트를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2face-205">Users can explore hello suspicious events using SQL Database Auditing toodetermine if they result from an attempt tooaccess, breach or exploit data in hello database.</span></span> <span data-ttu-id="2face-206">위협 요소 탐지 하면 간단한 tooaddress 잠재적인 위협 toohello 데이터베이스 없이 hello 필요 toobe 보안 전문가 또는 시스템 모니터링 하는 고급 보안을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-206">Threat Detection makes it simple tooaddress potential threats toohello database without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>
<span data-ttu-id="2face-207">예를 들어 위협 감지는 잠재적인 SQL 삽입 시도를 나타내는 비정상적인 데이터베이스 활동을 감지합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-207">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="2face-208">SQL 주입 hello 일반적인 웹 응용 프로그램 보안 문제에 hello 인터넷을 사용 하는 tooattack 데이터 기반 응용 프로그램 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="2face-208">SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="2face-209">공격자가 활용 응용 프로그램 취약점 tooinject 악의적인 SQL 문을 졌는 지 또는 hello 데이터베이스의 데이터 수정에 대 한 응용 프로그램 입력 필드에 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-209">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, for breaching or modifying data in hello database.</span></span>

1. <span data-ttu-id="2face-210">Hello toomonitor 사용할 SQL 데이터베이스의 구성 블레이드에서 toohello 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-210">Navigate toohello configuration blade of hello SQL database you want toomonitor.</span></span> <span data-ttu-id="2face-211">Hello 설정 블레이드에서 선택 **감사 및 위협 요소 탐지**합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-211">In hello Settings blade, select **Auditing & Threat Detection**.</span></span>

    ![탐색 창](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. <span data-ttu-id="2face-213">Hello에 **감사 및 위협 요소 탐지** 구성 블레이드 turn **ON** 감사를 위해 표시 하는 hello 위협 검색 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-213">In hello **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display hello threat detection settings.</span></span>

3. <span data-ttu-id="2face-214">위협 감지를 **켭니다**.</span><span class="sxs-lookup"><span data-stu-id="2face-214">Turn **ON** threat detection.</span></span>

4. <span data-ttu-id="2face-215">검색 비정상 데이터베이스 작업에 대해 보안 경고를 받을 전자 메일의 hello 목록을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-215">Configure hello list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>

5. <span data-ttu-id="2face-216">클릭 **저장** hello에 **감사 및 위협 검색** 블레이드 toosave hello 신규 또는 업데이트 된 감사 및 위협 검색 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="2face-216">Click **Save** in hello **Auditing & Threat detection** blade toosave hello new or updated auditing and threat detection policy.</span></span>

    ![탐색 창](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    <span data-ttu-id="2face-218">비정상적인 데이터베이스 활동이 감지되면 이에 대한 이메일 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2face-218">If anomalous database activities are detected, you will receive an email notification upon detection of anomalous database activities.</span></span> <span data-ttu-id="2face-219">hello 전자 메일 hello 비정상적인 활동, 데이터베이스 이름, 서버 이름 및 hello 이벤트 시간의 hello 특성을 포함 하 여 hello 의심 되는 보안 이벤트를 처리 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-219">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name and hello event time.</span></span> <span data-ttu-id="2face-220">또한, 가능한 원인에 정보를 제공 합니다 및 작업 tooinvestigate 권장 하 고 hello 잠재적인 위협 toohello 데이터베이스 완화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-220">In addition, it will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span> <span data-ttu-id="2face-221">이러한 메일 수신 하는 hello 어떤 toodo를 통해 수행 해야 하는 다음 단계 워크:</span><span class="sxs-lookup"><span data-stu-id="2face-221">hello next steps walk you through what toodo should you receive such an email:</span></span>

    ![위협 감지 전자 메일](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. <span data-ttu-id="2face-223">Hello 전자 메일의 hello에서 클릭 **Azure SQL 감사 로그** 링크를 hello Azure 포털을 시작 하 고 hello 의심 스러운 이벤트의 hello 시간대 hello 관련 된 감사 레코드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2face-223">In hello email, click on hello **Azure SQL Auditing Log** link, which will launch hello Azure portal and show hello relevant auditing records around hello time of hello suspicious event.</span></span>

    ![감사 레코드](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. <span data-ttu-id="2face-225">SQL 문 처럼 hello 데이터베이스 의심 스러운 활동에 대 한 자세한 내용은 hello 감사 레코드 tooview 클릭 실패 이유 및 클라이언트 IP입니다.</span><span class="sxs-lookup"><span data-stu-id="2face-225">Click on hello audit records tooview more details on hello suspicious database activities such as SQL statement, failure reason and client IP.</span></span>

    ![레코드 세부 정보](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. <span data-ttu-id="2face-227">Hello 감사 레코드 블레이드에서 클릭 **Excel에서 열기** tooopen 미리 구성 된 excel 서식 파일 tooimport 및 hello 의심 스러운 이벤트의 hello 시간대 hello 감사 로그의 심층 분석을 실행된 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-227">In hello Auditing Records blade, click  **Open in Excel** tooopen a pre-configured excel template tooimport and run deeper analysis of hello audit log around hello time of hello suspicious event.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2face-228">Excel 2010 또는 나중에 파워 쿼리 및 hello **빠른 결합** 설정은 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="2face-228">In Excel 2010 or later, Power Query and hello **Fast Combine** setting is required.</span></span>

    ![Excel에서 레코드 열기](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. <span data-ttu-id="2face-230">tooconfigure hello **빠른 결합** hello에 설정- **파워 쿼리** 리본 탭 **옵션** toodisplay hello 옵션 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="2face-230">tooconfigure hello **Fast Combine** setting - In hello **POWER QUERY** ribbon tab, select **Options** toodisplay hello Options dialog.</span></span> <span data-ttu-id="2face-231">Hello 개인 정보 섹션을 선택 하 고 hello 두 번째 옵션-'hello 개인 정보 수준을 무시 하 고 잠재적으로 성능 향상'를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-231">Select hello Privacy section and choose hello second option - 'Ignore hello Privacy Levels and potentially improve performance':</span></span>

    ![Excel 빠른 결합](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. <span data-ttu-id="2face-233">tooload SQL 감사 로그 hello 매개 변수가 확인 hello 설정 탭에서 올바르게 설정 하 고 다음 hello '데이터' 리본 선택 hello ' 모두 새로 고침 ' 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2face-233">tooload SQL audit logs, ensure that hello parameters in hello settings tab are set correctly and then select hello 'Data' ribbon and click hello 'Refresh All' button.</span></span>

    ![Excel 매개 변수](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. <span data-ttu-id="2face-235">hello에 hello 결과가 표시 **SQL 감사 로그** 시트 발견 되 고 응용 프로그램에서 hello 보안 이벤트의 hello 영향을 완화 하는 hello 비정상적인 활동의 심층 분석 toorun 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2face-235">hello results appear in hello **SQL Audit Logs** sheet which enables you toorun deeper analysis of hello anomalous activities that were detected, and mitigate hello impact of hello security event in your application.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2face-236">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2face-236">Next steps</span></span>
<span data-ttu-id="2face-237">악의적인 사용자 또는 몇 가지 간단한 단계만 무단된 액세스 로부터 사용자 데이터베이스의 hello 보호를 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2face-237">You can improve hello protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="2face-238">이 자습서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2face-238">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="2face-239">서버 및 데이터베이스에 대한 방화벽 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="2face-239">Set up firewall rules for your sever and or database</span></span>
> * <span data-ttu-id="2face-240">Tooyour 데이터베이스 보안 연결 문자열을 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="2face-240">Connect tooyour database using a secure connection string</span></span>
> * <span data-ttu-id="2face-241">사용자 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="2face-241">Manage user access</span></span>
> * <span data-ttu-id="2face-242">암호화로 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="2face-242">Protect your data with encryption</span></span>
> * <span data-ttu-id="2face-243">SQL Database 감사 사용</span><span class="sxs-lookup"><span data-stu-id="2face-243">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="2face-244">SQL Database 위협 감지 사용</span><span class="sxs-lookup"><span data-stu-id="2face-244">Enable SQL Database threat detection</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="2face-245">SQL Database 성능 향상</span><span class="sxs-lookup"><span data-stu-id="2face-245">Improve SQL Database performance</span></span>](sql-database-performance-tutorial.md)

