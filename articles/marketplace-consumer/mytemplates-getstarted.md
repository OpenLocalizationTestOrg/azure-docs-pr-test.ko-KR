---
title: "aaaGet 개인 템플릿으로 시작 | Microsoft Docs"
description: "추가, 관리 및 hello Azure 포털, hello Azure CLI 또는 PowerShell을 사용 하 여 개인 서식 파일을 공유 합니다."
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
ms.openlocfilehash: 1fe2c6422f62a98f7ae9ba5c61b9639d993f0bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-private-templates-on-hello-azure-portal"></a><span data-ttu-id="977af-103">Hello Azure 포털에 개인 템플릿으로 시작.</span><span class="sxs-lookup"><span data-stu-id="977af-103">Get started with private Templates on hello Azure Portal</span></span>
<span data-ttu-id="977af-104">[Azure 리소스 관리자](../azure-resource-manager/resource-group-authoring-templates.md) 템플릿은 선언적 템플릿을 사용 하 여 배포 toodefine입니다.</span><span class="sxs-lookup"><span data-stu-id="977af-104">An [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) template is a declarative template used toodefine your deployment.</span></span> <span data-ttu-id="977af-105">솔루션에 대 한 리소스 toodeploy hello를 정의 하 고 매개 변수 및 변수를 사용 하면 다양 한 환경에 대 한 tooinput 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="977af-105">You can define hello resources toodeploy for a solution, and specify parameters and variables that enable you tooinput values for different environments.</span></span> <span data-ttu-id="977af-106">hello 템플릿은 구성 JSON 및 사용할 수 있는 식의 배포에 대 한 tooconstruct 값입니다.</span><span class="sxs-lookup"><span data-stu-id="977af-106">hello template consists of JSON and expressions which you can use tooconstruct values for your deployment.</span></span>

