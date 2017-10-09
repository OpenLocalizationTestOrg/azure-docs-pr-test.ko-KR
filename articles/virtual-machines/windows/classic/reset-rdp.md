---
title: "암호 또는 Azure에서 Windows VM에서 원격 데스크톱 구성을 aaaReset hello | Microsoft Docs"
description: "Azure 포털 또는 Azure PowerShell 계정 암호 또는 Windows VM에서 원격 데스크톱 서비스 hello 클래식 배포 사용 하 여 모델을 사용 하 여 만든 tooreset hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 1721a91fc6c89b46df74e76dfcf918b1c4c77a4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-hello-classic-deployment-model"></a><span data-ttu-id="e3747-103">어떻게 tooreset hello 원격 데스크톱 서비스 또는 로그인 암호는 Windows VM에서 사용 하 여 만든 hello 클래식 배포 모델</span><span class="sxs-lookup"><span data-stu-id="e3747-103">How tooreset hello Remote Desktop service or its login password in a Windows VM created using hello Classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e3747-104">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../../../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e3747-105">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="e3747-106">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="e3747-107">수도 있습니다 [hello 리소스 관리자 배포 모델을 사용 하 여 만든 Vm에 대해 이러한 단계를 수행](../reset-rdp.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-107">You can also [perform these steps for VMs created with hello Resource Manager deployment model](../reset-rdp.md).</span></span>

<span data-ttu-id="e3747-108">Tooa Windows 가상 컴퓨터 (VM)를 연결할 수 없는 경우 hello 로컬 관리자 암호 재설정 또는 hello 원격 데스크톱 서비스 구성을 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-108">If you can't connect tooa Windows virtual machine (VM), you can reset hello local administrator password or reset hello Remote Desktop service configuration.</span></span> <span data-ttu-id="e3747-109">Azure PowerShell tooreset hello 암호에 hello Azure 포털 또는 hello VM 액세스 확장 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-109">You can use either hello Azure portal or hello VM Access extension in Azure PowerShell tooreset hello password.</span></span>

## <a name="ways-tooreset-configuration-or-credentials"></a><span data-ttu-id="e3747-110">같은 방법으로 tooreset 구성 또는 자격 증명</span><span class="sxs-lookup"><span data-stu-id="e3747-110">Ways tooreset configuration or credentials</span></span>
<span data-ttu-id="e3747-111">필요에 따라 몇 가지 방법으로 원격 데스크톱 서비스 및 자격 증명을 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-111">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="e3747-112">Hello Azure 포털을 사용 하 여 다시 설정</span><span class="sxs-lookup"><span data-stu-id="e3747-112">Reset using hello Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="e3747-113">Azure PowerShell을 사용하여 재설정</span><span class="sxs-lookup"><span data-stu-id="e3747-113">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="e3747-114">Azure portal</span><span class="sxs-lookup"><span data-stu-id="e3747-114">Azure portal</span></span>
<span data-ttu-id="e3747-115">Hello를 사용할 수 있습니다 [Azure 포털](https://portal.azure.com) tooreset hello 원격 데스크톱 서비스.</span><span class="sxs-lookup"><span data-stu-id="e3747-115">You can use hello [Azure portal](https://portal.azure.com) tooreset hello Remote Desktop service.</span></span> <span data-ttu-id="e3747-116">tooexpand hello 포털 메뉴 hello 왼쪽된 위 모서리에서 3 hello 막대를 클릭 한 다음 클릭 **가상 컴퓨터 (클래식)**:</span><span class="sxs-lookup"><span data-stu-id="e3747-116">tooexpand hello portal menu, click hello three bars in hello upper left corner and then click **Virtual machines (classic)**:</span></span>

![Azure VM 찾아보기](./media/reset-rdp/Portal-Select-Classic-VM.png)

<span data-ttu-id="e3747-118">Windows 가상 컴퓨터를 선택한 다음 클릭 **원격 다시 설정...** . hello 다음과 같은 대화 상자가 나타나면 tooreset hello 원격 데스크톱 구성:</span><span class="sxs-lookup"><span data-stu-id="e3747-118">Select your Windows virtual machine and then click **Reset Remote...**. hello following dialog appears tooreset hello Remote Desktop configuration:</span></span>

![RDP 구성 다시 설정 페이지](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

<span data-ttu-id="e3747-120">또한 hello 사용자 이름 및 hello 로컬 관리자 계정의 암호를 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-120">You can also reset hello username and password of hello local administrator account.</span></span> <span data-ttu-id="e3747-121">VM에서 **지원 + 문제 해결** > **암호 다시 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-121">From your VM, click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="e3747-122">hello 암호 재설정 블레이드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-122">hello password reset blade is displayed:</span></span>

![암호 다시 설정 페이지](./media/reset-rdp/Portal-PW-Reset-Windows.png)

<span data-ttu-id="e3747-124">Hello 새 사용자 이름 및 암호를 입력 한 후 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-124">After you enter hello new user name and password, click **Save**.</span></span>

## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="e3747-125">VMAccess 확장 및 PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3747-125">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="e3747-126">Hello 가상 컴퓨터에 VM 에이전트가 설치 되어 있는지 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-126">Make sure hello VM Agent is installed on hello virtual machine.</span></span> <span data-ttu-id="e3747-127">VMAccess 확장 hello toobe hello VM 에이전트는 사용 가능한 상태로 사용할 수 있습니다 설치 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-127">hello VMAccess extension doesn't need toobe installed before you can use it, as long as hello VM Agent is available.</span></span> <span data-ttu-id="e3747-128">다음 명령을 hello를 사용 하 여 VM 에이전트가 이미 설치 되어 해당 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-128">Verify that hello VM Agent is already installed by using hello following command.</span></span> <span data-ttu-id="e3747-129">("MyCloudService" 및 "myVM" 클라우드 서비스 및 VM을 hello 이름으로 각각 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-129">(Replace "myCloudService" and "myVM" by hello names of your cloud service and your VM, respectively.</span></span> <span data-ttu-id="e3747-130">매개 변수 없이 `Get-AzureVM` 을 실행하면 이러한 이름을 파악할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="e3747-130">You can learn these names by running `Get-AzureVM` without any parameters.)</span></span>

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="e3747-131">경우 hello **쓰기 호스트** 표시 명령 **True**, hello VM 에이전트가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-131">If hello **write-host** command displays **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="e3747-132">표시 하는 경우 **False**, hello 지침과 hello에 대 한 다운로드 링크 toohello 표시 [VM 에이전트 및 확장-2 부](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure 블로그 게시물입니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-132">If it displays **False**, see hello instructions and a link toohello download in hello [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure blog post.</span></span>

<span data-ttu-id="e3747-133">Hello 포털을 사용 하 여 hello 가상 컴퓨터를 만든 경우 확인 여부 `$vm.GetInstance().ProvisionGuestAgent` 반환 **True**합니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-133">If you created hello virtual machine by using hello portal, check whether `$vm.GetInstance().ProvisionGuestAgent` returns **True**.</span></span> <span data-ttu-id="e3747-134">그렇지 않은 경우 다음 명령을 사용하여 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-134">If not, you can set it by using this command:</span></span>

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

<span data-ttu-id="e3747-135">이 명령은 hello hello를 실행 하는 경우 다음 오류가 방지 **Set-azurevmextension** hello 다음 단계에서 명령을: "프로 비전 게스트 에이전트에서 설정 해야 hello VM 개체 IaaS VM 액세스 확장을 설정 하기 전에."</span><span class="sxs-lookup"><span data-stu-id="e3747-135">This command prevents hello following error when you're running hello **Set-AzureVMExtension** command in hello next steps: “Provision Guest Agent must be enabled on hello VM object before setting IaaS VM Access Extension.”</span></span>

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="e3747-136">**Hello 로컬 관리자 계정 암호를 다시 설정**</span><span class="sxs-lookup"><span data-stu-id="e3747-136">**Reset hello local administrator account password**</span></span>
<span data-ttu-id="e3747-137">Hello 현재 로컬 관리자 계정 이름 및 새 암호를 사용 하 여 로그인 자격 증명을 만들고 hello를 실행 한 다음 `Set-AzureVMAccessExtension` 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-137">Create a sign-in credential with hello current local administrator account name and a new password, and then run hello `Set-AzureVMAccessExtension` as follows.</span></span>

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

<span data-ttu-id="e3747-138">Hello 현재 계정이 아닌 다른 이름을 입력 하면 hello VMAccess 확장 hello 로컬 관리자 계정의 이름을 바꿉니다, 그리고 hello 암호 toothat 계정을 할당 및 로그 아웃 하는 원격 데스크톱을 발급 합니다. Hello 로컬 관리자 계정이 비활성화 된 경우 hello VMAccess 확장으로 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-138">If you type a different name than hello current account, hello VMAccess extension renames hello local administrator account, assigns hello password toothat account, and issues a Remote Desktop sign-out. If hello local administrator account is disabled, hello VMAccess extension enables it.</span></span>

<span data-ttu-id="e3747-139">이러한 명령에는 hello 원격 데스크톱 서비스 구성을 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-139">These commands also reset hello Remote Desktop service configuration.</span></span>

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="e3747-140">**Hello 원격 데스크톱 서비스 구성을 다시 설정**</span><span class="sxs-lookup"><span data-stu-id="e3747-140">**Reset hello Remote Desktop service configuration**</span></span>
<span data-ttu-id="e3747-141">tooreset hello 원격 데스크톱 서비스 구성, hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-141">tooreset hello Remote Desktop service configuration, run hello following command:</span></span>

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

<span data-ttu-id="e3747-142">hello VMAccess 확장 hello 가상 컴퓨터에서 두 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-142">hello VMAccess extension runs two commands on hello virtual machine:</span></span>

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

<span data-ttu-id="e3747-143">이 명령은 TCP 포트 3389를 사용 하 여 들어오는 원격 데스크톱 트래픽을 허용 하는 hello 기본 제공 하는 Windows 방화벽 그룹을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-143">This command enables hello built-in Windows Firewall group that allows incoming Remote Desktop traffic, which uses TCP port 3389.</span></span>

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

<span data-ttu-id="e3747-144">이 명령은 설정 hello fDenyTSConnections 레지스트리 값 too0, 원격 데스크톱 연결을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-144">This command sets hello fDenyTSConnections registry value too0, enabling Remote Desktop connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3747-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e3747-145">Next steps</span></span>
<span data-ttu-id="e3747-146">수 hello Azure VM 액세스 확장 응답 하지 않는 경우 없습니다 tooreset hello 암호 있는 [hello 로컬 Windows 암호를 재설정 오프 라인](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-146">If hello Azure VM access extension does not respond and you are unable tooreset hello password, you can [reset hello local Windows password offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="e3747-147">이 메서드는 더 많은 고급 프로세스 고 hello 문제가 있는 VM tooanother VM의 tooconnect hello 가상 하드 디스크를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-147">This method is a more advanced process and requires you tooconnect hello virtual hard disk of hello problematic VM tooanother VM.</span></span> <span data-ttu-id="e3747-148">먼저,이 문서에서 설명 하는 hello 단계를 수행 하 고만 최후의 수단으로 hello 오프 라인 암호 재설정 메서드를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3747-148">Follow hello steps documented in this article first, and only attempt hello offline password reset method as a last resort.</span></span>

[<span data-ttu-id="e3747-149">Azure VM 확장 및 기능</span><span class="sxs-lookup"><span data-stu-id="e3747-149">Azure VM extensions and features</span></span>](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="e3747-150">RDP 또는 SSH를 사용 하 여 tooan Azure 가상 컴퓨터 연결</span><span class="sxs-lookup"><span data-stu-id="e3747-150">Connect tooan Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="e3747-151">원격 데스크톱 연결 tooa Windows 기반 Azure 가상 컴퓨터 문제 해결</span><span class="sxs-lookup"><span data-stu-id="e3747-151">Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine</span></span>](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

