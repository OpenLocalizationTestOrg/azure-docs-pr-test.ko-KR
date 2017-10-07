---
title: "Windows Server Active directory 배포 Azure 가상 컴퓨터에서 aaaGuidelines | Microsoft Docs"
description: "알아보려면 어떻게 해야 toodeploy AD 도메인 서비스 및 온-프레미스로 AD 페더레이션 서비스에서 Azure 가상 컴퓨터 작동 방식을 알고 있는 경우."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
ms.assetid: 04df4c46-e6b6-4754-960a-57b823d617fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: femila
ms.openlocfilehash: 9ad5a5f138a6402cbb656d9160545846051207b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="guidelines-for-deploying-windows-server-active-directory-on-azure-virtual-machines"></a>Azure 가상 컴퓨터에 Windows Server Active Directory를 배포하기 위한 지침
이 문서에서는 hello 및 중요 한 차이점 배포 Windows Server Active Directory 도메인 서비스 (AD DS) Active Directory Federation Services (AD FS) 온-프레미스와 Microsoft Azure 가상 컴퓨터에 배포 하기를 설명 합니다.

## <a name="scope-and-audience"></a>범위 및 대상
hello 문서 경험이 이미 Active Directory 온-프레미스 배포에 대 한 사용 됩니다. Hello Microsoft Azure 가상 컴퓨터/Azure 가상 네트워크와 기존의 온-프레미스 Active Directory 배포에서 Active Directory 배포의 차이점을 설명 합니다. Azure 가상 컴퓨터와 Azure 가상 네트워크는 인프라-as a Service (IaaS) 조직 tooleverage 컴퓨팅 hello 클라우드에서 리소스에 대 한 제공 포함 됩니다.

