---
title: "클라우드 솔루션 공급자에 대 한 express 경로 aaaAzure | Microsoft Docs"
description: "이 문서에서는 클라우드 서비스 공급자에 대 한 정보를 원하는 tooincorporate Azure 서비스 및 판매 제품에 대 한 express 경로입니다."
documentationcenter: na
services: expressroute
author: richcar
manager: carmonm
editor: 
ms.assetid: f6c5f8ee-40ba-41a1-ae31-67669ca419a6
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: richcar
ms.openlocfilehash: 062ecbb5e461e4384b01c4ac478cab696b7ed398
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-for-cloud-solution-providers-csp"></a>클라우드 솔루션 공급자(CSP)용 Express 경로
Microsoft는 기존의 대리점 및 새로운 서비스 및 솔루션 hello 없는 고객을 위해 필요한 tooinvest 이러한 새 서비스를 개발 하는 배포자 (CSP) toobe 수 toorapidly 제공할 위한 하이퍼 스케일 서비스를 제공 합니다. tooallow hello 클라우드 솔루션 공급자 (CSP) hello 기능 toodirectly 이러한 새 서비스를 관리, Microsoft 프로그램 및 고객을 대신 하 여 hello CSP toomanage Microsoft Azure 리소스를 허용 하는 Api를 제공 합니다. 이러한 리소스 중 하나가 Express 경로입니다. ExpressRoute는 CSP tooconnect 기존 고객 리소스 tooAzure 서비스 hello를 사용 합니다. ExpressRoute는 Azure의 고속 개인 통신 링크 tooservices 합니다. 

ExpresRoute는 고가용성을 위해 연결 된 tooa 단일 고객 구독 이며 여러 고객에 게 프로세스에서 공유할 수 없는 있는 회로의 쌍으로 구성 됩니다. 각 회로 서로 다른 라우터 toomaintain hello 고가용성에서 종료 되어야 합니다.

> [!NOTE]
> Express 경로에는 대역폭 및 연결 한도가 있으므로 크고 복잡한 구현에는 단일 고객에 대해 여러 Express 경로 회로가 필요합니다.
> 
> 

Microsoft Azure tooyour 고객을 제공할 수 있습니다 점점 더 많은 서비스를 제공 합니다.  이러한 서비스 활용 toobest hello 사용 ExpressRoute 연결 tooprovide 고속 대기 시간이 짧은 액세스 toohello Microsoft Azure 환경에 필요 합니다.

