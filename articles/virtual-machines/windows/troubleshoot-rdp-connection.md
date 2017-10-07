---
title: "aaaCannot RDP tooa Azure에서 Windows VM에 연결 | Microsoft Docs"
description: "원격 데스크톱을 사용 하 여 Azure에서 tooyour Windows 가상 컴퓨터를 연결할 수 없을 때 문제를 해결 합니다."
keywords: "원격 데스크톱 오류, 원격 데스크톱 연결 오류 tooVM, 연결할 수 없습니다. 원격 데스크톱 문제 해결"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 0d740f8e-98b8-4e55-bb02-520f604f5b18
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: bbb36136e7a4b187fe8deea621d2b8d46d8aa102
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-remote-desktop-connections-tooan-azure-virtual-machine"></a>원격 데스크톱 연결 tooan Azure 가상 컴퓨터 문제 해결
hello 프로토콜 RDP (원격 데스크톱) 연결 tooyour Windows 기반 Azure 가상 컴퓨터 (VM)는 VM 수 없습니다 tooaccess 남게 다양 한 이유로 실패할 수 있습니다. hello VM, hello 네트워크 연결 또는 호스트 컴퓨터에서 원격 데스크톱 클라이언트 hello에 대 한 원격 데스크톱 서비스를 hello로 hello 문제가 될 수 있습니다. 이 문서는 hello 가장 일반적인 메서드 tooresolve RDP 연결 문제 중 일부를 안내합니다. 

