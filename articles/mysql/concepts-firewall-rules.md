---
title: "MySQL용 Azure 데이터베이스 서버 방화벽 규칙 | Microsoft Docs"
description: "MySQL용 Azure데이터베이스 서버의 방화벽 규칙에 대해 설명합니다."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 7456cef7a5da665ee3d70df64265b8186a79f9b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-database-for-mysql-server-firewall-rules"></a><span data-ttu-id="c4e97-103">MySQL용 Azure 데이터베이스 서버 방화벽 규칙</span><span class="sxs-lookup"><span data-stu-id="c4e97-103">Azure Database for MySQL server firewall rules</span></span>
<span data-ttu-id="c4e97-104">방화벽은 권한이 있는 컴퓨터를 지정할 때까지 데이터베이스 서버에 대한 모든 액세스를 금지합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e97-104">Firewalls prevent all access to your database server until you specify which computers have permission.</span></span> <span data-ttu-id="c4e97-105">방화벽은 각 요청이 시작된 IP 주소의 서버에 대한 액세스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e97-105">The firewall grants access to the server based on the originating IP address of each request.</span></span>

<span data-ttu-id="c4e97-106">방화벽을 구성하려면 허용 가능한 IP 주소 범위를 지정하는 방화벽 규칙을 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e97-106">To configure your firewall, you create firewall rules that specify ranges of acceptable IP addresses.</span></span> <span data-ttu-id="c4e97-107">서버 수준의 방화벽 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e97-107">You can create firewall rules at the server level.</span></span>

<span data-ttu-id="c4e97-108">**방화벽 규칙:** 이 규칙은 모든 MySQL용 Azure 데이터베이스 서버, 즉, 동일한 논리 서버 내의 모든 데이터베이스에 클라이언트가 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e97-108">**Firewall rules:** These rules enable clients to access your entire Azure Database for MySQL server, that is, all the databases within the same logical server.</span></span> <span data-ttu-id="c4e97-109">Azure Portal 또는 Azure CLI 명령을 사용하여 서버 수준 방화벽 규칙을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e97-109">Server-level firewall rules can be configured by using the Azure portal or using Azure CLI commands.</span></span> <span data-ttu-id="c4e97-110">서버 수준 방화벽 규칙을 만들려면 구독 소유자 또는 구독 참가자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e97-110">To create server-level firewall rules, you must be the subscription owner or a subscription contributor.</span></span>

## <a name="firewall-overview"></a><span data-ttu-id="c4e97-111">방화벽 개요</span><span class="sxs-lookup"><span data-stu-id="c4e97-111">Firewall overview</span></span>
<span data-ttu-id="c4e97-112">MySQL용 Azure 데이터베이스 서버에 대한 모든 데이터베이스 액세스는 기본적으로 방화벽에 의해 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e97-112">All database access to your Azure Database for MySQL server is blocked by the firewall by default.</span></span> <span data-ttu-id="c4e97-113">다른 컴퓨터에서 서버를 사용하려면 해당 서버에 대한 액세스를 허용하는 하나 이상의 서버 수준 방화벽 규칙을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e97-113">To begin using your server from another computer, you need to specify one or more server-level firewall rules to enable access to your server.</span></span> <span data-ttu-id="c4e97-114">방화벽 규칙을 사용하여 허용할 인터넷에서의 IP 주소 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e97-114">Use the firewall rules to specify which IP address ranges from the Internet to allow.</span></span> <span data-ttu-id="c4e97-115">Azure Portal 웹 사이트 자체에 대한 액세스는 이 방화벽 규칙의 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e97-115">Access to the Azure portal website itself is not impacted by the firewall rules.</span></span>

<span data-ttu-id="c4e97-116">인터넷과 Azure로부터의 연결 시도는 다음 다이어그램과 같이 MySQL용 Azure 데이터베이스에 연결하기 전에 먼저 방화벽을 통과해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e97-116">Connection attempts from the Internet and Azure must first pass through the firewall before they can reach your Azure Database for MySQL database, as shown in the following diagram:</span></span>

