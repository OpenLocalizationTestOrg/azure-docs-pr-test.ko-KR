---
title: "개인 Docker 레지스트리 만들기 - Azure Portal | Microsoft Docs"
description: "Azure Portal을 사용하여 개인 Docker 컨테이너 레지스트리 만들기 및 관리 시작"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7fbbb56d775ee96c9a44363a4e41d4fc3c630582
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-private-docker-container-registry-using-the-azure-portal"></a><span data-ttu-id="69983-103">Azure Portal을 사용하여 개인 Docker 컨테이너 레지스트리 만들기</span><span class="sxs-lookup"><span data-stu-id="69983-103">Create a private Docker container registry using the Azure portal</span></span>
<span data-ttu-id="69983-104">Azure Portal을 사용하여 컨테이너 레지스트리를 만들고 설정을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="69983-104">Use the Azure portal to create a container registry and manage its settings.</span></span> <span data-ttu-id="69983-105">[Azure CLI 2.0 명령](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md)을 사용하거나 Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376)를 통해 프로그래밍 방식으로 컨테이너 레지스트리를 만들고 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69983-105">You can also create and manage container registries using the [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) or programmatically with the Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>

<span data-ttu-id="69983-106">배경 지식 및 개념은 [개요](container-registry-intro.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69983-106">For background and concepts, see [the overview](container-registry-intro.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="69983-107">컨테이너 레지스트리 만들기</span><span class="sxs-lookup"><span data-stu-id="69983-107">Create a container registry</span></span>
1. <span data-ttu-id="69983-108">[Azure Portal](https://portal.azure.com)에서 **+ 새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69983-108">In the [Azure portal](https://portal.azure.com), click **+ New**.</span></span>
2. <span data-ttu-id="69983-109">**Azure 컨테이너 레지스트리**에 대한 마켓플레이스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="69983-109">Search the marketplace for **Azure container registry**.</span></span>
3. <span data-ttu-id="69983-110">게시자가 **Microsoft**인 **Azure 컨테이너 레지스트리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="69983-110">Select **Azure Container Registry**, with publisher **Microsoft**.</span></span>
    <span data-ttu-id="69983-111">![Azure Marketplace의 컨테이너 레지스트리 서비스](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span><span class="sxs-lookup"><span data-stu-id="69983-111">![Container Registry service in Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span></span>
4. <span data-ttu-id="69983-112">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69983-112">Click **Create**.</span></span> <span data-ttu-id="69983-113">**Azure 컨테이너 레지스트리** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="69983-113">The **Azure Container Registry** blade appears.</span></span>

    ![컨테이너 레지스트리 설정](./media/container-registry-get-started-portal/container-registry-settings.png)
5. <span data-ttu-id="69983-115">**Azure 컨테이너 레지스트리** 블레이드에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="69983-115">In the **Azure Container Registry** blade, enter the following information.</span></span> <span data-ttu-id="69983-116">완료하면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69983-116">Click **Create** when you are done.</span></span>

    <span data-ttu-id="69983-117">a.</span><span class="sxs-lookup"><span data-stu-id="69983-117">a.</span></span> <span data-ttu-id="69983-118">**레지스트리 이름**: 특정 레지스트리에 대한 전역적으로 고유한 최상위 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="69983-118">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="69983-119">이 예제의 경우 레지스트리 이름이 *myRegistry01*이지만 자신만의 고유한 이름으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="69983-119">In this example, the registry name is *myRegistry01*, but substitute a unique name of your own.</span></span> <span data-ttu-id="69983-120">이름은 문자와 숫자만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69983-120">The name can contain only letters and numbers.</span></span>

    <span data-ttu-id="69983-121">b.</span><span class="sxs-lookup"><span data-stu-id="69983-121">b.</span></span> <span data-ttu-id="69983-122">**리소스 그룹**: 기존 [리소스 그룹](../azure-resource-manager/resource-group-overview.md#resource-groups)을 선택하거나 새 리소스 그룹의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="69983-122">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span>

    <span data-ttu-id="69983-123">c.</span><span class="sxs-lookup"><span data-stu-id="69983-123">c.</span></span> <span data-ttu-id="69983-124">**위치**: **미국 중남부**와 같이 서비스를 [사용할 수 있는](https://azure.microsoft.com/regions/services/) Azure 데이터 센터 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="69983-124">**Location**: Select an Azure datacenter location where the service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="69983-125">d.</span><span class="sxs-lookup"><span data-stu-id="69983-125">d.</span></span> <span data-ttu-id="69983-126">**관리 사용자**: 필요한 경우 관리 사용자가 레지스트리에 액세스할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="69983-126">**Admin user**: If you want, enable an admin user to access the registry.</span></span> <span data-ttu-id="69983-127">이 설정은 레지스트리를 만든 후에 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69983-127">You can change this setting after creating the registry.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="69983-128">관리 사용자 계정을 통해 액세스를 제공하는 것 외에, 컨테이너 레지스트리는 Azure Active Directory 서비스 주체에 의해 지원되는 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="69983-128">In addition to providing access through an admin user account, container registries support authentication backed by Azure Active Directory service principals.</span></span> <span data-ttu-id="69983-129">자세한 내용 및 고려 사항은 [컨테이너 레지스트리로 인증](container-registry-authentication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69983-129">For more information and considerations, see [Authenticate with a container registry](container-registry-authentication.md).</span></span>
      >

    <span data-ttu-id="69983-130">e.</span><span class="sxs-lookup"><span data-stu-id="69983-130">e.</span></span> <span data-ttu-id="69983-131">**저장소 계정**: 기본 설정을 사용하여 [저장소 계정](../storage/common/storage-introduction.md)을 만들거나 동일한 위치에서 기존 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="69983-131">**Storage account**: Use the default setting to create a [storage account](../storage/common/storage-introduction.md), or select an existing storage account in the same location.</span></span> <span data-ttu-id="69983-132">Premium Storage는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69983-132">Currently Premium Storage is not supported.</span></span>

## <a name="manage-registry-settings"></a><span data-ttu-id="69983-133">레지스트리 설정 관리</span><span class="sxs-lookup"><span data-stu-id="69983-133">Manage registry settings</span></span>
<span data-ttu-id="69983-134">레지스트리를 만든 후 포털의 **Container Registry** 블레이드를 시작하여 레지스트리 설정을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="69983-134">After creating the registry, find the registry settings by starting at the **Container Registries** blade in the portal.</span></span> <span data-ttu-id="69983-135">예를 들어 레지스트리에 로그인하기 위해 설정이 필요하거나 관리 사용자를 사용하거나 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69983-135">For example, you might need the settings to log in to your registry, or you might want to enable or disable the admin user.</span></span>

1. <span data-ttu-id="69983-136">**Container Registry** 블레이드에서 레지스트리의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69983-136">On the **Container Registries** blade, click the name of your registry.</span></span>

    ![컨테이너 레지스트리 블레이드](./media/container-registry-get-started-portal/container-registry-blade.png)
2. <span data-ttu-id="69983-138">액세스 설정을 관리하려면 **액세스 키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69983-138">To manage access settings, click **Access key**.</span></span>

    ![컨테이너 레지스트리 액세스](./media/container-registry-get-started-portal/container-registry-access.png)
3. <span data-ttu-id="69983-140">다음 설정에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="69983-140">Note the following settings:</span></span>

   * <span data-ttu-id="69983-141">**로그인 서버** - 레지스트리에 로그인하기 위해 사용하는 정규화된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="69983-141">**Login server** - The fully qualified name you use to log in to the registry.</span></span> <span data-ttu-id="69983-142">이 예제에서는 `myregistry01.azurecr.io`입니다.</span><span class="sxs-lookup"><span data-stu-id="69983-142">In this example, it is `myregistry01.azurecr.io`.</span></span>
   * <span data-ttu-id="69983-143">**관리 사용자** - 레지스트리의 관리 사용자 계정을 사용하거나 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="69983-143">**Admin user** - Toggle to enable or disable the registry's admin user account.</span></span>
   * <span data-ttu-id="69983-144">**사용자 이름** 및 **암호** - 레지스트리에 로그인하는 데 사용할 수 있는 관리 사용자(사용하는 경우)의 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="69983-144">**Username** and **Password** - The credentials of the admin user account (if enabled) you can use to log in to the registry.</span></span> <span data-ttu-id="69983-145">암호는 선택적으로 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69983-145">You can optionally regenerate the passwords.</span></span> <span data-ttu-id="69983-146">다른 암호를 다시 생성하는 동안에 하나의 암호를 사용하여 레지스트리에 대한 연결을 유지할 수 있도록 두 개의 암호가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="69983-146">Two passwords are created so that you can maintain connections to the registry by using one password while you regenerate the other password.</span></span> <span data-ttu-id="69983-147">대신 서비스 주체로 인증하려면 [개인 Docker 컨테이너 레지스트리로 인증](container-registry-authentication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69983-147">To authenticate with a service principal instead, see [Authenticate with a private Docker container registry](container-registry-authentication.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="69983-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="69983-148">Next steps</span></span>
* [<span data-ttu-id="69983-149">Docker CLI를 사용하여 첫 번째 이미지 푸시</span><span class="sxs-lookup"><span data-stu-id="69983-149">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
