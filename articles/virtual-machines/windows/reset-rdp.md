---
title: "Windows VM에서 암호 또는 원격 데스크톱 구성 다시 설정 | Microsoft Docs"
description: "Azure 포털 또는 Azure PowerShell을 사용하여 Windows VM에서 계정 암호 또는 원격 데스크톱 서비스를 다시 설정하는 방법을 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 45c69812-d3e4-48de-a98d-39a0f5675777
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 2e002e3f336422b8fa1eceece889cd083e355a68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-the-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a><span data-ttu-id="398d0-103">Windows VM에서 원격 데스크톱 서비스 또는 해당 로그인 암호를 다시 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="398d0-103">How to reset the Remote Desktop service or its login password in a Windows VM</span></span>
<span data-ttu-id="398d0-104">Windows 가상 컴퓨터에 연결할 수 없는 경우 로컬 관리자 암호를 다시 설정할 수도 있고 원격 데스크톱 서비스 구성을 다시 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-104">If you can't connect to a Windows virtual machine (VM), you can reset the local administrator password or reset the Remote Desktop service configuration.</span></span> <span data-ttu-id="398d0-105">암호를 다시 설정하려면 Azure 포털이나 Azure PowerShell의 VM 액세스 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-105">You can use either the Azure portal or the VM Access extension in Azure PowerShell to reset the password.</span></span> <span data-ttu-id="398d0-106">PowerShell을 사용하는 경우 [최신 PowerShell 모듈을 설치 및 구성](/powershell/azure/overview)하고 Azure 구독에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-106">If you are using PowerShell, make sure that you have the [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in to your Azure subscription.</span></span> <span data-ttu-id="398d0-107">[클래식 배포 모델을 사용하여 만든 VM에 대해 이러한 단계를 수행](reset-rdp.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-107">You can also [perform these steps for VMs created with the Classic deployment model](reset-rdp.md).</span></span>

## <a name="ways-to-reset-configuration-or-credentials"></a><span data-ttu-id="398d0-108">구성 또는 자격 증명을 다시 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="398d0-108">Ways to reset configuration or credentials</span></span>
<span data-ttu-id="398d0-109">필요에 따라 몇 가지 방법으로 원격 데스크톱 서비스 및 자격 증명을 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-109">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="398d0-110">Azure 포털을 사용하여 재설정</span><span class="sxs-lookup"><span data-stu-id="398d0-110">Reset using the Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="398d0-111">Azure PowerShell을 사용하여 재설정</span><span class="sxs-lookup"><span data-stu-id="398d0-111">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="398d0-112">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="398d0-112">Azure portal</span></span>
<span data-ttu-id="398d0-113">포털 메뉴를 확장하려면 왼쪽 위 구석에 있는 세 개의 막대를 클릭한 다음 **가상 컴퓨터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-113">To expand the portal menu, click the three bars in the upper left corner and then click **Virtual machines**:</span></span>

