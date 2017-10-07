---
title: "aaaPreparing Azure 가상 컴퓨터를 사용자 환경 tooback | Microsoft Docs"
description: "환경이 Azure의 가상 컴퓨터를 백업할 준비가 되었는지 확인합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonn
editor: 
keywords: "백업; 백업;"
ms.assetid: 238ab93b-8acc-4262-81b7-ce930f76a662
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/25/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 3b914c507dd6ad703ea799115ae84ac229e27787
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-environment-tooback-up-azure-virtual-machines"></a>사용자 환경 tooback Azure 가상 컴퓨터를 준비 합니다.
> [!div class="op_single_selector"]
> * [Resource Manager 모델](backup-azure-arm-vms-prepare.md)
> * [클래식 모델](backup-azure-vms-prepare.md)
>
>

Azure VM(가상 컴퓨터)을 백업하려면 세 가지 조건을 충족해야 합니다.

* 백업 자격 증명 모음 toocreate 필요 하거나는 기존 백업 자격 증명 모음을 식별 *hello에서 VM으로 같은 지역*합니다.
* Azure 공용 인터넷 및 Azure 저장소 끝점 hello hello 간의 네트워크 연결을 설정 합니다.
* Hello VM에 hello VM 에이전트를 설치 합니다.

이러한 조건에서 이미 환경에 존재 하 다음 toohello 진행을 알고 있는 경우 [VMs 문서를 백업](backup-azure-vms.md)합니다. 그렇지 않으면 읽어 보려면이 문서를 안내 합니다 hello 단계 tooprepare Azure VM을 사용자 환경 tooback 합니다.

