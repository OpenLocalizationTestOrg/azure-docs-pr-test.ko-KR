---
title: "Azure aaaDelete 클러스터와 해당 리소스 | Microsoft Docs"
description: "방법 toocompletely 삭제 서비스 패브릭 클러스터 hello 클러스터를 포함 하 되 중 하나가 삭제 hello 리소스 그룹 또는 리소스를 선택적으로 삭제 하 여에 대해 알아봅니다."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: de422950-2d22-4ddb-ac47-dd663a946a7e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/24/2017
ms.author: chackdan
ms.openlocfilehash: 5c15a4184644da715cd69397f2150de86ab433ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-hello-resources-it-uses"></a><span data-ttu-id="e31f5-103">Azure 및 hello 리소스를 사용 하 여 서비스 패브릭 클러스터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-103">Delete a Service Fabric cluster on Azure and hello resources it uses</span></span>
<span data-ttu-id="e31f5-104">서비스 패브릭 클러스터 구성 된 다양 한 Azure 리소스 뿐만 아니라 자체 toohello 클러스터 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-104">A Service Fabric cluster is made up of many other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="e31f5-105">Toocompletely 서비스 패브릭 클러스터를 삭제 하므로 toodelete 모든 hello 리소스 구성 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-105">So toocompletely delete a Service Fabric cluster you also need toodelete all hello resources it is made of.</span></span>
<span data-ttu-id="e31f5-106">두 가지 옵션이 있습니다:에 클러스터 hello 중 하나가 삭제 hello 리소스 그룹이 (삭제 하 hello 클러스터 리소스 및 hello 리소스 그룹의 다른 리소스) 또는 특히 hello 클러스터 리소스를 삭제 하 고 리소스에 연결 (다른 하지 않음 에서 리소스 hello 리소스 그룹)입니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-106">You have two options: Either delete hello resource group that hello cluster is in (which deletes hello cluster resource and any other resources in hello resource group) or specifically delete hello cluster resource and it's associated resources (but not other resources in hello resource group).</span></span>

> [!NOTE]
> <span data-ttu-id="e31f5-107">Hello 클러스터 리소스를 삭제 **없는** 서비스 패브릭 클러스터는 구성 하는 다른 리소스를 hello 모두 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-107">Deleting hello cluster resource **does not** delete all hello other resources that your Service Fabric cluster is composed of.</span></span>
> 
> 

## <a name="delete-hello-entire-resource-group-rg-that-hello-service-fabric-cluster-is-in"></a><span data-ttu-id="e31f5-108">서비스 패브릭 클러스터에는 hello hello 전체 리소스 그룹 (RG)를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-108">Delete hello entire resource group (RG) that hello Service Fabric cluster is in</span></span>
<span data-ttu-id="e31f5-109">이 hello hello 리소스 그룹을 포함 하 여 클러스터와 연결 된 모든 hello 리소스를 삭제 하는 가장 쉬운 방법은 tooensure입니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-109">This is hello easiest way tooensure that you delete all hello resources associated with your cluster, including hello resource group.</span></span> <span data-ttu-id="e31f5-110">PowerShell을 사용 하 여 hello 리소스 그룹을 삭제할 수 있습니다 또는 hello Azure 포털을 통해.</span><span class="sxs-lookup"><span data-stu-id="e31f5-110">You can delete hello resource group using PowerShell or through hello Azure portal.</span></span> <span data-ttu-id="e31f5-111">리소스 그룹 관련된 tooService 패브릭 클러스터 되지 않은 리소스가 있는 경우, 특정 리소스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-111">If your resource group has resources that are not related tooService fabric cluster, then you can delete specific resources.</span></span>

