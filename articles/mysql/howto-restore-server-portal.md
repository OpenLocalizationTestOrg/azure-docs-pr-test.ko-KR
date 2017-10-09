---
title: "MySQL에 대 한 Azure 데이터베이스의 서버 aaaHow tooRestore | Microsoft Docs"
description: "이 문서에서는 설명 방법을 사용 하 여 MySQL에 대 한 Azure 데이터베이스의 서버 toorestore hello Azure 포털입니다."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b990d5b37c5d4924de9571192b923e3c81094ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-mysql-using-hello-azure-portal"></a><span data-ttu-id="70334-103">어떻게 tooBackup 및 복원을 사용 하 여 MySQL에 대 한 Azure 데이터베이스의 서버 hello Azure 포털</span><span class="sxs-lookup"><span data-stu-id="70334-103">How tooBackup and Restore a server in Azure Database for MySQL using hello Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="70334-104">자동으로 수행되는 백업</span><span class="sxs-lookup"><span data-stu-id="70334-104">Backup happens Automatically</span></span>
<span data-ttu-id="70334-105">MySQL에 대 한 Azure 데이터베이스를 사용할 때는 hello 데이터베이스 서비스가 자동으로 hello 서비스의 백업을 5 분 마다.</span><span class="sxs-lookup"><span data-stu-id="70334-105">When using Azure Database for MySQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="70334-106">hello 백업은 7 일 동안 사용할 수 있는 기본 계층과 35 일을 사용 하는 경우 표준 계층을 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="70334-106">hello backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="70334-107">자세한 내용은 [MySQL용 Azure Database 서비스 계층](concepts-service-tiers.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70334-107">For more information, see [Azure Database for MySQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="70334-108">이 자동 백업 기능을 사용 하 여 hello 서버와 모든 데이터베이스는 새 서버 tooan 이전 지정 시간으로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70334-108">Using this automatic backup feature you may restore hello server and all its databases into a new server tooan earlier point-in-time.</span></span>

## <a name="restore-in-hello-azure-portal"></a><span data-ttu-id="70334-109">Hello Azure 포털에서 복원</span><span class="sxs-lookup"><span data-stu-id="70334-109">Restore in hello Azure portal</span></span>
<span data-ttu-id="70334-110">MySQL에 대 한 azure 데이터베이스가 있습니다 toorestore hello 서버 백 tooa 지점을 시간에서 및 tooa hello 서버의 새 복사본으로.</span><span class="sxs-lookup"><span data-stu-id="70334-110">Azure Database for MySQL allows you toorestore hello server back tooa point in time and into tooa new copy of hello server.</span></span> <span data-ttu-id="70334-111">이 새 서버 toorecover 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70334-111">You can use this new server toorecover your data.</span></span> 

<span data-ttu-id="70334-112">예를 들어 테이블 실수로 되었으면 정오에 오늘 삭제 있습니다 수 복원 정오 직전 toohello 시간 및 hello 누락 된 테이블 및 hello 서버 새 복사본에서 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="70334-112">For example, if a table was accidentally dropped at noon today, you could restore toohello time just before noon and retrieve hello missing table and data from that new copy of hello server.</span></span>

<span data-ttu-id="70334-113">hello 다음 단계 hello 샘플 서버 tooa 지점 시간으로 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="70334-113">hello following steps restore hello sample server tooa point in time:</span></span>

1. <span data-ttu-id="70334-114">Hello에 로그인 [Azure 포털](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="70334-114">Sign into hello [Azure portal](https://portal.azure.com/)</span></span>

2. <span data-ttu-id="70334-115">MySQL용 Azure Database 서버를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="70334-115">Locate your Azure Database for MySQL server.</span></span> <span data-ttu-id="70334-116">Hello 왼쪽된 창에서 선택 **모든 리소스**, hello 목록에서 서버를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="70334-116">In hello left pane, select **All resources**, then select your server from hello list.</span></span>

3.  <span data-ttu-id="70334-117">Hello 서버 개요 블레이드의 hello 위쪽에 클릭 **복원** hello 도구 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="70334-117">On hello top of hello server overview blade, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="70334-118">hello 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="70334-118">hello Restore blade opens.</span></span>
<span data-ttu-id="70334-119">![복원 단추 클릭](./media/howto-restore-server-portal/click-restore-button.png)</span><span class="sxs-lookup"><span data-stu-id="70334-119">![click restore button](./media/howto-restore-server-portal/click-restore-button.png)</span></span>

4. <span data-ttu-id="70334-120">Hello 복원 양식 hello 필요한 정보로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="70334-120">Fill out hello Restore form with hello required information:</span></span>

- <span data-ttu-id="70334-121">**복원 지점 (UTC)**:를 지정 시간 toorestore hello 날짜 선택 및 시간 선택을 사용 하 여을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="70334-121">**Restore point (UTC)**: Using hello Date picker and time picker, select a point-in-time toorestore to.</span></span> <span data-ttu-id="70334-122">hello 지정 된 시간은 UTC 형식으로 UTC로 가능성이 tooconvert hello 현지 시간을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="70334-122">hello time specified is in UTC format, so you likely need tooconvert hello local time into UTC.</span></span>
- <span data-ttu-id="70334-123">**Toonew 서버 복원**: 새 서버 이름 toorestore hello에 기존 서버를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="70334-123">**Restore toonew server**: Provide a new server name toorestore hello existing server into.</span></span>
- <span data-ttu-id="70334-124">**위치**: hello 지역 선택 자동으로 hello 소스 서버 영역 채워집니다 및 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70334-124">**Location**: hello region choice automatically populates with hello source server region, and cannot be changed.</span></span>
- <span data-ttu-id="70334-125">**가격 책정 계층**: hello 계층 선택 항목을 자동으로 가격를 채워 hello 계층 hello 원본 서버와 동일한 가격 및 여기에서 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70334-125">**Pricing tier**: hello pricing tier choice automatically populates with hello same pricing tier as hello source server, and cannot be changed here.</span></span> 
<span data-ttu-id="70334-126">![PITR 복원](./media/howto-restore-server-portal/pitr-restore.png)</span><span class="sxs-lookup"><span data-stu-id="70334-126">![PITR Restore](./media/howto-restore-server-portal/pitr-restore.png)</span></span>

5. <span data-ttu-id="70334-127">클릭 **확인** toorestore hello 서버 toorestore tooa 지정 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="70334-127">Click **OK** toorestore hello server toorestore tooa point in time.</span></span> 

6. <span data-ttu-id="70334-128">Hello 복원 완료 된 후 예상 대로 데이터베이스가 복원 된 tooverify hello 생성 된 hello 새 서버를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="70334-128">After hello restore finishes, locate hello new server that was created tooverify hello databases were restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70334-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="70334-129">Next steps</span></span>
- [<span data-ttu-id="70334-130">MySQL용 Azure 데이터베이스에 대한 연결 라이브러리</span><span class="sxs-lookup"><span data-stu-id="70334-130">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)