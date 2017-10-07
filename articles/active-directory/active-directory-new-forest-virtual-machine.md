---
title: "Azure 가상 네트워크에 Active Directory 포리스트 aaaInstall | Microsoft Docs"
description: "Azure 가상 네트워크에서 가상 컴퓨터 (VM)에서 toocreate 새 Active Directory 포리스트 하는 방법에 대해 설명 하는 자습서입니다."
services: active-directory, virtual-network
keywords: "active directory 가상 컴퓨터, active directory 포리스트 설치, azure active directory 비디오  "
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
tags: 
ms.assetid: eb7170d0-266a-4caa-adce-1855589d65d1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/06/2017
ms.author: joflore
ms.openlocfilehash: 08121130777cc3c206d7b5b38974982884dca1c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-new-active-directory-forest-on-an-azure-virtual-network"></a>Azure 가상 네트워크에 새 Active Directory 포리스트 설치
이 항목에서는 방법을 toocreate 새 Windows Server Active Directory 환경의 가상 컴퓨터 (VM)에서 Azure 가상 네트워크에는 [Azure 가상 네트워크](../virtual-network/virtual-networks-overview.md)합니다. 이 경우 hello Azure 가상 네트워크는 연결 된 tooan 온-프레미스 네트워크 없음.

다음 관련 토픽을 참조할 수도 있습니다.

