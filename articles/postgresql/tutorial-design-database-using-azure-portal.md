---
title: "Azure Portal을 사용하여 첫 번째 Azure Database for PostgreSQL 디자인 | Microsoft Docs"
description: "이 자습서에서는 Azure Portal을 사용하여 첫 번째 Azure Database for PostgreSQL을 디자인하는 방법을 보여 줍니다."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: tutorial, mvc
ms.topic: tutorial
ms.date: 05/10/2017
ms.openlocfilehash: 2aa9d10749b54537495ad3e09566c43718f67a9e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-the-azure-portal"></a><span data-ttu-id="a3f03-103">Azure Portal을 사용하여 첫 번째 Azure Database for PostgreSQL 디자인</span><span class="sxs-lookup"><span data-stu-id="a3f03-103">Design your first Azure Database for PostgreSQL using the Azure portal</span></span>

<span data-ttu-id="a3f03-104">Azure Database for PostgreSQL은 클라우드에서 항상 사용 가능한 PostgreSQL 데이터베이스를 실행, 관리 및 크기 조정할 수 있게 하는 관리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-104">Azure Database for PostgreSQL is a managed service that enables you to run, manage, and scale highly available PostgreSQL databases in the cloud.</span></span> <span data-ttu-id="a3f03-105">Azure Portal을 사용하면 쉽게 서버를 관리하고 데이터베이스를 디자인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-105">Using the Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="a3f03-106">이 자습서에서는 Azure Portal을 사용하여 다음을 수행하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-106">In this tutorial, you use the Azure portal to learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="a3f03-107">Azure Database for PostgreSQL 만들기</span><span class="sxs-lookup"><span data-stu-id="a3f03-107">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="a3f03-108">서버 방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="a3f03-108">Configure the server firewall</span></span>
> * <span data-ttu-id="a3f03-109">[**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) 유틸리티를 사용하여 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="a3f03-109">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="a3f03-110">샘플 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="a3f03-110">Load sample data</span></span>
> * <span data-ttu-id="a3f03-111">쿼리 데이터</span><span class="sxs-lookup"><span data-stu-id="a3f03-111">Query data</span></span>
> * <span data-ttu-id="a3f03-112">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="a3f03-112">Update data</span></span>
> * <span data-ttu-id="a3f03-113">데이터 복원</span><span class="sxs-lookup"><span data-stu-id="a3f03-113">Restore data</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3f03-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a3f03-114">Prerequisites</span></span>
<span data-ttu-id="a3f03-115">Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-115">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="a3f03-116">Azure Portal에 로그인</span><span class="sxs-lookup"><span data-stu-id="a3f03-116">Log in to the Azure portal</span></span>
<span data-ttu-id="a3f03-117">[Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-117">Log in to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-postgresql"></a><span data-ttu-id="a3f03-118">PostgreSQL용 Azure Database 만들기</span><span class="sxs-lookup"><span data-stu-id="a3f03-118">Create an Azure Database for PostgreSQL</span></span>

<span data-ttu-id="a3f03-119">Azure Database for PostgreSQL 서버는 정의된 [계산 및 저장소 리소스](./concepts-compute-unit-and-storage.md) 집합으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-119">An Azure Database for PostgreSQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="a3f03-120">서버는 [Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md) 내에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-120">The server is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="a3f03-121">다음 단계에 따라 Azure Database for PostgreSQL 서버를 를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-121">Follow these steps to create an Azure Database for PostgreSQL server:</span></span>
1.  <span data-ttu-id="a3f03-122">Azure Portal의 왼쪽 위 모서리에 있는 **+ 새로 만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-122">Click the **+ New**  button found on the upper left-hand corner of the Azure portal.</span></span>
2.  <span data-ttu-id="a3f03-123">**새로 만들기** 페이지에서 **데이터베이스**를 선택하고, **데이터베이스** 페이지에서 **Azure Database for PostgreSQL**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-123">Select **Databases** from the **New** page, and select **Azure Database for PostgreSQL** from the **Databases** page.</span></span>
 <span data-ttu-id="a3f03-124">![PostgreSQL용 Azure Database - 데이터베이스 만들기](./media/tutorial-design-database-using-azure-portal/1-create-database.png)</span><span class="sxs-lookup"><span data-stu-id="a3f03-124">![Azure Database for PostgreSQL - Create the database](./media/tutorial-design-database-using-azure-portal/1-create-database.png)</span></span>

3.  <span data-ttu-id="a3f03-125">위 이미지와 같이 다음 정보를 사용하여 새 서버 세부 정보 양식을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-125">Fill out the new server details form with the following information, as shown on the preceding image:</span></span>
    - <span data-ttu-id="a3f03-126">서버 이름: **mypgserver-20170401**(서버 이름은 DNS 이름에 매핑되므로 전역적으로 고유해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="a3f03-126">Server name: **mypgserver-20170401** (name of a server maps to DNS name and is thus required to be globally unique)</span></span> 
    - <span data-ttu-id="a3f03-127">구독: 구독이 여러 개인 경우 리소스가 있거나 요금이 청구되는 적절한 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-127">Subscription: If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span>
    - <span data-ttu-id="a3f03-128">리소스 그룹: **myresourcegroup**</span><span class="sxs-lookup"><span data-stu-id="a3f03-128">Resource group: **myresourcegroup**</span></span>
    - <span data-ttu-id="a3f03-129">서버 관리자 로그인 및 선택한 암호</span><span class="sxs-lookup"><span data-stu-id="a3f03-129">Server admin login and password of your choice</span></span>
    - <span data-ttu-id="a3f03-130">위치</span><span class="sxs-lookup"><span data-stu-id="a3f03-130">Location</span></span>
    - <span data-ttu-id="a3f03-131">PostgreSQL 버전</span><span class="sxs-lookup"><span data-stu-id="a3f03-131">PostgreSQL Version</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="a3f03-132">여기에 지정한 서버 관리자 로그인 및 암호는 이 빠른 시작의 뒷부분에 나오는 서버 및 데이터베이스에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-132">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="a3f03-133">나중에 사용하기 위해 이 정보를 기억하거나 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-133">Remember or record this information for later use.</span></span>

4.  <span data-ttu-id="a3f03-134">**가격 책정 계층**을 클릭하고 새 데이터베이스의 서비스 계층 및 성능 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-134">Click **Pricing tier** to specify the service tier and performance level for your new database.</span></span> <span data-ttu-id="a3f03-135">이 빠른 시작을 위해 **기본** 계층, **50개 계산 단위** 및 **50GB**의 포함된 저장소를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-135">For this quick start, select **Basic** Tier, **50 Compute Units** and **50 GB** of included storage.</span></span>
 <span data-ttu-id="a3f03-136">![PostgreSQL용 Azure Database - 서비스 계층 선택](./media/tutorial-design-database-using-azure-portal/2-service-tier.png)</span><span class="sxs-lookup"><span data-stu-id="a3f03-136">![Azure Database for PostgreSQL - pick the service tier](./media/tutorial-design-database-using-azure-portal/2-service-tier.png)</span></span>
5.  <span data-ttu-id="a3f03-137">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-137">Click **Ok**.</span></span>
6.  <span data-ttu-id="a3f03-138">**만들기**를 클릭하여 서버를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-138">Click **Create** to provision the server.</span></span> <span data-ttu-id="a3f03-139">프로비전하는 데 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-139">Provisioning takes a few minutes.</span></span>

  > [!TIP]
  > <span data-ttu-id="a3f03-140">배포를 쉽게 추적할 수 있도록 **대시보드에 고정** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-140">Check the **Pin to dashboard** option to allow easy tracking of your deployments.</span></span>

7.  <span data-ttu-id="a3f03-141">도구 모음에서 **알림**을 클릭하여 배포 프로세스를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-141">On the toolbar, click **Notifications** to monitor the deployment process.</span></span>
 <span data-ttu-id="a3f03-142">![PostgreSQL용 Azure Database - 알림 확인](./media/tutorial-design-database-using-azure-portal/3-notifications.png)</span><span class="sxs-lookup"><span data-stu-id="a3f03-142">![Azure Database for PostgreSQL - See notifications](./media/tutorial-design-database-using-azure-portal/3-notifications.png)</span></span>
   
  <span data-ttu-id="a3f03-143">기본적으로 **postgres** 데이터베이스가 서버 아래에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-143">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="a3f03-144">[postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) 데이터베이스는 사용자, 유틸리티 및 타사 응용 프로그램에서 사용하는 기본 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-144">The [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 

## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="a3f03-145">서버 수준 방화벽 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="a3f03-145">Configure a server-level firewall rule</span></span>

<span data-ttu-id="a3f03-146">PostgreSQL용 Azure Database 서비스는 서버 수준 방화벽을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-146">The Azure Database for PostgreSQL service creates a firewall at the server-level.</span></span> <span data-ttu-id="a3f03-147">방화벽 규칙을 만들어 특정 IP 주소에 대한 방화벽을 열지 않는 한 이 방화벽은 외부 응용 프로그램과 도구에서 서버 및 서버의 데이터베이스에 연결되지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-147">This firewall prevents external applications and tools from connecting to the server and any databases on the server unless a firewall rule is created to open the firewall for specific IP addresses.</span></span> 

1.  <span data-ttu-id="a3f03-148">배포가 완료되면 왼쪽 메뉴에서 **모든 리소스**를 클릭하고 **mypgserver-20170401** 이름을 입력하여 새로 만든 서버를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-148">After the deployment completes, click **All Resources** from the left-hand menu and type in the name **mypgserver-20170401** to search for your newly created server.</span></span> <span data-ttu-id="a3f03-149">검색 결과에 나열된 서버 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-149">Click the server name listed in the search result.</span></span> <span data-ttu-id="a3f03-150">서버에 대한 **개요** 페이지가 열리고 추가 구성을 위한 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-150">The **Overview** page for your server opens and provides options for further configuration.</span></span>
 
 ![<span data-ttu-id="a3f03-151">PostgreSQL용 Azure Database - 서버 검색</span><span class="sxs-lookup"><span data-stu-id="a3f03-151">Azure Database for PostgreSQL - Search for server</span></span> ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

2.  <span data-ttu-id="a3f03-152">서버 블레이드에서 **연결 보안**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-152">In the server blade, select **Connection Security**.</span></span> 
3.  <span data-ttu-id="a3f03-153">**규칙 이름** 아래의 텍스트 상자를 클릭하고 연결을 위한 IP 범위를 허용 목록으로 만드는 새 방화벽 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-153">Click in the text box under **Rule Name,** and add a new firewall rule to whitelist the IP range for connectivity.</span></span> <span data-ttu-id="a3f03-154">이 자습서에서는 **규칙 이름 = AllowAllIps**, **시작 IP = 0.0.0.0** 및 **종료 IP = 255.255.255.255**를 입력하여 모든 IP를 허용한 다음 **저장**을 클릭하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-154">For this tutorial, let's allow all IPs by typing in **Rule Name = AllowAllIps**, **Start IP = 0.0.0.0** and **End IP = 255.255.255.255** and then click **Save**.</span></span> <span data-ttu-id="a3f03-155">IP 범위를 적용하는 방화벽 규칙을 설정하여 네트워크에서 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-155">You can set a firewall rule that covers an IP range to be able to connect from your network.</span></span>
 
 ![PostgreSQL용 Azure Database - 방화벽 규칙 만들기](./media/tutorial-design-database-using-azure-portal/5-firewall-2.png)

4.  <span data-ttu-id="a3f03-157">**저장**을 클릭한 다음 **X**을 클릭하여 **연결 보안** 페이지를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-157">Click **Save** and then click the **X** to close the **Connections Security** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="a3f03-158">Azure PostgreSQL 서버는 5432 포트를 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-158">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="a3f03-159">회사 네트워크 내에서 연결하려는 경우 5432 포트를 통한 아웃바운드 트래픽이 네트워크 방화벽에서 허용되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-159">If you are trying to connect from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="a3f03-160">이 경우 IT 부서에서 5432 포트를 열지 않으면 Azure SQL Database 서버에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-160">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 5432.</span></span>
  >


## <a name="get-the-connection-information"></a><span data-ttu-id="a3f03-161">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="a3f03-161">Get the connection information</span></span>

<span data-ttu-id="a3f03-162">Azure Database for PostgreSQL 서버를 만들 때 기본 **postgres** 데이터베이스도 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-162">When we created our Azure Database for PostgreSQL server, the default **postgres** database also gets created.</span></span> <span data-ttu-id="a3f03-163">데이터베이스 서버에 연결하려면 호스트 정보와 액세스 자격 증명을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-163">To connect to your database server, you need to provide host information and access credentials.</span></span>

1. <span data-ttu-id="a3f03-164">Azure Portal의 왼쪽 메뉴에서 **모든 리소스**를 클릭하고 방금 만든 **mypgserver-20170401** 서버를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-164">From the left-hand menu in Azure portal, click **All resources** and search for the server you just created **mypgserver-20170401**.</span></span>

  ![<span data-ttu-id="a3f03-165">PostgreSQL용 Azure Database - 서버 검색</span><span class="sxs-lookup"><span data-stu-id="a3f03-165">Azure Database for PostgreSQL - Search for server</span></span> ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

3. <span data-ttu-id="a3f03-166">**mypgserver-20170401**서버 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-166">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="a3f03-167">서버의 **개요** 페이지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-167">Select the server's **Overview** page.</span></span> <span data-ttu-id="a3f03-168">**서버 이름** 및 **서버 관리자 로그인 이름**을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-168">Make a note of the **Server name** and **Server admin login name**.</span></span>

 ![PostgreSQL용 Azure Database - 서버 관리자 로그인](./media/tutorial-design-database-using-azure-portal/6-server-name.png)


## <a name="connect-to-postgresql-database-using-psql-in-cloud-shell"></a><span data-ttu-id="a3f03-170">Cloud Shell에서 psql을 사용하여 PostgreSQL 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="a3f03-170">Connect to PostgreSQL database using psql in Cloud Shell</span></span>

<span data-ttu-id="a3f03-171">이제 psql 명령줄 유틸리티를 사용하여 PostgreSQL용 Azure Database 서버에 연결해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-171">Let's now use the psql command-line utility to connect to the Azure Database for PostgreSQL server.</span></span> 
1. <span data-ttu-id="a3f03-172">위쪽 탐색 창의 터미널 아이콘을 통해 Azure Cloud Shell을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-172">Launch the Azure Cloud Shell via the terminal icon on the top navigation pane.</span></span>

   ![PostgreSQL용 Azure Database - Azure Cloud Shell 터미널 아이콘](./media/tutorial-design-database-using-azure-portal/7-cloud-shell.png)

2. <span data-ttu-id="a3f03-174">브라우저에서 bash 명령을 입력할 수 있는 Azure Cloud Shell이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-174">The Azure Cloud Shell opens in your browser, enabling you to type bash commands.</span></span>

   ![PostgreSQL용 Azure Database - Azure Shell Bash 프롬프트](./media/tutorial-design-database-using-azure-portal/8-bash.png)

3. <span data-ttu-id="a3f03-176">Cloud Shell 프롬프트에서 psql 명령을 사용하여 PostgreSQL용 Azure Database 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-176">At the Cloud Shell prompt, connect to your Azure Database for PostgreSQL server using the psql commands.</span></span> <span data-ttu-id="a3f03-177">다음 형식은 [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) 유틸리티를 사용하여 PostgreSQL용 Azure Database 서버에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-177">The following format is used to connect to an Azure Database for PostgreSQL server with the [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility:</span></span>
   ```bash
   psql --host=<myserver> --port=<port> --username=<server admin login> --dbname=<database name>
   ```

   <span data-ttu-id="a3f03-178">예를 들어 다음 명령은 액세스 자격 증명을 사용하여 **mypgserver-20170401.postgres.database.azure.com** PostgreSQL 서버의 **postgres**라는 기본 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-178">For example, the following command connects to the default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="a3f03-179">메시지가 표시되면 서버 관리자 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-179">Enter your server admin password when prompted.</span></span>

   ```bash
   psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
   ```

## <a name="create-a-new-database"></a><span data-ttu-id="a3f03-180">새 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="a3f03-180">Create a New Database</span></span>
<span data-ttu-id="a3f03-181">서버에 연결되면 프롬프트에서 빈 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-181">Once you're connected to the server, create a blank database at the prompt.</span></span>
```bash
CREATE DATABASE mypgsqldb;
```

<span data-ttu-id="a3f03-182">프롬프트에서 다음 명령을 실행하여 새로 만든 **mypgsqldb** 데이터베이스에 대한 연결로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-182">At the prompt, execute the following command to switch connection to the newly created database **mypgsqldb**.</span></span>
```bash
\c mypgsqldb
```
## <a name="create-tables-in-the-database"></a><span data-ttu-id="a3f03-183">데이터베이스에서 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="a3f03-183">Create tables in the database</span></span>
<span data-ttu-id="a3f03-184">이제 Azure Database for PostgreSQL에 연결하는 방법을 알았으므로 몇 가지 기본 작업을 수행하는 방법을 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-184">Now that you know how to connect to the Azure Database for PostgreSQL, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="a3f03-185">먼저 테이블을 만들고 일부 데이터와 함께 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-185">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="a3f03-186">인벤토리 정보를 추적하는 테이블을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-186">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="a3f03-187">다음과 같이 입력하면 테이블 목록에서 새로 만든 테이블을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-187">You can see the newly created table in the list of tabvles now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="a3f03-188">테이블에 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="a3f03-188">Load data into the tables</span></span>
<span data-ttu-id="a3f03-189">이제 테이블을 만들었으므로 이 테이블에 일부 데이터를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-189">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="a3f03-190">열린 명령 프롬프트 창에서 다음 쿼리를 실행하여 데이터 행을 일부 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-190">At the open command prompt window, run the following query to insert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="a3f03-191">이제 앞에서 만든 테이블에 두 개의 샘플 데이터 행이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-191">You have now two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="a3f03-192">테이블의 데이터 쿼리 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="a3f03-192">Query and update the data in the tables</span></span>
<span data-ttu-id="a3f03-193">다음 쿼리를 실행하여 데이터베이스 테이블에서 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-193">Execute the following query to retrieve information from the database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="a3f03-194">또한 테이블의 데이터를 업데이트할 수도 있습니다</span><span class="sxs-lookup"><span data-stu-id="a3f03-194">You can also update the data in the tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="a3f03-195">이에 따라 데이터를 검색할 때 해당 행이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-195">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-data-to-a-previous-point-in-time"></a><span data-ttu-id="a3f03-196">이전 시점으로 데이터 복원</span><span class="sxs-lookup"><span data-stu-id="a3f03-196">Restore data to a previous point in time</span></span>
<span data-ttu-id="a3f03-197">실수로 이 테이블을 삭제했다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-197">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="a3f03-198">이 상황은 쉽게 복구할 수 있는 것이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-198">This situation is something you cannot easily recover from.</span></span> <span data-ttu-id="a3f03-199">Azure Database for PostgreSQL를 사용하면 특정 시점(마지막 시점에서 최대 7일 전(기본) 및 35일 전(표준))으로 되돌아가 이 시점의 새 서버로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-199">Azure Database for PostgreSQL allows you to go back to any point-in-time (in the last up to 7 days (Basic) and 35 days (Standard)) and restore this point-in-time to a new server.</span></span> <span data-ttu-id="a3f03-200">이 새 서버를 사용하여 삭제된 데이터를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-200">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="a3f03-201">다음 단계에서는 테이블이 추가되기 이전 시점으로 샘플 서버를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-201">The following steps restore the sample server to a point before the table was added.</span></span>

1.  <span data-ttu-id="a3f03-202">서버에 대한 Azure Database for PostgreSQL 페이지의 도구 모음에서 **복원**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-202">On the Azure Database for PostgreSQL page for your server, click **Restore** on the toolbar.</span></span> <span data-ttu-id="a3f03-203">**복원** 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-203">The **Restore** page opens.</span></span>
  <span data-ttu-id="a3f03-204">![Azure Portal - 복원 양식 옵션](./media/tutorial-design-database-using-azure-portal/9-azure-portal-restore.png)</span><span class="sxs-lookup"><span data-stu-id="a3f03-204">![Azure portal - Restore form options](./media/tutorial-design-database-using-azure-portal/9-azure-portal-restore.png)</span></span>
2.  <span data-ttu-id="a3f03-205">필요한 정보로 **복원** 양식을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-205">Fill out the **Restore** form with the required information:</span></span>

  ![Azure Portal - 복원 양식 옵션](./media/tutorial-design-database-using-azure-portal/10-azure-portal-restore.png)
  - <span data-ttu-id="a3f03-207">**복원 지점**: 데이터베이스를 변경하기 전의 특정 시점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-207">**Restore point**: Select a point-in-time that occurs before the server was changed</span></span>
  - <span data-ttu-id="a3f03-208">**대상 서버**: 복원하려는 새 서버의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-208">**Target server**: Provide a new server name you want to restore to</span></span>
  - <span data-ttu-id="a3f03-209">**위치**: 지역은 선택할 수 없으며, 기본적으로 원본 서버와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-209">**Location**: You cannot select the region, by default it is same as the source server</span></span>
  - <span data-ttu-id="a3f03-210">**가격 책정 계층**: 이 값은 서버를 복원할 때 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-210">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="a3f03-211">원본 서버와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-211">It is same as the source server.</span></span> 
3.  <span data-ttu-id="a3f03-212">**확인**을 클릭하여 서버를 테이블 삭제 이전의 [특정 시점으로 복원](./howto-restore-server-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-212">Click **OK** to restore the server to [restore to a point-in-time](./howto-restore-server-portal.md) before the tables was deleted.</span></span> <span data-ttu-id="a3f03-213">다른 특정 시점으로 서버를 복원하는 경우 [서비스 계층](./concepts-service-tiers.md)에 대한 보존 기간 내에 있다면 중복된 새 서버를 지정한 시점의 원본 서버로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-213">Restoring a server to a different point in time creates a duplicate new server as the original server as of the point in time you specify, provided that it is within the retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3f03-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a3f03-214">Next Steps</span></span>
<span data-ttu-id="a3f03-215">이 자습서에서는 Azure Portal 및 기타 유틸리티를 사용하여 다음을 수행하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-215">In this tutorial, you learned how to use the Azure portal and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="a3f03-216">Azure Database for PostgreSQL 만들기</span><span class="sxs-lookup"><span data-stu-id="a3f03-216">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="a3f03-217">서버 방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="a3f03-217">Configure the server firewall</span></span>
> * <span data-ttu-id="a3f03-218">[**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) 유틸리티를 사용하여 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="a3f03-218">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="a3f03-219">샘플 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="a3f03-219">Load sample data</span></span>
> * <span data-ttu-id="a3f03-220">쿼리 데이터</span><span class="sxs-lookup"><span data-stu-id="a3f03-220">Query data</span></span>
> * <span data-ttu-id="a3f03-221">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="a3f03-221">Update data</span></span>
> * <span data-ttu-id="a3f03-222">데이터 복원</span><span class="sxs-lookup"><span data-stu-id="a3f03-222">Restore data</span></span>

<span data-ttu-id="a3f03-223">다음에는 Azure CLI를 사용하여 유사한 작업을 수행하는 방법에 대해 알아보고, [Azure CLI를 사용하여 첫 번째 Azure Database for PostgreSQL 디자인](tutorial-design-database-using-azure-cli.md) 자습서를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f03-223">Next, learn how to use Azure CLI to do similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using Azure CLI](tutorial-design-database-using-azure-cli.md)</span></span>
