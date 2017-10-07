---
title: "Azure 트래픽 관리자와 Azure에서 가용성 간 지리적 AD FS 배포 aaaHigh | Microsoft Docs"
description: "이 문서에서는 살펴보겠습니다 어떻게 toodeploy 고가용성을 위해 Azure의 AD FS 합니다."
keywords: "Azure 트래픽 관리자, adfs 지리적 Azure 트래픽 관리자, 다중 데이터 센터, 지리적 데이터 센터, 다중 지리적 데이터 센터를 사용 하 여 ad fs azure의 AD FS를 배포, azure의 adfs, adfs azure, azure ad fs 배포, adfs 배포, ad fs를 azure의 adfs 배포 ad fs를 배포 합니다. azure의 adfs tooazure 이동 azure, azure ad fs, 소개 tooAD FS, Azure, azure에서 iaas, ADFS, AD FS에서 AD FS를 배포 합니다."
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: a14bc870-9fad-45ed-acd5-a90ccd432e54
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/01/2016
ms.author: anandy;billmath
ms.openlocfilehash: c5838d749cdc5c8aabbe62b255d568525da747ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-cross-geographic-ad-fs-deployment-in-azure-with-azure-traffic-manager"></a>Azure Traffic Manager를 사용하여 Azure에서 고가용성 교차 지리적 AD FS 배포
[Azure에서 AD FS 배포](active-directory-aadconnect-azure-adfs.md) 단계별 지침을 제공 toohow로를 통해 조직에서 Azure에 대 한 간단한 AD FS 인프라를 배포할 수 있습니다. 이 문서에서는 hello 다음 단계를 사용 하 여 Azure에서 AD fs 배포 간 지리적 toocreate 제공 [Azure 트래픽 관리자](../traffic-manager/traffic-manager-overview.md)합니다. Azure 트래픽 관리자를 늘려 지리적으로 분산 고가용성 및 조직에 대 한 고성능 AD FS 인프라를 만들기를 도와줍니다 hello 인프라에서 사용 가능한 toosuit 다른 필요한 라우팅 메서드의 범위 사용 합니다.

항상 사용 가능한 교차 지리적 AD FS 인프라에서는 다음을 수행할 수 있습니다.

* **단일 실패 지점이 제거:** 장애 조치 기능이 Azure 트래픽 관리자의 얻을 수 hello 구형의 부분에 hello 데이터 센터 중 하나가 작동이 중단 하는 경우에 항상 사용 가능한 AD FS 인프라
* **향상 된 성능:** 에서는 hello이 문서 tooprovide에서 배포를 더 빠르게 인증 사용자를 지원할 수 있는 고성능 AD FS 인프라 제안 합니다. 

## <a name="design-principles"></a>디자인 원칙
![전체 디자인](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/blockdiagram.png)

hello 기본적인 디자인 원칙 Azure의 AD FS 배포 hello 문서의 디자인 원칙에 나열 된 동일한 됩니다. 위의 hello 다이어그램 hello 기본 배포 tooanother 지리적 지역의의 간단한 확장을 보여 줍니다. 아래 몇 가지 포인트 tooconsider 배포 toonew 지리적 영역을 확장 하는 경우는

* **가상 네트워크:** 새 가상 네트워크를 만들어야 합니다. 원하는 toodeploy 추가 AD FS 인프라 hello 지리적 지역에 있습니다. 위의 hello 다이어그램에 표시 Geo1 VNET과 Geo2 VNET 각 지역에 두 개의 가상 네트워크를 hello 됩니다.
* **도메인 컨트롤러와 새 지역 VNET에 AD FS 서버:** hello AD FS 서버 hello 새 영역에 toocontact 도메인 컨트롤러에 없는 다른 작업을 훨씬 있도록 hello와 새 지리적 지역에 toodeploy 도메인 컨트롤러 좋습니다 트래버스하여 네트워크 toocomplete 인증 및 개선 함으로써 hello 성능.
* **저장소 계정:** 저장소 계정은 지역과 연결됩니다. 새 지리적 지역에 컴퓨터를 배포 하 고는, 이후 toocreate toobe hello 지역에서 사용 되는 새 저장소 계정을 갖습니다.  
* **네트워크 보안 그룹:** 지역에서 만든 네트워크 보안 그룹을 다른 지역에서 저장소 계정으로 사용할 수 없습니다. 따라서 hello와 새 지리적 지역에 INT 및 DMZ 서브넷에 대 한 toocreate 새 네트워크 보안 그룹 비슷한 toothose hello와 첫 번째 지리적 지역에 필요 합니다.
* **공용 IP 주소에 대 한 DNS 레이블을:** Azure 트래픽 관리자 tooendpoints를 참조할 수 DNS 레이블을 통해 전용입니다. 따라서 hello 외부 부하 분산 장치 ' 공용 IP 주소에 대 한 필수 toocreate DNS 레이블을 있습니다.
* **Azure 트래픽 관리자:** Microsoft Azure 트래픽 관리자 hello 전 세계 다른 데이터 센터에서 실행 하는 사용자 트래픽 tooyour 서비스 끝점의 toocontrol hello 배포를 허용 합니다. Azure 트래픽 관리자는 hello DNS 수준에서 작동합니다. DNS 응답 toodirect 최종 사용자 트래픽 tooglobally 분산 끝점을 사용합니다. 클라이언트 다음 toothose 끝점을 직접 연결합니다. 성능과 중 우선 순위 라우팅 다른 옵션으로 조직의 요구에 가장 적합 하며 hello 경로 옵션을 쉽게 선택할 수 있습니다. 
* **두 영역 간 V net tooV net 연결:** 않아도 hello 가상 네트워크 간 toohave 연결 자체입니다. 각 가상 네트워크 액세스 toodomain 컨트롤러에 AD FS 및 WAP 서버 자체에 있으므로 다른 지역에 hello 가상 네트워크 간의 모든 연결 없이 작업 수 있습니다. 

