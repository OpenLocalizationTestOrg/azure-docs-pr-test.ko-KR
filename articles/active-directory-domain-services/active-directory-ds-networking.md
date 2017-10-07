---
title: "Azure AD 도메인 서비스: 네트워킹 지침 | Microsoft Docs"
description: "Azure Active Directory Domain Services의 네트워킹 고려 사항"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 23a857a5-2720-400a-ab9b-1ba61e7b145a
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: maheshu
ms.openlocfilehash: 804d4ea7d1b3b07b6d224855c7adb90bdfe24022
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="networking-considerations-for-azure-ad-domain-services"></a>Azure AD 도메인 서비스의 네트워킹 고려 사항
## <a name="how-tooselect-an-azure-virtual-network"></a>어떻게 tooselect Azure 가상 네트워크
hello 다음 지침 선택할 수 있도록 Azure AD 도메인 서비스와 가상 네트워크 toouse 합니다.

### <a name="type-of-azure-virtual-network"></a>Azure 가상 네트워크 유형
* 클래식 Azure 가상 네트워크에서 Azure AD 도메인 서비스를 활성화할 수 있습니다.
* Azure AD 도메인 서비스는 **Azure Resource Manager를 사용하여 만든 가상 네트워크에서 활성화될 수 없습니다**.
* 가상 네트워크 리소스 관리자 기반 tooa 클래식 가상 네트워크를 Azure AD 도메인 서비스를 사용할 수 있는 연결할 수 있습니다. 그 후 hello 리소스 관리자 기반 가상 네트워크에서 Azure AD 도메인 서비스를 사용할 수 있습니다. 자세한 내용은 참조 hello [네트워크 연결](active-directory-ds-networking.md#network-connectivity) 섹션.
* **지역 가상 네트워크**: toouse 기존 가상 네트워크를 계획 하는 경우 지역 가상 네트워크 인지 확인 합니다.

  * Hello 레거시 선호도 그룹 메커니즘을 사용 하는 가상 네트워크는 Azure AD 도메인 서비스와 함께 사용할 수 없습니다.
  * Azure AD 도메인 서비스, toouse [레거시 가상 네트워크 tooregional 가상 네트워크 마이그레이션](../virtual-network/virtual-networks-migrate-to-regional-vnet.md)합니다.

### <a name="azure-region-for-hello-virtual-network"></a>Hello 가상 네트워크에 대 한 azure 지역
* 관리 되는 도메인에 배포 된 Azure AD 도메인 서비스 hello에 tooenable hello 서비스를 선택 하는 hello 가상 네트워크와 같은 Azure 지역입니다.
* Azure AD 도메인 서비스에서 지원하는 Azure 지역에서 가상 네트워크를 선택합니다.
* Hello 참조 [지역별 Azure 서비스](https://azure.microsoft.com/regions/#services/) 페이지 tooknow hello Azure AD 도메인 서비스를 사용할 수 있는 Azure 지역입니다.

### <a name="requirements-for-hello-virtual-network"></a>Hello 가상 네트워크에 대 한 요구 사항
* **근접 tooyour Azure 작업**: 선택 hello 가상 네트워크를 현재 호스트/tooAzure AD 도메인 서비스에 액세스 해야 하는 가상 컴퓨터를 호스트 합니다.
* **DNS 서버 사용자 지정/bring your own**: hello 가상 네트워크에 구성 된 사용자 지정 DNS 서버가 없는지 확인 합니다.
* **기존 도메인과 동일한 도메인 이름을 hello**: hello로 기존 도메인 있는지 확인 하세요 동일한 도메인 이름을 해당 가상 네트워크에서 사용할 수 있습니다. 예를 들어 hello 선택한 가상 네트워크에서 이미 사용할 수 있는 ' contoso.com' 이라는 도메인을 사용 한다고 가정 합니다. Azure AD 도메인 서비스는 관리 되는 도메인 hello로 tooenable 시도 나중 동일한 도메인 이름 (즉, '만든 contoso.com') 해당 가상 네트워크에 있습니다. Tooenable Azure AD 도메인 서비스는 동안 오류가 발생 하면 합니다. 이 오류는 해당 가상 네트워크에서 도메인 이름 hello에 대 한 tooname 충돌 때문입니다. 이 경우 Azure AD 도메인 서비스는 관리 되는 도메인을 다른 이름 tooset를 사용 해야 합니다. 또는 기존 도메인 hello를 프로 비전 해제할 수 있으며 tooenable Azure AD 도메인 서비스를 진행할 수 있습니다.

> [!WARNING]
> Hello 서비스를 활성화 한 후에 도메인 서비스 tooa 다른 가상 네트워크를 이동할 수 없습니다.
>
>

## <a name="network-security-groups-and-subnet-design"></a>네트워크 보안 그룹 및 서브넷 디자인
A [보안 그룹 NSG (네트워크)](../virtual-network/virtual-networks-nsg.md) 허용 하거나 거부할 네트워크 트래픽을 가상 네트워크에서 VM 인스턴스 tooyour 하는 액세스 제어 목록 (ACL) 규칙의 목록을 포함 합니다. NSG는 서브넷 또는 서브넷 내의 개별 VM 인스턴스 중 하나와 연결될 수 있습니다. NSG를 서브넷과 연결 하는 경우 해당 서브넷에 tooall hello VM 인스턴스 hello ACL 규칙에 적용 됩니다. 또한 트래픽 tooan 개별 VM을 제한할 수 NSG를 연결 하 여 추가 VM toothat 직접 합니다.

![권장되는 서브넷 디자인](./media/active-directory-domain-services-design-guide/vnet-subnet-design.png)

### <a name="best-practices-for-choosing-a-subnet"></a>서브넷을 선택하기 위한 모범 사례
* Azure AD 도메인 서비스 tooa 배포 **전용된 서브넷을 분리** Azure 가상 네트워크 내에서.
* 관리 되는 도메인에 대 한 전용 toohello 서브넷 Nsg는 적용 되지 않습니다. Nsg toohello 전용 서브넷을 적용 해야 하는 경우를 확인 하면 **hello 포트 필요한 tooservice 차단 하지 않으며 도메인 관리**합니다.
* 과도 하 게 관리 되는 도메인에 대 한 전용 hello 서브넷에서 사용할 수 있는 IP 주소의 hello 수를 제한 하지 않습니다. 이 제한은 관리 되는 도메인에 사용할 수 있는 두 명의 도메인 컨트롤러를 만들지 못하도록 hello 서비스를 방지 합니다.
* **Hello 게이트웨이 서브넷에서 Azure AD 도메인 서비스를 사용 하지 마십시오** 가상 네트워크의 합니다.

> [!WARNING]
> 에 연결할 때 Azure AD 도메인 서비스는 서브넷과 NSG를 사용할 경우 hello 도메인 관리 및 Microsoft의 능력 tooservice 중단 될 수 있습니다. 또한 Azure AD 테넌트와 관리되는 도메인 간의 동기화가 중단됩니다. **hello SLA toodeployments 여기서 NSG에서 적용 한 Azure AD 도메인 서비스를 차단 하 업데이트 도메인 관리 및 적용 되지 않습니다.**
>
>

### <a name="ports-required-for-azure-ad-domain-services"></a>Azure AD Domain Services에 필요한 포트
hello 다음 포트에 필요 tooservice Azure AD 도메인 서비스 및 관리 되는 도메인 유지 관리 합니다. 이러한 포트를 사용 하도록 설정한 관리 되는 도메인 hello 서브넷에 대 한 차단 되지 않았다는 확인 합니다.

| 포트 번호 | 목적 |
| --- | --- |
| 443 |Azure AD 테넌트와 동기화 |
| 3389 |도메인 관리 |
| 5986 |도메인 관리 |
| 636 |보안 LDAP (LDAPS) 액세스 tooyour 관리 되는 도메인 |

### <a name="sample-nsg-for-virtual-networks-with-azure-ad-domain-services"></a>Azure AD Domain Services를 사용하는 가상 네트워크에 대한 샘플 NSG
다음 표에서 hello 샘플을 NSG는 Azure AD 도메인 서비스는 관리 되는 도메인을 사용 하 여 가상 네트워크에 대해 구성할 수를 보여 줍니다. 이 규칙은 관리 되는 도메인 유지 되며 패치, 업데이트 및 Microsoft에서 모니터링할 수 있습니다 위에 지정 된 포트 tooensure hello에서 인바운드 트래픽을 허용 합니다. hello 기본 'DenyAll' 규칙 적용 tooall 인바운드 트래픽을 다른 hello에서 인터넷 합니다.

또한 hello를 NSG 방법을 통해 보안 LDAP 액세스 아래로 toolock hello 인터넷도 나타냅니다. 이 규칙 건너뛰기를 통해 보안 LDAP 액세스 tooyour 관리 되는 도메인을 설정 하지 않은 경우 인터넷 hello 합니다. hello NSG에는 TCP 포트를 통해 636 지정된 된 집합 에서만에서 IP 주소의 인바운드 LDAPS 액세스를 허용 하는 규칙 집합이 포함 되어 있습니다. hello NSG 규칙 tooallow LDAPS 액세스 hello 통해 지정 된 IP 주소에서 인터넷에 hello DenyAll NSG 규칙 보다 우선 순위가 높습니다.

![샘플 NSG toosecure LDAPS 액세스를 통해 인터넷 hello](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

**자세한 내용** - [네트워크 보안 그룹 만들기](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)


## <a name="network-connectivity"></a>네트워크 연결
Azure AD 도메인 서비스 관리되는 도메인은 Azure에서 단일 클래식 가상 네트워크 내에서만 활성화될 수 있습니다. Azure Resource Manager를 사용하여 만든 가상 네트워크는 지원되지 않습니다.

### <a name="scenarios-for-connecting-azure-networks"></a>Azure 네트워크 연결에 대한 시나리오
Azure 가상 네트워크 toouse hello hello 다음 배포 시나리오 중 하나에서 관리 되는 도메인을 연결 합니다.

#### <a name="use-hello-managed-domain-in-more-than-one-azure-classic-virtual-network"></a>사용 하 여 hello 둘 이상의 Azure 클래식 가상 네트워크의 도메인 관리
다른 Azure 클래식 가상 네트워크 toohello Azure를 연결할 수 있는 Azure AD 도메인 서비스를 사용할 수 있는 클래식 가상 네트워크입니다. 이 VPN 연결 toouse hello에 대 한 관리 되는 도메인 사용 하면 다른 가상 네트워크에 배포 된 작업 있습니다.

![클래식 가상 네트워크 연결](./media/active-directory-domain-services-design-guide/classic-vnet-connectivity.png)

#### <a name="use-hello-managed-domain-in-a-resource-manager-based-virtual-network"></a>리소스 관리자 기반 가상 네트워크의 관리 되는 도메인 hello를 사용 하 여
리소스 관리자 기반 가상 네트워크 toohello Azure를 연결할 수 있는 Azure AD 도메인 서비스를 사용할 수 있는 클래식 가상 네트워크입니다. 이 연결 hello 리소스 관리자 기반 가상 네트워크에 배포 하 여 작업을 toouse hello에 대 한 관리 되는 도메인이 있습니다.

![리소스 관리자 tooclassic 가상 네트워크 연결](./media/active-directory-domain-services-design-guide/classic-arm-vnet-connectivity.png)

### <a name="network-connection-options"></a>네트워크 연결 옵션
* **사이트 간 VPN 연결을 사용 하 여 VNet 대 VNet 연결**: 연결 하는 가상 네트워크 tooanother 가상 네트워크 (VNet 대 VNet)는 비슷한 tooconnecting 가상 네트워크 tooan 온-프레미스 사이트 위치입니다. 두 연결 유형에서는 VPN 게이트웨이 tooprovide IPsec/IKE를 사용 하 여 보안 터널을 사용 합니다.

    ![VPN Gateway를 사용하여 가상 네트워크 연결](./media/active-directory-domain-services-design-guide/vnet-connection-vpn-gateway.jpg)

    [추가 정보 - VPN 게이트웨이를 사용하여 가상 네트워크 연결](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)
* **VNet 대 VNet 연결을 사용 하 여 가상 네트워크 피어 링**: hello에 두 개의 가상 네트워크를 연결 하는 메커니즘은 가상 네트워크 피어 링 hello Azure backbone 네트워크를 통해 동일한 지역입니다. 겹치기, hello 두 가상 네트워크 연결의 모든 용도 대 한 하나로 표시 됩니다. 여전히 별도 리소스로 관리할 수는 있지만 이러한 가상 네트워크의 가상 컴퓨터는 개인 IP 주소를 사용하여 직접 서로 통신할 수 있습니다.

    ![피어링을 사용하여 가상 네트워크 연결](./media/active-directory-domain-services-design-guide/vnet-peering.png)

    [추가 정보 - 가상 네트워크 피어링](../virtual-network/virtual-network-peering-overview.md)

<br>

## <a name="related-content"></a>관련 콘텐츠
* [Azure 가상 네트워크 피어링](../virtual-network/virtual-network-peering-overview.md)
* [Hello 클래식 배포 모델에 대 한 VNet 대 VNet 연결 구성](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)
* [Azure 네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md)
* [네트워크 보안 그룹 만들기](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
