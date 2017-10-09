---
title: "aaaLOB 응용 프로그램 테스트 환경 | Microsoft Docs"
description: "어떻게 toocreate는 웹 기반의 비즈니스 응용 프로그램에는 하이브리드 클라우드 환경에 대 한 자세한 내용은 IT pro 또는 개발 테스트 합니다."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 92d2d8ce-60ed-4512-95e5-a7fe3b0ca00b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: e9f825bbb1cbeb841ee3c974ebf6721dc236c311
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a>테스트용 하이브리드 클라우드에 웹 기반 LOB 응용 프로그램 설치
이 항목에서는 Microsoft Azure에서 호스트되는 웹 기반 LOB(기간 업무) 응용 프로그램을 테스트하기 위한 시뮬레이션된 하이브리드 클라우드 환경을 만드는 과정을 안내합니다. 다음은 hello 결과 구성입니다.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

이 구성은 다음과 같이 구성됩니다.

* (테스트 랩 VNet hello) Azure에서 호스팅되는 시뮬레이션 된 온-프레미스 네트워크입니다.
* Azure에서 호스트되는 크로스-프레미스 가상 네트워크(TestVNET)
* VNet 간 VPN 연결
* 웹 기반 LOB 서버, SQL server 및 hello TestVNET 가상 네트워크의 보조 도메인 컨트롤러입니다.

이 구성은 다음 작업을 수행할 수 있는 기초 및 일반적인 시작 지점을 제공합니다.

* Azure에서 SQL Server 2014 데이터베이스 백 엔드를 사용하여 IIS(인터넷 정보 서비스)에서 호스트되는 LOB 응용 프로그램 개발 및 테스트
* 이 시뮬레이션된 하이브리드 클라우드 기반 IT 워크로드의 테스트 수행

이 하이브리드 클라우드 테스트 환경 구축 하는 세 가지 주요 단계 toosetting 가지가 있습니다.

1. Hello 시뮬레이션 된 하이브리드 클라우드 환경을 설정 합니다.
2. Hello SQL server 컴퓨터 (SQL1)를 구성 합니다.
3. Hello LOB 서버 (LOB1)를 구성 합니다.

