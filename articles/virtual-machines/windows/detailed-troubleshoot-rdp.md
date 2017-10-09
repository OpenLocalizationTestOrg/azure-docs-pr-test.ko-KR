---
title: "Azure에서 문제 해결 aaaDetailed 원격 데스크톱 | Microsoft Docs"
description: "원격 데스크톱 오류 tooa Azure의 가상 컴퓨터를 Windows 수 없는 위치에 대 한 자세한 문제 해결 단계를 검토 합니다."
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
keywords: "tooremote 데스크톱에 연결할 수 없습니다, 원격 데스크톱을 해결 원격 데스크톱 오류, 원격 데스크톱 문제 해결, 원격 데스크톱 문제 원격 데스크톱 연결할 수 없습니다"
ms.assetid: 9da36f3d-30dd-44af-824b-8ce5ef07e5e0
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: fcb0d06aa66b748f3ebbbbe3431471d3cbe7c60d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-troubleshooting-steps-for-remote-desktop-connection-issues-toowindows-vms-in-azure"></a>TooWindows Azure에서 Vm을 발급 하는 원격 데스크톱 연결에 대 한 자세한 문제 해결 단계
이 문서에서는 Azure 가상 컴퓨터의 Windows 기반 상세한 문제 해결 단계 toodiagnose 및 수정 하는 복잡 한 원격 데스크톱 오류 제공 합니다.

> [!IMPORTANT]
> tooeliminate hello 일반적인 원격 데스크톱 오류를 확인 하는지 tooread [원격 데스크톱에 대 한 기본 문제 해결 문서를 hello](troubleshoot-rdp-connection.md) 계속 진행 하기 전에.

원격 데스크톱에서 다루는 hello 특정 오류 메시지와 유사 하지 않습니다 오류 메시지가 발생할 수 있습니다 [문제 해결 가이드 기본 원격 데스크톱 hello](troubleshoot-rdp-connection.md)합니다. 이러한 단계 toodetermine 이유 hello RDP (원격 데스크톱) 클라이언트는 hello Azure VM에 없습니다 tooconnect toohello RDP 서비스를 수행 합니다.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

