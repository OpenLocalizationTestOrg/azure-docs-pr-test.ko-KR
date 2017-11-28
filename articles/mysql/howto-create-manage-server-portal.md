---
title: "aaaCreate 및 Azure 포털을 사용 하 여 MySQL server에 대 한 Azure 데이터베이스 관리 | Microsoft Docs"
description: "설명 신속 하 게 MySQL server에 대 한 새 Azure 데이터베이스를 만들 하는 방법을 hello Azure 포털을 사용 하 여 hello 서버를 관리 합니다."
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c532df43b3d2124d7bd34875b32d52357f162af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a><span data-ttu-id="119e3-103">Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="119e3-103">Create and manage Azure Database for MySQL server using Azure portal</span></span>
<span data-ttu-id="119e3-104">설명 신속 하 게 MySQL server에 대 한 새 Azure 데이터베이스를 만들 하는 방법을 hello Azure 포털을 사용 하 여 hello 서버를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-104">This article describes how you can quickly create a new Azure Database for MySQL server and manage hello server using hello Azure Portal.</span></span> <span data-ttu-id="119e3-105">서버 관리 서버 세부 정보 및 데이터베이스 보기, 암호 다시 설정 및 서버 hello 삭제를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-105">Server management includes viewing server details & databases, resetting password and deleting hello server.</span></span>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="119e3-106">Azure 포털 toohello에 로그인</span><span class="sxs-lookup"><span data-stu-id="119e3-106">Log in toohello Azure portal</span></span>
<span data-ttu-id="119e3-107">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-107">Log in toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="119e3-108">Azure Database for MySQL 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="119e3-108">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="119e3-109">이러한 단계 toocreate "mysqlserver4demo" 이라는 MySQL 서버에 대 한 Azure 데이터베이스를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-109">Follow these steps toocreate an Azure Database for MySQL server named “mysqlserver4demo”</span></span>

<span data-ttu-id="119e3-110">원 클릭 **새로** 단추 hello 왼쪽 위 모서리의 hello Azure 포털에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-110">1- Click **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

<span data-ttu-id="119e3-111">2 선택 **데이터베이스** hello 새 페이지 및 선택에서 **MySQL에 대 한 Azure 데이터베이스** hello 데이터베이스 페이지에서.</span><span class="sxs-lookup"><span data-stu-id="119e3-111">2- Select **Databases** from hello New page, and select **Azure Database for MySQL** from hello Databases page.</span></span>

> <span data-ttu-id="119e3-112">MySQL용 Azure Database 서버는 일련의 정의된 [계산 및 저장소](./concepts-compute-unit-and-storage.md) 리소스를 사용하여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-112">An Azure Database for MySQL server is created with a defined set of [compute and storage](./concepts-compute-unit-and-storage.md) resources.</span></span> <span data-ttu-id="119e3-113">MySQL server에 대 한 Azure 데이터베이스 및 Azure 리소스 그룹 내의 hello 데이터베이스가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-113">hello database is created within an Azure resource group and in an Azure Database for MySQL server.</span></span>

![create-new-server](./media/howto-create-manage-server-portal/create-new-server.png)

<span data-ttu-id="119e3-115">3-다음 정보는 hello로 MySQL 폼에 대 한 hello Azure 데이터베이스를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-115">3- Fill out hello Azure Database for MySQL form with hello following information:</span></span>

