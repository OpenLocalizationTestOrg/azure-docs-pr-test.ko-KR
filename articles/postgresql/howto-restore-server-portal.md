---
title: "어떻게 tooRestore PostgreSQL에 대 한 Azure 데이터베이스의 서버 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 toorestore PostgreSQL 사용에 대 한 Azure 데이터베이스의 서버 hello Azure 포털입니다."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: bc7351f384607397806d837afd3e1d7a26575e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-postgresql-using-hello-azure-portal"></a><span data-ttu-id="29123-103">어떻게 tooBackup 및 복원 PostgreSQL 사용에 대 한 Azure 데이터베이스의 서버 hello Azure 포털</span><span class="sxs-lookup"><span data-stu-id="29123-103">How tooBackup and Restore a server in Azure Database for PostgreSQL using hello Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="29123-104">자동으로 수행되는 백업</span><span class="sxs-lookup"><span data-stu-id="29123-104">Backup happens Automatically</span></span>
<span data-ttu-id="29123-105">PostgreSQL에 대 한 Azure 데이터베이스를 사용할 때는 hello 데이터베이스 서비스가 자동으로 hello 서비스의 백업을 5 분 마다.</span><span class="sxs-lookup"><span data-stu-id="29123-105">When using Azure Database for PostgreSQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="29123-106">hello 백업은 7 일 동안 사용할 수 있는 기본 계층과 35 일을 사용 하는 경우 표준 계층을 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="29123-106">hello backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="29123-107">자세한 내용은 [PostgreSQL용 Azure Database 서비스 계층](concepts-service-tiers.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29123-107">For more information, see [Azure Database for PostgreSQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="29123-108">이 자동 백업 기능을 사용 하 여 hello 서버와 모든 데이터베이스는 새 서버 tooan 이전 지정 시간으로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29123-108">Using this automatic backup feature you may restore hello server and all its databases into a new server tooan earlier point-in-time.</span></span>

## <a name="restore-in-hello-azure-portal"></a><span data-ttu-id="29123-109">Hello Azure 포털에서 복원</span><span class="sxs-lookup"><span data-stu-id="29123-109">Restore in hello Azure portal</span></span>
<span data-ttu-id="29123-110">Azure 데이터베이스 PostgreSQL에 대 한를 통해 toorestore hello 서버 백 tooa 지점 시간에서 및 tooa hello 서버의 새 복사본으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="29123-110">Azure Database for PostgreSQL allows you toorestore hello server back tooa point in time and into tooa new copy of hello server.</span></span> <span data-ttu-id="29123-111">이 새 서버 toorecover 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29123-111">You can use this new server toorecover your data.</span></span> 

<span data-ttu-id="29123-112">예를 들어 테이블 실수로 되었으면 정오에 오늘 삭제 있습니다 수 복원 정오 직전 toohello 시간 및 hello 누락 된 테이블 및 hello 서버 새 복사본에서 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="29123-112">For example, if a table was accidentally dropped at noon today, you could restore toohello time just before noon and retrieve hello missing table and data from that new copy of hello server.</span></span>

<span data-ttu-id="29123-113">hello 다음 단계 hello 샘플 서버 tooa 지점 시간으로 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="29123-113">hello following steps restore hello sample server tooa point in time:</span></span>
1. <span data-ttu-id="29123-114">Hello에 로그인 [Azure 포털](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="29123-114">Sign into hello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="29123-115">PostgreSQL용 Azure 데이터베이스 서버를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="29123-115">Locate your Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="29123-116">Hello Azure 포털에서에서 클릭 **모든 리소스** hello 왼쪽 메뉴 및 hello 이름에는 형식에서와 같은 **mypgserver 20170401**, 기존 서버에 대 한 toosearch 합니다.</span><span class="sxs-lookup"><span data-stu-id="29123-116">In hello Azure portal, click **All Resources** from hello left-hand menu and type in hello name, such as **mypgserver-20170401**, toosearch for your existing server.</span></span> <span data-ttu-id="29123-117">Hello 검색 결과에 나열 된 hello 서버 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29123-117">Click hello server name listed in hello search result.</span></span> <span data-ttu-id="29123-118">hello **개요** 페이지 서버 열리고 더 이상의 구성에 대 한 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="29123-118">hello **Overview** page for your server opens and provides options for further configuration.</span></span>

   ![Azure 포털-toolocate 서버 검색](media/postgresql-howto-restore-server-portal/1-locate.png)

3. <span data-ttu-id="29123-120">Hello 서버 개요 블레이드의 hello 위쪽에 클릭 **복원** hello 도구 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="29123-120">On hello top of hello server overview blade, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="29123-121">hello 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="29123-121">hello Restore blade opens.</span></span>

   ![PostgreSQL용 Azure Database - 개요 - 복원 단추](./media/postgresql-howto-restore-server-portal/2_server.png)

4. <span data-ttu-id="29123-123">Hello 복원 양식 hello 필요한 정보로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="29123-123">Fill out hello Restore form with hello required information:</span></span>

   ![<span data-ttu-id="29123-124">PostgreSQL용 Azure Database - 정보 복원</span><span class="sxs-lookup"><span data-stu-id="29123-124">Azure Database for PostgreSQL - Restore information</span></span> ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - <span data-ttu-id="29123-125">**복원 지점**:에-시간 hello 서버 변경 되기 전에 발생 하는 선택</span><span class="sxs-lookup"><span data-stu-id="29123-125">**Restore point**: Select a point-in-time that occurs before hello server was changed</span></span>
  - <span data-ttu-id="29123-126">**대상 서버**: toorestore에 사용할 새 서버 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="29123-126">**Target server**: Provide a new server name you want toorestore to</span></span>
  - <span data-ttu-id="29123-127">**위치**: hello 영역을 선택할 수 없습니다, 기본적으로 hello 원본 서버와 동일한은</span><span class="sxs-lookup"><span data-stu-id="29123-127">**Location**: You cannot select hello region, by default it is same as hello source server</span></span>
  - <span data-ttu-id="29123-128">**가격 책정 계층**: 이 값은 서버를 복원할 때 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="29123-128">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="29123-129">Hello 원본 서버와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="29123-129">It is same as hello source server.</span></span> 

5. <span data-ttu-id="29123-130">클릭 **확인** toorestore hello 서버 toorestore tooa 지정 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="29123-130">Click **OK** toorestore hello server toorestore tooa point in time.</span></span> 

6. <span data-ttu-id="29123-131">Hello 복원이 완료 되 면 데이터가 예상 대로 복원 된 tooverify hello 만들어지는 hello 새 서버를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="29123-131">Once hello restore finishes, locate hello new server that is created tooverify hello data was restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29123-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="29123-132">Next steps</span></span>
- [<span data-ttu-id="29123-133">PostgreSQL용 Azure Database에 대한 연결 라이브러리</span><span class="sxs-lookup"><span data-stu-id="29123-133">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
