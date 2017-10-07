---
title: "분리 된 네트워크 및 Azure AD 응용 프로그램 프록시에서 커넥터 그룹을 사용 하 여 위치에서 응용 프로그램 aaaPublishing | Microsoft Docs"
description: "에서는 어떻게 toocreate에서 Azure AD 응용 프로그램 프록시 커넥터 그룹 및 관리 합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: 8c9a84b365eab28eaaeb343d4d1e2e6990537fec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a>커넥터 그룹을 사용하여 별도의 네트워크 및 위치에서 응용 프로그램 게시
> [!div class="op_single_selector"]
> * [Azure Portal](active-directory-application-proxy-connectors-azure-portal.md)
> * [Azure 클래식 포털](active-directory-application-proxy-connectors.md)
>

고객은 점점 더 많은 시나리오와 응용 프로그램을 위해 Azure AD의 응용 프로그램 프록시를 활용합니다. 따라서 더 많은 토폴로지를 사용하여 응용 프로그램 프록시를 더욱 유연하게 만들었습니다. 특정 커넥터 tooserve 특정 응용 프로그램을 할당할 수 있도록 응용 프로그램 프록시 커넥터 그룹을 만들 수 있습니다. 이 기능을 사용 하면 더 많은 제어 및 방법 toooptimize 응용 프로그램 프록시 배포 합니다. 

각 응용 프로그램 프록시 커넥터 tooa 커넥터 그룹에 할당 됩니다. 모든 커넥터를 커넥터 그룹을 같은 고가용성 및 부하 분산에 대 한 별도 단위를 프록시로 toohello 속하는 hello 합니다. 모든 커넥터에 포함할 tooa 커넥터 그룹입니다. 그룹을 만들지 않는 경우 모든 커넥터는 기본 그룹에 있습니다. 관리자에 게 새 그룹 만들고 커넥터 toothem hello Azure 포털에서에서 할당할 수 있습니다. 

모든 응용 프로그램 tooa 커넥터 그룹에 할당 됩니다. 그룹을 만들지 않는 경우 tooa 기본 그룹 응용 프로그램에 할당 됩니다. 하지만 특정 커넥터 그룹과 함께 각 응용 프로그램 toowork를 그룹으로 커넥터를 구성 하는 경우 설정할 수 있습니다. 이 경우 해당 그룹의 유일한 hello 커넥터는 요청 시 hello 응용 프로그램을 제공합니다. 이 기능은 응용 프로그램이 서로 다른 위치에서 호스트되는 경우에 유용합니다. 응용 프로그램은 항상 물리적으로 닫기 toothem 되는 커넥터를 통해 제공 됩니다 되도록 위치에 따라 커넥터 그룹을 만들 수 있습니다.

>[!TIP] 
>대규모 응용 프로그램 프록시 배포를 설정한 경우 모든 응용 프로그램 toohello 기본 커넥터 그룹을 할당 하지 마세요. 이런 방식으로 새 커넥터 되지 않습니다 라이브 트래픽을 tooan 활성 커넥터 그룹을 할당할 때까지 합니다. 이 구성 하면 수도 tooput 커넥터 유휴 모드에서 백 toohello 기본 그룹을 이동 하 여 사용자가 영향을 주지 않고 유지 관리를 수행할 수 있도록 있습니다.

## <a name="prerequisites"></a>필수 조건
toogroup 커넥터, toomake 있는지 있는 있습니다 [여러 명의 커넥터가 설치](active-directory-application-proxy-enable.md)합니다. Hello 새 커넥터를 설치할 때 자동으로 조인 **기본** 커넥터 그룹입니다.

## <a name="create-connector-groups"></a>커넥터 그룹 만들기
이러한 단계 toocreate 원하는 수 만큼 커넥터 그룹을 사용 합니다. 

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
1. **Azure Active Directory** > **Enterprise 응용 프로그램** > **응용 프로그램 프록시**를 선택합니다.
2. **새 커넥터 그룹**을 선택합니다. hello 새 커넥터 그룹 블레이드가 나타납니다.

   ![새 커넥터 그룹 선택](./media/active-directory-application-proxy-connectors-azure-portal/new-group.png)

3. 새 커넥터 그룹에 이름을 지정 하 고이 그룹에 속하는 커넥터 hello 드롭다운 메뉴 tooselect을 사용 하십시오.
4. **저장**을 선택합니다.

## <a name="assign-applications-tooyour-connector-groups"></a>Tooyour 커넥터 그룹 응용 프로그램 할당
응용 프로그램 프록시를 사용하여 게시한 각 응용 프로그램에 대해 이 단계를 사용합니다. 먼저 게시, 또는 언제 든 지 이러한 단계 toochange hello 할당을 사용할 수 있습니다 때 응용 프로그램 tooa 커넥터 그룹을 할당할 수 있습니다.   

