---
title: "PowerShell 사용 하 여 Windows VM aaaCreate | Microsoft Docs"
description: "Azure PowerShell을 hello 클래식 배포 모델을 사용 하 여 Windows 가상 컴퓨터를 만듭니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 42c0d4be-573c-45d1-b9b0-9327537702f7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 5339f458c1f08f6e1752a53191f19402fab8ea25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-hello-classic-deployment-model"></a>PowerShell 및 hello 클래식 배포 모델에서 Windows 가상 컴퓨터 만들기
> [!div class="op_single_selector"]
> * [Azure Portal - Windows](tutorial.md)
> * [PowerShell - Windows](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. 너무 방법에 대해 알아봅니다[hello 리소스 관리자 모델을 사용 하 여 이러한 단계를 수행](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

이러한 단계에 만들고 빌딩 블록 방법을 사용 하 여 Windows 기반 Azure 가상 컴퓨터를 미리 구성 하는 toocustomize 집합의 Azure PowerShell 명령 하는 방법을 보여 줍니다. 이 프로세스를 사용 하는 사용자 지정 개발/테스트 또는 IT 전문가 환경 구축 toocreate 여러 명령은 신속 하 게 하는 설정 또는 tooquickly 새 Windows 기반 가상 컴퓨터에 대 한 명령 집합을 만들고 기존 배포를 확장 합니다.

다음 단계에서는 빈 칸 채우기 접근 방식에 따라 Azure PowerShell 명령 집합을 만듭니다. 이 방법은 새 tooPowerShell 또는 방금 tooknow 어떤 값 toospecify에 대해 원하는 구성이 성공적으로 완료 하는 경우 유용할 수 있습니다. 고급 PowerShell 사용자 수 hello 명령을 수행 하 고 hello 변수 ("$"로 시작 하 고 hello 선)에 대 한 고유한 값을 대체 합니다.

아직 수행 하지 않은 경우의 지침에 hello를 사용 하 여 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 로컬 컴퓨터에 Azure PowerShell tooinstall 합니다. 그런 다음 Windows PowerShell 명령 프롬프트를 엽니다.

## <a name="step-1-add-your-account"></a>1단계: 사용자 계정 추가
1. Hello PowerShell 프롬프트에서 입력 **Add-azureaccount** 클릭 **Enter**합니다. 
2. Azure 구독에 연결 된 hello 전자 메일 주소에 입력 하 고 클릭 **계속**합니다. 
3. Hello 계정의 암호를 입력 합니다. 
4. **로그인**을 클릭합니다.

## <a name="step-2-set-your-subscription-and-storage-account"></a>2단계: 구독 및 저장소 계정 설정
Hello Windows PowerShell 명령 프롬프트에서 다음이 명령을 실행 하 여 Azure 구독 및 저장소 계정을 설정 합니다. Hello < 및 > 문자를 포함 하는 hello 따옴표 안의 hello 올바른 이름으로 대체 합니다.

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

Hello 올바른 구독 이름을 hello hello의 hello 출력의 SubscriptionName 속성에서에서 가져올 수 있습니다 **Get-azuresubscription** 명령입니다. Hello hello의 hello 출력의 Label 속성에서에서 hello 올바른 저장소 계정 이름을 가져올 수 있습니다 **Get AzureStorageAccount** hello를 실행 한 후 명령을 **Select-azuresubscription** 명령입니다.

## <a name="step-3-determine-hello-imagefamily"></a>3 단계: hello ImageFamily 확인
다음으로, 해야 toodetermine hello ImageFamily 또는 레이블 값 hello 특정 이미지 해당 toohello toocreate를 원하는 Azure 가상 컴퓨터에 대 한 합니다. 이 명령 사용 하 여 사용 가능한 ImageFamily 값 hello 목록을 얻을 수 있습니다.

    Get-AzureVMImage | select ImageFamily -Unique

다음은 Windows 기반 컴퓨터의 ImageFamily 값에 대한 몇 가지 예입니다.

* Windows Server 2012 R2 Datacenter
* Windows Server 2008 R2 SP1
* Windows Server 2016 Technical Preview 4
* Windows Server 2012의 SQL Server 2012 SP1 Enterprise

원하는 hello 이미지를 찾을 경우 choice 또는 hello PowerShell 스크립팅 환경을 ISE (통합)의 hello 텍스트 편집기의 새 인스턴스를 엽니다. Hello 새 텍스트 파일 또는 hello hello ImageFamily 값으로 대체 되는 PowerShell ISE에 hello 다음을 복사 합니다.

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

경우에 따라 hello 이미지 이름이 hello hello ImageFamily 값 대신 Label 속성입니다. Hello ImageFamily 속성을 사용 하 여 원하는 hello 이미지를 찾지 못한 경우이 명령 사용 하 여 해당 레이블 속성에 의해 hello 이미지를 나열 합니다.

    Get-AzureVMImage | select Label -Unique

이 명령 사용 하 여 hello 오른쪽 이미지를 찾을 경우 choice 또는 hello PowerShell ISE의 hello 텍스트 편집기의 새 인스턴스를 엽니다. Hello 새 텍스트 파일 또는 hello hello 레이블 값으로 대체 되는 PowerShell ISE에 hello 다음을 복사 합니다.

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a>4단계: 명령 집합 작성
새 텍스트 파일 또는 ISE hello 및 다음 hello 변수 값 채우기 및 hello < 및 > 문자를 제거 합니다. 아래 블록의 hello 적절 한 집합을 복사 하 여 설정 명령 hello 나머지를 빌드하십시오. Hello 두 참조 [예제](#examples) hello 최종 결과의 개념에 대 한이 문서의 hello 끝입니다.

다음 두 명령 블록 중 하나를 선택하여 명령 집합을 시작합니다(필수).

옵션 1: 가상 컴퓨터 이름 및 크기를 지정합니다.

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

옵션 2: 이름, 크기 및 가용성 집합 이름을 지정합니다.

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

D, DS 또는 G 시리즈 가상 컴퓨터에 대 한 hello InstanceSize 값, 참조 [가상 컴퓨터와 Azure 클라우드 서비스 크기](https://msdn.microsoft.com/library/azure/dn197896.aspx)합니다.

> [!NOTE]
> Software Assurance와 함께 기업 계약 하 고 Windows 서버 hello tootake 활용 하려는 경우 [하이브리드 사용 혜택](https://azure.microsoft.com/pricing/hybrid-use-benefit/), 추가 된 **-LicenseType** 매개 변수 toohello  **New-azurevmconfig** hello 값을 전달 cmdlet **Windows_Server** 일반적인 hello에 대 한 사용 사례입니다.  업로드 한; 이미지를 사용 하는 확인 hello 혜택을 사용 하는 하이브리드로 hello 갤러리에서에서 독립 실행형 이미지를 사용할 수 없습니다.
> 
> 

필요에 따라 독립 실행형 Windows 컴퓨터에 대 한 hello 로컬 관리자 계정 및 암호를 지정 합니다.

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

강력한 암호를 선택합니다. toocheck의 강도 참조 [암호 검사기: 강력한 암호를 사용 하 여](https://www.microsoft.com/security/pc-security/password-checker.aspx)합니다.

필요에 따라 Windows 컴퓨터 tooan 기존 Active Directory 도메인을 tooadd hello hello 로컬 관리자 계정 및 암호, hello 도메인 및 hello 이름 및 도메인 계정의 암호를 지정 합니다.

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="<FQDN of hello domain that hello machine is joining>"
    $domacctdomain="<domain of hello account that has permission tooadd hello machine toohello domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

Windows 기반 가상 컴퓨터에 대 한 추가 사전 구성 옵션에 대 한 hello에 대 한 hello 구문을 참조 **Windows** 및 **WindowsDomain** 매개 변수 집합에 [ 추가 AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig)합니다.

필요에 따라 hello 가상 컴퓨터를 고정 DIP를 라고 특정 IP 주소를 할당 합니다.

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

특정 IP 주소를 사용할 수 있는지 확인할 수 있습니다.

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

필요에 따라 Azure 가상 네트워크의 hello 가상 컴퓨터 tooa 특정 서브넷을 할당 합니다.

    $vm1 | Set-AzureSubnet -SubnetNames "<name of hello subnet>"

필요에 따라 단일 데이터 디스크 toohello 가상 컴퓨터를 추가 합니다.

    $disksize=<size of hello disk in GB>
    $disklabel="<hello label on hello disk>"
    $lun=<Logical Unit Number (LUN) of hello disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

Active Directory 도메인 컨트롤러 설정 $hcaching 너무 "None"입니다.

Hello 가상 컴퓨터 tooan 기존 부하 분산 된 집합 외부 트래픽에 대해 필요에 따라 추가 합니다.

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of hello internal port>
    $pubport=<port number of hello external port>
    $endpointname="<name of hello endpoint>"
    $lbsetname="<name of hello existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

마지막으로, 이러한 필수 명령 블록 hello 가상 컴퓨터를 만드는 중 하나를 선택 합니다.

옵션 1: 기존 클라우드 서비스에 hello 가상 컴퓨터를 만듭니다.

    New-AzureVM –ServiceName "<short name of hello cloud service>" -VMs $vm1

hello hello 클라우드 서비스의 짧은 이름에는 클라우드 서비스의 hello Azure 포털 또는 hello Azure 포털에서에서 리소스 그룹의 hello 목록 hello 목록에 표시 된 hello 이름이입니다.

옵션 2: 기존 클라우드 서비스 및 가상 네트워크에 hello 가상 컴퓨터를 만듭니다.

    $svcname="<short name of hello cloud service>"
    $vnetname="<name of hello virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a>5단계: 명령 집합 실행
텍스트 편집기에서 빌드한 hello Azure PowerShell 명령 집합을 검토 하거나 PowerShell ISE 명령 4 단계에서 여러 개의 블록으로 구성 된 hello 합니다. 모든 필요한 hello 변수를 지정 하 고 hello 올바른 값을 가진 것을 확인 합니다. 또한 모든 hello < 및 > 문자를 제거 했는지 확인 합니다.

텍스트 편집기를 사용 하는 경우 복사 hello 명령은 toohello 클립보드를 설정 하 고 열린 Windows PowerShell 명령 프롬프트를 마우스 오른쪽 단추로 클릭 합니다. 이에서는 일련의 PowerShell 명령으로 hello 명령 집합을 발급 하 고 Azure 가상 컴퓨터를 만듭니다. 또는 hello PowerShell ISE에서에서 설정 하는 hello 명령을 실행 합니다.

이 가상 컴퓨터 또는 이와 유사한 가상 컴퓨터를 다시 만들려는 경우 다음과 같이 할 수 있습니다.

* 이 명령 집합을 PowerShell 스크립트 파일(*.ps1)로 저장
* 이 명령은 hello에 Azure 자동화 runbook으로 설정 저장 **자동화 계정을** hello Azure 포털의 섹션입니다.

## <a id="examples"></a>예제
다음은 Windows 기반 Azure 가상 컴퓨터를 만드는 toobuild Azure PowerShell 명령 집합 위에 hello 단계를 사용 하는 두 가지 예입니다.

### <a name="example-1"></a>예 1
PowerShell 필요한 명령 집합, Active Directory 도메인 컨트롤러에 대 한 toocreate hello 초기 가상 컴퓨터를:

* Windows Server 2012 R2 Datacenter 이미지 hello를 사용합니다.
* 이름이 hello AZDC1 합니다.
* 독립 실행형 컴퓨터임
* 20GB의 추가 데이터 디스크가 있음
* Hello 고정 IP 주소 192.168.244.4에 있습니다.
* Hello AZDatacenter 가상 네트워크의 hello 백 엔드 서브넷입니다.
* Hello TailspinToys Azure 클라우드 서비스입니다.

다음 hello 해당 Azure PowerShell 명령 집합 toocreate 가독성을 위해 각 블록 사이 빈 줄이 가상 컴퓨터를은입니다.

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

    $vm1 | Set-AzureSubnet -SubnetNames "BackEnd"

    $vm1 | Set-AzureStaticVNetIP -IPAddress 192.168.244.4

    $disksize=20
    $disklabel="DCData"
    $lun=0
    $hcaching="None"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

### <a name="example-2"></a>예 2
PowerShell 필요한 명령 집합 toocreate 업무의 서버에 대 한 가상 컴퓨터를:

* Windows Server 2012 R2 Datacenter 이미지 hello를 사용합니다.
* 이름이 hello LOB1 합니다.
* Hello corp.contoso.com 도메인의 구성원이입니다.
* 200GB의 추가 데이터 디스크가 있음
* Hello AZDatacenter 가상 네트워크의 hello 프런트 엔드 서브넷입니다.
* Hello TailspinToys Azure 클라우드 서비스입니다.

여기서는 hello 해당 Azure PowerShell 명령 집합 toocreate이 가상 컴퓨터입니다.

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="corp.contoso.com"
    $domacctdomain="CORP"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "FrontEnd"

    $disksize=200
    $disklabel="LOBData"
    $lun=0
    $hcaching="ReadWrite"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname


## <a name="next-steps"></a>다음 단계
127 GB 보다 큰 OS 디스크 해야 할 경우 다음을 할 수 있습니다 [hello 운영 체제 드라이브 확장](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

