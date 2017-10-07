---
title: "aaaCreate 개인 Docker 레지스트리-Azure 포털 | Microsoft Docs"
description: "만들기 및 관리 사설 Docker 컨테이너 레지스트리 Azure 포털 hello로 시작."
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
ms.openlocfilehash: 40f3ce44fea26e5fbeca865c9da6df55c2df9511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-portal"></a><span data-ttu-id="2973b-103">Hello Azure 포털을 사용 하 여 개인 Docker 컨테이너 등록 만들기</span><span class="sxs-lookup"><span data-stu-id="2973b-103">Create a private Docker container registry using hello Azure portal</span></span>
<span data-ttu-id="2973b-104">Azure 포털 toocreate 컨테이너 레지스트리 hello를 사용 하 하 고 해당 설정을 관리 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-104">Use hello Azure portal toocreate a container registry and manage its settings.</span></span> <span data-ttu-id="2973b-105">또한 생성 하 고 컨테이너 레지스트리에 hello를 사용 하 여 관리 수 [Azure CLI 2.0 명령은](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) 또는 프로그래밍 방식으로 컨테이너 레지스트리 hello [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="2973b-105">You can also create and manage container registries using hello [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>

<span data-ttu-id="2973b-106">배경 및 개념에 대 한 참조 [개요 hello](container-registry-intro.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-106">For background and concepts, see [hello overview](container-registry-intro.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="2973b-107">컨테이너 레지스트리 만들기</span><span class="sxs-lookup"><span data-stu-id="2973b-107">Create a container registry</span></span>
1. <span data-ttu-id="2973b-108">Hello에 [Azure 포털](https://portal.azure.com), 클릭 **+ 새로 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-108">In hello [Azure portal](https://portal.azure.com), click **+ New**.</span></span>
2. <span data-ttu-id="2973b-109">에 대 한 검색 hello 마켓플레이스 **Azure 컨테이너 레지스트리**합니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-109">Search hello marketplace for **Azure container registry**.</span></span>
3. <span data-ttu-id="2973b-110">게시자가 **Microsoft**인 **Azure 컨테이너 레지스트리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-110">Select **Azure Container Registry**, with publisher **Microsoft**.</span></span>
    <span data-ttu-id="2973b-111">![Azure Marketplace의 컨테이너 레지스트리 서비스](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span><span class="sxs-lookup"><span data-stu-id="2973b-111">![Container Registry service in Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span></span>
4. <span data-ttu-id="2973b-112">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-112">Click **Create**.</span></span> <span data-ttu-id="2973b-113">hello **Azure 컨테이너 레지스트리** 블레이드 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-113">hello **Azure Container Registry** blade appears.</span></span>

    ![컨테이너 레지스트리 설정](./media/container-registry-get-started-portal/container-registry-settings.png)
5. <span data-ttu-id="2973b-115">Hello에 **Azure 컨테이너 레지스트리** 블레이드에서 hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-115">In hello **Azure Container Registry** blade, enter hello following information.</span></span> <span data-ttu-id="2973b-116">완료하면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-116">Click **Create** when you are done.</span></span>

    <span data-ttu-id="2973b-117">a.</span><span class="sxs-lookup"><span data-stu-id="2973b-117">a.</span></span> <span data-ttu-id="2973b-118">**레지스트리 이름**: 특정 레지스트리에 대한 전역적으로 고유한 최상위 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-118">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="2973b-119">이 예제에서는 hello 레지스트리 이름이 *myRegistry01*, 되지만 대신 사용자 고유의의 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-119">In this example, hello registry name is *myRegistry01*, but substitute a unique name of your own.</span></span> <span data-ttu-id="2973b-120">hello 이름에는 문자와 숫자만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-120">hello name can contain only letters and numbers.</span></span>

    <span data-ttu-id="2973b-121">b.</span><span class="sxs-lookup"><span data-stu-id="2973b-121">b.</span></span> <span data-ttu-id="2973b-122">**리소스 그룹**: 기존 선택 [리소스 그룹](../azure-resource-manager/resource-group-overview.md#resource-groups) 또는 새 유형 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-122">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span>

    <span data-ttu-id="2973b-123">c.</span><span class="sxs-lookup"><span data-stu-id="2973b-123">c.</span></span> <span data-ttu-id="2973b-124">**위치**: 여기서 hello 서비스는 Azure 데이터 센터 위치를 선택 [사용 가능한](https://azure.microsoft.com/regions/services/)와 같은 **미국 중남부**합니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-124">**Location**: Select an Azure datacenter location where hello service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="2973b-125">d.</span><span class="sxs-lookup"><span data-stu-id="2973b-125">d.</span></span> <span data-ttu-id="2973b-126">**관리: 사용자**:는 관리자 사용자 tooaccess hello 레지스트리를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-126">**Admin user**: If you want, enable an admin user tooaccess hello registry.</span></span> <span data-ttu-id="2973b-127">Hello 레지스트리를 만든 후이 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-127">You can change this setting after creating hello registry.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="2973b-128">또한 tooproviding에 admin 사용자 계정을 통해 액세스할 컨테이너 레지스트리에 Azure Active Directory 서비스 사용자에 의해 지원 되는 인증을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-128">In addition tooproviding access through an admin user account, container registries support authentication backed by Azure Active Directory service principals.</span></span> <span data-ttu-id="2973b-129">자세한 내용 및 고려 사항은 [컨테이너 레지스트리로 인증](container-registry-authentication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2973b-129">For more information and considerations, see [Authenticate with a container registry](container-registry-authentication.md).</span></span>
      >

    <span data-ttu-id="2973b-130">e.</span><span class="sxs-lookup"><span data-stu-id="2973b-130">e.</span></span> <span data-ttu-id="2973b-131">**저장소 계정**: 기본 설정 toocreate hello를 사용 하 여 한 [저장소 계정](../storage/common/storage-introduction.md), hello에서 기존 저장소 계정을 선택 하거나 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-131">**Storage account**: Use hello default setting toocreate a [storage account](../storage/common/storage-introduction.md), or select an existing storage account in hello same location.</span></span> <span data-ttu-id="2973b-132">Premium Storage는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-132">Currently Premium Storage is not supported.</span></span>

## <a name="manage-registry-settings"></a><span data-ttu-id="2973b-133">레지스트리 설정 관리</span><span class="sxs-lookup"><span data-stu-id="2973b-133">Manage registry settings</span></span>
<span data-ttu-id="2973b-134">Hello 레지스트리를 만든 후 hello 레지스트리 설정의 찾을 hello부터 시작 하 여 **컨테이너 레지스트리에** 블레이드 hello 포털에서입니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-134">After creating hello registry, find hello registry settings by starting at hello **Container Registries** blade in hello portal.</span></span> <span data-ttu-id="2973b-135">예를 들어 hello 설정을 toolog tooyour 레지스트리에 할 수 있습니다 또는 tooenable 하거나 hello 관리: 사용자를 사용 하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-135">For example, you might need hello settings toolog in tooyour registry, or you might want tooenable or disable hello admin user.</span></span>

1. <span data-ttu-id="2973b-136">Hello에 **컨테이너 레지스트리에** 블레이드에서 레지스트리 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-136">On hello **Container Registries** blade, click hello name of your registry.</span></span>

    ![컨테이너 레지스트리 블레이드](./media/container-registry-get-started-portal/container-registry-blade.png)
2. <span data-ttu-id="2973b-138">toomanage 액세스 설정을 클릭 **선택 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-138">toomanage access settings, click **Access key**.</span></span>

    ![컨테이너 레지스트리 액세스](./media/container-registry-get-started-portal/container-registry-access.png)
3. <span data-ttu-id="2973b-140">다음 설정을 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="2973b-140">Note hello following settings:</span></span>

   * <span data-ttu-id="2973b-141">**로그인 서버** -toolog를 사용 하 여 toohello 레지스트리에 hello 정규화 된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-141">**Login server** - hello fully qualified name you use toolog in toohello registry.</span></span> <span data-ttu-id="2973b-142">이 예제에서는 `myregistry01.azurecr.io`입니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-142">In this example, it is `myregistry01.azurecr.io`.</span></span>
   * <span data-ttu-id="2973b-143">**관리: 사용자** -tooenable 설정/해제 하거나 hello 레지스트리 관리자 사용자 계정을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-143">**Admin user** - Toggle tooenable or disable hello registry's admin user account.</span></span>
   * <span data-ttu-id="2973b-144">**사용자 이름** 및 **암호** -(설정 된 경우) hello admin 사용자 계정의 자격 증명을 hello toohello 레지스트리에 toolog를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-144">**Username** and **Password** - hello credentials of hello admin user account (if enabled) you can use toolog in toohello registry.</span></span> <span data-ttu-id="2973b-145">필요에 따라 hello 암호를 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-145">You can optionally regenerate hello passwords.</span></span> <span data-ttu-id="2973b-146">다른 암호 hello를 다시 생성 하는 동안에 하나의 암호를 사용 하 여 연결 toohello 레지스트리 유지 관리할 수 있도록 두 개의 암호가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-146">Two passwords are created so that you can maintain connections toohello registry by using one password while you regenerate hello other password.</span></span> <span data-ttu-id="2973b-147">서비스 사용자와 tooauthenticate 대신 참조 [개인 Docker 컨테이너 레지스트리로 인증](container-registry-authentication.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2973b-147">tooauthenticate with a service principal instead, see [Authenticate with a private Docker container registry](container-registry-authentication.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2973b-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2973b-148">Next steps</span></span>
* [<span data-ttu-id="2973b-149">Hello Docker CLI를 사용 하 여 첫 번째 이미지 강제</span><span class="sxs-lookup"><span data-stu-id="2973b-149">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