1. 디렉터리에 대 한 hello 관리 대시보드를 선택 **엔터프라이즈 응용 프로그램** > **모든 응용 프로그램** > hello tooassign tooa 커넥터 그룹을 만들려는 응용 프로그램 >  **응용 프로그램 프록시**합니다.
2. 사용 하 여 hello **커넥터 그룹** 드롭다운 메뉴 tooselect hello 그룹 응용 프로그램 toouse hello 원하는 합니다.
3. 선택 **저장** tooapply hello 변경 합니다.

## <a name="use-cases-for-connector-groups"></a>커넥터 그룹의 사용 사례 

커넥터 그룹은 다음을 비롯한 다양한 시나리오에 유용합니다.

### <a name="sites-with-multiple-interconnected-datacenters"></a>여러 데이터 센터가 연결되어 있는 사이트

많은 조직에는 서로 연결된 데이터 센터가 여러 개 있습니다. 이 경우 원하는 tookeep hello 데이터 센터 내에서 많은 트래픽을 최대한 데이터 센터 간 링크는 비용이 많이 들고 느린 때문에 있습니다. 각 데이터 센터 tooserve hello 응용 프로그램만 hello 데이터 센터 내에 있는 커넥터를 배포할 수 있습니다. 이 방법은 데이터 센터 간 링크를 최소화 하 고 tooyour 사용자 완전히 투명 한 경험을 제공 합니다.

### <a name="applications-installed-on-isolated-networks"></a>격리된 네트워크에 설치된 응용 프로그램

Hello 주요 회사 네트워크의 일부가 아닌 되는 네트워크에서 응용 프로그램을 호스팅할 수 있습니다. 격리 된 네트워크 tooalso 응용 프로그램 격리 toohello 네트워크에 커넥터 그룹 전용 tooinstall 커넥터를 사용할 수 있습니다. 이는 일반적으로 타사 공급 업체가 조직의 특정 응용 프로그램을 유지 관리할 때 발생합니다. 

커넥터 그룹을 더 안전한 toooutsource 응용 프로그램 관리 toothird 타사 공급 업체 및 있습니다 tooinstall 전용 특정 응용 프로그램을 보다 쉽게 게시 있는 네트워크에 대 한 커넥터 사용.

### <a name="applications-installed-on-iaas"></a>IaaS에 설치된 응용 프로그램 

클라우드 액세스를 위해 IaaS에 설치 된 응용 프로그램에 대 한 커넥터 그룹을 공통 서비스 toosecure hello 액세스 tooall hello 앱을 제공 합니다. 커넥터 그룹 추가 종속성이 회사 네트워크에 생성 하거나 hello 앱 환경을 조각 하지 마십시오. 커넥터는 각 클라우드 데이터 센터에 설치될 수 있으며 해당 네트워크에 있는 응용 프로그램만 처리할 수 있습니다. 여러 커넥터 tooachieve 고가용성을 설치할 수 있습니다.

예를 들어 여러 가상 컴퓨터를 사용 하는 조직을 tootheir 자체 호스팅되는 IaaS 가상 네트워크 연결을 수행 합니다. tooallow 직원 toouse 이러한 응용 프로그램 개인 네트워크는 사이트 간 VPN을 사용 하 여 연결 된 toohello 회사 네트워크입니다. 이는 온-프레미스에 있는 직원들에게 좋은 경험을 제공합니다. 하지만 원격 직원에 대 한 이상적인 아래 hello 다이어그램에서 볼 수 있듯이 추가 온-프레미스 인프라 tooroute 액세스 필요 하기 때문에 되지:

![Azure Ad Iaas 네트워크](./media/application-proxy-publish-apps-separate-networks/application-proxy-iaas-network.png)
  
Azure AD 응용 프로그램 프록시 커넥터 그룹을 사용 회사 네트워크에서 추가 종속성을 만들지 않고는 공통 서비스 toosecure hello 액세스 tooall 응용 프로그램을 설정할 수 있습니다.

![Azure AD Iaas - 여러 클라우드 공급 업체](./media/application-proxy-publish-apps-separate-networks/application-proxy-multiple-cloud-vendors.png)

### <a name="multi-forest--different-connector-groups-for-each-forest"></a>다중 포리스트 - 포리스트마다 서로 다른 커넥터 그룹

응용 프로그램 프록시를 배포한 대부분의 고객은 KCD(Kerberos 제한 위임)를 수행하여 SSO(Single-Sign-On) 기능을 사용하고 있습니다. tooachieve이 hello 커넥터의 컴퓨터 필요 toobe 조인된 tooa 도메인 hello 응용 프로그램으로 hello 사용자가 위임할 수 있습니다. KCD는 포리스트 간 기능을 지원합니다. 그러나 서로 간에 신뢰할 수 없는 고유한 다중 포리스트 환경이 있는 회사의 경우 모든 포리스트에 대해 단일 커넥터를 사용할 수 없습니다. 