이 문서에서 언제 든 지 자세한 도움말을 보려는 경우 문의할 수 있습니다에 Azure 전문가 hello [MSDN Azure 및 스택 오버플로 포럼 hello](https://azure.microsoft.com/support/forums/)합니다. 또는 Azure 기술 지원 인시던트를 제출할 수 있습니다. Toohello 이동 [Azure 지원 사이트](https://azure.microsoft.com/support/options/) 선택 **Get Support**합니다.

<a id="quickfixrdp"></a>

## <a name="quick-troubleshooting-steps"></a>빠른 문제 해결 단계
각 문제 해결 단계를 수행한 후 toohello VM 다시 연결을 시도 합니다.

1. 원격 데스크톱 구성을 다시 설정합니다.
2. 네트워크 보안 그룹 규칙/Cloud Services 끝점을 확인합니다.
3. VM 콘솔 로그를 검토합니다.
4. Hello VM에 대 한 NIC hello를 다시 설정 합니다.
5. Hello VM 리소스 상태를 확인 합니다.
6. VM 암호를 다시 설정합니다.
7. VM이 다시 시작됩니다.
8. VM을 다시 배포 합니다.

자세한 단계와 설명이 필요한 경우 계속 읽어보세요. [자세한 RDP 문제 해결 시나리오](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 설명한 대로 라우터 및 방화벽과 같은 로컬 네트워크 장비가 아웃바운드 TCP 포트 3389를 차단하지 않는지 확인합니다.

> [!TIP]
> 경우 hello **연결** VM hello 포털에서 동시에 회색를 통해 연결 된 tooAzure 됩니다에 대 한 단추는 [Express 경로](../../expressroute/expressroute-introduction.md) 또는 [사이트 간 VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) 해야 연결을 toocreate 및 하기 전에 VM 공용 IP 주소 할당 RDP를 사용할 수 있습니다. 자세한 내용은 [Azure의 공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)에서 확인할 수 있습니다.


## <a name="ways-tootroubleshoot-rdp-issues"></a>같은 방법으로 tootroubleshoot RDP 문제
다음과 같이 hello 메서드를 다음 중 하나를 사용 하 여 hello 리소스 관리자 배포 모델을 사용 하 여 만든 Vm 해결할 수 있습니다.

* [Azure 포털](#using-the-azure-portal) -tooquickly 해야 할 경우 좋은 hello RDP 구성 이나 사용자 자격 증명 다시 설정 하 고 설치 된 Azure 도구를 hello 하지 않습니다.
* [Azure PowerShell](#using-azure-powershell) -익숙한 PowerShell 프롬프트를 신속 하 게 재설정 hello RDP 구성 또는 사용자 자격 증명 hello Azure PowerShell cmdlet을 사용 하는 경우.

Hello를 사용 하 여 만든 Vm 문제를 해결 하는 단계를 찾을 수도 있습니다 [클래식 배포 모델](#troubleshoot-vms-created-using-the-classic-deployment-model)합니다.

<a id="fix-common-remote-desktop-errors"></a>

## <a name="troubleshoot-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 문제 해결
각 문제 해결 단계 후 tooyour VM을 다시 연결 하십시오. 여전히 연결할 수 없는 경우 hello 다음 단계를 시도 합니다.

1. **RDP 연결 다시 설정**. 이 문제 해결 단계에 원격 연결을 사용할 수 없습니다. 또는 예를 들어 Windows 방화벽 규칙 RDP를 차단 하는 경우 hello RDP 구성을 다시 설정 합니다.
   
    Hello Azure 포털에서에서 VM을 선택 합니다. Hello 설정 창 toohello 아래로 스크롤하여 **지원 + 문제 해결** hello 목록의 아래쪽 근처 섹션. Hello 클릭 **암호 재설정** 단추입니다. 집합 hello **모드** 너무**구성만 재설정** hello를 클릭 한 다음 **업데이트** 단추:
   
    ![Hello Azure 포털에서에서 hello RDP 구성을 다시 설정](./media/troubleshoot-rdp-connection/reset-rdp.png)
2. **네트워크 보안 그룹 규칙 확인**. 사용 하 여 [IP 흐름 확인](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) tooconfirm 네트워크 보안 그룹의 규칙은 가상 컴퓨터에서 트래픽을 tooor를 차단 하는 경우. 또한 tooensure 인바운드 "허용" NSG 규칙 규칙 존재 및 RDP 포트 (기본값 3389)에 대 한 우선 순위를 가지도록 효과적인 보안 그룹을 검토할 수 있습니다. 자세한 내용은 참조 [효과적인 보안 규칙을 사용 하 여 tootroubleshoot VM 트래픽 흐름](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow)합니다.

3. **VM 부트 진단 검토**. 이 문제 해결 단계는 hello VM 문제를 보고 하는 경우 hello VM 콘솔 로그 toodetermine를 검토 합니다. 모든 VM에서 부팅 진단이 지원되는 것은 아니므로 이 문제 해결 단계는 선택 사항입니다.
   
    특정 문제 해결 단계 hello이이 문서에서는 다루지 않지만 하지만 RDP 연결에 영향을 주지는 광범위 한 문제를 나타낼 수 있습니다. Hello 콘솔 로그 및 VM 스크린샷을 검토에 대 한 자세한 내용은 참조 하십시오. [Vm에 대 한 부트 진단](boot-diagnostics.md)합니다.

4. **Hello VM에 대 한 재설정 hello NIC**합니다. 자세한 내용은 참조 [어떻게 tooreset Azure Windows VM에 대 한 NIC](reset-network-interface.md)합니다.
5. **Hello VM 리소스 상태 확인**합니다. 이 문제 해결 단계는 연결 toohello VM에 영향을 줄 수 있는 Azure 플랫폼 hello로 알려진된 문제가 없는지 확인 합니다.
   
    Hello Azure 포털에서에서 VM을 선택 합니다. Hello 설정 창 toohello 아래로 스크롤하여 **지원 + 문제 해결** hello 목록의 아래쪽 근처 섹션. Hello 클릭 **리소스 상태** 단추입니다. 정상 VM은 **사용 가능**으로 보고합니다.
   
    ![Hello Azure 포털에서에서 VM 리소스 상태를 확인 합니다.](./media/troubleshoot-rdp-connection/check-resource-health.png)
6. **사용자 자격 증명 다시 설정**. 이 문제 해결 단계 확실 하지 않거나 hello 자격 증명을 잊은 경우 hello 로컬 관리자 계정의 암호를 다시 설정 합니다.
   
    Hello Azure 포털에서에서 VM을 선택 합니다. Hello 설정 창 toohello 아래로 스크롤하여 **지원 + 문제 해결** hello 목록의 아래쪽 근처 섹션. Hello 클릭 **암호 재설정** 단추입니다. 있는지 hello 확인 **모드** 너무 설정**암호 재설정** 사용자 이름 및 새 암호를 입력 합니다. 마지막으로 hello 클릭 **업데이트** 단추:
   
    ![Hello Azure 포털에서에서 hello 사용자 자격 증명 다시 설정](./media/troubleshoot-rdp-connection/reset-password.png)
7. **VM 다시 시작**. 이 문제 해결 단계는 근본적인 문제를 해결할 수 hello VM 자체는 것입니다.
   
    Hello Azure 포털에서에서 VM을 선택 하 고 hello 클릭 **개요** 탭 합니다. Hello 클릭 **다시 시작** 단추:
   
    ![Hello Azure 포털에서에서 VM hello를 다시 시작](./media/troubleshoot-rdp-connection/restart-vm.png)
8. **VM 다시 배포**. 이 문제 해결 단계 VM tooanother 호스트 Azure toocorrect 내 모든 기본 플랫폼 또는 네트워킹 문제를 다시 배포합니다.
   
    Hello Azure 포털에서에서 VM을 선택 합니다. Hello 설정 창 toohello 아래로 스크롤하여 **지원 + 문제 해결** hello 목록의 아래쪽 근처 섹션. Hello 클릭 **재배포** 단추를 선택한 다음 클릭 **재배포**:
   
    ![Hello Azure 포털에서에서 VM hello를 다시 배포](./media/troubleshoot-rdp-connection/redeploy-vm.png)
   
    이 작업이 완료 되 면 임시 디스크 데이터는 손실 및 동적 IP 주소는 VM을 업데이트 하는 hello와 연결 된입니다.

RDP 문제가 계속 발생하는 경우 [지원 요청을 열거나](https://azure.microsoft.com/support/options/) [좀 더 자세한 RDP 문제 해결 개념 및 단계](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 읽어볼 수 있습니다.

## <a name="troubleshoot-using-azure-powershell"></a>Azure PowerShell을 사용하여 문제 해결
아직 없는 경우, [설치 및 구성 최신 Azure PowerShell hello](/powershell/azure/overview)합니다.

hello 다음 예에서는 변수를 사용 같은 `myResourceGroup`, `myVM`, 및 `myVMAccessExtension`합니다. 이러한 변수 이름 및 위치를 사용자 고유의 값으로 바꿉니다.

> [!NOTE]
> Hello를 사용 하 여 hello 사용자 자격 증명 및 hello RDP 구성을 다시 [집합 AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet. 예제를 따르는 hello에 `myVMAccessExtension` hello 프로세스의 일부로 지정 하는 이름입니다. VMAccessAgent hello로 이전에 작업 하는 경우에 사용 하 여 기존 확장 hello의 hello 이름을 가져올 수 있습니다 `Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"` hello VM의 toocheck hello 속성입니다. hello 출력의 hello 'Extensions' 섹션에서 모양 tooview hello 이름입니다.

각 문제 해결 단계 후 tooyour VM을 다시 연결 하십시오. 여전히 연결할 수 없는 경우 hello 다음 단계를 시도 합니다.

1. **RDP 연결 다시 설정**. 이 문제 해결 단계에 원격 연결을 사용할 수 없습니다. 또는 예를 들어 Windows 방화벽 규칙 RDP를 차단 하는 경우 hello RDP 구성을 다시 설정 합니다.
   
    라는 VM에서 hello RDP 연결을 재설정 하는 hello에 따라 예제 `myVM` hello에 `WestUS` 위치 및 이라는 hello 리소스 그룹에 `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location Westus -Name "myVMAccessExtension"
    ```
2. **네트워크 보안 그룹 규칙 확인**. 이 문제 해결 단계는 네트워크 보안 그룹 toopermit RDP 트래픽의에 규칙이 있는지 확인 합니다. RDP에 대 한 hello 기본 포트는 TCP 포트 3389입니다. VM을 만들 때 규칙 toopermit RDP 트래픽이 자동으로 생성 되지 않을 수 있습니다.
   
    먼저, 네트워크 보안 그룹 toohello에 대 한 모든 hello 구성 데이터를 할당 `$rules` 변수입니다. hello 다음 예제에서는 정보를 가져오고 hello 라는 네트워크 보안 그룹에 대 한 `myNetworkSecurityGroup` 이라는 hello 리소스 그룹에 `myResourceGroup`:
   
    ```powershell
    $rules = Get-AzureRmNetworkSecurityGroup -ResourceGroupName "myResourceGroup" `
        -Name "myNetworkSecurityGroup"
    ```
   
    이제이 네트워크 보안 그룹에 대해 구성 된 hello 규칙 보기 규칙 tooallow 인바운드 연결에 대 한 TCP 포트 3389를 다음과 같이 존재 하는지 확인 하십시오.
   
    ```powershell
    $rules.SecurityRules
    ```
   
    hello 다음 예제에서는 RDP 트래픽을 허용 하는 유효한 보안 규칙 `Protocol`, `DestinationPortRange`, `Access` 및 `Direction`이 올바르게 구성된 것을 볼 수 있습니다.
   
    ```powershell
    Name                     : default-allow-rdp
    Id                       : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/default-allow-rdp
    Etag                     : 
    ProvisioningState        : Succeeded
    Description              : 
    Protocol                 : TCP
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : *
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 1000
    Direction                : Inbound
    ```
   
    RDP 트래픽을 허용하는 규칙이 없는 경우 [네트워크 보안 그룹 규칙을 만듭니다](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). TCP 포트 3389를 허용합니다.
3. **사용자 자격 증명 다시 설정**. 이 문제 해결 단계에는 hello, 확실 하지 않은 하거나 잊어버린, hello 자격 증명을 지정 하는 hello 로컬 관리자 계정의 암호 다시 설정 합니다.
   
    첫째, 사용자 이름 hello 및 toohello 자격 증명을 할당 하 여 새 암호를 지정 `$cred` 다음과 같이 변수:
   
    ```powershell
    $cred=Get-Credential
    ```
   
    이제 VM에서 hello 자격 증명을 업데이트 합니다. hello 다음 예제에서는 업데이트 라는 VM에서 hello 자격 증명 `myVM` hello에 `WestUS` 위치 및 이라는 hello 리소스 그룹에 `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location WestUS -Name "myVMAccessExtension" `
        -UserName $cred.GetNetworkCredential().Username `
        -Password $cred.GetNetworkCredential().Password
    ```
4. **VM 다시 시작**. 이 문제 해결 단계는 근본적인 문제를 해결할 수 hello VM 자체는 것입니다.
   
    다음 예제에서는 다시 시작 하는 hello hello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:
   
    ```powershell
    Restart-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
    ```
5. **VM 다시 배포**. 이 문제 해결 단계 VM tooanother 호스트 Azure toocorrect 내 모든 기본 플랫폼 또는 네트워킹 문제를 다시 배포합니다.
   
    다음 예에서는 재배포 시 hello hello 라는 VM `myVM` hello에 `WestUS` 위치 및 이라는 hello 리소스 그룹에 `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

RDP 문제가 계속 발생하는 경우 [지원 요청을 열거나](https://azure.microsoft.com/support/options/) [좀 더 자세한 RDP 문제 해결 개념 및 단계](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 읽어볼 수 있습니다.

## <a name="troubleshoot-vms-created-using-hello-classic-deployment-model"></a>Hello 클래식 배포 모델을 사용 하 여 만든 Vm 문제 해결
각 문제 해결 단계를 수행한 후 toohello VM을 다시 연결을 시도 합니다.

1. **RDP 연결 다시 설정**. 이 문제 해결 단계에 원격 연결을 사용할 수 없습니다. 또는 예를 들어 Windows 방화벽 규칙 RDP를 차단 하는 경우 hello RDP 구성을 다시 설정 합니다.
   
    Hello Azure 포털에서에서 VM을 선택 합니다. Hello 클릭 **... 더 많은** 단추를 클릭 **원격 액세스를 다시 설정**:
   
    ![Hello Azure 포털에서에서 hello RDP 구성을 다시 설정](./media/troubleshoot-rdp-connection/classic-reset-rdp.png)
2. **Cloud Services 끝점 확인**. 이 문제 해결 단계에 클라우드 서비스 toopermit RDP 트래픽의 끝점이 있는지 확인 합니다. RDP에 대 한 hello 기본 포트는 TCP 포트 3389입니다. VM을 만들 때 규칙 toopermit RDP 트래픽이 자동으로 생성 되지 않을 수 있습니다.
   
   Hello Azure 포털에서에서 VM을 선택 합니다. Hello 클릭 **끝점** VM에 대 한 현재 구성 된 tooview hello 끝점 단추입니다. TCP 포트 3389에서 RDP 트래픽을 허용하는 끝점이 있는지 확인합니다.
   
   다음 예제는 hello RDP 트래픽을 허용 하는 올바른 끝점을 보여 줍니다.
   
   ![Hello Azure 포털에서에서 클라우드 서비스 끝점 확인](./media/troubleshoot-rdp-connection/classic-verify-cloud-services-endpoints.png)
   
   RDP 트래픽을 허용하는 끝점이 없는 경우 [Cloud Services 끝점을 만듭니다](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Tooprivate 포트 3389 TCP를 허용 합니다.
3. **VM 부트 진단 검토**. 이 문제 해결 단계는 hello VM 문제를 보고 하는 경우 hello VM 콘솔 로그 toodetermine를 검토 합니다. 모든 VM에서 부팅 진단이 지원되는 것은 아니므로 이 문제 해결 단계는 선택 사항입니다.
   
    특정 문제 해결 단계 hello이이 문서에서는 다루지 않지만 하지만 RDP 연결에 영향을 주지는 광범위 한 문제를 나타낼 수 있습니다. Hello 콘솔 로그 및 VM 스크린샷을 검토에 대 한 자세한 내용은 참조 하십시오. [Vm에 대 한 부트 진단](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/)합니다.
4. **Hello VM 리소스 상태 확인**합니다. 이 문제 해결 단계는 연결 toohello VM에 영향을 줄 수 있는 Azure 플랫폼 hello로 알려진된 문제가 없는지 확인 합니다.
   
    Hello Azure 포털에서에서 VM을 선택 합니다. Hello 설정 창 toohello 아래로 스크롤하여 **지원 + 문제 해결** hello 목록의 아래쪽 근처 섹션. Hello 클릭 **리소스 상태** 단추입니다. 정상 VM은 **사용 가능**으로 보고합니다.
   
    ![Hello Azure 포털에서에서 VM 리소스 상태를 확인 합니다.](./media/troubleshoot-rdp-connection/classic-check-resource-health.png)
5. **사용자 자격 증명 다시 설정**. 이 문제 해결 단계에는 hello 확실 하지 않거나 잊어버려 hello 자격 증명을 지정 하는 hello 로컬 관리자 계정의 암호 다시 설정 합니다.
   
    Hello Azure 포털에서에서 VM을 선택 합니다. Hello 설정 창 toohello 아래로 스크롤하여 **지원 + 문제 해결** hello 목록의 아래쪽 근처 섹션. Hello 클릭 **암호 재설정** 단추입니다. 사용자 이름 및 새 암호를 입력합니다. 마지막으로 hello 클릭 **저장** 단추:
   
    ![Hello Azure 포털에서에서 hello 사용자 자격 증명 다시 설정](./media/troubleshoot-rdp-connection/classic-reset-password.png)
6. **VM 다시 시작**. 이 문제 해결 단계는 근본적인 문제를 해결할 수 hello VM 자체는 것입니다.
   
    Hello Azure 포털에서에서 VM을 선택 하 고 hello 클릭 **개요** 탭 합니다. Hello 클릭 **다시 시작** 단추:
   
    ![Hello Azure 포털에서에서 VM hello를 다시 시작](./media/troubleshoot-rdp-connection/classic-restart-vm.png)

RDP 문제가 계속 발생하는 경우 [지원 요청을 열거나](https://azure.microsoft.com/support/options/) [좀 더 자세한 RDP 문제 해결 개념 및 단계](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 읽어볼 수 있습니다.

## <a name="troubleshoot-specific-rdp-errors"></a>특정 RDP 오류 해결
RDP 통해 VM tooconnect tooyour 하려고 할 때 특정 오류 메시지가 발생할 수 있습니다. hello 다음은 hello 가장 일반적인 오류 메시지입니다.

* [원격 데스크톱 라이선스 서버 사용 가능한 tooprovide 없습니다 라이선스 있기 때문에 hello 원격 연결이 끊어졌습니다](troubleshoot-specific-rdp-errors.md#rdplicense)합니다.
* [원격 데스크톱 hello 컴퓨터 "이름"에서 찾을 수 없는](troubleshoot-specific-rdp-errors.md#rdpname)합니다.
* [인증 오류가 발생 했습니다. hello 로컬 보안 기관에 연결할 수 없는](troubleshoot-specific-rdp-errors.md#rdpauth)합니다.
* [Windows 보안 오류: 자격 증명이 작동하지 않습니다](troubleshoot-specific-rdp-errors.md#wincred).
* [이 컴퓨터 toohello 원격 컴퓨터에 연결할 수 없는](troubleshoot-specific-rdp-errors.md#rdpconnect)합니다.

## <a name="additional-resources"></a>추가 리소스
이러한 오류 중에 발생 한 경우 여전히 toohello VM 원격 데스크톱을 통해 연결할 수 없는 읽기 세부 hello [문제 해결 가이드에 대 한 원격 데스크톱](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
* VM에서 실행 중인 응용 프로그램에 액세스 하는 단계를 문제 해결을 위해 참조 [문제 해결 액세스 tooan 응용 프로그램이 Azure VM에서 실행 중인](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
* Azure에서 SSH (보안 셸) tooconnect tooa Linux VM을 사용 하는 데 문제가 있는 경우 참조 [해결 SSH 연결 tooa Azure에서 Linux VM](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