## <a name="microsoft-azure-management"></a>Microsoft Azure 관리
Microsoft는 Csp Api toomanage와 hello Azure 고객 구독 사용자 고유의 서비스 관리 시스템과 통합 프로그래밍을 허용 하 여 합니다. 지원되는 관리 기능은 [여기](https://msdn.microsoft.com/library/partnercenter/dn974944.aspx)에서 확인할 수 있습니다.

## <a name="microsoft-azure-resource-management"></a>Microsoft Azure 리소스 관리
Hello에 따라 고객에 있는 계약 hello 구독 관리 되는 방식을 결정 합니다. hello CSP hello 만들기를 직접 관리할 수 있는 및 리소스 또는 hello 고객의 유지 관리는 hello Microsoft Azure 구독을 관리 하 고 필요한 hello Azure 리소스를 만들 수 있습니다. 두 모델 중 하나를 사용할는 고객의 Microsoft Azure 구독에서 리소스 만들기 hello를 관리 하는 경우: 모델 "Connect 통해" 또는 "Direct To" 모델입니다. 이러한 모델은 hello 다음 섹션에서에서 자세히 설명 되어 있습니다.  

### <a name="connect-through-model"></a>Connect-through 모델
![대체 텍스트](./media/expressroute-for-cloud-solution-providers/connect-through.png)  

Hello 통해 연결 모델 hello CSP 데이터 센터와 고객의 Azure 구독 간에 직접 연결을 만듭니다. hello 직접 연결을 ExpressRoute를 Azure와 네트워크 연결을 사용 하 여 이루어집니다. 그런 다음 고객 tooyour 네트워크를 연결합니다. 이 시나리오는 해당 hello 고객 hello CSP 네트워크 tooaccess Azure 서비스를 통해 전달 해야 합니다. 

고객이에서 관리 하지 않는 다른 Azure 구독이 있으면 안녕하세요, 공용 인터넷 또는 hello 아닌 CSP 구독에서 사용자를 프로 비전 되는 자신의 개인 연결 tooconnect toothose 서비스 hello 사용 되는 것입니다. 

Azure 서비스 관리를 CSP 해당 hello CSP는 다음에 복제 됩니다 Azure Active Directory의 CSP 구독 Administrate-On-Behalf-Of (AOBO)를 통해 관리를 위해 저장할 이전에 설정 된 고객 id를 가진 것으로 가정 합니다. 이 시나리오에 대 한 주요 견인차에는 여기서 지정된 파트너 또는 서비스 공급자가 설정 된 관계가 hello 고객과, hello 고객은 공급자 서비스를 현재 사용 또는 hello 파트너 desire tooprovide의 조합은 공급자 호스트 및 Azure 호스팅 솔루션 tooprovide 유연성과 주소 고객 문제만 CSP에서 충족 되지 않습니다. 이 모델은 아래 **그림**에 설명되어 있습니다.

![대체 텍스트](./media/expressroute-for-cloud-solution-providers/connect-through-model.png)

### <a name="connect-toomodel"></a>연결 toomodel
![대체 텍스트](./media/expressroute-for-cloud-solution-providers/connect-to.png)

Connect toomodel hello hello 서비스 공급자 고객의 데이터 센터 간에 직접 연결을 만듭니다. hello CSP 프로 비전 hello 고객의 (customer)를 통해 ExpressRoute를 사용 하 여 Azure 구독 및 네트워크입니다.

> [!NOTE]
> ExpressRoute에 대 한 hello 고객 toocreate 필요 하 고 hello ExpressRoute 회로 유지 관리 합니다.  
> 
> 

이 연결 시나리오 작성, 소유 하 고 전체 또는 부분적으로 hello 고객이 관리 하는 네트워크에 직접 연결을 사용 하 여 해당 hello 고객 고객 네트워크 tooaccess CSP 관리 Azure 구독을 통해 직접 연결 해야 합니다. 이러한 고객에 대 한 가정 hello 공급자가 현재 설정 하는 고객 id 저장소 않아도 및 hello 공급자에 도움이 되 hello 고객의 관리에 대 한 현재 식별 상점별 Azure Active Directory에 복제 하는 AOBO 하 여 등록 합니다. 이 시나리오에 대 한 주요 견인차에는 여기서 지정된 파트너 또는 서비스 공급자가 설정 된 관계가 hello 고객과, hello 고객은 공급자 서비스를 현재 사용 또는 hello 파트너에 게 기반으로 하는 전적으로 desire tooprovide 서비스 Hello 없는 azure 호스팅 솔루션 공급자의 기존 데이터 센터 또는 인프라에 대 한 필요 합니다.

![대체 텍스트](./media/expressroute-for-cloud-solution-providers/connect-to-model.png)

hello 이러한 두 옵션 중 하나를 선택 된 고객의 요구 사항에 따라 없으며 현재 tooprovide Azure 서비스입니다. 역할 기반 액세스 제어, 네트워킹를 연결 하는 이러한 모델 및 hello hello 세부 정보 및 identity 디자인 패턴이 링크를 따라 hello에 대 한 세부 정보에 포함 됩니다.

* **역할 기반 액세스 제어(RBAC)** - RBAC는 Azure Active Directory를 기반으로 합니다.  Azure RBAC에 대한 자세한 내용은 [여기](../active-directory/role-based-access-control-configure.md)를 참조하세요.
* **네트워킹** – 적용 됩니다. Microsoft Azure의 네트워킹의 다양 한 주제를 hello 합니다.
* **Azure Active Directory (AAD)** – AAD Microsoft Azure 및 타사 SaaS 응용 프로그램에 대 한 hello id 관리를 제공 합니다. Azure AD에 대한 자세한 내용은 [여기](https://azure.microsoft.com/documentation/services/active-directory/)를 참조하세요.  

## <a name="network-speeds"></a>네트워크 속도
ExpressRoute 50 Mb/s too10Gb/s에서 네트워크 속도 지원합니다. 이 통해 사용자는 자신의 고유 환경에 필요한 네트워크 대역폭의 toopurchase hello 양을.

> [!NOTE]
> 통신을 방해 하지 않고 필요에 따라 네트워크 대역폭을 늘릴 수 있습니다 하지만 tooreduce hello 네트워크 속도 hello 회로 중지 하 고 hello 낮은 네트워크 속도에서 다시 생성 해야 합니다.  
> 
> 

ExpressRoute는 hello 고속 연결을 더 효율적으로 사용에 대 한 여러 Vnet tooa 단일 express 경로 회로의 hello 연결을 지원합니다. 단일 express 경로 회로 hello가 소유 하는 여러 Azure 구독 간에 공유할 수 같은 고객 합니다.

## <a name="configuring-expressroute"></a>Express 경로 구성
Express 경로 구성 된 toosupport 세 종류의 트래픽 될 수 있습니다 ([라우팅 도메인](#ExpressRoute-routing-domains))에 단일 ExpressRoute 회로 통해 합니다. 이 트래픽은 Microsoft 피어링, Azure 공용 피어링 및 개인 피어링으로 분리됩니다. Hello ExpressRoute 회로 및 고객에 필요한 격리의 hello 크기에 따라 여러 ExpressRoute 회로 사용 하거나 트래픽 toobe에 단일 ExpressRoute 회로 통해 전송 중 하나 또는 모든 유형을 선택할 수 있습니다. 고객의 보안 상태 hello 수 없으며, 공용 트래픽과 통해 개인 트래픽 tootraverse hello 동일한 회로 합니다.

### <a name="connect-through-model"></a>Connect-through 모델
구성을 통해 connect hello에서 모든 고객 데이터 센터 리소스 toohello 구독 Azure에서 호스팅되는 기본 토대 tooconnect 네트워킹 hello에 대 한 책임 수 있습니다. 각 고객의 원하는 toouse Azure 기능이 필요 하 여 관리 되는 자신의 ExpressRoute 연결 hello 있습니다. hello 사용 하 여 hello 동일한 메서드 hello 고객 tooprocure hello ExpressRoute 회로 사용 합니다. hello를 수행 해야 hello 문서에 설명 된 동일한 단계 hello [express 경로 워크플로](expressroute-workflows.md) 회선 프로비저닝 및 회선 상태에 대 한 합니다. hello 다음 hello 프로토콜 BGP (경계 게이트웨이) 경로 toocontrol hello 트래픽 흐름 hello 온-프레미스 네트워크와 Azure vNet을 구성 합니다.

### <a name="connect-toomodel"></a>연결 toomodel
Connect tooconfiguration에서 고객이 이미는 기존 연결 tooAzure 했거나이 고객의 데이터 센터에서 express 경로 연결 합니다. 연결 toohello 인터넷 서비스 공급자는 초기화 데이터 센터 대신 tooAzure 직접 합니다. toobegin hello 프로 비전 프로세스를 고객 hello 단계를 수행 하는 hello 통해 연결 모델에서 설명한 것과 같이 합니다. Hello 회로 설정 된 후에 고객이 네트워크와 Azure Vnet tooconfigure hello 온-프레미스 라우터 toobe 수 tooaccess에 필요 합니다.

Hello 연결 설정을 지원할 수 있습니다 하 고, 데이터 센터의 hello 클라이언트 리소스 또는 Azure에서 호스트 되는 hello 리소스 센터 toocommunicate 프로그램에서 tooallow hello 리소스 라우팅합니다 hello 구성 키를 누릅니다.

## <a name="expressroute-routing-domains"></a>Express 경로 라우팅 도메인
Express 경로는 공용, 개인 및 Microsoft 피어링의 세 가지 라우팅 도메인을 제공합니다. 각각 hello 라우팅 도메인의 고가용성을 위해 활성-활성 구성에 있는 동일한 라우터 구성 됩니다. Express 경로 라우팅 도메인에 대한 자세한 내용은 [여기](expressroute-circuit-peerings.md)를 확인하세요.

사용자 지정 경로 필터 tooallow 유일한 hello 경로 tooallow 원할 정의할 수 있습니다. 대 한 자세한 내용은 toosee toomake 이러한 변경 내용을 참조 문서: [만들기 및 PowerShell을 사용 하 여 ExpressRoute 회로 대 한 라우팅 수정](expressroute-howto-routing-classic.md) 라우팅 필터에 대 한 자세한 내용은 합니다.

> [!NOTE]
> Microsoft 및 공용 피어 링에 대 한 연결 해야 하지만 hello 고객 또는 CSP가 소유한 공용 IP 주소 및 tooall 정의 된 규칙을 준수 해야 합니다. 자세한 내용은 참조 hello [ExpressRoute 필수 구성 요소](expressroute-prerequisites.md) 페이지.  
> 
> 

## <a name="routing"></a>라우팅
ExpressRoute 연결 toohello Azure hello Azure 가상 네트워크 게이트웨이 통해 네트워크입니다. 네트워크 게이트웨이는 Azure 가상 네트워크에 대한 라우팅을 제공합니다.

또한 Azure 가상 네트워크를 만들면 hello vNet의 hello 서브넷에서 hello vNet toodirect 트래픽에 대 한 기본 라우팅 테이블이 만들어집니다. Hello 기본 경로 테이블 hello 솔루션을 사용자 지정에 대 한 충분 하지 않은 경우 tooblock toospecific 서브넷 또는 외부 네트워크 경로 또는 경로 tooroute 나가는 트래픽 toocustom 어플라이언스를 만들 수 수 있습니다.

### <a name="default-routing"></a>기본 라우팅
hello 기본 경로 테이블에 경로 따라 hello 포함 됩니다.

* 한 서브넷 내에서 라우팅
* Hello 가상 네트워크 내의 서브넷 서브넷
* toohello 인터넷
* VPN 게이트웨이를 사용하여 가상 네트워크-가상 네트워크
* VPN 또는 Express 경로 게이트웨이를 사용하여 가상 네트워크-온-프레미스 네트워크

![대체 텍스트](./media/expressroute-for-cloud-solution-providers/default-routing.png)  

### <a name="user-defined-routing-udr"></a>UDR(사용자 정의 라우팅)
사용자 정의 경로 hello에서 아웃 바운드 트래픽의 hello 컨트롤이 할당 서브넷 hello 가상 네트워크의 tooother 서브넷 또는 중 하나 위에 hello (ExpressRoute; 인터넷 또는 VPN) 미리 정의 된 다른 게이트웨이 통해 합니다. 사용자 지정 경로를 hello 기본 라우팅 테이블을 대체 하는 사용자 지정 라우팅 테이블 hello 기본 시스템에 대 한 라우팅 테이블 대체 될 수 있습니다. 사용자 지정 라우팅을 사용 하 여 고객 방화벽 또는 침입 검색 어플라이언스와 같은 특정 경로 tooappliances 만들 하거나 hello 사용자 정의 경로 호스팅하는 hello 서브넷에서 액세스 toospecific 서브넷을 차단할 수 있습니다. 사용자 정의 경로에 대한 개요는 [여기](../virtual-network/virtual-networks-udr-overview.md)에서 확인하세요. 

## <a name="security"></a>보안
Connect tooor 연결-를 통해 사용 중인 어떤 모델 인지에 따라 고객의 vNet에 hello 보안 정책을 정의 또는 toohello CSP toodefine tootheir Vnet hello 보안 정책 요구 사항을 제공 합니다. 다음 보안 기준을 hello는 정의할 수 있습니다.

1. **고객 격리** -hello Azure 플랫폼 격리를 제공 고객 tooencapsulate 사용 되는 보안 데이터베이스에 고객 ID 및 vNet 정보를 저장 하 여 각 고객의 GRE 터널 트래픽 양입니다.
2. **네트워크 보안 그룹 (NSG)** 들어오고 트래픽 hello Azure의 Vnet 내에 서브넷을 정의 하기 위한 규칙은 합니다. 기본적으로 hello NSG hello 인터넷 toohello vNet과 vNet 내의 트래픽이 허용 규칙에서 규칙 tooblock 트래픽을 차단을 포함 합니다. 네트워크 보안 그룹에 대한 자세한 내용은 [여기](https://azure.microsoft.com/blog/network-security-groups/)를 확인하세요.
3. **강제 터널링** -인터넷 바운드 트래픽은 온 프레미스 데이터 센터에 hello ExpressRoute 연결 toohello 전환할 Azure toobe에서 발생 하는 옵션 tooredirect입니다. 강제 터널링에 대한 자세한 내용은 [여기](expressroute-routing.md#advertising-default-routes)를 확인하세요.  
4. **암호화** -hello ExpressRoute 회로 전용된 tooa 특정 고객 인 경우에는 hello 가능성을 네트워크 공급자 hello 수 통과 침입자 tooexamine 패킷 트래픽을 허용 합니다. 이 가능성, 고객 또는 CSP를 통해 트래픽을 암호화할 수 tooaddress 프레미스 리소스에 hello 및 Azure 리소스 (toohello 선택적 터널 모드 IPSec 고객 1에 대 한 참조 간에 전달 되는 모든 트래픽에 대 한 IPSec 터널 모드 정책을 정의 하 여 연결 hello 그림 5에서: ExpressRoute 보안, 위). 두 번째 옵션 hello toouse hello ExpressRoute 회로의 각 hello 끝점에는 방화벽 어플라이언스 것입니다. 이 추가 타사 방화벽 Vm/어플라이언스 toobe hello ExpressRoute 회로 통해 끝 tooencrypt hello 트래픽 모두에 설치 해야 합니다.

![대체 텍스트](./media/expressroute-for-cloud-solution-providers/expressroute-security.png)  

## <a name="next-steps"></a>다음 단계
hello 클라우드 솔루션 공급자 서비스는 hello 없이 값 tooyour 고객 비용이 많이 드는 인프라와 기능을 구매 현황을 hello 기본 아웃소싱 공급자로 유지 하면서에 필요한 방식으로 tooincrease를 제공 합니다. Hello에 기존 관리 프레임 워크 내에서 Microsoft Azure의 toointegrate 관리를 허용 하는 CSP API를 통해 Microsoft Azure로의 원활한 통합을 수행할 수 있습니다.  

추가 정보 링크를 따라 hello에서 찾을 수 있습니다.

[Microsoft 클라우드 솔루션 공급자 프로그램](https://partner.microsoft.com/en-US/Solutions/cloud-reseller-overview).  
[클라우드 솔루션 공급자 준비 tootransact 가져오기](https://partner.microsoft.com/en-us/solutions/cloud-reseller-pre-launch)합니다.  
[Microsoft 클라우드 솔루션 공급자 리소스](https://partner.microsoft.com/en-us/solutions/cloud-reseller-resources).