이 경우 포리스트당 특정 커넥터를 배포할 수 있습니다 및 집합 tooserve 실행 된 응용 프로그램 게시 tooserve는 해당 특정 포리스트의 사용자가 hello만 합니다. 각 커넥터 그룹마다 별도의 포리스트를 나타냅니다. Hello 테 넌 트와 대부분 hello 경험의는 포리스트 전반에 대 한 통합, 하는 동안 사용자가 Azure AD 그룹을 사용 하 여 tootheir 포리스트의 응용 프로그램을 할당할 수 있습니다.
 
### <a name="disaster-recovery-sites"></a>재해 복구 사이트

다음과 같이 사이트 구현 방법에 따라 DR(재해 복구) 사이트에서 수행할 수 있는 두 가지 방법이 있습니다.

* DR 사이트가 있는 hello 주 사이트와 동일 하 게 하 고 있어서 액티브-액티브 모드에서 빌드되는 경우 동일한 hello 네트워킹과 AD 설정 hello DR 사이트에서 hello hello 커넥터를 만들 수 있습니다 hello 주 사이트와 동일한 커넥터 그룹입니다. 이 통해 사용자에 대 한 Azure AD toodetect 장애 조치 합니다.
* DR 사이트는 hello 주 사이트에서 별도 hello DR 사이트에서 다른 커넥터 그룹을 만들 수 있습니다, 하나 1) 백업 응용 프로그램이 있는 경우 또는 2) 수동으로 필요에 따라 hello 기존 응용 프로그램 toohello DR 커넥터 그룹을 전환 합니다.
 
### <a name="serve-multiple-companies-from-a-single-tenant"></a>단일 테넌트에서 여러 회사 제공

여러 가지 다른 방법으로는 단일 서비스 공급자를 배포 하 고 Azure AD를 유지 관리 모델 tooimplement 관련 여러 회사에 대 한 서비스입니다. 커넥터 그룹 도움말 admin 님 안녕하세요 hello 커넥터와 다른 그룹으로 응용 프로그램을 분리 합니다. 소규모 회사에 적합 한는 한 가지 방법은 것 toohave 단일 hello 서로 다른 회사에 들어 있는 도메인 이름 및 네트워크 하는 동안 Azure AD 테 넌 트입니다. 또한 단일 IT 부서에서 규제 또는 비즈니스 상의 이유로 여러 회사에 서비스를 제공하는 M&A 시나리오 및 상황에서도 마찬가지입니다. 

## <a name="sample-configurations"></a>샘플 구성

구현할 수 있는 몇 가지 예는 커넥터 그룹을 다음 hello를 포함 됩니다.
 
### <a name="default-configuration--no-use-for-connector-groups"></a>기본 구성 - 커넥터 그룹 사용 안 함

커넥터 그룹을 사용하지 않는 경우 구성은 다음과 같습니다.

![Azure AD - 커넥터 그룹 없음](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-1.png)
 
이 구성은 소규모 배포 및 테스트에 충분합니다. 또한 조직에 플랫 네트워크 토폴로지가 있는 경우에도 잘 작동합니다.
 
### <a name="default-configuration-and-an-isolated-network"></a>기본 구성 및 격리된 네트워크

이 구성은 발전 된 hello 기본 IaaS 가상 네트워크와 같은 격리 된 네트워크에서 실행 되는 특정 응용 프로그램은 하나입니다. 

![Azure AD - 커넥터 그룹 없음](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-2.png)
 
### <a name="recommended-configuration--several-specific-groups-and-a-default-group-for-idle"></a>권장 구성 - 여러 특정 그룹 및 유휴 상태의 기본 그룹

권장 구성 크고 복잡 한 조직에 대 한 hello은 유휴 상태가 되거나 새로 설치 된 커넥터에 사용 되는 모든 응용 프로그램을 제공 하지 않는 그룹으로 toohave hello 기본 커넥터 그룹입니다. 모든 응용 프로그램은 사용자 지정된 커넥터 그룹을 통해 제공됩니다. 이렇게 하면 위에서 설명한 hello 시나리오의 모든 hello 복잡 한 작업입니다.

Hello 아래 예제에서는 hello 회사에는 두 데이터 센터, A와 B를 각 사이트를 제공 하는 두 명의 연결선으로 있습니다. 각 사이트에는 실행되는 다양한 응용 프로그램이 있습니다. 

![Azure AD - 커넥터 그룹 없음](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-3.png)
 
## <a name="next-steps"></a>다음 단계

* [Azure AD 응용 프로그램 프록시 커넥터 이해](application-proxy-understand-connectors.md)
* [Single Sign-On 사용](application-proxy-sso-overview.md)


