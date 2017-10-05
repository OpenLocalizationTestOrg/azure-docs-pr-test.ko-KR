---
title: "Azure에서 Windows VM에 Symantec Endpoint Protection 설치 | Microsoft Docs"
description: "클래식 배포 모델을 사용하여 새로운 또는 기존 Azure VM에 Symantec Endpoint Protection 보안 확장을 설치하고 구성하는 방법을 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 19dcebc7-da6b-4510-907b-d64088e81fa2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: iainfou
ms.openlocfilehash: 1603ebc7ee3c29277f30fbb802bdd8205b92d648
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a><span data-ttu-id="37415-103">Windows VM에서 Symantec Endpoint Protection을 설치하고 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="37415-103">How to install and configure Symantec Endpoint Protection on a Windows VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="37415-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37415-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="37415-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="37415-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="37415-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="37415-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="37415-107">이 문서에서는 Windows Server가 실행되는 기존 VM(가상 컴퓨터)에서 Symantec Endpoint Protection 클라이언트를 설치하고 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="37415-107">This article shows you how to install and configure the Symantec Endpoint Protection client on an existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="37415-108">이 전체 클라이언트는 바이러스 및 스파이웨어 보호, 방화벽, 침입 방지와 같은 서비스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="37415-108">This full client includes services such as virus and spyware protection, firewall, and intrusion prevention.</span></span> <span data-ttu-id="37415-109">이 클라이언트는 VM 에이전트를 사용하여 보안 확장 프로그램으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="37415-109">The client is installed as a security extension by using the VM Agent.</span></span>

