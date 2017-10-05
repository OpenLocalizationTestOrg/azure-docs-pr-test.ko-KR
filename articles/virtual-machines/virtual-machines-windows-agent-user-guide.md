---
title: "Azure Virtual Machines 에이전트 개요 | Microsoft Docs"
description: "Azure Virtual Machines 에이전트 개요"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 0a1f212e-053e-4a39-9910-8d622959f594
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: nepeters
ms.openlocfilehash: accfd5f0fec69175e584528ff9f6db66402cb89e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-virtual-machine-agent-overview"></a><span data-ttu-id="7da3f-103">Azure Virtual Machines 에이전트 개요</span><span class="sxs-lookup"><span data-stu-id="7da3f-103">Azure Virtual Machine Agent overview</span></span>

<span data-ttu-id="7da3f-104">Microsoft Azure VM 에이전트(Virtual Machine 에이전트)는 Azure 패브릭 컨트롤러와의 VM 상호 작용을 관리하는 간단한 보안 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-104">The Microsoft Azure Virtual Machine Agent (VM Agent) is a secured, lightweight process that manages VM interaction with the Azure Fabric Controller.</span></span> <span data-ttu-id="7da3f-105">VM 에이전트는 Azure Virtual Machine 확장을 설정하고 실행하는 데 기본적인 역할을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-105">The VM Agent has a primary role in enabling and executing Azure virtual machine extensions.</span></span> <span data-ttu-id="7da3f-106">VM 확장은 소프트웨어 설치 및 구성과 같은 가상 컴퓨터의 배포 후 구성을 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-106">VM Extensions enabling post deployment configuration of virtual machines, such as installing and configuring software.</span></span> <span data-ttu-id="7da3f-107">또한 가상 컴퓨터 확장은 가상 컴퓨터의 관리자 암호를 다시 설정하는 등의 복구 기능도 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-107">Virtual machine extensions also enable recovery features such as resetting the administrative password of a virtual machine.</span></span> <span data-ttu-id="7da3f-108">Azure VM 에이전트가 없으면 가상 컴퓨터 확장을 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-108">Without the Azure VM Agent, virtual machine extensions cannot be run.</span></span>

<span data-ttu-id="7da3f-109">이 문서에서는 Azure Virtual Machine 에이전트의 설치, 검색 및 제거에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-109">This document details installation, detection, and removal of the Azure Virtual Machine Agent.</span></span>

## <a name="install-the-vm-agent"></a><span data-ttu-id="7da3f-110">VM 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="7da3f-110">Install the VM Agent</span></span>

### <a name="azure-gallery-image"></a><span data-ttu-id="7da3f-111">Azure 갤러리 이미지</span><span class="sxs-lookup"><span data-stu-id="7da3f-111">Azure gallery image</span></span>

<span data-ttu-id="7da3f-112">Azure VM 에이전트는 기본적으로 Azure 갤러리 이미지에서 배포된 모든 Windows 가상 컴퓨터에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-112">The Azure VM Agent is installed by default on any Windows virtual machine deployed from an Azure Gallery image.</span></span> <span data-ttu-id="7da3f-113">포털, PowerShell, 명령줄 인터페이스 또는 Azure Resource Manager 템플릿에서 Azure 갤러리 이미지를 배포할 경우 Azure VM 에이전트도 함께 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-113">When deploying an Azure gallery image from the Portal, PowerShell, Command Line Interface, or an Azure Resource Manager template, the Azure VM Agent is also be installed.</span></span> 

### <a name="manual-installation"></a><span data-ttu-id="7da3f-114">수동 설치</span><span class="sxs-lookup"><span data-stu-id="7da3f-114">Manual installation</span></span>

