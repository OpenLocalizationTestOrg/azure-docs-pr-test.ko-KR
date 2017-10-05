---
title: "Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기 및 관리 | Microsoft Docs"
description: "이 문서에서는 Azure Portal을 사용하여 신속하게 새로운 MySQL용 Azure Database 서버를 만들고 해당 서버를 관리하는 방법을 설명합니다."
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4605518b6955d9943e76c25df2d4105a6a94433d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a><span data-ttu-id="eb5c9-103">Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="eb5c9-103">Create and manage Azure Database for MySQL server using Azure portal</span></span>
<span data-ttu-id="eb5c9-104">이 문서에서는 Azure Portal을 사용하여 신속하게 새로운 MySQL용 Azure Database 서버를 만들고 해당 서버를 관리하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-104">This article describes how you can quickly create a new Azure Database for MySQL server and manage the server using the Azure Portal.</span></span> <span data-ttu-id="eb5c9-105">서버 관리에는 서버 세부 정보 및 데이터베이스를 보고, 암호를 다시 설정하고 해당 서버를 삭제하는 것을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-105">Server management includes viewing server details & databases, resetting password and deleting the server.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="eb5c9-106">Azure 포털에 로그인</span><span class="sxs-lookup"><span data-stu-id="eb5c9-106">Log in to the Azure portal</span></span>
<span data-ttu-id="eb5c9-107">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-107">Log in to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="eb5c9-108">MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="eb5c9-108">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="eb5c9-109">“mysqlserver4demo”라는 MySQL용 Azure Database 서버를 만들려면 다음과 같은 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-109">Follow these steps to create an Azure Database for MySQL server named “mysqlserver4demo”</span></span>

<span data-ttu-id="eb5c9-110">1 - Azure Portal의 왼쪽 위에 있는 **새로 만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-110">1- Click **New** button found on the upper left-hand corner of the Azure portal.</span></span>

<span data-ttu-id="eb5c9-111">2 - 새로 만들기 페이지에서 **데이터베이스**를 선택하고 데이터베이스 페이지에서 **MySQL용 Azure Database**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-111">2- Select **Databases** from the New page, and select **Azure Database for MySQL** from the Databases page.</span></span>

> <span data-ttu-id="eb5c9-112">MySQL용 Azure Database 서버는 일련의 정의된 [계산 및 저장소](./concepts-compute-unit-and-storage.md) 리소스를 사용하여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-112">An Azure Database for MySQL server is created with a defined set of [compute and storage](./concepts-compute-unit-and-storage.md) resources.</span></span> <span data-ttu-id="eb5c9-113">데이터베이스는 Azure 리소스 그룹 및 MySQL용 Azure Database 서버에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-113">The database is created within an Azure resource group and in an Azure Database for MySQL server.</span></span>

![create-new-server](./media/howto-create-manage-server-portal/create-new-server.png)

<span data-ttu-id="eb5c9-115">3 - 다음 정보에 대한 MySQL용 Azure Database 양식을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-115">3- Fill out the Azure Database for MySQL form with the following information:</span></span>

