---
title: "Azure에서 Windows VM에서 Symantec Endpoint Protection aaaInstall | Microsoft Docs"
description: "자세한 내용은 방법 tooinstall에서 새로운 hello Symantec Endpoint Protection에 대 한 보안 확장 프로그램을 구성 하거나 기존 Azure VM hello 클래식 배포 모델을 사용 하 여 만든 합니다."
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
ms.openlocfilehash: cb6083366185c26c9f43ff94d835cd90725de5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a><span data-ttu-id="8ed0f-103">어떻게 tooinstall Windows VM에서 Symantec Endpoint Protection을 구성 하 고</span><span class="sxs-lookup"><span data-stu-id="8ed0f-103">How tooinstall and configure Symantec Endpoint Protection on a Windows VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="8ed0f-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8ed0f-105">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="8ed0f-106">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="8ed0f-107">이 문서에서는 어떻게 tooinstall 및 Windows Server를 실행 중인 기존 가상 컴퓨터 (VM)에 hello Symantec Endpoint Protection 클라이언트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-107">This article shows you how tooinstall and configure hello Symantec Endpoint Protection client on an existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="8ed0f-108">이 전체 클라이언트는 바이러스 및 스파이웨어 보호, 방화벽, 침입 방지와 같은 서비스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-108">This full client includes services such as virus and spyware protection, firewall, and intrusion prevention.</span></span> <span data-ttu-id="8ed0f-109">hello 클라이언트 hello VM 에이전트를 사용 하 여 보안 확장 프로그램으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-109">hello client is installed as a security extension by using hello VM Agent.</span></span>