![Azure VM 찾아보기](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-the-local-administrator-account-password"></a><span data-ttu-id="398d0-115">**로컬 관리자 계정 암호를 다시 설정**</span><span class="sxs-lookup"><span data-stu-id="398d0-115">**Reset the local administrator account password**</span></span>

<span data-ttu-id="398d0-116">Windows 가상 컴퓨터를 선택한 다음 **지원 + 문제 해결** > **암호 재설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-116">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="398d0-117">암호 다시 설정 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-117">The password reset blade is displayed:</span></span>

![암호 다시 설정 페이지](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

<span data-ttu-id="398d0-119">사용자 이름 및 새 암호를 입력한 후 **업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-119">Enter the username and a new password, then click **Update**.</span></span> <span data-ttu-id="398d0-120">VM에 연결을 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="398d0-120">Try connecting to your VM again.</span></span>

### <a name="reset-the-remote-desktop-service-configuration"></a><span data-ttu-id="398d0-121">**원격 데스크톱 서비스 구성을 다시 설정**</span><span class="sxs-lookup"><span data-stu-id="398d0-121">**Reset the Remote Desktop service configuration**</span></span>

<span data-ttu-id="398d0-122">Windows 가상 컴퓨터를 선택한 다음 **지원 + 문제 해결** > **암호 재설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-122">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="398d0-123">암호 다시 설정 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-123">The password reset blade is displayed.</span></span> 

![RDP 구성 다시 설정](./media/reset-rdp/Portal-RM-RDP-Reset.png)

<span data-ttu-id="398d0-125">드롭다운 메뉴에서 **구성만 재설정**을 선택하고 **업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-125">Select **Reset configuration only** from the drop-down menu, then click **Update**.</span></span> <span data-ttu-id="398d0-126">VM에 연결을 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="398d0-126">Try connecting to your VM again.</span></span>


## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="398d0-127">VMAccess 확장 및 PowerShell</span><span class="sxs-lookup"><span data-stu-id="398d0-127">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="398d0-128">[최신 PowerShell 모듈을 설치 및 구성](/powershell/azure/overview)하고 `Login-AzureRmAccount` cmdlet을 사용하여 Azure 구독에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-128">Make sure that you have the [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in to your Azure subscription with the `Login-AzureRmAccount` cmdlet.</span></span>

### <a name="reset-the-local-administrator-account-password"></a><span data-ttu-id="398d0-129">**로컬 관리자 계정 암호를 다시 설정**</span><span class="sxs-lookup"><span data-stu-id="398d0-129">**Reset the local administrator account password**</span></span>
<span data-ttu-id="398d0-130">[Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet을 사용하여 관리자 암호 또는 사용자 이름을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-130">Reset the administrator password or user name with the [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="398d0-131">계정 자격 증명을 다음과 같이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-131">Create your account credentials as follows:</span></span>

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> <span data-ttu-id="398d0-132">VM에서 현재 로컬 관리자 계정이 아닌 다른 이름을 입력한 경우 VMAccess 확장은 로컬 관리자 계정의 이름을 바꾸고, 해당 계정에 지정된 암호를 할당하며, 원격 데스크톱 로그오프 이벤트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-132">If you type a different name than the current local administrator account on your VM, the VMAccess extension renames the local administrator account, assigns your specified password to that account, and issues a Remote Desktop logoff event.</span></span> <span data-ttu-id="398d0-133">VM에서 로컬 관리자 계정이 사용되지 않도록 설정된 경우 VMAccess 확장은 이를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-133">If the local administrator account on your VM is disabled, the VMAccess extension enables it.</span></span>

<span data-ttu-id="398d0-134">다음 예제에서는 리소스 그룹 `myResourceGroup`의 VM `myVM`을 지정된 자격 증명으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-134">The following example updates the VM named `myVM` in the resource group named `myResourceGroup` to the credentials specified.</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-the-remote-desktop-service-configuration"></a><span data-ttu-id="398d0-135">**원격 데스크톱 서비스 구성을 다시 설정**</span><span class="sxs-lookup"><span data-stu-id="398d0-135">**Reset the Remote Desktop service configuration**</span></span>
<span data-ttu-id="398d0-136">[Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet을 사용하여 VM에 대한 원격 액세스를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-136">Reset remote access to your VM with the [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="398d0-137">다음 예제에서는 리소스 그룹 `myVMAccess`의 VM `myVM`에서 `myResourceGroup` 진단 확장을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-137">The following example resets the access extension named `myVMAccess` on the VM named `myVM` in the `myResourceGroup` resource group:</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> <span data-ttu-id="398d0-138">언제든지 VM은 단일 VM 액세스 에이전트를 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-138">At any point, a VM can have only a single VM access agent.</span></span> <span data-ttu-id="398d0-139">VM 액세스 에이전트 속성을 성공적으로 설정하려면 `-ForceRerun` 옵션을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-139">To set the VM access agent properties successfully, the `-ForceRerun` option can be used.</span></span> <span data-ttu-id="398d0-140">`-ForceRerun`을 사용하는 경우 VM 액세스 에이전트에 이전 명령에서 사용한 것과 동일한 이름을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-140">When using `-ForceRerun`, make sure to use the same name for the VM access agent as used in any previous commands.</span></span>

<span data-ttu-id="398d0-141">가상 컴퓨터에 원격으로 연결할 수 없으면 시도에 더 많은 단계를 [Windows 기반 Azure 가상 컴퓨터에 대한 원격 데스크톱 연결 문제 해결](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="398d0-141">If you still can't connect remotely to your virtual machine, see more steps to try at [Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="next-steps"></a><span data-ttu-id="398d0-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="398d0-142">Next steps</span></span>
<span data-ttu-id="398d0-143">Azure VM 액세스 확장이 응답하지 않고 암호를 다시 설정할 수 없는 경우 [오프라인으로 로컬 Windows 암호를 다시 설정](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-143">If the Azure VM access extension does not respond and you are unable to reset the password, you can [reset the local Windows password offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="398d0-144">이 방법은 좀 더 고급 프로세스로, 문제가 있는 VM의 가상 하드 디스크를 다른 VM에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-144">This method is a more advanced process and requires you to connect the virtual hard disk of the problematic VM to another VM.</span></span> <span data-ttu-id="398d0-145">먼저 이 문서에 설명된 단계를 수행하고, 오프라인 암호 다시 설정 방법은 최후의 수단으로만 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="398d0-145">Follow the steps documented in this article first, and only attempt the offline password reset method as a last resort.</span></span>

[<span data-ttu-id="398d0-146">Azure VM 확장 및 기능</span><span class="sxs-lookup"><span data-stu-id="398d0-146">Azure VM extensions and features</span></span>](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="398d0-147">RDP 또는 SSH를 사용하여 Azure 가상 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="398d0-147">Connect to an Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="398d0-148">Windows 기반 Azure 가상 컴퓨터에 대한 원격 데스크톱 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="398d0-148">Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine</span></span>](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

