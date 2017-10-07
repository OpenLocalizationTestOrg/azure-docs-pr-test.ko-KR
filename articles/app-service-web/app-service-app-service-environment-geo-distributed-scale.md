---
title: "앱 서비스 환경에 분산 조정 aaaGeo"
description: "Toohorizontally 트래픽 관리자 및 앱 서비스 환경을 사용 하 여 전 세계 분산을 사용 하 여 앱을 확장 하는 방법을 알아봅니다."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: c1b05ca8-3703-4d87-a9ae-819d741787fb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: stefsch
ms.openlocfilehash: 9b441f637d8b7f679b3d83240baf99b8ee57e8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="geo-distributed-scale-with-app-service-environments"></a>앱 서비스 환경으로 지역 분산된 규모
## <a name="overview"></a>개요
응용 프로그램 필요한 시나리오는 매우 높은 대규모 hello 계산 리소스 용량 사용 가능한 tooa 단일 배포 응용 프로그램을 초과할 수 있습니다.  투표 응용 프로그램, 스포츠 이벤트 및 방송된 엔터테인먼트 이벤트는 대규모를 필요로 하는 시나리오를 모두 포함하는 예입니다. 가로로 영역, toohandle 극단적인 부하 요구 사항 뿐만 아니라 단일 지역 내에서 수행 되는 여러 응용 프로그램 배포 응용 프로그램을 확장 하 여 대규모 요구 사항은 충족할 수 있습니다.

앱 서비스 환경은 수평적 규모 확장에 대한 이상적인 플랫폼입니다.  앱 서비스 환경 구성 선택 하 고 나면 알려진된 요청 속도 지원할 수 있는, 개발자가 "쿠키 커터" 방식으로 tooattain 원하는 최고 부하 용량에에서 앱 서비스 환경을 배포할 수 있습니다.

예를 들어 앱 서비스 환경 구성에서 실행 되는 응용 프로그램 (RP) 초당 테스트 된 toohandle 20k 요청 된 가정 합니다.  Hello 원하는 최대 로드 용량이 100k RPS, 다음 5 앱 서비스 환경을 만들 수 있습니다 및 구성 된 tooensure hello 응용 프로그램 hello 최대 예상된 부하를 처리할 수 있습니다.

고객은 일반적으로 사용자 지정 이동해 왔거나 베 니 티 도메인, 개발자가 필요를 사용 하 여 앱 액세스 하므로 hello 앱 서비스 환경 인스턴스의 모든 방식으로 toodistribute 응용 프로그램을 요청 합니다.  이 좋은 방법 tooaccomplish tooresolve hello 사용자 지정 도메인 사용 하는 [Azure 트래픽 관리자 프로필][AzureTrafficManagerProfile]합니다.  개별 앱 서비스 환경 hello 하는 hello 트래픽 관리자 프로필의 모든 구성된 toopoint 될 수 있습니다.  트래픽 관리자 고객 모든 hello hello 부하 분산 hello 트래픽 관리자 프로필의 설정에 따라 앱 서비스 환경에서 배포를 자동으로 처리 합니다.  이 방법은 여부에 관계 없이 모든 hello 앱 서비스 환경 되는 단일 Azure 지역에 배포 된 전 세계 여러 Azure 지역에 배포할 수 있습니다.

또한 고객을 hello 베 니 티 도메인을 통해 앱에 액세스 하므로 고객은 인식 응용 프로그램을 실행 하는 앱 서비스 환경 hello 수 없습니다.  결과적으로 개발자는 앱 서비스 환경을 관찰된 트래픽 부하에 따라 쉽고 빠르게 추가 및 제거할 수 있습니다.

아래 hello 개념적 다이어그램에서는 단일 지역 내에서 3 개의 앱 서비스 환경에 걸쳐 가로로 확장 하는 응용 프로그램을 보여 줍니다.

![개념적 아키텍처][ConceptualArchitecture] 

이 항목의 나머지 부분에서는 hello 관련된 된 여러 앱 서비스 환경을 사용 하 여 hello 샘플 응용 프로그램에 대 한 분산된 토폴로지를 설정 하는 hello 단계를 안내 합니다.

## <a name="planning-hello-topology"></a>Hello 토폴로지를 계획합니다.
분산된 응용 프로그램 사용 공간이 아웃 빌드하기 전에 수 toohave 조각 정보를 미리 몇 가지 있습니다.

