---
title: "aaaConnect 기존 Azure 앱 서비스 tooAzure MySQL에 대 한 데이터베이스 | Microsoft Docs"
description: "Tooproperly MySQL에 대 한 기존 Azure 앱 서비스 tooAzure 데이터베이스에 연결 하는 방법에 대 한 지침"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 6d5b16f316e186d665370adcd8b7c7bb38c8d51a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-an-existing-azure-app-service-tooazure-database-for-mysql-server"></a><span data-ttu-id="b9868-103">MySQL 서버는 기존 Azure 앱 서비스 tooAzure 데이터베이스 연결</span><span class="sxs-lookup"><span data-stu-id="b9868-103">Connect an existing Azure App Service tooAzure Database for MySQL server</span></span>
<span data-ttu-id="b9868-104">이 문서에서는 설명 MySQL server에 대 한 기존 Azure 앱 서비스 tooyour tooconnect Azure 데이터베이스 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b9868-104">This document explains how tooconnect an existing Azure App Service tooyour Azure Database for MySQL server.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b9868-105">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="b9868-105">Before you begin</span></span>
<span data-ttu-id="b9868-106">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9868-106">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b9868-107">Azure Database for MySQL 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9868-107">Create an Azure Database for MySQL server.</span></span> <span data-ttu-id="b9868-108">자세한 내용은 참조 너무[toocreate Azure 포털에서 MySQL 서버에 대 한 데이터베이스 방법](quickstart-create-mysql-server-database-using-azure-portal.md) 또는 [toocreate Azure CLI를 사용 하 여 MySQL server에 대 한 데이터베이스 방법](quickstart-create-mysql-server-database-using-azure-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9868-108">For details, refer too[How toocreate Azure Database for MySQL server from Portal](quickstart-create-mysql-server-database-using-azure-portal.md) or [How toocreate Azure Database for MySQL server using CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span></span>

<span data-ttu-id="b9868-109">현재 MySQL에 대 한 Azure 앱 서비스 tooan Azure 데이터베이스에서에서 두 개의 솔루션 tooenable 액세스는.</span><span class="sxs-lookup"><span data-stu-id="b9868-109">Currently there are two solutions tooenable access from an Azure App Service tooan Azure Database for MySQL.</span></span> <span data-ttu-id="b9868-110">두 솔루션 모두 서버 수준 방화벽 규칙 설정 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9868-110">Both solutions involve setting up server-level firewall rules.</span></span>

## <a name="solution-1---create-a-firewall-rule-tooallow-all-ips"></a><span data-ttu-id="b9868-111">해결 방법 1-방화벽 규칙 tooallow를 모든 Ip 만들기</span><span class="sxs-lookup"><span data-stu-id="b9868-111">Solution 1 - Create a firewall rule tooallow all IPs</span></span>
<span data-ttu-id="b9868-112">MySQL에 대 한 azure 데이터베이스 사용 하 여 방화벽 tooprotect 데이터 액세스 보안을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9868-112">Azure Database for MySQL provides access security using a firewall tooprotect your data.</span></span> <span data-ttu-id="b9868-113">MySQL server에 대 한 Azure 앱 서비스 tooAzure 데이터베이스에서에서 연결 염두에서에 둬야 해당 hello 아웃 바운드 응용 프로그램 서비스의 Ip 특성상 동적 이므로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9868-113">When connecting from an Azure App Service tooAzure Database for MySQL server, keep in mind that hello outbound IPs of App Service are dynamic in nature.</span></span> 

<span data-ttu-id="b9868-114">Azure 앱 서비스의 tooensure hello 가용성,이 솔루션 tooallow 모든 Ip를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b9868-114">tooensure hello availability of your Azure App Service, we recommend using this solution tooallow ALL IPs.</span></span>

> [!NOTE]
> <span data-ttu-id="b9868-115">Microsoft Azure 서비스 tooconnect tooAzure 데이터베이스에 대 한 모든 Ip MySQL에 대 한 허용 장기 솔루션 tooavoid에 대 한 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9868-115">Microsoft is working for a long-term solution tooavoid allowing all IPs for Azure services tooconnect tooAzure Database for MySQL.</span></span>

1. <span data-ttu-id="b9868-116">Hello MySQL 서버 블레이드의 설정에서 머리글을 클릭 하 여 **연결 보안** tooopen hello 연결 보안 블레이드 hello MySQL에 대 한 Azure 데이터베이스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9868-116">On hello MySQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for MySQL.</span></span>

   ![Azure Portal - 보안 연결 클릭](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="b9868-118">**규칙 이름**, **시작 IP** 및 **종료 IP**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b9868-118">Enter **RULE NAME**, **START IP**, and **END IP**.</span></span> <span data-ttu-id="b9868-119">그런 다음 **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9868-119">Then click **Save**.</span></span>
   - <span data-ttu-id="b9868-120">규칙 이름: 모든-IP-허용</span><span class="sxs-lookup"><span data-stu-id="b9868-120">Rule name: Allow-All-IPs</span></span>
   - <span data-ttu-id="b9868-121">시작 IP: 0.0.0.0</span><span class="sxs-lookup"><span data-stu-id="b9868-121">Start IP: 0.0.0.0</span></span>
   - <span data-ttu-id="b9868-122">종료 IP: 255.255.255.255</span><span class="sxs-lookup"><span data-stu-id="b9868-122">End IP: 255.255.255.255</span></span>

   ![Azure Portal - 모든 IP 추가](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-tooexplicitly-allow-outbound-ips"></a><span data-ttu-id="b9868-124">솔루션 2-만들 방화벽 규칙 tooexplicitly 아웃 바운드 Ip 허용</span><span class="sxs-lookup"><span data-stu-id="b9868-124">Solution 2 - Create a firewall rule tooexplicitly allow outbound IPs</span></span>
<span data-ttu-id="b9868-125">Azure 앱 서비스의 아웃 바운드 Ip hello 모두 명시적으로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9868-125">You can explicitly add all hello outbound IPs of your Azure App Service.</span></span>

1. <span data-ttu-id="b9868-126">Hello 응용 프로그램 서비스 속성 블레이드를 보려면 사용자 **아웃 바운드 IP 주소**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9868-126">On hello App Service Properties blade, view your **OUTBOUND IP ADDRESS**.</span></span>

   ![Azure Portal - 아웃바운드 IP 확인](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. <span data-ttu-id="b9868-128">Hello MySQL 연결 보안 블레이드에서 아웃 바운드 Ip 개별적으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9868-128">On hello MySQL Connection security blade, add outbound IPs one by one.</span></span>

   ![Azure Portal - 명시적 IP 추가](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. <span data-ttu-id="b9868-130">너무 기억**저장** 방화벽 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="b9868-130">Remember too**Save** your firewall rules.</span></span>

<span data-ttu-id="b9868-131">Hello Azure 앱 서비스 시간에 따른 tookeep IP 주소 상수 시도 하지만 hello IP 주소가 변경 될 수 있습니다 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9868-131">Though hello Azure App service attempts tookeep IP addresses constant over time, there are cases where hello IP addresses may change.</span></span> <span data-ttu-id="b9868-132">예를 들어 응용 프로그램 재활용 때 hello 또는 배율 작업이 발생 하거나 tooincrease hello 용량에 중점을 지역 데이터를 Azure에서 새 컴퓨터가 추가 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="b9868-132">For example, when hello app recycles or a scale operation occurs, or when new machines are added in Azure regional data centers tooincrease hello capacity.</span></span> <span data-ttu-id="b9868-133">Hello IP 주소를 변경, hello 앱에서 더 이상 연결할 수는 hello 이벤트 가동 중지 시간 발생할 수 toohello MySQL 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="b9868-133">When hello IP addresses change, hello app could experience downtime in hello event it can no longer connect toohello MySQL server.</span></span> <span data-ttu-id="b9868-134">Hello 앞에 솔루션 중 하나를 선택 하는 경우이 가능성을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9868-134">Consider this potential when choosing one of hello preceding solutions.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="b9868-135">SSL 구성</span><span class="sxs-lookup"><span data-stu-id="b9868-135">SSL configuration</span></span>
<span data-ttu-id="b9868-136">Azure Database for MySQL은 기본적으로 SSL을 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9868-136">Azure Database for MySQL has SSL Enabled by default.</span></span> <span data-ttu-id="b9868-137">응용 프로그램에서 SSL tooconnect toohello 데이터베이스를 사용 하지 않으므로 MySQL 서버에서 SSL toodisable를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9868-137">If your application is not using SSL tooconnect toohello database, then you need toodisable SSL on MySQL server.</span></span> <span data-ttu-id="b9868-138">방법에 대 한 자세한 내용은 tooconfigure SSL, 참조 [MySQL에 대 한 Azure 데이터베이스를 사용 하 여 SSL](howto-configure-ssl.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9868-138">For details on how tooconfigure SSL, See [Using SSL with Azure Database for MySQL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9868-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b9868-139">Next steps</span></span>
<span data-ttu-id="b9868-140">연결 문자열에 대 한 자세한 내용은 참조 너무[연결 문자열](howto-connection-string.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9868-140">For more information about connection strings, refer too[Connection Strings](howto-connection-string.md).</span></span>
