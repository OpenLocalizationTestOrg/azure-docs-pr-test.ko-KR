---
title: "가상 컴퓨터 크기 집합 using aaaCreate hello Azure 포털 | Microsoft Docs"
description: "Azure Portal을 사용하여 확장 집합을 배포합니다."
keywords: "가상 컴퓨터 확장 집합"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9c1583f0-bcc7-4b51-9d64-84da76de1fda
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: negat
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23c88f4b1ba99994a38f8886f60735da74e5c17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-hello-azure-portal"></a><span data-ttu-id="f24c9-104">방법으로 가상 컴퓨터 크기 집합 a toocreate hello Azure 포털</span><span class="sxs-lookup"><span data-stu-id="f24c9-104">How toocreate a Virtual Machine Scale Set with hello Azure portal</span></span>
<span data-ttu-id="f24c9-105">이 자습서에서는 얼마나 쉬운지 가상 컴퓨터 크기 집합 toocreate 단 몇 분 후에 hello Azure 포털을 사용 하 여 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-105">This tutorial shows you how easy it is toocreate a Virtual Machine Scale Set in just a few minutes, by using hello Azure portal.</span></span> <span data-ttu-id="f24c9-106">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="choose-hello-vm-image-from-hello-marketplace"></a><span data-ttu-id="f24c9-107">Hello 마켓플레이스에서 hello VM 이미지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-107">Choose hello VM image from hello marketplace</span></span>
<span data-ttu-id="f24c9-108">Hello 포털에서 CentOS, CoreOS, Debian, 열기 Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, Ubuntu Server 또는 Windows Server 이미지를 사용 하 여 설정 하는 눈금을 쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-108">From hello portal, you can easily deploy a scale set with CentOS, CoreOS, Debian, Open Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, Ubuntu Server, or Windows Server images.</span></span>