<span data-ttu-id="7da3f-115">Windows VM 에이전트는 Windows 설치 관리자 패키지를 사용하여 수동으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-115">The Windows VM agent can be manually installed using a Windows installer package.</span></span> <span data-ttu-id="7da3f-116">Azure에 배포되는 사용자 지정 가상 컴퓨터 이미지를 만들 때 수동 설치가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-116">Manual installation may be necessary when creating a custom virtual machine image that will be deployed in Azure.</span></span> <span data-ttu-id="7da3f-117">Windows VM 에이전트를 수동으로 설치하려면 이 위치 [Microsoft Azure VM 에이전트 다운로드](http://go.microsoft.com/fwlink/?LinkID=394789)에서 VM 에이전트 설치 관리자를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-117">To manually install the Windows VM Agent, download the VM Agent installer from this location [Windows Azure VM Agent Download](http://go.microsoft.com/fwlink/?LinkID=394789).</span></span> 

<span data-ttu-id="7da3f-118">Windows 설치 관리자 파일을 두 번 클릭하여 VM 에이전트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-118">The VM Agent can be installed by double-clicking the windows installer file.</span></span> <span data-ttu-id="7da3f-119">VM 에이전트를 자동 또는 무인으로 설치하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-119">For an automated or unattended installation of the VM agent, run the following command.</span></span>

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-the-vm-agent"></a><span data-ttu-id="7da3f-120">VM 에이전트 검색</span><span class="sxs-lookup"><span data-stu-id="7da3f-120">Detect the VM Agent</span></span>

### <a name="powershell"></a><span data-ttu-id="7da3f-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7da3f-121">PowerShell</span></span>

<span data-ttu-id="7da3f-122">Azure Resource Manager PowerShell 모듈을 사용하여 Azure Virtual Machines에 대한 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-122">The Azure Resource Manager PowerShell module can be used to retrieve information about Azure Virtual Machines.</span></span> <span data-ttu-id="7da3f-123">`Get-AzureRmVM`을 실행하면 Azure VM 에이전트의 프로비저닝 상태를 비롯한 다양한 정보가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-123">Running `Get-AzureRmVM` returns quite a bit of information including the provisioning state for the Azure VM Agent.</span></span>

```PowerShell
Get-AzureRmVM
```

<span data-ttu-id="7da3f-124">다음은 `Get-AzureRmVM` 출력의 일부에 불과합니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-124">The following is just a subset of the `Get-AzureRmVM` output.</span></span> <span data-ttu-id="7da3f-125">`OSProfile` 내부에 중첩된 `ProvisionVMAgent` 속성을 사용하여 VM 에이전트가 가상 컴퓨터에 배포되었는지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-125">Notice the `ProvisionVMAgent` property nested inside `OSProfile`, this property can be used to determine if the VM agent has been deployed to the virtual machine.</span></span>

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

<span data-ttu-id="7da3f-126">다음 스크립트를 사용하여 가상 컴퓨터 이름 및 VM 에이전트의 상태에 대한 간단한 목록을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-126">The following script can be used to return a concise list of virtual machine names and the state of the VM Agent.</span></span>

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a><span data-ttu-id="7da3f-127">수동 검색</span><span class="sxs-lookup"><span data-stu-id="7da3f-127">Manual Detection</span></span>

<span data-ttu-id="7da3f-128">Microsoft Azure VM에 로그인한 경우 작업 관리자를 사용하여 실행 중인 프로세스를 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-128">When logged in to a Windows Azure VM, task manager can be used to examine running processes.</span></span> <span data-ttu-id="7da3f-129">Azure VM 에이전트를 확인하려면 작업 관리자를 열고 세부 정보 탭을 클릭한 다음 프로세스 이름 `WindowsAzureGuestAgent.exe`를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-129">To check for the Azure VM Agent, open Task Manager > click the details tab, and look for a process name `WindowsAzureGuestAgent.exe`.</span></span> <span data-ttu-id="7da3f-130">이 프로세스가 있으면 VM 에이전트가 설치되어 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-130">The presence of this process indicates that the VM agent is installed.</span></span>

## <a name="upgrade-the-vm-agent"></a><span data-ttu-id="7da3f-131">VM 에이전트 업그레이드</span><span class="sxs-lookup"><span data-stu-id="7da3f-131">Upgrade the VM Agent</span></span>

<span data-ttu-id="7da3f-132">Windows용 Azure VM 에이전트는 자동으로 업그레이드됩니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-132">The Azure VM Agent for Windows is automatically upgraded.</span></span> <span data-ttu-id="7da3f-133">새 가상 컴퓨터는 Azure에 배포될 때 최신 VM 에이전트는 받습니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-133">As new virtual machines are deployed to Azure, they receive the latest VM agent.</span></span> <span data-ttu-id="7da3f-134">새 VM 에이전트를 포함하려면 사용자 지정 VM 이미지를 수동으로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7da3f-134">Custom VM images should be manually updated to include the new VM agent.</span></span>