| <span data-ttu-id="eb5c9-116">**양식 필드**</span><span class="sxs-lookup"><span data-stu-id="eb5c9-116">**Form Field**</span></span> | <span data-ttu-id="eb5c9-117">**필드 설명**</span><span class="sxs-lookup"><span data-stu-id="eb5c9-117">**Field Description**</span></span> |
|----------------|-----------------------|
| <span data-ttu-id="eb5c9-118">*서버 이름*</span><span class="sxs-lookup"><span data-stu-id="eb5c9-118">*Server name*</span></span> | <span data-ttu-id="eb5c9-119">azure-mysql(서버 이름은 전역적으로 고유함)</span><span class="sxs-lookup"><span data-stu-id="eb5c9-119">azure-mysql (server name is globally unique)</span></span> |
| <span data-ttu-id="eb5c9-120">*구독*</span><span class="sxs-lookup"><span data-stu-id="eb5c9-120">*Subscription*</span></span> | <span data-ttu-id="eb5c9-121">MySQLaaS(드롭다운 목록에서 선택)</span><span class="sxs-lookup"><span data-stu-id="eb5c9-121">MySQLaaS (select from drop down)</span></span> |
| <span data-ttu-id="eb5c9-122">*리소스 그룹*</span><span class="sxs-lookup"><span data-stu-id="eb5c9-122">*Resource group*</span></span> | <span data-ttu-id="eb5c9-123">myresource(새 리소스 그룹을 만들거나 기존 그룹 선택)</span><span class="sxs-lookup"><span data-stu-id="eb5c9-123">myresource (create a new resource group or use an existing one)</span></span> |
| <span data-ttu-id="eb5c9-124">*서버 관리자 로그인*</span><span class="sxs-lookup"><span data-stu-id="eb5c9-124">*Server admin login*</span></span> | <span data-ttu-id="eb5c9-125">myadmin(관리자 계정 이름을 설정함)</span><span class="sxs-lookup"><span data-stu-id="eb5c9-125">myadmin (setup admin account name)</span></span> |
| <span data-ttu-id="eb5c9-126">*암호*</span><span class="sxs-lookup"><span data-stu-id="eb5c9-126">*Password*</span></span> | <span data-ttu-id="eb5c9-127">암호 관리자 계정 암호</span><span class="sxs-lookup"><span data-stu-id="eb5c9-127">setup admin account password</span></span> |
| <span data-ttu-id="eb5c9-128">*암호 확인*</span><span class="sxs-lookup"><span data-stu-id="eb5c9-128">*Confirm password*</span></span> | <span data-ttu-id="eb5c9-129">관리자 계정 암호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-129">confirm admin account password</span></span> |
| <span data-ttu-id="eb5c9-130">*위치*:</span><span class="sxs-lookup"><span data-stu-id="eb5c9-130">*Location*</span></span> | <span data-ttu-id="eb5c9-131">북유럽(북유럽 및 미국 서부 중 선택)</span><span class="sxs-lookup"><span data-stu-id="eb5c9-131">North Europe (select between North Europe and West US)</span></span> |
| <span data-ttu-id="eb5c9-132">*버전*</span><span class="sxs-lookup"><span data-stu-id="eb5c9-132">*Version*</span></span> | <span data-ttu-id="eb5c9-133">5.6(MySQL용 Azure Database 서버 버전 선택)</span><span class="sxs-lookup"><span data-stu-id="eb5c9-133">5.6 (choose Azure Database for MySQL server version)</span></span> |

<span data-ttu-id="eb5c9-134">4- **가격 책정 계층**을 클릭하고 새 서버의 서비스 계층 및 성능 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-134">4- Click **Pricing tier** to specify the service tier and performance level for your new server.</span></span> <span data-ttu-id="eb5c9-135">계산 단위는 기본 계층 50에서 100 및 표준 계층 100에서 200 사이로 구성할 수 있으며, 저장소는 포함된 금액에 따라 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-135">Compute Unit can be configured between 50 and 100 in Basic tier, 100 and 200 in Standard tier, and storage can be added based on included amount.</span></span> <span data-ttu-id="eb5c9-136">이 방법 가이드에서는 계산 단위 50 및 50GB를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-136">For this HowTo guide, let’s choose 50 Compute Unit and 50GB.</span></span> <span data-ttu-id="eb5c9-137">**확인**을 클릭하여 선택 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-137">Click **OK** to save your selection.</span></span>
<span data-ttu-id="eb5c9-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span><span class="sxs-lookup"><span data-stu-id="eb5c9-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span></span>

<span data-ttu-id="eb5c9-139">5- **만들기**를 클릭하여 서버를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-139">5- Click **Create** to provision the server.</span></span> <span data-ttu-id="eb5c9-140">프로비전하는 데 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-140">Provisioning takes a few minutes.</span></span>

> <span data-ttu-id="eb5c9-141">배포를 쉽게 추적할 수 있는 **대시보드에 고정** 옵션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-141">Check the **Pin to dashboard** option to allow easy tracking of your deployments.</span></span>
> [!NOTE]
> <span data-ttu-id="eb5c9-142">공개 미리 보기를 위해 기본 계층에서 최대 1000GB 및 표준 계층에서 10000GB 저장소가 지원되며 최대 저장소는 일시적으로 여전히 1000GB로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-142">Although up to 1000GB in Basic tier and 10000GB in Standard tier will be supported for storage, for Public Preview, the maximum storage is still limited to 1000GB temporarily.</span></span> 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a><span data-ttu-id="eb5c9-143">MySQL용 Azure Database 서버 업데이트</span><span class="sxs-lookup"><span data-stu-id="eb5c9-143">Update an Azure Database for MySQL server</span></span>
<span data-ttu-id="eb5c9-144">새 서버가 프로비전되면 사용자는 사용자 암호를 다시 설정하거나 계산 단위를 변경하여 서버를 강화/규모 축소하는 등의 기존 서버를 편집할 수 있는 2가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-144">After new server is provisioned, user has 2 options to edit an existing server: reset administrator password or scale up/down the server by changing the compute-units.</span></span>