* **Hello 앱에 대 한 사용자 지정 도메인:** 고객에서 tooaccess hello 앱을 사용 하는 hello 사용자 지정 도메인 이름은 무엇입니까?  Hello 샘플 응용 프로그램 hello 사용자 지정 도메인 이름이 *www.scalableasedemo.com*
* **트래픽 관리자 도메인:** 도메인 이름을 만들 때 선택한 toobe 필요는 [Azure 트래픽 관리자 프로필][AzureTrafficManagerProfile]합니다.  이 이름은 hello로 결합 됩니다 *trafficmanager.net* tooregister 트래픽 관리자에서 관리 되는 도메인 항목 접미사입니다.  Hello 샘플 응용 프로그램에 대 한 hello 이름 선택은 *ase 데모 확장 가능한*합니다.  따라서 hello 전체 도메인 이름을 트래픽 관리자에서 관리 되는 *ase demo.trafficmanager.net 확장 가능한*합니다.
* **Hello 응용 프로그램 사용 공간 크기 조정에 대 한 전략:** hello 응용 프로그램의 공간에 배포 되는 단일 지역에서 여러 앱 서비스 환경?  여러 영역?  두 방법을 혼합 및 일치?  hello 의사 결정 고객 트래픽이 발생 한 위치,도 안녕하세요 rest 응용 프로그램을 지 원하는 백 엔드 인프라의 크기를 조정할 수 하는 방법의 기대치를 기반으로 해야 합니다.  예를 들어 100% 상태 비저장 응용 프로그램의 경우 Azure 지역 마다 여러 App Service Environment의 조합을 사용하여 앱을 크게 확장할 수 있으며 여러 Azure 지역에 걸쳐 배포된 App Service Environment로 곱해집니다.  15 + 공용 Azure 지역에서 사용할 수 있는 toochoose, 고객 전세계 대규모 응용 프로그램의 공간 진정으로 빌드할 수 있습니다.  이 문서에 사용 되는 hello 샘플 응용 프로그램을 세 가지 앱 서비스 환경에는 단일 Azure 지역 (미국 중남부) 생성 되었습니다.
* **앱 서비스 환경 hello에 대 한 명명 규칙:** Each 앱 서비스 환경 이름은 고유 해야 합니다.  하나 또는 두 개의 앱 서비스 환경 이외의 것이 유용한 toohave 명명 규칙 toohelp 각 앱 서비스 환경을 식별 합니다.  Hello 샘플 응용 프로그램에 대 한 간단한 명명 규칙이 사용 되었습니다.  hello hello 3 앱 서비스 환경 이름은 소문자 *fe1ase*, *fe2ase*, 및 *fe3ase*합니다.
* **Hello 앱에 대 한 명명 규칙:** hello 배포 된 앱의 각 인스턴스에 대해은 이름을 hello 앱의 여러 인스턴스를 배포할 하므로 필요 합니다.  앱 서비스 환경을 잘 알려지지 않은 있지만 매우 편리 하 게 기능 중 하나는 응용 프로그램 이름이 같은 여러 앱 서비스 환경에 걸쳐 사용할 수는 hello입니다.  각 앱 서비스 환경에 고유한 도메인 접미사가 있으므로 개발자는 각 환경에 사용 가능한 toore hello과 같은 응용 프로그램 이름을 선택할 수 있습니다.  예를 들어 개발자가 앱을 *myapp.foo1.p.azurewebsites.net*, *myapp.foo2.p.azurewebsites.net*, *myapp.foo3.p.azurewebsites.net* 등과 같이 명명할 수 있습니다.  Hello 샘플 응용 프로그램에 대 한 하지만 각 응용 프로그램 인스턴스 또한 고유한 이름이 지정 됩니다.  hello 사용 되는 응용 프로그램 인스턴스 이름은 *webfrontend1*, *webfrontend2*, 및 *webfrontend3*합니다.

## <a name="setting-up-hello-traffic-manager-profile"></a>트래픽 관리자 프로필 hello 설정
응용 프로그램의 여러 인스턴스는 여러 앱 서비스 환경에 배포 된 후 hello 개별 앱 인스턴스 트래픽 관리자를 등록할 수 있습니다.  Hello 샘플 응용 프로그램 트래픽 관리자 프로필에 대 한 필요한 *ase demo.trafficmanager.net 확장 가능한* 고객 배포의 다음 hello tooany 앱 인스턴스를 라우팅할 수 있는:

