---
title: "암호 또는 Windows VM에서 원격 데스크톱 구성을 aaaReset hello | Microsoft Docs"
description: "Tooreset 계정 암호 또는 원격 데스크톱 서비스를 사용 하 여 Windows VM을 Azure 포털 또는 Azure PowerShell hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 5258df7196621f0adb50debd08dd248922a966de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a>원격 데스크톱 서비스 또는 Windows VM의 로그인 암호 tooreset hello 하는 방법
Tooa Windows 가상 컴퓨터 (VM)를 연결할 수 없는 경우 hello 로컬 관리자 암호 재설정 또는 hello 원격 데스크톱 서비스 구성을 다시 설정할 수 있습니다. Azure PowerShell tooreset hello 암호에 hello Azure 포털 또는 hello VM 액세스 확장 중 하나를 사용할 수 있습니다. PowerShell을 사용 하는 경우 확인 hello 하십시오 [최신 PowerShell 모듈 설치 및 구성](/powershell/azure/overview) tooyour Azure 구독에에서 로그인 하 고 있습니다. 수도 있습니다 [hello 클래식 배포 모델을 사용 하 여 만든 Vm에 대해 이러한 단계를 수행](reset-rdp.md)합니다.

## <a name="ways-tooreset-configuration-or-credentials"></a>같은 방법으로 tooreset 구성 또는 자격 증명
필요에 따라 몇 가지 방법으로 원격 데스크톱 서비스 및 자격 증명을 재설정할 수 있습니다.

- [Hello Azure 포털을 사용 하 여 다시 설정](#azure-portal)
- [Azure PowerShell을 사용하여 재설정](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a>Azure portal
tooexpand hello 포털 메뉴 hello 왼쪽된 위 모서리에서 3 hello 막대를 클릭 한 다음 클릭 **가상 컴퓨터**:

![Azure VM 찾아보기](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-hello-local-administrator-account-password"></a>**Hello 로컬 관리자 계정 암호를 다시 설정**

Windows 가상 컴퓨터를 선택한 다음 **지원 + 문제 해결** > **암호 재설정**을 클릭합니다. hello 암호 재설정 블레이드가 표시 됩니다.

![암호 다시 설정 페이지](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

Hello 사용자 이름 및 새 암호를 입력 한 다음 클릭 **업데이트**합니다. Tooyour VM을 다시 연결 하십시오.

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Hello 원격 데스크톱 서비스 구성을 다시 설정**

Windows 가상 컴퓨터를 선택한 다음 **지원 + 문제 해결** > **암호 재설정**을 클릭합니다. hello 암호 재설정 블레이드가 표시 됩니다. 

![RDP 구성 다시 설정](./media/reset-rdp/Portal-RM-RDP-Reset.png)

선택 **구성만 재설정** hello 드롭 다운 메뉴에서 클릭 **업데이트**합니다. Tooyour VM을 다시 연결 하십시오.


## <a name="vmaccess-extension-and-powershell"></a>VMAccess 확장 및 PowerShell
Hello 갖도록 [최신 PowerShell 모듈 설치 및 구성](/powershell/azure/overview) tooyour hello로 Azure 구독에에서 로그인 하 고 `Login-AzureRmAccount` cmdlet.

### <a name="reset-hello-local-administrator-account-password"></a>**Hello 로컬 관리자 계정 암호를 다시 설정**
재설정 hello 관리자 암호 또는 사용자 이름과 hello로 [집합 AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet. 계정 자격 증명을 다음과 같이 만듭니다.

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> Hello 현재 로컬 관리자 계정 이름이 다른 VM에를 입력 하면 hello VMAccess 확장 hello 로컬 관리자 계정의 이름을 바꿉니다, 그리고 지정 된 암호가 toothat 계정에 할당 및 원격 데스크톱 오프 한 후 이벤트를 발급 합니다. VM에 hello 로컬 관리자 계정이 비활성화 된 활성화 hello VMAccess 확장 합니다.

다음 예에서는 업데이트 hello hello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup` toohello 자격 증명을 지정 합니다.

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Hello 원격 데스크톱 서비스 구성을 다시 설정**
원격 액세스 tooyour VM hello로 재설정 [집합 AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet. hello 다음 예제에서는 재설정 라는 hello 액세스 확장 `myVMAccess` hello 라는 VM에서 `myVM` hello에 `myResourceGroup` 리소스 그룹:

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> 언제든지 VM은 단일 VM 액세스 에이전트를 하나만 사용할 수 있습니다. tooset hello VM 액세스 에이전트 속성 성공적으로 hello `-ForceRerun` 옵션을 사용할 수 있습니다. 사용 하는 경우 `-ForceRerun`, toouse hello hello VM 에이전트용 액세스 이전의 모든 명령을 사용한 것과 동일한 이름 있는지 확인 합니다.

계속 연결할 수 없으면 원격으로 tooyour 가상 컴퓨터, 참조에 더 많은 단계 tootry [문제를 해결 하는 원격 데스크톱 연결 tooa Windows 기반 Azure 가상 컴퓨터](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.


## <a name="next-steps"></a>다음 단계
수 hello Azure VM 액세스 확장 응답 하지 않는 경우 없습니다 tooreset hello 암호 있는 [hello 로컬 Windows 암호를 재설정 오프 라인](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 이 메서드는 더 많은 고급 프로세스 고 hello 문제가 있는 VM tooanother VM의 tooconnect hello 가상 하드 디스크를 필요 합니다. 먼저,이 문서에서 설명 하는 hello 단계를 수행 하 고만 최후의 수단으로 hello 오프 라인 암호 재설정 메서드를 시도 합니다.

[Azure VM 확장 및 기능](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[RDP 또는 SSH를 사용 하 여 tooan Azure 가상 컴퓨터 연결](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[원격 데스크톱 연결 tooa Windows 기반 Azure 가상 컴퓨터 문제 해결](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

