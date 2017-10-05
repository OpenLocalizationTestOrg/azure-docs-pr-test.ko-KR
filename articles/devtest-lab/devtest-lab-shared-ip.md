---
title: "Azure DevTest Labs에서 공유 IP 주소 이해 | Microsoft Docs"
description: "Azure DevTest Labs에서 공유 IP 주소를 사용하여 랩 VM에 액세스하는 데 필요한 공용 IP 주소를 최소화하는 방법에 대해 알아봅니다."
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: 9f6e1980bf5ea5b41da98a135d89f1c5159921a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a><span data-ttu-id="ef8d4-103">Azure DevTest Labs에서 공유 IP 주소 이해</span><span class="sxs-lookup"><span data-stu-id="ef8d4-103">Understand shared IP addresses in Azure DevTest Labs</span></span>

<span data-ttu-id="ef8d4-104">Azure DevTest Labs에서는 랩 VM이 동일한 공용 IP 주소를 공유하여 개별 랩 VM에 액세스하는 데 필요한 공용 IP 주소 수를 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef8d4-104">Azure DevTest Labs lets lab VMs share the same public IP address to minimize the number of public IP addresses required to access your individual lab VMs.</span></span>  <span data-ttu-id="ef8d4-105">이 문서에서는 공유 IP의 작동 방식과 관련 구성 옵션에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ef8d4-105">This article describes how shared IPs work and their related configuration options.</span></span>

## <a name="shared-ip-setting"></a><span data-ttu-id="ef8d4-106">공유 IP 설정</span><span class="sxs-lookup"><span data-stu-id="ef8d4-106">Shared IP setting</span></span>

<span data-ttu-id="ef8d4-107">랩을 만들면 가상 네트워크의 서브넷에 상주합니다.</span><span class="sxs-lookup"><span data-stu-id="ef8d4-107">When you create a lab, it resides in a subnet of a virtual network.</span></span>  <span data-ttu-id="ef8d4-108">기본적으로 이 서브넷은 **Enable shared public IP**(공유 공용 IP 사용)을 *예*로 설정하면 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef8d4-108">By default, this subnet is created with **Enable shared public IP** set to *Yes*.</span></span>  <span data-ttu-id="ef8d4-109">이 구성은 전체 서브넷에 하나의 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef8d4-109">This configuration creates one public IP address for the entire subnet.</span></span>  <span data-ttu-id="ef8d4-110">가상 네트워크 및 서브넷 구성에 대한 자세한 내용은 [Azure DevTest Labs에서 가상 네트워크 구성](devtest-lab-configure-vnet.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef8d4-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span></span>

![새 랩 서브넷](media/devtest-lab-shared-ip/lab-subnet.png)

<span data-ttu-id="ef8d4-112">기존 랩의 경우 **구성 및 정책 > Virtual Networks**를 선택하여 이 옵션을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef8d4-112">For existing labs, you can enable this option by selecting **Configuration and policies > Virtual Networks**.</span></span> <span data-ttu-id="ef8d4-113">그런 다음, 목록에서 가상 네트워크를 선택하고 선택한 서브넷에 대해 **공유 공용 IP 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef8d4-113">Then, select a virtual network from the list and choose **ENABLE SHARED PUBLIC IP** for a selected subnet.</span></span> <span data-ttu-id="ef8d4-114">랩 VM 간에 공용 IP 주소를 공유하지 않으려는 경우 아무 랩에서나 이 옵션을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef8d4-114">You can also disable this option in any lab if you don't want to share a public IP address across lab VMs.</span></span>

<span data-ttu-id="ef8d4-115">이 랩에 생성된 모든 VM은 기본적으로 공유 IP를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ef8d4-115">Any VMs created in this lab default to using a shared IP.</span></span>  <span data-ttu-id="ef8d4-116">VM을 만들 때 **IP 주소 구성** 아래 **고급 설정** 블레이드에서 이 설정을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef8d4-116">When creating the VM, this setting can be observed in the **Advanced settings** blade under **IP address configuration**.</span></span>

![새 VM](media/devtest-lab-shared-ip/new-vm.png)

- <span data-ttu-id="ef8d4-118">**공유:** **공유**로 생성된 모든 VM은 하나의 리소스 그룹(RG)에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef8d4-118">**Shared:** All VMs created as **Shared** are placed into one resource group (RG).</span></span> <span data-ttu-id="ef8d4-119">해당 RG에는 단일 IP 주소가 할당되며, RG에 있는 모든 VM은 이 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ef8d4-119">A single IP address is assigned for that RG and all VMs in the RG will use that IP address.</span></span>
- <span data-ttu-id="ef8d4-120">**공개:** 만든 각 VM에 자체 IP 주소가 있으며 자체 리소스 그룹에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef8d4-120">**Public:** Every VM you create has its own IP address and is created in its own resource group.</span></span>
- <span data-ttu-id="ef8d4-121">**비공개:** 만든 각 VM이 개인 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ef8d4-121">**Private:** Every VM you create uses a private IP address.</span></span> <span data-ttu-id="ef8d4-122">원격 데스크톱을 사용하여 인터넷에서 직접 이 VM에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ef8d4-122">You will not be able to connect to this VM directly from the internet with Remote Desktop.</span></span>

<span data-ttu-id="ef8d4-123">공유 IP가 사용된 VM이 서브넷에 추가될 때마다 DevTest Labs는 자동으로 부하 분산 장치에 VM을 추가하고 공용 IP 주소에 TCP 포트 번호를 할당하여 VM의 RDP 포트에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ef8d4-123">Whenever a VM with shared IP enabled is added to the subnet, DevTest Labs automatically adds the VM to a load balancer and assigns a TCP port number on the public IP address, forwarding to the RDP port on the VM.</span></span>  

## <a name="using-the-shared-ip"></a><span data-ttu-id="ef8d4-124">공유 IP 사용</span><span class="sxs-lookup"><span data-stu-id="ef8d4-124">Using the shared IP</span></span>

- <span data-ttu-id="ef8d4-125">**Linux 사용자:** IP 주소 또는 정규화된 도메인 이름, 콜론, 포트를 순서대로 사용하여 VM에 SSH합니다.</span><span class="sxs-lookup"><span data-stu-id="ef8d4-125">**Linux users:** SSH to the VM by using the IP address or fully qualified domain name, followed by a colon, followed by the port.</span></span> <span data-ttu-id="ef8d4-126">예를 들어 아래 이미지에서 VM에 연결되는 RDP 주소는 `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`입니다.</span><span class="sxs-lookup"><span data-stu-id="ef8d4-126">For example, in the image below, the RDP address to connect to the VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span></span>

  ![VM 예](media/devtest-lab-shared-ip/vm-info.png)

- <span data-ttu-id="ef8d4-128">**Windows 사용자:** Azure Portal에서 **연결** 단추를 선택하여 미리 구성된 RDP 파일을 다운로드하고 VM에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="ef8d4-128">**Windows users:** Select the **Connect** button on the Azure portal to download a pre-configured RDP file and access the VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef8d4-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ef8d4-129">Next steps</span></span>

* [<span data-ttu-id="ef8d4-130">Azure DevTest Labs에서 랩 정책 정의</span><span class="sxs-lookup"><span data-stu-id="ef8d4-130">Define lab policies in Azure DevTest Labs</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="ef8d4-131">Azure DevTest Labs에서 가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="ef8d4-131">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md)





