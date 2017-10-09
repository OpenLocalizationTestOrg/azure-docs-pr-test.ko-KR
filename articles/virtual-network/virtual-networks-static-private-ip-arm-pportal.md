---
title: "Vm-Azure 포털에 대 한 aaaConfigure 개인 IP 주소 | Microsoft Docs"
description: "Tooconfigure 개인 IP 주소를 사용 하 여 가상 컴퓨터에 대 한 Azure 포털을 hello 하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 11245645-357d-4358-9a14-dd78e367b494
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 474161303cdf8cb98e16ffd7cef6b74debdbc49a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-portal"></a><span data-ttu-id="5516b-103">Hello Azure 포털을 사용 하 여 가상 컴퓨터에 대 한 개인 IP 주소를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-103">Configure private IP addresses for a virtual machine using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5516b-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="5516b-104">Azure portal</span></span>](virtual-networks-static-private-ip-arm-pportal.md)
> * [<span data-ttu-id="5516b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5516b-105">PowerShell</span></span>](virtual-networks-static-private-ip-arm-ps.md)
> * [<span data-ttu-id="5516b-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5516b-106">Azure CLI</span></span>](virtual-networks-static-private-ip-arm-cli.md)
> * [<span data-ttu-id="5516b-107">Azure Portal(클래식)</span><span class="sxs-lookup"><span data-stu-id="5516b-107">Azure portal (Classic)</span></span>](virtual-networks-static-private-ip-classic-pportal.md)
> * [<span data-ttu-id="5516b-108">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="5516b-108">PowerShell (Classic)</span></span>](virtual-networks-static-private-ip-classic-ps.md)
> * [<span data-ttu-id="5516b-109">Azure CLI(클래식)</span><span class="sxs-lookup"><span data-stu-id="5516b-109">Azure CLI (Classic)</span></span>](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="5516b-110">이 문서에서는 hello 리소스 관리자 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-110">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="5516b-111">수도 있습니다 [hello 클래식 배포 모델에 개인 고정 IP 주소 관리](virtual-networks-static-private-ip-classic-pportal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-111">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="5516b-112">다음 hello 샘플 단계를 이미 만든 단순한 환경을 기대 합니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-112">hello sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="5516b-113">이 문서에 표시 된 대로 toorun hello 단계를 원하는 경우 먼저 hello 테스트 환경을 구축에 설명 된 [vnet을 만든](virtual-networks-create-vnet-arm-pportal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-113">If you want toorun hello steps as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-pportal.md).</span></span>

## <a name="how-toocreate-a-vm-for-testing-static-private-ip-addresses"></a><span data-ttu-id="5516b-114">개인 고정 IP를 테스트 하기 위한 VM toocreate 해결 하는 방법을</span><span class="sxs-lookup"><span data-stu-id="5516b-114">How toocreate a VM for testing static private IP addresses</span></span>
<span data-ttu-id="5516b-115">Hello Azure 포털을 사용 하 여 hello hello 리소스 관리자 배포 모드에서 vm을 만드는 동안 정적 개인 IP 주소를 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-115">You cannot set a static private IP address during hello creation of a VM in hello Resource Manager deployment mode by using hello Azure portal.</span></span> <span data-ttu-id="5516b-116">다음 설정의 개인 IP toobe을 정적, VM hello를 먼저 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-116">You must create hello VM first, tehn set its private IP toobe static.</span></span>

<span data-ttu-id="5516b-117">toocreate 라는 VM *DNS01* hello에 *프런트 엔드* 라는 VNet의 서브넷 *TestVNet*, 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-117">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet*, follow hello steps below.</span></span>