| <span data-ttu-id="119e3-116">**양식 필드**</span><span class="sxs-lookup"><span data-stu-id="119e3-116">**Form Field**</span></span> | <span data-ttu-id="119e3-117">**필드 설명**</span><span class="sxs-lookup"><span data-stu-id="119e3-117">**Field Description**</span></span> |
|----------------|-----------------------|
| <span data-ttu-id="119e3-118">*서버 이름*</span><span class="sxs-lookup"><span data-stu-id="119e3-118">*Server name*</span></span> | <span data-ttu-id="119e3-119">azure-mysql(서버 이름은 전역적으로 고유함)</span><span class="sxs-lookup"><span data-stu-id="119e3-119">azure-mysql (server name is globally unique)</span></span> |
| <span data-ttu-id="119e3-120">*구독*</span><span class="sxs-lookup"><span data-stu-id="119e3-120">*Subscription*</span></span> | <span data-ttu-id="119e3-121">MySQLaaS(드롭다운 목록에서 선택)</span><span class="sxs-lookup"><span data-stu-id="119e3-121">MySQLaaS (select from drop down)</span></span> |
| <span data-ttu-id="119e3-122">*리소스 그룹*</span><span class="sxs-lookup"><span data-stu-id="119e3-122">*Resource group*</span></span> | <span data-ttu-id="119e3-123">myresource(새 리소스 그룹을 만들거나 기존 그룹 선택)</span><span class="sxs-lookup"><span data-stu-id="119e3-123">myresource (create a new resource group or use an existing one)</span></span> |
| <span data-ttu-id="119e3-124">*서버 관리자 로그인*</span><span class="sxs-lookup"><span data-stu-id="119e3-124">*Server admin login*</span></span> | <span data-ttu-id="119e3-125">myadmin(관리자 계정 이름을 설정함)</span><span class="sxs-lookup"><span data-stu-id="119e3-125">myadmin (setup admin account name)</span></span> |
| <span data-ttu-id="119e3-126">*암호*</span><span class="sxs-lookup"><span data-stu-id="119e3-126">*Password*</span></span> | <span data-ttu-id="119e3-127">암호 관리자 계정 암호</span><span class="sxs-lookup"><span data-stu-id="119e3-127">setup admin account password</span></span> |
| <span data-ttu-id="119e3-128">*암호 확인*</span><span class="sxs-lookup"><span data-stu-id="119e3-128">*Confirm password*</span></span> | <span data-ttu-id="119e3-129">관리자 계정 암호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-129">confirm admin account password</span></span> |
| <span data-ttu-id="119e3-130">*위치*:</span><span class="sxs-lookup"><span data-stu-id="119e3-130">*Location*</span></span> | <span data-ttu-id="119e3-131">북유럽(북유럽 및 미국 서부 중 선택)</span><span class="sxs-lookup"><span data-stu-id="119e3-131">North Europe (select between North Europe and West US)</span></span> |
| <span data-ttu-id="119e3-132">*버전*</span><span class="sxs-lookup"><span data-stu-id="119e3-132">*Version*</span></span> | <span data-ttu-id="119e3-133">5.6(MySQL용 Azure Database 서버 버전 선택)</span><span class="sxs-lookup"><span data-stu-id="119e3-133">5.6 (choose Azure Database for MySQL server version)</span></span> |

<span data-ttu-id="119e3-134">4 클릭 **가격 책정 계층** toospecify hello 서비스 계층과 성능 수준을 새 서버에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-134">4- Click **Pricing tier** toospecify hello service tier and performance level for your new server.</span></span> <span data-ttu-id="119e3-135">계산 단위는 기본 계층 50에서 100 및 표준 계층 100에서 200 사이로 구성할 수 있으며, 저장소는 포함된 금액에 따라 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-135">Compute Unit can be configured between 50 and 100 in Basic tier, 100 and 200 in Standard tier, and storage can be added based on included amount.</span></span> <span data-ttu-id="119e3-136">이 방법 가이드에서는 계산 단위 50 및 50GB를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-136">For this HowTo guide, let’s choose 50 Compute Unit and 50GB.</span></span> <span data-ttu-id="119e3-137">클릭 **확인** toosave 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-137">Click **OK** toosave your selection.</span></span>
<span data-ttu-id="119e3-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span><span class="sxs-lookup"><span data-stu-id="119e3-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span></span>

<span data-ttu-id="119e3-139">5 클릭 **만들기** tooprovision hello 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-139">5- Click **Create** tooprovision hello server.</span></span> <span data-ttu-id="119e3-140">프로비전하는 데 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-140">Provisioning takes a few minutes.</span></span>

> <span data-ttu-id="119e3-141">Hello 확인 **Pin toodashboard** 배포 옵션 tooallow 간편한 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-141">Check hello **Pin toodashboard** option tooallow easy tracking of your deployments.</span></span>
> [!NOTE]
> <span data-ttu-id="119e3-142">기본 계층에서 too1000GB 및 표준에 10000 GB를 계층 지원이 제공 됩니다 저장소, 공개 미리 보기에 대 한 최대 저장소 hello 이지만 여전히 제한 too1000GB 일시적으로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-142">Although up too1000GB in Basic tier and 10000GB in Standard tier will be supported for storage, for Public Preview, hello maximum storage is still limited too1000GB temporarily.</span></span> 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a><span data-ttu-id="119e3-143">MySQL용 Azure Database 서버 업데이트</span><span class="sxs-lookup"><span data-stu-id="119e3-143">Update an Azure Database for MySQL server</span></span>
<span data-ttu-id="119e3-144">새 서버를 프로 비전 되 면 사용자에 게 2 옵션 tooedit 기존 서버: hello 계산 단위를 변경 하 여 관리자 암호 자릿수 또는 소수 위쪽/아래쪽 hello 서버를 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-144">After new server is provisioned, user has 2 options tooedit an existing server: reset administrator password or scale up/down hello server by changing hello compute-units.</span></span>