## <a name="steps-toointegrate-azure-traffic-manager"></a>단계 toointegrate Azure 트래픽 관리자
### <a name="deploy-ad-fs-in-hello-new-geographical-region"></a>AD FS를 hello와 새 지리적 지역에 배포
Hello 단계와 지침에 따라 [Azure의 AD FS 배포](active-directory-aadconnect-azure-adfs.md) toodeploy hello 동일한 토폴로지 hello와 새 지리적 지역에 있습니다.

### <a name="dns-labels-for-public-ip-addresses-of-hello-internet-facing-public-load-balancers"></a>hello (공용) 부하 분산 장치 인터넷 연결 공용 IP 주소에 대 한 DNS 레이블
Hello Azure 트래픽 관리자 끝점으로 tooDNS 레이블을 참조할 수 있습니다 위에서 설명 했 듯이 되며 따라서 hello 외부 부하 분산 장치 ' 공용 IP 주소에 대 한 중요 한 toocreate DNS 레이블을 있습니다. 아래 스크린샷은 hello 공용 IP 주소에 대 한 DNS 레이블을 구성 하는 방법을 보여 줍니다. 

![DNS 레이블](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfabstsdnslabel.png)

### <a name="deploying-azure-traffic-manager"></a>Azure Traffic Manager 배포
트래픽 관리자 프로필 toocreate 아래 hello 단계를 수행 합니다. 자세한 내용은 참조할 수도 있습니다 너무[Azure 트래픽 관리자 프로필을 관리할](../traffic-manager/traffic-manager-manage-profiles.md)합니다.

1. **Traffic Manager 프로필 만들기:** Traffic Manager 프로필에 고유한 이름을 지정합니다. 이 hello 프로필의 일부인 hello DNS 이름의 이름과 역할을 트래픽 관리자 도메인 이름 레이블이 hello에 대 한 접두사입니다. hello 이름 / 트래픽 관리자에 대 한 접두사를 too.trafficmanager.net toocreate DNS 레이블을 추가 합니다. hello 아래 스크린샷은 hello 트래픽 관리자 DNS 접두사 내용이 mysts.trafficmanager.net 되므로 mysts 및 결과 DNS 레이블을 설정 합니다. 
   
    ![Traffic Manager 프로필 만들기](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/trafficmanager01.png)
2. **트래픽 라우팅 방법:** Traffic Manager에서 사용할 수 있는 세 가지 트래픽 라우팅이 있습니다.
   
   * 우선 순위 
   * 성능
   * 가중치 적용
     
     **성능** hello 옵션 tooachieve 응답성이 높은 AD FS 인프라 좋습니다. 그러나 배포 요구 사항에 가장 적합한 라우팅 방법을 선택할 수 있습니다. hello AD FS 기능 hello 라우팅 옵션을 선택 하 여 영향을 받지 않습니다. 자세한 내용은 [Traffic Manager 트래픽 라우팅 방법](../traffic-manager/traffic-manager-routing-methods.md) 을 참조하세요. Hello 위의 샘플 스크린 샷 hello를 볼 수 **성능** 메서드를 선택 합니다.
