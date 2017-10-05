---
title: "Azure SQL Database 보안 | Microsoft Docs"
description: "Azure SQL Database 보안 기술 및 기능에 대해 자세히 알아봅니다."
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
ms.openlocfilehash: 4bc09ad13ed0c9dc9257e9c75ec6f9ff3d689a0b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="secure-your-azure-sql-database"></a><span data-ttu-id="5c263-103">Azure SQL Database 보안</span><span class="sxs-lookup"><span data-stu-id="5c263-103">Secure your Azure SQL Database</span></span>

<span data-ttu-id="5c263-104">SQL Database는 방화벽 규칙, 사용자에게 ID 확인을 요구하는 인증 메커니즘 및 역할 기반 멤버 자격과 권한을 통한 데이터 인증을 사용하여 데이터베이스에 대한 액세스를 제한할 뿐만 아니라 행 수준 보안과 동적 데이터 마스킹을 사용하여 데이터베이스에 대한 액세스도 제한함으로써 데이터를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-104">SQL Database secures your data by limiting access to your database using firewall rules, authentication mechanisms requiring users to prove their identity, and authorization to data through role-based memberships and permissions, as well as through row-level security and dynamic data masking.</span></span>

<span data-ttu-id="5c263-105">몇 가지 간단한 단계만 거치면 악의적인 사용자 또는 무단 액세스로부터 데이터베이스를 보호하는 기능을 크게 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-105">You can improve the protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="5c263-106">이 자습서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-106">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="5c263-107">Azure Portal의 서버에 대해 서버 수준 방화벽 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="5c263-107">Set up server-level firewall rules for your server in the Azure portal</span></span>
> * <span data-ttu-id="5c263-108">SSMS를 사용하여 데이터베이스에 대해 데이터베이스 수준 방화벽 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="5c263-108">Set up database-level firewall rules for your database using SSMS</span></span>
> * <span data-ttu-id="5c263-109">보안 연결 문자열을 사용하여 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="5c263-109">Connect to your database using a secure connection string</span></span>
> * <span data-ttu-id="5c263-110">사용자 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="5c263-110">Manage user access</span></span>
> * <span data-ttu-id="5c263-111">암호화로 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="5c263-111">Protect your data with encryption</span></span>
> * <span data-ttu-id="5c263-112">SQL Database 감사 사용</span><span class="sxs-lookup"><span data-stu-id="5c263-112">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="5c263-113">SQL Database 위협 감지 사용</span><span class="sxs-lookup"><span data-stu-id="5c263-113">Enable SQL Database threat detection</span></span>

<span data-ttu-id="5c263-114">Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-114">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c263-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5c263-115">Prerequisites</span></span>