이 워크로드에는 Azure 구독이 필요합니다. MSDN 또는 Visual Studio 구독이 있는 경우에는 [Visual Studio 구독자를 위한 월간 Azure 크레딧](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 참조하세요.

프로덕션 Azure에서 호스팅되는 LOB 응용 프로그램의 예를 들어 참조 hello **업무용 응용 프로그램** 에서 아키텍처 청사진 [Microsoft 소프트웨어 아키텍처 다이어그램 및 청사진](http://msdn.microsoft.com/dn630664)합니다.

## <a name="phase-1-set-up-hello-simulated-hybrid-cloud-environment"></a>1 단계: hello 시뮬레이션 된 하이브리드 클라우드 환경 설정
Hello 만들기 [시뮬레이션 된 하이브리드 클라우드 테스트 환경](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 이 테스트 환경을 hello hello APP1 서버 hello Corpnet 서브넷에 있는지에 필요 하지 않으면 때문에 당분간를 종료 수 있습니다.

다음은 현재 구성입니다.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-hello-sql-server-computer-sql1"></a>2 단계: 구성 hello SQL server 컴퓨터 (SQL1)
Hello Azure 포털에서에서 필요한 경우 hello DC2 컴퓨터를 시작 합니다.

그런 다음 로컬 컴퓨터의 Azure PowerShell 명령 프롬프트에서 다음 명령을 사용하여 SQL1용 가상 컴퓨터를 만듭니다. 이전 toorunning hello 변수 값 및 제거 hello < 및 > 문자에서 이러한 명령을 입력 합니다.

    $rgName="<your resource group name>"
    $locName="<hello Azure location of your resource group>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName SQL1 -VMSize Standard_A4
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-SQLDataDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name "Data" -DiskSizeInGB 100 -VhdUri $vhdURI  -CreateOption empty

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for hello SQL Server computer." 
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName SQL1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftSQLServer -Offer SQL2014-WS2012R2 -Skus Standard -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

S q l 1의 hello 로컬 관리자 계정을 사용 하 여 Azure 포털 tooconnect tooSQL1 hello를 사용 합니다.

Windows 방화벽 규칙 tooallow 기본 연결 테스트 및 SQL Server 트래픽 다음으로 구성 합니다. SQL1의 관리자 수준 Windows PowerShell 명령 프롬프트에서 다음 명령을 실행합니다.

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

IP 주소 192.168.0.4에서에서 4 개의 성공 응답 hello ping 명령을 발생 해야 합니다.

다음으로 hello 추가 hello 드라이브 문자 f: 새 볼륨으로 s q l 1에서 추가 데이터 디스크.

1. Hello 왼쪽된 창에서 서버 관리자의을 클릭 **파일 및 저장소 서비스**, 클릭 하 고 **디스크**합니다.
2. Hello 내용 창의 hello **디스크** 그룹에서 클릭 **2 디스크** (hello로 **파티션** 도**알 수 없는**).
3. **작업**을 클릭한 후 **새 볼륨**을 클릭합니다.
4. Hello hello 새 볼륨 마법사의 페이지를 시작 하기 전에 클릭 **다음**합니다.
5. Hello 선택 hello 서버 및 디스크 페이지에서 클릭 **디스크 2**, 클릭 하 고 **다음**합니다. 메시지가 표시되면 **확인**을 클릭합니다.
6. Hello hello 볼륨 페이지의 hello 크기 지정, 클릭 **다음**합니다.
7. Hello 할당 tooa 드라이브 문자 또는 폴더 페이지를 클릭 **다음**합니다.
8. Hello 선택 파일 시스템 설정 페이지에서 클릭 **다음**합니다.
9. 선택 확인 페이지 hello 클릭 **만들기**합니다.
10. 완료되면 **닫기**를 클릭합니다.

S q l 1 hello Windows PowerShell 명령 프롬프트에서 이러한 명령을 실행 합니다.

    md f:\Data
    md f:\Log
    md f:\Backup

다음에 s q l 1 hello Windows PowerShell 프롬프트에서 다음이 명령 사용 하 여 s q l 1 toohello 회사 Windows Server Active Directory 도메인에 가입 합니다.

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

메시지가 나타나면 CORP\User1 hello 계정을 사용 하 여 hello에 대 한 도메인 계정 자격 증명 toosupply **Add-computer** 명령입니다.

를 다시 시작한 후 Azure 포털 tooconnect tooSQL1 hello를 사용 하 여 *s q l 1의 hello 로컬 관리자 계정으로*합니다.

다음으로, 사용자 계정 권한을 새 데이터베이스에 대해 SQL Server 2014 toouse hello f: 드라이브를 구성 합니다.

1. Hello 시작 화면에서 입력 **SQL Server Management**, 클릭 하 고 **SQL Server 2014 Management Studio**합니다.
2. **tooServer 연결**, 클릭 **연결**합니다.
3. Hello 개체 탐색기 트리 창에서 마우스 오른쪽 단추로 클릭 **SQL1**, 클릭 하 고 **속성**합니다.
4. Hello에 **서버 속성** 창 클릭 **데이터베이스 설정**합니다.
5. Hello 찾을 **데이터베이스 기본 위치** 이러한 값을 설정 합니다. 
   * 에 대 한 **데이터**, hello 경로 형식의 **f:\Data**합니다.
   * 에 대 한 **로그**, hello 경로 형식의 **f:\Log**합니다.
   * 에 대 한 **백업**, hello 경로 형식의 **f:\Backup**합니다.
   * 참고: 새 데이터베이스에서만 이러한 위치를 사용합니다.
6. Hello 클릭 **확인** tooclose hello 창.
7. Hello에 **개체 탐색기** 트리 창에서 열기 **보안**합니다.
8. **로그인**을 마우스 오른쪽 단추로 클릭하고 **새 로그인**을 클릭합니다.
9. **로그인 이름**에 **CORP\User1**을 입력합니다.
10. Hello에 **서버 역할** 페이지 **sysadmin**, 클릭 하 고 **확인**합니다.
11. Microsoft SQL Server Management Studio를 닫습니다.

다음은 현재 구성입니다.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-hello-lob-server-lob1"></a>3 단계: hello LOB 서버 (LOB1)를 구성 합니다.
먼저 로컬 컴퓨터에 hello Azure PowerShell 명령 프롬프트에서 다음이 명령을 사용 하 여 LOB1에 대 한 가상 컴퓨터를 만듭니다.

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName LOB1 -VMSize Standard_A2
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for LOB1."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName LOB1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/LOB1-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name LOB1-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

를 사용 하 여 hello Azure 포털 tooconnect tooLOB1 LOB1의 hello 로컬 관리자 계정의 hello 자격 증명을 사용 합니다.

다음으로 기본 연결을 테스트 하는 것에 대 한 Windows 방화벽 규칙 tooallow 트래픽을 구성 합니다. LOB1의 관리자 수준 Windows PowerShell 명령 프롬프트에서 다음 명령을 실행합니다.

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

IP 주소 192.168.0.4에서에서 4 개의 성공 응답 hello ping 명령을 발생 해야 합니다.

다음으로 hello Windows PowerShell 프롬프트에서 다음이 명령 사용 하 여 LOB1 toohello CORP Active Directory 도메인에 가입 합니다.

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

메시지가 나타나면 CORP\User1 hello 계정을 사용 하 여 hello에 대 한 도메인 계정 자격 증명 toosupply **Add-computer** 명령입니다.

를 다시 시작한 후 Azure 포털 tooconnect tooLOB1 hello를 사용 하 여 hello CORP\User1 계정 및 암호를 사용 합니다.

그런 다음 IIS에 대해 LOB1을 구성하고 CLIENT1의 액세스를 테스트합니다.

1. 서버 관리자에서 **역할 및 기능 추가**를 클릭합니다.
2. Hello에 **시작 하기 전에** 페이지 **다음**합니다.
3. Hello에 **설치 유형 선택** 페이지 **다음**합니다.
4. Hello에 **대상 서버 선택** 페이지 **다음**합니다.
5. Hello에 **서버 역할** 페이지 **웹 서버 (IIS)** hello 목록에 **역할**합니다.
6. 메시지가 나타나면 **기능 추가**를 클릭하고 **다음**을 클릭합니다.
7. Hello에 **기능 선택** 페이지 **다음**합니다.
8. Hello에 **웹 서버 (IIS)** 페이지 **다음**합니다.
9. Hello에 **역할 서비스 선택** 페이지 선택 또는 hello LOB 응용 프로그램 테스트에 필요한 hello 서비스에 대 한 확인란의 선택을 취소 하 고 클릭 **다음**합니다.
10. Hello에 **설치 선택 확인** 페이지 **설치**합니다.
11. 구성 요소의 hello 설치가 완료 될 때까지 기다린 후 클릭 **닫기**합니다.
12. Hello Azure 포털에서에서 hello CORP\User1 계정 자격 증명을 사용 하 여 toohello CLIENT1 컴퓨터를 연결 하 고 Internet Explorer를 시작 합니다.
13. Hello 주소 표시줄에 입력 **http://lob1/** 한 다음 ENTER 키를 누릅니다. Hello 기본 IIS 8 웹 페이지 표시 되어야 합니다.

다음은 현재 구성입니다.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

이 환경은 이제 웹 기반 응용 프로그램 LOB1 및 테스트 하는 기능에 CLIENT1에서 hello Corpnet 서브넷에 대기 중인 toodeploy 있습니다.

## <a name="next-step"></a>다음 단계
* Hello를 사용 하 여 새 가상 컴퓨터를 추가 [Azure 포털](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