### <a name="change-the-administrator-user-password"></a><span data-ttu-id="eb5c9-145">관리자 암호 변경</span><span class="sxs-lookup"><span data-stu-id="eb5c9-145">Change the administrator user password</span></span>
<span data-ttu-id="eb5c9-146">1- 서버 **개요** 블레이드에서 **암호 재설정**을 클릭하여 암호 입력 및 확인 창을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-146">1- On the server **Overview** blade, click **Reset password** to populate a password input and confirmation window.</span></span>

<span data-ttu-id="eb5c9-147">2- 새 암호를 입력하고 아래와 같이 창에서 암호를 확인합니다. ![reset-password](./media/howto-create-manage-server-portal/reset-password.png)</span><span class="sxs-lookup"><span data-stu-id="eb5c9-147">2- Enter new password and confirm the password in the window as below: ![reset-password](./media/howto-create-manage-server-portal/reset-password.png)</span></span>

<span data-ttu-id="eb5c9-148">3- **확인**을 클릭하여 새 암호를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-148">3- Click **OK** to save the new password.</span></span>

### <a name="scale-updown-by-changing-compute-units"></a><span data-ttu-id="eb5c9-149">계산 단위를 변경하여 강화/규모 축소</span><span class="sxs-lookup"><span data-stu-id="eb5c9-149">Scale up/down by changing Compute Units</span></span>

<span data-ttu-id="eb5c9-150">1- 서버 블레이드의 **설정**에서 **가격 책정 계층**을 클릭하여 MySQL용 Azure Database 서버에 대한 가격 책정 계층 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-150">1- On the server blade, under **Settings**, click **Pricing tier** to open the Pricing tier blade for the Azure Database for MySQL server.</span></span>

<span data-ttu-id="eb5c9-151">2- **MySQL용 Azure Database 서버 만들기**의 4단계에 따라 동일한 가격 책정 계층의 계산 단위를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-151">2- Follow Step 4 in **Create an Azure Database for MySQL server** to change Compute Units in the same pricing tier.</span></span>

## <a name="delete-an-azure-database-for-mysql-server"></a><span data-ttu-id="eb5c9-152">MySQL용 Azure Database 서버 삭제</span><span class="sxs-lookup"><span data-stu-id="eb5c9-152">Delete an Azure Database for MySQL server</span></span>

<span data-ttu-id="eb5c9-153">1- 서버 **개요** 블레이드에서 **삭제** 명령 단추를 클릭하여 삭제 확인 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-153">1- On the server **Overview** blade, click **Delete** command button to open the Deleting confirmation blade.</span></span>

<span data-ttu-id="eb5c9-154">2- 이중 확인을 위해 블레이드의 입력 상자에 올바른 서버 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-154">2- Type the correct server name in input box of the blade for double confirmation.</span></span>

<span data-ttu-id="eb5c9-155">3- **삭제** 단추를 다시 클릭하여 삭제 작업을 확인하고 알림 표시줄에 “삭제 성공” 메시지가 표시되길 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-155">3- Click **Delete** button again to confirm deleting action and wait for “Deleting success” popup on the notification bar.</span></span>

## <a name="list-the-azure-database-for-mysql-databases"></a><span data-ttu-id="eb5c9-156">MySQL용 Azure Database 데이터베이스 나열</span><span class="sxs-lookup"><span data-stu-id="eb5c9-156">List the Azure Database for MySQL databases</span></span>
<span data-ttu-id="eb5c9-157">서버 **개요** 블레이드에서 맨 아래에 데이터베이스 타일이 표시될 때까지 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-157">On the server **Overview** blade, scroll down until you see the database tile on the bottom.</span></span> <span data-ttu-id="eb5c9-158">모든 데이터베이스가 테이블에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-158">All the databases will be listed in the table.</span></span> <span data-ttu-id="eb5c9-159">**삭제** 명령 단추를 클릭하여 삭제 확인 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-159">click **Delete** command button to open the Deleting confirmation blade.</span></span>

![show-databases](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a><span data-ttu-id="eb5c9-161">MySQL용 Azure Database 서버의 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="eb5c9-161">Show details of an Azure Database for MySQL server</span></span>
<span data-ttu-id="eb5c9-162">서버 블레이드의 **설정**에서 **속성**을 클릭하면 **속성** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-162">Click **Properties** under **Settings** on the server blade will open the **Properties** blade.</span></span> <span data-ttu-id="eb5c9-163">그러면 서버에 대한 자세한 모든 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb5c9-163">Then you can view all detailed information about the server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb5c9-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eb5c9-164">Next steps</span></span>

[<span data-ttu-id="eb5c9-165">빠른 시작: Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="eb5c9-165">Quickstart: Create Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