<span data-ttu-id="5c263-116">이 자습서를 완료하려면 다음 항목이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-116">To complete this tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="5c263-117">SSMS([SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms))의 최신 버전</span><span class="sxs-lookup"><span data-stu-id="5c263-117">Installed the newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> 
- <span data-ttu-id="5c263-118">Microsoft Excel</span><span class="sxs-lookup"><span data-stu-id="5c263-118">Installed Microsoft Excel</span></span>
- <span data-ttu-id="5c263-119">Azure SQL Server 및 Database - [Azure Portal에서 Azure SQL Database 만들기](sql-database-get-started-portal.md), [Azure CLI를 사용하여 단일 Azure SQL Database 만들기](sql-database-get-started-cli.md) 및 [PowerShell을 사용하여 단일 Azure SQL Database 만들기](sql-database-get-started-powershell.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c263-119">Created an Azure SQL server and database - See [Create an Azure SQL database in the Azure portal](sql-database-get-started-portal.md), [Create a single Azure SQL database using the Azure CLI](sql-database-get-started-cli.md), and [Create a single Azure SQL database using PowerShell](sql-database-get-started-powershell.md).</span></span> 

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="5c263-120">Azure 포털에 로그인</span><span class="sxs-lookup"><span data-stu-id="5c263-120">Log in to the Azure portal</span></span>

<span data-ttu-id="5c263-121">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-121">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="5c263-122">Azure Portal에서 서버 수준 방화벽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="5c263-122">Create a server-level firewall rule in the Azure portal</span></span>

<span data-ttu-id="5c263-123">Azure에서 SQL Database는 방화벽으로 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-123">SQL databases are protected by a firewall in Azure.</span></span> <span data-ttu-id="5c263-124">기본적으로 다른 Azure 서비스의 연결을 제외하고 서버와 서버 내부의 데이터베이스에 대한 모든 연결은 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-124">By default, all connections to the server and the databases inside the server are rejected except for connections from other Azure services.</span></span> <span data-ttu-id="5c263-125">자세한 내용은 [Azure SQL Database 서버 수준 및 데이터베이스 수준 방화벽 규칙 구성](sql-database-firewall-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c263-125">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="5c263-126">가장 안전한 구성은 ‘Azure 서비스에 대한 액세스 허용’을 [끄기]로 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-126">The most secure configuration is to set 'Allow access to Azure services' to OFF.</span></span> <span data-ttu-id="5c263-127">Azure VM 또는 클라우드 서비스에서 데이터베이스에 연결해야 하는 경우 [예약된 IP](../virtual-network/virtual-networks-reserved-public-ip.md)를 만들고 방화벽을 통해 예약된 IP 주소 액세스만 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-127">If you need to connect to the database from an Azure VM or cloud service, you should create a [Reserved IP](../virtual-network/virtual-networks-reserved-public-ip.md) and allow only the reserved IP address access through the firewall.</span></span> 

<span data-ttu-id="5c263-128">특정 IP 주소에서 연결을 허용하도록 서버에 대한 [SQL Database 서버 수준 방화벽 규칙](sql-database-firewall-configure.md)을 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-128">Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your server to allow connections from a specific IP address.</span></span> 

> [!NOTE]
> <span data-ttu-id="5c263-129">Azure에서 이전 자습서 또는 빠른 시작 중 하나를 사용하여 샘플 데이터베이스를 만들고 해당 자습서를 통해 진행할 때 사용한 동일한 IP 주소를 가진 컴퓨터에서 이 자습서를 수행하는 경우 서버 수준 방화벽 규칙을 이미 만들었다면 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-129">If you have created a sample database in Azure using one of the previous tutorials or quickstarts and are performing this tutorial on a computer with the same IP address that it had when you walked through those tutorials, you can skip this step as you will have already created a server-level firewall rule.</span></span>
>

1. <span data-ttu-id="5c263-130">왼쪽 메뉴에서 **SQL Database**를 클릭하고 **SQL Database** 페이지에서 방화벽 규칙을 구성할 데이터베이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-130">Click **SQL databases** from the left-hand menu and click the database you would like to configure the firewall rule for on the **SQL databases** page.</span></span> <span data-ttu-id="5c263-131">데이터베이스에 대한 개요 페이지가 열리고 이 페이지에 정규화된 서버 이름(예: **mynewserver-20170313.database.windows.net**)이 표시되며 추가 구성을 위한 옵션도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-131">The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver-20170313.database.windows.net**) and provides options for further configuration.</span></span>

      ![서버 방화벽 규칙](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. <span data-ttu-id="5c263-133">이전 이미지에 표시된 대로 도구 모음에서 **서버 방화벽 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-133">Click **Set server firewall** on the toolbar as shown in the previous image.</span></span> <span data-ttu-id="5c263-134">SQL Database 서버에 대한 **방화벽 설정** 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-134">The **Firewall settings** page for the SQL Database server opens.</span></span> 

3. <span data-ttu-id="5c263-135">도구 모음에서 **클라이언트 IP 추가**를 클릭하여 포털에 연결된 컴퓨터의 공용 IP 주소를 추가하거나 수동으로 방화벽 규칙을 입력한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-135">Click **Add client IP** on the toolbar to add the public IP address of the computer connected to the portal with or enter the firewall rule manually and then click **Save**.</span></span>

      ![set server firewall rule](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. <span data-ttu-id="5c263-137">**확인**을 클릭한 후 **X**를 클릭하여 **방화벽 설정** 페이지를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-137">Click **OK** and then click the **X** to close the **Firewall settings** page.</span></span>

<span data-ttu-id="5c263-138">이제 지정된 IP 주소 또는 IP 주소 범위로 서버의 모든 데이터베이스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-138">You can now connect to any database in the server with the specified IP address or IP address range.</span></span>

> [!NOTE]
> <span data-ttu-id="5c263-139">SQL Database는 포트 1433을 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-139">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="5c263-140">회사 네트워크 내에서 연결을 시도하는 경우 포트 1433을 통한 아웃바운드 트래픽이 네트워크 방화벽에서 허용되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-140">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="5c263-141">이 경우 IT 부서에서 포트 1433을 열지 않으면 Azure SQL Database 서버에 연결할 수 없습니다</span><span class="sxs-lookup"><span data-stu-id="5c263-141">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a><span data-ttu-id="5c263-142">SSMS를 사용하여 데이터베이스 수준 방화벽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="5c263-142">Create a database-level firewall rule using SSMS</span></span>

<span data-ttu-id="5c263-143">데이터베이스 수준 방화벽 규칙을 사용하면 동일한 논리 서버 내에서 다른 데이터베이스에 다른 방화벽 설정을 만들고 이식 가능한 방화벽 규칙을 만들 수 있습니다. 즉, [장애 조치](sql-database-geo-replication-overview.md)하는 동안 데이터베이스를 SQL Server에 저장하지 않고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-143">Database-level firewall rules enable you to create different firewall settings for different databases within the same logical server and to create firewall rules that are portable - meaning that they follow the database during a [failover](sql-database-geo-replication-overview.md) rather than being stored on the SQL server.</span></span> <span data-ttu-id="5c263-144">데이터베이스 수준 방화벽 규칙은 Transact-SQL 문을 사용하는 경우에 한해 첫 번째 서버 수준 방화벽 규칙을 구성한 후에만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-144">Database-level firewall rules can only be configured by using Transact-SQL statements and only after you have configured the first server-level firewall rule.</span></span> <span data-ttu-id="5c263-145">자세한 내용은 [Azure SQL Database 서버 수준 및 데이터베이스 수준 방화벽 규칙 구성](sql-database-firewall-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c263-145">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="5c263-146">다음 단계에 따라 데이터베이스 관련 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-146">Follows these steps to create a database-specific firewall rule.</span></span>

1. <span data-ttu-id="5c263-147">예를 들어 [SQL Server Management Studio](./sql-database-connect-query-ssms.md)를 사용하여 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="5c263-147">Connect to your database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span></span>

2. <span data-ttu-id="5c263-148">개체 탐색기에서 방화벽 규칙을 추가할 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-148">In Object Explorer, right-click on the database you want to add a firewall rule for and click **New Query**.</span></span> <span data-ttu-id="5c263-149">데이터베이스에 연결된 비어 있는 쿼리 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-149">A blank query window opens that is connected to your database.</span></span>

3. <span data-ttu-id="5c263-150">쿼리 창에서 IP 주소를 공용 IP 주소로 수정하고 다음과 같은 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-150">In the query window, modify the IP address to your public IP address and then execute the following query:</span></span>

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. <span data-ttu-id="5c263-151">도구 모음에서 **실행**을 클릭하여 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-151">On the toolbar, click **Execute** to create the firewall rule.</span></span>

## <a name="view-how-to-connect-an-application-to-your-database-using-a-secure-connection-string"></a><span data-ttu-id="5c263-152">보안 연결 문자열을 사용하여 응용 프로그램을 데이터베이스에 연결하는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-152">View how to connect an application to your database using a secure connection string</span></span>

<span data-ttu-id="5c263-153">클라이언트 응용 프로그램과 SQL Database 간에 암호화된 연결의 보안을 보장하려면 연결 문자열을 다음과 같이 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-153">To ensure a secure, encrypted connection between a client application and SQL Database, the connection string has to be configured to:</span></span>

- <span data-ttu-id="5c263-154">암호화된 연결을 요청하고</span><span class="sxs-lookup"><span data-stu-id="5c263-154">Request an encrypted connection, and</span></span>
- <span data-ttu-id="5c263-155">서버 인증서를 신뢰하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-155">To not trust the server certificate.</span></span> 

<span data-ttu-id="5c263-156">이렇게 하면 TLS(전송 계층 보안)를 사용하여 연결이 설정되고 메시지 가로채기(man-in-the-middle) 공격의 위험을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-156">This establishes a connection using Transport Layer Security (TLS) and reduces the risk of man-in-the-middle attacks.</span></span> <span data-ttu-id="5c263-157">아래 스크린샷의 ADO.NET에 표시된 것처럼 Azure Portal에서 지원되는 클라이언트 드라이버의 SQL Database에 대해 올바르게 구성된 연결 문자열을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-157">You can obtain correctly configured connection strings for your SQL Database for supported client drivers from the Azure portal as shown for ADO.net in this screenshot.</span></span>

1. <span data-ttu-id="5c263-158">왼쪽 메뉴에서 **SQL Database**를 선택하고 **SQL Database** 페이지에서 데이터베이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-158">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span>

2. <span data-ttu-id="5c263-159">데이터베이스의 **개요** 페이지에서 **데이터베이스 연결 문자열 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-159">On the **Overview** page for your database, click **Show database connection strings**.</span></span>

3. <span data-ttu-id="5c263-160">전체 **ADO.NET** 연결 문자열을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-160">Review the complete **ADO.NET** connection string.</span></span>

    ![ADO.NET 연결 문자열](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a><span data-ttu-id="5c263-162">데이터베이스 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5c263-162">Creating database users</span></span>

<span data-ttu-id="5c263-163">사용자를 만들기 전에 먼저 Azure SQL Database가 지원하는 두 가지 인증 유형 중 하나를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-163">Before creating any users, you must first choose from one of two authentication types supported by Azure SQL Database:</span></span> 

<span data-ttu-id="5c263-164">**SQL 인증**은 논리 서버 내 특정 데이터베이스의 컨텍스트 내에서만 유효한 로그인 및 사용자에 대해 사용자 이름 및 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-164">**SQL Authentication**, which uses username and password for logins and users that are valid only in the context of a specific database within a logical server.</span></span> 

<span data-ttu-id="5c263-165">**Azure Active Directory 인증**은 Azure Active Directory에서 관리되는 ID를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-165">**Azure Active Directory Authentication**, which uses identities managed by Azure Active Directory.</span></span> 

<span data-ttu-id="5c263-166">[Azure Active Directory](./sql-database-aad-authentication.md)를 사용하여 SQL Database에 대해 인증을 수행하려면 채워진 Azure Active Directory가 있어야 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-166">If you want to use [Azure Active Directory](./sql-database-aad-authentication.md) to authenticate against SQL Database, a populated Azure Active Directory must exist before you can proceed.</span></span>

<span data-ttu-id="5c263-167">SQL 인증을 사용하여 사용자를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-167">Follow these steps to create a user using SQL Authentication:</span></span>

1. <span data-ttu-id="5c263-168">서버 관리자 자격 증명(예: [SQL Server Management Studio](./sql-database-connect-query-ssms.md))을 사용하여 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-168">Connect to your database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) using your server admin credentials.</span></span>

2. <span data-ttu-id="5c263-169">개체 탐색기에서 새 사용자를 추가할 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-169">In Object Explorer, right-click on the database you want to add a new user on and click **New Query**.</span></span> <span data-ttu-id="5c263-170">선택한 데이터베이스에 연결된 비어 있는 쿼리 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-170">A blank query window opens that is connected to the selected database.</span></span>

3. <span data-ttu-id="5c263-171">쿼리 창에서 다음 쿼리를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-171">In the query window, enter the following query:</span></span>

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. <span data-ttu-id="5c263-172">도구 모음에서 **실행**을 클릭하여 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-172">On the toolbar, click **Execute** to create the user.</span></span>

5. <span data-ttu-id="5c263-173">기본적으로 사용자는 데이터베이스에 연결할 수 있지만 데이터를 읽거나 쓰는 권한은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-173">By default, the user can connect to the database, but has no permissions to read or write data.</span></span> <span data-ttu-id="5c263-174">새로 만든 사용자에게 이러한 권한을 부여하려면 새 쿼리 창에서 다음 두 가지 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-174">To grant these permissions to the newly created user, execute the following two commands in a new query window</span></span>

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

<span data-ttu-id="5c263-175">새로운 사용자 만들기와 같은 관리자 작업을 실행해야 하는 경우가 아니라면 데이터베이스 수준에서 관리자가 아닌 계정을 만들어서 데이터베이스에 연결하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-175">It is best practice to create these non-administrator accounts at the database level to connect to your database unless you need to execute administrator tasks like creating new users.</span></span> <span data-ttu-id="5c263-176">Azure Active Directory를 사용하여 인증하는 방법에 대한 자세한 내용은 [Azure Active Directory 자습서](./sql-database-aad-authentication-configure.md)를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="5c263-176">Please review the [Azure Active Directory tutorial](./sql-database-aad-authentication-configure.md) on how to authenticate using Azure Active Directory.</span></span>


## <a name="protect-your-data-with-encryption"></a><span data-ttu-id="5c263-177">암호화로 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="5c263-177">Protect your data with encryption</span></span>

<span data-ttu-id="5c263-178">Azure SQL Database 투명한 데이터 암호화(TDE)는 암호화된 데이터베이스에 액세스하는 응용 프로그램을 변경하지 않고도 미사용 데이터를 자동으로 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-178">Azure SQL Database transparent data encryption (TDE) automatically encrypts your data at rest, without requiring any changes to the application accessing the encrypted database.</span></span> <span data-ttu-id="5c263-179">새로 만든 데이터베이스의 경우 TDE는 기본적으로 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-179">For newly created databases, TDE is on by default.</span></span> <span data-ttu-id="5c263-180">데이터베이스에 TDE를 사용하도록 설정하거나 TDE가 켜져 있는지 확인하려면 다음과 같은 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-180">To enable TDE for your database or to verify that TDE is on, follow these steps:</span></span>

1. <span data-ttu-id="5c263-181">왼쪽 메뉴에서 **SQL Database**를 선택하고 **SQL Database** 페이지에서 데이터베이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-181">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 

2. <span data-ttu-id="5c263-182">**투명한 데이터 암호화**를 클릭하여 TDE의 구성 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-182">Click on **Transparent data encryption** to open the configuration page for TDE.</span></span>

    ![투명한 데이터 암호화](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. <span data-ttu-id="5c263-184">필요한 경우 **데이터 암호화**를 켜짐으로 설정하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-184">If necessary, set **Data encryption** to ON and click **Save**.</span></span>

<span data-ttu-id="5c263-185">암호화 프로세스가 백그라운드에서 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-185">The encryption process starts in the background.</span></span> <span data-ttu-id="5c263-186">[SQL Server Management Studio](./sql-database-connect-query-ssms.md)를 사용하여 `sys.dm_database_encryption_keys` 보기의 encryption_state 열을 쿼리하고 SQL Database에 연결하여 진행률을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-186">You can monitor the progress by connecting to SQL Database using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) by querying the encryption_state column of the `sys.dm_database_encryption_keys` view.</span></span>

## <a name="enable-sql-database-auditing-if-necessary"></a><span data-ttu-id="5c263-187">필요한 경우 SQL Database 감사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-187">Enable SQL Database auditing, if necessary</span></span>

<span data-ttu-id="5c263-188">Azure SQL Database 감사는 데이터베이스 이벤트를 추적하고 Azure Storage 계정의 감사 로그에 이벤트를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-188">Azure SQL Database Auditing tracks database events and writes them to an audit log in your Azure Storage account.</span></span> <span data-ttu-id="5c263-189">감사는 규정 준수를 유지 관리하고, 데이터베이스 작업을 이해하고, 잠재적인 보안 위반을 나타낼 수 있는 불일치 및 이상 활동을 파악하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-189">Auditing can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate potential security violations.</span></span> <span data-ttu-id="5c263-190">SQL Database에 대한 기본 감사 정책을 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-190">Follow these steps to create a default auditing policy for your SQL database:</span></span>

1. <span data-ttu-id="5c263-191">왼쪽 메뉴에서 **SQL Database**를 선택하고 **SQL Database** 페이지에서 데이터베이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-191">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 

2. <span data-ttu-id="5c263-192">설정 블레이드에서 **감사 및 위협 감지**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-192">In the Settings blade, select **Auditing & Threat Detection**.</span></span> <span data-ttu-id="5c263-193">서버 수준 감사를 비활성화하면 이 컨텍스트의 서버 감사 설정을 보거나 수정할 수 있는 **서버 감사 설정 보기** 링크가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-193">Notice that sever-level auditing is diabled and that there is a **View server settings** link that allows you to view or modify the server auditing settings from this context.</span></span>

    ![감사 블레이드](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. <span data-ttu-id="5c263-195">서버 수준에서 지정된 형식과 다른 감사 형식(또는 위치)을 사용하는 경우 감사를 **켜고** **Blob** 감사 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-195">If you prefer to enable an Audit type (or location?) different from the one specified at the server level, turn **ON** Auditing, and choose the **Blob** Auditing Type.</span></span> <span data-ttu-id="5c263-196">서버 Blob 감사가 활성화되면 구성된 데이터베이스 감사가 서버 Blob 감사와 나란히 존재하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-196">If server Blob auditing is enabled, the database configured audit will exist side by side with the server Blob audit.</span></span>

    ![감사 설정](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. <span data-ttu-id="5c263-198">**저장소 세부 정보** 를 선택하여 감사 로그 저장소 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-198">Select **Storage Details** to open the Audit Logs Storage Blade.</span></span> <span data-ttu-id="5c263-199">로그가 저장되는 Azure 저장소 계정을 선택하고, 이 기간 후 오래된 로그가 삭제되는 보존 기간을 선택한 다음 하단에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-199">Select the Azure storage account where logs will be saved, and the retention period, after which the old logs will be deleted, then click **OK** at the bottom.</span></span> 

   > [!TIP]
   > <span data-ttu-id="5c263-200">감사 보고서 템플릿을 활용하려면 감사되는 모든 데이터베이스에 대해 동일한 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-200">Use the same storage account for all audited databases to get the most out of the auditing reports templates.</span></span>
   > 

5. <span data-ttu-id="5c263-201">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-201">Click **Save**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5c263-202">감사 이벤트를 사용자 지정하려면 PowerShell 또는 REST API를 통해 다음 작업을 수행합니다. 자세한 내용은 [Automation(PowerShell/REST API)](sql-database-auditing.md#subheading-7) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c263-202">If you want to customize the audited events, you can do this via PowerShell or REST API - see the [Automation (PowerShell / REST API)](sql-database-auditing.md#subheading-7) section for more details.</span></span>
>

## <a name="enable-sql-database-threat-detection"></a><span data-ttu-id="5c263-203">SQL Database 위협 감지 사용</span><span class="sxs-lookup"><span data-stu-id="5c263-203">Enable SQL Database threat detection</span></span>

<span data-ttu-id="5c263-204">위협 감지는 비정상적인 활동에 대한 보안 경고를 제공하여 잠재적인 위협이 발생하면 고객이 이를 감지하고 대응할 수 있도록 하는 새로운 차원의 보안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-204">Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="5c263-205">사용자는 데이터베이스의 데이터를 액세스, 침범 또는 악용하려는 시도로 인해 의심스러운 이벤트가 발생했는지를 판단하기 위해서 SQL Database 감사를 사용하여 의심스러운 이벤트를 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-205">Users can explore the suspicious events using SQL Database Auditing to determine if they result from an attempt to access, breach or exploit data in the database.</span></span> <span data-ttu-id="5c263-206">위협 감지는 보안 전문가가 되거나 고급 보안 모니터링 시스템을 관리할 필요 없이 데이터베이스에 대한 잠재적인 위협에 간단하게 대처할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-206">Threat Detection makes it simple to address potential threats to the database without the need to be a security expert or manage advanced security monitoring systems.</span></span>
<span data-ttu-id="5c263-207">예를 들어 위협 감지는 잠재적인 SQL 삽입 시도를 나타내는 비정상적인 데이터베이스 활동을 감지합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-207">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="5c263-208">SQL 삽입은 데이터 기반 응용 프로그램 공격에 사용되는 인터넷 상의 일반적인 웹 응용 프로그램 보안 문제 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-208">SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="5c263-209">공격자는 데이터베이스의 데이터를 침범하거나 수정하기 위해 응용 프로그램의 취약성을 이용하여 악의적인 SQL 문을 응용 프로그램 항목 필드에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-209">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, for breaching or modifying data in the database.</span></span>

1. <span data-ttu-id="5c263-210">모니터링할 SQL Database의 구성 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-210">Navigate to the configuration blade of the SQL database you want to monitor.</span></span> <span data-ttu-id="5c263-211">설정 블레이드에서 **감사 및 위협 감지**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-211">In the Settings blade, select **Auditing & Threat Detection**.</span></span>

    ![탐색 창](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. <span data-ttu-id="5c263-213">**감사 및 위협 감지** 구성 블레이드에서 감사를 **켜면** 위협 감지 설정이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-213">In the **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display the threat detection settings.</span></span>

3. <span data-ttu-id="5c263-214">위협 감지를 **켭니다**.</span><span class="sxs-lookup"><span data-stu-id="5c263-214">Turn **ON** threat detection.</span></span>

4. <span data-ttu-id="5c263-215">비정상적인 데이터베이스 활동이 감지되는 경우 보안 경고를 수신할 이메일 목록을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-215">Configure the list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>

5. <span data-ttu-id="5c263-216">**감사 및 위협 감지** 블레이드에서 **저장**을 클릭하여 새로운 또는 업데이트된 감사 및 위협 감지 정책을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-216">Click **Save** in the **Auditing & Threat detection** blade to save the new or updated auditing and threat detection policy.</span></span>

    ![탐색 창](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    <span data-ttu-id="5c263-218">비정상적인 데이터베이스 활동이 감지되면 이에 대한 이메일 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-218">If anomalous database activities are detected, you will receive an email notification upon detection of anomalous database activities.</span></span> <span data-ttu-id="5c263-219">이메일에는 비정상적인 활동의 특징, 데이터베이스 이름, 서버 이름, 이벤트 시간을 포함하여 의심스러운 보안 이벤트에 대한 정보가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-219">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name and the event time.</span></span> <span data-ttu-id="5c263-220">또한 가능한 원인에 대한 정보와 데이터베이스에 대한 잠재적인 위협을 조사하고 완화시키기 위해 권장되는 조치가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-220">In addition, it will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span> <span data-ttu-id="5c263-221">다음 단계에서는 이러한 전자 메일을 받기 위해 수행해야 할 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-221">The next steps walk you through what to do should you receive such an email:</span></span>

    ![위협 감지 전자 메일](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. <span data-ttu-id="5c263-223">전자 메일에서 **Azure SQL 감사 로그** 링크를 클릭하면 Azure Portal이 열리고 의심스러운 이벤트가 발생한 무렵의 시간에 해당하는 감사 레코드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-223">In the email, click on the **Azure SQL Auditing Log** link, which will launch the Azure portal and show the relevant auditing records around the time of the suspicious event.</span></span>

    ![감사 레코드](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. <span data-ttu-id="5c263-225">의심스러운 데이터베이스 활동에 대한 세부 정보(예: SQL 문, 실패 원인, 클라이언트 IP)를 보려면 감사 레코드를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-225">Click on the audit records to view more details on the suspicious database activities such as SQL statement, failure reason and client IP.</span></span>

    ![레코드 세부 정보](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. <span data-ttu-id="5c263-227">미리 구성된 Excel 템플릿을 열고 의심스러운 이벤트가 발생한 무렵의 시간에 대한 감사 로그를 가져와서 심층적인 분석을 실행하려면 감사 레코드 블레이드에서 **Excel에서 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-227">In the Auditing Records blade, click  **Open in Excel** to open a pre-configured excel template to import and run deeper analysis of the audit log around the time of the suspicious event.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5c263-228">Excel 2010 이상의 경우 파워 쿼리 및 **빠른 결합** 설정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-228">In Excel 2010 or later, Power Query and the **Fast Combine** setting is required.</span></span>

    ![Excel에서 레코드 열기](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. <span data-ttu-id="5c263-230">**빠른 결합** 설정을 구성하려면 - **파워 쿼리** 리본 탭에서 **옵션**을 선택하여 옵션 대화 상자를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-230">To configure the **Fast Combine** setting - In the **POWER QUERY** ribbon tab, select **Options** to display the Options dialog.</span></span> <span data-ttu-id="5c263-231">개인 정보 섹션을 선택하고 두 번째 옵션 '개인 정보 보호 수준을 무시하고 잠재적으로 성능 향상'을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-231">Select the Privacy section and choose the second option - 'Ignore the Privacy Levels and potentially improve performance':</span></span>

    ![Excel 빠른 결합](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. <span data-ttu-id="5c263-233">SQL 감사 로그를 로드하려면, 설정 탭의 매개 변수가 바르게 설정되었는지 확인한 후 '데이터' 리본을 선택하고 '모두 새로 고침' 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-233">To load SQL audit logs, ensure that the parameters in the settings tab are set correctly and then select the 'Data' ribbon and click the 'Refresh All' button.</span></span>

    ![Excel 매개 변수](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. <span data-ttu-id="5c263-235">**SQL 감사 로그** 시트에 결과가 표시되며 사용자는 이를 통해 감지된 비정상적인 활동을 심층적으로 분석하고 응용 프로그램의 보안 이벤트에 대한 영향을 완화시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-235">The results appear in the **SQL Audit Logs** sheet which enables you to run deeper analysis of the anomalous activities that were detected, and mitigate the impact of the security event in your application.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5c263-236">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5c263-236">Next steps</span></span>
<span data-ttu-id="5c263-237">몇 가지 간단한 단계만 거치면 악의적인 사용자 또는 무단 액세스로부터 데이터베이스를 보호하는 기능을 크게 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-237">You can improve the protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="5c263-238">이 자습서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5c263-238">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="5c263-239">서버 및 데이터베이스에 대한 방화벽 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="5c263-239">Set up firewall rules for your sever and or database</span></span>
> * <span data-ttu-id="5c263-240">보안 연결 문자열을 사용하여 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="5c263-240">Connect to your database using a secure connection string</span></span>
> * <span data-ttu-id="5c263-241">사용자 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="5c263-241">Manage user access</span></span>
> * <span data-ttu-id="5c263-242">암호화로 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="5c263-242">Protect your data with encryption</span></span>
> * <span data-ttu-id="5c263-243">SQL Database 감사 사용</span><span class="sxs-lookup"><span data-stu-id="5c263-243">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="5c263-244">SQL Database 위협 감지 사용</span><span class="sxs-lookup"><span data-stu-id="5c263-244">Enable SQL Database threat detection</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="5c263-245">SQL Database 성능 향상</span><span class="sxs-lookup"><span data-stu-id="5c263-245">Improve SQL Database performance</span></span>](sql-database-performance-tutorial.md)

