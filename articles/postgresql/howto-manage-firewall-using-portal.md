---
title: "Azure Portal을 사용한 PostgreSQL용 Azure Database 방화벽 규칙 만들기 및 관리 | Microsoft Docs"
description: "Azure Portal을 사용한 PostgreSQL용 Azure Database 방화벽 규칙 만들기 및 관리"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 20ac1392949a6f604e68d984cb50273b61051037
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-the-azure-portal"></a><span data-ttu-id="f2ec8-103">Azure Portal을 사용한 PostgreSQL용 Azure Database 방화벽 규칙 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="f2ec8-103">Create and manage Azure Database for PostgreSQL firewall rules using the Azure portal</span></span>
<span data-ttu-id="f2ec8-104">관리자는 서버 수준 방화벽 규칙을 사용하여 특정 IP 주소 또는 IP 주소 범위에서 PostgreSQL용 Azure Database 서버에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-104">Server-level firewall rules enable administrators to access an Azure Database for PostgreSQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f2ec8-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f2ec8-105">Prerequisites</span></span>
<span data-ttu-id="f2ec8-106">이 방법 가이드를 단계별로 실행하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-106">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="f2ec8-107">서버 [PostgreSQL용 Azure Database 만들기](quickstart-create-server-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f2ec8-107">A server [Create an Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)</span></span>

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="f2ec8-108">Azure Portal에서 서버 수준 방화벽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="f2ec8-108">Create a server-level firewall rule in the Azure portal</span></span>
1. <span data-ttu-id="f2ec8-109">PostgreSQL 서버 블레이드의 설정 머리글에서 **연결 보안**을 클릭하여 PostgreSQL용 Azure Database에 대한 연결 보안 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-109">On the PostgreSQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for PostgreSQL.</span></span>

  ![Azure Portal - 보안 연결 클릭](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="f2ec8-111">도구 모음에서 **내 IP 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-111">Click **Add My IP** on the toolbar.</span></span> <span data-ttu-id="f2ec8-112">그러면 Azure 시스템에서 감지하여 사용자 컴퓨터의 IP 주소를 사용하는 규칙이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-112">This will create a rule automatically with the IP address of your computer, as perceived by the Azure system.</span></span>

  ![Azure Portal - 내 IP 추가 클릭](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="f2ec8-114">구성을 저장하기 전에 사용자의 IP 주소를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-114">Verify your IP address before saving the configuration.</span></span> <span data-ttu-id="f2ec8-115">상황에 따라 Azure Portal에서 관찰하는 IP 주소는 인터넷 및 Azure 서버에 액세스할 때 사용된 IP 주소와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-115">In some situations, the IP address observed by Azure portal differs from the IP address used when accessing the internet and Azure servers.</span></span> <span data-ttu-id="f2ec8-116">따라서, 규칙 함수를 예상대로 만들기 위해 시작 IP 및 끝 IP를 변경해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-116">Therefore, you may need to change the Start IP and End IP to make the rule function as expected.</span></span>
<span data-ttu-id="f2ec8-117">검색 엔진 또는 기타 온라인 도구를 사용하여 사용자 고유의 IP 주소를 확인합니다(예를 들어, "내 IP 주소는 무엇입니까" Bing 검색).</span><span class="sxs-lookup"><span data-stu-id="f2ec8-117">Use a search engine or other online tool to check your own IP address (for example, Bing search "what is my IP").</span></span>

  ![내 IP 주소는 무엇입니까에 대한 Bing 검색](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="f2ec8-119">추가 주소 범위를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-119">Add additional address ranges.</span></span> <span data-ttu-id="f2ec8-120">PostgreSQL용 Azure Database 방화벽에 대한 규칙에서 단일 IP 주소 또는 주소 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-120">In the rules for the Azure Database for PostgreSQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="f2ec8-121">하나의 단일 IP 주소에 규칙을 제한하려는 경우 시작 IP 및 끝 IP에 대한 필드에 동일한 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-121">If you want to limit the rule to one single IP address, type the same address in the field for Start IP and End IP.</span></span> <span data-ttu-id="f2ec8-122">방화벽을 열면 관리자와 사용자가 유효한 자격 증명이 있는 PostgreSQL 서버의 데이터베이스에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-122">Opening the firewall enables administrators and users to login to any database on the PostgreSQL server to which they have valid credentials.</span></span>

  ![<span data-ttu-id="f2ec8-123">Azure Portal - 방화벽 규칙</span><span class="sxs-lookup"><span data-stu-id="f2ec8-123">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. <span data-ttu-id="f2ec8-124">도구 모음에서 **저장**을 클릭하여 이 서버 수준 방화벽 규칙을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-124">Click **Save** on the toolbar to save this server-level firewall rule.</span></span> <span data-ttu-id="f2ec8-125">방화벽 규칙에 대한 업데이트가 성공적으로 수행되었는지 확인될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-125">Wait for the confirmation that the update to the firewall rules was successful.</span></span>

  ![Azure Portal - 저장 클릭](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="f2ec8-127">Azure 포털을 통해 기존 서버 수준 방화벽 규칙 관리</span><span class="sxs-lookup"><span data-stu-id="f2ec8-127">Manage existing server-level firewall rules through the Azure portal</span></span>
<span data-ttu-id="f2ec8-128">방화벽 규칙을 관리하는 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-128">Repeat the steps to manage the firewall rules.</span></span>
* <span data-ttu-id="f2ec8-129">현재 컴퓨터를 추가하려면 **+ 내 IP 추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-129">To add the current computer, click the button to + **Add My IP**.</span></span> <span data-ttu-id="f2ec8-130">**저장** 을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-130">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="f2ec8-131">추가 IP 주소를 추가 하려면 규칙 이름, 시작 IP 주소 및 끝 IP 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-131">To add additional IP addresses, type in the Rule Name, Start IP Address, and End IP Address.</span></span> <span data-ttu-id="f2ec8-132">**저장** 을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-132">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="f2ec8-133">기존 규칙을 수정 하려면 규칙의 필드 중 하나를 클릭 후 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-133">To modify an existing rule, click any of the fields in the rule and modify.</span></span> <span data-ttu-id="f2ec8-134">**저장** 을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-134">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="f2ec8-135">기존 규칙을 삭제하려면 줄임표 [...]를 클릭하고 삭제를 클릭하여 규칙을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-135">To delete an existing rule, click the ellipsis […] and click Delete remove the rule.</span></span> <span data-ttu-id="f2ec8-136">**저장**을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-136">Click **Save** to save the changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2ec8-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f2ec8-137">Next steps</span></span>
- <span data-ttu-id="f2ec8-138">마찬가지로 [Azure CLI를 사용한 PostgreSQL용 Azure Database 방화벽 규칙 만들기 및 관리](howto-manage-firewall-using-cli.md)를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-138">Similarly, you can script to [Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md)</span></span>
- <span data-ttu-id="f2ec8-139">PostgreSQL용 Azure Database 서버 연결에 대한 도움말은 [PostgreSQL용 Azure Database에 대한 연결 라이브러리](concepts-connection-libraries.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2ec8-139">For help in connecting to an Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