<span data-ttu-id="f24c9-109">첫째, toohello 이동 [Azure 포털](https://portal.azure.com) 웹 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-109">First, navigate toohello [Azure portal](https://portal.azure.com) in a web browser.</span></span> <span data-ttu-id="f24c9-110">클릭 `New`, 검색할 `scale set`를 선택한 후 hello `Virtual machine scale set` 항목:</span><span class="sxs-lookup"><span data-stu-id="f24c9-110">Click `New`, search for `scale set`, and then select hello `Virtual machine scale set` entry:</span></span>

![ScaleSetPortalOverview](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalOverview.PNG)

## <a name="create-hello-scale-set"></a><span data-ttu-id="f24c9-112">Hello 크기 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="f24c9-112">Create hello scale set</span></span>
<span data-ttu-id="f24c9-113">이제 hello 기본 설정을 사용 하 고 신속 하 게 hello 크기 집합을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-113">Now you can use hello default settings and quickly create hello scale set.</span></span>

* <span data-ttu-id="f24c9-114">Hello에 `Basics` 블레이드에서 hello 크기 집합의 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-114">On hello `Basics` blade, enter a name for hello scale set.</span></span> <span data-ttu-id="f24c9-115">이 이름은 기본 hello 됩니다의 hello hello 크기 집합 앞에 hello 부하 분산 장치의 FQDN, 해야 hello 이름을 모든 Azure에서 고유 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-115">This name becomes hello base of hello FQDN of hello load balancer in front of hello scale set, so make sure hello name is unique across all Azure.</span></span>
* <span data-ttu-id="f24c9-116">원하는 OS 유형을 선택하고, 원하는 사용자 이름을 입력한 후 원하는 인증 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-116">Select your desired OS type, enter your desired username, and select which authentication type you prefer.</span></span> <span data-ttu-id="f24c9-117">암호를 선택 하면 긴 하 고는 세 가지 hello 4 개의 다음 복잡성 요구 사항을 충족 하는 12 자 이상 이어야 합니다: 하나의 \t-소문자, 대문자 한 문자, 숫자, 및 특수 문자를 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-117">If you choose a password, it must be at least 12 characters long and meet three out of hello four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="f24c9-118">자세한 내용은 [사용자 이름 및 암호 요구 사항](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f24c9-118">See more about [username and password requirements](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span> <span data-ttu-id="f24c9-119">선택 하면 `SSH public key`에서 공개 키, 개인 키로 되지 있는지 tooonly 붙여넣기 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-119">If you choose `SSH public key`, be sure tooonly paste in your public key, NOT your private key:</span></span>

![ScaleSetPortalBasics](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalBasics.PNG)

* <span data-ttu-id="f24c9-121">여부나를 배치 그룹이 여러 개를 넘으면 toolimit hello 배율 설정 tooa 단일 배치 그룹은 여부를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-121">Choose whether you would like toolimit hello scale set tooa single placement group or whether it should span multiple placement groups.</span></span> <span data-ttu-id="f24c9-122">크기 조정 설정 하는 100 개 이상의 Vm 용량 too1 000) (위쪽에 특정 제한 사항과 함께 수 hello 크기 집합 toospan 배치 그룹을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-122">Allowing hello scale set toospan placement groups allows for scale sets over 100 VMs in capacity (up too1,000) with certain limitations.</span></span> <span data-ttu-id="f24c9-123">자세한 내용은 [SDK 설명서](./virtual-machine-scale-sets-placement-groups.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f24c9-123">For more information, see [this documentation](./virtual-machine-scale-sets-placement-groups.md).</span></span>
* <span data-ttu-id="f24c9-124">원하는 리소스 그룹 이름 및 위치를 입력한 다음 `OK`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-124">Enter your desired resource group name and location, and then click `OK`.</span></span>
* <span data-ttu-id="f24c9-125">Hello에 `Virtual machine scale set service settings` 블레이드: 원하는 도메인 이름 레이블 (hello base의 hello 크기 집합 앞에 hello 부하 분산 장치에 대 한 FQDN hello)를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-125">On hello `Virtual machine scale set service settings` blade: enter your desired domain name label (hello base of hello FQDN for hello load balancer in front of hello scale set).</span></span> <span data-ttu-id="f24c9-126">이 레이블은 모든 Azure에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-126">This label must be unique across all Azure.</span></span>
* <span data-ttu-id="f24c9-127">원하는 운영 체제 디스크 이미지, 인스턴스 수 및 컴퓨터 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-127">Choose your desired operating system disk image, instance count, and machine size.</span></span>
* <span data-ttu-id="f24c9-128">원하는 디스크 유형 선택: 관리 또는 관리 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-128">Choose your desired disk type: managed or unmanaged.</span></span> <span data-ttu-id="f24c9-129">자세한 내용은 [SDK 설명서](./virtual-machine-scale-sets-managed-disks.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f24c9-129">For more information, see [this documentation](./virtual-machine-scale-sets-managed-disks.md).</span></span> <span data-ttu-id="f24c9-130">Toohave hello 크기 집합을 선택 하는 경우 여러 배치 그룹으로 확장, 관리 되는 디스크 크기 조정 설정 toospan 배치 그룹에 대 한 필요 하므로이 옵션을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-130">If you chose toohave hello scale set span multiple placement groups, this option will not be available because managed disk is required for scale sets toospan placement groups.</span></span>
* <span data-ttu-id="f24c9-131">자동 크기 조정을 사용하거나 사용하지 않도록 설정하고 사용하도록 설정하는 경우 다음을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-131">Enable or disable autoscale and configure if enabled:</span></span>

![ScaleSetPortalService](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalService.PNG)

* <span data-ttu-id="f24c9-133">Hello에 `Summary` 블레이드, 유효성 검사를 수행 하는 경우 클릭 `OK` toostart hello 확장 배포를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-133">On hello `Summary` blade, when validation is done, click `OK` toostart hello scale set deployment.</span></span>


## <a name="connect-tooa-vm-in-hello-scale-set"></a><span data-ttu-id="f24c9-134">Hello 크기 집합의 tooa VM 연결</span><span class="sxs-lookup"><span data-stu-id="f24c9-134">Connect tooa VM in hello scale set</span></span>
<span data-ttu-id="f24c9-135">Toolimit를 선택한 경우 눈금 tooa 단일 배치 그룹을 설정한 다음 toohello에 크기 집합을 쉽게 연결 하는 NAT 구성 된 규칙 toolet hello 크기 집합이 배포 (toocreate 필요할 hello 규모에 맞게 tooconnect toohello 가상 컴퓨터를 설정 하지는 jumpbox hello에 크기 집합 hello와 동일한 가상 네트워크).</span><span class="sxs-lookup"><span data-stu-id="f24c9-135">If you chose toolimit your scale set tooa single placement group, then hello scale set is deployed with NAT rules configured toolet you connect toohello scale set easily (if not, tooconnect toohello virtual machines in hello scale set, you likely need toocreate a jumpbox in hello same virtual network as hello scale set).</span></span> <span data-ttu-id="f24c9-136">toosee toohello 이동, `Inbound NAT Rules` hello 크기 집합에 대 한 hello 부하 분산 장치 탭:</span><span class="sxs-lookup"><span data-stu-id="f24c9-136">toosee them, navigate toohello `Inbound NAT Rules` tab of hello load balancer for hello scale set:</span></span>

![ScaleSetPortalNatRules](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalNatRules.PNG)

<span data-ttu-id="f24c9-138">Tooeach hello 눈금에는 VM이 NAT 규칙을 사용 하 여 집합을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-138">You can connect tooeach VM in hello scale set using these NAT rules.</span></span> <span data-ttu-id="f24c9-139">예를 들어, Windows 크기 집합에 대 한 들어오는 포트 50000에서 NAT 규칙이 있을 경우 수 RDP 통해 toothat 컴퓨터에서 연결할 `<load-balancer-ip-address>:50000`합니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-139">For instance, for a Windows scale set, if there is a NAT rule on incoming port 50000, you could connect toothat machine via RDP on `<load-balancer-ip-address>:50000`.</span></span> <span data-ttu-id="f24c9-140">Hello 명령을 사용 하 여 연결 하듯이 Linux 크기 집합에 대해 `ssh -p 50000 <username>@<load-balancer-ip-address>`합니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-140">For a Linux scale set, you would connect using hello command `ssh -p 50000 <username>@<load-balancer-ip-address>`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f24c9-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f24c9-141">Next steps</span></span>
<span data-ttu-id="f24c9-142">CLI hello에서 toodeploy 비율을 설정 하는 방법에 대 한 설명서를 참조 하십시오. [이 설명서](virtual-machine-scale-sets-cli-quick-create.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-142">For documentation on how toodeploy scale sets from hello CLI, see [this documentation](virtual-machine-scale-sets-cli-quick-create.md).</span></span>

<span data-ttu-id="f24c9-143">PowerShell에서 toodeploy 비율을 설정 하는 방법에 대 한 설명서를 참조 하십시오. [이 설명서](virtual-machine-scale-sets-windows-create.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-143">For documentation on how toodeploy scale sets from PowerShell, see [this documentation](virtual-machine-scale-sets-windows-create.md).</span></span>

<span data-ttu-id="f24c9-144">Visual Studio에서 toodeploy 비율을 설정 하는 방법에 대 한 설명서를 참조 하십시오. [이 설명서](virtual-machine-scale-sets-vs-create.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-144">For documentation on how toodeploy scale sets from Visual Studio, see [this documentation](virtual-machine-scale-sets-vs-create.md).</span></span>

<span data-ttu-id="f24c9-145">일반 설명서에 대 한 체크 아웃 hello [크기 집합에 대 한 설명서 개요 페이지](virtual-machine-scale-sets-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-145">For general documentation, check out hello [documentation overview page for scale sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="f24c9-146">일반 정보에 대 한 체크 아웃 hello [크기 집합에 대 한 기본 방문 페이지](https://azure.microsoft.com/services/virtual-machine-scale-sets/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f24c9-146">For general information, check out hello [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

