---
title: "가상 컴퓨터 에이전트 개요 aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 178766925673419cd661dbb460b8427bbfaf54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-agent-overview"></a><span data-ttu-id="fa277-103">Azure Virtual Machines 에이전트 개요</span><span class="sxs-lookup"><span data-stu-id="fa277-103">Azure Virtual Machine Agent overview</span></span>

<span data-ttu-id="fa277-104">Microsoft Azure 가상 컴퓨터 에이전트 (VM 에이전트) hello는 hello Azure 패브릭 컨트롤러와 VM의 상호 작용을 관리 하는 안전 하 고 간단한 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-104">hello Microsoft Azure Virtual Machine Agent (VM Agent) is a secured, lightweight process that manages VM interaction with hello Azure Fabric Controller.</span></span> <span data-ttu-id="fa277-105">hello VM 에이전트를 사용 하도록 설정 하 고 Azure 가상 컴퓨터 확장 실행에서 기본 역할을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-105">hello VM Agent has a primary role in enabling and executing Azure virtual machine extensions.</span></span> <span data-ttu-id="fa277-106">VM 확장은 소프트웨어 설치 및 구성과 같은 가상 컴퓨터의 배포 후 구성을 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-106">VM Extensions enabling post deployment configuration of virtual machines, such as installing and configuring software.</span></span> <span data-ttu-id="fa277-107">또한 가상 컴퓨터 확장 hello 가상 컴퓨터의 관리자 암호를 재설정 하는 등의 복구 기능을 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-107">Virtual machine extensions also enable recovery features such as resetting hello administrative password of a virtual machine.</span></span> <span data-ttu-id="fa277-108">Hello Azure VM 에이전트 없이 가상 컴퓨터 확장을 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-108">Without hello Azure VM Agent, virtual machine extensions cannot be run.</span></span>

<span data-ttu-id="fa277-109">설치, 검색, 및의 hello Azure 가상 컴퓨터 에이전트 제거가이 문서에 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-109">This document details installation, detection, and removal of hello Azure Virtual Machine Agent.</span></span>

## <a name="install-hello-vm-agent"></a><span data-ttu-id="fa277-110">Hello VM 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-110">Install hello VM Agent</span></span>

### <a name="azure-gallery-image"></a><span data-ttu-id="fa277-111">Azure 갤러리 이미지</span><span class="sxs-lookup"><span data-stu-id="fa277-111">Azure gallery image</span></span>

<span data-ttu-id="fa277-112">hello Azure VM 에이전트는 Azure 갤러리 이미지에서 배포 된 모든 Windows 가상 컴퓨터에서 기본적으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-112">hello Azure VM Agent is installed by default on any Windows virtual machine deployed from an Azure Gallery image.</span></span> <span data-ttu-id="fa277-113">Hello 포털, PowerShell, 명령줄 인터페이스 또는 Azure 리소스 관리자 템플릿에서 Azure 갤러리 이미지를 배포할 때 hello Azure VM 에이전트는도 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-113">When deploying an Azure gallery image from hello Portal, PowerShell, Command Line Interface, or an Azure Resource Manager template, hello Azure VM Agent is also be installed.</span></span> 

### <a name="manual-installation"></a><span data-ttu-id="fa277-114">수동 설치</span><span class="sxs-lookup"><span data-stu-id="fa277-114">Manual installation</span></span>