1. <span data-ttu-id="5516b-118">브라우저에서 toohttp://portal.azure.com를 탐색 하 고, 필요한 경우 Azure 계정을 사용해 합니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-118">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="5516b-119">클릭 **새로** > **계산** > **Windows Server 2012 R2 Datacenter**, 해당 hello 확인 **배포모델선택** 목록 표시 이미 **리소스 관리자**, 클릭 하 고 **만들기**그림과 같이 hello 아래, 합니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-119">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that hello **Select a deployment model** list already shows **Resource Manager**, and then click **Create**, as seen in hello figure below.</span></span>
   
    ![Azure 포털에서 VM 만들기](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. <span data-ttu-id="5516b-121">Hello에 **기본 사항** 블레이드를 생성 하는 hello VM toobe의 hello 이름을 입력 (*DNS01* 시나리오에서), 로컬 관리자 계정 및 암호를 아래 hello 그림 에서처럼 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-121">In hello **Basics** blade, enter hello name of hello VM toobe created (*DNS01* in our scenario), hello local administrator account, and password, as seen in hello figure below.</span></span>
   
    ![기본 사항 블레이드](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. <span data-ttu-id="5516b-123">Hello 있는지 확인 **위치** 선택한 *중앙 미국*, 클릭 **기존 선택** 아래 **리소스 그룹**, 클릭**리소스 그룹** 클릭 한 다음 다시 *TestRG*, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-123">Make sure hello **Location** selected is *Central US*, then click **Select existing** under **Resource group**, then click **Resource group** again, then click *TestRG*, and then click **OK**.</span></span>
   
    ![기본 사항 블레이드](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. <span data-ttu-id="5516b-125">Hello에 **크기 선택** 블레이드를 **표준 A1**, 클릭 하 고 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-125">In hello **Choose a size** blade, select **A1 Standard**, and then click **Select**.</span></span>
   
    ![크기 선택 블레이드](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. <span data-ttu-id="5516b-127">에 **설정** 블레이드에서 확인 되었는지 hello 다음 속성이 설정 된 아래의 hello 값으로 설정 되 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-127">In teh **Settings** blade, make sure hello following properties are set are set with hello values below, and then click **OK**.</span></span>
   
    <span data-ttu-id="5516b-128">-**저장소 계정**: *vnetstorage*</span><span class="sxs-lookup"><span data-stu-id="5516b-128">-**Storage account**: *vnetstorage*</span></span>
   
   * <span data-ttu-id="5516b-129">**네트워크**: *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="5516b-129">**Network**: *TestVNet*</span></span>
   * <span data-ttu-id="5516b-130">**서브넷**: *FrontEnd*</span><span class="sxs-lookup"><span data-stu-id="5516b-130">**Subnet**: *FrontEnd*</span></span>
     
     ![크기 선택 블레이드](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. <span data-ttu-id="5516b-132">Hello에 **요약** 블레이드에서 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-132">In hello **Summary** blade, click **OK**.</span></span> <span data-ttu-id="5516b-133">공지 hello 타일 아래에 대시보드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-133">Notice hello tile below displayed in your dashboard.</span></span>
   
    ![Azure 포털에서 VM 만들기](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="5516b-135">어떻게 tooretrieve 정적 개인 IP 주소는 VM에 대 한 정보</span><span class="sxs-lookup"><span data-stu-id="5516b-135">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="5516b-136">tooview hello 정적 개인 IP 주소 정보 hello에 대 한 위의 hello 단계를 사용 하 여 만든 VM 아래 hello 단계를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-136">tooview hello static private IP address information for hello VM created with hello steps above, execute hello steps below.</span></span>

1. <span data-ttu-id="5516b-137">Hello Azure Azure 포털에서 클릭 **모두 찾아보기** > **가상 컴퓨터** > **DNS01** > **모든 설정** > **네트워크 인터페이스** 나열 된 hello 유일한 네트워크 인터페이스에서 다음을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-137">From hello Azure Azure portal, click **BROWSE ALL** > **Virtual machines** > **DNS01** > **All settings** > **Network interfaces** and then click on hello only network interface listed.</span></span>
   
    ![VM 타일 배포](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. <span data-ttu-id="5516b-139">Hello에 **네트워크 인터페이스** 블레이드에서 클릭 **모든 설정을** > **IP 주소** 및 통지 hello **할당** 및 **IP 주소** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-139">In hello **Network interface** blade, click **All settings** > **IP addresses** and notice hello **Assignment** and **IP address** values.</span></span>
   
    ![VM 타일 배포](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="5516b-141">정적 개인 IP tooadd tooan 기존 VM을 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5516b-141">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="5516b-142">아래의 hello 단계를 수행 하는 tooadd는 정적 개인 IP 주소 toohello 위의 hello 단계를 사용 하 여 만든 VM:</span><span class="sxs-lookup"><span data-stu-id="5516b-142">tooadd a static private IP address toohello VM created using hello steps above, follow hello steps below:</span></span>

1. <span data-ttu-id="5516b-143">Hello에서 **IP 주소** 위에 표시 된 블레이드 클릭 **정적** 아래 **할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-143">From hello **IP addresses** blade shown above, click **Static** under **Assignment**.</span></span>
2. <span data-ttu-id="5516b-144">**IP 주소**에 *192.168.1.101*을 입력하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-144">Type *192.168.1.101* for **IP address**, and then click **Save**.</span></span>
   
    ![Azure 포털에서 VM 만들기](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> <span data-ttu-id="5516b-146">클릭 한 후 if **저장** hello 할당 너무 설정 않음을 알게**동적**, 입력 한 hello IP 주소를 이미 사용 중임을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-146">If after clicking **Save** you notice that hello assignment is still set too**Dynamic**, it means that hello IP address you typed is already in use.</span></span> <span data-ttu-id="5516b-147">다른 IP 주소로 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="5516b-147">Try a different IP address.</span></span>
> 
> 

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="5516b-148">어떻게 tooremove 정적 개인 IP는 VM에서을 해결합니다</span><span class="sxs-lookup"><span data-stu-id="5516b-148">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="5516b-149">tooremove hello 정적 개인 IP 주소, 위에서 만든 VM hello에서 단계 다음에 나오는 hello를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-149">tooremove hello static private IP address from hello VM created above, complete hello following step:</span></span>

<span data-ttu-id="5516b-150">Hello에서 **IP 주소** 위에 표시 된 블레이드 클릭 **동적** 아래 **할당**, 클릭 하 고 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-150">From hello **IP addresses** blade shown above, click **Dynamic** under **Assignment**, and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5516b-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5516b-151">Next steps</span></span>
* <span data-ttu-id="5516b-152">[예약된 공용 IP](virtual-networks-reserved-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="5516b-153">[ILPIP(인스턴스 수준 공용 IP)](virtual-networks-instance-level-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="5516b-154">Hello 참조 [예약 된 IP REST Api](https://msdn.microsoft.com/library/azure/dn722420.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="5516b-154">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

