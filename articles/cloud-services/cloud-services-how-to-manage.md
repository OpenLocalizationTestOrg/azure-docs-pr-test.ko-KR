---
title: "일반적인 클라우드 서비스 관리 작업(클래식) | Microsoft Docs"
description: "Azure 클래식 포털에서 클라우드 서비스를 관리하는 방법에 대해 알아봅니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 41a30e50-067c-485b-96fd-434a6d057abc
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 2ee76dfcb579e53975b1f61a6590f8d78dc0961b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-cloud-services"></a><span data-ttu-id="452a9-103">클라우드 서비스를 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="452a9-103">How to Manage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="452a9-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="452a9-104">Azure portal</span></span>](cloud-services-how-to-manage-portal.md)
> * [<span data-ttu-id="452a9-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="452a9-105">Azure classic portal</span></span>](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="452a9-106">Azure 클래식 포털 **클라우드 서비스** 영역에서 서비스 역할 또는 배포를 업데이트하고, 스테이징된 배포의 수준을 프로덕션으로 올리고, 리소스 종속성을 표시하고 리소스를 확장할 수 있도록 클라우드 서비스에 리소스를 연결하고, 클라우드 서비스 또는 배포를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-106">In the **Cloud Services** area of the Azure classic portal, you can update a service role or a deployment, promote a staged deployment to production, link resources to your cloud service so that you can see the resource dependencies and scale the resources together, and delete a cloud service or a deployment.</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="452a9-107">방법: 클라우드 서비스 역할 또는 배포 업데이트</span><span class="sxs-lookup"><span data-stu-id="452a9-107">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="452a9-108">클라우드 서비스의 응용 프로그램 코드를 업데이트해야 하는 경우 대시보드, **클라우드 서비스** 페이지 또는 **인스턴스** 페이지에서 **업데이트**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-108">If you need to update the application code for your cloud service, use **Update** on the dashboard, **Cloud Services** page, or **Instances** page.</span></span> <span data-ttu-id="452a9-109">단일 역할이나 모든 역할을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-109">You can update a single role or all roles.</span></span> <span data-ttu-id="452a9-110">새 서비스 패키지 및 서비스 구성 파일을 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-110">You'll need to upload a new service package and service configuration file.</span></span>

1. <span data-ttu-id="452a9-111">[Azure 클래식 포털](https://manage.windowsazure.com/)에서 대시보드, **클라우드 서비스** 페이지 또는 **인스턴스** 페이지에 있는 **업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-111">In the [Azure classic portal](https://manage.windowsazure.com/), on the dashboard, **Cloud Services** page, or **Instances** page, click **Update**.</span></span>

    ![배포 업데이트](./media/cloud-services-how-to-manage/CloudServices_UpdateDeployment.png)

2. <span data-ttu-id="452a9-113">**배포 레이블**에 배포를 식별하는 이름(예: mycloudservice4)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-113">In **Deployment label**, enter a name to identify the deployment (for example, mycloudservice4).</span></span> <span data-ttu-id="452a9-114">배포 레이블은 대시보드의 **빠른 시작** 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-114">You'll find the deployment label under **quick start** on the dashboard.</span></span>
3. <span data-ttu-id="452a9-115">**패키지**에서 **찾아보기**를 사용하여 서비스 패키지 파일(.cspkg)을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-115">In **Package**, use **Browse** to upload the service package file (.cspkg).</span></span>
4. <span data-ttu-id="452a9-116">**구성**에서 **찾아보기**를 사용하여 서비스 구성 파일(.cscfg)을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-116">In **Configuration**, use **Browse** to upload the service configuration file (.cscfg).</span></span>
5. <span data-ttu-id="452a9-117">클라우드 서비스의 모든 역할을 업그레이드하려는 경우 **역할**에서 **모두**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-117">In **Role**, select **All** if you want to upgrade all roles in the cloud service.</span></span> <span data-ttu-id="452a9-118">단일 역할 업데이터를 수행하려면 업데이트할 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-118">To perform a single role update, select the role you want to update.</span></span> <span data-ttu-id="452a9-119">업데이트할 특정 역할을 선택하더라도 서비스 구성 파일의 업데이트는 모든 역할에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-119">Even if you select a specific role to update, the updates in the service configuration file are applied to all roles.</span></span>
6. <span data-ttu-id="452a9-120">업데이트로 인해 역할 수 또는 역할 크기가 변경되는 경우에는 **역할 크기 또는 역할의 수가 변경되어도 업데이트 허용** 확인란을 선택하여 업데이트가 진행되도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-120">If the update changes the number of roles or the size of any role, select the **Allow update if role sizes or number of roles changes** check box to enable the update to proceed.</span></span>

    <span data-ttu-id="452a9-121">역할의 크기, 즉 역할 인스턴스를 호스트하는 가상 컴퓨터의 크기나 역할의 수를 변경하는 경우 각 역할 인스턴스(가상 컴퓨터)를 이미지로 다시 설치해야 하며, 이때 로컬 데이터가 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-121">Be aware that if you change the size of a role (that is, the size of a virtual machine that hosts a role instance) or the number of roles, each role instance (virtual machine) must be re-imaged, and any local data will be lost.</span></span>

7. <span data-ttu-id="452a9-122">서비스 역할에 역할 인스턴스가 하나만 있는 경우 **단일 인스턴스가 포함된 역할이 하나 이상 있는 경우에도 배포** 확인란을 선택하여 업그레이드가 계속 진행되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-122">If any service roles have only one role instance, select the **Update even if one or more role contain a single instance check box** to enable the upgrade to proceed.</span></span>

    <span data-ttu-id="452a9-123">Azure는 각 역할에 둘 이상의 역할 인스턴스(가상 컴퓨터)가 있는 경우에만 클라우드 서비스 업데이트 중 99.95%의 서비스 가용성을 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-123">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="452a9-124">이에 따라, 가상 컴퓨터 하나는 클라이언트 요청을 처리하고 다른 하나는 업데이트를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-124">That enables one virtual machine to process client requests while the other is being updated.</span></span>

8. <span data-ttu-id="452a9-125">**확인** (확인 표시)을 클릭하여 서비스 업데이트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-125">Click **OK** (checkmark) to begin updating the service.</span></span>

## <a name="how-to-swap-deployments-to-promote-a-staged-deployment-to-production"></a><span data-ttu-id="452a9-126">방법: 스테이징된 배포의 수준을 프로덕션으로 올려 배포 교환</span><span class="sxs-lookup"><span data-stu-id="452a9-126">How to: Swap deployments to promote a staged deployment to production</span></span>
<span data-ttu-id="452a9-127">**교환** 을 사용하여 클라우드 서비스 스테이징 배포의 수준을 프로덕션으로 올립니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-127">Use **Swap** to promote a staging deployment of a cloud service to production.</span></span> <span data-ttu-id="452a9-128">새로운 클라우드 서비스 릴리스를 배포할 때는 고객이 현재 릴리스를 프로덕션에서 사용하고 있는 동안 클라우드 서비스 스테이징 환경에서 새 릴리스를 스테이징하고 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-128">When you decide to deploy a new release of a cloud service, you can stage and test your new release in your cloud service staging environment while your customers are using the current release in production.</span></span> <span data-ttu-id="452a9-129">새 릴리스를 프로덕션으로 이동할 준비가 되면 **교환** 을 사용하여 두 배포의 주소로 사용 중인 URL을 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-129">When you're ready to promote the new release to production, you can use **Swap** to switch the URLs by which the two deployments are addressed.</span></span>

<span data-ttu-id="452a9-130">**클라우드 서비스** 페이지나 대시보드에서 배포를 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-130">You can swap deployments from the **Cloud Services** page or the dashboard.</span></span>

1. <span data-ttu-id="452a9-131">[Azure 클래식 포털](https://manage.windowsazure.com/)에서 **클라우드 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-131">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**.</span></span>
2. <span data-ttu-id="452a9-132">클라우드 서비스 목록에서 클라우드 서비스를 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-132">In the list of cloud services, click the cloud service to select it.</span></span>
3. <span data-ttu-id="452a9-133">**교환**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-133">Click **Swap**.</span></span>

    <span data-ttu-id="452a9-134">다음과 같은 확인 메시지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-134">The following confirmation prompt opens.</span></span>

    ![클라우드 서비스 교환](./media/cloud-services-how-to-manage/CloudServices_Swap.png)

4. <span data-ttu-id="452a9-136">배포 정보를 확인한 후 **예** 를 클릭하여 배포를 교환합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-136">After you verify the deployment information, click **Yes** to swap the deployments.</span></span>

    <span data-ttu-id="452a9-137">변경되는 것은 배포의 VIP(가상 IP) 주소뿐이기 때문에 배포 교환은 신속하게 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-137">The deployment swap happens quickly because the only thing that changes is the virtual IP addresses (VIPs) for the deployments.</span></span>

    <span data-ttu-id="452a9-138">계산 비용을 절약하려면 새 프로덕션 배포가 예상대로 수행된다는 것이 확인될 때 스테이징 환경의 배포를 삭제하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-138">To save compute costs, you can delete the deployment in the staging environment when you're sure the new production deployment is performing as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="452a9-139">배포 교환에 대한 일반적인 질문</span><span class="sxs-lookup"><span data-stu-id="452a9-139">Common questions about swapping deployments</span></span>

<span data-ttu-id="452a9-140">**배포 교환을 위한 필수 조건**</span><span class="sxs-lookup"><span data-stu-id="452a9-140">**What are the prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="452a9-141">성공적인 배포 교환을 위한 2가지 핵심 필수 조건은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-141">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="452a9-142">프로덕션 슬롯에 정적 IP 주소를 사용하려는 경우에는 스테이징 슬롯을 위해서도 하나를 예비해 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-142">If you would like to use a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="452a9-143">그러지 않으면 교체가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-143">Otherwise, the swap will fail.</span></span>

- <span data-ttu-id="452a9-144">역할의 모든 인스턴스는 교체를 수행하기 전에 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-144">All instances of your roles must be running before you can perform the swap.</span></span> <span data-ttu-id="452a9-145">Azure 클래식 포털 또는 [Windows PowerShell의 Get-AzureRole 명령](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0)을 사용하여 인스턴스 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-145">You can check the status of your instances in the Azure classic portal or by using [the Get-AzureRole command in Windows PowerShell](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0).</span></span>

<span data-ttu-id="452a9-146">게스트 OS 업데이트 및 서비스 복구 작업으로 인해 배포 교체가 실패할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-146">Note that guest OS updates and service healing operations can also cause deployment swaps to fail.</span></span> <span data-ttu-id="452a9-147">자세한 내용은 [클라우드 서비스 배포 문제 해결](cloud-services-troubleshoot-deployment-problems.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="452a9-147">See [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md) for more details.</span></span>

<span data-ttu-id="452a9-148">**교체 시 응용 프로그램 가동 중지가 발생할 수 있습니까? 어떻게 처리해야 합니까?**</span><span class="sxs-lookup"><span data-stu-id="452a9-148">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="452a9-149">마지막 섹션에서 설명한 대로 배포 교체는 Azure Load Balancer에서의 구성 변경일 뿐이므로, 일반적으로 매우 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-149">As described in the last section, a deployment swap is typically very fast since it is just a configuration change in the Azure load balancer.</span></span> <span data-ttu-id="452a9-150">그러나 경우에 따라 10초 이상 걸리며 일시적인 연결 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="452a9-151">고객에게 미치는 영향을 최소화하려면 [고객 재시도 논리](../best-practices-retry-general.md) 구현을 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="452a9-151">To limit impact to your customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-to-a-cloud-service"></a><span data-ttu-id="452a9-152">방법: 클라우드 서비스에 리소스 연결</span><span class="sxs-lookup"><span data-stu-id="452a9-152">How to: Link a resource to a cloud service</span></span>
<span data-ttu-id="452a9-153">다른 리소스에 대한 클라우드 서비스 종속성을 표시하려면 Azure SQL 데이터베이스 인스턴스 또는 저장소 계정을 클라우드 서비스에 연결하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-153">To show your cloud service's dependencies on other resources, you can link an Azure SQL Database instance or a storage account to the cloud service.</span></span> <span data-ttu-id="452a9-154">**연결된 리소스** 페이지에서 리소스를 연결 및 연결 해제하고 클라우드 서비스 대시보드에서 사용을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-154">You can link and unlink resources on the **Linked Resources** page, and then monitor their usage on the cloud service dashboard.</span></span> <span data-ttu-id="452a9-155">연결된 저장소 계정의 모니터링이 켜져 있는 경우 클라우드 서비스 대시보드에서 Total Requests를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-155">If a linked storage account has monitoring turned on, you can monitor Total Requests on the cloud service dashboard.</span></span>

<span data-ttu-id="452a9-156">기존이나 새로운 SQL 데이터베이스 인스턴스 또는 저장소 계정을 클라우드 서비스에 연결하려면 **연결**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-156">Use **Link** to link a new or existing SQL Database instance or storage account to your cloud service.</span></span> <span data-ttu-id="452a9-157">그런 다음, 데이터베이스 및 이를 사용 중인 클라우드 서비스 역할을 **크기 조정** 페이지에서 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-157">You can then scale the database along with the cloud service role that is using it on the **Scale** page.</span></span> <span data-ttu-id="452a9-158">(저장소 계정은 사용량이 늘어나면 자동으로 확장됩니다.) 자세한 내용은 [클라우드 서비스 및 연결된 리소스를 확장하는 방법](cloud-services-how-to-scale.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="452a9-158">(A storage account scales automatically as usage increases.) For more information, see [How to Scale a Cloud Service and Linked Resources](cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="452a9-159">Azure 클래식 포털의 **데이터베이스** 노드에서 데이터베이스를 모니터링하고 관리하며 확장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-159">You also can monitor, manage, and scale the database in the **Databases** node of the Azure classic portal.</span></span>

<span data-ttu-id="452a9-160">여기서 리소스 "연결"은 앱을 리소스에 연결하는 것이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-160">"Linking" a resource in this sense doesn't connect your app to the resource.</span></span> <span data-ttu-id="452a9-161">**연결**을 사용하여 새 데이터베이스를 만드는 경우 응용 프로그램 코드에 연결 문자열을 추가한 후 클라우드 서비스를 업그레이드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-161">If you create a new database using **Link**, you'll need to add the connection strings to your application code and then upgrade the cloud service.</span></span> <span data-ttu-id="452a9-162">연결된 저장소 계정의 리소스를 사용하는 앱인 경우에도 연결 문자열을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-162">You'll also need to add connection strings if your app uses resources in a linked storage account.</span></span>

<span data-ttu-id="452a9-163">다음 절차는 새 SQL 데이터베이스 서버에 배포된 새 SQL 데이터베이스 인스턴스를 클라우드 서비스에 연결하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-163">The following procedure describes how to link a new SQL Database instance, deployed on a new SQL Database server, to a cloud service.</span></span>

### <a name="to-link-a-sql-database-instance-to-a-cloud-service"></a><span data-ttu-id="452a9-164">SQL 데이터베이스 인스턴스를 클라우드 서비스에 연결하려면</span><span class="sxs-lookup"><span data-stu-id="452a9-164">To link a SQL Database instance to a cloud service</span></span>
1. <span data-ttu-id="452a9-165">[Azure 클래식 포털](http://manage.windowsazure.com/)에서 **클라우드 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-165">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**.</span></span> <span data-ttu-id="452a9-166">그런 다음 클라우드 서비스의 이름을 클릭하여 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-166">Then click the name of the cloud service to open the dashboard.</span></span>
2. <span data-ttu-id="452a9-167">**연결된 리소스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-167">Click **Linked Resources**.</span></span>

    <span data-ttu-id="452a9-168">**연결된 리소스** 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-168">The **Linked Resources** page opens.</span></span>

    ![연결된 리소스 페이지](./media/cloud-services-how-to-manage/CloudServices_LinkedResourcesPage.png)

3. <span data-ttu-id="452a9-170">**연결된 리소스** 또는 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-170">Click either **Link a Resource** or **Link**.</span></span>

    <span data-ttu-id="452a9-171">**연결된 리소스** 마법사가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-171">The **Link Resource** wizard starts.</span></span>

    ![연결 페이지1](./media/cloud-services-how-to-manage/CloudServices_LinkedResources_LinkPage1.png)

4. <span data-ttu-id="452a9-173">**새 리소스 만들기** 또는 **기존 리소스에 연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-173">Click **Create a new resource** or **Link an existing resource**.</span></span>
5. <span data-ttu-id="452a9-174">연결할 리소스 종류를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-174">Choose the type of resource to link.</span></span> <span data-ttu-id="452a9-175">[Azure 클래식 포털](http://manage.windowsazure.com/)에서 **SQL 데이터베이스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-175">In the [Azure classic portal](http://manage.windowsazure.com/), click **SQL Database**.</span></span> <span data-ttu-id="452a9-176">(Azure 클래식 포털에서만 저장소 계정을 클라우드 서비스에 연결할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="452a9-176">(Only the Azure classic portal supports linking a storage account to a cloud service.)</span></span>
6. <span data-ttu-id="452a9-177">데이터베이스 구성을 완료하려면 도움말에서 Azure 클래식 포털의 **SQL 데이터베이스** 영역에 대한 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="452a9-177">To complete the database configuration, follow instructions in help for the **SQL Databases** area of the Azure classic portal.</span></span>

    <span data-ttu-id="452a9-178">메시지 영역에서 연결 작업의 진행률을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-178">You can follow the progress of the linking operation in the message area.</span></span>

    <span data-ttu-id="452a9-179">연결이 완료되면 클라우드 서비스 대시보드에서 연결된 리소스의 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-179">When linking is complete, you can monitor the status of the linked resource on the cloud service dashboard.</span></span> <span data-ttu-id="452a9-180">연결된 SQL 데이터베이스의 확장에 대한 자세한 내용은 [클라우드 서비스 및 연결된 리소스를 확장하는 방법](cloud-services-how-to-scale.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="452a9-180">For information about scaling a linked SQL Database, see [How to Scale a Cloud Service and Linked Resources](cloud-services-how-to-scale.md).</span></span>

### <a name="to-unlink-a-linked-resource"></a><span data-ttu-id="452a9-181">연결된 리소스를 연결 해제하려면</span><span class="sxs-lookup"><span data-stu-id="452a9-181">To unlink a linked resource</span></span>
1. <span data-ttu-id="452a9-182">[Azure 클래식 포털](http://manage.windowsazure.com/)에서 **클라우드 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-182">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**.</span></span> <span data-ttu-id="452a9-183">그런 다음 클라우드 서비스의 이름을 클릭하여 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-183">Then click the name of the cloud service to open the dashboard.</span></span>
2. <span data-ttu-id="452a9-184">**연결된 리소스**를 클릭한 후 리소스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-184">Click **Linked Resources**, and then select the resource.</span></span>
3. <span data-ttu-id="452a9-185">**연결 해제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-185">Click **Unlink**.</span></span> <span data-ttu-id="452a9-186">확인 메시지가 나타나면 **예** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-186">Then click **Yes** at the confirmation prompt.</span></span>

    <span data-ttu-id="452a9-187">SQL 데이터베이스 연결 해제는 데이터베이스 또는 데이터베이스와 응용 프로그램의 연결에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-187">Unlinking a SQL Database has no effect on the database or the application's connections to the database.</span></span> <span data-ttu-id="452a9-188">여전히 Azure 클래식 포털의 **SQL 데이터베이스** 영역에서 데이터베이스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-188">You can still manage the database in the **SQL Databases** area of the Azure classic portal.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="452a9-189">방법: 배포 및 클라우드 서비스 삭제</span><span class="sxs-lookup"><span data-stu-id="452a9-189">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="452a9-190">클라우드 서비스를 삭제하려면 먼저 각각의 기존 배포를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-190">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="452a9-191">계산 비용을 절약하려면 프로덕션 배포가 예상대로 작동한다는 것이 확인된 후 스테이징 배포를 삭제하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-191">To save compute costs, you can delete your staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="452a9-192">클라우드 서비스가 실행되고 있지 않은 경우에도 역할 인스턴스의 계산 비용이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-192">You are billed compute costs for role instances even if a cloud service is not running.</span></span>

<span data-ttu-id="452a9-193">배포 또는 클라우드 서비스를 삭제하려면 다음 절차를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="452a9-193">Use the following procedure to delete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="452a9-194">[Azure 클래식 포털](http://manage.windowsazure.com/)에서 **클라우드 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-194">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**.</span></span>
2. <span data-ttu-id="452a9-195">클라우드 서비스를 선택한 후 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-195">Select the cloud service, and then click **Delete**.</span></span> <span data-ttu-id="452a9-196">대시보드를 열지 않고 클라우드 서비스를 선택하려면 클라우드 서비스 항목에서 이름을 제외한 아무 위치나 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-196">(To select a cloud service without opening the dashboard, click anywhere except the name in the cloud service entry.)</span></span>

    <span data-ttu-id="452a9-197">스테이징 또는 프로덕션에 배포가 있는 경우 창 아래쪽에 다음과 비슷한 선택 메뉴가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-197">If you have a deployment in staging or production, you will see a menu of choices similar to the following one at the bottom of the window.</span></span> <span data-ttu-id="452a9-198">클라우드 서비스를 삭제하려면 먼저 기존 배포를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-198">Before you can delete the cloud service, you must delete any existing deployments.</span></span>

    ![삭제 메뉴](./media/cloud-services-how-to-manage/CloudServices_DeleteMenu.png)

3. <span data-ttu-id="452a9-200">배포를 삭제하려면 **Delete production deployment** 또는 **Delete staging deployment**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-200">To delete a deployment, click **Delete production deployment** or **Delete staging deployment**.</span></span> <span data-ttu-id="452a9-201">그리고 확인 메시지가 나타나면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-201">Then, at the confirmation prompt, click **Yes**.</span></span>
4. <span data-ttu-id="452a9-202">클라우드 서비스를 삭제할 계획이면 필요한 경우 3단계를 반복하여 다른 배포를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-202">If you plan to delete the cloud service, repeat step 3, if needed, to delete your other deployment.</span></span>
5. <span data-ttu-id="452a9-203">클라우드 서비스를 삭제하려면 **클라우드 서비스 삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-203">To delete the cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="452a9-204">그리고 확인 메시지가 나타나면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-204">Then, at the confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="452a9-205">클라우드 서비스에 대해 자세한 모니터링이 구성되어 있는 경우, 클라우드 서비스를 삭제해도 Azure는 저장소 계정에서 모니터링 데이터를 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-205">If verbose monitoring is configured for your cloud service, Azure does not delete the monitoring data from your storage account when you delete the cloud service.</span></span> <span data-ttu-id="452a9-206">이 데이터를 수동으로 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-206">You will need to delete the data manually.</span></span> <span data-ttu-id="452a9-207">메트릭 테이블이 있는 위치에 대한 자세한 내용은 [클라우드 서비스를 모니터링하는 방법](cloud-services-how-to-monitor.md)에서 "방법: Azure 클래식 포털 외부에서 자세한 모니터링 데이터 액세스"를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="452a9-207">For information about where to find the metrics tables, see "How to: Access verbose monitoring data outside the Azure classic portal" in [How to Monitor Cloud Services](cloud-services-how-to-monitor.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="452a9-208">다음 단계</span><span class="sxs-lookup"><span data-stu-id="452a9-208">Next steps</span></span>
* <span data-ttu-id="452a9-209">[클라우드 서비스의 일반 구성](cloud-services-how-to-configure.md)</span><span class="sxs-lookup"><span data-stu-id="452a9-209">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="452a9-210">[클라우드 서비스를 배포](cloud-services-how-to-create-deploy.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-210">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="452a9-211">[사용자 지정 도메인 이름](cloud-services-custom-domain-name.md)을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="452a9-211">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="452a9-212">[SSL 인증서](cloud-services-configure-ssl-certificate.md)구성</span><span class="sxs-lookup"><span data-stu-id="452a9-212">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>
