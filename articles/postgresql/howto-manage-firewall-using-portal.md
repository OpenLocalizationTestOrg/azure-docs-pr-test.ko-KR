---
title: "aaaCreate hello Azure 포털을 사용 하 여 PostgreSQL 방화벽 규칙에 대 한 Azure 데이터베이스 관리 및 | Microsoft Docs"
description: "만들기 및 hello Azure 포털을 사용 하 여 PostgreSQL 방화벽 규칙에 대 한 Azure 데이터베이스 관리"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6a41a077168657769e442401e9df9931aa809240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-hello-azure-portal"></a><span data-ttu-id="e0794-103">만들기 및 hello Azure 포털을 사용 하 여 PostgreSQL 방화벽 규칙에 대 한 Azure 데이터베이스 관리</span><span class="sxs-lookup"><span data-stu-id="e0794-103">Create and manage Azure Database for PostgreSQL firewall rules using hello Azure portal</span></span>
<span data-ttu-id="e0794-104">서버 수준 방화벽 규칙에서 지정된 된 IP 주소 또는 IP 주소 범위 PostgreSQL 서버에 대 한 관리자 tooaccess Azure 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0794-104">Server-level firewall rules enable administrators tooaccess an Azure Database for PostgreSQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e0794-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e0794-105">Prerequisites</span></span>
<span data-ttu-id="e0794-106">이 방법 tooguide 통해 toostep를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="e0794-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="e0794-107">서버 [PostgreSQL용 Azure Database 만들기](quickstart-create-server-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="e0794-107">A server [Create an Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)</span></span>

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="e0794-108">Hello Azure 포털에에서 서버 수준 방화벽 규칙을 만들려면</span><span class="sxs-lookup"><span data-stu-id="e0794-108">Create a server-level firewall rule in hello Azure portal</span></span>
1. <span data-ttu-id="e0794-109">Hello PostgreSQL 서버 블레이드의 설정에서 머리글을 클릭 하 여 **연결 보안** tooopen hello 연결 보안 블레이드 hello Azure PostgreSQL 데이터베이스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0794-109">On hello PostgreSQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for PostgreSQL.</span></span>

  ![Azure Portal - 보안 연결 클릭](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="e0794-111">클릭 **내 IP 추가** hello 도구 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="e0794-111">Click **Add My IP** on hello toolbar.</span></span> <span data-ttu-id="e0794-112">이 규칙을 자동으로 만듭니다 hello Azure 시스템에서 인식 한 대로 컴퓨터의 hello IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0794-112">This will create a rule automatically with hello IP address of your computer, as perceived by hello Azure system.</span></span>

  ![Azure Portal - 내 IP 추가 클릭](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="e0794-114">Hello 구성 저장 하기 전에 IP 주소를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0794-114">Verify your IP address before saving hello configuration.</span></span> <span data-ttu-id="e0794-115">경우에 따라 Azure 포털을 살펴 hello IP 주소가 사용 된 hello IP 주소에서 다릅니다 때 인터넷 및 Azure 서버 hello에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0794-115">In some situations, hello IP address observed by Azure portal differs from hello IP address used when accessing hello internet and Azure servers.</span></span> <span data-ttu-id="e0794-116">따라서 toochange hello IP 시작 및 끝 IP toomake hello 규칙 함수 예상 대로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0794-116">Therefore, you may need toochange hello Start IP and End IP toomake hello rule function as expected.</span></span>
<span data-ttu-id="e0794-117">검색 엔진 또는 다른 온라인 도구 toocheck 사용자의 IP 주소 (예를 들어 Bing 검색 "란 내 IP")를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0794-117">Use a search engine or other online tool toocheck your own IP address (for example, Bing search "what is my IP").</span></span>

  ![내 IP 주소는 무엇입니까에 대한 Bing 검색](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="e0794-119">추가 주소 범위를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e0794-119">Add additional address ranges.</span></span> <span data-ttu-id="e0794-120">PostgreSQL 방화벽에 대 한 hello Azure 데이터베이스에 대 한 hello 규칙에서 단일 IP 주소 또는 주소 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0794-120">In hello rules for hello Azure Database for PostgreSQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="e0794-121">Toolimit hello 규칙 tooone 단일 IP 주소, 시작 IP 및 끝 IP 주소 hello 필드에 같게 형식 hello 하려면.</span><span class="sxs-lookup"><span data-stu-id="e0794-121">If you want toolimit hello rule tooone single IP address, type hello same address in hello field for Start IP and End IP.</span></span> <span data-ttu-id="e0794-122">Hello 방화벽을 열고 hello PostgreSQL 서버 toowhich 유효한 자격 증명을 서로에 toologin tooany 데이터베이스를 관리자와 사용자가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0794-122">Opening hello firewall enables administrators and users toologin tooany database on hello PostgreSQL server toowhich they have valid credentials.</span></span>

  ![<span data-ttu-id="e0794-123">Azure Portal - 방화벽 규칙</span><span class="sxs-lookup"><span data-stu-id="e0794-123">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. <span data-ttu-id="e0794-124">클릭 **저장** 에 hello 도구 모음 toosave이 서버 수준 방화벽 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="e0794-124">Click **Save** on hello toolbar toosave this server-level firewall rule.</span></span> <span data-ttu-id="e0794-125">Hello toohello 방화벽 규칙 업데이트 성공 했음을 hello 확인 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="e0794-125">Wait for hello confirmation that hello update toohello firewall rules was successful.</span></span>

  ![Azure Portal - 저장 클릭](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="e0794-127">Hello Azure 포털을 통해 기존 서버 수준 방화벽 규칙 관리</span><span class="sxs-lookup"><span data-stu-id="e0794-127">Manage existing server-level firewall rules through hello Azure portal</span></span>
<span data-ttu-id="e0794-128">Hello 단계 toomanage hello 방화벽 규칙을 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0794-128">Repeat hello steps toomanage hello firewall rules.</span></span>
* <span data-ttu-id="e0794-129">tooadd hello 현재 컴퓨터를 너무 hello 단추를 클릭 + **내 IP 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e0794-129">tooadd hello current computer, click hello button too+ **Add My IP**.</span></span> <span data-ttu-id="e0794-130">클릭 **저장** toosave hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0794-130">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="e0794-131">규칙 이름, 시작 IP 주소 및 끝 IP 주소에 hello tooadd 추가 IP 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0794-131">tooadd additional IP addresses, type in hello Rule Name, Start IP Address, and End IP Address.</span></span> <span data-ttu-id="e0794-132">클릭 **저장** toosave hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0794-132">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="e0794-133">기존 규칙을 toomodify hello 규칙의 hello 필드 중 하나를 클릭 하 고 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0794-133">toomodify an existing rule, click any of hello fields in hello rule and modify.</span></span> <span data-ttu-id="e0794-134">클릭 **저장** toosave hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0794-134">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="e0794-135">toodelete 기존 규칙을 hello 줄임표 [...]를 클릭 하 고 제거 hello 규칙 삭제를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0794-135">toodelete an existing rule, click hello ellipsis […] and click Delete remove hello rule.</span></span> <span data-ttu-id="e0794-136">클릭 **저장** toosave hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0794-136">Click **Save** toosave hello changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0794-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e0794-137">Next steps</span></span>
- <span data-ttu-id="e0794-138">마찬가지로, 스크립팅할 수 있습니다 너무[만들기 및 Azure CLI를 사용 하 여 PostgreSQL 방화벽 규칙에 대 한 Azure 데이터베이스 관리](howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="e0794-138">Similarly, you can script too[Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md)</span></span>
- <span data-ttu-id="e0794-139">PostgreSQL 서버에 대 한 tooan Azure 데이터베이스 연결에 대 한 도움말을 참조 하십시오. [PostgreSQL에 대 한 Azure 데이터베이스에 대 한 연결 라이브러리](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="e0794-139">For help in connecting tooan Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
