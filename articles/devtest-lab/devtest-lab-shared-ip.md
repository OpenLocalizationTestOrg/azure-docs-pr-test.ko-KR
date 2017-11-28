---
title: "aaaUnderstand Azure DevTest Labs에서 IP 주소를 공유 | Microsoft Docs"
description: "Azure DevTest Labs 사용 하는 방법을 공유 IP 주소 toominimize hello 공용 IP 주소가 필요한 tooaccess 랩 Vm에 알아봅니다."
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
ms.openlocfilehash: 8756410117a9d550d567d372174bf1ea96703c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a><span data-ttu-id="f00e9-103">Azure DevTest Labs에서 공유 IP 주소 이해</span><span class="sxs-lookup"><span data-stu-id="f00e9-103">Understand shared IP addresses in Azure DevTest Labs</span></span>

<span data-ttu-id="f00e9-104">동일한 공용 IP 주소 toominimize hello 수의 공용 IP 주소가 필요한 tooaccess 개별 랩 Vm hello 하는 azure DevTest Labs 하면 랩 Vm 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="f00e9-104">Azure DevTest Labs lets lab VMs share hello same public IP address toominimize hello number of public IP addresses required tooaccess your individual lab VMs.</span></span>  <span data-ttu-id="f00e9-105">이 문서에서는 공유 IP의 작동 방식과 관련 구성 옵션에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f00e9-105">This article describes how shared IPs work and their related configuration options.</span></span>

## <a name="shared-ip-setting"></a><span data-ttu-id="f00e9-106">공유 IP 설정</span><span class="sxs-lookup"><span data-stu-id="f00e9-106">Shared IP setting</span></span>

<span data-ttu-id="f00e9-107">랩을 만들면 가상 네트워크의 서브넷에 상주합니다.</span><span class="sxs-lookup"><span data-stu-id="f00e9-107">When you create a lab, it resides in a subnet of a virtual network.</span></span>  <span data-ttu-id="f00e9-108">기본적으로이 서브넷을 만든 **공용 IP를 공유 하는 활성화** 도*예*합니다.</span><span class="sxs-lookup"><span data-stu-id="f00e9-108">By default, this subnet is created with **Enable shared public IP** set too*Yes*.</span></span>  <span data-ttu-id="f00e9-109">이 구성은 hello 전체 서브넷에 대 한 공용 IP 주소를 하나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f00e9-109">This configuration creates one public IP address for hello entire subnet.</span></span>  <span data-ttu-id="f00e9-110">가상 네트워크 및 서브넷 구성에 대한 자세한 내용은 [Azure DevTest Labs에서 가상 네트워크 구성](devtest-lab-configure-vnet.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f00e9-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span></span>

![새 랩 서브넷](media/devtest-lab-shared-ip/lab-subnet.png)

<span data-ttu-id="f00e9-112">기존 랩의 경우 **구성 및 정책 > Virtual Networks**를 선택하여 이 옵션을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f00e9-112">For existing labs, you can enable this option by selecting **Configuration and policies > Virtual Networks**.</span></span> <span data-ttu-id="f00e9-113">그런 다음 hello 목록에서 가상 네트워크를 선택 하 고 선택 **공유 공용 IP를 사용 하도록 설정** 선택한 서브넷에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f00e9-113">Then, select a virtual network from hello list and choose **ENABLE SHARED PUBLIC IP** for a selected subnet.</span></span> <span data-ttu-id="f00e9-114">랩 Vm에서 공용 IP 주소를 tooshare 않으려는 경우에 모든 랩에이 옵션을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f00e9-114">You can also disable this option in any lab if you don't want tooshare a public IP address across lab VMs.</span></span>

