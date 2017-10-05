---
title: "기존 Azure App Service를 Azure Database for MySQL에 연결 | Microsoft Docs"
description: "기존 Azure App Service를 Azure Database for MySQL에 적절하게 연결하는 방법에 대한 지침"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 735e21e8135d67405ec6b88d75be1711a2f071f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-an-existing-azure-app-service-to-azure-database-for-mysql-server"></a><span data-ttu-id="c9c90-103">기존 Azure App Service를 Azure Database for MySQL 서버에 연결</span><span class="sxs-lookup"><span data-stu-id="c9c90-103">Connect an existing Azure App Service to Azure Database for MySQL server</span></span>
<span data-ttu-id="c9c90-104">이 문서에서는 기존 Azure App Service를 Azure Database for MySQL 서버에 연결하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c9c90-104">This document explains how to connect an existing Azure App Service to your Azure Database for MySQL server.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c9c90-105">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="c9c90-105">Before you begin</span></span>
<span data-ttu-id="c9c90-106">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c9c90-106">Log in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c9c90-107">Azure Database for MySQL 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9c90-107">Create an Azure Database for MySQL server.</span></span> <span data-ttu-id="c9c90-108">자세한 내용은 [포털에서 Azure Database for MySQL 서버 만들기](quickstart-create-mysql-server-database-using-azure-portal.md) 또는 [CLI를 사용하여 Azure Database for MySQL 서버 만들기](quickstart-create-mysql-server-database-using-azure-cli.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9c90-108">For details, refer to [How to create Azure Database for MySQL server from Portal](quickstart-create-mysql-server-database-using-azure-portal.md) or [How to create Azure Database for MySQL server using CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span></span>

<span data-ttu-id="c9c90-109">현재 Azure App Service에서 Azure Database for MySQL로의 액세스를 가능하게 하는 두 가지 솔루션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9c90-109">Currently there are two solutions to enable access from an Azure App Service to an Azure Database for MySQL.</span></span> <span data-ttu-id="c9c90-110">두 솔루션 모두 서버 수준 방화벽 규칙 설정 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9c90-110">Both solutions involve setting up server-level firewall rules.</span></span>

## <a name="solution-1---create-a-firewall-rule-to-allow-all-ips"></a><span data-ttu-id="c9c90-111">솔루션 1 - 모든 IP를 허용하는 방화벽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="c9c90-111">Solution 1 - Create a firewall rule to allow all IPs</span></span>
<span data-ttu-id="c9c90-112">Azure Database for MySQL은 데이터를 보호하는 방화벽을 사용하여 액세스 보안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c9c90-112">Azure Database for MySQL provides access security using a firewall to protect your data.</span></span> <span data-ttu-id="c9c90-113">Azure App Service에서 Azure Database for MySQL 서버로 연결할 때 App Service의 아웃바운드 IP는 기본적으로 동적이라는 것을 염두에 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9c90-113">When connecting from an Azure App Service to Azure Database for MySQL server, keep in mind that the outbound IPs of App Service are dynamic in nature.</span></span> 

<span data-ttu-id="c9c90-114">Azure App Service의 가용성을 보장하려면 이 솔루션을 사용하여 모든 IP를 허용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c9c90-114">To ensure the availability of your Azure App Service, we recommend using this solution to allow ALL IPs.</span></span>

> [!NOTE]
> <span data-ttu-id="c9c90-115">Azure 서비스에 대한 모든 IP에서 Azure Database for MySQL에 연결하는 것을 방지하기 위해 현재 Microsoft는 장기 솔루션을 개발 중입니다.</span><span class="sxs-lookup"><span data-stu-id="c9c90-115">Microsoft is working for a long-term solution to avoid allowing all IPs for Azure services to connect to Azure Database for MySQL.</span></span>

1. <span data-ttu-id="c9c90-116">MySQL 서버 블레이드의 설정 머리글에서 **연결 보안**을 클릭하여 MySQL용 Azure Database에 대한 연결 보안 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c9c90-116">On the MySQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for MySQL.</span></span>

   ![Azure Portal - 보안 연결 클릭](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="c9c90-118">**규칙 이름**, **시작 IP** 및 **종료 IP**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c9c90-118">Enter **RULE NAME**, **START IP**, and **END IP**.</span></span> <span data-ttu-id="c9c90-119">그런 다음 **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9c90-119">Then click **Save**.</span></span>
   - <span data-ttu-id="c9c90-120">규칙 이름: 모든-IP-허용</span><span class="sxs-lookup"><span data-stu-id="c9c90-120">Rule name: Allow-All-IPs</span></span>
   - <span data-ttu-id="c9c90-121">시작 IP: 0.0.0.0</span><span class="sxs-lookup"><span data-stu-id="c9c90-121">Start IP: 0.0.0.0</span></span>
   - <span data-ttu-id="c9c90-122">종료 IP: 255.255.255.255</span><span class="sxs-lookup"><span data-stu-id="c9c90-122">End IP: 255.255.255.255</span></span>

   ![Azure Portal - 모든 IP 추가](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-to-explicitly-allow-outbound-ips"></a><span data-ttu-id="c9c90-124">솔루션 2 - 아웃바운드 IP를 명시적으로 허용하는 방화벽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="c9c90-124">Solution 2 - Create a firewall rule to explicitly allow outbound IPs</span></span>
<span data-ttu-id="c9c90-125">Azure App Service의 모든 아웃바운드 IP를 명시적으로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9c90-125">You can explicitly add all the outbound IPs of your Azure App Service.</span></span>

1. <span data-ttu-id="c9c90-126">App Service 속성 블레이드에서 **아웃바운드 IP 주소**를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c9c90-126">On the App Service Properties blade, view your **OUTBOUND IP ADDRESS**.</span></span>

   ![Azure Portal - 아웃바운드 IP 확인](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. <span data-ttu-id="c9c90-128">MySQL 연결 보안 블레이드에서 아웃바운드 IP를 하나씩 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9c90-128">On the MySQL Connection security blade, add outbound IPs one by one.</span></span>

   ![Azure Portal - 명시적 IP 추가](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. <span data-ttu-id="c9c90-130">잊지 말고 방화벽 규칙을 **저장**하세요.</span><span class="sxs-lookup"><span data-stu-id="c9c90-130">Remember to **Save** your firewall rules.</span></span>

<span data-ttu-id="c9c90-131">Azure App Service에서는 시간이 지나도 IP 주소를 동일하게 유지하려고 하지만 경우에 따라 IP 주소가 변경될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9c90-131">Though the Azure App service attempts to keep IP addresses constant over time, there are cases where the IP addresses may change.</span></span> <span data-ttu-id="c9c90-132">수용작업량을 늘리기 위해 앱 재활용 또는 크기 조정 작업이 발생하거나 Azure 지역 데이터 센터에 새 컴퓨터가 추가되는 경우를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9c90-132">For example, when the app recycles or a scale operation occurs, or when new machines are added in Azure regional data centers to increase the capacity.</span></span> <span data-ttu-id="c9c90-133">IP 주소가 변경되면 앱에서 더 이상 MySQL 서버에 연결할 수 없는 경우 가동 중지가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9c90-133">When the IP addresses change, the app could experience downtime in the event it can no longer connect to the MySQL server.</span></span> <span data-ttu-id="c9c90-134">이전 솔루션 중 하나를 선택할 때 이러한 가능성을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9c90-134">Consider this potential when choosing one of the preceding solutions.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="c9c90-135">SSL 구성</span><span class="sxs-lookup"><span data-stu-id="c9c90-135">SSL configuration</span></span>
<span data-ttu-id="c9c90-136">Azure Database for MySQL은 기본적으로 SSL을 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9c90-136">Azure Database for MySQL has SSL Enabled by default.</span></span> <span data-ttu-id="c9c90-137">응용 프로그램에서 데이터베이스에 연결할 때 SSL을 사용하지 않는 경우 MySQL 서버에서 SSL을 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9c90-137">If your application is not using SSL to connect to the database, then you need to disable SSL on MySQL server.</span></span> <span data-ttu-id="c9c90-138">SSL을 구성하는 방법에 대한 자세한 내용은 [Azure Database for MySQL에 SSL 사용](howto-configure-ssl.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9c90-138">For details on how to configure SSL, See [Using SSL with Azure Database for MySQL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9c90-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c9c90-139">Next steps</span></span>
<span data-ttu-id="c9c90-140">연결 문자열에 대한 자세한 내용은 [연결 문자열](howto-connection-string.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9c90-140">For more information about connection strings, refer to [Connection Strings](howto-connection-string.md).</span></span>