* 다음이 단계를 보여 주는 비디오를 참조 하십시오. [Azure 가상 네트워크에 tooinstall 새 Active Directory 포리스트 하는 방법](http://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/How-to-install-a-new-Active-Directory-forest-on-an-Azure-virtual-network)
* 필요에 따라 수 [사이트 간 VPN 구성](../vpn-gateway/vpn-gateway-site-to-site-create.md) 새 포리스트 설치 하거나 온-프레미스 포리스트 tooan Azure 가상 네트워크를 확장 합니다. 이러한 단계는 [Azure 가상 네트워크에 복제 Active Directory 도메인 컨트롤러 설치](active-directory-install-replica-active-directory-domain-controller.md)를 참조하세요.
* Azure 가상 네트워크에 AD DS(Active Directory 도메인 서비스)를 설치하는 방법에 대한 개념 지침은 [Azure 가상 컴퓨터에 Windows Server Active Directory 배포에 대한 지침](https://msdn.microsoft.com/library/azure/jj156090.aspx)을 참조하세요.

## <a name="scenario-diagram"></a>시나리오 다이어그램
이 시나리오에서는 외부 사용자 도메인에 가입 된 서버에서 실행 되는 응용 프로그램 tooaccess 필요 합니다. Azure 가상 네트워크에서 자신의 클라우드 서비스에 설치 된 hello 응용 프로그램 서버를 실행 하는 hello Vm 및 도메인 컨트롤러를 실행 하는 hello Vm 설치 됩니다. 또한 내결함성 향상을 위해 가용성 집합 내에도 포함됩니다.

![Azure Virtual Network의 가상 컴퓨터에서 Active Directory 포리스트][1] 7

## <a name="how-does-this-differ-from-on-premises"></a>온-프레미스와의 차이점
Azure에 도메인 컨트롤러를 설치할 때와 온-프레미스에 설치할 때의 차이점은 크지 않습니다. hello 주요 차이점은 다음 표에 hello에 나열 됩니다.

| tooconfigure 중... | 온-프레미스 | Azure 가상 네트워크 |
| --- | --- | --- |
| **Hello 도메인 컨트롤러에 대 한 IP 주소** |Hello 네트워크 어댑터 속성에 고정 IP 주소 할당 |고정 IP 주소를 hello Set-azurestaticvnetip cmdlet tooassign 실행 |
| **DNS 클라이언트 확인 프로그램** |기본 / 보조 DNS 서버 주소 hello에 도메인 구성원의 네트워크 어댑터 속성 설정 |DNS 서버 주소 hello hello 가상 네트워크 속성 설정 |
| **Active Directory 데이터베이스 저장소** |필요에 따라 C:\에서 hello 기본 저장소 위치를 변경 |C:\에서 toochange 기본 저장소 위치를 필요 |

## <a name="create-an-azure-virtual-network"></a>Azure 가상 네트워크 만들기
1. Azure 클래식 포털 toohello에 로그인 합니다.
2. 가상 네트워크를 만듭니다. **네트워크** > **가상 네트워크 만들기**를 클릭합니다. 다음 테이블 toocomplete hello 마법사 hello hello 값을 사용 합니다.

   | 마법사 페이지 | 값 지정 |
   | --- | --- |
   |  **가상 네트워크 세부 정보** |<p>이름: 가상 네트워크의 이름 입력</p><p>지역: hello 가장 가까운 지역을 선택합니다</p> |
   |  **DNS 및 VPN** |<p>DNS 서버는 비워 둠</p><p>VPN 옵션 선택 안 함</p> |
   |  **가상 네트워크 주소 공간** |<p>서브넷 이름: 서브넷의 이름 입력</p><p>시작 IP: <b>10.0.0.0</b></p><p>CIDR: <b>/24 (256)</b></p> |

## <a name="create-vms-toorun-hello-domain-controller-and-dns-server-roles"></a>Vm toorun hello 도메인 컨트롤러 및 DNS 서버 역할 만들기
다음 단계 toocreate 필요에 따라 Vm toohost hello DC 역할 hello를 반복 합니다. 두 개 이상의 가상 Dc tooprovide 내결함성 및 중복성을 배포 해야 합니다. Azure 가상 네트워크는 유사 하 게 구성 하는 두 개 이상의 Dc 포함 경우 hello (즉, 두 Gc 실행된 DNS 서버는 모두 및 보유 하 고 모든 FSMO 역할 등) 이러한 Dc 가용성 향상 된 내결함성에 대 한 집합에서 실행 하는 hello Vm을 배치 합니다.

UI hello 대신 Windows PowerShell을 사용 하 여 toocreate hello Vm 참조 [Azure PowerShell을 사용 하 여 toocreate 및 Windows 기반 가상 컴퓨터를 미리 구성](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.

1. Hello 클래식 포털에서 클릭 **새로** > **계산** > **가상 컴퓨터** > **갤러리에서**. Hello 다음 toocomplete hello 마법사를 사용 합니다. 다른 값이 제안 하거나 필요한 경우를 제외 설정에 대 한 hello 기본값을 허용 합니다.

   | 마법사 페이지 | 값 지정 |
   | --- | --- |
   |  **이미지 선택** |Windows Server 2012 R2 Datacenter |
   |  **가상 컴퓨터 구성** |<p>가상 컴퓨터 이름: 단일 레이블 이름(예: AzureDC1)을 입력합니다.</p><p>새 사용자 이름: hello 사용자 이름을 입력 합니다. 이 사용자는 hello hello VM 로컬 관리자 그룹의 구성원 됩니다. 해야 toohello VM에서에서이 이름을 toosign hello에 대 한 처음으로. hello 기본 제공 계정인 관리자 작동 하지 않습니다.</p><p>새 암호/확인: 암호를 입력합니다.</p> |
   |  **가상 컴퓨터 구성** |<p>클라우드 서비스: 선택 <b>새 클라우드 서비스를 만들</b> hello 첫 번째 VM을 호스트 하는 더 많은 Vm을 만들 때 동일한 클라우드 서비스 이름 선택 hello DC 역할입니다.</p><p>클라우드 서비스 DNS 이름: 전역적으로 고유한 이름을 지정합니다.</p><p>지역/선호도 그룹/가상 네트워크: hello 가상 네트워크 이름 (예: WestUSVNet)를 지정 합니다.</p><p>저장소 계정: 선택 <b>자동으로 생성 된 저장소 계정을 사용 하 여</b> hello 첫 번째 VM과 동일한 저장소 계정 이름을 호스트 하는 더 많은 Vm을 만들 때 다음 선택 hello DC 역할입니다.</p><p>가용성 집합: <b>가용성 집합 만들기</b>를 선택합니다.</p><p>가용성 집합 이름은: hello 첫 번째 VM을 만들 때 설정할 hello 가용성에 대 한 이름을 입력 한 다음 동일한 더 많은 Vm을 만들 때 이름을 선택 합니다.</p> |
   |  **가상 컴퓨터 구성** |<p>선택 <b>VM 에이전트 설치 hello</b> 및 기타 확장 해야 합니다.</p> |
2. 디스크 tooeach hello DC 서버 역할을 실행 하는 VM을 연결 합니다. hello 추가 디스크가 필요한 toostore hello AD 데이터베이스, 로그 및 SYSVOL 있습니다. (예: 10GB) hello 디스크에 대 한 크기를 지정 하 고 hello 둡니다 **호스트 캐시 기본 설정** 도**None**합니다. Hello 단계에 대 한 참조 [어떻게 tooAttach 데이터 디스크 tooa Windows 가상 컴퓨터](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.
3. Toohello VM에에서 처음 로그인 후에 열 **서버 관리자** > **파일 및 저장소 서비스** toocreate NTFS를 사용 하 여이 디스크의 볼륨을 합니다.
4. Hello DC 역할 실행할 Vm에 대 한 고정 IP 주소를 예약 합니다. 고정 IP 주소를 tooreserve hello Microsoft 웹 플랫폼 설치 관리자 다운로드 및 [Azure PowerShell 설치](/powershell/azure/overview) hello Set-azurestaticvnetip cmdlet을 실행 합니다. 예:

    `Get-AzureVM -ServiceName AzureDC1 -Name AzureDC1 | Set-AzureStaticVNetIP -IPAddress 10.0.0.4 | Update-AzureVM`

고정 IP 주소 설정에 대한 자세한 내용은 [VM의 고정 내부 IP 주소 구성](../virtual-network/virtual-networks-reserved-private-ip.md)을 참조하세요.

## <a name="install-windows-server-active-directory"></a>Windows Server Active Directory 설치
사용 하 여 동일한 루틴을 너무 hello[AD DS 설치](https://technet.microsoft.com/library/jj574166.aspx) 온-프레미스를 사용 하는 (즉, 사용할 수 있습니다 hello UI, 응답 파일, 또는 Windows PowerShell). 새 포리스트 tooprovide 관리자 자격 증명 tooinstall이 필요합니다. hello Active Directory 데이터베이스에 대 한 toospecify hello 위치, 로그 및 SYSVOL toohello VM을 연결 하는 hello 운영 체제 드라이브 toohello 추가 데이터 디스크에서 hello 기본 저장소 위치를 변경 합니다.

Hello DC 설치가 완료 되 면 toohello VM을 다시 연결 하 고 toohello DC에 로그온 합니다. Toospecify 도메인 자격 증명을 기억 합니다.

## <a name="reset-hello-dns-server-for-hello-azure-virtual-network"></a>Hello Azure 가상 네트워크에 대 한 hello DNS 서버를 다시 설정
1. 새 DC/DNS 서버 hello hello DNS 전달자 설정을 다시 설정 합니다.
   1. 서버 관리자에서 **도구** > **DNS**를 클릭합니다.
   2. **DNS 관리자**hello hello DNS 서버 이름을 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다.
   3. Hello에 **전달자** 탭 hello 전달자의 hello IP 주소를 클릭 하 고 클릭 **편집**합니다.  Hello IP 주소를 선택 하 고 클릭 **삭제**합니다.
   4. 클릭 **확인** tooclose hello 편집기 및 **확인** 다시 tooclose hello DNS 서버 속성입니다.
2. Hello 가상 네트워크에 대 한 hello DNS 서버 설정을 업데이트 합니다.
   1. 클릭 **가상 네트워크** > 앞에서 만든 hello 가상 네트워크를 두 번 클릭 > **구성** > **DNS 서버**hello 이름을 입력 하 고 DIP 중 하나의 hello hello DC/DNS 서버 역할을 클릭 하 여를 실행 하는 hello Vm **저장**합니다.
   2. Hello VM을 선택 하 고 클릭 **다시 시작** tootrigger hello VM tooconfigure DNS 확인자 설정 hello 새로운 DNS 서버 hello IP 주소를 사용 합니다.

## <a name="create-vms-for-domain-members"></a>도메인 구성원에 대한 VM 만들기
1. 응용 프로그램 서버로 toocreate Vm toorun 단계를 수행 하는 hello를 반복 합니다. 다른 값이 제안 하거나 필요한 경우를 제외 설정에 대 한 hello 기본값을 허용 합니다.

   | 마법사 페이지 | 값 지정 |
   | --- | --- |
   |  **이미지 선택** |Windows Server 2012 R2 Datacenter |
   |  **가상 컴퓨터 구성** |<p>가상 컴퓨터 이름: 단일 레이블 이름(예: AppServer1)을 입력합니다.</p><p>새 사용자 이름: hello 사용자 이름을 입력 합니다. 이 사용자는 hello hello VM 로컬 관리자 그룹의 구성원 됩니다. 해야 toohello VM에서에서이 이름을 toosign hello에 대 한 처음으로. hello 기본 제공 계정인 관리자 작동 하지 않습니다.</p><p>새 암호/확인: 암호를 입력합니다.</p> |
   |  **가상 컴퓨터 구성** |<p>클라우드 서비스: 선택 **새 클라우드 서비스를 만들** hello에 대 한 첫 번째 VM을 선택 하는 많은 수의 Vm 만들 때 서비스 이름을 클라우드 동일 호스팅할 hello 응용 프로그램입니다.</p><p>클라우드 서비스 DNS 이름: 전역적으로 고유한 이름을 지정합니다.</p><p>지역/선호도 그룹/가상 네트워크: hello 가상 네트워크 이름 (예: WestUSVNet)를 지정 합니다.</p><p>저장소 계정: 선택 **자동으로 생성 된 저장소 계정을 사용 하 여** hello에 대 한 첫 번째 VM 선택한 후 더 많은 Vm를 만들 때 동일한 저장소 계정 이름을 지정 하는 hello 응용 프로그램을 호스트 합니다.</p><p>가용성 집합: **가용성 집합 만들기**를 선택합니다.</p><p>가용성 집합 이름은: hello 첫 번째 VM을 만들 때 설정할 hello 가용성에 대 한 이름을 입력 한 다음 동일한 더 많은 Vm을 만들 때 이름을 선택 합니다.</p> |
   |  **가상 컴퓨터 구성** |<p>선택 <b>VM 에이전트 설치 hello</b> 및 기타 확장 해야 합니다.</p> |
2. 각 VM을 프로 비전 한 후 로그인 toohello 도메인에 가입 합니다. **서버 관리자**에서 **로컬 서버** > **작업 그룹** > **변경...**을 클릭한 다음 선택한 후 **도메인** 및 온-프레미스 도메인의 형식 hello 이름입니다. 도메인 사용자의 자격 증명을 제공 하 고 hello VM toocomplete hello 도메인 가입 다시 시작 합니다.

UI hello 대신 Windows PowerShell을 사용 하 여 toocreate hello Vm 참조 [Azure PowerShell을 사용 하 여 toocreate 및 Windows 기반 가상 컴퓨터를 미리 구성](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.

Windows PowerShell 사용에 대한 자세한 내용은 [Azure Cmdlets 시작하기](/powershell/azure/overview) 및 [Azure Cmdlet 참조](/powershell/azure/get-started-azureps)를 확인하세요.

## <a name="see-also"></a>참고 항목
* [Azure 가상 네트워크에 tooinstall 새 Active Directory 포리스트 하는 방법](http://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/How-to-install-a-new-Active-Directory-forest-on-an-Azure-virtual-network)
* [Azure 가상 컴퓨터에 Windows Server Active Directory를 배포하기 위한 지침](https://msdn.microsoft.com/library/azure/jj156090.aspx)
* [사이트 간 VPN 구성](../vpn-gateway/vpn-gateway-site-to-site-create.md)
* [Azure 가상 네트워크에 복제 Active Directory 도메인 컨트롤러 설치](active-directory-install-replica-active-directory-domain-controller.md)
* [Microsoft Azure IT Pro IaaS: (01) 가상 컴퓨터 기본 사항(영문)](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure IT Pro IaaS: (05) 가상 네트워크 및 프레미스 간 연결 만들기(영문)](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)
* [Virtual Network 개요](../virtual-network/virtual-networks-overview.md)
* [어떻게 tooinstall Azure PowerShell 및 구성](/powershell/azure/overview)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure Cmdlet 참조](/powershell/azure/get-started-azureps)
* [Azure VM 고정 IP 주소 설정](http://windowsitpro.com/windows-azure/set-azure-vm-static-ip-address)
* [어떻게 tooassign 고정 IP tooAzure VM](http://www.bhargavs.com/index.php/2014/03/13/how-to-assign-static-ip-to-azure-vm/)
* [새 Active Directory 포리스트 설치](https://technet.microsoft.com/library/jj574166.aspx)
* [소개 tooActive Directory 도메인 서비스 (AD DS) Virtualization (Level 100)](https://technet.microsoft.com/library/hh831734.aspx)

<!--Image references-->
[1]: ./media/active-directory-new-forest-virtual-machine/AD_Forest.png