이 문서에서 언제 든 지 자세한 도움말을 보려는 경우 문의할 수 있습니다에 Azure 전문가 hello [MSDN Azure hello 및 스택 오버플로 포럼 hello](https://azure.microsoft.com/support/forums/)합니다. 또는 Azure 기술 지원 인시던트를 제출할 수도 있습니다. Toohello 이동 [Azure 지원 사이트](https://azure.microsoft.com/support/options/) 클릭 **Get Support**합니다. Azure 지원을 사용 하는 방법에 대 한 내용은 하세요 hello [Microsoft Azure 지원 FAQ](https://azure.microsoft.com/support/faq/)합니다.

## <a name="components-of-a-remote-desktop-connection"></a>원격 데스크톱 연결을 위한 구성 요소
다음과 같은 구성 요소가 hello RDP 연결에 관련 된:

![](./media/detailed-troubleshoot-rdp/tshootrdp_0.png)

계속 하기 전에 것 toomentally hello 마지막 성공적으로 원격 데스크톱 연결 toohello VM 이후 변경 된 내용 검토이 도움이 될 수 있습니다. 예:

* hello hello VM 또는 hello 포함 된 클라우드 서비스 hello VM의 공용 IP 주소 (가상 IP 주소 hello 라고도 [VIP](https://en.wikipedia.org/wiki/Virtual_IP_address)) 변경 되었습니다. DNS 클라이언트 캐시에 아직 hello hello RDP 실패 원인은 *이전 IP 주소* hello DNS 이름에 대 한 등록 합니다. DNS 클라이언트 캐시를 플러시하고 hello VM을 다시 연결 해 보십시오. 또는 새 VIP hello와 직접 연결 해 보십시오.
* 사용 하는 타사 응용 프로그램 toomanage 원격 데스크톱 연결 hello Azure 포털에서 생성 된 hello 연결을 사용 하는 대신 합니다. Hello 원격 데스크톱 트래픽 hello에 대 한 올바른 TCP 포트를 포함 하는 hello 응용 프로그램 구성을 확인 합니다. Hello에 클래식 가상 컴퓨터에 대 한이 포트를 확인할 수 있습니다 [Azure 포털](https://portal.azure.com), hello VM 설정을 클릭 하 여 > 끝점입니다.

## <a name="preliminary-steps"></a>준비 단계
계속 하기 전에 toohello 자세한 문제 해결,

* Hello 모든 문제에 대 한 Azure 포털에서에서 가상 컴퓨터 hello의 hello 상태를 확인 합니다.
* Hello에 따라 [hello 기본적인 문제 해결의 일반적인 RDP 오류에 대 한 빠른 해결 단계를 안내](troubleshoot-rdp-connection.md#quick-troubleshooting-steps)합니다.

그런 다음 toohello 원격 데스크톱을 통해 VM을 다시 연결 하십시오.

## <a name="detailed-troubleshooting-steps"></a>자세한 문제 해결
원격 데스크톱 클라이언트 hello 수 tooreach hello Azure VM에 원격 데스크톱 서비스를 hello 아닐 due tooissues hello 원본에서:

* [원격 데스크톱 클라이언트 컴퓨터](#source-1-remote-desktop-client-computer)
* [조직 인트라넷 에지 장치](#source-2-organization-intranet-edge-device)
* [클라우드 서비스 끝점 및 액세스 제어 목록(ACL)](#source-3-cloud-service-endpoint-and-acl)
* [네트워크 보안 그룹](#source-4-network-security-groups)
* [Windows 기반 Azure VM](#source-5-windows-based-azure-vm)

## <a name="source-1-remote-desktop-client-computer"></a>발생지 1: 원격 데스크톱 클라이언트 컴퓨터
컴퓨터에 원격 데스크톱을 만들 수 있는지 확인 연결 tooanother 온-프레미스, Windows 기반 컴퓨터입니다.

![](./media/detailed-troubleshoot-rdp/tshootrdp_1.png)

수 없는 경우 hello에 나오는 설정에 따라 컴퓨터를 확인 합니다.

* 원격 데스크톱 트래픽을 차단하는 로컬 방화벽 설정
* 원격 데스크톱 연결을 방지하는 로컬에 설치된 클라이언트 프록시 소프트웨어
* 원격 데스크톱 연결을 방지하는 로컬에 설치된 네트워크 모니터링 소프트웨어
* 트래픽을 모니터링하거나 특정 유형의 트래픽을 허용/비허용하며 원격 데스크톱 연결을 방지하는 다른 유형의 보안 소프트웨어

이러한 모든 경우 hello 소프트웨어를 사용 하지 않도록 일시적으로 원격 데스크톱을 통해 tooconnect tooan 온-프레미스 컴퓨터를 시도 하십시오. 이러한 방식으로 hello 실제 원인을 알아낼 수 있습니다, 하는 경우 네트워크 관리자 toocorrect hello 소프트웨어 설정 tooallow 원격 데스크톱 연결을 사용 합니다.

## <a name="source-2-organization-intranet-edge-device"></a>발생지 2: 조직 인트라넷 에지 장치
컴퓨터에 직접 인터넷에서 원격 데스크톱 연결 tooyour Azure 가상 컴퓨터를 만들 수 toohello 연결을 확인 합니다.

![](./media/detailed-troubleshoot-rdp/tshootrdp_2.png)

직접 연결 하는 컴퓨터가 없는 경우 toohello 인터넷을 만들고 리소스 그룹 또는 클라우드 서비스에서 새로운 Azure 가상 컴퓨터와 테스트 합니다. 자세한 내용은 [Azure에서 Windows를 실행하는 가상 컴퓨터 만들기](../virtual-machines-windows-hero-tutorial.md)를 참조하세요. Hello 테스트 후 hello 가상 컴퓨터 및 hello 리소스 그룹 또는 hello 클라우드 서비스를 삭제할 수 있습니다.

컴퓨터 직접 연결 된 toohello 인터넷으로 원격 데스크톱 연결을 만들면 수에 대 한 조직의 인트라넷 가장자리 장치를 확인 하십시오.

* 내부 방화벽 HTTPS 연결 toohello 인터넷을 차단 합니다.
* 원격 데스크톱 연결을 방지하는 프록시 서버
* 경계 네트워크의 장치에서 실행되는, 원격 데스크톱 연결을 방지하는 침입 탐지 또는 네트워크 모니터링 소프트웨어

사용자 조직의 인트라넷 가장자리 장치 tooallow HTTPS 기반 원격 데스크톱 연결 toohello 인터넷의 네트워크 관리자 toocorrect hello 설정과 함께 작동 합니다.

## <a name="source-3-cloud-service-endpoint-and-acl"></a>발생지 3: 클라우드 서비스 끝점 및 ACL
가 있는 Azure VM 만든 Vm hello 클래식 배포 모델을 사용 하 여 확인에 대 한 hello에 동일한 클라우드 서비스 또는 가상 네트워크는 원격 데스크톱 연결 tooyour Azure VM을 만들 수 있습니다.

![](./media/detailed-troubleshoot-rdp/tshootrdp_3.png)

> [!NOTE]
> 리소스 관리자에서 만든 가상 컴퓨터에 대 한 건너뛸 너무[소스 4: 네트워크 보안 그룹](#source-4-network-security-groups)합니다.

다른 가상 컴퓨터에 hello 동일한 클라우드 서비스 또는 가상 네트워크를 만드십시오 하지 않은 경우. Hello 단계에 따라 [Windows Azure에서 실행 중인 가상 컴퓨터를 만드는](../virtual-machines-windows-hero-tutorial.md)합니다. Hello 테스트가 완료 된 후 hello 테스트 가상 컴퓨터를 삭제 합니다.

동일한 클라우드 서비스 또는 가상 네트워크 hello에 원격 데스크톱 tooa 가상 컴퓨터를 통해 연결할 수 있는 경우 이러한 설정을 확인 합니다.

* hello 대상 VM에 원격 데스크톱 트래픽에 대 한 끝점 구성을 hello: hello hello 끝점의 개인 TCP 포트에는 VM의 원격 데스크톱 서비스는 hello에서 수신 하는 hello TCP 포트 일치 해야 합니다 (기본값은 3389 임).
* hello 대상 VM에 원격 데스크톱 트래픽 끝점 hello에 대 한 ACL hello: Acl 허용 toospecify 허용 되거나 hello는 원본 IP 주소를 기준으로 인터넷에서 들어오는 트래픽을 거부 합니다. 잘못 구성 된 Acl 들어오는 원격 데스크톱 트래픽 toohello 끝점을 방지할 수 있습니다. 공용 IP 주소에 프록시 또는 다른 지 서버에서 들어오는 트래픽을 허용 하 여 Acl tooensure를 확인 합니다. 자세한 내용은 [네트워크 ACL(액세스 제어 목록)이란?](../../virtual-network/virtual-networks-acl.md)

toocheck은 hello 끝점이 hello 소스 hello 문제의 경우 hello 현재 끝점을 제거 하 고 hello 범위 49152-65535 hello 외부 포트 번호에 대 한 임의 포트를 선택 하는 새 대시보드를 만듭니다. 자세한 내용은 참조 [어떻게 끝점 tooa 가상 컴퓨터를 tooset](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.

## <a name="source-4-network-security-groups"></a>소스 4: 네트워크 보안 그룹
네트워크 보안 그룹은 허용되는 인바운드 및 아웃바운드 트래픽을 더 세부적으로 제어하는 데 사용됩니다. Azure 가상 네트워크의 서브넷 및 클라우드 서비스에 적용되는 규칙을 만들 수 있습니다.

사용 하 여 [IP 흐름 확인](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) tooconfirm 네트워크 보안 그룹의 규칙은 가상 컴퓨터에서 트래픽을 tooor를 차단 하는 경우. 또한 tooensure 인바운드 "허용" NSG 규칙 규칙 존재 및 RDP 포트 (기본값 3389)에 대 한 우선 순위를 가지도록 효과적인 보안 그룹을 검토할 수 있습니다. 자세한 내용은 참조 [효과적인 보안 규칙을 사용 하 여 tootroubleshoot VM 트래픽 흐름](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow)합니다.

## <a name="source-5-windows-based-azure-vm"></a>발생지 5: Windows 기반 Azure VM
![](./media/detailed-troubleshoot-rdp/tshootrdp_5.png)

Hello 지침에 따라 [이 여기서](reset-rdp.md)합니다. 이 문서에는 hello 가상 컴퓨터에 대 한 hello 원격 데스크톱 서비스를 다시 설정합니다.

* Hello "원격 데스크톱" Windows 방화벽 기본 규칙 (TCP 포트 3389)를 사용 합니다.
* Hello 사용 하 고 Server\fDenyTSConnections 레지스트리 값 too0를 설정 하 여 원격 데스크톱 연결을 설정 합니다.

Hello 연결을 컴퓨터에서 다시 시도 하십시오. 원격 데스크톱을 통해 수 없습니다. tooconnect 인 경우 hello 다음 발생 가능한 문제를 확인 합니다.

* 원격 데스크톱 서비스 hello hello 대상 VM에서 실행 되지 않습니다.
* hello 원격 데스크톱 서비스는 TCP 포트 3389에서 수신 하지 않는 합니다.
* Windows 방화벽 또는 다른 로컬 방화벽에 원격 데스크톱 트래픽을 방지하는 아웃바운드 규칙이 있습니다.
* 침입 검색 또는 네트워크 모니터링 hello Azure 가상 컴퓨터에서 실행 중인 소프트웨어 때문에 원격 데스크톱 연결 합니다.

Hello 클래식 배포 모델을 사용 하 여 만든 Vm에 대해서는 원격 Azure PowerShell 세션 toohello Azure 가상 컴퓨터를 사용할 수 있습니다. 먼저 인증서 tooinstall hello 가상 컴퓨터 호스팅 클라우드 서비스에 대 한 합니다. 너무 이동[가상 컴퓨터 원격 PowerShell 액세스 보호를 구성 tooAzure](http://gallery.technet.microsoft.com/scriptcenter/Configures-Secure-Remote-b137f2fe) hello를 다운로드 하 고 **InstallWinRMCertAzureVM.ps1** 스크립트 파일 tooyour 로컬 컴퓨터입니다.

다음으로, 아직 없는 경우 Azure PowerShell을 설치합니다. 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

그런 다음 Azure PowerShell 명령 프롬프트를 열고 hello 현재 toohello의 위치를 변경 hello **InstallWinRMCertAzureVM.ps1** 스크립트 파일입니다. Azure PowerShell 스크립트 toorun hello 올바르게 실행 정책을 설정 해야 합니다. Hello 실행 **Get-executionpolicy** 현재의 정책 수준 toodetermine 명령입니다. Hello 적절 한 수준 설정에 대 한 내용은 [Set-executionpolicy](https://technet.microsoft.com/library/hh849812.aspx)합니다.

다음으로, Azure 구독 이름, hello 클라우드 서비스 이름 및 가상 컴퓨터 이름 (hello < 및 > 문자 제거)를 입력 한 후 이러한 명령을 실행 합니다.

```powershell
$subscr="<Name of your Azure subscription>"
$serviceName="<Name of hello cloud service that contains hello target virtual machine>"
$vmName="<Name of hello target virtual machine>"
.\InstallWinRMCertAzureVM.ps1 -SubscriptionName $subscr -ServiceName $serviceName -Name $vmName
```

Hello에서 hello 올바른 구독 이름을 가져올 수 있습니다 *SubscriptionName* 속성의 hello hello 디스플레이의 **Get-azuresubscription** 명령입니다. Hello에서 hello 가상 컴퓨터용 클라우드 서비스 이름 hello를 얻을 수 있습니다 *ServiceName* hello의 hello 디스플레이에 열 **Get-azurevm** 명령입니다.

새 인증서 hello 있는지 확인 합니다. Hello hello 현재 사용자에 대 한 인증서 스냅인 열고 **신뢰할 수 있는 루트 인증 기관 인증서** 폴더입니다. 인증서 발급 대상 toocolumn hello에 클라우드 서비스의 hello DNS 이름으로 표시 됩니다 (예: cloudservice4testing.cloudapp.net).

다음으로, 이러한 명령을 사용하여 원격 Azure PowerShell 세션을 시작합니다.

```powershell
$uri = Get-AzureWinRMUri -ServiceName $serviceName -Name $vmName
$creds = Get-Credential
Enter-PSSession -ConnectionUri $uri -Credential $creds
```

올바른 관리자 자격 증명을 입력 한 후 다음 Azure PowerShell 프롬프트는 다음과 유사한 toohello를 나타나야 합니다.

```powershell
[cloudservice4testing.cloudapp.net]: PS C:\Users\User1\Documents>
```

이 메시지의 첫 번째 부분 hello는 "cloudservice4testing.cloudapp.net"에서 다를 수 있습니다는 hello 대상 VM에 포함 된 클라우드 서비스 이름입니다. 이제 서비스 tooinvestigate hello 문제 언급이 클라우드에 대 한 Azure PowerShell 명령을 실행 하 고 hello 구성 해결할 수 있습니다.

### <a name="toomanually-correct-hello-remote-desktop-services-listening-tcp-port"></a>toomanually 올바른 hello TCP 포트를 수신 대기 하는 원격 데스크톱 서비스
프롬프트 hello 원격 Azure PowerShell 세션에서이 명령을 실행 합니다.

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

PortNumber 속성이 hello hello 현재 포트 번호를 보여 줍니다. 필요한 경우이 명령을 사용 하 여 hello 원격 데스크톱 포트 번호 백 tooits 기본값 (3389) 변경 합니다.

```powershell
Set-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber" -Value 3389
```

Hello 포트를이 명령을 사용 하 여 변경 된 too3389를 되었는지 확인 합니다.

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

이 명령을 사용 하 여 hello 원격 Azure PowerShell 세션을 종료 합니다.

```powershell
Exit-PSSession
```

해당 hello hello Azure VM에 대 한 원격 데스크톱 끝점을 사용 하면 TCP 포트 3398를 내부 포트로 확인 합니다. Hello Azure VM을 다시 시작 하 고 hello 원격 데스크톱 연결을 다시 시도 하십시오.

## <a name="additional-resources"></a>추가 리소스
[Windows 가상 컴퓨터에 대 한 암호 tooreset 또는 hello 원격 데스크톱 서비스 하는 방법](reset-rdp.md)

[어떻게 tooinstall Azure PowerShell 및 구성](/powershell/azure/overview)

[SSH (보안 셸) 연결 tooa Linux 기반 Azure 가상 컴퓨터 문제 해결](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Azure 가상 컴퓨터에서 실행 되는 액세스 tooan 응용 프로그램 문제 해결](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