3. **끝점을 구성:** hello 트래픽 관리자 페이지에서 끝점을 클릭 하 고 추가 선택 합니다. 이 추가 끝점 페이지 비슷한 toohello 아래 스크린샷에서 열립니다.
   
   ![끝점 구성](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfsendpoint.png)
   
   Hello 서로 다른 입력 아래 hello 지침을 따릅니다.
   
   **형식:** tooan Azure 공용 IP 주소를 가리키는 것 처럼 Azure 끝점을 선택 합니다.
   
   **이름:** hello 끝점과 tooassociate 원하는 이름을 만듭니다. 이 않은 hello DNS 이름 및 DNS 레코드는 관련이 없습니다.
   
   **대상 리소스 종류:** hello value toothis 속성으로 선택 하는 공용 IP 주소입니다. 
   
   **대상 리소스:** 이렇게 하면 옵션 toochoose hello 다른 DNS 레이블에서 사용할 수 있는 구독에서 합니다. Hello DNS 레이블을 구성 하는 해당 toohello 끝점을 선택 합니다.
   
   Azure 트래픽 관리자 tooroute hello 트래픽을 원하는 각 지역에 대 한 끝점을 추가 합니다.
   자세한 내용 및 단계는 방법에 대 한 tooadd / 트래픽 관리자에서 끝점을 구성, 너무 참조[끝점을 추가, 사용 안 함, 활성화 또는 삭제](../traffic-manager/traffic-manager-endpoints.md)
4. **프로브를 구성:** hello 트래픽 관리자 페이지에서 구성을 클릭 합니다. HTTP 포트 80에서 toochange hello 모니터 설정 tooprobe 및 상대 경로 /adfs/probe 필요 hello 구성 페이지에서
   
    ![프로브 구성](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/mystsconfig.png) 
   
   > [!NOTE]
   > **Hello 끝점의 hello 상태 온라인 상태 인지 확인 hello 구성이 완료 되 면**합니다. 모든 끝점이 '저하' 상태에 있는 경우 Azure 트래픽 관리자는 hello 진단 잘못 되었습니다. 하 고 모든 끝점에 연결할 수 있는 것으로 가정 하는 최상의 시도 tooroute hello 트래픽을 수행 합니다.
   > 
   > 
5. **Azure 트래픽 관리자에 대 한 DNS 레코드를 수정:** 페더레이션 서비스 CNAME toohello Azure 트래픽 관리자 DNS 이름 이어야 합니다. CNAME에에서 만들어 hello 공용 DNS 레코드 hello Azure 트래픽 관리자에 도달 하면 실제로 누구 든 지이 tooreach hello 페더레이션 서비스 하려고 시도 합니다.
   
    예를 들어, toopoint hello 페더레이션 서비스 fs.fabidentity.com toohello 트래픽 관리자 tooupdate를 수행 하 여 DNS 리소스 레코드 toobe hello 필요 합니다.
   
    <code>fs.fabidentity.com IN CNAME mysts.trafficmanager.net</code>

## <a name="test-hello-routing-and-ad-fs-sign-in"></a>테스트 hello 라우팅 및 AD FS 로그인
### <a name="routing-test"></a>테스트 라우팅
Hello 라우팅에 대 한 매우 기본적인 테스트 tootry ping hello 페더레이션 서비스에서에서 DNS 이름을 각 지역에 있는 컴퓨터는 것입니다. Hello 라우팅 방법 선택에 따라 실제로 ping hello 끝점 hello ping 디스플레이에 반영 됩니다. 예를 들어 hello 성능을 선택한 경우 toohello 가장 가까운 hello 끝점 다음 라우팅 hello 클라이언트의 영역에 도달 됩니다. 다음은 두 개의 다른 지역의 클라이언트 컴퓨터에서 ping을 두 번의 hello 스냅숏을 한국 우편 영역에 하나, 하나는 West US에입니다. 

![테스트 라우팅](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/pingtest.png)

### <a name="ad-fs-sign-in-test"></a>AD FS 로그인 테스트
hello 가장 쉬운 방법은 tootest AD FS hello IdpInitiatedSignon.aspx 페이지를 사용 하는 것입니다. 에 필요한 tooenable 순서 toobe 수 toodo IdpInitiatedSignOn hello AD FS 속성에 hello 합니다. AD FS 설치 tooverify 아래 hello 단계를 수행 합니다.

1. 실행 hello tooset PowerShell을 사용 하 여 hello AD FS 서버의 cmdlet 아래 것 tooenabled 합니다. 
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true
2. 외부 컴퓨터에서 https://<yourfederationservicedns>/adfs/ls/IdpInitiatedSignon.aspx에 액세스합니다.
3. AD FS hello 페이지가 표시 되어야 다음과 유사한:
   
    ![ADFS 테스트 - 인증 질문](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest1.png)
   
    그리고 성공적으로 로그인하면 아래와 같은 성공 메시지가 표시됩니다.
   
    ![ADFS 테스트 - 인증 성공](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest2.png)

## <a name="related-links"></a>관련 링크
* [Azure에서 기본 AD FS 배포](active-directory-aadconnect-azure-adfs.md)
* [Microsoft Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md)
* [트래픽 관리자 트래픽 라우팅 방법](../traffic-manager/traffic-manager-routing-methods.md)

## <a name="next-steps"></a>다음 단계
* [Azure 트래픽 관리자 프로필 관리](../traffic-manager/traffic-manager-manage-profiles.md)
* [끝점 추가, 사용 안 함, 사용 또는 삭제](../traffic-manager/traffic-manager-endpoints.md) 