### <a name="change-hello-administrator-user-password"></a><span data-ttu-id="119e3-145">Hello 관리자 사용자 암호 변경</span><span class="sxs-lookup"><span data-stu-id="119e3-145">Change hello administrator user password</span></span>
<span data-ttu-id="119e3-146">1-hello 서버에서 **개요** 블레이드에서 클릭 **암호 재설정** toopopulate 암호 입력 및 확인 창이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-146">1- On hello server **Overview** blade, click **Reset password** toopopulate a password input and confirmation window.</span></span>

<span data-ttu-id="119e3-147">2-새 암호를 입력 하 고 아래와 같이 hello 창의 hello 암호 확인: ![암호 재설정](./media/howto-create-manage-server-portal/reset-password.png)</span><span class="sxs-lookup"><span data-stu-id="119e3-147">2- Enter new password and confirm hello password in hello window as below: ![reset-password](./media/howto-create-manage-server-portal/reset-password.png)</span></span>

<span data-ttu-id="119e3-148">3 번 클릭 **확인** toosave hello에 대 한 새 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-148">3- Click **OK** toosave hello new password.</span></span>

### <a name="scale-updown-by-changing-compute-units"></a><span data-ttu-id="119e3-149">계산 단위를 변경하여 강화/규모 축소</span><span class="sxs-lookup"><span data-stu-id="119e3-149">Scale up/down by changing Compute Units</span></span>

<span data-ttu-id="119e3-150">1-에 hello 서버 블레이드에서 아래 **설정**, 클릭 **가격 책정 계층** tooopen hello 가격 책정 계층 블레이드 MySQL server에 대 한 hello Azure 데이터베이스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-150">1- On hello server blade, under **Settings**, click **Pricing tier** tooopen hello Pricing tier blade for hello Azure Database for MySQL server.</span></span>

<span data-ttu-id="119e3-151">다음 2 단계 4 **MySQL server 용 Azure 데이터베이스 만들기** toochange 계산 단위 가격 책정 계층을 동일한 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-151">2- Follow Step 4 in **Create an Azure Database for MySQL server** toochange Compute Units in hello same pricing tier.</span></span>

## <a name="delete-an-azure-database-for-mysql-server"></a><span data-ttu-id="119e3-152">MySQL용 Azure Database 서버 삭제</span><span class="sxs-lookup"><span data-stu-id="119e3-152">Delete an Azure Database for MySQL server</span></span>

<span data-ttu-id="119e3-153">1-서버의 hello **개요** 블레이드에서 클릭 **삭제** 명령 단추 tooopen hello Deleting 확인 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-153">1- On hello server **Overview** blade, click **Delete** command button tooopen hello Deleting confirmation blade.</span></span>

<span data-ttu-id="119e3-154">2-형식 hello hello 블레이드 double 확인의 입력된 상자에 올바른 서버 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-154">2- Type hello correct server name in input box of hello blade for double confirmation.</span></span>

<span data-ttu-id="119e3-155">3 번 클릭 **삭제** 단추를 다시 tooconfirm 작업을 삭제 하 고 hello 알림 표시줄에 "성공 삭제" 팝업 때까지 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-155">3- Click **Delete** button again tooconfirm deleting action and wait for “Deleting success” popup on hello notification bar.</span></span>

## <a name="list-hello-azure-database-for-mysql-databases"></a><span data-ttu-id="119e3-156">MySQL 데이터베이스에 대 한 목록 hello Azure 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="119e3-156">List hello Azure Database for MySQL databases</span></span>
<span data-ttu-id="119e3-157">Hello 서버의 **개요** 블레이드에서 hello 데이터베이스 나타날 때까지 아래로 스크롤하여 hello 아래쪽에 바둑판식으로 배열 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-157">On hello server **Overview** blade, scroll down until you see hello database tile on hello bottom.</span></span> <span data-ttu-id="119e3-158">모든 hello 데이터베이스 hello 테이블에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-158">All hello databases will be listed in hello table.</span></span> <span data-ttu-id="119e3-159">클릭 **삭제** 명령 단추 tooopen hello Deleting 확인 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-159">click **Delete** command button tooopen hello Deleting confirmation blade.</span></span>

![show-databases](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a><span data-ttu-id="119e3-161">MySQL용 Azure Database 서버의 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="119e3-161">Show details of an Azure Database for MySQL server</span></span>
<span data-ttu-id="119e3-162">클릭 **속성** 아래 **설정** hello 서버의 블레이드가 열리고 hello **속성** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-162">Click **Properties** under **Settings** on hello server blade will open hello **Properties** blade.</span></span> <span data-ttu-id="119e3-163">그런 다음 서버 hello에 대 한 모든 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119e3-163">Then you can view all detailed information about hello server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="119e3-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="119e3-164">Next steps</span></span>

[<span data-ttu-id="119e3-165">빠른 시작: Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="119e3-165">Quickstart: Create Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
