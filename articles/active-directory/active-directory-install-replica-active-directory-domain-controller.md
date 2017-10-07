---
title: "Azure에서 복제본 Active Directory 도메인 컨트롤러 aaaInstall | Microsoft Docs"
description: "자습서는 Azure 가상 컴퓨터에서 어떻게 tooinstall 온-프레미스 Active Directory에서 도메인 컨트롤러의 포리스트에 대해 설명입니다."
services: virtual-network
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 8c9ebf1b-289a-4dd6-9567-a946450005c0
ms.service: virtual-network
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 74876fce2ca2a29f02c2828f9b3a21227248233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-replica-active-directory-domain-controller-in-an-azure-virtual-network"></a>Azure 가상 네트워크에 복제 Active Directory 도메인 컨트롤러 설치
이 항목에서는 방법을 tooinstall Azure 가상 네트워크에서 Azure 가상 컴퓨터 (Vm)에서 온-프레미스 Active Directory 도메인에 대 한 추가 도메인 컨트롤러 (라고도 복제본 Dc).

> [!IMPORTANT]
> Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다.

다음 관련 토픽을 참조할 수도 있습니다.

* 선택적으로 Azure 가상 네트워크에 새 Active Directory 포리스트를 설치할 수 있습니다. 이러한 단계는 [Azure 가상 네트워크에 새 Active Directory 포리스트 설치](active-directory-new-forest-virtual-machine.md)를 참조하세요.
* Azure 가상 네트워크에 AD DS(Active Directory 도메인 서비스)를 설치하는 방법에 대한 개념 지침은 [Azure 가상 컴퓨터에 Windows Server Active Directory 배포에 대한 지침](https://msdn.microsoft.com/library/azure/jj156090.aspx)을 참조하세요.

## <a name="scenario-diagram"></a>시나리오 다이어그램
이 시나리오에서는 외부 사용자 도메인에 가입 된 서버에서 실행 되는 응용 프로그램 tooaccess 필요 합니다. hello hello 응용 프로그램 서버를 실행 하 고 복제본 Dc hello 하는 Vm은 Azure 가상 네트워크에 설치 됩니다. hello 가상 네트워크 될 수 있습니다 하 여 연결 된 toohello 온-프레미스 네트워크는 [사이트 간 VPN](../vpn-gateway/vpn-gateway-site-to-site-create.md) hello 다음과 같이 연결을 다이어그램 또는 있습니다 사용할 수 [ExpressRoute](../expressroute/expressroute-locations-providers.md) 더 빠른 연결에 대 한 합니다.

hello 응용 프로그램 서버 및 hello Dc 배포 되는 별도 클라우드 서비스 내에서 toodistribute 계산 처리 내에서 [가용성 집합](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 향상된 내결함성에 대 한 합니다.
hello Dc Active Directory 복제를 사용 하 여 서로 및 온-프레미스 Dc를 복제 합니다. 동기화 도구가 필요하지 않습니다.

![Azure VNet에서 복제 Active Directory 도메인 컨트롤러의 다이어그램][1]

## <a name="create-an-active-directory-site-for-hello-azure-virtual-network"></a>Hello Azure 가상 네트워크에 대 한 Active Directory 사이트 만들기
것이 좋습니다 toocreate hello 네트워크 지역 해당 toohello 가상 네트워크를 나타내는 Active Directory에서 사이트입니다. 그러면 인증, 복제 및 기타 DC 위치 작업을 최적화하는 데 도움이 됩니다. hello 다음 단계에서는 설명 방법을 toocreate, 한 사이트 자세한 배경을 알고 싶으면, 참조 및 [새 사이트 추가](https://technet.microsoft.com/library/cc781496.aspx)합니다.

1. Active Directory 사이트 및 서비스를 엽니다(**서버 관리자** > **도구** > **Active Directory 사이트 및 서비스**).
2. Azure 가상 네트워크를 만든 사이트 toorepresent hello 영역을 만들: 클릭 **사이트** > **동작** > **새 사이트** > 형식 미국 서 부 Azure 같은 hello 새 사이트의 hello 이름 > 사이트 링크를 선택 > **확인**합니다.
3. 서브넷을 만들고 hello 새 사이트에 연결: 두 번 클릭 **사이트** > 마우스 오른쪽 단추로 클릭 **서브넷** > **새 서브넷** > hello의 IP 주소 범위 입력 가상 네트워크 (예: hello 시나리오 다이어그램에서 10.1.0.0/16) hello > 선택 hello 새로운 Azure 사이트 > **확인**합니다.

## <a name="create-an-azure-virtual-network"></a>Azure 가상 네트워크 만들기
1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com), 클릭 **새로** > **네트워크 서비스** > **가상 네트워크**  >  **사용자 지정 만들기** 및 사용 하 여 hello 다음 toocomplete hello 마법사 값입니다.

   | 마법사 페이지 | 값 지정 |
   | --- | --- |
   |  **가상 네트워크 세부 정보** |<p>이름: WestUSVNet 같은 hello 가상 네트워크에 대 한 이름을 입력 합니다.</p><p>지역: hello 가장 가까운 영역을 선택 합니다.</p> |
   |  **DNS 및 VPN 연결** |<p>DNS 서버: hello 이름과 하나 이상의 온-프레미스 DNS 서버의 IP 주소를 지정 합니다.</p><p>연결: **사이트 간 VPN 구성**을 선택합니다.</p><p>로컬 네트워크: 새 로컬 네트워크를 지정합니다.</p><p>VPN 대신 ExpressRoute를 사용하는 경우 [Exchange 공급자를 통해 ExpressRoute 연결 구성](../expressroute/expressroute-locations-providers.md)을 참조하세요.</p> |
   |  **사이트 간 연결** |<p>이름: hello 온-프레미스 네트워크에 대 한 이름을 입력 합니다.</p><p>VPN 장치 IP 주소: hello toohello 가상 네트워크 연결 하는 hello 장치의 공용 IP 주소를 지정 합니다. NAT 뒤 hello VPN 장치를 찾을 수 없습니다.</p><p>주소: hello 주소 범위 (예: hello 시나리오 다이어그램에서 192.168.0.0/16) 온-프레미스 네트워크를 지정 합니다.</p> |
   |  **가상 네트워크 주소 공간** |<p>주소 공간: 원하는 toorun hello (예: hello 시나리오 다이어그램에서 10.1.0.0/16) Azure 가상 네트워크에서에서 Vm에 대 한 hello IP 주소 범위를 지정 합니다. 이 주소 범위는 hello 온-프레미스 네트워크의 hello 주소 범위와 겹칠 수 없습니다.</p><p>서브넷: 이름 및 응용 프로그램 서버 hello에 대 한 서브넷에 대 한 주소 지정 (프런트 엔드, 같은 10.1.1.0/24) 및 Dc hello에 대 한 (백 엔드, 같은 10.1.2.0/24).</p><p>**게이트웨이 서브넷 추가**를 클릭합니다.</p> |
2. 다음으로 hello 가상 네트워크 게이트웨이 toocreate 보안 사이트 간 VPN 연결을 구성 합니다. 참조 [가상 네트워크 게이트웨이 구성](../vpn-gateway/vpn-gateway-configure-vpn-gateway-mp.md) hello 지침에 대 한 합니다.
3. Hello 새 가상 네트워크와 온-프레미스 VPN 장치 간에 hello 사이트 간 VPN 연결을 만듭니다. 참조 [가상 네트워크 게이트웨이 구성](../vpn-gateway/vpn-gateway-configure-vpn-gateway-mp.md) hello 지침에 대 한 합니다.

## <a name="create-azure-vms-for-hello-dc-roles"></a>DC 역할 hello에 대 한 Azure Vm 만들기
다음 단계 toocreate 필요에 따라 Vm toohost hello DC 역할 hello를 반복 합니다. 두 개 이상의 가상 Dc tooprovide 내결함성 및 중복성을 배포 해야 합니다. Azure 가상 네트워크는 유사 하 게 구성 하는 두 개 이상의 Dc 포함 경우 hello (즉, 두 Gc 실행된 DNS 서버는 모두 및 보유 하 고 모든 FSMO 역할 등) 이러한 Dc 가용성 향상 된 내결함성에 대 한 집합에서 실행 하는 hello Vm을 배치 합니다.
UI hello 대신 Windows PowerShell을 사용 하 여 toocreate hello Vm 참조 [Azure PowerShell을 사용 하 여 toocreate 및 Windows 기반 가상 컴퓨터를 미리 구성](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.

1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com), 클릭 **새로** > **계산** > **가상 컴퓨터**  >  **갤러리에서**합니다. Hello 다음 toocomplete hello 마법사를 사용 합니다. 다른 값이 제안 하거나 필요한 경우를 제외 설정에 대 한 hello 기본값을 허용 합니다.

   | 마법사 페이지 | 값 지정 |
   | --- | --- |
   |  **이미지 선택** |Windows Server 2012 R2 Datacenter |
   |  **가상 컴퓨터 구성** |<p>가상 컴퓨터 이름: 단일 레이블 이름(예: AzureDC1)을 입력합니다.</p><p>새 사용자 이름: hello 사용자 이름을 입력 합니다. 이 사용자는 hello hello VM 로컬 관리자 그룹의 구성원 됩니다. 해야 toohello VM에서에서이 이름을 toosign hello에 대 한 처음으로. hello 기본 제공 계정인 관리자 작동 하지 않습니다.</p><p>새 암호/확인: 암호를 입력합니다.</p> |
   |  **가상 컴퓨터 구성** |<p>클라우드 서비스: 선택 <b>새 클라우드 서비스를 만들</b> hello 첫 번째 VM을 호스트 하는 더 많은 Vm을 만들 때 동일한 클라우드 서비스 이름 선택 hello DC 역할입니다.</p><p>클라우드 서비스 DNS 이름: 전역적으로 고유한 이름을 지정합니다.</p><p>지역/선호도 그룹/가상 네트워크: hello 가상 네트워크 이름 (예: WestUSVNet)를 지정 합니다.</p><p>저장소 계정: 선택 <b>자동으로 생성 된 저장소 계정을 사용 하 여</b> hello 첫 번째 VM과 동일한 저장소 계정 이름을 호스트 하는 더 많은 Vm을 만들 때 다음 선택 hello DC 역할입니다.</p><p>가용성 집합: <b>가용성 집합 만들기</b>를 선택합니다.</p><p>가용성 집합 이름은: hello 첫 번째 VM을 만들 때 설정할 hello 가용성에 대 한 이름을 입력 한 다음 동일한 더 많은 Vm을 만들 때 이름을 선택 합니다.</p> |
   |  **가상 컴퓨터 구성** |<p>선택 <b>VM 에이전트 설치 hello</b> 및 기타 확장 해야 합니다.</p> |
2. 디스크 tooeach hello DC 서버 역할을 실행 하는 VM을 연결 합니다. hello 추가 디스크가 필요한 toostore hello AD 데이터베이스, 로그 및 SYSVOL 있습니다. (예: 10GB) hello 디스크에 대 한 크기를 지정 하 고 hello 둡니다 **호스트 캐시 기본 설정** 도**None**합니다. Hello 단계에 대 한 참조 [어떻게 tooAttach 데이터 디스크 tooa Windows 가상 컴퓨터](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.
3. Toohello VM에에서 처음 로그인 후에 열 **서버 관리자** > **파일 및 저장소 서비스** toocreate NTFS를 사용 하 여이 디스크의 볼륨을 합니다.
4. Hello DC 역할 실행할 Vm에 대 한 고정 IP 주소를 예약 합니다. 고정 IP 주소를 tooreserve hello Microsoft 웹 플랫폼 설치 관리자 다운로드 및 [Azure PowerShell 설치](/powershell/azure/overview) hello Set-azurestaticvnetip cmdlet을 실행 합니다. 예:

    'Get-AzureVM -ServiceName AzureDC1 -Name AzureDC1 | Set-AzureStaticVNetIP -IPAddress 10.0.0.4 | Update-AzureVM

고정 IP 주소 설정에 대한 자세한 내용은 [VM의 고정 내부 IP 주소 구성](../virtual-network/virtual-networks-reserved-private-ip.md)을 참조하세요.

## <a name="install-ad-ds-on-azure-vms"></a>Azure VM에 AD DS 설치
VM tooa 하 고 온-프레미스 네트워크에 걸쳐 hello 사이트 간 VPN 또는 express 경로 연결 tooresources 연결을 갖는지 확인 합니다. Hello Azure Vm에서 AD DS를 설치 합니다. 온-프레미스 네트워크 (UI, Windows PowerShell 또는 응답 파일)에 추가 DC tooinstall를 사용 하는 동일한 프로세스를 사용할 수 있습니다. AD DS를 설치 하는 대로 hello AD 데이터베이스, 로그 및 SYSVOL의 hello 위치에 대 한 hello 새 볼륨을 지정 해야 합니다. AD DS 설치에 리프레셔가 필요한 경우 [Active Directory Domain Services 설치](https://technet.microsoft.com/library/hh472162.aspx)(수준 100) 또는 [기존 도메인에 복제본 Windows Server 2012 도메인 컨트롤러 설치(수준 200)](https://technet.microsoft.com/library/jj574134.aspx)를 참조하세요.

## <a name="reconfigure-dns-server-for-hello-virtual-network"></a>Hello 가상 네트워크의 DNS 서버를 다시 구성
1. Hello에 [Azure 포털](https://portal.azure.com), hello에 **리소스 검색** 상자에 입력 *가상 네트워크*, 클릭 **가상 네트워크 (클래식)** 에서 hello 검색 결과입니다. Hello 가상 네트워크의 hello 이름을 클릭 한 다음 [hello 가상 네트워크용 DNS 서버 IP 주소를 다시 구성](../virtual-network/virtual-network-manage-network.md#dns-servers) toouse hello 고정 IP 주소 할당 toohello 온-프레미스 DNS의 hello IP 주소 대신의 복제본 Dc 서버입니다.
2. hello 가상 네트워크에 모든 hello 복제본 DC Vm hello 가상 네트워크에서 toouse DNS 서버로 구성 된 tooensure 클릭 **가상 컴퓨터**, 각 VM에 대 한 hello 상태 열을 클릭 하 고 클릭 **다시 시작** . Hello VM 표시 될 때까지 기다렸다가 **실행** toosign를 시도 하기 전에 상태입니다.

## <a name="create-vms-for-application-servers"></a>응용 프로그램 서버에 대한 VM 만들기
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

## <a name="additional-resources"></a>추가 리소스
* [Azure 가상 컴퓨터에 Windows Server Active Directory를 배포하기 위한 지침](https://msdn.microsoft.com/library/azure/jj156090.aspx)
* [어떻게 tooupload 기존 온-프레미스 Hyper-v 도메인 컨트롤러 tooAzure Azure PowerShell을 사용 하 여](http://support.microsoft.com/kb/2904015)
* [Azure 가상 네트워크에 새 Active Directory 포리스트 설치](active-directory-new-forest-virtual-machine.md)
* [Azure 가상 네트워크](../virtual-network/virtual-networks-overview.md)
* [Microsoft Azure IT Pro IaaS: (01) 가상 컴퓨터 기본 사항(영문)](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure IT Pro IaaS: (05) 가상 네트워크 및 프레미스 간 연결 만들기(영문)](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure 관리 Cmdlet](/powershell/module/azurerm.compute/#virtual_machines)

<!--Image references-->
[1]: ./media/active-directory-install-replica-active-directory-domain-controller/ReplicaDCsOnAzureVNet.png