##<a name="supported-operating-system-for-backup"></a>지원되는 백업용 운영 체제
 * **Linux**: Azure Backup은 Core OS Linux를 제외한 [Azure 인증 배포 목록](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 지원합니다. _도 하 게 다른 Bring-Your-소유-Linux 배포판 hello VM 에이전트는 hello 가상 컴퓨터에서 사용할 수 있는 정상적으로 작동 못할 수도 있으며 Python에 대 한 지원. 그러나 이러한 배포판을 백업에 대해서는 보증하지 않습니다._
 * **Windows Server**: Windows Server 2008 R2 이전 버전은 지원되지 않습니다.


## <a name="limitations-when-backing-up-and-restoring-a-vm"></a>VM 백업 및 복원 시의 제한 사항
> [!NOTE]
> Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델인 [리소스 관리자와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)모델이 있습니다. hello 다음 목록에서는 hello 제한 hello 클래식 모델에 배포 하는 경우.
>
>

* 16개 이상의 데이터 디스크가 있는 가상 컴퓨터의 백업은 지원되지 않습니다.
* 예약된 IP 주소가 있고 정의된 끝점이 없는 가상 컴퓨터의 백업은 지원되지 않습니다.
* 백업 데이터는 탑재 된 네트워크 연결 된 드라이브 tooVM 포함 되지 않습니다.
* 복원하는 동안 기존 가상 컴퓨터의 교체는 지원되지 않습니다. 먼저 hello 기존 가상 컴퓨터 및 모든 관련된 디스크를 삭제 하 고 hello 데이터 백업에서 복원 합니다.
* 지역 간 백업 및 복원은 지원되지 않습니다.
* Azure의 모든 공용 영역에 사용할 hello Azure 백업 서비스를 사용 하 여 가상 컴퓨터를 백업 합니다 (hello 참조 [검사 목록](https://azure.microsoft.com/regions/#services) 지원 되는 지역). 원하는 hello 영역 지원 되지 않는 오늘 경우 자격 증명 모음을 만드는 동안 hello 드롭다운 목록에서 표시 되지 않습니다.
* Hello Azure 백업 서비스를 사용 하 여 가상 컴퓨터를 백업 합니다. 선택 운영 체제 버전에 대해서만 지원 됩니다.
* 다중 DC 구성의 일부인 도메인 컨트롤러(DC) VM 복원은 PowerShell을 통해서만 지원됩니다. [다중 DC 도메인 컨트롤러 복원](backup-azure-restore-vms.md#restoring-domain-controller-vms)에 대해 자세히 알아보세요.
* 특수 한 네트워크 구성을 따르고 hello에 있는 가상 컴퓨터를 복원 PowerShell 통해만 지원 됩니다. Hello에 hello 복원 워크플로 사용 하 여 만든 Vm hello 복원 작업이 완료 된 후 UI가 이러한 구성을는 하지 않습니다. toolearn 더 참조 [특수 한 네트워크 구성으로 복원 Vm](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations)합니다.
  * 부하 분산 장치 구성에서의 가상 컴퓨터(내부 및 외부)
  * 다중의 예약된 IP 주소가 있는 가상 컴퓨터
  * 다중 네트워크 어댑터가 있는 가상 컴퓨터

## <a name="create-a-backup-vault-for-a-vm"></a>VM에 대한 백업 자격 증명 모음 만들기
백업 자격 증명 모음에는 모든 hello 백업 및 시간에 따라 생성 된 복구 지점을 저장 하는 엔터티입니다. hello 백업 자격 증명 모음에는 적용 된 toohello 가상 컴퓨터를 백업할 수 있는 hello 백업 정책이 포함 되어 있습니다.

> [!IMPORTANT]
> 2017 년 3 월 부터는 hello 클래식 포털 toocreate 백업 자격 증명 모음은 더 이상 사용할 수 없습니다. 기존 백업 자격 증명 모음은 계속 지원 되며 가능한 너무[toocreate 백업 자격 증명 모음은 Azure PowerShell을 사용 하 여](./backup-client-automation-classic.md#create-a-backup-vault)합니다. 이후의 향상 된 내용을 tooRecovery 서비스 자격 증명 모음을만 적용 되므로 모든 배포에 대해 복구 서비스 자격 증명 모음을 만드는 것이 좋습니다.


이 이미지는 hello hello 관계 다양 한 Azure 백업 엔터티를 보여: ![Azure 백업 엔터티 및 관계](./media/backup-azure-vms-prepare/vault-policy-vm.png)



## <a name="network-connectivity"></a>네트워크 연결
순서 toomanage hello VM 스냅숏 백업 확장 hello 필요 연결 toohello Azure 공용 IP 주소입니다. Hello 오른쪽 인터넷에 연결 하지 않고 hello 가상 컴퓨터의 HTTP 요청 시간 제한 및 hello 백업 작업이 실패합니다. 배포에 액세스 제한이 있다면(예: 네트워크 보안 그룹(NSG)을 통해), 백업 트래픽에 대해 명확한 경로를 제공하기 위해 이 옵션 중 하나를 선택합니다.

* [화이트 리스트 hello Azure 데이터 센터 IP 범위](http://www.microsoft.com/en-us/download/details.aspx?id=41653) -어떻게 toowhitelist hello IP 주소에 대 한 지침은 hello 문서를 참조 합니다.
* 트래픽 라우팅을 위해 HTTP 프록시 서버를 배포합니다.

어떤 옵션 toouse를 결정할 때는 hello 장단점은 관리 효율성, 세분화 된 제어 및 비용 까지입니다.

| 옵션 | 장점 | 단점 |
| --- | --- | --- |
| 허용 목록 IP 범위 |추가 비용 없음<br><br>NSG에 대 한 액세스를 열기 위한 hello를 사용 하 여 <i>집합 AzureNetworkSecurityRule</i> cmdlet. |시간에 따른 영향을 받음 hello IP 범위 변경으로 복잡 한 toomanage 합니다.<br><br>Azure 및 뿐 아니라 저장소의 toohello 전체 액세스를 제공합니다. |
| HTTP 프록시 |Url 허용 hello 저장소 hello 프록시에 세부적으로 제어 합니다. hello 프록시의 toosetup 세부적으로 제어 https://\*.blob.core.windows.net/\* URL 패턴 toobe 허용 목록 필요 합니다. toowhitelist에만 저장소 계정에서 hello VM 사용 하는 hello https://\<storageAccount\>.blob.core.windows.net/\* URL 패턴 toobe 허용 목록 필요 합니다. <br>단일 지점 인터넷 액세스 tooVMs 합니다.<br>IP 주소 변경 내용을 tooAzure 대상이 아닙니다. |Hello 프록시 소프트웨어와 함께 VM을 실행 하기 위한 추가 비용이 있습니다. |

### <a name="whitelist-hello-azure-datacenter-ip-ranges"></a>화이트 리스트 hello Azure 데이터 센터 IP 범위
toowhitelist hello Azure 데이터 센터 IP 범위를 참조 하십시오. hello [Azure 웹 사이트](http://www.microsoft.com/en-us/download/details.aspx?id=41653) hello IP 범위 및 지침에 대 한 자세한 내용은 합니다.

### <a name="using-an-http-proxy-for-vm-backups"></a>VM 백업에 HTTP 프록시 사용
VM을 백업할 때 hello VM에 예비 내선 번호 hello hello 스냅숏 관리 명령을 tooAzure HTTPS API를 사용 하 여 저장소를 보냅니다. 액세스 toohello에 대해 구성 된 hello 유일한 구성 요소 이므로 hello HTTP 프록시를 통해 hello 예비 내선 번호 트래픽을 라우팅할 공용 인터넷 합니다.

> [!NOTE]
> 사용 해야 하는 hello 프록시 소프트웨어에 대 한 권장 사항 없음 있습니다. 아웃 바운드 인력을 가진 프록시를 선택 하는 확인 하 고 hello 구성 단계와 호환 되는 키를 누릅니다. 제 3 자 있으며 소프트웨어 hello 프록시 설정도 수정 하지 있는지 확인
>
>

아래 예제에서는 이미지 hello hello 세 가지 구성 단계가 필요한 toouse HTTP 프록시를 보여 줍니다.

* 응용 프로그램 VM 경로 대 한 모든 HTTP 트래픽이 바인딩된 hello 공용 인터넷을 통해 프록시 VM입니다.
* 프록시 VM hello 가상 네트워크의 Vm에서 들어오는 트래픽을 허용합니다.
* hello 그룹 NSG (네트워크 보안) 라는 NSF 잠금에는 보안 규칙 아웃 바운드 인터넷 트래픽을 허용 프록시 VM에서 필요 합니다.

![HTTP 프록시 배포 다이어그램을 사용하는 NSG](./media/backup-azure-vms-prepare/nsg-with-http-proxy.png)

toouse HTTP 프록시 toocommunicating toohello 공용 인터넷을 다음이 단계를 수행 합니다.

#### <a name="step-1-configure-outgoing-network-connections"></a>1단계. 나가는 네트워크 연결 구성
###### <a name="for-windows-machines"></a>Windows 컴퓨터의 경우
로컬 시스템 계정에 대한 프록시 서버 구성을 설정합니다.

1. [PsExec](https://technet.microsoft.com/sysinternals/bb897553)
2. 관리자 권한 프롬프트에서 다음 명령을 실행합니다.

     ```
     psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"
     ```
     Internet Explorer 창이 열립니다.
3. 이동 tooTools-> 인터넷 옵션-> 연결-> LAN 설정 합니다.
4. 시스템 계정에 대한 프록시 설정을 확인합니다. 프록시 IP 및 포트를 설정합니다.
5. Internet Explorer를 닫습니다.

시스템 수준의 프록시 구성을 설정하고 나가는 HTTP/HTTPS 트래픽에 사용됩니다.

설치 프로그램 프록시 서버에 있으면 현재 사용자 계정 (로컬 시스템 계정이 아닌 함)를 사용 하 여 hello 스크립트 tooapply 다음 해당 tooSYSTEMACCOUNT:

```
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name DefaultConnectionSettings -Value $obj.DefaultConnectionSettings
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name SavedLegacySettings -Value $obj.SavedLegacySettings
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name ProxyEnable -Value $obj.ProxyEnable
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name Proxyserver -Value $obj.Proxyserver
```

> [!NOTE]
> 프록시 서버 로그에 "(407)프록시 인증 필요"가 발견되면, 인증이 제대로 설정되었는지 확인합니다.
>
>

###### <a name="for-linux-machines"></a>Linux 컴퓨터의 경우
다음 줄 toohello hello 추가 ```/etc/environment``` 파일:

```
http_proxy=http://<proxy IP>:<proxy port>
```

다음 줄 toohello hello 추가 ```/etc/waagent.conf``` 파일:

```
HttpProxy.Host=<proxy IP>
HttpProxy.Port=<proxy port>
```

#### <a name="step-2-allow-incoming-connections-on-hello-proxy-server"></a>2단계. Hello 프록시 서버에서 들어오는 연결을 허용 합니다.
1. Hello 프록시 서버에서 Windows 방화벽을 엽니다. hello 가장 쉬운 방법은 tooaccess hello 방화벽은 고급 보안이 포함 된 Windows 방화벽에 대 한 toosearch입니다.

    ![Hello 방화벽을 열으십시오](./media/backup-azure-vms-prepare/firewall-01.png)
2. Hello Windows 방화벽 대화 상자에서 마우스 오른쪽 단추로 클릭 **인바운드 규칙** 클릭 **새 규칙...** .

    ![새 규칙 만들기](./media/backup-azure-vms-prepare/firewall-02.png)
3. Hello에 **새 인바운드 규칙 마법사**, hello 선택 **사용자 지정** hello에 대 한 옵션 **규칙 유형** 클릭 **다음**합니다.
4. Hello 페이지 tooselect hello에 **프로그램**, 선택 **모든 프로그램** 클릭 **다음**합니다.
5. Hello에 **프로토콜 및 포트** 페이지 hello 다음 정보를 입력 하 고 클릭 **다음**:

    ![새 규칙 만들기](./media/backup-azure-vms-prepare/firewall-03.png)

   * *프로토콜 유형*에서 *TCP*를 선택합니다.
   * 에 대 한 *로컬 포트* 선택 *특정 포트*, 아래의 hello 필드에 지정 hello ```<Proxy Port>``` 구성 된 합니다.
   * *원격 포트*에서 *모든 포트*를 선택합니다.

     Hello 마법사의 나머지에서는 hello 모든 hello 방식으로 toohello 종료를 클릭 하 고이 규칙 이름을 지정 합니다.

#### <a name="step-3-add-an-exception-rule-toohello-nsg"></a>3단계. 예외 규칙 toohello NSG를 추가 합니다.
Azure PowerShell 명령 프롬프트를 hello 다음 명령을 입력 합니다.

다음 명령을 hello 예외 toohello NSG를 추가 합니다. 이 예외 10.0.0.5에서 모든 포트에서의 TCP 트래픽을 허용 tooany 포트 80 (HTTP) 또는 443 (HTTPS)에 대 한 인터넷 주소입니다. 특정 포트가 필요한 경우 hello 공용 인터넷을 toohello 포트 있는지 tooadd 수 ```-DestinationPortRange``` 도 합니다.

```
Get-AzureNetworkSecurityGroup -Name "NSG-lockdown" |
Set-AzureNetworkSecurityRule -Name "allow-proxy " -Action Allow -Protocol TCP -Type Outbound -Priority 200 -SourceAddressPrefix "10.0.0.5/32" -SourcePortRange "*" -DestinationAddressPrefix Internet -DestinationPortRange "80-443"
```

*Hello, 적절 한 tooyour 배포 세부 정보로 hello 예에서 hello 이름을 바꾸는 것을 확인 합니다.*

## <a name="vm-agent"></a>VM 에이전트
Hello Azure 가상 컴퓨터를 백업할 수 있습니다, 전에 hello Azure VM 에이전트에 hello 가상 컴퓨터에 제대로 설치를 확인 해야 합니다. Hello VM 에이전트가 가상 컴퓨터를 hello hello 시 선택적 구성 요소를 만들어질 이므로, 해당 hello 확인란 hello 가상 컴퓨터 프로 비전 하기 전에 hello VM 에이전트 선택에 대 한 확인 합니다.

### <a name="manual-installation-and-update"></a>수동 설치 및 업데이트
hello VM 에이전트 hello Azure 갤러리에서에서 생성 된 Vm에 이미 있습니다. 그러나 온-프레미스 데이터 센터에서 마이그레이션된 가상 컴퓨터 hello VM 에이전트가 설치 되어 있어야 합니다. 이러한 Vm에 대 한 hello VM 에이전트 toobe 명시적으로 설치 해야 합니다. 에 대해 자세히 알아보세요 [hello VM에 에이전트를 설치 하는 기존 VM](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx)합니다.

| **작업** | **Windows** | **Linux** |
| --- | --- | --- |
| Hello VM 에이전트 설치 |<li>다운로드 및 설치 hello [에이전트 MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)합니다. 관리자 권한 toocomplete hello 설치를 해야 합니다. <li>[Hello VM 속성을 업데이트](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) 에이전트 hello tooindicate가 설치 되어 있습니다. |<li> Hello 최신 설치 [Linux 에이전트](https://github.com/Azure/WALinuxAgent) GitHub에서 합니다. 관리자 권한 toocomplete hello 설치를 해야 합니다. <li> [Hello VM 속성을 업데이트](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) 에이전트 hello tooindicate가 설치 되어 있습니다. |
| Hello VM 에이전트를 업데이트합니다. |업데이트 hello VM 에이전트를 다시 설치 하는 hello 단순하게 [VM 에이전트 이진](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)합니다. <br><br>Hello VM 에이전트를 업데이트 하는 동안 백업 작업이 수행 되지 실행 되 고 있는지 확인 합니다. |Hello 지침에 따라 [hello Linux VM 에이전트를 업데이트 ](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. <br><br>Hello VM 에이전트를 업데이트 하는 동안 백업 작업이 수행 되지 실행 되 고 있는지 확인 합니다. |
| Hello VM 에이전트 설치 유효성 검사 |<li>Toohello 이동 *C:\WindowsAzure\Packages* hello Azure VM에서에서 폴더입니다. <li>Hello WaAppAgent.exe 파일이 없는 찾아야 합니다.<li> Hello 파일을 마우스 오른쪽 단추로 클릭 한 다음 너무 이동 하십시오**속성**를 선택한 후 hello **세부 정보** 탭 hello 제품 버전 필드 2.6.1198.718 이루어져야 합니다. 이상. |해당 없음 |

Hello에 대 한 자세한 내용은 [VM 에이전트](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) 및 [어떻게 tooinstall 것](https://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/)합니다.

### <a name="backup-extension"></a>백업 확장
hello 가상 컴퓨터를 tooback, hello Azure 백업 서비스 확장 toohello VM 에이전트를 설치합니다. hello Azure 백업 서비스에 원활 하 게 업그레이드 및 추가 사용자 개입 없이 hello 예비 내선 번호를 패치 합니다.

예비 내선 번호 hello hello VM을 실행 하는 경우 설치 됩니다. 또한 실행 중인 VM hello 응용 프로그램 일치 복구 지점의 얻을의 가장 큰 기회를 제공 합니다. 그러나 hello Azure 백업 서비스는 VM-hello tooback 계속 해제 되어, 고 hello 확장 수 없는 경우에 설치 (즉, 오프 라인 VM). 이 경우 hello 복구 지점 수는 *크래시 일관성이 있는* 위에서 설명한 것 처럼 합니다.

## <a name="questions"></a>질문이 있으십니까?
기능의 경우 원하는 toosee 포함 또는 질문이 있는 경우 [피드백](http://aka.ms/azurebackup_feedback)합니다.

## <a name="next-steps"></a>다음 단계
VM를 백업 하기 위한 환경을 준비 했으면, 했으므로 다음 논리 단계는 toocreate 백업 합니다. 문서를 계획 하는 hello Vm을 백업 하는 방법에 대 한 자세한 정보를 제공 합니다.

* [가상 컴퓨터 설정](backup-azure-vms.md)
* [VM 백업 인프라 계획](backup-azure-vms-introduction.md)
* [가상 컴퓨터 백업 관리](backup-azure-manage-vms.md)