* **webfrontend1.fe1ase.p.azurewebsites.net:** hello 샘플 응용 프로그램에 배포 된 인스턴스의 hello 첫 번째 앱 서비스 환경입니다.
* **webfrontend2.fe2ase.p.azurewebsites.net:** hello 샘플 응용 프로그램에 배포 된 인스턴스의 hello 두 번째 앱 서비스 환경입니다.
* **webfrontend3.fe3ase.p.azurewebsites.net:** hello 샘플 응용 프로그램에 배포 된 인스턴스의 hello 세 번째 앱 서비스 환경입니다.

가장 쉬운 방법은 tooregister 여러 Azure 앱 서비스 끝점을 hello에서 모두 실행 hello **동일한** hello Powershell로는 Azure 지역 [Azure 리소스 관리자 트래픽 관리자 지원] [ ARMTrafficManager].  

hello 첫 번째 단계는 Azure 트래픽 관리자 프로필 toocreate입니다.  hello 코드 아래 hello 샘플 응용 프로그램에 대 한 hello 호스트 프로필이 생성 되었는지는 방법을 보여 줍니다.

    $profile = New-AzureTrafficManagerProfile –Name scalableasedemo -ResourceGroupName yourRGNameHere -TrafficRoutingMethod Weighted -RelativeDnsName scalable-ase-demo -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"

Hello 어떻게 확인 *RelativeDnsName* 매개 변수를 너무 설정한*ase 데모 확장 가능한*합니다.  도메인 이름 어떻게 hello은이 *ase demo.trafficmanager.net 확장 가능한* 생성 되어 트래픽 관리자 프로필과 연결 된입니다.

hello *TrafficRoutingMethod* hello 부하 분산 트래픽 관리자 toodetermine hello 사용 가능한 끝점의 모든 toospread 고객을 로드 하는 방법에서 사용 하는 정책 매개 변수를 정의 합니다.  이 예제에서는 hello에 *가 중* 메서드 선택 되었습니다.  이렇게 하면 모든 hello 등록 응용 프로그램 끝점에 연결 된 각 끝점 hello 상대 가중치에 따라 분산 되 고 고객 요청 합니다. 

각 응용 프로그램 인스턴스는 만든 hello 프로필을 기본 Azure 끝점으로 toohello 프로필을 추가 됩니다.  아래 hello 코드 참조 tooeach 프런트 엔드 웹 응용 프로그램을 가져오고 hello 통해 트래픽 관리자 끝점으로 각 응용 프로그램을 추가 하는 다음 *TargetResourceId* 매개 변수입니다.

    $webapp1 = Get-AzureRMWebApp -Name webfrontend1
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend1 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp1.Id –EndpointStatus Enabled –Weight 10

    $webapp2 = Get-AzureRMWebApp -Name webfrontend2
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend2 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp2.Id –EndpointStatus Enabled –Weight 10

    $webapp3 = Get-AzureRMWebApp -Name webfrontend3
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend3 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp3.Id –EndpointStatus Enabled –Weight 10

    Set-AzureTrafficManagerProfile –TrafficManagerProfile $profile

되어 한 번의 호출 너무*추가 AzureTrafficManagerEndpointConfig* 각 개별 응용 프로그램 인스턴스에 대 한 합니다.  hello *TargetResourceId* 각 Powershell 명령에서 매개 변수 hello 세 가지 배포 응용 프로그램 인스턴스 중 하나를 참조 합니다.  트래픽 관리자 프로필 hello hello 프로필에 등록 된 모든 세 끝점에서 부하를 분산 됩니다.

Hello에 대 한 동일한 값 (10) hello hello 세 끝점 사용의 모든 *가중치* 매개 변수입니다.  그러면 트래픽 관리자에서 세 가지 앱 인스턴스에 상대적으로 균일하게 고객 요청을 분산하게 됩니다. 

## <a name="pointing-hello-apps-custom-domain-at-hello-traffic-manager-domain"></a>트래픽 관리자 도메인 hello에서 hello 응용 프로그램의 사용자 지정 도메인을 가리키는
필요한 hello 마지막 단계에는 hello toopoint hello 트래픽 관리자 도메인에 hello 응용 프로그램의 사용자 지정 도메인입니다.  가리키는 즉 hello 샘플 응용 프로그램에 대 한 *www.scalableasedemo.com* 에서 *ase demo.trafficmanager.net 확장 가능한*합니다.  이 단계는 toobe hello 사용자 지정 도메인을 관리 하는 hello 도메인 등록 기관에 완료 해야 합니다.  