### <a name="delete-hello-resource-group-using-azure-powershell"></a><span data-ttu-id="e31f5-112">Azure PowerShell을 사용 하 여 hello 리소스 그룹 삭제</span><span class="sxs-lookup"><span data-stu-id="e31f5-112">Delete hello resource group using Azure PowerShell</span></span>
<span data-ttu-id="e31f5-113">Hello 다음 Azure PowerShell cmdlet을 실행 하 여 hello 리소스 그룹을 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-113">You can also delete hello resource group by running hello following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="e31f5-114">컴퓨터에 Azure PowerShell 1.0 이상이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-114">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="e31f5-115">이전 수행 하지 않은 경우에 설명 된 hello 단계에 따라 [어떻게 tooinstall 및 Azure PowerShell을 구성 합니다.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="e31f5-115">If you have not done this before, follow hello steps outlined in [How tooinstall and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="e31f5-116">PowerShell 창을 열고 hello 다음 PS cmdlet을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-116">Open a PowerShell window and run hello following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

<span data-ttu-id="e31f5-117">Hello를 사용 하지 않은 경우 프롬프트 tooconfirm hello 삭제 받아볼 수 *-Force* 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-117">You will get a prompt tooconfirm hello deletion if you did not use hello *-Force* option.</span></span> <span data-ttu-id="e31f5-118">Hello RG에서 확인 하 고 포함 된 모든 hello 리소스 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-118">On confirmation hello RG and all hello resources it contains are deleted.</span></span>

### <a name="delete-a-resource-group-in-hello-azure-portal"></a><span data-ttu-id="e31f5-119">Hello Azure 포털에에서 있는 리소스 그룹 삭제</span><span class="sxs-lookup"><span data-stu-id="e31f5-119">Delete a resource group in hello Azure portal</span></span>
1. <span data-ttu-id="e31f5-120">로그인 toohello [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-120">Login toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e31f5-121">원하는 toodelete toohello 서비스 패브릭 클러스터를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-121">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
3. <span data-ttu-id="e31f5-122">Hello hello 클러스터 essentials 페이지에서 리소스 그룹 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-122">Click on hello Resource Group name on hello cluster essentials page.</span></span>
4. <span data-ttu-id="e31f5-123">그러면 hello **리소스 그룹 Essentials** 페이지.</span><span class="sxs-lookup"><span data-stu-id="e31f5-123">This brings up hello **Resource Group Essentials** page.</span></span>
5. <span data-ttu-id="e31f5-124">**삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-124">Click **Delete**.</span></span>
6. <span data-ttu-id="e31f5-125">Hello 리소스 그룹의 해당 페이지 toocomplete hello 삭제 시 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-125">Follow hello instructions on that page toocomplete hello deletion of hello resource group.</span></span>

![리소스 그룹 삭제][ResourceGroupDelete]

## <a name="delete-hello-cluster-resource-and-hello-resources-it-uses-but-not-other-resources-in-hello-resource-group"></a><span data-ttu-id="e31f5-127">삭제 hello 클러스터 리소스 및를 사용 하는 hello 리소스 있지만 hello 리소스 그룹의 다른 리소스에 없습니다</span><span class="sxs-lookup"><span data-stu-id="e31f5-127">Delete hello cluster resource and hello resources it uses, but not other resources in hello resource group</span></span>
<span data-ttu-id="e31f5-128">리소스 그룹에 리소스를 관련된 toohello 서비스 패브릭 클러스터 toodelete, 원하는 경우 보다 쉽게 toodelete hello 전체 리소스 그룹.</span><span class="sxs-lookup"><span data-stu-id="e31f5-128">If your resource group has only resources that are related toohello Service Fabric cluster you want toodelete, then it is easier toodelete hello entire resource group.</span></span> <span data-ttu-id="e31f5-129">리소스 그룹의 tooselectively delete hello 리소스 여 하나씩을 하려는 경우에 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-129">If you want tooselectively delete hello resources one-by-one in your resource group, then follow these steps.</span></span>

<span data-ttu-id="e31f5-130">Hello 서비스 패브릭 리소스 관리자 템플릿 중 하나를 사용 하 여 hello 템플릿 갤러리에서 또는 hello 포털을 사용 하 여 클러스터를 배포한 경우 다음 모든 hello 리소스 클러스터 사용 하 여 hello를 태그로 지정 됩니다 hello 두 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-130">If you deployed your cluster using hello portal or using one of hello Service Fabric Resource Manager templates from hello template gallery, then all hello resources that hello cluster uses are tagged with hello following two tags.</span></span> <span data-ttu-id="e31f5-131">원하는 어떤 리소스 toodecide 사용할 수 toodelete 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-131">You can use them toodecide which resources you want toodelete.</span></span>

<span data-ttu-id="e31f5-132">***태그 #1:*** 키 = clusterName, 값 = 'hello 클러스터의 이름'</span><span class="sxs-lookup"><span data-stu-id="e31f5-132">***Tag#1:*** Key = clusterName, Value = 'name of hello cluster'</span></span>

<span data-ttu-id="e31f5-133">***Tag#2:*** 키 = resourceName, 값 = ServiceFabric</span><span class="sxs-lookup"><span data-stu-id="e31f5-133">***Tag#2:*** Key = resourceName, Value = ServiceFabric</span></span>

### <a name="delete-specific-resources-in-hello-azure-portal"></a><span data-ttu-id="e31f5-134">Hello Azure 포털의에서 특정 리소스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-134">Delete specific resources in hello Azure portal</span></span>
1. <span data-ttu-id="e31f5-135">로그인 toohello [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-135">Login toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e31f5-136">원하는 toodelete toohello 서비스 패브릭 클러스터를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-136">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
3. <span data-ttu-id="e31f5-137">너무 이동**모든 설정을** hello essentials 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-137">Go too**All settings** on hello essentials blade.</span></span>
4. <span data-ttu-id="e31f5-138">클릭 **태그** 아래 **리소스 관리** hello 설정 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-138">Click on **Tags** under **Resource Management** in hello settings blade.</span></span>
5. <span data-ttu-id="e31f5-139">Hello 중 하나를 클릭 **태그** hello 태그 블레이드 tooget 태그가 있는 모든 hello 리소스 목록에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-139">Click on one of hello **Tags** in hello tags blade tooget a list of all hello resources with that tag.</span></span>
   
    ![리소스 태그][ResourceTags]
6. <span data-ttu-id="e31f5-141">태그가 지정 된 리소스 목록이 hello를 만든 후 각 hello 리소스 클릭 하 고 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-141">Once you have hello list of tagged resources, click on each of hello resources and delete them.</span></span>
   
    ![태그가 지정된 리소스][TaggedResources]

### <a name="delete-hello-resources-using-azure-powershell"></a><span data-ttu-id="e31f5-143">Azure PowerShell을 사용 하 여 hello 리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="e31f5-143">Delete hello resources using Azure PowerShell</span></span>
<span data-ttu-id="e31f5-144">Hello 리소스 여 하나씩 hello 다음 Azure PowerShell cmdlet을 실행 하 여 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-144">You can delete hello resources one-by-one by running hello following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="e31f5-145">컴퓨터에 Azure PowerShell 1.0 이상이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-145">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="e31f5-146">이전 수행 하지 않은 경우에 설명 된 hello 단계에 따라 [어떻게 tooinstall 및 Azure PowerShell을 구성 합니다.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="e31f5-146">If you have not done this before, follow hello steps outlined in [How tooinstall and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="e31f5-147">PowerShell 창을 열고 hello 다음 PS cmdlet을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e31f5-147">Open a PowerShell window and run hello following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="e31f5-148">각 hello 리소스에 대 한 원하는 toodelete를 hello 다음 실행:</span><span class="sxs-lookup"><span data-stu-id="e31f5-148">For each of hello resources you want toodelete, run hello following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of hello resource group>" -Force
```

<span data-ttu-id="e31f5-149">toodelete hello 클러스터 리소스를 hello 다음 실행:</span><span class="sxs-lookup"><span data-stu-id="e31f5-149">toodelete hello cluster resource, run hello following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of hello resource group>" -Force
```

## <a name="next-steps"></a><span data-ttu-id="e31f5-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e31f5-150">Next steps</span></span>
<span data-ttu-id="e31f5-151">클러스터 업그레이드 및 서비스를 분할 하는 방법에 대 한 자세한 내용은 tooalso 다음 읽기 hello:</span><span class="sxs-lookup"><span data-stu-id="e31f5-151">Read hello following tooalso learn about upgrading a cluster and partitioning services:</span></span>

* [<span data-ttu-id="e31f5-152">클러스터 업그레이드 알아보기</span><span class="sxs-lookup"><span data-stu-id="e31f5-152">Learn about cluster upgrades</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="e31f5-153">최대 크기를 위해 상태 저장 서비스를 분할하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="e31f5-153">Learn about partitioning stateful services for maximum scale</span></span>](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
