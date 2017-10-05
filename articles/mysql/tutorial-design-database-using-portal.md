---
title: "첫 번째 Azure Database for MySQL 데이터베이스 디자인 - Azure Portal | Microsoft Docs"
description: "이 자습서에서는 Azure Portal을 사용하여 Azure Database for MySQL 서버 및 데이터베이스를 만들고 관리하는 방법에 대해 설명합니다."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: c7b76cacbdc4e483353f64cc4e50c974867bb5b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="bb98c-103">첫 번째 Azure Database for MySQL 데이터베이스 디자인</span><span class="sxs-lookup"><span data-stu-id="bb98c-103">Design your first Azure Database for MySQL database</span></span>
<span data-ttu-id="bb98c-104">Azure Database for MySQL은 클라우드에서 항상 사용 가능한 MySQL 데이터베이스를 실행, 관리 및 크기 조정할 수 있게 하는 관리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-104">Azure Database for MySQL is a managed service that enables you to run, manage, and scale highly available MySQL databases in the cloud.</span></span> <span data-ttu-id="bb98c-105">Azure Portal을 사용하면 쉽게 서버를 관리하고 데이터베이스를 디자인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-105">Using the Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="bb98c-106">이 자습서에서는 Azure Portal을 사용하여 다음을 수행하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-106">In this tutorial, you use the Azure portal to learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bb98c-107">Azure Database for MySQL 만들기</span><span class="sxs-lookup"><span data-stu-id="bb98c-107">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="bb98c-108">서버 방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="bb98c-108">Configure the server firewall</span></span>
> * <span data-ttu-id="bb98c-109">mysql 명령줄 도구를 사용하여 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="bb98c-109">Use mysql command-line tool to create a database</span></span>
> * <span data-ttu-id="bb98c-110">샘플 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="bb98c-110">Load sample data</span></span>
> * <span data-ttu-id="bb98c-111">쿼리 데이터</span><span class="sxs-lookup"><span data-stu-id="bb98c-111">Query data</span></span>
> * <span data-ttu-id="bb98c-112">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="bb98c-112">Update data</span></span>
> * <span data-ttu-id="bb98c-113">데이터 복원</span><span class="sxs-lookup"><span data-stu-id="bb98c-113">Restore data</span></span>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="bb98c-114">Azure 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-114">Sign in to the Azure portal</span></span>
<span data-ttu-id="bb98c-115">원하는 웹 브라우저를 열고 [Microsoft Azure Portal](https://portal.azure.com/)을 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-115">Open your favorite web browser, and visit the [Microsoft Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="bb98c-116">자격 증명을 입력하여 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-116">Enter your credentials to sign in to the portal.</span></span> <span data-ttu-id="bb98c-117">기본 보기는 서비스 대시보드입니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-117">The default view is your service dashboard.</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="bb98c-118">Azure Database for MySQL 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="bb98c-118">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="bb98c-119">Azure Database for MySQL 서버는 정의된 [계산 및 저장소 리소스](./concepts-compute-unit-and-storage.md) 집합을 사용하여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-119">An Azure Database for MySQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="bb98c-120">서버는 [Azure 리소스 그룹](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) 내에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-120">The server is created within an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

1. <span data-ttu-id="bb98c-121">**데이터베이스** > **MySQL용 Azure Database**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-121">Navigate to **Databases** > **Azure Database for MySQL**.</span></span> <span data-ttu-id="bb98c-122">**데이터베이스** 범주 아래에서 MySQL 서버를 찾을 수 없으면 **모두 표시**를 클릭하여 사용 가능한 모든 데이터베이스 서비스를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-122">If you cannot find MySQL Server under **Databases** category, click **See all** to show all available database services.</span></span> <span data-ttu-id="bb98c-123">검색 상자에 **MySQL용 Azure Database**를 입력하여 신속하게 서비스를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-123">You can also type **Azure Database for MySQL** in the search box to quickly find the service.</span></span>
<span data-ttu-id="bb98c-124">![2-1 MySQL로 이동](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span><span class="sxs-lookup"><span data-stu-id="bb98c-124">![2-1 Navigate to MySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span></span>

2. <span data-ttu-id="bb98c-125">**MySQL용 Azure Database** 타일을 클릭한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-125">Click **Azure Database for MySQL** tile, and then click **Create**.</span></span>

<span data-ttu-id="bb98c-126">이 예제에서는 Azure Database for MySQL 양식을 다음 정보로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-126">In our example, fill out the Azure Database for MySQL form with the following information:</span></span>

| <span data-ttu-id="bb98c-127">**설정**</span><span class="sxs-lookup"><span data-stu-id="bb98c-127">**Setting**</span></span> | <span data-ttu-id="bb98c-128">**제안 값**</span><span class="sxs-lookup"><span data-stu-id="bb98c-128">**Suggested value**</span></span> | <span data-ttu-id="bb98c-129">**필드 설명**</span><span class="sxs-lookup"><span data-stu-id="bb98c-129">**Field Description**</span></span> |
|---|---|---|
| <span data-ttu-id="bb98c-130">*서버 이름*</span><span class="sxs-lookup"><span data-stu-id="bb98c-130">*Server name*</span></span> | <span data-ttu-id="bb98c-131">myserver4demo</span><span class="sxs-lookup"><span data-stu-id="bb98c-131">myserver4demo</span></span>  | <span data-ttu-id="bb98c-132">서버 이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-132">Server name has to be globally unique.</span></span> |
| <span data-ttu-id="bb98c-133">*구독*</span><span class="sxs-lookup"><span data-stu-id="bb98c-133">*Subscription*</span></span> | <span data-ttu-id="bb98c-134">mysubscription</span><span class="sxs-lookup"><span data-stu-id="bb98c-134">mysubscription</span></span> | <span data-ttu-id="bb98c-135">드롭다운에서 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-135">Select your subscription from the drop-down.</span></span> |
| <span data-ttu-id="bb98c-136">*리소스 그룹*</span><span class="sxs-lookup"><span data-stu-id="bb98c-136">*Resource group*</span></span> | <span data-ttu-id="bb98c-137">myresourcegroup</span><span class="sxs-lookup"><span data-stu-id="bb98c-137">myresourcegroup</span></span> | <span data-ttu-id="bb98c-138">리소스 그룹을 만들거나 기존 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-138">Create a resource group or use an existing one.</span></span> |
| <span data-ttu-id="bb98c-139">*서버 관리자 로그인*</span><span class="sxs-lookup"><span data-stu-id="bb98c-139">*Server admin login*</span></span> | <span data-ttu-id="bb98c-140">myadmin</span><span class="sxs-lookup"><span data-stu-id="bb98c-140">myadmin</span></span> | <span data-ttu-id="bb98c-141">관리자 계정 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-141">Setup admin account name.</span></span> |
| <span data-ttu-id="bb98c-142">*암호*</span><span class="sxs-lookup"><span data-stu-id="bb98c-142">*Password*</span></span> |  | <span data-ttu-id="bb98c-143">강력한 관리자 계정 암호를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-143">Set a strong admin account password.</span></span> |
| <span data-ttu-id="bb98c-144">*암호 확인*</span><span class="sxs-lookup"><span data-stu-id="bb98c-144">*Confirm password*</span></span> |  | <span data-ttu-id="bb98c-145">관리자 계정 암호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-145">Confirm the admin account password.</span></span> |
| <span data-ttu-id="bb98c-146">*위치*</span><span class="sxs-lookup"><span data-stu-id="bb98c-146">*Location*</span></span> |  | <span data-ttu-id="bb98c-147">사용 가능한 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-147">Select an available region.</span></span> |
| <span data-ttu-id="bb98c-148">*버전*</span><span class="sxs-lookup"><span data-stu-id="bb98c-148">*Version*</span></span> | <span data-ttu-id="bb98c-149">5.7</span><span class="sxs-lookup"><span data-stu-id="bb98c-149">5.7</span></span> | <span data-ttu-id="bb98c-150">최신 버전을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-150">Choose the latest version.</span></span> |
| <span data-ttu-id="bb98c-151">*성능 구성*</span><span class="sxs-lookup"><span data-stu-id="bb98c-151">*Configure performance*</span></span> | <span data-ttu-id="bb98c-152">기본, 50 계산 단위, 50GB</span><span class="sxs-lookup"><span data-stu-id="bb98c-152">Basic, 50 compute units, 50 GB</span></span>  | <span data-ttu-id="bb98c-153">**가격 책정 계층**, **계산 단위**, **저장소(GB)**를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-153">Choose **Pricing tier**, **Compute Units**, **Storage (GB)**, and then click **OK**.</span></span> |
| <span data-ttu-id="bb98c-154">*대시보드에 고정*</span><span class="sxs-lookup"><span data-stu-id="bb98c-154">*Pin to Dashboard*</span></span> | <span data-ttu-id="bb98c-155">확인</span><span class="sxs-lookup"><span data-stu-id="bb98c-155">Check</span></span> | <span data-ttu-id="bb98c-156">나중에 쉽게 서버를 찾을 수 있도록 이 확인란을 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-156">Recommended to check this box so you may find the server easily later on</span></span> |
<span data-ttu-id="bb98c-157">그런 다음에 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-157">Then, click **Create**.</span></span> <span data-ttu-id="bb98c-158">1, 2분 안에 새 Azure Database for MySQL 서버가 클라우드에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-158">In a minute or two, a new Azure Database for MySQL server is running in the cloud.</span></span> <span data-ttu-id="bb98c-159">도구 모음에서 **알림** 단추를 클릭하여 배포 프로세스를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-159">You can click **Notifications** button on the toolbar to monitor the deployment process.</span></span>

## <a name="configure-firewall"></a><span data-ttu-id="bb98c-160">방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="bb98c-160">Configure firewall</span></span>
<span data-ttu-id="bb98c-161">Azure Databases for MySQL은 방화벽으로 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-161">Azure Databases for MySQL are protected by a firewall.</span></span> <span data-ttu-id="bb98c-162">기본적으로 서버 및 서버 내의 데이터베이스에 대한 모든 연결은 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-162">By default, all connections to the server and the databases inside the server are rejected.</span></span> <span data-ttu-id="bb98c-163">처음으로 MySQL용 Azure Database에 연결하기 전에 먼저 방화벽을 구성하여 클라이언트 컴퓨터의 공용 네트워크 IP 주소(또는 IP 주소 범위)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-163">Before connecting to Azure Database for MySQL for the first time, configure the firewall to add the client machine's public network IP address (or IP address range).</span></span>

1. <span data-ttu-id="bb98c-164">새로 만든 서버를 클릭한 다음 **연결 보안**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-164">Click your newly created server, and then click **Connection security**.</span></span>
   <span data-ttu-id="bb98c-165">![3-1 연결 보안](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span><span class="sxs-lookup"><span data-stu-id="bb98c-165">![3-1 Connection security](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span></span>
2. <span data-ttu-id="bb98c-166">**내 IP를 추가**하거나 여기서 방화벽 규칙을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-166">You can **Add My IP**, or configure firewall rules here.</span></span> <span data-ttu-id="bb98c-167">규칙을 만든 후에 **저장**을 클릭해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-167">Remember to click **Save** after you have created the rules.</span></span>
<span data-ttu-id="bb98c-168">이제 mysql 명령줄 도구 또는 MySQL Workbench GUI 도구를 사용하여 서버에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-168">You can now connect to the server using mysql command-line tool or MySQL Workbench GUI tool.</span></span>

> [!TIP]
> <span data-ttu-id="bb98c-169">Azure Databases for MySQL 서버는 3306 포트를 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-169">Azure Database for MySQL server communicates over port 3306.</span></span> <span data-ttu-id="bb98c-170">회사 네트워크 내에서 연결하려는 경우 3306 포트를 통한 아웃바운드 트래픽이 네트워크 방화벽에서 허용되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-170">If you are trying to connect from within a corporate network, outbound traffic over port 3306 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="bb98c-171">이 경우 IT 부서에서 포트 3306을 열지 않으면 Azure MySQL 서버에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-171">If so, you cannot connect to Azure MySQL server unless your IT department opens port 3306.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="bb98c-172">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="bb98c-172">Get connection information</span></span>
<span data-ttu-id="bb98c-173">Azure Portal에서 MySQL용 Azure Database 서버의 정규화된 **서버 이름** 및 **서버 관리자 로그인 이름**을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-173">Get the fully qualified **Server name** and **Server admin login name** for your Azure Database for MySQL server from the Azure portal.</span></span> <span data-ttu-id="bb98c-174">정규화된 서버 이름을 사용하여 mysql 명령줄 도구를 통해 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-174">You use the fully qualified server name to connect to your server using mysql command-line tool.</span></span> 

1. <span data-ttu-id="bb98c-175">[Azure Portal](https://portal.azure.com/)의 왼쪽 메뉴에서 **모든 리소스**를 클릭하고 이름을 입력한 다음 MySQL용 Azure Database 서버를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-175">In [Azure portal](https://portal.azure.com/), click **All resources** from the left-hand menu, type the name, and search for your Azure Database for MySQL server.</span></span> <span data-ttu-id="bb98c-176">서버 이름을 선택하여 세부 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-176">Select the server name to view the details.</span></span>

2. <span data-ttu-id="bb98c-177">설정 제목 아래에서 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-177">Under the Settings heading, click **Properties**.</span></span> <span data-ttu-id="bb98c-178">**서버 이름** 및 **서버 관리자 로그인 이름**을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-178">Note down **SERVER NAME** and **SERVER ADMIN LOGIN NAME**.</span></span> <span data-ttu-id="bb98c-179">각 필드 옆에 있는 복사 단추를 클릭하여 클립보드에 복사할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-179">You may click the copy button next to each field to copy to the clipboard.</span></span>
   <span data-ttu-id="bb98c-180">![4-2 서버 속성](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span><span class="sxs-lookup"><span data-stu-id="bb98c-180">![4-2 server properties](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span></span>

<span data-ttu-id="bb98c-181">이 예제에서 서버 이름은 *myserver4demo.mysql.database.azure.com*이고, 서버 관리자 로그인은 *myadmin@myserver4demo*입니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-181">In this example, the server name is *myserver4demo.mysql.database.azure.com*, and the server admin login is *myadmin@myserver4demo*.</span></span>

## <a name="connect-to-the-server-using-mysql"></a><span data-ttu-id="bb98c-182">mysql을 사용하여 서버에 연결</span><span class="sxs-lookup"><span data-stu-id="bb98c-182">Connect to the server using mysql</span></span>
<span data-ttu-id="bb98c-183">[mysql 명령줄 도구](https://dev.mysql.com/doc/refman/5.7/en/mysql.html)를 사용하여 Azure Database for MySQL 서버로의 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-183">Use [mysql command-line tool](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) to establish a connection to your Azure Database for MySQL server.</span></span> <span data-ttu-id="bb98c-184">브라우저의 Azure Cloud Shell에서나 로컬로 설치된 mysql 도구를 사용하여 사용자 컴퓨터에서 mysql 명령줄 도구를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-184">You can run the mysql command-line tool from the Azure Cloud Shell in the browser or from your own machine using mysql tools installed locally.</span></span> <span data-ttu-id="bb98c-185">Azure Cloud Shell을 시작하려면 이 문서의 코드 블록에서 `Try It` 단추를 클릭하거나 Azure Portal을 방문하고 오른쪽 위 도구 모음에서 `>_` 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-185">To launch the Azure Cloud Shell, click the `Try It` button on a code block in this article, or visit the Azure portal and click the `>_` icon in the top right toolbar.</span></span> 

<span data-ttu-id="bb98c-186">연결할 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-186">Type the command to connect:</span></span>
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="bb98c-187">빈 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="bb98c-187">Create a blank database</span></span>
<span data-ttu-id="bb98c-188">서버에 연결되면 사용할 빈 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-188">Once you’re connected to the server, create a blank database to work with.</span></span>
```sql
CREATE DATABASE mysampledb;
```

<span data-ttu-id="bb98c-189">프롬프트에서 다음 명령을 실행하여 새로 만든 이 데이터베이스에 대한 연결로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-189">At the prompt, run the following command to switch connection to this newly created database:</span></span>
```sql
USE mysampledb;
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="bb98c-190">데이터베이스에서 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="bb98c-190">Create tables in the database</span></span>
<span data-ttu-id="bb98c-191">이제 Azure Database for MySQL 데이터베이스에 연결하는 방법을 알았으므로 몇 가지 기본 작업을 수행하는 방법을 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-191">Now that you know how to connect to the Azure Database for MySQL database, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="bb98c-192">먼저 테이블을 만들고 일부 데이터와 함께 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-192">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="bb98c-193">인벤토리 정보를 저장하는 테이블을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-193">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="bb98c-194">테이블에 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="bb98c-194">Load data into the tables</span></span>
<span data-ttu-id="bb98c-195">이제 테이블을 만들었으므로 이 테이블에 일부 데이터를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-195">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="bb98c-196">열린 명령 프롬프트 창에서 다음 쿼리를 실행하여 데이터 행을 일부 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-196">At the open command prompt window, run the following query to insert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="bb98c-197">이제 앞에서 만든 테이블에 두 개의 샘플 데이터 행이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-197">Now you have two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="bb98c-198">테이블의 데이터 쿼리 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="bb98c-198">Query and update the data in the tables</span></span>
<span data-ttu-id="bb98c-199">다음 쿼리를 실행하여 데이터베이스 테이블에서 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-199">Execute the following query to retrieve information from the database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="bb98c-200">또한 테이블의 데이터를 업데이트할 수도 있습니다</span><span class="sxs-lookup"><span data-stu-id="bb98c-200">You can also update the data in the tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="bb98c-201">이에 따라 데이터를 검색할 때 해당 행이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-201">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="bb98c-202">이전 시점으로 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="bb98c-202">Restore a database to a previous point in time</span></span>
<span data-ttu-id="bb98c-203">실수로 중요한 데이터베이스 테이블을 삭제했는데 데이터를 쉽게 복구할 수 없다고 상상해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-203">Imagine you have accidentally deleted an important database table, and cannot recover the data easily.</span></span> <span data-ttu-id="bb98c-204">MySQL용 Azure Database를 사용하면 서버를 지정 시간으로 복원하여 데이터베이스의 복사본을 새 서버에 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-204">Azure Database for MySQL allows you to restore the server to a point in time, creating a copy of the databases into new server.</span></span> <span data-ttu-id="bb98c-205">이 새 서버를 사용하여 삭제된 데이터를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-205">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="bb98c-206">다음 단계에서는 테이블이 추가되기 이전 시점으로 샘플 서버를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-206">The following steps restore the sample server to a point before the table was added.</span></span>

1. <span data-ttu-id="bb98c-207">Azure Portal에서 MySQL용 Azure Database를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-207">In the Azure portal, locate your Azure Database for MySQL.</span></span> <span data-ttu-id="bb98c-208">**개요** 페이지의 도구 모음에서 **복원**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-208">On the **Overview** page, click **Restore** on the toolbar.</span></span> <span data-ttu-id="bb98c-209">복원 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-209">The Restore page opens.</span></span>

   ![10-1 데이터베이스 복원](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. <span data-ttu-id="bb98c-211">**복원** 양식을 필요한 정보로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-211">Fill out the **Restore** form with the required information.</span></span>
   
   ![10-2 복원 양식](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - <span data-ttu-id="bb98c-213">**복원 지점**: 나열된 기간 내에서 복원하려는 지정 시간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-213">**Restore point**: Select a point-in-time that you want to restore to, within the timeframe listed.</span></span> <span data-ttu-id="bb98c-214">현지 표준 시간대를 UTC로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-214">Make sure to convert your local timezone to UTC.</span></span>
   - <span data-ttu-id="bb98c-215">**새 서버로 복원**: 복원하려는 새 서버 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-215">**Restore to new server**: Provide a new server name you want to restore to.</span></span>
   - <span data-ttu-id="bb98c-216">**위치**: 지역은 원본 서버와 같으며 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-216">**Location**: The region is same as the source server, and cannot be changed.</span></span>
   - <span data-ttu-id="bb98c-217">**가격 책정 계층**: 가격 책정 계층은 원본 서버와 같으며 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-217">**Pricing tier**: The pricing tier is the same as the source server, and cannot be changed.</span></span>
   
3. <span data-ttu-id="bb98c-218">**확인**을 클릭하여 서버를 테이블 삭제 이전의 [지정 시간으로 복원](./howto-restore-server-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-218">Click **OK** to restore the server to [restore to a point in time](./howto-restore-server-portal.md) before the table was deleted.</span></span> <span data-ttu-id="bb98c-219">서버를 복원하면 지정한 지정 시간을 기준으로 서버의 새 복사본이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-219">Restoring a server creates a new copy of the server, as of the point in time you specify.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bb98c-220">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bb98c-220">Next steps</span></span>
<span data-ttu-id="bb98c-221">이 자습서에서는 Azure Portal을 사용하여 다음을 수행하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="bb98c-221">In this tutorial, you use the Azure portal to learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bb98c-222">Azure Database for MySQL 만들기</span><span class="sxs-lookup"><span data-stu-id="bb98c-222">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="bb98c-223">서버 방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="bb98c-223">Configure the server firewall</span></span>
> * <span data-ttu-id="bb98c-224">mysql 명령줄 도구를 사용하여 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="bb98c-224">Use mysql command-line tool to create a database</span></span>
> * <span data-ttu-id="bb98c-225">샘플 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="bb98c-225">Load sample data</span></span>
> * <span data-ttu-id="bb98c-226">쿼리 데이터</span><span class="sxs-lookup"><span data-stu-id="bb98c-226">Query data</span></span>
> * <span data-ttu-id="bb98c-227">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="bb98c-227">Update data</span></span>
> * <span data-ttu-id="bb98c-228">데이터 복원</span><span class="sxs-lookup"><span data-stu-id="bb98c-228">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bb98c-229">MySQL용 Azure Database에 응용 프로그램을 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="bb98c-229">How to connect applications to Azure Database for MySQL</span></span>](./howto-connection-string.md)