![방화벽 작동 방식을 보여 주는 예제 흐름](./media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-the-internet"></a><span data-ttu-id="c4e97-118">인터넷에서 연결하기</span><span class="sxs-lookup"><span data-stu-id="c4e97-118">Connecting from the Internet</span></span>
<span data-ttu-id="c4e97-119">서버 수준 방화벽 규칙은 MySQL용 Azure 데이터베이스 서버의 모든 데이터베이스에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e97-119">Server-level firewall rules apply to all databases on the Azure Database for MySQL server.</span></span>

<span data-ttu-id="c4e97-120">요청된 IP 주소가 서버 수준 방화벽 규칙의 지정된 범위 안에 있을 경우, 연결이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e97-120">If the IP address of the request is within one of the ranges specified in the server-level firewall rules, the connection is granted.</span></span>

<span data-ttu-id="c4e97-121">요청 IP 주소가 데이터베이스 수준 또는 서버 수준 방화벽 규칙의 지정된 범위 안에 없을 경우, 연결 요청이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e97-121">If the IP address of the request is not within the ranges specified in any of the database-level or server-level firewall rules, the connection request fails.</span></span>

## <a name="programmatically-managing-firewall-rules"></a><span data-ttu-id="c4e97-122">방화벽 규칙을 프로그래밍 방식으로 관리</span><span class="sxs-lookup"><span data-stu-id="c4e97-122">Programmatically managing firewall rules</span></span>
<span data-ttu-id="c4e97-123">Azure Portal 외에도 Azure CLI를 사용하여 방화벽 규칙을 프로그래밍 방식으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e97-123">In addition to the Azure portal, firewall rules can be managed programmatically using Azure CLI.</span></span> <span data-ttu-id="c4e97-124">[Azure CLI를 사용한 MySQL용 Azure 데이터베이스 방화벽 규칙 만들기 및 관리](./howto-manage-firewall-using-cli.md)도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4e97-124">See also [Create and manage Azure Database for MySQL firewall rules using Azure CLI](./howto-manage-firewall-using-cli.md)</span></span>

## <a name="troubleshooting-the-database-firewall"></a><span data-ttu-id="c4e97-125">데이터베이스 방화벽 문제 해결</span><span class="sxs-lookup"><span data-stu-id="c4e97-125">Troubleshooting the database firewall</span></span>
<span data-ttu-id="c4e97-126">MySQL용 Microsoft Azure 데이터베이스 서버 서비스로의 연결이 예상대로 작동되지 않는 경우 다음 사항을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="c4e97-126">Consider the following points when access to the Microsoft Azure Database for MySQL server service does not behave as you expect:</span></span>

* <span data-ttu-id="c4e97-127">**허용 목록의 변경사항이 아직 적용되지 않았습니다.** MySQL용 Azure 데이터베이스 서버 방화벽 구성에 변경 내용이 적용되려면 최대 5분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e97-127">**Changes to the allow list have not taken effect yet:** There may be as much as a five-minute delay for changes to the Azure Database for MySQL Server firewall configuration to take effect.</span></span>

* <span data-ttu-id="c4e97-128">**로그인이 올바르지 않거나 암호가 올바르지 않습니다.** 로그인에 MySQL용 Azure 데이터베이스 서버에 대한 권한이 없거나 사용한 암호가 틀렸을 경우 MySQL용 Azure 데이터베이스 서버에 대한 연결이 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e97-128">**The login is not authorized or an incorrect password was used:** If a login does not have permissions on the Azure Database for MySQL server or the password used is incorrect, the connection to the Azure Database for MySQL server is denied.</span></span> <span data-ttu-id="c4e97-129">방화벽 설정은 클라이언트에게 서버에 연결을 시도할 수 있는 기회를 제공합니다. 각 클라이언트는 꼭 필요한 보안 자격 증명을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e97-129">Creating a firewall setting only provides clients with an opportunity to attempt connecting to your server; each client must provide the necessary security credentials.</span></span>

* <span data-ttu-id="c4e97-130">**동적 IP 주소:** 동적 IP 주소를 통해 인터넷에 연결되어 있고 방화벽을 통과하는 데 문제가 있는 경우 다음 해결 방법 중 하나를 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e97-130">**Dynamic IP address:** If you have an Internet connection with dynamic IP addressing and you are having trouble getting through the firewall, you could try one of the following solutions:</span></span>

* <span data-ttu-id="c4e97-131">ISP(인터넷 서비스 공급자)는 MySQL용 Azure 데이터베이스 서버에 연결될 클라이언트에 할당된 IP 주소 범위를 요청하고, 방화벽 규칙에 따라 IP 주소 범위를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e97-131">Ask your Internet Service Provider (ISP) for the IP address range assigned to your client computers that access the Azure Database for MySQL server, and then add the IP address range as a firewall rule.</span></span>

* <span data-ttu-id="c4e97-132">클라이언트 컴퓨터 대신 고정 IP 주소를 얻고, 방화벽 규칙에 따라 IP 주소 범위를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e97-132">Get static IP addressing instead for your client computers, and then add the IP addresses as firewall rules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4e97-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c4e97-133">Next steps</span></span>

<span data-ttu-id="c4e97-134">[Azure Portal을 사용한 MySQL용 Azure 데이터베이스 방화벽 규칙 만들기 및 관리](./howto-manage-firewall-using-portal.md)
[Azure CLI를 사용한 MySQL용 Azure 데이터베이스 방화벽 규칙 만들기 및 관리](./howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="c4e97-134">[Create and manage Azure Database for MySQL firewall rules using the Azure portal](./howto-manage-firewall-using-portal.md)
[Create and manage Azure Database for MySQL firewall rules using Azure CLI](./howto-manage-firewall-using-cli.md)</span></span>
