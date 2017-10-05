---
title: "Azure Portal을 사용하여 가상 컴퓨터 확장 집합 만들기 | Microsoft Docs"
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
ms.openlocfilehash: 7157a429829974b45dad29ac53fb5fb46c71f821
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-virtual-machine-scale-set-with-the-azure-portal"></a><span data-ttu-id="cfbac-104">Azure Portal을 사용하여 가상 컴퓨터 확장 집합을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="cfbac-104">How to create a Virtual Machine Scale Set with the Azure portal</span></span>
<span data-ttu-id="cfbac-105">이 자습서에서는 Azure Portal을 사용하여 가상 컴퓨터 확장 집합을 몇 분 이내에 간편하게 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-105">This tutorial shows you how easy it is to create a Virtual Machine Scale Set in just a few minutes, by using the Azure portal.</span></span> <span data-ttu-id="cfbac-106">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="choose-the-vm-image-from-the-marketplace"></a><span data-ttu-id="cfbac-107">마켓플레이스에서 VM 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-107">Choose the VM image from the marketplace</span></span>
<span data-ttu-id="cfbac-108">포털에서 CentOS, CoreOS, Debian, Open Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, Ubuntu Server 또는 Windows Server 이미지를 사용하여 확장 집합을 쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-108">From the portal, you can easily deploy a scale set with CentOS, CoreOS, Debian, Open Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, Ubuntu Server, or Windows Server images.</span></span>