<span data-ttu-id="fa277-115">Windows installer 패키지를 사용 하 여 hello Windows VM 에이전트를 수동으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-115">hello Windows VM agent can be manually installed using a Windows installer package.</span></span> <span data-ttu-id="fa277-116">Azure에 배포되는 사용자 지정 가상 컴퓨터 이미지를 만들 때 수동 설치가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-116">Manual installation may be necessary when creating a custom virtual machine image that will be deployed in Azure.</span></span> <span data-ttu-id="fa277-117">이 위치에서 hello VM 에이전트 설치 관리자를 다운로드 하는 Windows VM 에이전트 toomanually 설치 hello [Windows Azure VM 에이전트 다운로드](http://go.microsoft.com/fwlink/?LinkID=394789)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-117">toomanually install hello Windows VM Agent, download hello VM Agent installer from this location [Windows Azure VM Agent Download](http://go.microsoft.com/fwlink/?LinkID=394789).</span></span> 

<span data-ttu-id="fa277-118">hello windows installer 파일을 두 번 클릭 하 여 hello VM 에이전트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-118">hello VM Agent can be installed by double-clicking hello windows installer file.</span></span> <span data-ttu-id="fa277-119">Hello VM 에이전트의 자동 또는 무인 설치를 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-119">For an automated or unattended installation of hello VM agent, run hello following command.</span></span>

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-hello-vm-agent"></a><span data-ttu-id="fa277-120">Hello VM 에이전트를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-120">Detect hello VM Agent</span></span>

### <a name="powershell"></a><span data-ttu-id="fa277-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fa277-121">PowerShell</span></span>

<span data-ttu-id="fa277-122">hello Azure 리소스 관리자 PowerShell 모듈 사용된 tooretrieve 정보에 대 한 Azure 가상 컴퓨터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-122">hello Azure Resource Manager PowerShell module can be used tooretrieve information about Azure Virtual Machines.</span></span> <span data-ttu-id="fa277-123">실행 `Get-AzureRmVM` 많은 양의 hello 프로비저닝 hello Azure VM 에이전트에 대 한 상태 등의 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-123">Running `Get-AzureRmVM` returns quite a bit of information including hello provisioning state for hello Azure VM Agent.</span></span>

```PowerShell
Get-AzureRmVM
```

<span data-ttu-id="fa277-124">hello 다음은 hello의 일부만 `Get-AzureRmVM` 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-124">hello following is just a subset of hello `Get-AzureRmVM` output.</span></span> <span data-ttu-id="fa277-125">공지 hello `ProvisionVMAgent` 속성 내에 중첩 된 `OSProfile`, hello VM 에이전트가 가상 컴퓨터 배포 toohello 되어 있으면이 속성 사용된 toodetermine 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-125">Notice hello `ProvisionVMAgent` property nested inside `OSProfile`, this property can be used toodetermine if hello VM agent has been deployed toohello virtual machine.</span></span>

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

<span data-ttu-id="fa277-126">다음 스크립트는 hello 사용된 tooreturn 간결 하 게 가상 컴퓨터 이름 및 hello VM 에이전트의 hello 상태 목록이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-126">hello following script can be used tooreturn a concise list of virtual machine names and hello state of hello VM Agent.</span></span>

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a><span data-ttu-id="fa277-127">수동 검색</span><span class="sxs-lookup"><span data-stu-id="fa277-127">Manual Detection</span></span>

<span data-ttu-id="fa277-128">Windows Azure VM tooa 로그인, 작업 관리자 실행 중인 프로세스에 사용 되는 tooexamine 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-128">When logged in tooa Windows Azure VM, task manager can be used tooexamine running processes.</span></span> <span data-ttu-id="fa277-129">toocheck hello Azure VM 에이전트에 대 한 작업 관리자를 열고 > hello 세부 정보 탭을 클릭 하 고 프로세스 이름에 대 한 확인 `WindowsAzureGuestAgent.exe`합니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-129">toocheck for hello Azure VM Agent, open Task Manager > click hello details tab, and look for a process name `WindowsAzureGuestAgent.exe`.</span></span> <span data-ttu-id="fa277-130">이 프로세스의 hello 존재 해당 hello VM 에이전트가 설치 된 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-130">hello presence of this process indicates that hello VM agent is installed.</span></span>

## <a name="upgrade-hello-vm-agent"></a><span data-ttu-id="fa277-131">Hello VM 에이전트를 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-131">Upgrade hello VM Agent</span></span>

<span data-ttu-id="fa277-132">Windows 용 hello Azure VM 에이전트 자동 업그레이드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-132">hello Azure VM Agent for Windows is automatically upgraded.</span></span> <span data-ttu-id="fa277-133">새 가상 컴퓨터에 배포 된 tooAzure로 hello 최신 VM 에이전트를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-133">As new virtual machines are deployed tooAzure, they receive hello latest VM agent.</span></span> <span data-ttu-id="fa277-134">사용자 지정 VM 이미지를 수동으로 업데이트 tooinclude hello 새 VM 에이전트가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa277-134">Custom VM images should be manually updated tooinclude hello new VM agent.</span></span>
