---
title: "개인 템플릿을 사용하여 시작 | Microsoft Docs"
description: "Azure 포털, Azure CLI, PowerShell을 사용하여 개인 템플릿을 추가, 관리 및 공유합니다."
services: marketplace-customer
documentationcenter: 
author: VybavaRamadoss
manager: asimm
editor: 
tags: marketplace, azure-resource-manager
keywords: 
ms.assetid: 6ec20778-b578-4885-acb5-104b0e51ea1a
ms.service: marketplace
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: vybavar
ms.openlocfilehash: 01657619cbe579c6818a790cc3ab95a33936a565
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-private-templates-on-the-azure-portal"></a><span data-ttu-id="bb96f-103">Azure 포털에서 개인 템플릿을 사용하여 시작</span><span class="sxs-lookup"><span data-stu-id="bb96f-103">Get started with private Templates on the Azure Portal</span></span>
<span data-ttu-id="bb96f-104">[Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) 템플릿은 배포를 정의하는 데 사용된 선언적 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-104">An [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) template is a declarative template used to define your deployment.</span></span> <span data-ttu-id="bb96f-105">솔루션에 대해 배포할 리소스를 정의하고, 여러 환경의 값을 입력하는 데 사용할 수 있는 변수 및 매개 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-105">You can define the resources to deploy for a solution, and specify parameters and variables that enable you to input values for different environments.</span></span> <span data-ttu-id="bb96f-106">템플릿은 배포에 대한 값을 생성하는 데 사용할 수 있는 식과 JSON으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-106">The template consists of JSON and expressions which you can use to construct values for your deployment.</span></span>