<span data-ttu-id="f00e9-115">모든 Vm 공유 IP이 랩 기본 toousing에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f00e9-115">Any VMs created in this lab default toousing a shared IP.</span></span>  <span data-ttu-id="f00e9-116">이 설정은 hello에서 관측할 수 hello VM을 만들 때 **고급 설정** 아래 블레이드 **IP 주소 구성을**합니다.</span><span class="sxs-lookup"><span data-stu-id="f00e9-116">When creating hello VM, this setting can be observed in hello **Advanced settings** blade under **IP address configuration**.</span></span>

![새 VM](media/devtest-lab-shared-ip/new-vm.png)

- <span data-ttu-id="f00e9-118">**공유:** **공유**로 생성된 모든 VM은 하나의 리소스 그룹(RG)에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="f00e9-118">**Shared:** All VMs created as **Shared** are placed into one resource group (RG).</span></span> <span data-ttu-id="f00e9-119">단일 IP 주소는 RG hello RG에 있는 모든 Vm은 사용 해당 IP 주소 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f00e9-119">A single IP address is assigned for that RG and all VMs in hello RG will use that IP address.</span></span>
- <span data-ttu-id="f00e9-120">**공개:** 만든 각 VM에 자체 IP 주소가 있으며 자체 리소스 그룹에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f00e9-120">**Public:** Every VM you create has its own IP address and is created in its own resource group.</span></span>
- <span data-ttu-id="f00e9-121">**비공개:** 만든 각 VM이 개인 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f00e9-121">**Private:** Every VM you create uses a private IP address.</span></span> <span data-ttu-id="f00e9-122">Hello에서 직접 VM 수 tooconnect toothis 됩니다 인터넷 원격 데스크톱을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f00e9-122">You will not be able tooconnect toothis VM directly from hello internet with Remote Desktop.</span></span>

<span data-ttu-id="f00e9-123">사용 하도록 설정 하는 공유 IP 사용 하 여 VM toohello 서브넷을 추가할 때마다 DevTest Labs 자동으로 hello VM tooa 부하 분산 장치 더하고 toohello hello VM의 RDP 포트 전달 hello 공용 IP 주소에 TCP 포트 번호를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="f00e9-123">Whenever a VM with shared IP enabled is added toohello subnet, DevTest Labs automatically adds hello VM tooa load balancer and assigns a TCP port number on hello public IP address, forwarding toohello RDP port on hello VM.</span></span>  

## <a name="using-hello-shared-ip"></a><span data-ttu-id="f00e9-124">IP 공유 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="f00e9-124">Using hello shared IP</span></span>

- <span data-ttu-id="f00e9-125">**Linux 사용자:** hello IP 주소 또는 정규화 된 도메인 이름, 그 뒤에 콜론을 사용 하 여 SSH toohello VM hello 포트 옵니다.</span><span class="sxs-lookup"><span data-stu-id="f00e9-125">**Linux users:** SSH toohello VM by using hello IP address or fully qualified domain name, followed by a colon, followed by hello port.</span></span> <span data-ttu-id="f00e9-126">예를 들어 아래 hello 이미지 hello RDP 중점적으로 다루고 tooconnect toohello VM은 `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`합니다.</span><span class="sxs-lookup"><span data-stu-id="f00e9-126">For example, in hello image below, hello RDP address tooconnect toohello VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span></span>

  ![VM 예](media/devtest-lab-shared-ip/vm-info.png)

- <span data-ttu-id="f00e9-128">**Windows 사용자에 게:** 선택 hello **연결** 미리 구성 된 RDP 파일을 Azure 포털 toodownload hello에서 단추 및 hello VM에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="f00e9-128">**Windows users:** Select hello **Connect** button on hello Azure portal toodownload a pre-configured RDP file and access hello VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f00e9-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f00e9-129">Next steps</span></span>

* [<span data-ttu-id="f00e9-130">Azure DevTest Labs에서 랩 정책 정의</span><span class="sxs-lookup"><span data-stu-id="f00e9-130">Define lab policies in Azure DevTest Labs</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="f00e9-131">Azure DevTest Labs에서 가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="f00e9-131">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md)