필요한 AD 배포에 익숙하지 않은, 참조 hello [AD DS 배포 가이드](https://technet.microsoft.com/library/cc753963) 또는 [AD FS 배포 계획](https://technet.microsoft.com/library/dn151324.aspx) 적절 하 게 합니다.

이 문서 hello 판독기 hello 다음 개념에 잘 알고 있다고 가정 합니다.

* Windows Server AD DS 배포 및 관리
* 배포 하 고 DNS toosupport Windows Server AD DS 인프라 구성
* Windows Server AD FS 배포 및 관리
* Windows Server AD FS 토큰을 사용할 수 있는 신뢰 당사자 응용 프로그램(웹 사이트 및 웹 서비스) 배포, 구성 및 관리
* 어떻게 tooconfigure a 가상 컴퓨터, 가상 같은 일반적인 가상 컴퓨터 개념, 디스크 및 가상 네트워크

이 문서에 Windows Server AD DS 또는 AD FS가 부분적으로 온-프레미스로 배포 하 고 Azure 가상 컴퓨터에 부분적으로 배포 된 하이브리드 배포 시나리오에 대 한 hello 요구 사항을 강조 표시 합니다. hello 먼저 살펴봅니다 hello의 중요 한 차이점과 디자인 및 배포에 영향을 주는 중요 한 결정 사항을와 온 프레미스 Azure 가상 컴퓨터에 Windows Server AD DS 및 AD FS를 실행 합니다. hello 용지 hello 나머지 각 hello 의사 결정 사항을 좀 더 자세하게 및 어떻게 tooapply hello 지침 toovarious 배포 시나리오에 대 한 지침을 설명 합니다.

이 문서에서의 hello 구성을 설명 하지 않습니다 [Azure Active Directory](http://azure.microsoft.com/services/active-directory/), 클라우드 응용 프로그램에 대 한 id 관리 및 액세스 제어 기능을 제공 하는 REST 기반 서비스인 합니다. 그러나 Azure Active Directory (Azure AD) 및 Windows Server AD DS는 디자인 된 toowork 함께 tooprovide id 및 액세스 관리 솔루션을 지금의 하이브리드 IT 환경과 최신 응용 프로그램입니다. toohelp은 hello 차이 및 Windows Server AD DS와 Azure AD 간의 관계를 이해, hello 다음을 고려 하세요.

1. 발생할 수 있습니다 Windows Server AD DS hello 클라우드의 Azure 가상 컴퓨터에 Azure tooextend를 사용 하는 경우 온-프레미스 데이터 센터 hello 클라우드입니다.
2. 사용자가 single sign on tooSoftware-as a Service (SaaS) 응용 프로그램 toogive Azure AD를 사용할 수 있습니다. 이 기술은 Microsoft Office 365에서 사용되며, Azure 또는 기타 클라우드 플랫폼에서 실행하는 응용 프로그램에서도 이 기술을 사용할 수 있습니다.
3. Facebook, Google, Microsoft 및 hello 클라우드 또는 온-프레미스에서 호스트 되는 다른 identity 공급자 tooapplications의 id를 사용 하 여 Azure AD (액세스 제어 서비스) toolet 사용자 로그인을 사용할 수 있습니다.

이러한 차이점에 대한 자세한 내용은 [Azure ID](fundamentals-identity.md)를 참조하세요.

## <a name="related-resources"></a>관련 리소스
다운로드 하 고 hello를 실행 하면 [Azure 가상 컴퓨터 준비 평가](https://www.microsoft.com/download/details.aspx?id=40898)합니다. hello 평가 자동으로 온-프레미스 환경 검사 하 고 hello에 따라 사용자 지정된 보고서를 생성 지침 있는이 항목 toohelp hello 환경 tooAzure 마이그레이션할 합니다.

먼저 검토 하는 hello 자습서, 가이드 및 비디오 hello 다음 항목을 포함 하는 것이 좋습니다.

* [Hello Azure 포털에서에서 클라우드 전용 가상 네트워크 구성](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)
* [Hello Azure 포털에서에서 사이트 간 VPN 구성](../vpn-gateway/vpn-gateway-site-to-site-create.md)
* [Azure 가상 네트워크에 새 Active Directory 포리스트 설치](active-directory-new-forest-virtual-machine.md)
* [Azure에서 복제 Active Directory 도메인 컨트롤러 설치](active-directory-install-replica-active-directory-domain-controller.md)
* [Microsoft Azure IT Pro IaaS: (01) 가상 컴퓨터 기본 사항(영문)](https://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure IT Pro IaaS: (05) 가상 네트워크 및 프레미스 간 연결 만들기(영문)](https://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)

## <a name="introduction"></a>소개
hello Azure 가상 컴퓨터에 Windows Server Active Directory를 배포 하기 위한 기본적인 요구 사항은 거의 다르지에서 온-프레미스 가상 컴퓨터 (및, toosome 정도 까지는 물리적 컴퓨터)에 배포 합니다. 예를 들어 hello에서 Azure 가상 컴퓨터에 배포 하는 hello 도메인 컨트롤러 (Dc)는 복제본의 기존 Windows Server AD DS의 경우 온-프레미스 회사 도메인/포리스트에서 이면 hello Azure 배포 수 대부분 hello에 동일한 방식으로 있습니다 다른 모든 추가 Windows Server Active Directory 사이트를 처리할 수 있습니다. 즉, Windows Server AD ds에서 만든 사이트 서브넷을 정의 합니다, 그리고 hello 서브넷 toothat 사이트를 연결 하 고 적절 한 사이트 링크를 사용 하 여 tooother 사이트를 연결 합니다. 그러나 어느 정도 차이가 있는 일반적인 tooall Azure 배포를 지 toohello 특정 배포 시나리오에 따라 달라 집니다. 두 가지 근본적인 차이점은 다음과 같습니다.

### <a name="azure-virtual-machines-may-need-connectivity-toohello-on-premises-corporate-network"></a>Azure 가상 컴퓨터 연결 toohello 온-프레미스 회사 네트워크를 할 수 있습니다.
Azure 가상 컴퓨터 백 tooan 온-프레미스 회사 네트워크에 필요한 사이트-사이트를 포함 하는 Azure 가상 네트워크에서 또는 사이트와 지점 간 가상 사설망 (VPN) 연결 구성 요소 수 tooseamlessly Azure 가상 컴퓨터를 연결 하 고 온-프레미스 컴퓨터입니다. 온-프레미스 도메인 구성원 컴퓨터 tooaccess Azure 가상 컴퓨터에 독점적으로 호스팅되는 도메인 컨트롤러를 소유한 Windows Server Active Directory 도메인이 VPN 구성 요소를 사용 하면 수도 있습니다. 하지만 것이 중요 한 toonote, 경우 hello VPN 실패 하는지, 인증 및 Windows Server Active Directory에 종속 된 다른 작업이 실패할 수도 있습니다. 사용자가 기존 캐시 된 자격 증명을 사용할 모든 피어 투 피어에 수 toosign 수 있습니다 또는 toobe 발급 되거나 유효 하지 않게 된 아직는 티켓에 대 한 클라이언트와 서버 간 인증 시도 실패 합니다.

참조 [가상 네트워크](http://azure.microsoft.com/documentation/services/virtual-network/) 비롯 한 단계별 자습서의 목록과 데모 비디오에 대 한 [hello Azure 포털에서에서 사이트 간 VPN 구성](../vpn-gateway/vpn-gateway-site-to-site-create.md)합니다.

> [!NOTE]
> 또한 온-프레미스 네트워크와 연결되지 않은 Azure 가상 네트워크에 Windows Server Active Directory를 배포할 수도 있습니다. 그러나이 항목의 hello 지침은 Azure 가상 네트워크 주소 지정 기능을 필수 tooWindows 서버 IP를 제공 하기 때문에 사용 된다고 가정 합니다.
> 
> 

### <a name="static-ip-addresses-must-be-configured-with-azure-powershell"></a>고정 IP 주소는 Azure PowerShell을 통해 구성되어야 합니다.
동적 주소는 기본적으로 할당 되지만 hello Set-azurestaticvnetip cmdlet tooassign 고정 IP 주소를 대신 사용 합니다. 서비스 복구 및 VM 종료/다시 시작을 통해 유지되는 고정 IP 주소를 설정합니다. 자세한 내용은 [가상 컴퓨터에 대한 고정 내부 IP 주소](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/)를 참조하세요.

## <a name="BKMK_Glossary"></a>용어 및 정의
hello 다음은이 문서에서 참조 되는 다양 한 Azure 기술에 대 한 조건의 부분 목록입니다.

* **Azure 가상 컴퓨터**: toodeploy Vm 거의 모두 실행 일반적으로 고객을 허용 하는 Azure의 hello IaaS 제공 온-프레미스 서버 작업입니다.
* **Azure 가상 네트워크**: hello 고객이 만들고 Azure에서 가상 네트워크를 관리 하며 안전 하 게 연결할 수 있게 해 주는 Azure 서비스에에서 직접 tootheir 네트워킹 온-프레미스 네트워킹 인프라 가상 사설망 (VPN)을 사용 하 여 합니다.
* **가상 IP 주소**:는 인터넷 연결 IP 주소 즉 바인딩되지 않았습니다 tooa 특정 컴퓨터나 네트워크 인터페이스 카드입니다. 클라우드 서비스는 리디렉션된 tooan Azure VM 네트워크 트래픽을 받기 위한 가상 IP 주소를 할당 됩니다. 가상 IP 주소는 하나 이상의 Azure 가상 컴퓨터를 포함할 수 있는 클라우드 서비스의 속성입니다. 또한 Azure 가상 네트워크는 하나 이상의 클라우드 서비스를 포함할 수 있습니다. 가상 IP 주소는 기본 부하 분산 기능을 제공합니다.
* **동적 IP 주소**: hello IP 주소는 내부 전용입니다. 구성 해야으로 고정 IP 주소 (사용 하 여 hello Set-azurestaticvnetip cmdlet) hello DC/DNS 서버 역할을 호스트 하는 Vm에 대 한 합니다.
* **서비스 복구가**: Azure 자동으로 반환 하는 서비스 tooa 실행 상태 다시 해당 hello 서비스를 검색 한 후 hello 프로세스가 실패 했습니다. 서비스 복구는 가용성과 복원 력을 지 원하는 Azure의 hello 측면 중 하나입니다. 낮지만 VM에서 실행 되는 DC에 대 한 복구 인시던트 이후의 서비스는 hello 결과 유사한 tooan 계획 되지 않은 부팅 하지만 몇 가지 부작용:
  
  * hello VM의에서 가상 네트워크 어댑터 hello 바뀝니다.
  * hello hello 가상 네트워크 어댑터의 MAC 주소 바뀝니다.
  * hello hello VM의 프로세서/c p U ID 바뀝니다.
  * hello hello 가상 네트워크 어댑터의 IP 구성 변경 되지 않습니다 hello VM의 가상 네트워크에 연결 된 tooa 올바르고 hello VM의 IP 주소는 정적 하기만 합니다.
  
  이러한 동작에 영향을 주지 Windows Server Active Directory 않기 때문에 hello MAC 주소 또는 프로세서/c p U ID에 의존 하지 않고 Azure에서 모든 Windows Server Active Directory 배포는 위에서 설명한 대로 Azure 가상 네트워크에서 실행 되는 toobe 것이 좋습니다. .

## <a name="is-it-safe-toovirtualize-windows-server-active-directory-domain-controllers"></a>Windows Server Active Directory 도메인 컨트롤러 안전 toovirtualize 입니까?
Azure 가상 컴퓨터에 Windows Server Active Directory Dc를 배포는 주체 toohello 동일한 지침 가상 컴퓨터에서 온-프레미스로 Dc를 실행 합니다. DC 백업 및 복원을 위한 지침을 따르는 한 가상화된 DC 실행은 안전한 사례입니다. 가상화된 DC를 실행하기 위한 제약 조건 및 지침에 대한 자세한 내용은 [Hyper-V에서 도메인 컨트롤러 실행](https://technet.microsoft.com/library/dd363553)을 참조하세요.

하이퍼바이저는 Windows Server Active Directory를 비롯한 대부분의 분산된 시스템에 문제가 발생할 수 있는 기술을 제공 또는 하찮아 보이게 합니다. 예를 들어 물리적 서버에 디스크를 복제 하거나 San 등의 사용을 비롯 한 서버의 tooroll 백 hello 상태 지원 되지 않는 메서드를 사용할 수 있습니다 하지만 실제 서버에서 이렇게 하는 하이퍼바이저에서 가상 컴퓨터 스냅숏을 복원 보다 훨씬 더 어렵습니다. 발생할 수 있는 hello 동일한 기능을 제공 하는 azure 바람직하지 않은 조건을 합니다. 예를 들어 Dc의 VHD 파일 복원 하면 비슷한 상황이 toousing 스냅숏 복원 기능 발생할 수 있기 때문에 정기 백업 미 실시를 수행 하는 대신 복사 하지 마세요.

이러한 롤백은 Dc 간 toopermanently 분기 상태를 일으킬 수 있는 USN 거품에 설명 합니다. 다음과 같은 문제가 발생할 수 있습니다.

* 느린 개체
* 암호 불일치
* 특성 값 불일치
* Hello 스키마 마스터가 롤백되는 경우의 스키마 불일치

DC에 영향을 주는 방법에 대한 자세한 내용은 [USN 및 USN 롤백](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv.aspx#usn_and_usn_rollback)을 참조하세요.

Windows Server 2012 부터는 [tooAD DS에에서 추가 세이프 가드가 작성 되며](https://technet.microsoft.com/library/hh831734.aspx)합니다. 이러한 보호 기능 hello 기본 하이퍼바이저 플랫폼이 Vm-generationid를 지 원하는 hello 앞에서 언급 한 문제 로부터 가상화 된 도메인 컨트롤러를 보호를 지원 합니다. Azure는 Windows Server 2012 또는 나중에 Azure 가상 컴퓨터를 실행 하는 도메인 컨트롤러 hello 추가 세이프 가드가 있음을 의미 있는 Vm-generationid를 지원 합니다.

> [!NOTE]
> 종료 하 고 hello를 사용 하는 대신 hello 게스트 운영 체제 내에서 Azure의 hello 도메인 컨트롤러 역할을 실행 하는 VM을 다시 시작 해야 **종료** hello Azure 포털에서에서 옵션입니다. 현재 VM 아래로 포털 tooshut hello를 사용 하 여 hello VM toobe 할당 취소 하면 됩니다. Deallocated VM hello 청구 요금을 발생 하지 않는다는 이점은 있지만 다시 설정 hello VM-생성 Id는 DC에 바람직하지 않습니다. Hello VM-생성 Id를 다시 설정 hello AD DS 데이터베이스의 hello invocationID도 다시 설정, hello RID 풀이 무시 되 고 SYSVOL이 신뢰할 수 없는로 표시 됩니다. 자세한 내용은 참조 [소개 tooActive Directory Domain Services (AD DS) Virtualization](https://technet.microsoft.com/library/hh831734.aspx) 및 [안전 하 게 DFSR 가상화](http://blogs.technet.com/b/filecab/archive/2013/04/05/safely-virtualizing-dfsr.aspx)합니다.
> 
> 

## <a name="why-deploy-windows-server-ad-ds-on-azure-virtual-machines"></a>Azure 가상 컴퓨터에 Windows Server AD DS를 배포하는 이유는 무엇입니까?
많은 Windows Server AD DS 배포 시나리오는 Azure에서 VM으로 배포하기에 적합합니다. 예를 들어 아시아의 원격 위치에서 tooauthenticate 사용자는 유럽의 회사가 있다고 가정 합니다. hello 회사 이전에 배포 하지 아시아의 Windows Server Active Directory Dc 비용 toohello toodeploy 되 고 제한 된 전문 지식 toomanage hello 서버 배포 후 합니다. 결과적으로, 아시아의 인증 요청은 최적이 아닌 결과로 유럽의 DC에서 지원됩니다. 이 경우 hello 아시아의 Azure 데이터 센터 내에서 실행 해야 사용자가 지정한 VM에 DC를 배포할 수 있습니다. 해당 DC tooan toohello 원격 위치에는 인증 성능이 향상 됩니다 직접 연결 된 Azure 가상 네트워크를 연결 합니다.

Azure에 잘 맞는 대체 toootherwise 비용이 많이 드는 재해 복구 (DR) 사이트로 이기도합니다. 상대적으로 저렴 한 비용 적은 수의 도메인 컨트롤러와 Azure에서 단일 가상 네트워크를 호스팅 hello 때문에 매력적인 대안이 나타냅니다.

마지막으로, 네트워크 응용 프로그램을 Azure에 SharePoint가 Windows Server Active Directory 필요 하지만 온-프레미스 네트워크 또는 회사 Windows Server Active Directory hello hello에 대 한 종속성 없이 같은 toodeploy를 할 수 있습니다. 서버의 요구 사항을 Azure toomeet hello SharePoint에서 분리 된 포리스트를 배포 합니다.이 경우 최적입니다. 다시 연결 toohello 온-프레미스 네트워크와 회사 Active Directory hello 필요 네트워크 응용 프로그램 배포도 지원 됩니다.

> [!NOTE]
> 계층 3 연결을 제공 하므로 hello Azure 가상 네트워크와 온-프레미스 네트워크 간의 연결 또한 Azure에서 Azure 가상 컴퓨터로 실행 되는 온-프레미스 tooleverage Dc를 실행 하는 구성원 서버를 사용할 수를 제공 하는 VPN 구성 요소 가상 네트워크입니다. 그러나 hello VPN을 사용할 수 없는 경우 간 통신 온-프레미스 컴퓨터와 인증 되 고 다른 오류는 다양 한 Azure 기반 도메인 컨트롤러에서는 작동 하지 않습니다.  
> 
> 

## <a name="contrasts-between-deploying-windows-server-active-directory-domain-controllers-on-azure-virtual-machines-versus-on-premises"></a>Azure 가상 컴퓨터와 온-프레미스에 Windows Server Active Directory 도메인 컨트롤러 배포 간의 비교
* 단일 VM 두 개 이상 포함 된 Windows Server Active Directory 배포 시나리오, Azure 가상 네트워크 IP 주소 일관성을 위해 필요한 toouse입니다. 이 가이드에서는 DC가 Azure 가상 네트워크에서 실행 중임을 가정합니다.
* 온-프레미스 DC와 마찬가지로 고정 IP 주소를 사용하는 것이 좋습니다. 고정 IP 주소는 Azure PowerShell을 사용하여 구성할 수 있습니다. 자세한 내용은 [VM에 대한 고정 내부 IP 주소](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/) 를 참조하세요. 모니터링 시스템 또는 hello 게스트 운영 체제 내에서 고정 IP 주소 구성을 확인 하는 기타 솔루션이 있는 경우 동일한 IP 주소 toohello 네트워크 어댑터의 정적 속성 hello VM hello를 할당할 수 있습니다. 하지만 hello VM 서비스 복구가 수행 하거나 hello 포털에서 종료 되 고 해당 주소가 할당 취소 하는 경우 해당 hello 네트워크 어댑터 취소 될 수 있습니다. 이 경우 hello hello 게스트 내의 고정 IP 주소 toobe 할 다시 설정 합니다.
* 가상 네트워크에 Vm을 배포 하지 의미 하는 것 (않거나 필요) 백 tooan 온-프레미스 네트워크를 연결 합니다. hello 가상 네트워크에는 단순히 그러한 가능성 수 있습니다. Azure와 온-프레미스 네트워크 간의 개인 통신에 대한 가상 네트워크를 만들어야 합니다. Toodeploy hello 온-프레미스 네트워크 VPN 끝점이 필요합니다. hello VPN은 Azure toohello 온-프레미스 네트워크에서 열립니다. 자세한 내용은 참조 [가상 네트워크 개요](../virtual-network/virtual-networks-overview.md) 및 [hello Azure 포털에서에서 사이트 간 VPN 구성](../vpn-gateway/vpn-gateway-site-to-site-create.md)합니다.

> [!NOTE]
> 옵션 너무[지점-사이트 VPN 만들기](../vpn-gateway/vpn-gateway-point-to-site-create.md) 사용할 수 있는 tooconnect 개별 Windows 기반 컴퓨터는 Azure 가상 네트워크를 tooan 직접 합니다.
> 
> 

* 가상 네트워크를 만드는지 여부에 관계 없이 Azure는 송신 트래픽에 대한 요금을 청구하지만 하지만 수신 트래픽에 대한 요금을 청구하지 않습니다. 다양한 Windows Server Active Directory 디자인 선택은 배포에서 생성되는 송신 트래픽의 양에 영향을 줄 수 있습니다. 예를 들어 읽기 전용 도메인 컨트롤러(RODC) 배포는 아웃바운드를 복제하지 않으므로 송신 트래픽을 제한합니다. 하지만 쓰기 작업 hello DC 및 hello에 대 한 hello 결정 toodeploy RODC toobe hello 필요 tooperform에 대해 비교 평가 해야 [호환성](https://technet.microsoft.com/library/cc755190) Rodc와 응용 프로그램 및 서비스 hello 사이트에 있어야 합니다. 트래픽 요금에 대한 자세한 내용은 [Azure 가격 개요](http://azure.microsoft.com/pricing/)를 참조하세요.
* Vm에서 온-프레미스, RAM, 디스크 크기 등과 같은 서버 리소스 toouse 어떤를 완전히 제어할 수 있을 때 Azure에서 미리 구성 된 서버 크기의 목록에서 선택 해야 있습니다. DC에 대 한 데이터 디스크 순서 toostore hello Windows Server Active Directory 데이터베이스에 추가 toohello 운영 체제 디스크에 필요 합니다.

## <a name="can-you-deploy-windows-server-ad-fs-on-azure-virtual-machines"></a>Azure 가상 컴퓨터에 Windows Server AD FS를 배포할 수 있습니까?
예, Azure 가상 컴퓨터에 Windows Server AD FS를 배포 하 고 hello [AD FS 배포에 대 한 유용한](https://technet.microsoft.com/library/dn151324.aspx) 온-프레미스 동일 하 게 적용 tooAD FS 배포 Azure에서. 하지만 일부의 hello 모범 사례와 같은 부하 분산 및 고가용성 제공 이상의 기술이 필요한 어떤 AD FS 자체입니다. Hello 기본 인프라에서 제공 되어야 합니다. 몇 가지 모범 사례를 검토하고 Azure VM 및 Azure 가상 네트워크를 사용하여 실현할 수 있는 방법을 살펴 보겠습니다.

1. **보안 토큰 서비스 (STS) 서버를 제공 하는 대신 직접 toohello 인터넷 합니다.**
   
    Hello STS는 보안 토큰을 발급 하기 때문에 유용 합니다. 따라서 STS 서버를 AD FS 서버를 처리 해야 같은 hello 동일 도메인 컨트롤러로 보호 수준입니다. STS가 손상 되 면 악의적인 사용자가 잠재적으로 해당 선택 toorelying 당사자 응용 프로그램과 신뢰 조직의 다른 STS 서버의 클레임이 포함 된 hello 기능 tooissue 액세스 토큰입니다.
2. **Hello hello AD FS 서버와 동일한 네트워크의 모든 사용자 도메인에 대 한 Active Directory 도메인 컨트롤러를 배포 합니다.**
   
    AD FS 서버 tooauthenticate 사용자가 Active Directory 도메인 서비스를 사용합니다. Hello hello AD FS 서버와 동일한 네트워크에서 도메인 컨트롤러 toodeploy 것이 좋습니다. 이 경우 사이 링크 hello hello Azure 네트워크와 온-프레미스 네트워크를 중단 하 고 더 낮은 대기 시간 및 로그인에 대 한 향상 된 성능을 활성화 비즈니스 연속성을 제공 합니다.
3. **Hello 부하 분산 및 고가용성에 대 한 여러 AD FS 노드를 배포 합니다.**
   
    대부분의 경우에서 AD FS를 사용 하도록 설정 하는 응용 프로그램의 hello 실패 허용 되지 않습니다 hello 필요한 응용 프로그램에 보안 토큰은 종종 중요 업무용 이므로. 결과적으로, AD FS 이제에 있으므로 hello 요주의 경로 tooaccessing 업무용 응용 프로그램, hello AD FS 서비스 여러 AD FS 프록시 및 AD FS 서버를 통해 항상 사용 가능 해야 합니다. 요청을 부하 분산 장치 배포 tooachieve hello AD FS 프록시 및 AD FS hello 서버 앞에 일반적으로 배포 됩니다.
4. **인터넷 액세스에 대한 하나 이상의 웹 응용 프로그램 프록시 노드를 배포합니다.**
   
    사용자가 hello AD FS 서비스에 의해 보호 tooaccess 응용 프로그램을 할 때 hello AD FS 서비스 요구 toobe에서 사용할 수 있는 인터넷 hello 합니다. 이 hello 웹 응용 프로그램 프록시 서비스를 배포 하 여 달성 됩니다. 고가용성 및 부하 분산의 hello 목적을 위해 노드를 하나 이상 toodeploy 것이 좋습니다.
5. **Hello 웹 응용 프로그램 프록시 노드 toointernal 네트워크 리소스에서 액세스를 제한 합니다.**
   
    외부 사용자에 게 tooaccess AD FS에서 tooallow hello 인터넷 toodeploy 웹 응용 프로그램 프록시 노드 (또는 이전 버전의 Windows Server AD FS 프록시) 사용 해야 합니다. hello 웹 응용 프로그램 프록시 노드는 직접 인터넷 toohello를 노출 합니다. 액세스 하기만 toohello AD FS 서버 TCP 포트 443 및 80을 통해 및은 필요한 toobe 도메인에 가입 하지 않습니다. 해당 통신 tooall 것이 좋습니다 (특히 도메인 컨트롤러) 다른 컴퓨터에서 차단 됩니다.
   
    이는 일반적으로 DMZ를 통해 온-프레미스에서 수행됩니다. 방화벽 작업 toorestrict 트래픽 hello DMZ toohello 온-프레미스 네트워크에서 허용 목록 모드를 사용 하 여 (즉,만 hello에서 트래픽을 지정 IP 주소 및 포트 허용 되 고 다른 모든 트래픽을 차단 over 지정).

hello 다음 그림에 기존의 온-프레미스 AD FS 배포 합니다.

![기존의 온-프레미스 Active Directory Federation Services 배포 다이어그램](media/active-directory-deploying-ws-ad-guidelines/ADFS_onprem.png)

그러나 Azure 네이티브, 완전 한 기능의 방화벽 기능을 제공 하지 않는 때문에 다른 옵션에 사용 되는 toobe toorestrict 트래픽이 필요. hello 다음 표에 각 옵션의 장점 및 단점 있습니다.

| 옵션 | 장점 | 단점 |
| --- | --- | --- |
| [Azure 네트워크 ACL](../virtual-network/virtual-networks-acl.md) |보다 저렴하고 간단한 초기 구성 |네트워크 ACL 구성을 추가로 필요한 경우 새 Vm toohello 배포에 추가 됩니다. |
| [Barracuda NG 방화벽](https://www.barracuda.com/products/ngfirewall) |작업의 허용 목록 모드 및 네트워크 ACL 구성이 필요하지 않음 |초기 설치에 대한 증가된 비용 및 복잡성 |

hello 개략적인 단계 toodeploy AD FS이 경우에 다음과 같습니다.

1. VPN 또는 [ExpressRoute](http://azure.microsoft.com/services/expressroute/)를 사용하여 크로스-프레미스 연결로 가상 네트워크를 만듭니다.
2. Hello 가상 네트워크에서 도메인 컨트롤러를 배포 합니다. 이 단계는 선택 사항이지만 권장됩니다.
3. Hello 가상 네트워크에 도메인 가입 된 AD FS 서버를 배포 합니다.
4. 만들기는 [내부 부하 분산 집합](http://azure.microsoft.com/blog/internal-load-balancing/) hello AD FS 서버를 포함 하 고 hello 가상 네트워크 (동적 IP 주소) 내에서 새 개인 IP 주소를 사용 합니다.
   
   1. DNS toocreate hello FQDN toopoint toohello (동적)의 개인 IP 주소 hello 내부 부하 분산 집합을 업데이트 합니다.
5. 클라우드 서비스 (또는 별도 가상 네트워크) hello에 대 한 웹 응용 프로그램 프록시 노드 만들기.
6. Hello 웹 응용 프로그램 프록시 노드 hello 클라우드 서비스 또는 가상 네트워크에 배포
   
   1. Hello 웹 응용 프로그램 프록시 노드를 포함 하는 외부 부하 분산 집합을 만듭니다.
   2. Hello 외부 DNS 이름 (FQDN) toopoint toohello 클라우드 서비스 공용 IP 주소 (가상 IP 주소 hello)를 업데이트 합니다.
   3. AD FS 프록시 toouse hello hello AD FS 서버에 대 한 toohello 내부 부하 분산 집합을 해당 하는 FQDN을 구성 합니다.
   4. 클레임 기반 웹 사이트 toouse 업데이트 클레임 공급자에 대 한 외부 FQDN hello 합니다.
7. Hello AD FS 가상 네트워크의 웹 응용 프로그램 프록시 tooany 컴퓨터 간의 액세스를 제한 합니다.

toorestrict 트래픽 hello Azure 내부 부하 분산 장치에 대 한 부하 분산 집합 hello toobe만 트래픽 tooTCP 포트 80 및 443에 대해 구성 되어야 하며 모든 다른 트래픽 toohello 동적의 내부 IP 주소 hello 부하 분산 집합에 대 한 삭제 합니다.

![TCP 443 + 80 허용으로 ADFS 네트워크 ACL의 다이어그램.](media/active-directory-deploying-ws-ad-guidelines/ADFS_ACLs.png)

트래픽 toohello AD FS 서버 hello 원본에 의해서만 허용 됩니다.

* hello Azure 내부 부하 분산 장치입니다.
* hello hello 온-프레미스 네트워크에 대 한 관리자의 IP 주소입니다.

> [!WARNING]
> hello 디자인 hello Azure 가상 네트워크의에서 다른 Vm 또는 hello 온-프레미스 네트워크에 있는 모든 위치에서 웹 응용 프로그램 프록시 노드 하지 못하도록 해야 합니다. Express 경로 연결에 대 한 hello 온-프레미스 어플라이언스 또는 사이트 간 VPN 연결에 대 한 hello VPN 장치에서 방화벽 규칙을 구성 하 여 수행할 수 있습니다.
> 
> 

내부 부하 분산 장치, hello AD FS 서버 및 toohello 가상 네트워크 추가 하는 다른 서버 등의 여러 장치에 대 한 hello 필요 tooconfigure hello 네트워크 Acl을 단점은 toothis 옵션입니다. 장치 네트워크 Acl toorestrict 트래픽 tooit를 구성 하지 않고 toohello 배포를 추가 하 고, 위험 hello 전체 배포 될 수 있습니다. Hello 웹 응용 프로그램 프록시 노드의 hello IP 주소가 변경 되 면 hello 네트워크 Acl 재설정 해야 합니다 (hello 프록시를 의미 하는 구성 된 toouse 해야 [동적 고정 IP 주소](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/)).

![네트워크 ACLS를 사용한 Azure의 ADFS.](media/active-directory-deploying-ws-ad-guidelines/ADFS_Azure.png)

두 번째 방법은 toouse hello [Barracuda NG Firewall](https://www.barracuda.com/products/ngfirewall) AD FS 프록시 서버와 hello AD FS 서버 간의 기기 toocontrol 트래픽입니다. 이 옵션 보안 및 고가용성을 위한 모범 사례를 준수 하며 hello 초기 설치 후에 덜 관리 hello Barracuda NG Firewall 어플라이언스는 방화벽 관리 허용 목록 모드를 제공 하 고 설치할 수 있습니다. Azure 가상 네트워크에서 직접 새 서버를 toohello 배포를 추가 하는 언제 든 지 hello 필요 tooconfigure 네트워크 Acl 제거 하는 합니다. 하지만 이 옵션은 초기 배포의 복잡성과 비용이 있습니다.

이 경우 두 개의 가상 네트워크가 하나 대신 배포됩니다. 이를 VNet1 및 VNet2라고 합니다. VNet1 hello 프록시를 포함 되 고 VNet2 hello Sts와 hello 네트워크 연결 백 toohello 회사 네트워크를 포함 합니다. VNet1 실제로 (하지만 거의) 되므로 VNet2에서 및를 차례로 hello 회사 네트워크에서 격리 합니다. VNet1은 다음 연결 된 tooVNet2 사용 하 여 특수 터널링 기술을 통해로 전송 독립 네트워크 아키텍처 (TINA). hello TINA 터널은 Barracuda NG firewall을 사용 하 여 hello 가상 네트워크의 연결 된 tooeach-hello 가상 네트워크 각각에서 한 Barracuda 합니다.  가용성이 높은 것이 좋습니다; 각 가상 네트워크에 두 개의 Barracudas를 배포 하는 하나의 활성 hello 수동 하나씩 있습니다. Azure에서 기존 온-프레미스 DMZ의 toomimic hello 작업 수 있는 매우 효율적인 방화벽 기능이 제공 합니다.

![방화벽을 사용한 Azure의 ADFS.](media/active-directory-deploying-ws-ad-guidelines/ADFS_Azure_firewall.png)

자세한 내용은 참조 [AD FS: 클레임 인식 온-프레미스 프런트 엔드 응용 프로그램 toohello 인터넷 확장](#BKMK_CloudOnlyFed)합니다.

### <a name="an-alternative-tooad-fs-deployment-if-hello-goal-is-office-365-sso-alone"></a>Hello ´ ֲ Office 365 SSO만 하는 경우에 대체 tooAD FS 배포
목표는만 tooenable 로그인 Office 365에 대 한 다른 대체 toodeploying AD FS 모두가 않습니다. 이 경우 단순히 동기화 온-프레미스 암호를 사용 하 여 디렉터리 동기화를 배포 하는 달성이 방법은 AD FS 또는 Azure 필요 하지 않기 때문에 동일한 최종 결과는 최소한의 배포 복잡성 hello 합니다.

hello 다음 표에서 비교와 AD FS를 배포 하지 않고 hello 로그인 프로세스가 어떻게 작동 합니다.

| AD FS 및 DirSync를 사용하여 Office 365 Single Sign-On | DirSync + 암호 동기화를 사용하여 Office 365 동일한 로그온 |
| --- | --- |
| 1. hello 사용자 tooa 회사 네트워크에 로그온 및 인증 된 tooWindows Server Active Directory는 합니다. |1. hello 사용자 tooa 회사 네트워크에 로그온 및 인증 된 tooWindows Server Active Directory는 합니다. |
| 2. hello 사용자가 Office 365 tooaccess (저는 @contoso.com). |2. hello 사용자가 Office 365 tooaccess (저는 @contoso.com). |
| 3. Office 365 hello 사용자 tooAzure를 AD로 리디렉션합니다. |3. Office 365 hello 사용자 tooAzure를 AD로 리디렉션합니다. |
| 4. Azure AD hello 사용자를 인증할 수 없는 하 고 온-프레미스 AD FS와 트러스트에 대 한 이해를 hello 사용자 tooAD를 FS로 리디렉션합니다. |4. Azure AD는 Kerberos 티켓을 직접 수락할 수 없고 및 트러스트 관계가 없으므로 해당 hello 사용자 자격 증명을 입력 하도록 요청 합니다. |
| 5. hello 사용자 보냅니다는 Kerberos 티켓 toohello AD FS STS 합니다. |5. hello 사용자가 hello 입력 동일한 온-프레미스 암호를 및 Azure AD hello 사용자 이름 및 디렉터리 동기화에 의해 동기화 된 암호에 대해 확인 합니다. |
| 6. AD FS는 Kerberos 티켓 toohello 필요한 토큰 형식/클레임으로 및 hello 사용자 tooAzure AD 리디렉션합니다 hello를 변환 합니다. |6. Azure AD 사용자 tooOffice를 hello 365로 리디렉션합니다. |
| 7. hello 사용자 tooAzure AD가 인증 (됩니다 또 다른 변환이 발생). |7. hello 사용자 tooOffice 365와 OWA hello Azure AD 토큰을 사용 하 여 로그인 할 수 있습니다. |
| 8. Azure AD 사용자 tooOffice를 hello 365로 리디렉션합니다. | |
| 9. hello 사용자가 자동으로 tooOffice 365에 로그인 합니다. | |

Office 365 DirSync와 암호 동기화 시나리오 (AD FS 없음)와 hello에서 single sign on으로 바뀝니다 "동일 로그온" 여기서 "same" 이라는 의미로, 사용자가 Office 365에 액세스할 때 동일한 온-프레미스 자격 증명 입력 다시 해야 합니다. 참고 hello 사용자의 브라우저 toohelp 하 여이 데이터를 기억 될 수 있는 후속 프롬프트를 줄입니다.

### <a name="additional-food-for-thought"></a>추가 고려 사항
* Azure 가상 컴퓨터에서 AD FS 프록시를 배포 하는 경우 연결 toohello AD FS 서버가 필요 합니다. 온-프레미스 인 경우 AD FS 서버와 hello 가상 네트워크 tooallow hello 웹 응용 프로그램 프록시 노드 toocommunicate에서 제공 하는 hello 사이트 간 VPN 연결을 활용 하는 것이 좋습니다.
* Azure 가상에 AD FS 서버를 배포 하는 경우 컴퓨터를 연결 tooWindows Server Active Directory 도메인 컨트롤러, 특성 저장소 및 구성 데이터베이스는 필요 하며 사이트 간 VPN 연결 또는 express 경로도 필요할 수 있습니다. 사이의 hello Azure 가상 네트워크 및 hello 온-프레미스 네트워크입니다.
* 요금이 적용 됩니다 (송신 트래픽)는 Azure 가상 컴퓨터에서 tooall 트래픽입니다. 비용이 주요 요인인 hello 경우 좋습니다 toodeploy hello 웹 응용 프로그램 프록시 노드를 Azure에 AD FS hello 서버 온-프레미스 됩니다. Hello AD FS 서버를 Azure 가상 컴퓨터에 배포 하는 경우 추가 비용이 발생된 tooauthenticate 온-프레미스 사용자가 됩니다. 송신 트래픽에 ExpressRoute hello 또는 hello VPN 사이트 간 연결을 순회 중인지 여부에 관계 없이 비용을 발생 시킵니다.
* Toouse Azure의 기본 서버 부하 분산 AD FS 서버의 고가용성에 대 한 기능을 결정 한 경우 부하 분산 된 hello 클라우드 서비스 내에서 hello 가상 컴퓨터의 사용 되는 toodetermine hello 상태는 프로브를 제공 하는지 note 합니다. (것과 반대로 tooweb 또는 작업자 역할)로 가상 컴퓨터를 Azure의 hello 경우 toohello 기본 프로브 응답 하는 hello 에이전트가 Azure 가상 컴퓨터에 없기 때문에 사용자 지정 프로브 사용 되어야 합니다. 여기에서는 편의 위해 사용자 지정 TCP 프로브를 사용할 수 있습니다-그러기 위해서는 TCP 연결 (TCP SYN 세그먼트 전송 했 고 toowith TCP SYN ACK 세그먼트) 여야 toodetermine 성공적으로 설정 된 가상 컴퓨터 상태입니다. 가상 컴퓨터에서 실제로 수신 대기 하는 TCP 포트 toowhich hello 사용자 지정 프로브 toouse를 구성할 수 있습니다.

> [!NOTE]
> 필요한 tooexpose hello toohello 인터넷 (예: 포트 80 및 443) 공유할 수 없으므로 직접 포트 설정 하는 동일한 컴퓨터는 hello 동일한 클라우드 서비스입니다. 따라서 응용 프로그램에 대 한 포트 요구 사항 및 Windows Server AD FS 사이 겹치는 순서 tooavoid 잠재적인 대로 Windows Server AD FS 서버에 대 한 전용된 클라우드 서비스를 만드는 것이 좋습니다.
> 
> 

## <a name="deployment-scenarios"></a>배포 시나리오
다음 단원을 hello 일반적인 배포 시나리오 toodraw 주의 tooimportant 고려 사항의 요점 계정에는 고려해 야 하는 합니다. 각 시나리오는 hello 결정 사항 및 요인 tooconsider 하는 방법에 대 한 링크 toomore 세부 정보를 포함 합니다.

1. [AD DS: 회사 네트워크 연결에 대한 요구 사항 없이 AD DS 인식 응용 프로그램 배포](#BKMK_CloudOnly)
   
    예를 들어 인터넷 연결 SharePoint 서비스는 Azure 가상 컴퓨터에 배포됩니다. hello 응용 프로그램이 회사 네트워크 리소스에 의존 하지 않습니다. hello 응용 프로그램이 Windows Server AD DS에 필요 하지만 하지 않아도 회사 Windows Server AD DS hello 합니다.
2. [AD FS: 클레임 인식 온-프레미스 프런트 엔드 응용 프로그램 toohello 인터넷 확장](#BKMK_CloudOnlyFed)
   
    예를 들어 온-프레미스 성공적으로 배포 되 고 회사 사용자가 사용 하는 클레임 인식 응용 프로그램 필요 toobecome hello 인터넷에서에서 액세스할 수 있습니다. hello 응용 프로그램은 자체 회사 id를 사용 하 여 비즈니스 파트너와 기존 회사 사용자 hello 인터넷을 통해 직접 액세스 toobe가 필요 합니다.
3. [AD DS: toohello 회사 네트워크 연결을 필요로 하는 Windows Server AD DS 인식 응용 프로그램 배포](#BKMK_HybridExt)
   
    예를 들어 Windows 통합 인증을 지원하고 구성 및 사용자 프로필 데이터에 대한 리포지토리로 Windows Server AD DS를 사용하는 LDAP 인식 응용 프로그램은 Azure 가상 컴퓨터에 배포됩니다. 기존의 회사 Windows Server AD DS hello 응용 프로그램 tooleverage hello 바람직하지 이며 single sign on 제공 합니다. hello 응용 프로그램은 클레임 인식 되지 않습니다.

### <a name="BKMK_CloudOnly"></a>1. AD DS: 회사 네트워크 연결에 대한 요구 사항 없이 AD DS 인식 응용 프로그램 배포
![클라우드 전용 AD DS 배포](media/active-directory-deploying-ws-ad-guidelines/ADDS_cloud.png)
**그림 1**

#### <a name="description"></a>설명
SharePoint가 Azure 가상 컴퓨터에 배포 하 고 hello 응용 프로그램이 회사 네트워크 리소스에 대 한 종속성이 없습니다. hello 응용 프로그램에서 필요 않도록 지정 되었으나 Windows Server AD DS *하지* 필요 회사 Windows Server AD DS hello 합니다. Kerberos 또는 페더레이션된 트러스트가 없습니다는 사용자가 자체 hello 클라우드의 Azure 가상 컴퓨터에도 호스트 된 hello Windows Server AD DS 도메인으로 hello 응용 프로그램을 통해 프로 비전 하기 때문에 필요 합니다.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>시나리오 고려 사항 및 기술 영역 toohello 시나리오를 적용 하는 방법
* [네트워크 토폴로지](#BKMK_NetworkTopology): 크로스-프레미스 연결(사이트 간 연결이라고도 함) 없이 Azure 가상 네트워크를 만듭니다.
* [DC 배포 구성](#BKMK_DeploymentConfig): 새로운 단일 도메인 Windows Server Active Directory 포리스트에 새 도메인 컨트롤러를 배포합니다. 이것은 hello Windows DNS 서버와 함께 배포 되어야 합니다.
* [Windows Server Active Directory 사이트 토폴로지](#BKMK_ADSiteTopology): 사용 하 여 hello 기본 Windows Server Active Directory 사이트 (모든 컴퓨터는 기본 첫 번째-사이트 이름에).
* [IP 주소 지정 및 DNS](#BKMK_IPAddressDNS):
  
  * Hello Set-azurestaticvnetip Azure PowerShell cmdlet을 사용 하 여 hello DC에 대 한 고정 IP 주소를 설정 합니다.
  * 설치 및 Windows Server DNS를 Azure에서 도메인 컨트롤러 hello 구성.
  * Hello 이름과 hello hello DC 및 DNS 서버 역할을 호스팅하는 VM의 IP 주소로 hello 가상 네트워크 속성을 구성 합니다.
* [글로벌 카탈로그](#BKMK_GC): hello hello 포리스트의 첫 번째 DC 이어야 합니다는 글로벌 카탈로그 서버입니다. 단일 도메인 포리스트에서 글로벌 카탈로그 hello hello DC에서에서 추가 작업 필요 하지 않기 때문에 추가 Dc Gc로도 구성 해야 합니다.
* [Hello Windows Server AD DS 데이터베이스 및 SYSVOL의 배치](#BKMK_PlaceDB): 순서 toostore hello Windows Server Active Directory 데이터베이스, 로그 및 SYSVOL의 Azure Vm으로 실행 되는 데이터 디스크 tooDCs를 추가 합니다.
* [백업 및 복원](#BKMK_BUR): toostore 시스템 상태 백업 위치를 결정 합니다. 필요한 경우 다른 데이터 디스크 toohello DC VM toostore 백업을 추가 합니다.

### <a name="BKMK_CloudOnlyFed"></a>2의 AD FS: 클레임 인식 온-프레미스 프런트 엔드 응용 프로그램 toohello 인터넷 확장
![크로스-프레미스 연결로 페더레이션](media/active-directory-deploying-ws-ad-guidelines/Federation_xprem.png)
**그림 2**

#### <a name="description"></a>설명
온-프레미스 성공적으로 배포 되 고 회사 사용자에 게 요구 toobecome hello 인터넷에서 직접 액세스 하 여 사용 하는 클레임 인식 응용 프로그램입니다. hello 응용 프로그램 데이터를 저장 하는 웹 프런트 엔드 tooa SQL 데이터베이스 역할을 합니다. hello 응용 프로그램에서 사용 하는 hello SQL 서버 hello 회사 네트워크에도 있습니다. 두 개의 Windows Server AD FS Sts 및 부하 분산 장치가 온-프레미스 배포 tooprovide 액세스 toohello 회사 사용자에 게 되었습니다. 이제 hello 응용 프로그램은 자체 회사 id를 사용 하 여 비즈니스 파트너와 기존 회사 사용자 hello 인터넷을 통해 직접 추가로 액세스 toobe가 필요 합니다.

노력 toosimplify 및이 새로운 요구 사항의 배포 및 구성 요구를 충족 hello 결정 했습니다 추가 웹 프런트 엔드 및 두 개의 Windows Server AD FS 프록시 서버는 Azure 가상 컴퓨터에 설치할 수 있습니다. 모든 4 개의 Vm 됩니다 toohello 인터넷에 직접 노출 하 고 연결 toohello 온-프레미스 네트워크를 Azure 가상 네트워크의 사이트 간 VPN 기능을 사용 하 여 제공 됩니다.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>시나리오 고려 사항 및 기술 영역 toohello 시나리오를 적용 하는 방법
* [네트워크 토폴로지](#BKMK_NetworkTopology): Azure 가상 네트워크를 만들고 [크로스-프레미스 연결을 구성합니다](../vpn-gateway/vpn-gateway-site-to-site-create.md).
  
  > [!NOTE]
  > 각각의 hello Windows Server AD FS 인증서에 대 한 hello URL 내에 정의 된 hello 인증서 템플릿 및 hello 결과 인증서를 Azure에서 실행 되는 Windows Server AD FS hello 인스턴스를 통해 연결할 수 있는지 확인 합니다. PKI 인프라의 크로스-프레미스 연결 tooparts가 필요할 수 있습니다. 예제 hello CRL의 끝점이 LDAP 기반이 고 단독으로 온-프레미스에 호스트 되는 경우 다음 크로스-프레미스 연결 해야 합니다. 필요 없는 경우 hello 인터넷을 통해 해당 CRL을 액세스할 수 있는 CA에서 발급 한 toouse 필요한 인증서 수 있습니다.
  > 
  > 
* [클라우드 서비스 구성](#BKMK_CloudSvcConfig): 두 개의 부하 분산된 가상 IP 주소를 제공하기 위해 두 개의 클라우드 서비스가 있는지 확인합니다. hello 첫 번째 클라우드 서비스의 가상 IP 주소 toohello 방향이 지정 된 두 명의 Windows Server AD FS 프록시 Vm으로 포트 80 및 443 됩니다. hello Windows Server AD FS 프록시 Vm 됩니다 구성 hello Windows Server AD FS Sts를 향한은 hello 온-프레미스 부하 분산 장치의 toopoint toohello IP 주소. hello 두 번째 클라우드 서비스의 가상 IP 주소에 포트 80 및 443에서 hello 웹 프런트 엔드를 다시 실행 하는 방향이 지정 된 toohello 두 Vm 됩니다. 사용자 지정 프로브를 구성 tooensure hello 부하 분산 장치에 트래픽을 toofunctioning Windows Server AD FS 프록시와 웹 프런트 엔드 Vm 으로만 전송 합니다.
* [페더레이션 서버 구성](#BKMK_FedSrvConfig): hello 클라우드에서 만든 hello Windows Server Active Directory 포리스트에 대 한 구성 Windows Server AD FS 페더레이션 서버 (STS) toogenerate 보안 토큰입니다. Tooaccept id를 원하는 다른 파트너를 hello와 페더레이션 클레임 공급자 트러스트 관계를 설정 하 고 hello 다른 응용 프로그램에 대 한 toogenerate 토큰을 원하는 신뢰 당사자 트러스트 관계를 구성 합니다.
  
    대부분의 시나리오에서 Windows Server AD FS 프록시 서버는 보안용으로 인터넷 연결 용량에 배포되는 반면 해당 Windows Server AD FS 페더레이션 항목은 직접 인터넷 연결에서 격리됩니다. 배포 시나리오에 관계 없이 공개적으로 노출 된 IP 주소 및 포트 수를 tooload 분산으로가지고 있는 두 개의 Windows Server AD FS STS 인스턴스 또는 프록시 인스턴스를 제공 하는 가상 IP 주소와 함께 클라우드 서비스를 구성 해야 합니다.
* [Windows Server AD FS 고가용성 구성](#BKMK_ADFSHighAvail): 것이 좋습니다 toodeploy 장애 조치 및 부하 분산에 대 한 두 개 이상의 서버가 포함 된 Windows Server AD FS 팜을 합니다. Hello 내부의 부하 분산 기능 Azure toodistribute 들어오는 요청 hello 팜의 서버에서 hello 사용 하 tooconsider hello 내부 데이터베이스 WID (Windows)를 사용 하 여 Windows Server AD FS 구성 데이터에 사용할 수 있습니다.

자세한 내용은 참조 hello [AD DS 배포 가이드](https://technet.microsoft.com/library/cc753963)합니다.

### <a name="BKMK_HybridExt"></a>3. AD DS: toohello 회사 네트워크 연결을 필요로 하는 Windows Server AD DS 인식 응용 프로그램 배포
![크로스-프레미스 AD DS 배포](media/active-directory-deploying-ws-ad-guidelines/ADDS_xprem.png)
**그림 3**

#### <a name="description"></a>설명
LDAP 인식 응용 프로그램이 Azure 가상 컴퓨터에 배포됩니다. Windows 통합 인증을 지원하고 구성 및 사용자 프로필 데이터에 대한 리포지토리로 Windows Server AD DS를 사용합니다. hello 목표 hello 응용 프로그램 tooleverage hello 기존의 회사 Windows Server AD DS 하며 single sign on 제공 합니다. hello 응용 프로그램은 클레임 인식 되지 않습니다. 사용자가 hello 인터넷에서 직접 tooaccess hello 응용 프로그램이 있어야 합니다. toooptimize 성능 및 비용에 대 한 결정 했습니다 hello 회사 도메인의 일부인 두 명의 추가 도메인 컨트롤러를 Azure의 hello 응용 프로그램과 함께 배포 하는 것입니다.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>시나리오 고려 사항 및 기술 영역 toohello 시나리오를 적용 하는 방법
* [네트워크 토폴로지](#BKMK_NetworkTopology): [크로스-프레미스 연결](../vpn-gateway/vpn-gateway-site-to-site-create.md)로 Azure 가상 네트워크를 만듭니다.
* [설치 방법](#BKMK_InstallMethod): hello 회사 Windows Server Active Directory 도메인의 복제본 Dc를 배포 합니다. 복제본 DC에 대 한 VM hello에 Windows Server AD DS를 설치할 수 있습니다 및 toobe 필요한 데이터를 사용 하 여 hello 설치 IFM (미디어에서) 기능 tooreduce hello 양 toohello를 복제 하는 선택적으로 설치 하는 동안 새 DC입니다. 자습서는 [Azure에서 복제 Active Directory 도메인 컨트롤러 설치](active-directory-install-replica-active-directory-domain-controller.md)를 참조하세요. IFM을 사용 하는 경우에 보다 효율적인 toobuild hello 가상 DC 온-프레미스 및 Windows Server AD DS를 설치 하는 동안 복제 하는 대신 hello 전체 가상 하드 디스크 (VHD) toohello 클라우드를 이동할 수 있습니다. 보안을 위해 복사한 tooAzure 되 면 hello 온-프레미스 네트워크에서 VHD hello을 삭제 하는 것이 좋습니다.
* [Windows Server Active Directory 사이트 토폴로지](#BKMK_ADSiteTopology): Active Directory 사이트 및 서비스에서 새로운 Azure 사이트를 만듭니다. Windows Server Active Directory 서브넷 개체 toorepresent hello Azure 가상 네트워크를 만들고 hello 서브넷 toohello 사이트를 추가 합니다. Hello 새로운 Azure 사이트와는 hello Azure 가상 네트워크 VPN 끝점이 \ 순서 toocontrol hello 사이트를 포함 하 고 Azure에서 Windows Server Active Directory 트래픽을 tooand를 최적화 하는 새 사이트 링크를 만듭니다.
* [IP 주소 지정 및 DNS](#BKMK_IPAddressDNS):
  
  * Hello Set-azurestaticvnetip Azure PowerShell cmdlet을 사용 하 여 hello DC에 대 한 고정 IP 주소를 설정 합니다.
  * 설치 및 Windows Server DNS를 Azure에서 도메인 컨트롤러 hello 구성.
  * Hello 이름과 hello hello DC 및 DNS 서버 역할을 호스팅하는 VM의 IP 주소로 hello 가상 네트워크 속성을 구성 합니다.
* [지리적으로 분산된 DC](#BKMK_DistributedDCs): 필요에 따라 추가 가상 네트워크를 구성합니다. Active Directory 사이트 토폴로지 toodifferent Azure 해당 하는 지역에 dc가 필요한 경우 영역 보다 적절 하 게 toocreate Active Directory 사이트를 선택 합니다.
* [읽기 전용 Dc](#BKMK_RODC): Rodc와 hello 사이트의 hello DC 및 hello 호환성에 대 한 응용 프로그램 및 서비스 작업 쓰기를 수행 하기 위한 요구 사항에 따라 hello Azure 사이트에서에서 RODC를 배포할 수 있습니다. 응용 프로그램 호환성에 대 한 자세한 내용은 참조 hello [읽기 전용 도메인 컨트롤러 응용 프로그램 호환성 가이드](https://technet.microsoft.com/library/cc755190)합니다.
* [글로벌 카탈로그](#BKMK_GC): Gc는 다중 도메인 포리스트에서 로그온 요청 필요한 tooservice 합니다. Hello Azure 사이트에서에서 GC를 배포 하지 않는 경우 인증 요청 다른 사이트의 Gc를 쿼리해야 하면 송신 트래픽 비용이 시 합니다. 트래픽는 toominimize, Active Directory 사이트 및 서비스에서 Azure 사이트 hello에 대 한 캐싱을 유니버설 그룹 구성원을 사용할 수 있습니다.
  
    GC를 배포 하는 경우 사이트 링크를 구성 하 고 hello Azure 사이트에서에서 GC hello tooreplicate 해야 하는 다른 Gc에서 원본 DC로 선호 되지 않도록 사이트 링크 비용 동일한 부분 도메인 파티션을 hello 합니다.
* [Hello Windows Server AD DS 데이터베이스 및 SYSVOL의 배치](#BKMK_PlaceDB): 순서 toostore hello Windows Server Active Directory 데이터베이스, 로그 및 SYSVOL의 Azure Vm에서 실행 되는 데이터 디스크 tooDCs를 추가 합니다.
* [백업 및 복원](#BKMK_BUR): toostore 시스템 상태 백업 위치를 결정 합니다. 필요한 경우 다른 데이터 디스크 toohello DC VM toostore 백업을 추가 합니다.

## <a name="deployment-decisions-and-factors"></a>배포 결정 및 요인
이 테이블에는 hello Windows Server Active Directory 기술 영역 hello 시나리오 앞에 영향을 및 아래에 링크 toomore 자세히와 해당 결정 tooconsider hello에 요약 되어 있습니다. 어떤 기술 영역은 하지 않을 수 tooevery 적용 가능한 배포 시나리오에서는 있으며 어떤 기술 영역은 다른 기술 영역 보다 더 중요 tooa 배포 시나리오를 수 있습니다.

예를 들어 가상 네트워크에서 복제본 DC를 배포 하 고 포리스트에 단일 도메인에 다음 toodeploy 글로벌 카탈로그 서버 선택이 경우 됩니다 중요 한 toohello 배포 시나리오는 추가적인 복제를 만들지 않으므로 요구 사항입니다. 에 hello 포리스트에 여러 도메인이 다른 손 hello에 다음 hello 의사 결정 toodeploy 가상 네트워크에 글로벌 카탈로그는 사용 가능한 대역폭, 성능, 인증, 디렉터리 조회 등에 영향을 줄 수 있습니다.

| Windows Server Active Directory 기술 영역 | 의사 결정 | 요소 |
| --- | --- | --- |
| [네트워크 토폴로지](#BKMK_NetworkTopology) |가상 네트워크를 만듭니까? |<li>요구 사항 tooaccess Corp 리소스</li> <li>인증</li> <li>계정 관리</li> |
| [DC 배포 구성](#BKMK_DeploymentConfig) |<li>트러스트 없이 별도 포리스트를 배포합니까?</li> <li>페더레이션이 포함된 새 포리스트를 배포합니까?</li> <li>Windows Server Active Directory 포리스트 트러스트 또는 Kerberos가 포함된 새 포리스트를 배포합니까?</li> <li>복제본 DC를 배포하여 회사 포리스트를 확장합니까?</li> <li>새 자식 도메인 또는 도메인 트리를 배포하여 회사 포리스트를 확장합니까?</li> |<li>보안</li> <li>규정 준수</li> <li>비용</li> <li>복원력 및 내결함성</li> <li>응용 프로그램 호환성</li> |
| [Windows Server Active Directory 사이트 토폴로지](#BKMK_ADSiteTopology) |어떻게 하면 toooptimize 트래픽이 Azure 가상 네트워크 서브넷, 사이트 및 사이트 링크를 구성 하 고 비용을 최소화? |<li>서브넷 및 사이트 정의</li> <li>사이트 링크 속성 및 변경 알림</li> <li>복제 압축</li> |
| [IP 주소 지정 및 DNS](#BKMK_IPAddressDNS) |Tooconfigure IP 주소 하 고 이름 확인을 어떻게? |<li>Hello 사용 하 여 hello Set-azurestaticvnetip cmdlet tooassign 고정 IP 주소를 사용 하 여</li> <li>Windows Server DNS 서버를 설치 하 고 hello 이름과 hello hello DC 및 DNS 서버 역할을 호스팅하는 VM의 IP 주소로 hello 가상 네트워크 속성을 구성 합니다.</li> |
| [지리적으로 분산된 DC](#BKMK_DistributedDCs) |어떻게에 tooreplicate tooDCs 가상로 네트워크 구분? |Active Directory 사이트 토폴로지 toodifferent Azure의 해당 지역에 dc가 필요한 경우 영역 보다 적절 하 게 toocreate Active Directory 사이트를 선택 합니다. [가상 네트워크 toovirtual 네트워크 연결 구성](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) 별도 가상 네트워크에 도메인 컨트롤러 간 tooreplicate 합니다. |
| [읽기 전용 DC](#BKMK_RODC) |읽기 전용 또는 쓰기 가능 DC를 사용합니까? |<li>HBI/PII 특성 필터링</li> <li>암호 필터링</li> <li>아웃바운드 트래픽 제한</li> |
| [글로벌 카탈로그](#BKMK_GC) |글로벌 카탈로그를 설치합니까? |<li>단일 도메인 포리스트의 경우 모든 DC GC를 만듭니다.</li> <li>다중 도메인 포리스트의 경우 인증에 GC가 필요합니다.</li> |
| [설치 방법](#BKMK_InstallMethod) |어떻게 Azure에서 DC tooinstall? |다음 중 한 방법으로 찾을 수 있습니다. <li>Windows PowerShell 또는 Dcpromo를 사용하여 AD DS 설치</li> <li>온-프레미스 가상 DC의 VHD 이동</li> |
| [Hello Windows Server AD DS 데이터베이스 및 SYSVOL의 배치](#BKMK_PlaceDB) |여기서 toostore Windows Server AD DS 데이터베이스, 로그 및 SYSVOL? |Dcpromo.exe 기본값을 변경합니다. 이러한 중요한 Active Directory 파일은 쓰기 캐싱을 구현하는 운영 체제 디스크 대신 Azure Data Disks에 배치 *되어야* 합니다. |
| [백업 및 복원](#BKMK_BUR) |어떻게 toosafeguard 및 복구 데이터? |시스템 상태 백업 만들기 |
| [페더레이션 서버 구성](#BKMK_FedSrvConfig) |<li>Hello 클라우드에서 페더레이션이 포함 된 새 포리스트를 배포 합니까?</li> <li>온-프레미스 AD FS를 배포 하 고 hello 클라우드에서 프록시를 노출?</li> |<li>보안</li> <li>규정 준수</li> <li>비용</li> <li>비즈니스 파트너에 의해 액세스 tooapplications</li> |
| [클라우드 서비스 구성](#BKMK_CloudSvcConfig) |클라우드 서비스는 암시적으로 배포 하는 가상 컴퓨터를 만들면 처음으로 hello 합니다. Toodeploy 추가 클라우드 서비스를 필요 한가요? |<li>VM 또는 Vm에 직접 표시 toohello 인터넷 필요 합니까?</li> <li> 부하 분산 hello 서비스 필요 합니까?</li> |
| [공용 및 개인 IP 주소 지정(동적 IP 및 가상 IP)에 대한 페더레이션 서버 요구 사항](#BKMK_FedReqVIPDIP) |<li>Windows Server AD FS hello 인스턴스 toobe hello 인터넷에서 직접 액세스 해야 합니까?</li> <li>Hello 클라우드에서 배포 되는 hello 응용 프로그램에 고유한 인터넷 연결 IP 주소와 포트 필요 합니까?</li> |배포에 필요한 각 가상 IP 주소에 대한 단일 클라우드 서비스 만들기 |
| [Windows Server AD FS 고가용성 구성](#BKMK_ADFSHighAvail) |<li>Windows Server AD FS 서버 팜에 있는 노드는 몇 개입니까?</li> <li>내 Windows Server AD FS 프록시 팜에 노드 toodeploy 몇 개입니까?</li> |복원력 및 내결함성 |

### <a name="BKMK_NetworkTopology"></a>네트워크 토폴로지
순서 toomeet hello IP 주소 일관성과 DNS 요구 사항을 Windows Server AD DS는 toofirst 만들기는 [Azure 가상 네트워크](../virtual-network/virtual-networks-overview.md) 및 가상 컴퓨터 tooit 연결 합니다. 투명 하 게 연결 Azure 가상 네트워크 컴퓨터 tooon 온-프레미스 컴퓨터 toooptionally 연결 tooyour 온-프레미스 회사를 확장 하는지 여부를 결정 해야를 만드는 동안 — 기존 VPN 기술을 사용 하 여 그렇게 하 고 VPN 끝점 hello hello 회사 네트워크 가장자리에서 노출 되어야 필요 합니다. 즉, VPN hello 하지 반대로 Azure toohello 회사 네트워크에서 시작 됩니다.

Note 초과 hello 표준 요금 tooeach VM 가상 네트워크 tooyour 온-프레미스 네트워크를 확장 하는 경우 추가 요금이 적용 됨. 특히, hello VPN에서 온-프레미스 컴퓨터와 통신 하는 각 VM에서 생성 하는 송신 트래픽에 hello 및 hello Azure 가상 네트워크 게이트웨이의 CPU 시간에 대 한 요금이 있습니다. 네트워크 트래픽 요금에 대한 자세한 내용은 [한눈에 보는 Azure 가격 책정](http://azure.microsoft.com/pricing/)을 참조하세요.

### <a name="BKMK_DeploymentConfig"></a>DC 배포 구성
hello hello 서비스에 대 한 hello 요구 사항에 따라 달라 집니다 DC를 구성 하는 hello 방법은 Azure에서 toorun을 합니다. 예를 들어 회사 포리스트에서 분리, 새 포리스트를 배포할 수 있는, toointernal 회사 리소스에 특정 하지 않은 액세스 하지만 디렉터리 서비스를 필요로 하는의 개념 증명, 새 응용 프로그램 또는 일부 기타 단기 프로젝트를 테스트 합니다.

가지이 점으로, 분리 된 포리스트 DC를 복제 하지 않는 온-프레미스 Dc hello 시스템 자체에서 생성 되는 아웃 바운드 네트워크 트래픽을 직접 비용을 절감 합니다. 네트워크 트래픽 요금에 대한 자세한 내용은 [한눈에 보는 Azure 가격 책정](http://azure.microsoft.com/pricing/)을 참조하세요.

또 다른 예로 서비스에 대 한 개인 정보 보호 요구 사항이 있는 있고 hello 서비스 액세스 tooyour에 종속 되어 있다고 가정 내부 Windows Server Active Directory 합니다. Hello 클라우드에서 hello 서비스에 대 한 toohost 데이터, 허용 되는 경우 Azure에서 내부 포리스트에 대해 새 자식 도메인을 배포할 수 있습니다. 이 경우 hello 순서 toohelp 주소 개인 정보 보호 문제가에 글로벌 카탈로그) (없이 새로운 자식 도메인을 hello에 대 한 DC를 배포할 수 있습니다. 이 시나리오에서는 복제본 DC 배포와 함께 온-프레미스 DC와 연결하기 위한 가상 네트워크가 필요합니다.

새 포리스트를 만들 경우 선택 여부 toouse [Active Directory 트러스트](https://technet.microsoft.com/library/cc771397) 또는 [페더레이션 트러스트](https://technet.microsoft.com/library/dd807036)합니다. 호환성, 보안, 규정 준수, 비용 및 복원 력으로 지정 된 hello 요구 사항의 균형을 조정 합니다. 예를 들어 tootake 활용 [선택적 인증](https://technet.microsoft.com/library/cc755844) toodeploy Azure에서 새 포리스트를 선택 하 고 hello 온-프레미스 포리스트와 클라우드 포리스트 hello 간에 Windows Server Active Directory 트러스트를 만들 수 있습니다. 그러나 hello 응용 프로그램은 클레임 인식, Active Directory 포리스트 트러스트 대신 페더레이션 트러스트를 배포할 수 있습니다. 또 다른 요인은 hello 비용 tooeither replicate 더 많은 데이터가 온-프레미스 Windows Server Active Directory toohello 클라우드를 확장 하 여 될 되거나 아웃 바운드 트래픽을 더 인증 및 쿼리 로드의 결과로 생성 됩니다.

가용성 및 내결함성에 대한 요구 사항은 선택에도 영향을 줍니다. 예를 들어 hello 링크 중단 되 면 Kerberos 트러스트 또는 페더레이션 트러스트를 활용 하는 응용 프로그램은 모든 가능성이 않는 한 완전히 작동 Azure에 충분 한 인프라가 배포 합니다. 복제본 Dc와 같은 대체 배포 구성은 (쓰기 가능 또는 Rodc) 수 tootolerate 링크 중단 되 고 hello 가능성이 증가 합니다.

### <a name="BKMK_ADSiteTopology"></a>Windows Server Active Directory 사이트 토폴로지
하면 필요한 toocorrectly 정의 사이트 및 사이트 링크 순서 toooptimize 트래픽 고 비용을 최소화 합니다. 사이트, 사이트 링크 및 서브넷 Dc와 인증 트래픽 흐름 hello 간의 hello 복제 토폴로지에 영향을 줍니다. 트래픽 요금에 따라 hello 고려 배포 및 배포 시나리오의 toohello 요구 사항에 따라 Dc 구성:

* Hello 게이트웨이 자체에 대 한 시간당 아주 적은 수수료가 있습니다.
  
  * 필요에 따라 시작 및 중지할 수 있습니다.
  * Azure Vm은 hello 회사 네트워크에서 분리를 중지 하면
* 인바운드 트래픽은 무료입니다.
* 아웃 바운드 트래픽을 너무에 따라 청구 됩니다[가격에서 요약 Azure](http://azure.microsoft.com/pricing/)합니다. 다음과 같이 온-프레미스 사이트와 hello 클라우드 사이트 간의 사이트 링크 속성을 최적화할 수 있습니다.
  
  * 여러 개의 가상 네트워크를 사용 하는 경우 구성 hello 사이트 링크 및 비용과 우선 순위를 정하여 hello Azure에서에서 Windows Server AD DS tooprevent 하나 위에 동일한 수준의 서비스 비용 없이 hello를 제공할 수 있는 사이트 적절 하 게 합니다. 모든 사이트 링크 (BASL) 옵션 (기본적으로 활성화 되어) hello 브리지를 사용 하지 않도록 설정 고려할 수 있습니다. 이렇게 하면 직접 연결된 사이트만 서로 복제합니다. 전이적으로 연결 된 사이트의 Dc는 더 이상 서로 직접 공동 수 tooreplicate 하지만 공통 사이트 또는 사이트를 통해 복제 해야 합니다. 어떤 이유로 중개 사이트 hello 없게, 전이적으로 연결 된 사이트의 Dc 간 복제 hello 사이트 간 연결을 사용할 수 있는 경우에 발생 하지 않습니다. 마지막으로, 섹션 전이적 복제 동작이 바람직한을 유지 하는 경우 사이트 링크 브리지를 만듭니다 hello 적절 한 사이트 링크와 사이트, 온-프레미스, 회사 네트워크 사이트를 포함 하는 합니다.
  * [사이트 링크 비용 구성](https://technet.microsoft.com/library/cc794882) 적절 하 게 tooavoid 의도 하지 않은 트래픽을 합니다. 예를 들어 경우 **가장 가까운 다음 사이트 시도** 설정을 사용 하는, hello Azure 사이트 백 toohello를 연결 하는 hello 사이트 링크 개체와 관련 된 hello 비용을 증가 시켜 사이트는 다음 hello 되지 있는지 hello 가상 네트워크를 가장 가까운 확인 회사 네트워크입니다.
  * 사이트 링크를 구성 [간격](https://technet.microsoft.com/library/cc794878) 및 [일정](https://technet.microsoft.com/library/cc816906) tooconsistency 요구 사항과 개체 변경 비율에 따라 합니다. 복제 일정을 대기 시간 허용치에 맞춥니다. Dc는 hello 복제 간격 감소 이면 충분 한 개체 변경 비율 비용을 절약할 수 있으므로 값의 마지막 상태 hello만 복제 됩니다.
* 비용 최소화가 매우 중요한 경우 복제가 예약되었고 변경 알림이 활성화되지 않았는지 확인합니다. 사이트 간 복제 시 hello 기본 구성입니다. 이 hello RODC는 아웃 바운드 변경을 복제 하지 않습니다는 RODC를 가상 네트워크에 배포 하는 경우에 중요 하지 않습니다. 하지만 쓰기 가능 DC를 배포 하는 경우 hello 사이트 링크 불필요 한 빈도로 구성된 tooreplicate 업데이트 아닌지 확인 해야 합니다. (GC) 글로벌 카탈로그 서버를 배포 하는 경우는 GC가 포함 된 다른 모든 사이트가 원본 사이트 링크를 통해 연결 된 사이트의 DC에서에서 도메인 파티션을 복제 또는 hello Azure 사이트를 hello의 GC 보다 비용이 낮은 사이트 링크에 있는지 확인 합니다.
* 수 toofurther는 여전히 hello 복제 압축 알고리즘을 변경 하 여 사이트 간 복제에 의해 발생 하는 네트워크 트래픽이 감소 합니다. hello 압축 알고리즘 hello REG_DWORD 레지스트리 항목 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Replicator compression algorithm으로 제어 됩니다. hello 기본값은 3, toohello Xpress 압축 알고리즘을 연관 시킵니다. 변경 내용을 hello 알고리즘 tooMSZip hello 값 too2, 변경할 수 있습니다. 대부분의 경우에서 이렇게 하면 hello 압축 증가 하지만 CPU 사용률의 hello 부담을 수행 합니다. 자세한 내용은 [Active Directory 복제 토폴로지 작동 방법](https://technet.microsoft.com/library/cc755994)을 참조하세요.

### <a name="BKMK_IPAddressDNS"></a>IP 주소 지정 및 DNS
Azure 가상 컴퓨터는 기본적으로 "DHCP 임대 주소"로 할당됩니다. Azure 가상 네트워크 동적 주소가 가상 컴퓨터와 hello 가상 컴퓨터의 hello 수명 동안 지속, 되기 때문에 Windows Server AD DS의 hello 요구 사항이 충족 됩니다.

결과적으로, Azure에서 동적 주소를 사용 하는 경우 hello 임대 기간 동안 hello 라우팅할 수이 고 hello 임대 기간이 hello는 hello 클라우드 서비스의 수명과 같은 toohello 때문에 고정 IP 주소를 사용 하는 있습니다.

그러나 hello VM이 종료 하는 경우 hello 동적 주소가 할당 됩니다. tooprevent hello IP 주소 할당 취소를 할 수 있습니다 [Set-azurestaticvnetip tooassign 고정 IP 주소를 사용 하 여](http://social.technet.microsoft.com/wiki/contents/articles/23447.how-to-assign-a-private-static-ip-to-an-azure-vm.aspx)합니다.

이름 확인을 위해 배포 사용자 고유의 (또는 기존 활용) DNS 서버 인프라; Azure 제공 DNS 이름 확인 요구 사항을 Windows Server AD DS의 고급 hello를 충족 하지 않습니다. 예를 들어 동적 SRV 레코드 등을 지원하지 않습니다. 이름 확인은 DC 및 도메인에 가입된 클라이언트에 대한 중요한 구성 항목입니다. DC는 리소스 레코드를 등록하고 다른 DC의 리소스 레코드를 해결해야 합니다.
내결함성과 성능상의 이유로 것은 Azure에서 실행 하는 hello Dc 최적의 tooinstall hello Windows Server DNS 서비스입니다. Hello 이름과 hello DNS 서버의 IP 주소가 있는 hello Azure 가상 네트워크 속성을 구성 합니다. Hello 가상 네트워크의 다른 Vm 시작 hello 동적 IP 주소 할당의 일부로 DNS 서버를 통해 해당 DNS 클라이언트 확인자 설정이 구성 됩니다.

> [!NOTE]
> Hello 인터넷을 통해 직접 Azure에서 호스트 되는 온-프레미스 컴퓨터 tooa Windows Server AD DS Active Directory 도메인에 가입할 수 없습니다. Active Directory 및 도메인 가입 작업 hello 렌더링 비현실적 toodirectly 노출 hello 필요한 포트에 대 한와 사실상 전체 DC toohello 인터넷 포트 요구 사항 hello 합니다.
> 
> 

VM은 시작 시 또는 이름 변경 내용이 있을 때 자동으로 해당 DNS 이름을 등록합니다.

이 예제에서 및 tooprovision 첫 번째 VM hello 하 고에 AD DS를 설치 하는 방법을 보여 주는 또 다른 예에 대 한 자세한 내용은 참조 [Microsoft Azure에서 새로운 Active Directory 포리스트 설치](active-directory-new-forest-virtual-machine.md)합니다. Windows PowerShell 사용에 대한 자세한 내용은 [Azure PowerShell 설치](/powershell/azureps-cmdlets-docs) 및 [Azure 관리 Cmdlet](/powershell/module/azurerm.compute/#virtual_machines)을 참조하세요.

### <a name="BKMK_DistributedDCs"></a>지리적으로 분산된 DC
Azure는 서로 다른 가상 네트워크에 여러 DC를 호스팅하는 경우 이점을 제공합니다.

* 다중 사이트 내결함성
* 물리적으로 접근 toobranch 사무실 (낮은 대기 시간)

가상 네트워크 간의 직접 통신을 구성 하는 방법에 대 한 정보를 참조 하십시오. [가상 네트워크 toovirtual 네트워크 연결을 구성](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)합니다.

### <a name="BKMK_RODC"></a>읽기 전용 DC
Toodeploy 읽기 지 toochoose 필요-유일한 아니면 쓰기 가능 Dc입니다. 물리적으로 제어를 없을 것 이지만 Rodc는 위험한 클라이언트, 지점과 같이 물리적 보안 위치에서 배포 하는 디자인 된 toobe 때문에 저장할된 toodeploy Rodc를 수 있습니다.

Azure hello 분기 지점의 물리적 보안 위험을 표시 하지 않는 않지만 Rodc 있습니다 toobe 비용 효율이 hello 지 원하는 기능으로는 전혀 다른 이유로 하지만 잘 맞는 toothese 환경 때문에 있습니다. 예를 들어 Rodc에는 아웃 바운드 복제 하지을 수 tooselectively 됩니다 한 암호 (암호)를 채웁니다. 이 암호가 없는 hello hello 단점은에서 요청 시 아웃 바운드 트래픽을 toovalidate 필요할 수 있습니다 때 사용자 또는 컴퓨터를 인증 합니다. 그러나 암호는 선택적으로 미리 채워지고 캐시할 수 있습니다.

Rodc 중요 한 데이터 toohello RODC 포함 된 특성 된 특성 집합 fas (복제가)를 추가할 수 있으므로에 그리고 HBI 및 PII 문제와 관련 하 여 추가 이점을 제공 합니다. hello FAS는 사용자 지정 가능한 집합 복제 tooRODCs 없는 특성입니다. 허용 되지 않거나 toostore PII 또는 HBI Azure에서 원하지 않는 경우 hello FAS를 안전 장치로 사용할 수 있습니다. 자세한 내용은 RODC 필터링된 특성 집합[(https://technet.microsoft.com/library/cc753459)]을 참조하세요.

응용 프로그램이 Rodc와 호환 되도록 확인 toouse를 계획 합니다. 많은 Windows Server Active Directory 사용 응용 프로그램, Rodc와 잘 작동 하지만 일부 응용 프로그램 액세스 tooa 없는 경우 실패 또는 비효율적으로 수행할 수 쓰기 가능 DC입니다. 자세한 내용은 [읽기 전용 DC 응용 프로그램 호환성 가이드](https://technet.microsoft.com/library/cc755190)를 참조하세요.

### <a name="BKMK_GC"></a>글로벌 카탈로그
Toochoose 여부 필요한 tooinstall 글로벌 카탈로그 (GC). 단일 도메인 포리스트에서 모든 DC를 글로벌 카탈로그 서버로 구성해야 합니다. 추가 복제 트래픽이 없기 때문에 비용이 증가하지 않습니다.

다중 도메인 포리스트의 경우 Gc hello 인증 프로세스 중 필요한 tooexpand 유니버설 그룹 멤버 자격을는 합니다. GC를 배포 하지 않는 경우 Azure에서 DC에 대해 인증 하는 hello 가상 네트워크에 대 한 작업은 간접적으로 생성 아웃 바운드 인증 트래픽을 tooquery Gc 온-프레미스 각 인증 시도 중입니다.

hello 비용 Gc와 관련 된는 모든 도메인 (부분에서)를 호스트 하기 때문에 예측 하기가 어렵습니다. 인터넷 서비스를 호스트 하 고 Windows Server AD DS에 대해 사용자를 인증 하는 hello 작업을 하는 경우 hello 비용은 완전히 예측 수 있습니다. toohelp 인증 하는 동안 hello 클라우드 사이트 외부의 GC 쿼리를 줄일 수 있습니다, [유니버설 그룹 구성원 자격 캐싱을 사용 하도록 설정](https://technet.microsoft.com/library/cc816928)합니다.

### <a name="BKMK_InstallMethod"></a>설치 방법
Toochoose를 어떻게 해야 hello 가상 네트워크에서 Dc tooinstall hello:

* 새 DC를 승격합니다. 자세한 내용은 [Azure 가상 네트워크에 새 Active Directory 포리스트 설치](active-directory-new-forest-virtual-machine.md)를 참조하세요.
* Hello 온-프레미스 가상 DC toohello 클라우드의 VHD를 이동 합니다. 이 경우 해당 hello 온-프레미스 가상 DC "이동" 없습니다 "복사" 또는 "복제 된". 있어야

Dc에 대 한 (것과 반대로 tooAzure "웹" 또는 "작업자" 역할 Vm)로 Azure 가상 컴퓨터를 사용 합니다. 지속성이 있으며 DC에 대한 상태의 내구성이 필요합니다. Azure 가상 컴퓨터는 DC와 같은 작업을 위해 설계되었습니다.

Dc를 복제 하거나 toodeploy SYSPREP를 사용 하지 마십시오. hello 기능 tooclone Dc는 Windows Server 2012부터 사용할 수 있습니다. 복제 기능 hello hello 기본 하이퍼바이저에서 VMGenerationID에 대 한 지원이 필요 합니다. Windows Server 2012 및 Azure 가상 네트워크의 Hyper-V는 모두 타사 가상화 소프트웨어 공급 업체와 마찬가지로 VMGenerationID를 지원합니다.

### <a name="BKMK_PlaceDB"></a>Hello Windows Server AD DS 데이터베이스 및 SYSVOL의 배치
Windows Server AD DS 데이터베이스, 로그 및 SYSVOL toolocate hello 하는 위치를 선택 합니다. Azure 데이터 디스크에 배포해야 합니다.

> [!NOTE]
> Azure 데이터 디스크는 제한 된 too1 TB입니다.
> 
> 

데이터 디스크 드라이브는 기본적으로 쓰기를 캐시하지 않습니다. 데이터 디스크 드라이브는 연결 된 tooa VM은 쓰기 캐싱을 사용 합니다. 쓰기-캐싱을 통해을 사용 하면 있는지 hello 쓰기는 커밋된 toodurable Azure 저장소 hello hello VM의 운영 체제 측면에서 hello 트랜잭션이 완료 되기 전에입니다. 쓰기 속도가 약간 느려지는의 hello 부담 내 구성을 제공합니다.

이 쓰기 디스크 캐싱이 DC hello 가정을 무효화 하기 때문에 Windows Server AD DS에 대 한 중요 합니다. Windows Server AD DS 시도 toodisable 쓰기 캐싱을 이지만 toohello 디스크 IO 시스템 toohonor을 것입니다. 오류 toodisable 쓰기 캐싱을 수, 특정 상황에서 USN 롤백이 생성 되어 느린 개체와 다른 문제입니다.

가상 Dc에 대 한 모범 사례로 수행 hello를 수행 합니다.

* None hello Azure 데이터 디스크에 hello 호스트 캐시 기본 설정을 설정 합니다. 이는 AD DS 작업에 대한 쓰기 캐싱을 사용하여 문제를 방지합니다.
* 동일한 데이터 디스크 또는 데이터 디스크를 분리 하는 hello에 hello 데이터베이스, 로그 및 SYSVOL을 저장 합니다. 일반적으로 이것이 hello 운영 체제 자체에 사용 되는 hello 디스크에서 별도 디스크입니다. hello 요점은 hello Windows Server AD DS 데이터베이스 및 SYSVOL Azure 운영 체제 디스크 유형에 저장 되지 않아야 합니다. 기본적으로 hello AD DS 설치 프로세스 이러한 구성 요소를 설치 Azure에 대 한 권장 되지 않는 %systemroot% 폴더에 있습니다.

### <a name="BKMK_BUR"></a>백업 및 복원
일반적으로 DC 및 보다 구체적으로 VM에서 실행되는 것의 백업 및 복원에 지원되는 것과 지원되지 않는 것을 확인합니다. [가상화된 DC에 대한 백업 및 복원 고려 사항](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv#backup_and_restore_considerations_for_virtualized_domain_controllers)을 참조하세요.

Windows Server 백업과 같은 Windows Server AD DS에 대한 백업 요구 사항을 특별히 인식하는 백업 소프트웨어만을 사용하여 시스템 상태 백업을 만듭니다.

정기 백업을 수행하는 대신 DC의 VHD 파일을 복사하거나 복제하지 마십시오. 복원이 필요한 경우 Windows Server 2012 및 지원되는 하이퍼바이저 없이 복제되거나 복사된 VHD를 사용하여 수행하면 USN 거품이 발생합니다.

### <a name="BKMK_FedSrvConfig"></a>페더레이션 서버 구성
Windows Server AD FS 페더레이션 서버 (Sts)의 hello 구성 여부 hello toodeploy Azure에서 지정 하는 응용 프로그램 필요 tooaccess 온-프레미스 네트워크에 있는 리소스에 일부 의존 합니다.

Hello 다음 조건을 충족 하는 hello 응용 프로그램을 온-프레미스 네트워크에서 격리 된 상태로 hello 응용 프로그램을 배포할 수 있습니다.

* SAML 보안 토큰에 동의합니다.
* 노출 가능한 경우 toohello 인터넷은
* 온-프레미스 리소스에 액세스하지 않습니다.

이 경우 Windows Server AD FS STS를 다음과 같이 구성합니다.

1. Azure에서 분리된 단일 도메인 포리스트를 구성합니다.
2. Windows Server AD FS 페더레이션 서버 팜을 구성 하 여 toohello 포리스트에 대 한 페더레이션된 액세스를 제공 합니다.
3. Hello 온-프레미스 포리스트에서 Windows Server AD FS (페더레이션 서버 팜 및 페더레이션 서버 프록시 팜을)를 구성 합니다.
4. Hello 온-프레미스 및 Windows Server AD FS의 Azure 인스턴스 간에 페더레이션 트러스트 관계를 설정 합니다.

다른 손 hello, hello에 해야 경우 tooon 온-프레미스 리소스에 액세스도 구성할 수 있습니다 Windows Server AD FS를 Azure에서 응용 프로그램 hello 다음과 같습니다.

1. 온-프레미스 네트워크와 Azure 간의 연결을 구성합니다.
2. Hello 온-프레미스 포리스트에서 Windows Server AD FS 페더레이션 서버 팜을 구성 합니다.
3. Azure에서 Windows Server AD FS 페더레이션 서버 프록시 팜을 구성합니다.

이 구성은 hello 비슷한 tooconfiguring Windows Server AD FS 응용 프로그램과 함께 경계 네트워크에 온-프레미스 리소스의 hello 노출을 줄이는 이점이 있습니다.

어느 시나리오에서든 B2B 공동 작업이 필요한 경우 더 많은 ID 공급자로 트러스트 관계를 설정할 수 있습니다.

### <a name="BKMK_CloudSvcConfig"></a>클라우드 서비스 구성
클라우드 서비스는 직접 인터넷 toohello 또는 tooexpose 인터넷 연결 부하 분산 된 VM tooexpose를 높이려는 경우 응용 프로그램입니다. 각 클라우드 서비스는 단일 구성 가능한 가상 IP 주소를 제공하기 때문에 이것이 가능합니다.

### <a name="BKMK_FedReqVIPDIP"></a>공용 및 개인 IP 주소 지정(동적 IP 및 가상 IP)에 대한 페더레이션 서버 요구 사항
각 Azure 가상 컴퓨터는 동적 IP 주소를 받습니다. 동적 IP 주소는 Azure 내에서만 액세스할 수 있는 개인 주소입니다. 그러나 대부분의 경우에서 됩니다 필요한 tooconfigure Windows Server AD FS 배포에 대 한 가상 IP 주소. hello 가상 IP 필요한 tooexpose Windows Server AD FS 끝점 toohello 인터넷 이며 인증 및 지속적인 관리에 대 한 페더레이션된 파트너와 클라이언트에서 사용할 수 있습니다. 가상 IP 주소는 하나 이상의 Azure 가상 컴퓨터를 포함하는 클라우드 서비스의 속성입니다. Azure와 Windows Server AD FS에 배포 된 hello 클레임 인식 응용 프로그램은 공통 포트를 모두 인터넷 연결 및 공유, 각각 자체의 가상 IP 주소에 필요 하 고 hello 응용 프로그램에 대 한 필요한 toocreate 한 클라우드 서비스 수 없으므로 및 Windows Server AD FS에 대 한 두 번째.

Hello 용어 가상 IP 주소 및 IP 주소를 동적 정의 참조 하십시오. [용어 및 정의](#BKMK_Glossary)합니다.

### <a name="BKMK_ADFSHighAvail"></a>Windows Server AD FS 고가용성 구성
가능한 toodeploy 독립 실행형 Windows Server AD FS 페더레이션 서비스 이지만, AD FS STS 및 프로덕션 환경에 대 한 프록시를 모두에 대해 두 개 이상의 노드가 있는 팜이 toodeploy을 것이 좋습니다.

참조 [AD FS 2.0 배포 토폴로지 고려 사항](https://technet.microsoft.com/library/gg982489) hello에 [AD FS 2.0 디자인 가이드](https://technet.microsoft.com/library/dd807036) toodecide 배포 구성에 가장 옵션을 특정 요구 사항에 맞게 합니다.

> [!NOTE]
> 순서 tooget 부하 분산 hello에 hello Windows Server AD FS 팜의 모든 멤버를 구성 하는 Azure에서 Windows Server AD FS 끝점에 대 한 동일한 클라우드 서비스, 항목과 hello Azure의 기능에 대해 부하 분산 (기본값 80) HTTP 및 HTTPS 포트 (기본값 443)를 사용 합니다. 자세한 내용은 [Azure 부하 분산 장치 프로브](https://msdn.microsoft.com/library/azure/jj151530)를 참조하세요.
> Windows Server NLB(네트워크 부하 분산)는 Azure에서 지원되지 않습니다.
> 
> 