<span data-ttu-id="bb96f-107">[Azure Portal](https://portal.azure.com)에서 [Azure Marketplace](https://azure.microsoft.com/marketplace/)의 확장으로 **Microsoft.Gallery** 리소스 공급자와 함께 새 **템플릿** 기능을 사용하여 사용자가 개인 라이브러리에서 개인 템플릿을 만들고 관리하며 배포하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-107">You can use the new **Templates** capability in the [Azure Portal](https://portal.azure.com) along with the **Microsoft.Gallery** resource provider as an extension of the [Azure Marketplace](https://azure.microsoft.com/marketplace/) to enable users to create, manage and deploy private templates from a personal library.</span></span>

<span data-ttu-id="bb96f-108">이 문서는 Azure 포털을 사용하여 개인 **템플릿** 을 추가, 관리 및 공유하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-108">This document walks you through adding, managing and sharing a private **Template** using the Azure Portal.</span></span>

## <a name="guidance"></a><span data-ttu-id="bb96f-109">지침</span><span class="sxs-lookup"><span data-stu-id="bb96f-109">Guidance</span></span>
<span data-ttu-id="bb96f-110">다음 제안으로 솔루션으로 작업할 때 **템플릿** 을 완벽하게 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-110">The following suggestions will help you take full advantage of **Templates** when working with your solutions:</span></span>

* <span data-ttu-id="bb96f-111">**템플릿** 은 Resource Manager 템플릿 및 추가 메타데이터를 포함하는 캡슐화된 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-111">A **Template** is an encapsulating resource that contains an Resource Manager template and additional metadata.</span></span> <span data-ttu-id="bb96f-112">마켓플레이스에 있는 항목과 매우 비슷하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-112">It behaves very similarly to an item in the Marketplace.</span></span> <span data-ttu-id="bb96f-113">주요 차이점은 공용 마켓플레이스 항목이 아니라 비공개 항목이라는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-113">The key difference is that it is a private item as opposed to the public Marketplace items.</span></span>
* <span data-ttu-id="bb96f-114">**템플릿** 라이브러리는 자신의 배포를 사용자 지정해야 하는 사용자에 대해 제대로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-114">The **Templates** library works well for users who need to customize their deployments.</span></span>
* <span data-ttu-id="bb96f-115">**템플릿** 은 Azure 내에서 간단한 리포지토리가 필요한 사용자에 대해 제대로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-115">**Templates** work well for users who need a simple repository within Azure.</span></span>
* <span data-ttu-id="bb96f-116">기존 Resource Manager 템플릿으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-116">Start with an existing Resource Manager template.</span></span> <span data-ttu-id="bb96f-117">[github](https://github.com/Azure/azure-quickstart-templates)에서 템플릿을 찾거나 기존 리소스 그룹에서 [템플릿을 내보냅니다](../azure-resource-manager/resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="bb96f-117">Find templates in [github](https://github.com/Azure/azure-quickstart-templates) or [Export template](../azure-resource-manager/resource-manager-export-template.md) from an existing resource group.</span></span>
* <span data-ttu-id="bb96f-118">**템플릿** 은 템플릿을 게시하는 사용자와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-118">**Templates** are tied to the user who publishes them.</span></span> <span data-ttu-id="bb96f-119">게시자 이름은 읽기 액세스 권한이 있는 모든 사람에게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-119">The publisher name is visible to everyone who has read access to it.</span></span>
* <span data-ttu-id="bb96f-120">**템플릿** 은 Resource Manager 리소스이며 게시된 후에는 이름을 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-120">**Templates** are Resource Manager resources and cannot be renamed once published.</span></span>

## <a name="add-a-template-resource"></a><span data-ttu-id="bb96f-121">템플릿 리소스 추가</span><span class="sxs-lookup"><span data-stu-id="bb96f-121">Add a Template resource</span></span>
<span data-ttu-id="bb96f-122">Azure 포털에서 **템플릿** 리소스를 만드는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-122">There are two ways to create a **Template** resource in the Azure portal.</span></span>

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a><span data-ttu-id="bb96f-123">방법 1: 실행 중인 리소스 그룹에서 새 템플릿 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="bb96f-123">Method 1 : Create a new Template resource from a running resource group</span></span>
1. <span data-ttu-id="bb96f-124">Azure 포털에서 기존 리소스 그룹으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-124">Navigate to an existing resource group on the Azure Portal.</span></span> <span data-ttu-id="bb96f-125">**설정**에서 **템플릿 내보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-125">Select **Export template** in **Settings**.</span></span>
2. <span data-ttu-id="bb96f-126">Resource Manager 템플릿을 내보낸 후는 **템플릿 저장** 단추를 사용하여 **템플릿** 리포지토리에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-126">Once the Resource Manager template is exported, use the **Save Template** button to save it to the **Templates** repository.</span></span> <span data-ttu-id="bb96f-127">템플릿 내보내기에 대한 전체 세부 정보는 [여기](../azure-resource-manager/resource-manager-export-template.md)에서 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="bb96f-127">Find complete details for Export template [here](../azure-resource-manager/resource-manager-export-template.md).</span></span>
   <br /><br /><span data-ttu-id="bb96f-128">
   ![리소스 그룹 내보내기](media/rg-export-portal1.PNG)</span><span class="sxs-lookup"><span data-stu-id="bb96f-128">
![Resource group export](media/rg-export-portal1.PNG)</span></span>  <br />
3. <span data-ttu-id="bb96f-129">**템플릿에 저장** 명령 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-129">Select the **Save to Template** command button.</span></span>
   <br /><br />
4. <span data-ttu-id="bb96f-130">다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-130">Enter the following information:</span></span>
   
   * <span data-ttu-id="bb96f-131">이름 – 템플릿 개체의 이름(참고: Azure Resource Manager 기반 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-131">Name – Name of the template object (NOTE: This is an Azure Resource Manager based name.</span></span> <span data-ttu-id="bb96f-132">모든 명명 제한 사항을 적용하고 만든 후에는 변경할 수 없습니다).</span><span class="sxs-lookup"><span data-stu-id="bb96f-132">All naming restrictions apply and it cannot be changed once created).</span></span>
   * <span data-ttu-id="bb96f-133">설명 – 템플릿에 대한 간단한 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-133">Description – Quick summary about the template.</span></span>
     
     ![템플릿 저장](media/save-template-portal1.PNG)  <br />
5. <span data-ttu-id="bb96f-135">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-135">Click **Save**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bb96f-136">내보낸 Resource Manager 템플릿에 오류가 있는 경우 내보내기 템플릿 블레이드에 알림이 표시되지만 이 Resource Manager 템플릿을 해당 템플릿에 계속 저장할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-136">The Export template blade shows notifications when the exported Resource Manager template has errors, but you will still be able to save this Resource Manager template to the Templates.</span></span> <span data-ttu-id="bb96f-137">내보낸 Resource Manager 템플릿을 다시 배포하기 전에 Resource Manager 템플릿 문제를 확인하여 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-137">Ensure that you check and fix any Resource Manager template issues before redeploying the exported Resource Manager template.</span></span>
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a><span data-ttu-id="bb96f-138">방법 2: 찾아보기에서 새 템플릿 리소스 추가</span><span class="sxs-lookup"><span data-stu-id="bb96f-138">Method 2 : Add a new Template resource from browse</span></span>
<span data-ttu-id="bb96f-139">**찾아보기 > 템플릿**에서 +추가 명령 단추를 사용하여 처음부터 새 **템플릿**을 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-139">You can also add a new **Template** from scratch using the +Add command button in **Browse > Templates**.</span></span> <span data-ttu-id="bb96f-140">이름, 설명 및 Resource Manager 템플릿 JSON을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-140">You will need to provide a Name, Description and the Resource Manager template JSON.</span></span>

![템플릿 추가](media/add-template-portal1.PNG)  <br />

> [!NOTE]
> <span data-ttu-id="bb96f-142">Microsoft.Gallery는 테넌트 기반 Azure 리소스 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-142">Microsoft.Gallery is a Tenant based Azure resource provider.</span></span> <span data-ttu-id="bb96f-143">템플릿 리소스는 리소스를 만든 사용자와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-143">The Template resource is tied to the user who created it.</span></span> <span data-ttu-id="bb96f-144">특정 구독에 연결되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-144">It is not tied to any specific subscription.</span></span> <span data-ttu-id="bb96f-145">구독은 템플릿을 배포하는 경우에만 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-145">A subscription needs to be chosen only when deploying a Template.</span></span>
> 
> 

## <a name="view-template-resources"></a><span data-ttu-id="bb96f-146">템플릿 리소스 보기</span><span class="sxs-lookup"><span data-stu-id="bb96f-146">View Template resources</span></span>
<span data-ttu-id="bb96f-147">사용 가능한 모든 **템플릿**은 **찾아보기 > 템플릿**에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-147">All **Templates** available to you can be seen at **Browse > Templates**.</span></span> <span data-ttu-id="bb96f-148">여기에는 만든 **템플릿** 과 다양한 수준의 권한으로 공유한 템플릿이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-148">This includes **Templates** you have created as well as ones that have been shared with you with varying levels of permissions.</span></span> <span data-ttu-id="bb96f-149">자세한 정보는 아래 [액세스 제어](#access-control-for-a-tenant-resource-provider) 섹션에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-149">More details in the [access control](#access-control-for-a-tenant-resource-provider) section below.</span></span>

![템플릿 보기](media/view-template-portal1.PNG)  <br />

<span data-ttu-id="bb96f-151">목록에 있는 항목을 클릭하여 **템플릿** 에 대한 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-151">You can view the details of a **Template** by clicking into an item in the list.</span></span>

![템플릿 보기](media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a><span data-ttu-id="bb96f-153">템플릿 리소스 편집</span><span class="sxs-lookup"><span data-stu-id="bb96f-153">Edit a Template resource</span></span>
<span data-ttu-id="bb96f-154">찾아보기 목록에서 항목을 마우스 오른쪽 단추로 클릭하거나 편집 명령 단추를 선택하여 **템플릿** 에 대한 편집 흐름을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-154">You can initiate the edit flow for a **Template** by right clicking the item on the Browse list or by choosing the Edit command button.</span></span>

![템플릿 편집](media/edit-template-portal1a.PNG)  <br />

<span data-ttu-id="bb96f-156">설명 또는 Resource Manager 템플릿 텍스트를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-156">You can edit the description or Resource Manager template text.</span></span> <span data-ttu-id="bb96f-157">Resource Manager 리소스 이름이기 때문에 이름은 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-157">You cannot edit the name since it is an Resource Manager resource name.</span></span> <span data-ttu-id="bb96f-158">Resource Manager 템플릿 JSON을 편집할 때 유효한 JSON인지 확인하기 위해 유효성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-158">When you edit the Resource Manager template JSON we will validate to ensure that it is valid JSON.</span></span> <span data-ttu-id="bb96f-159">**확인**을 선택한 후 **저장**을 선택하여 업데이트된 템플릿을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-159">Choose **OK** and then **Save** to save your updated template.</span></span>

![템플릿 편집](media/edit-template-portal2a.PNG)  <br />

<span data-ttu-id="bb96f-161">**템플릿** 이 저장된 후에는 확인 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-161">Once the **Template** is saved you will see a confirmation notification.</span></span>

![템플릿 편집](media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a><span data-ttu-id="bb96f-163">템플릿 리소스 배포</span><span class="sxs-lookup"><span data-stu-id="bb96f-163">Deploy a Template resource</span></span>
<span data-ttu-id="bb96f-164">**읽기** 권한이 있는 **템플릿**을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-164">You can deploy any **Template** that you have **Read** permissions on.</span></span> <span data-ttu-id="bb96f-165">배포 흐름에서 표준 Azure 템플릿을 배포 블레이드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-165">The deployment flow launches the standard Azure Template deployment blade.</span></span> <span data-ttu-id="bb96f-166">배포를 진행하기 위해 Resource Manager 템플릿 매개 변수의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-166">Fill out the values for the Resource Manager template parameters to proceed with the deployment.</span></span>

![템플릿 배포](media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a><span data-ttu-id="bb96f-168">템플릿 리소스 공유</span><span class="sxs-lookup"><span data-stu-id="bb96f-168">Share a Template resource</span></span>
<span data-ttu-id="bb96f-169">**템플릿** 리소스를 동료와 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-169">A **Template** resource can be shared with your peers.</span></span> <span data-ttu-id="bb96f-170">공유는 [Azure에서 모든 리소스에 대한 역할 할당](../active-directory/role-based-access-control-configure.md)과 유사하게 동작합니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-170">Sharing behaves similarly to [role assignment for any resource on Azure](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="bb96f-171">**템플릿** 소유자는 템플릿 리소스와 상호 작용할 수 있는 다른 사용자에게 사용 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-171">The **Template** owner provides permissions to other users who can interact with a Template resource.</span></span> <span data-ttu-id="bb96f-172">**템플릿** 을 공유하는 개인 또는 사용자 그룹은 Resource Manager 템플릿 및 해당 갤러리 속성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-172">The person or group of people you share the **Template** with will be able to see the Resource Manager template and its gallery properties.</span></span>

### <a name="access-control-for-the-microsoftgallery-resources"></a><span data-ttu-id="bb96f-173">Microsoft.Gallery 리소스에 대한 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="bb96f-173">Access control for the Microsoft.Gallery resources</span></span>
| <span data-ttu-id="bb96f-174">역할</span><span class="sxs-lookup"><span data-stu-id="bb96f-174">Role</span></span> | <span data-ttu-id="bb96f-175">권한</span><span class="sxs-lookup"><span data-stu-id="bb96f-175">Permissions</span></span> |
| --- | --- |
| <span data-ttu-id="bb96f-176">소유자</span><span class="sxs-lookup"><span data-stu-id="bb96f-176">Owner</span></span> |<span data-ttu-id="bb96f-177">공유를 포함하여 템플릿 리소스에 대한 모든 권한 허용</span><span class="sxs-lookup"><span data-stu-id="bb96f-177">Allows full control on the Template resource including Share</span></span> |
| <span data-ttu-id="bb96f-178">판독기</span><span class="sxs-lookup"><span data-stu-id="bb96f-178">Reader</span></span> |<span data-ttu-id="bb96f-179">템플릿 리소스에 대한 읽기 및 실행(배포) 허용</span><span class="sxs-lookup"><span data-stu-id="bb96f-179">Allows Read and Execute(Deploy) on the Template resource</span></span> |
| <span data-ttu-id="bb96f-180">참여자</span><span class="sxs-lookup"><span data-stu-id="bb96f-180">Contributor</span></span> |<span data-ttu-id="bb96f-181">템플릿 리소스에 대한 편집 및 삭제 권한 허용.</span><span class="sxs-lookup"><span data-stu-id="bb96f-181">Allows Edit and Delete permission on the Template resource.</span></span> <span data-ttu-id="bb96f-182">사용자는 다른 사용자와 템플릿을 공유할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-182">User cannot Share the Template with others</span></span> |

<span data-ttu-id="bb96f-183">마우스 오른쪽 단추를 클릭하면 표시되는 찾아보기 항목이나 특정 항목의 보기 블레이드에서 **공유** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-183">Select **Share** on the browse item by right clicking or on the view blade of a specific item.</span></span> <span data-ttu-id="bb96f-184">그러면 공유 환경이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-184">This launches a Share experience.</span></span>

![템플릿 공유](media/share-template-portal1a.png)  <br />

 <span data-ttu-id="bb96f-186">이제 특정 **템플릿**에 대한 액세스를 제공하는 데 역할, 사용자 또는 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-186">You can now choose a role and a user or group to provide access to a particular **Template**.</span></span> <span data-ttu-id="bb96f-187">사용 가능한 역할은 소유자, 판독기 및 참가자입니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-187">The available roles are Owner, Reader and Contributor.</span></span> <span data-ttu-id="bb96f-188">자세한 정보는 위의 [액세스 제어](#access-control-for-a-tenant-resource-provider) 섹션에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-188">More details in the [access control](#access-control-for-a-tenant-resource-provider) section above.</span></span>

![템플릿 공유](media/share-template-portal2b.png)  <br />

![템플릿 공유](media/share-template-portal3b.png)  <br />

<span data-ttu-id="bb96f-191">**선택** 및 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-191">Click **Select** and **Ok**.</span></span> <span data-ttu-id="bb96f-192">이제 리소스에 추가된 사용자 또는 그룹을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-192">You can now see the users or groups you added to the resource.</span></span>

![템플릿 공유](media/share-template-portal4b.png)  <br />

> [!NOTE]
> <span data-ttu-id="bb96f-194">템플릿은 동일한 Azure Active Directory 테넌트의 사용자 및 그룹과만 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-194">A Template can only be shared with users and groups in the same Azure Active Directory tenant.</span></span> <span data-ttu-id="bb96f-195">테넌트에 없는 전자 메일 주소와 템플릿을 공유하는 경우 사용자에게 게스트로 테넌트에 가입하라는 초대가 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb96f-195">If you share a Template with an email address that is not in your tenant, an invitation will be sent asking the user to join the tenant as a guest.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="bb96f-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bb96f-196">Next steps</span></span>
* <span data-ttu-id="bb96f-197">Resource Manager 템플릿을 만드는 방법에 대한 자세한 내용은 [템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="bb96f-197">To learn about creating Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="bb96f-198">Resource Manager 템플릿에서 사용할 수 있는 함수를 이해하려면 [템플릿 함수](../azure-resource-manager/resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="bb96f-198">To understand the functions you can use in an Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md)</span></span>
* <span data-ttu-id="bb96f-199">템플릿 설계에 대한 지침은 [Azure 리소스 관리자 템플릿 설계의 모범 사례](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span><span class="sxs-lookup"><span data-stu-id="bb96f-199">For guidance on designing your templates, see [Best practices for designing Azure Resource Manager templates](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span></span>

