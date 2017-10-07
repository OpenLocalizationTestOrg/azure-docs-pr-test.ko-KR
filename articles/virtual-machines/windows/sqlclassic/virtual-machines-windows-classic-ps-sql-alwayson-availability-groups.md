---
title: "aaaConfigure hello Always On 가용성 그룹에 PowerShell을 사용 하 여 Azure VM | Microsoft Docs"
description: "이 자습서에서는 hello 클래식 배포 모델을 사용 하 여 만든 리소스를 사용 합니다. Azure에서 PowerShell toocreate Always On 가용성 그룹을 사용합니다."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a4e2f175-fe56-4218-86c7-a43fb916cc64
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: d4a27e203b2ff299adebec2b010c03422459b3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-always-on-availability-group-on-an-azure-vm-with-powershell"></a>PowerShell과 함께 Azure VM에서 hello Always On 가용성 그룹을 구성 합니다.
> [!div class="op_single_selector"]
> * [클래식: UI](../classic/portal-sql-alwayson-availability-groups.md)
> * [클래식: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
<br/>

시작하기 전에 이제 Azure Resource Manager 모델에서 이 작업을 완료할 수 있는지 확인하는 것이 좋습니다. 새 배포에는 Azure Resource Manager 모델을 사용하는 것이 좋습니다. [Azure Virtual Machines의 SQL Server Always On 가용성 그룹](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md)을 참조하세요.

> [!IMPORTANT]
> 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.

Azure 가상 컴퓨터 (Vm)는 고가용성 SQL Server 시스템의 데이터베이스 관리자가 toolower hello 비용을 시킬 수 있습니다. 이 자습서에서는 SQL Server Always On-종단 Azure 환경 내를 사용 하 여 가용성 tooimplement 그룹화 하는 방법을 보여 줍니다. Hello 자습서의 hello 끝 요소 다음 hello Azure에서 SQL Server Always On 솔루션 구성 됩니다.

* 프런트 엔드 및 백 엔드 서브넷을 비롯한 여러 서브넷을 포함하는 가상 네트워크
* Active Directory 도메인을 포함한 도메인 컨트롤러
* 배포 된 toohello 백 엔드 서브넷 및 Active Directory 도메인에 가입된 toohello 두 SQL Server Vm
* Hello 노드 과반수 쿼럼 모델 3 노드 Windows 장애 조치 클러스터입니다.
* 가용성 데이터베이스의 동기 커밋 복제본 두 개가 포함된 가용성 그룹

이 시나리오의 좋은 점은 비용 효율성이나 다른 요소가 아닌 Azure에서의 간소함입니다. 예를 들어 hello 2 개 노드 장애 조치 클러스터에서 쿼럼 파일 공유 감시로 hello 도메인 컨트롤러를 사용 하 여 Azure에서 계산 시간 hello 2 복제본 가용성 그룹 toosave에 대 한 Vm 수를 최소화할 수 있습니다. 이 메서드는 hello 구성 이상에서 씩 hello VM 수를 줄입니다.

이 자습서는 단계를 필요한 tooset hello hello tooshow 각 단계의 hello 세부 사항까지 설명 하지 않고 솔루션 위에서 설명 것입니다. 따라서 대신 제공 하는 hello GUI 구성 단계를 사용 하 여 PowerShell tootake 스크립팅을 통해 신속 하 게 각 한 단계씩 합니다. 이 자습서에서는 hello 다음을 가정합니다.

* 가상 컴퓨터 구독이 hello는 Azure 계정이 이미 있습니다.
* 이전에 설치한 hello [Azure PowerShell cmdlet](/powershell/azure/overview)합니다.
* 온-프레미스 솔루션에 대한 Always On 가용성 그룹을 확실하게 이해하고 있습니다. 자세한 내용은 [Always On 가용성 그룹(SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx)을 참조하세요.

## <a name="connect-tooyour-azure-subscription-and-create-hello-virtual-network"></a>Tooyour Azure 구독을 연결 하 고 hello 가상 네트워크 만들기
1. 로컬 컴퓨터의 PowerShell 창에서 hello Azure 모듈을 가져올 게시 설정 파일 tooyour 컴퓨터 hello를 다운로드 하 여 hello 다운로드 한 게시 설정을 가져와서 PowerShell 세션 tooyour Azure 구독을 연결 합니다.

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    hello **Get-azurepublishsettingsfile** 명령에서 자동으로 azure 관리 인증서를 생성 하 고 tooyour 컴퓨터를 다운로드 합니다. 브라우저는 자동으로 열리고 Azure 구독에 대 한 증명된 tooenter hello Microsoft 계정 자격 증명을 하는. 다운로드 한 hello **.publishsettings** 파일 모든 hello 필요한 정보를 toomanage Azure 구독에 포함 되어 있습니다. 이 파일 tooa 로컬 디렉터리를 저장 한 후 hello를 사용 하 여 가져올 **Import-azurepublishsettingsfile** 명령입니다.

   > [!NOTE]
   > hello.publishsettings 파일은 Azure 구독 및 서비스 사용자 자격 증명 (인코딩되지 않음)을 사용 하는 tooadminister를 포함 합니다. 이 파일에 대 한 보안 모범 사례 hello toostore은 일시적으로 원본 디렉터리 외부 (예를 들어 hello: Libraries\Documents 폴더), 그 다음 hello 가져오기 완료 된 후 삭제 합니다. Access toohello.publishsettings 파일을 얻은 악의적인 사용자는 수 편집 만들고 Azure 서비스를 삭제 합니다.

2. 일련의 합니다를 사용 하는 toocreate 클라우드 IT 인프라 변수를 정의 합니다.

        $location = "West US"
        $affinityGroupName = "ContosoAG"
        $affinityGroupDescription = "Contoso SQL HADR Affinity Group"
        $affinityGroupLabel = "IaaS BI Affinity Group"
        $networkConfigPath = "C:\scripts\Network.netcfg"
        $virtualNetworkName = "ContosoNET"
        $storageAccountName = "<uniquestorageaccountname>"
        $storageAccountLabel = "Contoso SQL HADR Storage Account"
        $storageAccountContainer = "https://" + $storageAccountName + ".blob.core.windows.net/vhds/"
        $winImageName = (Get-AzureVMImage | where {$_.Label -like "Windows Server 2008 R2 SP1*"} | sort PublishedDate -Descending)[0].ImageName
        $sqlImageName = (Get-AzureVMImage | where {$_.Label -like "SQL Server 2012 SP1 Enterprise*"} | sort PublishedDate -Descending)[0].ImageName
        $dcServerName = "ContosoDC"
        $dcServiceName = "<uniqueservicename>"
        $availabilitySetName = "SQLHADR"
        $vmAdminUser = "AzureAdmin"
        $vmAdminPassword = "Contoso!000"
        $workingDir = "c:\scripts\"

    명령을 나중에 성공할 tooensure 다음 주의 toohello 지불:

   * 변수 **$storageAccountName** 및 **$dcServiceName** 이기 때문에 고유 해야 tooidentify 클라우드 저장소 계정과 클라우드 서버를 각각 사용, 인터넷 hello에 있습니다.
   * 변수에 대 한 지정한 이름과 hello **$affinityGroupName** 및 **$virtualNetworkName** hello 나중에 사용할 가상 네트워크 구성 문서에 구성 되어 있습니다.
   * **$sqlImageName** SQL Server 2012 서비스 팩 1 Enterprise Edition을 포함 하는 hello VM 이미지의 업데이트 hello 이름을 지정 합니다.
   * 간단한 설명을 위해 **Contoso! 000** 동일 hello는 hello 전체 자습서 전체에서 사용 되는 암호입니다.

3. 선호도 그룹을 만듭니다.

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. 구성 파일을 가져와서 가상 네트워크를 만듭니다.

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    hello 구성 파일에 다음 XML 문서 hello 포함 되어 있습니다. 이라는 가상 네트워크를 지정 간단히 말해서 **ContosoNET** 라는 hello 선호도 그룹에 **ContosoAG**합니다. Hello 주소 공간 **10.10.0.0/16** 있으며, 두 서브넷 **10.10.1.0/24** 및 **10.10.2.0/24**, 않는 hello 프런트 서브넷과 백 서브넷인 각각. hello 프런트 서브넷은 Microsoft SharePoint와 같은 클라이언트 응용 프로그램을 배치할 수 있습니다. hello 백 서브넷은 hello SQL Server Vm을 배치할 수 있습니다. Hello를 변경 하는 경우 **$affinityGroupName** 및 **$virtualNetworkName** 변수 이전에 변경 해야 hello 이름 아래에 해당 합니다.

        <NetworkConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <Dns />
            <VirtualNetworkSites>
              <VirtualNetworkSite name="ContosoNET" AffinityGroup="ContosoAG">
                <AddressSpace>
                  <AddressPrefix>10.10.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="Front">
                    <AddressPrefix>10.10.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="Back">
                    <AddressPrefix>10.10.2.0/24</AddressPrefix>
                  </Subnet>
                </Subnets>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

5. Hello 선호도 그룹을 만든 구독에 hello 현재 저장소 계정으로 설정 하와 연결 된 저장소 계정을 만듭니다.

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. Hello 새 클라우드 서비스 및 가용성 집합의 hello 도메인 컨트롤러 서버를 만듭니다.

        New-AzureVMConfig `
            -Name $dcServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$dcServerName.vhd" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -Windows `
                -DisableAutomaticUpdates `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword |
                New-AzureVM `
                    -ServiceName $dcServiceName `
                    –AffinityGroup $affinityGroupName `
                    -VNetName $virtualNetworkName

    이러한 파이프 된 명령은 다음 작업 hello지 않습니다.

   * **New-AzureVMConfig** 는 VM 구성을 만듭니다.
   * **추가 AzureProvisioningConfig** 제공 hello 독립 실행형 Windows 서버의 구성 매개 변수입니다.
   * **추가 AzureDataDisk** 하는 옵션 집합 tooNone 캐싱 hello로 Active Directory 데이터를 저장 하는 데 사용할 hello 데이터 디스크를 추가 합니다.
   * **새 AzureVM** 새 클라우드 서비스를 만들고 만듭니다 hello 새 클라우드 서비스에서 새 Azure VM hello 합니다.

7. Hello 새 VM toobe 완전히 프로 비전 기다렸다가 hello 원격 데스크톱 파일 tooyour 작업 디렉터리를 다운로드 합니다. 를 하기 때문에 hello 새 Azure VM 오랜 시간이 tooprovision hello `while` 루프가 toopoll 사용할 준비가 될 때까지 새 VM을 hello 합니다.

        $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName

        While ($VMStatus.InstanceStatus -ne "ReadyRole")
        {
            write-host "Waiting for " $VMStatus.Name "... Current Status = " $VMStatus.InstanceStatus
            Start-Sleep -Seconds 15
            $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName
        }

        Get-AzureRemoteDesktopFile `
            -ServiceName $dcServiceName `
            -Name $dcServerName `
            -LocalPath "$workingDir$dcServerName.rdp"

hello 도메인 컨트롤러 서버는 이제 성공적으로 프로 비전 합니다. 다음으로,이 도메인 컨트롤러 서버에는 hello Active Directory 도메인을 구성 합니다. 로컬 컴퓨터에 hello PowerShell 창을 열어 둡니다. 사용 않으려는 다시 이후 toocreate hello 두 SQL Server Vm입니다.

## <a name="configure-hello-domain-controller"></a>Hello 도메인 컨트롤러 구성
1. Hello 원격 데스크톱 파일을 시작 하 여 toohello 도메인 컨트롤러 서버를 연결 합니다. Hello 컴퓨터 관리자의 AzureAdmin 사용자 이름과 암호를 사용 하 여 **Contoso! 000**를 만들 때 지정 하는 새 VM hello 합니다.
2. 관리자 모드에서 PowerShell 창을 엽니다.
3. Hello 다음 실행 **DCPROMO 합니다. EXE** hello 명령 tooset **corp.contoso.com** M 드라이브에 데이터 디렉터리 hello와 도메인입니다.

        dcpromo.exe `
            /unattend `
            /ReplicaOrNewDomain:Domain `
            /NewDomain:Forest `
            /NewDomainDNSName:corp.contoso.com `
            /ForestLevel:4 `
            /DomainNetbiosName:CORP `
            /DomainLevel:4 `
            /InstallDNS:Yes `
            /ConfirmGc:Yes `
            /CreateDNSDelegation:No `
            /DatabasePath:"C:\Windows\NTDS" `
            /LogPath:"C:\Windows\NTDS" `
            /SYSVOLPath:"C:\Windows\SYSVOL" `
            /SafeModeAdminPassword:"Contoso!000"

    Hello 명령이 완료 된 후 자동으로 hello VM 다시 시작 합니다.

4. Hello 원격 데스크톱 파일을 시작 하 여 toohello 도메인 컨트롤러 서버를 다시 연결 합니다. 이번에는 **CORP\Administrator**로 로그인합니다.
5. 관리자 모드에서 PowerShell 창을 열고 hello 다음 명령을 사용 하 여 hello Active Directory PowerShell 모듈을 가져오려면:

        Import-Module ActiveDirectory

6. 다음 명령을 tooadd 세 개의 사용자 toohello 도메인 hello를 실행 합니다.

        $pwd = ConvertTo-SecureString "Contoso!000" -AsPlainText -Force
        New-ADUser `
            -Name 'Install' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc1' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc2' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true

    **CORP\Install** tooconfigure 사용 되는 모든 항목은 관련 toohello SQL Server 서비스 인스턴스, 장애 조치 클러스터 hello hello 가용성 그룹입니다. **CORP\SQLSvc1** 및 **CORP\SQLSvc2** hello 두 SQL Server Vm에 대 한 hello SQL Server 서비스 계정으로 사용 됩니다.
7. 다음을 실행 하는 hello 다음 명령을 toogive **CORP\Install** hello hello 도메인에서 권한을 toocreate 컴퓨터 개체입니다.

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    hello 위에서 지정한 GUID는 hello 컴퓨터 개체 유형에 대 한 hello GUID입니다. hello **CORP\Install** 계정 필요한 hello **모든 속성 읽기** 및 **컴퓨터 개체 만들기** hello 장애 조치에 대 한 개체 사용 권한 toocreate hello 활성 직접 클러스터입니다. hello **모든 속성 읽기** 권한이 부여 되어 tooCORP\Install 기본적으로 toogrant 필요는 없습니다 것 명시적으로 합니다. 권한에 대 한 자세한 내용은 필요한 toocreate hello 장애 조치 클러스터에 대 한 참조 [장애 조치 클러스터 단계별 가이드: Active Directory에서 계정 구성](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx)합니다.

    Active Directory와 hello 사용자 개체의 구성을 완료 했으므로 다음에 두 SQL Server Vm을 만들 고 toothis 도메인에 가입 합니다.

## <a name="create-hello-sql-server-vms"></a>Hello SQL Server Vm 만들기
1. 로컬 컴퓨터에서 열려 있는 toouse hello PowerShell 창을 계속 합니다. Hello 다음 추가 변수를 정의 합니다.

        $domainName= "corp"
        $FQDN = "corp.contoso.com"
        $subnetName = "Back"
        $sqlServiceName = "<uniqueservicename>"
        $quorumServerName = "ContosoQuorum"
        $sql1ServerName = "ContosoSQL1"
        $sql2ServerName = "ContosoSQL2"
        $availabilitySetName = "SQLHADR"
        $dataDiskSize = 100
        $dnsSettings = New-AzureDns -Name "ContosoBackDNS" -IPAddress "10.10.0.4"

    IP 주소를 hello **10.10.0.4** toohello는 일반적으로 할당 hello에서 만드는 첫 번째 VM **10.10.0.0/16** Azure 가상 네트워크의 서브넷입니다. 실행 하 여 hello 서버의 주소를 도메인 컨트롤러 인지 확인 해야 **IPCONFIG**합니다.
2. 다음 파이프 된 명령은 toocreate hello를 먼저 실행된 hello hello 장애 조치 클러스터의 VM 이름이 **ContosoQuorum**:

        New-AzureVMConfig `
            -Name $quorumServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$quorumServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    New-AzureVM `
                        -ServiceName $sqlServiceName `
                        –AffinityGroup $affinityGroupName `
                        -VNetName $virtualNetworkName `
                        -DnsSettings $dnsSettings

    위의 hello 명령에 대 한 hello 다음 note:

   * **New-azurevmconfig** hello 원하는 가용성 집합 이름을 사용 하 여 VM 구성을 만듭니다. hello 다음 Vm 만들어집니다 hello로 동일한 가용성 집합 이름이 가입 하는 되도록 toohello 동일한 가용성 집합입니다.
   * **추가 AzureProvisioningConfig** 조인 hello 만든 VM toohello Active Directory 도메인.
   * **Set-azuresubnet** 장소 hello 백 서브넷에 VM을 hello 합니다.
   * **새 AzureVM** 새 클라우드 서비스를 만들고 만듭니다 hello 새 클라우드 서비스에서 새 Azure VM hello 합니다. hello **DnsSettings** hello hello 새 클라우드 서비스의 서버에서 hello IP 주소에 대 한 매개 변수를 해당 hello DNS 서버 지정 **10.10.0.4**합니다. 도메인 컨트롤러 서버 hello의 hello IP 주소입니다. 이 매개 변수는 필요 tooenable hello 클라우드 서비스 toojoin toohello Active Directory 도메인에 새 Vm을 성공적으로 hello 합니다. 이 매개 변수가 없으면 수동으로 설정 해야 hello IPv4 설정을 VM toouse hello 도메인 컨트롤러 서버에서 hello 주 DNS 서버로 hello VM 프로 비전 되 고 다음 hello VM toohello Active Directory 도메인에 가입 합니다.
3. 명명 된 SQL Server Vm toocreate hello 명령 실행된 hello 다음 파이프 된 **ContosoSQL1** 및 **ContosoSQL2**합니다.

        # Create ContosoSQL1...
        New-AzureVMConfig `
            -Name $sql1ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql1ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 1 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

        # Create ContosoSQL2...
        New-AzureVMConfig `
            -Name $sql2ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql2ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 2 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

    위 hello 명령에 대 한 hello 다음 note:

   * **New-azurevmconfig** 사용 하 여 hello hello 도메인 컨트롤러 서버와 동일한 가용성 집합 이름을 사용 하 여 hello hello 가상 컴퓨터 갤러리의 SQL Server 2012 서비스 팩 1 엔터프라이즈 버전 이미지 및 합니다. 또한 운영 체제 디스크 tooread 캐싱 전용 (쓰기 캐싱이 아닌) hello를 설정 합니다. Hello 데이터베이스 파일 tooa 별도 데이터 디스크는 연결 toohello VM 및 없는 읽기 사용 하 여 구성 하거나 쓰기 캐싱을 마이그레이션하는 것이 좋습니다. 그러나 hello 차선책은 hello 운영 체제 디스크에 대 한 캐싱을 읽기 tooremove 제거할 수는 없으므로 쓰기 hello 운영 체제 디스크에 캐시 합니다.
   * **추가 AzureProvisioningConfig** 조인 hello 만든 VM toohello Active Directory 도메인.
   * **Set-azuresubnet** 장소 hello 백 서브넷에 VM을 hello 합니다.
   * **추가 AzureEndpoint** 클라이언트 응용 프로그램 hello 인터넷에서 이러한 SQL Server 서비스 인스턴스에 액세스할 수 있도록 액세스 끝점을 추가 합니다. TooContosoSQL1 및 ContosoSQL2 서로 다른 포트가 제공 됩니다.
   * **새 AzureVM** 만듭니다 새 SQL Server VM hello hello에서 동일한 클라우드 서비스 ContosoQuorum으로 합니다. 동일한 클라우드 서비스 하려는 경우에 toobe hello hello Vm을 배치 해야 hello 동일한 가용성 집합입니다.
4. 각 VM toodownload 및 각 VM toobe 완전히 프로 비전에 대 한 원격 데스크톱 파일 tooyour 작업 디렉터리로를 기다립니다. hello `for` 루프 세 개의 새로운 Vm hello을 순환 하 고 각각의 hello 최상위 중괄호 안의 hello 명령을 실행 합니다.

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until hello VM status is "ReadyRole"
            While ($VM.InstanceStatus -ne "ReadyRole")
            {
                write-host "  Current Status = " $VM.InstanceStatus
                Start-Sleep -Seconds 15
                $VM = Get-AzureVM -ServiceName $VM.ServiceName -Name $VM.InstanceName
            }

            write-host "  Current Status = " $VM.InstanceStatus

            # Download remote desktop file
            Get-AzureRemoteDesktopFile -ServiceName $VM.ServiceName -Name $VM.InstanceName -LocalPath "$workingDir$($VM.InstanceName).rdp"
        }

    hello SQL Server Vm이 이제 프로 비전 하 고 실행 되지만 SQL Server와 함께 기본 옵션으로 설치 하는 키를 누릅니다.

## <a name="initialize-hello-failover-cluster-vms"></a>Hello 장애 조치 클러스터 Vm 초기화
이 섹션에는 hello 장애 조치 클러스터와 hello SQL Server 설치에 사용할 toomodify hello 3 명의 서버가 필요 합니다. 구체적으로 살펴보면 다음과 같습니다.

* 모든 서버: tooinstall hello 필요한 **장애 조치 클러스터링** 기능입니다.
* 모든 서버: tooadd 필요한 **CORP\Install** hello 컴퓨터로 **관리자**합니다.
* ContosoSQL1 및 ContosoSQL2만: tooadd 필요한 **CORP\Install** 로 **sysadmin** hello 기본 데이터베이스의 역할입니다.
* ContosoSQL1 및 ContosoSQL2만: tooadd 필요한 **NT AUTHORITY\System** 다음 권한을 hello로 로그인 기능으로:

  * 가용성 그룹 변경
  * SQL 연결
  * 서버 상태 보기
* ContosoSQL1 및 ContosoSQL2만: hello **TCP** 프로토콜이 hello SQL Server VM에서 이미 설정 되어 있습니다. 그러나 여전히 tooopen hello 방화벽에 필요한 SQL Server의 원격 액세스 합니다.

이제 준비 toostart 것입니다. 부터는 **ContosoQuorum**, 아래의 hello 단계를 수행 합니다.

1. 너무 연결**ContosoQuorum** hello 원격 데스크톱 파일을 시작 하 여 합니다. Hello 컴퓨터 관리자의 이름을 사용 하 여 **AzureAdmin** 및 암호 **Contoso! 000**, hello Vm을 만들 때 지정 합니다.
2. hello 컴퓨터 성공적으로 가입한 너무 확인**corp.contoso.com**합니다.
3. 계속 하기 전에 hello 자동화 된 초기화 작업을 실행 하는 hello SQL Server 설치 toofinish 될 때까지 기다립니다.
4. 관리자 모드에서 PowerShell 창을 엽니다.
5. Hello Windows 장애 조치 클러스터링 기능을 설치 합니다.

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. **CORP\Install**을 로컬 관리자로 추가합니다.

        net localgroup administrators "CORP\Install" /Add
7. ContosoQuorum에서 로그아웃합니다. 이제 이 서버에서는 작업을 마쳤습니다.

        logoff.exe

다음으로 **ContosoSQL1** 및 **ContosoSQL2**를 초기화합니다. 두 SQL Server Vm에 대 한 동일한 hello 단계 아래를 따릅니다.

1. Hello 원격 데스크톱 파일을 시작 하 여 toohello 두 SQL Server Vm을 연결 합니다. Hello 컴퓨터 관리자의 이름을 사용 하 여 **AzureAdmin** 및 암호 **Contoso! 000**, hello Vm을 만들 때 지정 합니다.
2. hello 컴퓨터 성공적으로 가입한 너무 확인**corp.contoso.com**합니다.
3. 계속 하기 전에 hello 자동화 된 초기화 작업을 실행 하는 hello SQL Server 설치 toofinish 될 때까지 기다립니다.
4. 관리자 모드에서 PowerShell 창을 엽니다.
5. Hello Windows 장애 조치 클러스터링 기능을 설치 합니다.

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. **CORP\Install**을 로컬 관리자로 추가합니다.

        net localgroup administrators "CORP\Install" /Add
7. Hello를 SQL Server PowerShell 공급자를 가져옵니다.

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. 추가 **CORP\Install** hello 기본 SQL Server 인스턴스에 대 한 hello sysadmin 역할을 합니다.

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. 추가 **NT AUTHORITY\System** 위에서 설명한 세 hello 권한으로 로그인 기능으로 합니다.

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. SQL Server의 원격 액세스에 대 한 hello 방화벽을 엽니다.

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. 두 VM에서 로그아웃합니다.

         logoff.exe

마지막으로 준비 tooconfigure hello 가용성 그룹 것입니다. Hello SQL Server PowerShell 공급자 tooperform에 hello 사용를 사용 하 여 **ContosoSQL1**합니다.

## <a name="configure-hello-availability-group"></a>Hello 가용성 그룹 구성
1. 너무 연결**ContosoSQL1** hello 원격 데스크톱 파일을 시작 하 여 다시 합니다. Hello 컴퓨터 계정을 사용 하 여 로그인 하는 대신 사용 하 여 로그인 **CORP\Install**합니다.
2. 관리자 모드에서 PowerShell 창을 엽니다.
3. Hello 다음 변수를 정의 합니다.

        $server1 = "ContosoSQL1"
        $server2 = "ContosoSQL2"
        $serverQuorum = "ContosoQuorum"
        $acct1 = "CORP\SQLSvc1"
        $acct2 = "CORP\SQLSvc2"
        $password = "Contoso!000"
        $clusterName = "Cluster1"
        $timeout = New-Object System.TimeSpan -ArgumentList 0, 0, 30
        $db = "MyDB1"
        $backupShare = "\\$server1\backup"
        $quorumShare = "\\$server1\quorum"
        $ag = "AG1"
4. Hello를 SQL Server PowerShell 공급자를 가져옵니다.

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. ContosoSQL1 tooCORP\SQLSvc1에 대 한 hello SQL Server 서비스 계정을 변경 합니다.

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. ContosoSQL2 tooCORP\SQLSvc2에 대 한 hello SQL Server 서비스 계정을 변경 합니다.

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. 다운로드 **CreateAzureFailoverCluster.ps1** 에서 [Always On 가용성 그룹에서 Azure VM에 대 한 장애 조치 클러스터 만들기](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello 로컬 작업 디렉터리입니다. 이 스크립트 toohelp 기능 장애 조치 클러스터를 만들고 사용 합니다. Windows 장애 조치 클러스터링과 상호 작용 방식 hello Azure에 대 한 중요 정보에 대 한 네트워크, 참조 [Azure 가상 컴퓨터의 SQL Server에 대 한 고가용성 및 재해 복구](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)합니다.
8. Tooyour 작업 디렉터리를 변경 하 고 다운로드 한 hello 스크립트와 함께 hello 장애 조치 클러스터를 만듭니다.

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. Hello 기본 SQL Server 인스턴스에 대 한 Always On 가용성 그룹에서 사용 하도록 설정 **ContosoSQL1** 및 **ContosoSQL2**합니다.

        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server1\Default `
            -Force
        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server2\Default `
            -NoServiceRestart
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
10. 백업 디렉터리를 만들고 hello SQL Server 서비스 계정에 대 한 권한을 부여 합니다. Hello 보조 복제본에서이 디렉터리 tooprepare hello 가용성 데이터베이스를 사용 합니다.

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. 데이터베이스를 만들 **ContosoSQL1** 호출 **MyDB1**, 전체 백업과 로그 백업을 모두 및에 복원할 **ContosoSQL2** hello로 **WITH NORECOVERY** 옵션입니다.

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. Hello SQL Server Vm에 hello 가용성 그룹 끝점을 만들고 hello 끝점에 hello 적절 한 사용 권한을 설정 하십시오.

         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server1\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"
         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server2\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"

         Invoke-SqlCmd -Query "CREATE LOGIN [$acct2] FROM WINDOWS" -ServerInstance $server1
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct1]" -ServerInstance $server2
13. Hello 가용성 복제본을 만듭니다.

         $primaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server1 `
             -EndpointURL "TCP://$server1.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
         $secondaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server2 `
             -EndpointURL "TCP://$server2.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
14. 마지막으로 hello 가용성 그룹과 조인 hello toohello 가용성 그룹 보조 복제본을 만듭니다.

         New-SqlAvailabilityGroup `
             -Name $ag `
             -Path "SQLSERVER:\SQL\$server1\Default" `
             -AvailabilityReplica @($primaryReplica,$secondaryReplica) `
             -Database $db
         Join-SqlAvailabilityGroup `
             -Path "SQLSERVER:\SQL\$server2\Default" `
             -Name $ag
         Add-SqlAvailabilityDatabase `
             -Path "SQLSERVER:\SQL\$server2\Default\AvailabilityGroups\$ag" `
             -Database $db

## <a name="next-steps"></a>다음 단계
이제 Azure에서 가용성 그룹을 만들어 SQL Server Always On을 성공적으로 구현했습니다. 이 가용성 그룹에 대 한 수신기 tooconfigure 참조 [Azure에서 Always On 가용성 그룹에 대 한 ILB 수신기 구성](../classic/ps-sql-int-listener.md)합니다.

Azure에서 SQL Server를 사용하는 방법에 대한 기타 정보는 [Azure Virtual Machines의 SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.
