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
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-hello-classic-deployment-model"></a>어떻게 tooreset hello 원격 데스크톱 서비스 또는 로그인 암호는 Windows VM에서 사용 하 여 만든 hello 클래식 배포 모델
> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../../../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. 수도 있습니다 [hello 리소스 관리자 배포 모델을 사용 하 여 만든 Vm에 대해 이러한 단계를 수행](../reset-rdp.md)합니다.

Tooa Windows 가상 컴퓨터 (VM)를 연결할 수 없는 경우 hello 로컬 관리자 암호 재설정 또는 hello 원격 데스크톱 서비스 구성을 다시 설정할 수 있습니다. Azure PowerShell tooreset hello 암호에 hello Azure 포털 또는 hello VM 액세스 확장 중 하나를 사용할 수 있습니다.

## <a name="ways-tooreset-configuration-or-credentials"></a>같은 방법으로 tooreset 구성 또는 자격 증명
필요에 따라 몇 가지 방법으로 원격 데스크톱 서비스 및 자격 증명을 재설정할 수 있습니다.

- [Hello Azure 포털을 사용 하 여 다시 설정](#azure-portal)
- [Azure PowerShell을 사용하여 재설정](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a>Azure portal
Hello를 사용할 수 있습니다 [Azure 포털](https://portal.azure.com) tooreset hello 원격 데스크톱 서비스. tooexpand hello 포털 메뉴 hello 왼쪽된 위 모서리에서 3 hello 막대를 클릭 한 다음 클릭 **가상 컴퓨터 (클래식)**:

![Azure VM 찾아보기](./media/reset-rdp/Portal-Select-Classic-VM.png)

Windows 가상 컴퓨터를 선택한 다음 클릭 **원격 다시 설정...** . hello 다음과 같은 대화 상자가 나타나면 tooreset hello 원격 데스크톱 구성:

![RDP 구성 다시 설정 페이지](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

또한 hello 사용자 이름 및 hello 로컬 관리자 계정의 암호를 재설정할 수 있습니다. VM에서 **지원 + 문제 해결** > **암호 다시 설정**을 클릭합니다. hello 암호 재설정 블레이드가 표시 됩니다.

![암호 다시 설정 페이지](./media/reset-rdp/Portal-PW-Reset-Windows.png)

Hello 새 사용자 이름 및 암호를 입력 한 후 클릭 **저장**합니다.

## <a name="vmaccess-extension-and-powershell"></a>VMAccess 확장 및 PowerShell
Hello 가상 컴퓨터에 VM 에이전트가 설치 되어 있는지 hello를 확인 합니다. VMAccess 확장 hello toobe hello VM 에이전트는 사용 가능한 상태로 사용할 수 있습니다 설치 필요 하지 않습니다. 다음 명령을 hello를 사용 하 여 VM 에이전트가 이미 설치 되어 해당 hello를 확인 합니다. ("MyCloudService" 및 "myVM" 클라우드 서비스 및 VM을 hello 이름으로 각각 바꿉니다. 매개 변수 없이 `Get-AzureVM` 을 실행하면 이러한 이름을 파악할 수 있습니다.)

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

경우 hello **쓰기 호스트** 표시 명령 **True**, hello VM 에이전트가 설치 되어 있습니다. 표시 하는 경우 **False**, hello 지침과 hello에 대 한 다운로드 링크 toohello 표시 [VM 에이전트 및 확장-2 부](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure 블로그 게시물입니다.

Hello 포털을 사용 하 여 hello 가상 컴퓨터를 만든 경우 확인 여부 `$vm.GetInstance().ProvisionGuestAgent` 반환 **True**합니다. 그렇지 않은 경우 다음 명령을 사용하여 설정할 수 있습니다.

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

이 명령은 hello hello를 실행 하는 경우 다음 오류가 방지 **Set-azurevmextension** hello 다음 단계에서 명령을: "프로 비전 게스트 에이전트에서 설정 해야 hello VM 개체 IaaS VM 액세스 확장을 설정 하기 전에."

### <a name="reset-hello-local-administrator-account-password"></a>**Hello 로컬 관리자 계정 암호를 다시 설정**
Hello 현재 로컬 관리자 계정 이름 및 새 암호를 사용 하 여 로그인 자격 증명을 만들고 hello를 실행 한 다음 `Set-AzureVMAccessExtension` 다음과 같습니다.

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

Hello 현재 계정이 아닌 다른 이름을 입력 하면 hello VMAccess 확장 hello 로컬 관리자 계정의 이름을 바꿉니다, 그리고 hello 암호 toothat 계정을 할당 및 로그 아웃 하는 원격 데스크톱을 발급 합니다. Hello 로컬 관리자 계정이 비활성화 된 경우 hello VMAccess 확장으로 활성화 합니다.

이러한 명령에는 hello 원격 데스크톱 서비스 구성을 다시 설정 합니다.

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Hello 원격 데스크톱 서비스 구성을 다시 설정**
tooreset hello 원격 데스크톱 서비스 구성, hello 다음 명령을 실행 합니다.

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

hello VMAccess 확장 hello 가상 컴퓨터에서 두 명령을 실행합니다.

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

이 명령은 TCP 포트 3389를 사용 하 여 들어오는 원격 데스크톱 트래픽을 허용 하는 hello 기본 제공 하는 Windows 방화벽 그룹을 설정 합니다.

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

이 명령은 설정 hello fDenyTSConnections 레지스트리 값 too0, 원격 데스크톱 연결을 사용 합니다.

## <a name="next-steps"></a>다음 단계
수 hello Azure VM 액세스 확장 응답 하지 않는 경우 없습니다 tooreset hello 암호 있는 [hello 로컬 Windows 암호를 재설정 오프 라인](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 이 메서드는 더 많은 고급 프로세스 고 hello 문제가 있는 VM tooanother VM의 tooconnect hello 가상 하드 디스크를 필요 합니다. 먼저,이 문서에서 설명 하는 hello 단계를 수행 하 고만 최후의 수단으로 hello 오프 라인 암호 재설정 메서드를 시도 합니다.

[Azure VM 확장 및 기능](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[RDP 또는 SSH를 사용 하 여 tooan Azure 가상 컴퓨터 연결](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[원격 데스크톱 연결 tooa Windows 기반 Azure 가상 컴퓨터 문제 해결](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

