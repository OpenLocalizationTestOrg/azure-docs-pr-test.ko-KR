---
title: "hello Azure 포털을 사용 하 여 aaaManage Nsg | Microsoft Docs"
description: "자세한 내용은 방법 toomanage hello Azure 포털을 사용 하 여 Nsg를 기존 합니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: ad9a4060bd81bae4597ad5a4f59622e10cd214cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-nsgs-using-hello-portal"></a><span data-ttu-id="6496d-103">Hello 포털을 사용 하 여 Nsg를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-103">Manage NSGs using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6496d-104">포털</span><span class="sxs-lookup"><span data-stu-id="6496d-104">Portal</span></span>](virtual-network-manage-nsg-arm-portal.md)
> * [<span data-ttu-id="6496d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6496d-105">PowerShell</span></span>](virtual-network-manage-nsg-arm-ps.md)
> * [<span data-ttu-id="6496d-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6496d-106">Azure CLI</span></span>](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="6496d-107">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6496d-108">이 문서에서는 Microsoft hello 클래식 배포 모델 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-108">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="6496d-109">정보 검색</span><span class="sxs-lookup"><span data-stu-id="6496d-109">Retrieve Information</span></span>
<span data-ttu-id="6496d-110">기존 NSG를 보고 기존 NSG에 대한 규칙을 검색하며 NSG가 연결된 리소스에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-110">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="6496d-111">기존 NSG 보기</span><span class="sxs-lookup"><span data-stu-id="6496d-111">View existing NSGs</span></span>

<span data-ttu-id="6496d-112">tooview 모든 단계를 수행 하는 전체 hello 구독에서 Nsg를 기존:</span><span class="sxs-lookup"><span data-stu-id="6496d-112">tooview all existing NSGs in a subscription, complete hello following steps:</span></span>

1. <span data-ttu-id="6496d-113">브라우저에서 toohttp://portal.azure.com를 탐색 하 고, 필요한 경우 Azure 계정을 사용해 합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-113">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>

2. <span data-ttu-id="6496d-114">**찾아보기 >** > **네트워크 보안 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-114">Click **Browse >** > **Network security groups**.</span></span>

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. <span data-ttu-id="6496d-116">Hello Nsg의 hello 목록을 확인 **네트워크 보안 그룹** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-116">Check hello list of NSGs in hello **Network security groups** blade.</span></span>

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a><span data-ttu-id="6496d-118">리소스 그룹에서 NSG 보기</span><span class="sxs-lookup"><span data-stu-id="6496d-118">View NSGs in a resource group</span></span>

<span data-ttu-id="6496d-119">Nsg의 hello tooview hello 목록 **RG NSG** 리소스 그룹, 단계를 수행 하는 전체 hello:</span><span class="sxs-lookup"><span data-stu-id="6496d-119">tooview hello list of NSGs in hello **RG-NSG** resource group, complete hello following steps:</span></span>

1. <span data-ttu-id="6496d-120">**리소스 그룹 >** > **RG-NSG** > **...**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-120">Click **Resource groups >** > **RG-NSG** > **...**.</span></span>

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. <span data-ttu-id="6496d-122">리소스의 hello 목록에서 항목을 찾을 hello NSG 아이콘 표시 hello에 나와 있는 것 처럼 **리소스** 블레이드 아래 합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-122">In hello list of resources, look for items displaying hello NSG icon, as shown in hello **Resources** blade below.</span></span>

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="6496d-124">NSG에 대한 모든 규칙 나열</span><span class="sxs-lookup"><span data-stu-id="6496d-124">List all rules for an NSG</span></span>

<span data-ttu-id="6496d-125">명명 된 NSG의 tooview hello 규칙 **NSG 프런트 엔드**완료, 다음 단계 hello:</span><span class="sxs-lookup"><span data-stu-id="6496d-125">tooview hello rules of an NSG named **NSG-FrontEnd**, complete hello following steps:</span></span>

1. <span data-ttu-id="6496d-126">Hello에서 **네트워크 보안 그룹** 블레이드에서 또는 hello **리소스** 위에 표시 된 블레이드 클릭 **NSG 프런트 엔드**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-126">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="6496d-127">Hello에 **설정** 탭을 클릭 **인바운드 보안 규칙**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-127">In hello **Settings** tab, click **Inbound security rules**.</span></span>

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. <span data-ttu-id="6496d-129">hello **인바운드 보안 규칙** 블레이드는 아래와 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-129">hello **Inbound security rules** blade is displayed as shown below.</span></span>

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. <span data-ttu-id="6496d-131">Hello에 **설정** 탭을 클릭 **아웃 바운드 보안 규칙** toosee hello 아웃 바운드 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-131">In hello **Settings** tab, click **Outbound security rules** toosee hello outbound rules.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6496d-132">tooview 기본 규칙을 클릭 하 여 hello **규칙 기본** hello hello 규칙을 표시 하는 hello 블레이드 맨 위에 있는 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-132">tooview default rules, click hello **Default rules** icon at hello top of hello blade that displays hello rules.</span></span>
    >

### <a name="view-nsgs-associations"></a><span data-ttu-id="6496d-133">NSG 연결 보기</span><span class="sxs-lookup"><span data-stu-id="6496d-133">View NSGs associations</span></span>

<span data-ttu-id="6496d-134">tooview 어떤 리소스 hello **NSG 프런트 엔드** NSG는 다음 단계와 연결 하 고 완전 hello:</span><span class="sxs-lookup"><span data-stu-id="6496d-134">tooview what resources hello **NSG-FrontEnd** NSG is associate with, complete hello following steps:</span></span>

1. <span data-ttu-id="6496d-135">Hello에서 **네트워크 보안 그룹** 블레이드에서 또는 hello **리소스** 위에 표시 된 블레이드 클릭 **NSG 프런트 엔드**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-135">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="6496d-136">Hello에 **설정** 탭을 클릭 **서브넷** 어떤 서브넷은 tooview toohello NSG를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-136">In hello **Settings** tab, click **Subnets** tooview what subnets are associated toohello NSG.</span></span>

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. <span data-ttu-id="6496d-138">Hello에 **설정** 탭을 클릭 **네트워크 인터페이스** tooview Nic 이란 관련 toohello NSG 합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-138">In hello **Settings** tab, click **Network interfaces** tooview what NICs are associated toohello NSG.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="6496d-139">규칙 관리</span><span class="sxs-lookup"><span data-stu-id="6496d-139">Manage rules</span></span>
<span data-ttu-id="6496d-140">기존 NSG 규칙 tooan 추가, 기존 규칙을 편집 하 고 규칙을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-140">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="6496d-141">규칙 추가</span><span class="sxs-lookup"><span data-stu-id="6496d-141">Add a rule</span></span>
<span data-ttu-id="6496d-142">허용 하는 규칙 tooadd **인바운드** 트래픽 tooport **443** 모든 컴퓨터 toohello에서 **NSG 프런트 엔드** NSG, 단계를 수행 하는 전체 hello:</span><span class="sxs-lookup"><span data-stu-id="6496d-142">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, complete hello following steps:</span></span>

1. <span data-ttu-id="6496d-143">Hello에서 **네트워크 보안 그룹** 블레이드에서 또는 hello **리소스** 위에 표시 된 블레이드 클릭 **NSG 프런트 엔드**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-143">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="6496d-144">Hello에 **설정** 탭을 클릭 **인바운드 보안 규칙**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-144">In hello **Settings** tab, click **Inbound security rules**.</span></span>
3. <span data-ttu-id="6496d-145">Hello에 **인바운드 보안 규칙** 블레이드에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-145">In hello **Inbound security rules** blade, click **Add**.</span></span> <span data-ttu-id="6496d-146">그런 다음, hello **인바운드 보안 규칙 추가** 블레이드에서 아래와 같이 hello 값을 작성 한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-146">Then, in hello **Add inbound security rule** blade, fill hello values as shown below, and then click **OK**.</span></span>

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    <span data-ttu-id="6496d-148">몇 초 후 hello hello에서 새 규칙을 확인 **인바운드 보안 규칙** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-148">After a few seconds, notice hello new rule in hello **Inbound security rules** blade.</span></span>

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a><span data-ttu-id="6496d-150">규칙 변경</span><span class="sxs-lookup"><span data-stu-id="6496d-150">Change a rule</span></span>
<span data-ttu-id="6496d-151">tooallow 위에서 만든 toochange hello 규칙 hello에서 트래픽 인바운드 **인터넷** 단계를 수행 하는 유일한, 전체 hello:</span><span class="sxs-lookup"><span data-stu-id="6496d-151">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, complete hello following steps:</span></span>

1. <span data-ttu-id="6496d-152">Hello에서 **네트워크 보안 그룹** 블레이드에서 또는 hello **리소스** 위에 표시 된 블레이드 클릭 **NSG 프런트 엔드**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-152">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="6496d-153">Hello에 **설정** 탭에서 위에서 만든 hello 규칙을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-153">In hello **Settings** tab, click hello rule created above.</span></span>
3. <span data-ttu-id="6496d-154">Hello에 **허용 https** 블레이드, 변경 hello **소스** 아래와 같이 속성을 클릭 한 다음 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-154">In hello **allow-https** blade, change hello **Source** property as shown below, and then click **Save**.</span></span>

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a><span data-ttu-id="6496d-156">규칙 삭제</span><span class="sxs-lookup"><span data-stu-id="6496d-156">Delete a rule</span></span>

<span data-ttu-id="6496d-157">toodelete hello 규칙 위에서 만든, 전체 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-157">toodelete hello rule created above, complete hello following steps:</span></span>

1. <span data-ttu-id="6496d-158">Hello에서 **네트워크 보안 그룹** 블레이드에서 또는 hello **리소스** 위에 표시 된 블레이드 클릭 **NSG 프런트 엔드**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-158">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="6496d-159">Hello에 **설정** 탭에서 위에서 만든 hello 규칙을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-159">In hello **Settings** tab, click hello rule created above.</span></span>
3. <span data-ttu-id="6496d-160">Hello에 **허용 https** 블레이드에서 클릭 **삭제**, 클릭 하 고 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-160">In hello **allow-https** blade, click **Delete**, and then click **Yes**.</span></span>

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a><span data-ttu-id="6496d-162">연결 관리</span><span class="sxs-lookup"><span data-stu-id="6496d-162">Manage associations</span></span>
<span data-ttu-id="6496d-163">NSG toosubnets 및 Nic를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-163">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="6496d-164">또한 연결된 모든 리소스에서 NSG를 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-164">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="6496d-165">NSG tooa NIC에 연결</span><span class="sxs-lookup"><span data-stu-id="6496d-165">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="6496d-166">tooassociate hello **NSG 프런트 엔드** NSG toohello **TestNICWeb1** NIC를 다음 단계 완료 hello:</span><span class="sxs-lookup"><span data-stu-id="6496d-166">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="6496d-167">Hello에서 **네트워크 보안 그룹** 블레이드에서 또는 hello **리소스** 위에 표시 된 블레이드 클릭 **NSG 프런트 엔드**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-167">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="6496d-168">Hello에 **설정** 탭을 클릭 **네트워크 인터페이스** > **연결** > **TestNICWeb1**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-168">In hello **Settings** tab, click **Network interfaces** > **Associate** > **TestNICWeb1**.</span></span>

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="6496d-170">NIC에서 NSG 분리</span><span class="sxs-lookup"><span data-stu-id="6496d-170">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="6496d-171">toodissociate hello **NSG 프런트 엔드** hello에서 NSG **TestNICWeb1** NIC를 다음 단계 완료 hello:</span><span class="sxs-lookup"><span data-stu-id="6496d-171">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="6496d-172">Hello Azure 포털에서에서 클릭 **리소스 그룹 >** > **RG NSG** > **...**   >  **TestNICWeb1**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-172">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestNICWeb1**.</span></span>

2. <span data-ttu-id="6496d-173">Hello에 **TestNICWeb1** 블레이드에서 클릭 **의 보안 변경 중...**   >  **None**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-173">In hello **TestNICWeb1** blade, click **Change security...** > **None**.</span></span>

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> <span data-ttu-id="6496d-175">기존 NSG이 블레이드 tooassociate hello NIC tooany를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-175">You can also use this blade tooassociate hello NIC tooany existing NSG.</span></span>
>

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="6496d-176">서브넷에서 NSG 분리</span><span class="sxs-lookup"><span data-stu-id="6496d-176">Dissociate an NSG from a subnet</span></span>

<span data-ttu-id="6496d-177">toodissociate hello **NSG 프런트 엔드** hello에서 NSG **프런트 엔드** 서브넷, 단계를 수행 하는 전체 hello:</span><span class="sxs-lookup"><span data-stu-id="6496d-177">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, complete hello following steps:</span></span>

1. <span data-ttu-id="6496d-178">Hello Azure 포털에서에서 클릭 **리소스 그룹 >** > **RG NSG** > **...**   >  **TestVNet**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-178">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>

2. <span data-ttu-id="6496d-179">Hello에 **설정** 블레이드에서 클릭 **서브넷** > **프런트 엔드** > **네트워크 보안 그룹**  >  **None**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-179">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **None**.</span></span>

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. <span data-ttu-id="6496d-181">Hello에 **프런트 엔드** 블레이드에서 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-181">In hello **FrontEnd** blade, click **Save**.</span></span>

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="6496d-183">NSG tooa 서브넷 연결</span><span class="sxs-lookup"><span data-stu-id="6496d-183">Associate an NSG tooa subnet</span></span>

<span data-ttu-id="6496d-184">tooassociate hello **NSG 프런트 엔드** NSG toohello **FronEnd** 다시 서브넷, 단계를 수행 하는 전체 hello:</span><span class="sxs-lookup"><span data-stu-id="6496d-184">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, complete hello following steps:</span></span>

1. <span data-ttu-id="6496d-185">Hello Azure 포털에서에서 클릭 **리소스 그룹 >** > **RG NSG** > **...**   >  **TestVNet**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-185">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>
2. <span data-ttu-id="6496d-186">Hello에 **설정** 블레이드에서 클릭 **서브넷** > **프런트 엔드** > **네트워크 보안 그룹**  >  **NSG 프런트 엔드**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-186">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
3. <span data-ttu-id="6496d-187">Hello에 **프런트 엔드** 블레이드에서 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-187">In hello **FrontEnd** blade, click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="6496d-188">Thh NSG의에서 한 NSG tooa 서브넷에 연결할 수도 있습니다 **설정을** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-188">You can also associate an NSG tooa subnet from thh NSG's **Settings** blade.</span></span>
>

## <a name="delete-an-nsg"></a><span data-ttu-id="6496d-189">NSG 삭제</span><span class="sxs-lookup"><span data-stu-id="6496d-189">Delete an NSG</span></span>
<span data-ttu-id="6496d-190">NSG tooany 리소스를 연결 되지 않은 경우에 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-190">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="6496d-191">다음 단계 완료 hello NSG toodelete: 합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-191">toodelete an NSG, complete hello following steps:.</span></span>

1. <span data-ttu-id="6496d-192">Hello Azure 포털에서에서 클릭 **리소스 그룹 >** > **RG NSG** > **...**   >  **NSG 프런트 엔드**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-192">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="6496d-193">Hello에 **설정** 블레이드에서 클릭 **네트워크 인터페이스**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-193">In hello **Settings** blade, click **Network interfaces**.</span></span>
3. <span data-ttu-id="6496d-194">나열 된 모든 Nic가 없을 경우 hello NIC를 클릭 하 고에 2 단계에 따라 [NIC에서 NSG를 분리](#Dissociate-an-NSG-from-a-NIC)합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-194">If there are any NICs listed, click hello NIC, and follow step 2 in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC).</span></span>
4. <span data-ttu-id="6496d-195">각 NIC에 3단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-195">Repeat step 3 for each NIC.</span></span>
5. <span data-ttu-id="6496d-196">Hello에 **설정** 블레이드에서 클릭 **서브넷**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-196">In hello **Settings** blade, click **Subnets**.</span></span>
6. <span data-ttu-id="6496d-197">나열 된 모든 서브넷에 있는 경우 hello 서브넷을 클릭 하 고 2와 3 단계에 따라 [서브넷에서 NSG를 분리](#Dissociate-an-NSG-from-a-subnet)합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-197">If there are any subnets listed, click hello subnet and follow steps 2 and 3 in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet).</span></span>
7. <span data-ttu-id="6496d-198">왼쪽된 toohello 스크롤합니다 **NSG 프런트 엔드** 블레이드에서 클릭 **삭제** > **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="6496d-198">Scrolls left toohello **NSG-FrontEnd** blade, then click **Delete** > **Yes**.</span></span>

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a><span data-ttu-id="6496d-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6496d-200">Next steps</span></span>
* <span data-ttu-id="6496d-201">[로깅을 사용합니다](virtual-network-nsg-manage-log.md) .</span><span class="sxs-lookup"><span data-stu-id="6496d-201">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>