<span data-ttu-id="8ed0f-110">Symantec에서 온-프레미스 솔루션에 대 한 기존 구독이 있는 경우 사용할 수 있습니다 tooprotect Azure 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-110">If you have an existing subscription from Symantec for an on-premises solution, you can use it tooprotect your Azure virtual machines.</span></span> <span data-ttu-id="8ed0f-111">아직 구독 고객이 아닌 경우에는 평가판 구독에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-111">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="8ed0f-112">이 솔루션에 대한 자세한 내용은 [Microsoft Azure 플랫폼의 Symantec Endpoint Protection][Symantec](영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-112">For more information about this solution, see [Symantec Endpoint Protection on Microsoft's Azure platform][Symantec].</span></span> <span data-ttu-id="8ed0f-113">이 페이지에는 역시 링크 toolicensing 정보 및 이미 Symantec 고객 인 경우 hello 클라이언트를 설치 하기 위한 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-113">This page also has links toolicensing information and instructions for installing hello client if you're already a Symantec customer.</span></span>

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a><span data-ttu-id="8ed0f-114">기존 VM에 Symantec Endpoint Protection 설치</span><span class="sxs-lookup"><span data-stu-id="8ed0f-114">Install Symantec Endpoint Protection on an existing VM</span></span>
<span data-ttu-id="8ed0f-115">시작 하기 전에 hello 다음을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-115">Before you begin, you need hello following:</span></span>

* <span data-ttu-id="8ed0f-116">hello Azure PowerShell 모듈, 0.8.2 버전 또는 이후 버전의 경우 회사의 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-116">hello Azure PowerShell module, version 0.8.2 or later, on your work computer.</span></span> <span data-ttu-id="8ed0f-117">Hello hello로 설치 된 Azure PowerShell 버전을 확인할 수 있습니다 **Get-module azure | format-table 버전** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-117">You can check hello version of Azure PowerShell that you have installed with hello **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="8ed0f-118">지침 및 링크 toohello 최신 버전에 대 한 참조 [어떻게 tooInstall 및 Azure PowerShell 구성][PS]합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-118">For instructions and a link toohello latest version, see [How tooInstall and Configure Azure PowerShell][PS].</span></span> <span data-ttu-id="8ed0f-119">사용 하 여 Azure 구독 tooyour `Add-AzureAccount`합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-119">Log in tooyour Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="8ed0f-120">hello에서 실행 중인 VM 에이전트가 hello Azure 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-120">hello VM Agent running on hello Azure Virtual Machine.</span></span>

<span data-ttu-id="8ed0f-121">첫째, hello 가상 컴퓨터에 VM 에이전트가 이미 설치 되어 해당 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-121">First, verify that hello VM Agent is already installed on hello virtual machine.</span></span> <span data-ttu-id="8ed0f-122">Hello 클라우드 서비스 이름 및 가상 컴퓨터 이름을 입력 한 후 hello 다음 관리자 권한 Azure PowerShell 명령 프롬프트에서 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-122">Fill in hello cloud service name and virtual machine name, and then run hello following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="8ed0f-123">Hello < 및 > 문자를 포함 하 여 hello 인용 부호 있는 모든 항목을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-123">Replace everything within hello quotes, including hello < and > characters.</span></span>

> [!TIP]
> <span data-ttu-id="8ed0f-124">Hello 클라우드 서비스 및 가상 컴퓨터 이름을 모르는 경우 실행 **Get-azurevm** 현재 구독에서 모든 가상 컴퓨터에 대 한 toolist hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-124">If you don't know hello cloud service and virtual machine names, run **Get-AzureVM** toolist hello names for all virtual machines in your current subscription.</span></span>

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="8ed0f-125">경우 hello **쓰기 호스트** 표시 명령 **True**, hello VM 에이전트가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-125">If hello **write-host** command displays **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="8ed0f-126">표시 하는 경우 **False**, hello 지침 및 다운로드 hello Azure 블로그 게시물에서에서 링크 toohello 참조 [VM 에이전트 및 확장-2 부][Agent]합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-126">If it displays **False**, see hello instructions and a link toohello download in hello Azure blog post [VM Agent and Extensions - Part 2][Agent].</span></span>

<span data-ttu-id="8ed0f-127">Hello VM 에이전트를 설치 하는 경우 이러한 명령을 tooinstall hello Symantec Endpoint Protection 에이전트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-127">If hello VM Agent is installed, run these commands tooinstall hello Symantec Endpoint Protection agent.</span></span>

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

<span data-ttu-id="8ed0f-128">보안 확장 프로그램 Symantec hello tooverify이 설치 되어 있고 최신 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-128">tooverify that hello Symantec security extension has been installed and is up-to-date:</span></span>

1. <span data-ttu-id="8ed0f-129">Toohello 가상 컴퓨터에 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-129">Log on toohello virtual machine.</span></span> <span data-ttu-id="8ed0f-130">자세한 내용은 [어떻게 tooLog tooa Windows Server를 실행 하는 가상 컴퓨터에][Logon]합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-130">For instructions, see [How tooLog on tooa Virtual Machine Running Windows Server][Logon].</span></span>
2. <span data-ttu-id="8ed0f-131">Windows Server 2008 R2의 경우, **시작 > Symantec Endpoint Protection**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-131">For Windows Server 2008 R2, click **Start > Symantec Endpoint Protection**.</span></span> <span data-ttu-id="8ed0f-132">Windows Server 2012 또는 hello 시작 화면에서 Windows Server 2012 r 2에 대 한 입력 **Symantec**, 클릭 하 고 **Symantec Endpoint Protection**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-132">For Windows Server 2012 or Windows Server 2012 R2, from hello start screen, type **Symantec**, and then click **Symantec Endpoint Protection**.</span></span>
3. <span data-ttu-id="8ed0f-133">Hello에서 **상태** hello 탭 **상태 Symantec Endpoint Protection** 창에서 업데이트를 적용 하거나 필요한 경우 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed0f-133">From hello **Status** tab of hello **Status-Symantec Endpoint Protection** window, apply updates or restart if needed.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8ed0f-134">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="8ed0f-134">Additional resources</span></span>
<span data-ttu-id="8ed0f-135">[어떻게 tooLog tooa Windows Server를 실행 하는 가상 컴퓨터에][Logon]</span><span class="sxs-lookup"><span data-stu-id="8ed0f-135">[How tooLog on tooa Virtual Machine Running Windows Server][Logon]</span></span>

<span data-ttu-id="8ed0f-136">[Azure VM 확장 및 기능][Ext]</span><span class="sxs-lookup"><span data-stu-id="8ed0f-136">[Azure VM Extensions and Features][Ext]</span></span>

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
