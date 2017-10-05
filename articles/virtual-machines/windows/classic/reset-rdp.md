---
title: "Azure에서 Windows VM의 암호 또는 원격 데스크톱 구성 다시 설정 | Microsoft Docs"
description: "Azure Portal 또는 Azure PowerShell을 통해 클래식 배포 모델을 사용하여 만든 Windows VM에서 계정 암호 또는 원격 데스크톱 서비스를 다시 설정하는 방법을 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 43e5cf1ab3bc3121d7e3915ea0785998e0ee2fc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-the-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-the-classic-deployment-model"></a><span data-ttu-id="07d9c-103">클래식 배포 모델을 사용하여 만든 Windows VM에서 원격 데스크톱 서비스 또는 해당 로그인 암호를 다시 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="07d9c-103">How to reset the Remote Desktop service or its login password in a Windows VM created using the Classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="07d9c-104">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../../../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="07d9c-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="07d9c-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="07d9c-107">[Resource Manager 배포 모델을 사용하여 만든 VM에 대해서도 이러한 단계를 수행](../reset-rdp.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-107">You can also [perform these steps for VMs created with the Resource Manager deployment model](../reset-rdp.md).</span></span>

<span data-ttu-id="07d9c-108">Windows 가상 컴퓨터에 연결할 수 없는 경우 로컬 관리자 암호를 다시 설정할 수도 있고 원격 데스크톱 서비스 구성을 다시 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-108">If you can't connect to a Windows virtual machine (VM), you can reset the local administrator password or reset the Remote Desktop service configuration.</span></span> <span data-ttu-id="07d9c-109">암호를 다시 설정하려면 Azure 포털이나 Azure PowerShell의 VM 액세스 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-109">You can use either the Azure portal or the VM Access extension in Azure PowerShell to reset the password.</span></span>

## <a name="ways-to-reset-configuration-or-credentials"></a><span data-ttu-id="07d9c-110">구성 또는 자격 증명을 다시 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="07d9c-110">Ways to reset configuration or credentials</span></span>
<span data-ttu-id="07d9c-111">필요에 따라 몇 가지 방법으로 원격 데스크톱 서비스 및 자격 증명을 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-111">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="07d9c-112">Azure 포털을 사용하여 재설정</span><span class="sxs-lookup"><span data-stu-id="07d9c-112">Reset using the Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="07d9c-113">Azure PowerShell을 사용하여 재설정</span><span class="sxs-lookup"><span data-stu-id="07d9c-113">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="07d9c-114">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="07d9c-114">Azure portal</span></span>
<span data-ttu-id="07d9c-115">[Azure Portal](https://portal.azure.com)을 사용하여 원격 데스크톱 서비스를 초기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-115">You can use the [Azure portal](https://portal.azure.com) to reset the Remote Desktop service.</span></span> <span data-ttu-id="07d9c-116">포털 메뉴를 확장하려면 왼쪽 위 구석에 있는 세 개의 막대를 클릭한 다음 **가상 컴퓨터(클래식)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-116">To expand the portal menu, click the three bars in the upper left corner and then click **Virtual machines (classic)**:</span></span>

![Azure VM 찾아보기](./media/reset-rdp/Portal-Select-Classic-VM.png)

<span data-ttu-id="07d9c-118">Windows 가상 컴퓨터를 선택하고 **원격으로 다시 설정...**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-118">Select your Windows virtual machine and then click **Reset Remote...**.</span></span> <span data-ttu-id="07d9c-119">원격 데스크톱 구성을 재설정하도록 다음 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-119">The following dialog appears to reset the Remote Desktop configuration:</span></span>

![RDP 구성 다시 설정 페이지](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

<span data-ttu-id="07d9c-121">로컬 관리자 계정의 이름 및 암호를 다시 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-121">You can also reset the username and password of the local administrator account.</span></span> <span data-ttu-id="07d9c-122">VM에서 **지원 + 문제 해결** > **암호 다시 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-122">From your VM, click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="07d9c-123">암호 다시 설정 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-123">The password reset blade is displayed:</span></span>

![암호 다시 설정 페이지](./media/reset-rdp/Portal-PW-Reset-Windows.png)

<span data-ttu-id="07d9c-125">새 사용자 이름 및 암호를 입력한 후 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-125">After you enter the new user name and password, click **Save**.</span></span>

## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="07d9c-126">VMAccess 확장 및 PowerShell</span><span class="sxs-lookup"><span data-stu-id="07d9c-126">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="07d9c-127">VM 에이전트가 가상 컴퓨터에 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-127">Make sure the VM Agent is installed on the virtual machine.</span></span> <span data-ttu-id="07d9c-128">VM 에이전트를 사용할 수 있는 한 VMAccess 확장은 설치하지 않아도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-128">The VMAccess extension doesn't need to be installed before you can use it, as long as the VM Agent is available.</span></span> <span data-ttu-id="07d9c-129">다음 명령을 사용하여 VM 에이전트가 이미 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-129">Verify that the VM Agent is already installed by using the following command.</span></span> <span data-ttu-id="07d9c-130">"myCloudService" 및 "myVM"을 각각 클라우드 서비스 및 VM의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-130">(Replace "myCloudService" and "myVM" by the names of your cloud service and your VM, respectively.</span></span> <span data-ttu-id="07d9c-131">매개 변수 없이 `Get-AzureVM` 을 실행하면 이러한 이름을 파악할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="07d9c-131">You can learn these names by running `Get-AzureVM` without any parameters.)</span></span>

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="07d9c-132">**write-host** 명령에서 **True**가 표시되면 VM 에이전트가 설치되어 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-132">If the **write-host** command displays **True**, the VM Agent is installed.</span></span> <span data-ttu-id="07d9c-133">**False**가 표시되면 [VM 에이전트 및 확장 - 2부](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure 블로그 게시물에서 지침 및 다운로드 링크를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-133">If it displays **False**, see the instructions and a link to the download in the [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure blog post.</span></span>

<span data-ttu-id="07d9c-134">포털에서 가상 컴퓨터를 만든 경우 `$vm.GetInstance().ProvisionGuestAgent` 이 **True**를 반환하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-134">If you created the virtual machine by using the portal, check whether `$vm.GetInstance().ProvisionGuestAgent` returns **True**.</span></span> <span data-ttu-id="07d9c-135">그렇지 않은 경우 다음 명령을 사용하여 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-135">If not, you can set it by using this command:</span></span>

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

<span data-ttu-id="07d9c-136">이 명령은 다음 단계인 “IaaS VM 액세스 확장을 설정하기 전에 VM 개체에서 게스트 에이전트 프로비전을 사용하도록 설정”에서 **Set-AzureVMExtension** 명령을 실행할 때 다음과 같은 오류를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-136">This command prevents the following error when you're running the **Set-AzureVMExtension** command in the next steps: “Provision Guest Agent must be enabled on the VM object before setting IaaS VM Access Extension.”</span></span>

### <a name="reset-the-local-administrator-account-password"></a><span data-ttu-id="07d9c-137">**로컬 관리자 계정 암호를 다시 설정**</span><span class="sxs-lookup"><span data-stu-id="07d9c-137">**Reset the local administrator account password**</span></span>
<span data-ttu-id="07d9c-138">현재 로컬 관리자 계정 이름 및 새 암호로 로그인 자격 증명을 만들고 다음과 같이 `Set-AzureVMAccessExtension` 을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-138">Create a sign-in credential with the current local administrator account name and a new password, and then run the `Set-AzureVMAccessExtension` as follows.</span></span>

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

<span data-ttu-id="07d9c-139">현재 계정이 아닌 다른 이름을 입력하는 경우 VMAccess 확장은 로컬 관리자 계정의 이름을 바꾸며, 해당 계정에 암호를 할당하고 원격 데스크톱 로그아웃을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-139">If you type a different name than the current account, the VMAccess extension renames the local administrator account, assigns the password to that account, and issues a Remote Desktop sign-out.</span></span> <span data-ttu-id="07d9c-140">로컬 관리자 계정이 비활성화 된 경우 VMAccess 확장으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-140">If the local administrator account is disabled, the VMAccess extension enables it.</span></span>

<span data-ttu-id="07d9c-141">이 명령은 원격 데스크톱 서비스 구성을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-141">These commands also reset the Remote Desktop service configuration.</span></span>

### <a name="reset-the-remote-desktop-service-configuration"></a><span data-ttu-id="07d9c-142">**원격 데스크톱 서비스 구성을 다시 설정**</span><span class="sxs-lookup"><span data-stu-id="07d9c-142">**Reset the Remote Desktop service configuration**</span></span>
<span data-ttu-id="07d9c-143">원격 데스크톱 서비스 구성을 재설정하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-143">To reset the Remote Desktop service configuration, run the following command:</span></span>

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

<span data-ttu-id="07d9c-144">VMAccess 확장은 가상 컴퓨터에서 다음 두 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-144">The VMAccess extension runs two commands on the virtual machine:</span></span>

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

<span data-ttu-id="07d9c-145">이 명령은 들어오는 원격 데스크톱 트래픽을 허용하는 기본 제공 Windows 방화벽 그룹을 활성화하며 TCP 포트 3389를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-145">This command enables the built-in Windows Firewall group that allows incoming Remote Desktop traffic, which uses TCP port 3389.</span></span>

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

<span data-ttu-id="07d9c-146">이 명령은 원격 데스크톱 연결을 사용하도록 설정하는 fDenyTSConnections 레지스트리 값을 0으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-146">This command sets the fDenyTSConnections registry value to 0, enabling Remote Desktop connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07d9c-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="07d9c-147">Next steps</span></span>
<span data-ttu-id="07d9c-148">Azure VM 액세스 확장이 응답하지 않고 암호를 다시 설정할 수 없는 경우 [오프라인으로 로컬 Windows 암호를 다시 설정](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-148">If the Azure VM access extension does not respond and you are unable to reset the password, you can [reset the local Windows password offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="07d9c-149">이 방법은 좀 더 고급 프로세스로, 문제가 있는 VM의 가상 하드 디스크를 다른 VM에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-149">This method is a more advanced process and requires you to connect the virtual hard disk of the problematic VM to another VM.</span></span> <span data-ttu-id="07d9c-150">먼저 이 문서에 설명된 단계를 수행하고, 오프라인 암호 다시 설정 방법은 최후의 수단으로만 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="07d9c-150">Follow the steps documented in this article first, and only attempt the offline password reset method as a last resort.</span></span>

[<span data-ttu-id="07d9c-151">Azure VM 확장 및 기능</span><span class="sxs-lookup"><span data-stu-id="07d9c-151">Azure VM extensions and features</span></span>](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="07d9c-152">RDP 또는 SSH를 사용하여 Azure 가상 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="07d9c-152">Connect to an Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="07d9c-153">Windows 기반 Azure 가상 컴퓨터에 대한 원격 데스크톱 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="07d9c-153">Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine</span></span>](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

