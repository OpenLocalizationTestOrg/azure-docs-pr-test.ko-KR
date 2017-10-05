---
title: "MySQL용 Azure Database에서 서버를 복원하는 방법 | Microsoft Docs"
description: "이 문서에서는 Azure Portal을 사용하여 MySQL용 Azure Database에서 서버를 복원하는 방법을 설명합니다."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 8c06dce534b628a602127fd02b152c8e04e02cc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-mysql-using-the-azure-portal"></a><span data-ttu-id="41d47-103">Azure Portal을 사용하여 MySQL용 Azure Database에서 서버를 백업 및 복원하는 방법</span><span class="sxs-lookup"><span data-stu-id="41d47-103">How To Backup and Restore a server in Azure Database for MySQL using the Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="41d47-104">자동으로 수행되는 백업</span><span class="sxs-lookup"><span data-stu-id="41d47-104">Backup happens Automatically</span></span>
<span data-ttu-id="41d47-105">MySQL용 Azure Database를 사용할 경우 데이터베이스 서비스가 자동으로 5분마다 서비스 백업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="41d47-105">When using Azure Database for MySQL, the database service automatically makes a backup of the service every 5 minutes.</span></span> 

<span data-ttu-id="41d47-106">백업은 기본 계층을 사용하는 경우 7일, 표준 계층을 사용하는 경우 35일 동안 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41d47-106">The backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="41d47-107">자세한 내용은 [MySQL용 Azure Database 서비스 계층](concepts-service-tiers.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41d47-107">For more information, see [Azure Database for MySQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="41d47-108">이 자동 백업 기능을 사용하면 서버 및 모든 데이터베이스를 새 서버에 이전 특정 시점으로 복원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41d47-108">Using this automatic backup feature you may restore the server and all its databases into a new server to an earlier point-in-time.</span></span>

## <a name="restore-in-the-azure-portal"></a><span data-ttu-id="41d47-109">Azure Portal에서 복원</span><span class="sxs-lookup"><span data-stu-id="41d47-109">Restore in the Azure portal</span></span>
<span data-ttu-id="41d47-110">MySQL용 Azure Database를 사용하면 서버를 다시 특정 시점으로 서버의 새로운 복사본에 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41d47-110">Azure Database for MySQL allows you to restore the server back to a point in time and into to a new copy of the server.</span></span> <span data-ttu-id="41d47-111">이 새 서버를 사용하여 데이터를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41d47-111">You can use this new server to recover your data.</span></span> 

<span data-ttu-id="41d47-112">예를 들어 오늘 정오에 실수로 테이블을 삭제한 경우 정오 바로 전으로 복원하고 누락된 테이블과 데이터를 서버의 새로운 복사본에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41d47-112">For example, if a table was accidentally dropped at noon today, you could restore to the time just before noon and retrieve the missing table and data from that new copy of the server.</span></span>

<span data-ttu-id="41d47-113">다음 단계는 샘플 서버를 특정 시점으로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="41d47-113">The following steps restore the sample server to a point in time:</span></span>

1. <span data-ttu-id="41d47-114">[Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="41d47-114">Sign into the [Azure portal](https://portal.azure.com/)</span></span>

2. <span data-ttu-id="41d47-115">MySQL용 Azure Database 서버를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="41d47-115">Locate your Azure Database for MySQL server.</span></span> <span data-ttu-id="41d47-116">왼쪽 창에서 **모든 리소스**를 선택한 다음, 목록에서 서버를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41d47-116">In the left pane, select **All resources**, then select your server from the list.</span></span>

3.  <span data-ttu-id="41d47-117">서버 개요 블레이드 맨 위에서 도구 모음에 있는 **복원**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41d47-117">On the top of the server overview blade, click **Restore** on the toolbar.</span></span> <span data-ttu-id="41d47-118">복원 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="41d47-118">The Restore blade opens.</span></span>
<span data-ttu-id="41d47-119">![복원 단추 클릭](./media/howto-restore-server-portal/click-restore-button.png)</span><span class="sxs-lookup"><span data-stu-id="41d47-119">![click restore button](./media/howto-restore-server-portal/click-restore-button.png)</span></span>

4. <span data-ttu-id="41d47-120">필요한 정보로 복원 양식을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="41d47-120">Fill out the Restore form with the required information:</span></span>

- <span data-ttu-id="41d47-121">**복원 지점(UTC)**: 날짜 선택 및 시간 선택을 사용하여 복원할 특정 시점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41d47-121">**Restore point (UTC)**: Using the Date picker and time picker, select a point-in-time to restore to.</span></span> <span data-ttu-id="41d47-122">지정된 시간은 UTC 형식이므로 현지 시간을 UTC로 변환해야 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="41d47-122">The time specified is in UTC format, so you likely need to convert the local time into UTC.</span></span>
- <span data-ttu-id="41d47-123">**새 서버에 복원**: 기존 서버를 복원할 새 서버 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="41d47-123">**Restore to new server**: Provide a new server name to restore the existing server into.</span></span>
- <span data-ttu-id="41d47-124">**위치**: 지역 선택은 자동으로 원본 서버 지역으로 채워지며 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="41d47-124">**Location**: The region choice automatically populates with the source server region, and cannot be changed.</span></span>
- <span data-ttu-id="41d47-125">**가격 책정 계층**: 가격 책정 계층 선택은 자동으로 원본 서버와 동일한 가격 책정 계층으로 채워지고 여기서 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="41d47-125">**Pricing tier**: The pricing tier choice automatically populates with the same pricing tier as the source server, and cannot be changed here.</span></span> 
<span data-ttu-id="41d47-126">![PITR 복원](./media/howto-restore-server-portal/pitr-restore.png)</span><span class="sxs-lookup"><span data-stu-id="41d47-126">![PITR Restore](./media/howto-restore-server-portal/pitr-restore.png)</span></span>

5. <span data-ttu-id="41d47-127">**확인**을 클릭하여 특정 시점으로 복원할 서버를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="41d47-127">Click **OK** to restore the server to restore to a point in time.</span></span> 

6. <span data-ttu-id="41d47-128">복원이 완료되면 예상대로 데이터베이스가 복원되었는지 확인하기 위해 생성하였던 새 서버를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="41d47-128">After the restore finishes, locate the new server that was created to verify the databases were restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41d47-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="41d47-129">Next steps</span></span>
- [<span data-ttu-id="41d47-130">MySQL용 Azure 데이터베이스에 대한 연결 라이브러리</span><span class="sxs-lookup"><span data-stu-id="41d47-130">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)