<span data-ttu-id="cfbac-109">먼저 웹 브라우저에서 [Azure Portal](https://portal.azure.com) 로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-109">First, navigate to the [Azure portal](https://portal.azure.com) in a web browser.</span></span> <span data-ttu-id="cfbac-110">`New`를 클릭하고 `scale set`을 검색한 후 `Virtual machine scale set` 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-110">Click `New`, search for `scale set`, and then select the `Virtual machine scale set` entry:</span></span>

![ScaleSetPortalOverview](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalOverview.PNG)

## <a name="create-the-scale-set"></a><span data-ttu-id="cfbac-112">확장 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="cfbac-112">Create the scale set</span></span>
<span data-ttu-id="cfbac-113">이제 기본 설정을 사용하여 신속하게 확장 집합을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-113">Now you can use the default settings and quickly create the scale set.</span></span>

* <span data-ttu-id="cfbac-114">`Basics` 블레이드에서 확장 집합의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-114">On the `Basics` blade, enter a name for the scale set.</span></span> <span data-ttu-id="cfbac-115">이 이름은 확장 집합 앞에 있는 부하 분산 장치 FQDN의 기반이 됩니다. 따라서 모든 Azure에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-115">This name becomes the base of the FQDN of the load balancer in front of the scale set, so make sure the name is unique across all Azure.</span></span>
* <span data-ttu-id="cfbac-116">원하는 OS 유형을 선택하고, 원하는 사용자 이름을 입력한 후 원하는 인증 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-116">Select your desired OS type, enter your desired username, and select which authentication type you prefer.</span></span> <span data-ttu-id="cfbac-117">암호를 선택하는 경우 12자 이상이어야 하고 1개의 소문자, 1개의 대문자, 1개의 숫자 및 1개의 특수 문자의 네 가지 복잡성 요구 사항 중 적어도 세 가지를 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-117">If you choose a password, it must be at least 12 characters long and meet three out of the four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="cfbac-118">자세한 내용은 [사용자 이름 및 암호 요구 사항](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfbac-118">See more about [username and password requirements](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span> <span data-ttu-id="cfbac-119">`SSH public key`를 선택하는 경우 개인 키가 아니라 공개 키만 붙여넣어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-119">If you choose `SSH public key`, be sure to only paste in your public key, NOT your private key:</span></span>

![ScaleSetPortalBasics](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalBasics.PNG)

* <span data-ttu-id="cfbac-121">단일 배치 그룹으로 설정하여 확장 집합을 제한하기를 원하는지 또는 여러 개의 배치 그룹에 걸쳐 확장해야 하는지 여부를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-121">Choose whether you would like to limit the scale set to a single placement group or whether it should span multiple placement groups.</span></span> <span data-ttu-id="cfbac-122">확장 집합을 배치 그룹으로 확장할 수 있도록 허용하면 특정 제한 사항과 함께 확장 집합은 용량이 100VM 이상(최대 1,000개) 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-122">Allowing the scale set to span placement groups allows for scale sets over 100 VMs in capacity (up to 1,000) with certain limitations.</span></span> <span data-ttu-id="cfbac-123">자세한 내용은 [SDK 설명서](./virtual-machine-scale-sets-placement-groups.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfbac-123">For more information, see [this documentation](./virtual-machine-scale-sets-placement-groups.md).</span></span>
* <span data-ttu-id="cfbac-124">원하는 리소스 그룹 이름 및 위치를 입력한 다음 `OK`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-124">Enter your desired resource group name and location, and then click `OK`.</span></span>
* <span data-ttu-id="cfbac-125">`Virtual machine scale set service settings` 블레이드에서 원하는 도메인 이름 레이블(확장 집합 앞에 있는 부하 분산 장치 FQDN의 기준)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-125">On the `Virtual machine scale set service settings` blade: enter your desired domain name label (the base of the FQDN for the load balancer in front of the scale set).</span></span> <span data-ttu-id="cfbac-126">이 레이블은 모든 Azure에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-126">This label must be unique across all Azure.</span></span>
* <span data-ttu-id="cfbac-127">원하는 운영 체제 디스크 이미지, 인스턴스 수 및 컴퓨터 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-127">Choose your desired operating system disk image, instance count, and machine size.</span></span>
* <span data-ttu-id="cfbac-128">원하는 디스크 유형 선택: 관리 또는 관리 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-128">Choose your desired disk type: managed or unmanaged.</span></span> <span data-ttu-id="cfbac-129">자세한 내용은 [SDK 설명서](./virtual-machine-scale-sets-managed-disks.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfbac-129">For more information, see [this documentation](./virtual-machine-scale-sets-managed-disks.md).</span></span> <span data-ttu-id="cfbac-130">확장 집합을 여러 배치 그룹으로 확장하도록 선택한 경우 이 옵션은 확장 집합을 배치 그룹으로 확장하는 데 관리되는 디스크가 필요하기 때문에 이 옵션을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-130">If you chose to have the scale set span multiple placement groups, this option will not be available because managed disk is required for scale sets to span placement groups.</span></span>
* <span data-ttu-id="cfbac-131">자동 크기 조정을 사용하거나 사용하지 않도록 설정하고 사용하도록 설정하는 경우 다음을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-131">Enable or disable autoscale and configure if enabled:</span></span>

![ScaleSetPortalService](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalService.PNG)

* <span data-ttu-id="cfbac-133">`Summary` 블레이드에서 유효성 검사가 수행되면 `OK`를 클릭하여 확장 집합 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-133">On the `Summary` blade, when validation is done, click `OK` to start the scale set deployment.</span></span>


## <a name="connect-to-a-vm-in-the-scale-set"></a><span data-ttu-id="cfbac-134">확장 집합의 VM에 연결</span><span class="sxs-lookup"><span data-stu-id="cfbac-134">Connect to a VM in the scale set</span></span>
<span data-ttu-id="cfbac-135">단일 배치 그룹으로 설정된 규모를 제한하기로 선택한 경우에 확장 집합에 쉽게 연결할 수 있도록 구성하는 NAT 규칙과 함께 확장 집합이 배포됩니다(그렇지 않으면 확장 집합에 있는 가상 컴퓨터에 연결하려면 확장 집합과 동일한 가상 네트워크에 jumpbox를 만들어야 할 수 있습니다).</span><span class="sxs-lookup"><span data-stu-id="cfbac-135">If you chose to limit your scale set to a single placement group, then the scale set is deployed with NAT rules configured to let you connect to the scale set easily (if not, to connect to the virtual machines in the scale set, you likely need to create a jumpbox in the same virtual network as the scale set).</span></span> <span data-ttu-id="cfbac-136">이를 보려면 확장 집합에 대한 부하 분산 장치의 `Inbound NAT Rules` 탭을 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-136">To see them, navigate to the `Inbound NAT Rules` tab of the load balancer for the scale set:</span></span>

![ScaleSetPortalNatRules](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalNatRules.PNG)

<span data-ttu-id="cfbac-138">이러한 NAT 규칙을 사용하여 확장 집합의 각 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-138">You can connect to each VM in the scale set using these NAT rules.</span></span> <span data-ttu-id="cfbac-139">예를 들어 Windows 확장 집합의 경우 수신 포트 50000에 대한 NAT 규칙이 있으면 `<load-balancer-ip-address>:50000`의 RDP를 통해 해당 컴퓨터에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-139">For instance, for a Windows scale set, if there is a NAT rule on incoming port 50000, you could connect to that machine via RDP on `<load-balancer-ip-address>:50000`.</span></span> <span data-ttu-id="cfbac-140">Linux 확장 집합의 경우 `ssh -p 50000 <username>@<load-balancer-ip-address>`명령을 사용하여 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfbac-140">For a Linux scale set, you would connect using the command `ssh -p 50000 <username>@<load-balancer-ip-address>`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfbac-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cfbac-141">Next steps</span></span>
<span data-ttu-id="cfbac-142">CLI에서 확장 집합을 배포하는 방법에 대한 설명서를 보려면 [이 설명서](virtual-machine-scale-sets-cli-quick-create.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfbac-142">For documentation on how to deploy scale sets from the CLI, see [this documentation](virtual-machine-scale-sets-cli-quick-create.md).</span></span>

<span data-ttu-id="cfbac-143">PowerShell에서 확장 집합을 배포하는 방법에 대한 설명서를 보려면 [이 설명서](virtual-machine-scale-sets-windows-create.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfbac-143">For documentation on how to deploy scale sets from PowerShell, see [this documentation](virtual-machine-scale-sets-windows-create.md).</span></span>

<span data-ttu-id="cfbac-144">Visual Studio에서 확장 집합을 배포하는 방법에 대한 설명서를 보려면 [이 설명서](virtual-machine-scale-sets-vs-create.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfbac-144">For documentation on how to deploy scale sets from Visual Studio, see [this documentation](virtual-machine-scale-sets-vs-create.md).</span></span>

<span data-ttu-id="cfbac-145">일반 설명서는 [확장 집합에 대한 설명서 개요 페이지](virtual-machine-scale-sets-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfbac-145">For general documentation, check out the [documentation overview page for scale sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="cfbac-146">일반적인 정보는 [확장 집합에 대한 주 방문 페이지](https://azure.microsoft.com/services/virtual-machine-scale-sets/)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="cfbac-146">For general information, check out the [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