<span data-ttu-id="977af-107">Hello를 새 사용할 수 있습니다 **템플릿** hello에서 기능 [Azure 포털](https://portal.azure.com) hello 함께 **Microsoft.Gallery** hello의 확장으로 리소스 공급자 [ Azure 마켓플레이스](https://azure.microsoft.com/marketplace/) tooenable 사용자 toocreate 관리 하 고 개인 라이브러리 개인 템플릿을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-107">You can use hello new **Templates** capability in hello [Azure Portal](https://portal.azure.com) along with hello **Microsoft.Gallery** resource provider as an extension of hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) tooenable users toocreate, manage and deploy private templates from a personal library.</span></span>

<span data-ttu-id="977af-108">이 문서에서는 추가, 관리 하 고 개인 공유 **템플릿** Azure 포털 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-108">This document walks you through adding, managing and sharing a private **Template** using hello Azure Portal.</span></span>

## <a name="guidance"></a><span data-ttu-id="977af-109">지침</span><span class="sxs-lookup"><span data-stu-id="977af-109">Guidance</span></span>
<span data-ttu-id="977af-110">hello 다음 제안 사항을 할 완전히 활용 **템플릿** 솔루션을 작업할 때:</span><span class="sxs-lookup"><span data-stu-id="977af-110">hello following suggestions will help you take full advantage of **Templates** when working with your solutions:</span></span>

* <span data-ttu-id="977af-111">**템플릿** 은 Resource Manager 템플릿 및 추가 메타데이터를 포함하는 캡슐화된 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="977af-111">A **Template** is an encapsulating resource that contains an Resource Manager template and additional metadata.</span></span> <span data-ttu-id="977af-112">Hello Marketplace에서에서 tooan 항목 매우 비슷하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-112">It behaves very similarly tooan item in hello Marketplace.</span></span> <span data-ttu-id="977af-113">주요 차이점 hello 것과 반대로 toohello 공용 마켓플레이스 항목으로 비공개 항목 된다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="977af-113">hello key difference is that it is a private item as opposed toohello public Marketplace items.</span></span>
* <span data-ttu-id="977af-114">hello **템플릿** 라이브러리 배포 toocustomize 해야 하는 사용자에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-114">hello **Templates** library works well for users who need toocustomize their deployments.</span></span>
* <span data-ttu-id="977af-115">**템플릿** 은 Azure 내에서 간단한 리포지토리가 필요한 사용자에 대해 제대로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-115">**Templates** work well for users who need a simple repository within Azure.</span></span>
* <span data-ttu-id="977af-116">기존 Resource Manager 템플릿으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-116">Start with an existing Resource Manager template.</span></span> <span data-ttu-id="977af-117">[github](https://github.com/Azure/azure-quickstart-templates)에서 템플릿을 찾거나 기존 리소스 그룹에서 [템플릿을 내보냅니다](../azure-resource-manager/resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="977af-117">Find templates in [github](https://github.com/Azure/azure-quickstart-templates) or [Export template](../azure-resource-manager/resource-manager-export-template.md) from an existing resource group.</span></span>
* <span data-ttu-id="977af-118">**템플릿** 동률된 toohello 사용자에 게 게시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="977af-118">**Templates** are tied toohello user who publishes them.</span></span> <span data-ttu-id="977af-119">hello 게시자 이름이 tooit 읽기 권한을 가진 tooeveryone 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="977af-119">hello publisher name is visible tooeveryone who has read access tooit.</span></span>
* <span data-ttu-id="977af-120">**템플릿** 은 Resource Manager 리소스이며 게시된 후에는 이름을 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="977af-120">**Templates** are Resource Manager resources and cannot be renamed once published.</span></span>

## <a name="add-a-template-resource"></a><span data-ttu-id="977af-121">템플릿 리소스 추가</span><span class="sxs-lookup"><span data-stu-id="977af-121">Add a Template resource</span></span>
<span data-ttu-id="977af-122">두 가지 방법으로 toocreate는 **템플릿** hello Azure 포털에서에서 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="977af-122">There are two ways toocreate a **Template** resource in hello Azure portal.</span></span>

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a><span data-ttu-id="977af-123">방법 1: 실행 중인 리소스 그룹에서 새 템플릿 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="977af-123">Method 1 : Create a new Template resource from a running resource group</span></span>
1. <span data-ttu-id="977af-124">Tooan hello Azure 포털에서 기존 리소스 그룹을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-124">Navigate tooan existing resource group on hello Azure Portal.</span></span> <span data-ttu-id="977af-125">**설정**에서 **템플릿 내보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-125">Select **Export template** in **Settings**.</span></span>
2. <span data-ttu-id="977af-126">Hello를 사용 하 여 hello 리소스 관리자 템플릿을 내보낸 후 **템플릿 저장** 단추 toosave 것 toohello **템플릿** 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="977af-126">Once hello Resource Manager template is exported, use hello **Save Template** button toosave it toohello **Templates** repository.</span></span> <span data-ttu-id="977af-127">템플릿 내보내기에 대한 전체 세부 정보는 [여기](../azure-resource-manager/resource-manager-export-template.md)에서 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="977af-127">Find complete details for Export template [here](../azure-resource-manager/resource-manager-export-template.md).</span></span>
   <br /><br /><span data-ttu-id="977af-128">
   ![리소스 그룹 내보내기](media/rg-export-portal1.PNG)</span><span class="sxs-lookup"><span data-stu-id="977af-128">
![Resource group export](media/rg-export-portal1.PNG)</span></span>  <br />
3. <span data-ttu-id="977af-129">선택 hello **tooTemplate 저장** 명령 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="977af-129">Select hello **Save tooTemplate** command button.</span></span>
   <br /><br />
4. <span data-ttu-id="977af-130">Hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-130">Enter hello following information:</span></span>
   
   * <span data-ttu-id="977af-131">이름-hello 템플릿 개체의 이름 (참고: Azure 리소스 관리자 기반 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="977af-131">Name – Name of hello template object (NOTE: This is an Azure Resource Manager based name.</span></span> <span data-ttu-id="977af-132">모든 명명 제한 사항을 적용하고 만든 후에는 변경할 수 없습니다).</span><span class="sxs-lookup"><span data-stu-id="977af-132">All naming restrictions apply and it cannot be changed once created).</span></span>
   * <span data-ttu-id="977af-133">설명 – hello 서식 파일에 대 한 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="977af-133">Description – Quick summary about hello template.</span></span>
     
     ![템플릿 저장](media/save-template-portal1.PNG)  <br />
5. <span data-ttu-id="977af-135">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-135">Click **Save**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="977af-136">hello 내보내기 템플릿 블레이드 알림을 표시 hello 리소스 관리자에서 내보낸된 템플릿에 오류가 있지만 수 toosave은 여전히이 리소스 관리자 템플릿 toohello 템플릿.</span><span class="sxs-lookup"><span data-stu-id="977af-136">hello Export template blade shows notifications when hello exported Resource Manager template has errors, but you will still be able toosave this Resource Manager template toohello Templates.</span></span> <span data-ttu-id="977af-137">확인 하 고 재배포 hello 리소스 관리자 템플릿 내보내기 전에 모든 리소스 관리자 템플릿 문제 해결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-137">Ensure that you check and fix any Resource Manager template issues before redeploying hello exported Resource Manager template.</span></span>
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a><span data-ttu-id="977af-138">방법 2: 찾아보기에서 새 템플릿 리소스 추가</span><span class="sxs-lookup"><span data-stu-id="977af-138">Method 2 : Add a new Template resource from browse</span></span>
<span data-ttu-id="977af-139">새 추가할 수 **템플릿** 안녕하세요 + 추가 명령 단추를 사용 하 여 처음부터 **찾아보기 > 템플릿**합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-139">You can also add a new **Template** from scratch using hello +Add command button in **Browse > Templates**.</span></span> <span data-ttu-id="977af-140">이름, 설명 및 리소스 관리자 템플릿 JSON hello tooprovide 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-140">You will need tooprovide a Name, Description and hello Resource Manager template JSON.</span></span>

![템플릿 추가](media/add-template-portal1.PNG)  <br />

> [!NOTE]
> <span data-ttu-id="977af-142">Microsoft.Gallery는 테넌트 기반 Azure 리소스 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="977af-142">Microsoft.Gallery is a Tenant based Azure resource provider.</span></span> <span data-ttu-id="977af-143">hello 템플릿 리소스는 동 점된 toohello 사용자 만든 사람입니다.</span><span class="sxs-lookup"><span data-stu-id="977af-143">hello Template resource is tied toohello user who created it.</span></span> <span data-ttu-id="977af-144">동 점된 tooany 특정 구독 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="977af-144">It is not tied tooany specific subscription.</span></span> <span data-ttu-id="977af-145">구독 toobe 서식 파일을 배포 하는 경우에 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-145">A subscription needs toobe chosen only when deploying a Template.</span></span>
> 
> 

## <a name="view-template-resources"></a><span data-ttu-id="977af-146">템플릿 리소스 보기</span><span class="sxs-lookup"><span data-stu-id="977af-146">View Template resources</span></span>
<span data-ttu-id="977af-147">모든 **템플릿** 에서 사용할 수 있는 tooyou를 볼 수 있습니다 **찾아보기 > 템플릿**합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-147">All **Templates** available tooyou can be seen at **Browse > Templates**.</span></span> <span data-ttu-id="977af-148">여기에는 만든 **템플릿** 과 다양한 수준의 권한으로 공유한 템플릿이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="977af-148">This includes **Templates** you have created as well as ones that have been shared with you with varying levels of permissions.</span></span> <span data-ttu-id="977af-149">Hello에 대 한 자세한 내용은 [액세스 제어](#access-control-for-a-tenant-resource-provider) 아래 섹션.</span><span class="sxs-lookup"><span data-stu-id="977af-149">More details in hello [access control](#access-control-for-a-tenant-resource-provider) section below.</span></span>

![템플릿 보기](media/view-template-portal1.PNG)  <br />

<span data-ttu-id="977af-151">hello 세부 정보를 볼 수는 **템플릿** hello 목록에서 항목을 클릭 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-151">You can view hello details of a **Template** by clicking into an item in hello list.</span></span>

![템플릿 보기](media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a><span data-ttu-id="977af-153">템플릿 리소스 편집</span><span class="sxs-lookup"><span data-stu-id="977af-153">Edit a Template resource</span></span>
<span data-ttu-id="977af-154">에 대 한 hello 편집 흐름을 시작할 수는 **템플릿** hello 항목 hello 브라우즈 목록에서 마우스 오른쪽 단추로 클릭 하 여 또는 hello 편집 명령 단추를 선택 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-154">You can initiate hello edit flow for a **Template** by right clicking hello item on hello Browse list or by choosing hello Edit command button.</span></span>

![템플릿 편집](media/edit-template-portal1a.PNG)  <br />

<span data-ttu-id="977af-156">Hello 설명 또는 리소스 관리자 템플릿 텍스트를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="977af-156">You can edit hello description or Resource Manager template text.</span></span> <span data-ttu-id="977af-157">리소스 관리자 리소스 이름 이므로 이름 hello를 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="977af-157">You cannot edit hello name since it is an Resource Manager resource name.</span></span> <span data-ttu-id="977af-158">JSON hello 리소스 관리자 템플릿을 편집할 때 tooensure 것은 유효한 JSON을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-158">When you edit hello Resource Manager template JSON we will validate tooensure that it is valid JSON.</span></span> <span data-ttu-id="977af-159">선택 **확인** 차례로 **저장** toosave 서식 파일에 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-159">Choose **OK** and then **Save** toosave your updated template.</span></span>

![템플릿 편집](media/edit-template-portal2a.PNG)  <br />

<span data-ttu-id="977af-161">한 번 hello **템플릿** 저장 된 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="977af-161">Once hello **Template** is saved you will see a confirmation notification.</span></span>

![템플릿 편집](media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a><span data-ttu-id="977af-163">템플릿 리소스 배포</span><span class="sxs-lookup"><span data-stu-id="977af-163">Deploy a Template resource</span></span>
<span data-ttu-id="977af-164">**읽기** 권한이 있는 **템플릿**을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="977af-164">You can deploy any **Template** that you have **Read** permissions on.</span></span> <span data-ttu-id="977af-165">hello 배포 흐름 hello 표준 Azure 템플릿 배포 블레이드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-165">hello deployment flow launches hello standard Azure Template deployment blade.</span></span> <span data-ttu-id="977af-166">Hello 배포와 함께 리소스 관리자 템플릿 매개 변수 tooproceed hello에 대 한 hello 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-166">Fill out hello values for hello Resource Manager template parameters tooproceed with hello deployment.</span></span>

![템플릿 배포](media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a><span data-ttu-id="977af-168">템플릿 리소스 공유</span><span class="sxs-lookup"><span data-stu-id="977af-168">Share a Template resource</span></span>
<span data-ttu-id="977af-169">**템플릿** 리소스를 동료와 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="977af-169">A **Template** resource can be shared with your peers.</span></span> <span data-ttu-id="977af-170">공유 비슷하게 너무[Azure에서 모든 리소스에 대 한 역할 할당](../active-directory/role-based-access-control-configure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-170">Sharing behaves similarly too[role assignment for any resource on Azure](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="977af-171">hello **템플릿** 소유자 권한을 tooother 사용자에 게 제공 상호 작용할 수 있는 템플릿 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="977af-171">hello **Template** owner provides permissions tooother users who can interact with a Template resource.</span></span> <span data-ttu-id="977af-172">hello 개인 또는 그룹 hello 공유 하는 사람의 **템플릿** 됩니다 수 toosee hello 리소스 관리자 템플릿 및 해당 갤러리 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="977af-172">hello person or group of people you share hello **Template** with will be able toosee hello Resource Manager template and its gallery properties.</span></span>

### <a name="access-control-for-hello-microsoftgallery-resources"></a><span data-ttu-id="977af-173">Hello Microsoft.Gallery 리소스에 대 한 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="977af-173">Access control for hello Microsoft.Gallery resources</span></span>
| <span data-ttu-id="977af-174">역할</span><span class="sxs-lookup"><span data-stu-id="977af-174">Role</span></span> | <span data-ttu-id="977af-175">권한</span><span class="sxs-lookup"><span data-stu-id="977af-175">Permissions</span></span> |
| --- | --- |
| <span data-ttu-id="977af-176">소유자</span><span class="sxs-lookup"><span data-stu-id="977af-176">Owner</span></span> |<span data-ttu-id="977af-177">공유를 포함 하 여 hello 템플릿 리소스에 대 한 모든 권한을 허용합니다</span><span class="sxs-lookup"><span data-stu-id="977af-177">Allows full control on hello Template resource including Share</span></span> |
| <span data-ttu-id="977af-178">읽기 권한자</span><span class="sxs-lookup"><span data-stu-id="977af-178">Reader</span></span> |<span data-ttu-id="977af-179">Hello 템플릿 리소스에서 읽기 및 Execute(Deploy) 허용</span><span class="sxs-lookup"><span data-stu-id="977af-179">Allows Read and Execute(Deploy) on hello Template resource</span></span> |
| <span data-ttu-id="977af-180">참여자</span><span class="sxs-lookup"><span data-stu-id="977af-180">Contributor</span></span> |<span data-ttu-id="977af-181">Hello 템플릿 리소스에 대 한 권한을 편집 및 삭제를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-181">Allows Edit and Delete permission on hello Template resource.</span></span> <span data-ttu-id="977af-182">사용자는 다른 사용자와 hello 서식 파일을 공유할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="977af-182">User cannot Share hello Template with others</span></span> |

<span data-ttu-id="977af-183">선택 **공유** 마우스 오른쪽 단추로 클릭 하 여 또는 특정 항목의 hello 보기 블레이드에서 hello 찾아보기 항목에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="977af-183">Select **Share** on hello browse item by right clicking or on hello view blade of a specific item.</span></span> <span data-ttu-id="977af-184">그러면 공유 환경이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="977af-184">This launches a Share experience.</span></span>

![템플릿 공유](media/share-template-portal1a.png)  <br />

 <span data-ttu-id="977af-186">이제 역할과 사용자 또는 그룹 tooprovide 액세스 tooa 특정를 선택할 수 있습니다 **템플릿**합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-186">You can now choose a role and a user or group tooprovide access tooa particular **Template**.</span></span> <span data-ttu-id="977af-187">hello 사용 가능한 역할 소유자, 독자 및 참가자 됩니다.</span><span class="sxs-lookup"><span data-stu-id="977af-187">hello available roles are Owner, Reader and Contributor.</span></span> <span data-ttu-id="977af-188">Hello에 대 한 자세한 내용은 [액세스 제어](#access-control-for-a-tenant-resource-provider) 위의 섹션.</span><span class="sxs-lookup"><span data-stu-id="977af-188">More details in hello [access control](#access-control-for-a-tenant-resource-provider) section above.</span></span>

![템플릿 공유](media/share-template-portal2b.png)  <br />

![템플릿 공유](media/share-template-portal3b.png)  <br />

<span data-ttu-id="977af-191">**선택** 및 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-191">Click **Select** and **Ok**.</span></span> <span data-ttu-id="977af-192">Hello 사용자 또는 그룹 표시 toohello 리소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="977af-192">You can now see hello users or groups you added toohello resource.</span></span>

![템플릿 공유](media/share-template-portal4b.png)  <br />

> [!NOTE]
> <span data-ttu-id="977af-194">서식 파일만 공유할 수는 사용자 및 그룹 hello 동일한 Azure Active Directory 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="977af-194">A Template can only be shared with users and groups in hello same Azure Active Directory tenant.</span></span> <span data-ttu-id="977af-195">테 넌 트에 있지 않은 전자 메일 주소가 있는 서식 파일을 공유 하는 경우 요청 hello 사용자 toojoin hello 테 넌 트에 게스트로 초대 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="977af-195">If you share a Template with an email address that is not in your tenant, an invitation will be sent asking hello user toojoin hello tenant as a guest.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="977af-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="977af-196">Next steps</span></span>
* <span data-ttu-id="977af-197">리소스 관리자 템플릿을 만드는 방법에 대해 toolearn 참조 [템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="977af-197">toolearn about creating Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="977af-198">리소스 관리자 서식 파일에서 사용 가능한 toounderstand hello 함수 참조 [템플릿 함수](../azure-resource-manager/resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="977af-198">toounderstand hello functions you can use in an Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md)</span></span>
* <span data-ttu-id="977af-199">템플릿 설계에 대한 지침은 [Azure 리소스 관리자 템플릿 설계의 모범 사례](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span><span class="sxs-lookup"><span data-stu-id="977af-199">For guidance on designing your templates, see [Best practices for designing Azure Resource Manager templates](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span></span>