등록자의 도메인 관리 도구를 사용 하 여 CNAME 레코드 요구 toobe hello 트래픽 관리자 도메인에서 어떤 지점 hello 사용자 지정 도메인을 생성 합니다.  아래 hello 그림이 CNAME 구성의 모양을의 예를 보여 줍니다.

![사용자 지정 도메인에 대한 CNAME][CNAMEforCustomDomain] 

이 항목에서 설명 하지 않지만 각 개별 앱 인스턴스 toohave hello 사용자 지정 도메인 등록 된도 필요 함을 기억 합니다.  그렇지 않으면 요청 tooan 응용 프로그램 인스턴스를 사용 하면 hello 응용 프로그램 등록 hello 앱 된 hello 사용자 지정 도메인이 없는 경우 hello 요청이 실패 합니다.  

사용자 지정 도메인은이 예제에서는 hello *www.scalableasedemo.com*, 하며 각 응용 프로그램 인스턴스에 연결 된 hello 사용자 지정 도메인입니다.

![사용자 지정 도메인][CustomDomain] 

Azure 앱 서비스 앱을 사용자 지정 도메인을 등록에 대해 간략하게, hello 다음 문서를 참조 하세요. [사용자 지정 도메인 등록][RegisterCustomDomain]합니다.

## <a name="trying-out-hello-distributed-topology"></a>시험적으로 hello 분산 토폴로지
hello hello 트래픽 관리자 및 DNS 구성의 최종 결과 요청에 대 한 *www.scalableasedemo.com* 순서 따르면 hello를 통해 전달 됩니다.

1. 브라우저 또는 장치는 *www.scalableasedemo.com*
2. hello hello 도메인 등록 기관에서 CNAME 항목 hello DNS 조회 리디렉션 toobe tooAzure 트래픽 관리자 하면 됩니다.
3. 에 대 한 DNS 조회 *ase demo.trafficmanager.net 확장 가능한* hello Azure 트래픽 관리자 DNS 서버 중 하나에 대 한 합니다.
4. Hello 부하 분산 정책에 따라 (hello *TrafficRoutingMethod* hello 트래픽 관리자 프로필을 만들 때 이전에 사용 되는 매개 변수), 트래픽 관리자는 hello 중 하나를 선택 끝점을 구성 하 고 반환 하는의 FQDN hello 끝점 toohello 브라우저 또는 장치입니다.
5. 앱 서비스 환경에서 실행 되는 응용 프로그램 인스턴스의 hello Url hello hello 끝점의 FQDN 이므로, hello 브라우저나 장치로 묻습니다 Microsoft Azure DNS 서버 tooresolve hello FQDN tooan IP 주소. 
6. hello 브라우저나 장치로 hello HTTP/S 요청 toohello IP 주소를 전송 합니다.  
7. hello 앱 서비스 환경 중 하나에서 실행 되는 hello 앱 인스턴스 중 하나에 도달 하는 hello 요청 합니다.

hello 콘솔 아래 그림과 hello 샘플 응용 프로그램의 사용자 지정 도메인 성공적으로 확인 하 고 tooan 응용 프로그램에서 실행 중인 인스턴스 hello 3 샘플 앱 서비스 환경 중 하나에 대 한 DNS 조회 (이 경우 앱 서비스 환경 hello 3 중 두 번째 hello):

![DNS 조회][DNSLookup] 

## <a name="additional-links-and-information"></a>추가 링크 및 정보
모든 문서와 방법을-hello에서 사용할 수 있는 앱 서비스 환경에 대 한의 하려면 [응용 프로그램 서비스 환경에 대 한 추가 정보](../app-service/app-service-app-service-environments-readme.md)합니다.

Powershell hello에 대 한 설명서 [Azure 리소스 관리자 트래픽 관리자 지원][ARMTrafficManager]합니다.  

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[AzureTrafficManagerProfile]: ../traffic-manager/traffic-manager-manage-profiles.md
[ARMTrafficManager]: ../traffic-manager/traffic-manager-powershell-arm.md
[RegisterCustomDomain]: app-service-web-tutorial-custom-domain.md


<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-geo-distributed-scale/ConceptualArchitecture-1.png
[CNAMEforCustomDomain]:  ./media/app-service-app-service-environment-geo-distributed-scale/CNAMECustomDomain-1.png
[DNSLookup]:  ./media/app-service-app-service-environment-geo-distributed-scale/DNSLookup-1.png
[CustomDomain]:  ./media/app-service-app-service-environment-geo-distributed-scale/CustomDomain-1.png 