<span data-ttu-id="37415-110">온-프레미스 솔루션용 Symantec의 기존 구독이 있는 경우 Azure 가상 컴퓨터를 보호하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37415-110">If you have an existing subscription from Symantec for an on-premises solution, you can use it to protect your Azure virtual machines.</span></span> <span data-ttu-id="37415-111">아직 구독 고객이 아닌 경우에는 평가판 구독에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37415-111">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="37415-112">이 솔루션에 대한 자세한 내용은 [Microsoft Azure 플랫폼의 Symantec Endpoint Protection][Symantec](영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37415-112">For more information about this solution, see [Symantec Endpoint Protection on Microsoft's Azure platform][Symantec].</span></span> <span data-ttu-id="37415-113">이 페이지에는 Symantec 고객을 위한 라이선스 정보 및 이 클라이언트를 설치하는 방법에 대한 링크도 제공되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37415-113">This page also has links to licensing information and instructions for installing the client if you're already a Symantec customer.</span></span>

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a><span data-ttu-id="37415-114">기존 VM에 Symantec Endpoint Protection 설치</span><span class="sxs-lookup"><span data-stu-id="37415-114">Install Symantec Endpoint Protection on an existing VM</span></span>
<span data-ttu-id="37415-115">이 작업을 시작하려면 다음 조건을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37415-115">Before you begin, you need the following:</span></span>

* <span data-ttu-id="37415-116">Azure PowerShell 모듈 버전 0.8.2 이상이 작업 컴퓨터에 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37415-116">The Azure PowerShell module, version 0.8.2 or later, on your work computer.</span></span> <span data-ttu-id="37415-117">**Get-Module azure | format-table version** 명령을 사용하여 설치한 Azure PowerShell의 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37415-117">You can check the version of Azure PowerShell that you have installed with the **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="37415-118">지침 및 최신 버전에 대한 링크를 보려면 [Azure PowerShell을 설치 및 구성하는 방법][PS]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37415-118">For instructions and a link to the latest version, see [How to Install and Configure Azure PowerShell][PS].</span></span> <span data-ttu-id="37415-119">`Add-AzureAccount`를 사용하여 Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="37415-119">Log in to your Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="37415-120">Azure 가상 컴퓨터에서 VM 에이전트를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37415-120">The VM Agent running on the Azure Virtual Machine.</span></span>

<span data-ttu-id="37415-121">먼저, VM 에이전트가 가상 컴퓨터에 이미 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="37415-121">First, verify that the VM Agent is already installed on the virtual machine.</span></span> <span data-ttu-id="37415-122">클라우드 서비스 이름과 가상 컴퓨터 이름을 입력하고 관리자 수준의 Azure PowerShell 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="37415-122">Fill in the cloud service name and virtual machine name, and then run the following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="37415-123">< 및 > 문자를 포함하여 따옴표 안의 모든 항목을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="37415-123">Replace everything within the quotes, including the < and > characters.</span></span>

> [!TIP]
> <span data-ttu-id="37415-124">클라우드 서비스 및 가상 컴퓨터 이름을 모르는 경우 **Get-AzureVM** 을 실행하여 현재 구독의 모든 가상 컴퓨터에 대해 이름을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="37415-124">If you don't know the cloud service and virtual machine names, run **Get-AzureVM** to list the names for all virtual machines in your current subscription.</span></span>

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="37415-125">**write-host** 명령에서 **True**가 표시되면 VM 에이전트가 설치되어 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="37415-125">If the **write-host** command displays **True**, the VM Agent is installed.</span></span> <span data-ttu-id="37415-126">**False**가 표시되면 Azure 블로그 게시물 [VM 에이전트 및 확장 - 2부][Agent]에서 지침 및 다운로드 링크를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="37415-126">If it displays **False**, see the instructions and a link to the download in the Azure blog post [VM Agent and Extensions - Part 2][Agent].</span></span>

<span data-ttu-id="37415-127">VM 에이전트가 설치된 경우 이러한 명령을 실행하여 Symantec Endpoint Protection 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="37415-127">If the VM Agent is installed, run these commands to install the Symantec Endpoint Protection agent.</span></span>

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

<span data-ttu-id="37415-128">Symantec 보안 확장이 설치되고 최신 상태인지 확인하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="37415-128">To verify that the Symantec security extension has been installed and is up-to-date:</span></span>

1. <span data-ttu-id="37415-129">가상 컴퓨터에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="37415-129">Log on to the virtual machine.</span></span> <span data-ttu-id="37415-130">지침은 [Windows Server를 실행하는 가상 컴퓨터에 로그온하는 방법][Logon]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37415-130">For instructions, see [How to Log on to a Virtual Machine Running Windows Server][Logon].</span></span>
2. <span data-ttu-id="37415-131">Windows Server 2008 R2의 경우, **시작 > Symantec Endpoint Protection**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37415-131">For Windows Server 2008 R2, click **Start > Symantec Endpoint Protection**.</span></span> <span data-ttu-id="37415-132">Windows Server 2012 또는 Windows Server 2012 R2의 경우, 시작 화면에서 **Symantec**을 입력하고 **Symantec Endpoint Protection**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37415-132">For Windows Server 2012 or Windows Server 2012 R2, from the start screen, type **Symantec**, and then click **Symantec Endpoint Protection**.</span></span>
3. <span data-ttu-id="37415-133">**Status-Symantec Endpoint Protection** 창의 **상태** 탭에서 필요한 경우 업데이트를 적용하거나 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="37415-133">From the **Status** tab of the **Status-Symantec Endpoint Protection** window, apply updates or restart if needed.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="37415-134">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="37415-134">Additional resources</span></span>
<span data-ttu-id="37415-135">[Windows Server를 실행하는 가상 컴퓨터에 로그온하는 방법][Logon]</span><span class="sxs-lookup"><span data-stu-id="37415-135">[How to Log on to a Virtual Machine Running Windows Server][Logon]</span></span>

<span data-ttu-id="37415-136">[Azure VM 확장 및 기능][Ext]</span><span class="sxs-lookup"><span data-stu-id="37415-136">[Azure VM Extensions and Features][Ext]</span></span>

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
