---
title: "앱 서비스 환경 v1 aaaHow tooConfigure"
description: "구성, 관리 및 hello 앱 서비스 환경 v 1의 모니터링"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: b5a1da49-4cab-460d-b5d2-edd086ec32f4
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: f9539a72517276d8a1e340a408841561e8b8f56d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-an-app-service-environment-v1"></a>App Service Environment v1 구성

> [!NOTE]
> 앱 서비스 환경 v1 hello에 대 한이 문서는입니다.  최신 버전의 hello 쉽게 toouse 되며 더 강력한 인프라에서 실행 하는 앱 서비스 환경 있습니다. hello로 시작 하는 hello 새 버전에 대 한 자세한 toolearn [소개 toohello 앱 서비스 환경](../app-service/app-service-environment/intro.md)합니다.
> 

## <a name="overview"></a>개요
Azure 앱 서비스 환경은 크게 몇 가지 주요 구성 요소로 이루어져 있습니다.

* 호스 티 드 서비스 hello 앱 서비스 환경에서에서 실행 되는 계산 리소스
* 저장소
* 데이터베이스
* 클래식(V1) 또는 Resource Manager(V2) Azure 가상 네트워크(VNet) 
* 것에서 실행 되는 hello 앱 서비스 환경 호스팅된 서비스를 사용 하 여 서브넷

### <a name="compute-resources"></a>계산 리소스
4 개의 리소스 풀에 대 한 hello 계산 리소스를 사용합니다.  각 ASE(앱 서비스 환경)에는 프런트 엔드 1개 및 가능한 작업자 풀 3개로 이루어진 집합이 있습니다. 모든 세 작업자 풀-toouse 필요 하지 않습니다을 삼아 하나 또는 두 개의 합니다.

hello 호스트 hello 리소스 풀 (프런트 엔드 및 작업자)에 직접 액세스할 수 있는 tootenants 않습니다. Tooconnect toothem 프로토콜 RDP (원격 데스크톱)를 사용 하 여 하, 해당 프로 비전 변경 하거나에 관리자의 역할을 할 수 없습니다.

리소스 풀 수량 및 크기를 설정할 수 있습니다. ASE에서 P1-P4 레이블이 지정된 4개의 크기 옵션이 있습니다. 해당 크기 및 가격에 대한 자세한 내용은 [앱 서비스 가격](../app-service/app-service-value-prop-what-is.md)을 참조하세요.
Hello 수량 또는 크기를 변경 합니다. 크기 조정 작업이 호출 됩니다.  한 번에 하나의 크기 조정 작업만 진행할 수 있습니다.

**프런트 엔드**: hello 프런트 엔드 프로그램 ASE에 저장 된 앱에 대 한 hello HTTP/HTTPS 끝점에는 있습니다. 실행 하지 작업 hello에 프런트 엔드 합니다.

* ASE는 개발/테스트 워크로드 및 하위 수준 프로덕션 워크로드에 충분한 2개의 P2로 시작합니다. 이 P3s 보통 tooheavy에 대 한 프로덕션 작업.
* 보통 tooheavy 프로덕션 작업에 대 한 예약 된 유지 관리 발생할 때 실행 하는 충분 한 프런트 엔드는 4 개 이상의 P3s tooensure을 해야 하는 것이 좋습니다. 예약된 유지 관리 작업은 한 번에 하나의 프런트 엔드를 종료합니다. 따라서 유지 관리 작업 동안 전반적으로 사용 가능한 프런트 엔드 용량이 줄어듭니다.
* 프런트 엔드 tooan 시간 tooprovision 차지할 수 있습니다. 
* 더 이상 눈금 미세 조정에 대 한 hello CPU 비율, 메모리 비율 및 hello 프런트 엔드 풀에 대 한 활성 요청 메트릭을 모니터링 해야 합니다. Hello CPU 또는 메모리 비율을 70% 이상 P3s를 실행 하는 경우 더 많은 프런트 엔드를 추가 합니다. 활성 요청 값 hello too15, 000 too20, 프런트 엔드 당 000 요청 평균, 더 많은 프런트 엔드 추가 해야 합니다. hello 전반적인 목표는 tookeep CPU 및 메모리 백분율 70%에서 활성 요청을 처리 하며 평균 toobelow 아웃 프런트 엔드 당 15, 000 요청 P3s를 실행 하는 경우 아래 합니다.  

**작업자**: hello 작업자는 앱 실제로 실행 합니다. 수직 확장 hello의 작업자를 사용 하 여 작업자 풀 연결 된 해당 앱 서비스 계획입니다.

* 작업자를 즉시 추가할 수 없습니다. Tooan 시간 tooprovision을 소비 될 수 있습니다.
* 모든 풀에 대 한 계산 리소스의 hello 크기 업데이트 도메인 별로 < 1 시간 소요 됩니다. ASE에 20개의 업데이트 도메인이 있습니다. 10 개의 인스턴스를 사용 하 여 작업자 풀의 hello 계산 크기의 배율 조정 too10 시간 toocomplete를 걸릴 수 있습니다.
* 작업자 풀에 사용 되는 hello 계산 리소스의 hello 크기를 변경 하면 해당 작업자 풀에서 실행 되는 hello 앱의 콜드 시작 하면 합니다.

모든 앱을 실행 하지 않는 작업자 풀의 리소스 크기를 계산 하는 toochange hello hello 가장 빠른 방법은입니다.

* 작업자 too2의 hello 수량을 축소 합니다.  hello 포털에서 크기 아래로 hello 최소 소수 자릿수는 2입니다. 몇 분 toodeallocate 사용자 인스턴스가 사용 합니다. 
* Hello 새 계산 크기와 인스턴스 수를 선택 합니다. 여기에서 too2 시간 toocomplete 최대 걸립니다.

앱 요구할 경우 더 큰 계산 리소스 크기, 활용 hello 이전 지침을 사용할 수 없습니다. 그러한 응용 프로그램을 호스팅하는 hello 작업자 풀의 hello 크기를 변경 하는 대신 hello 원하는 크기의 작업자와 다른 작업자 풀 채운 toothat 풀을 통해 앱을 이동 합니다.

* Hello 다른 작업자 풀의 크기를 계산 하는 데 필요한 hello의 추가 인스턴스를 만듭니다. 이를 tooan 시간 toocomplete 소요 됩니다.
* 더 큰 크기 toohello 새로 구성 된 작업자 풀 해야 하는 hello 앱을 호스트 하 여 앱 서비스 계획을 다시 할당 합니다. 분 toocomplete 보다 작은 수행 해야 하는 빠른 작업입니다.  
* 이러한 사용 되지 않은 인스턴스를 더 이상 필요 없는 경우 hello 첫 번째 작업자 풀을 축소 합니다. 이 작업은 몇 분 toocomplete.

**자동 크기 조정**: 하나 수 있는 toomanage hello 도구의 계산 리소스 사용량은 자동 크기 조정 합니다. 프런트 엔드 또는 작업자 풀에 대해 자동 크기 조정을 사용할 수 있습니다. Hello 아침에서 증가 등 모든 풀 형식의 인스턴스를 수행할 수 있으며 hello 저녁에 줄일 수 있습니다. 또는 아마도 hello 작업자 풀에서 사용할 수 있는 작업자 수가 특정 임계값 아래로 떨어질 경우 인스턴스 추가할 수 있습니다.

계산 리소스 풀 메트릭 주위 tooset 자동 크기 조정 규칙을 사용할 경우 해당 프로 비전 유의 hello 시간에 유지 해야 합니다. 앱 서비스 환경 자동 크기 조정에 대 한 자세한 내용은 참조 하십시오. [어떻게 앱 서비스 환경에서 자동 크기 조정 tooconfigure][ASEAutoscale]합니다.

### <a name="storage"></a>저장소
ASE 각각은 500GB의 저장소로 구성됩니다. 이 공간은 ASE hello에서 모든 hello 앱에서 사용 됩니다. 이 저장 공간 hello ASE의 일부인 및 현재 커야 바뀌면된 toouse 저장 공간 합니다. Toostill 필요한 경우 조정 tooyour 가상 네트워크 수신 라우팅 서버 또는 보안을 수행 하면 액세스 tooAzure-저장소를 허용 하거나 hello ASE 작동 하지 않을 수 있습니다.

### <a name="database"></a>데이터베이스
hello 데이터베이스 내에서 실행 되는 hello 앱에 대 한 hello 정보 뿐만 아니라 hello 환경을 정의 하는 hello 정보를 보유 합니다. 너무 hello Azure 보유 구독의 부분입니다. 되었기 직접 기능 toomanipulate를 수 있습니다. Toostill 필요한 경우 조정 tooyour 가상 네트워크 수신 라우팅 서버 또는 보안을 수행 하면 액세스 tooSQL Azure-허용 또는 hello ASE 작동 하지 않을 수 있습니다.

### <a name="network"></a>네트워크
hello 프로그램 ASE 함께 사용 되는 VNet hello ASE를 만들 때 설정한 또는 미리 설정한 수 있습니다. Hello에 hello ASE toobe ASE 만드는 동안 hello 서브넷을 만들 때 강제로 hello 가상 네트워크와 동일한 리소스 그룹입니다. Hello 리소스 그룹 프로그램 ASE toobe 다른 컨텍스트를 VNet에서 사용 해야 할 경우 다음 필요한 toocreate 리소스 관리자 템플릿을 사용 하 여 ASE 합니다.

ASE에 사용 되는 hello 가상 네트워크에 몇 가지 제한 사항이 있습니다.

* hello 가상 네트워크를 지역 가상 네트워크가 있어야 합니다.
* Toobe hello ASE를 배포 하는 8 개 이상의 주소를 사용 하 여 서브넷 필요 합니다.
* 서브넷에 사용 되는 toohost ASE 되 면 hello 서브넷의 hello 주소 범위를 변경할 수 없습니다. 이러한 이유로 hello 서브넷 주소가 이상 64 tooaccommodate 향후 ASE 성장을 포함 하는 것이 좋습니다.
* Hello ASE hello 서브넷에서 다른 수 있습니다.

Hello ASE를 포함 하는 hello 호스팅된 서비스와는 달리 hello [가상 네트워크] [ virtualnetwork] 및 사용자 정의 컨트롤에서는 서브넷입니다.  가상 네트워크 UI hello 또는 PowerShell을 통해 가상 네트워크를 관리할 수 있습니다.  ASE는 클래식 또는 Resource Manager VNet에 배포될 수 있습니다.  hello 포털 및 API 경험 클래식에서 리소스 관리자 Vnet와 약간 다릅니다 있더라도 hello ASE 경험 동일 hello 됩니다.

사용 되는 toohost ASE VNet hello 개인 r f c 1918의 IP 주소 중 하나를 사용할 수 또는 공용 IP 주소를 사용할 수 있습니다.  원하는 toouse r f c 1918에서 다루지 않은 IP 범위 (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16) toocreate VNet과 서브넷 toobe ASE 생성 미리 ASE 프로그램에서 사용 해야 합니다.

이 기능에는 가상 네트워크에 Azure 앱 서비스 hello 배치, 때문에 프로그램 ASE에서 호스트 되는 앱 직접 ExpressRoute 또는 사이트 간 가상 사설망 (Vpn)을 통해 사용할 수 있는 리소스에 지금 액세스할 수를 의미 합니다. 앱 서비스 환경 내에 있는 hello 앱 추가 네트워킹 기능 tooaccess 리소스 사용 가능한 toohello 가상 네트워크 앱 서비스 환경을 호스팅하는 필요 하지 않습니다. 즉,에 toouse VNET 통합 또는 하이브리드 연결 tooget tooresources 또는 연결 된 tooyour 가상 네트워크 필요 하지 않습니다. 여전히 모두 사용할 수 있습니다 이러한 기능의 tooyour 가상 네트워크를 연결 되지 않은 네트워크의 tooaccess 리소스 것입니다.

예를 들어 VNET 통합 toointegrate은 구독에 있지만 프로그램 ASE에 있는 연결 된 toohello 가상 네트워크는 가상 네트워크와 함께 사용할 수 있습니다. 하이브리드 연결 tooaccess 리소스와 마찬가지로 일반적으로 다른 네트워크에 있는 계속 사용할 수 있습니다.  

가상 네트워크는 ExpressRoute VPN을 사용 하 여 구성, 있는 경우에 ASE에 hello 라우팅 요구 사항 중 일부의 알고 있어야 합니다. ASE와 호환되지 않는 일부 사용자 정의 경로(UDR) 구성이 있습니다. ExpressRoute를 사용하는 가상 네트워크에서 ASE 실행에 대한 자세한 내용은 [ExpressRoute를 사용하는 가상 네트워크에서 App Service Environment 실행][ExpressRoute]을 참조하세요.

#### <a name="securing-inbound-traffic"></a>인바운드 트래픽 보안
두 가지 기본 방법을 toocontrol는 인바운드 트래픽을 tooyour ASE 합니다.  네트워크 보안 Groups(NSGs) toocontrol 어떤 IP를 사용할 수 있습니다 주소 여기에 설명 된 대로 사용자 ASE에 액세스할 수 [어떻게 toocontrol 인바운드 앱 서비스 환경에서 트래픽을](app-service-app-service-environment-control-inbound-traffic.md) 내부 부하로 프로그램 ASE를 구성할 수도 있습니다 Balancer(ILB) 합니다.  이러한 기능은 Nsg tooyour ILB ASE를 사용 하 여 toorestrict 액세스 하려는 경우에 함께 사용할 수 있습니다.

ASE를 만들면 VNet에 VIP가 만들어집니다.  외부 및 내부의 두 가지 VIP 유형이 있습니다.  외부 VIP를 사용하여 ASE를 만들 경우 ASE의 앱에 인터넷 라우팅 가능 IP 주소를 통해 액세스할 수 있습니다. 내부를 선택하는 경우 ASE는 ILB로 구성되고, 인터넷에 직접 액세스할 수 없습니다.  ILB ASE는 외부 VIP가 여전히 필요하지만 Azure 관리 및 유지 관리 액세스에만 사용됩니다.  

ILB ASE를 만드는 동안 hello ILB ASE에서 사용 하는 hello 하위 도메인을 제공 하 고 지정한 hello 하위 도메인에 대해 고유한 DNS toomanage 갖습니다.  Hello 하위 도메인 이름 설정 때문에 HTTPS 액세스에 사용 되는 toomanage hello 인증서도 필요 합니다.  ASE 생성 중인 tooprovide hello 인증서 라는 메시지가 표시 됩니다.  만들기 및 ILB ASE를 사용 하 여에 대해 자세히 toolearn 읽을 [는 내부 부하 분산 장치를 사용 하 여 앱 서비스 환경으로][ILBASE]합니다. 

## <a name="portal"></a>포털
관리 하 고 hello Azure 포털에에서 UI hello를 사용 하 여 앱 서비스 환경을 모니터링할 수 있습니다. ASE를 사용 하도록 설정한 경우 라면 가능성이 toosee hello 앱 서비스 기호 프로그램 사이드바 합니다. 이 기호는 hello Azure 포털에서에서 사용 되는 toorepresent 앱 서비스 환경.

![앱 서비스 환경 기호][1]

tooopen 앱 서비스 환경 모두 나열 하는 UI hello, hello 아이콘 또는 select hello 펼침 단추를 사용할 수 있습니다 (">" 기호) hello 사이드바 tooselect 앱 서비스 환경 hello 맨 아래에 있습니다. 나열 된 hello ASEs 중 하나를 선택 하 여 hello toomonitor 사용된 되는 UI를 열고 관리 합니다.

![앱 서비스 환경을 모니터링 및 관리하기 위한 UI][2]

이 첫 번째 블레이드는 리소스 풀 단위당 메트릭 차트와 함께 ASE의 속성 일부를 보여 줍니다. Hello에 표시 된 hello 속성 중 일부를 **Essentials** 블록 연결 된 hello 블레이드를 열 수 있는 하이퍼링크도 있습니다. 예를 들어 hello를 선택할 수 있습니다 **가상 네트워크** hello 프로그램 ASE에서 실행 되는 가상 네트워크와 연결 된 이름 tooopen hello UI 합니다. **App Service 계획** 및 **앱**은 각각 ASE에 있는 이러한 항목을 나열하는 블레이드를 엽니다.  

### <a name="monitoring"></a>모니터링
hello 차트를 사용 하면 다양 한 각 리소스 풀의 성능 메트릭 toosee 있습니다. Hello 프런트 엔드 풀에 대 한 hello 평균 CPU 및 메모리를 모니터링할 수 있습니다. 에 대 한 작업자 풀 사용 되는 hello 수량 및 사용할 수 있는 hello 수량을 모니터링할 수 있습니다.

여러 앱 서비스 계획을 만들 수는 hello 작업자의 작업자 풀 사용 합니다. hello 작업 게 hello CPU 및 메모리 사용량 거의 hello 방식으로의 유용한 정보를 제공 하지 않는 hello 프런트 엔드 서버와 마찬가지로 방식으로 동일한 hello에 배포 되지 않는 합니다. 더 중요 한 tootrack는 개수에 사용한 작업자 및-사용 가능한 다른 사용자가이 시스템을 관리 하는 경우에 특히 toouse 합니다.  

경고를 hello 차트 tooset에서 추적할 수 있는 hello 메트릭을 모두 사용할 수 있습니다. 설정 여기 works hello와 다른 위치에서 동일한 앱 서비스에서 경고 합니다. 어느 hello에서 경고를 설정할 수 **경고** 일부 또는 모든 메트릭을 선택 하 고 UI를 드릴링 하에서 UI **추가 경고**합니다.

![메트릭 UI][3]

지금까지 설명한 hello 메트릭을 hello 앱 서비스 환경 메트릭입니다. Hello 앱 서비스 계획 수준에서 사용할 수 있는 메트릭을 있습니다. CPU 및 메모리의 모니터링이 합리적입니다.

ASE에 앱 서비스 계획 hello 모두 앱 서비스 계획을 전용된입니다. 즉, hello hello 할당 된 호스트 toothat 앱 서비스 계획에서 실행 되는 유일한 앱은 해당 앱 서비스 계획의 hello 앱. 앱 서비스 계획에 대 한 toosee 내용은 hello ASE UI 또는에서 hello 목록에서 앱 서비스 계획 (를) 실행 **찾아보기 앱 서비스 계획** (나열 된 모든 대상).   

### <a name="settings"></a>설정
Hello ASE 블레이드 내에서 한 **설정을** 몇 가지 중요 한 기능이 포함 된 섹션:

**설정** > **속성**: hello **설정을** 블레이드 ASE 블레이드를 표시 하는 경우 자동으로 열립니다. Top은 hello에 **속성**합니다. 여기에서 중복 toowhat에 표시 된 항목의 여러 가지 **Essentials**, 이란 매우 유용 하지만 **가상 IP 주소**,으로 **아웃 바운드 IP 주소**합니다.

![설정 블레이드 및 속성][4]

**설정** > **IP 주소**: ASE에서 IP SSL(Secure Sockets Layer) 앱을 만들 때 IP SSL 주소가 필요합니다. 하나 순서 tooobtain에서 프로그램 ASE 할당 될 수 있는 소유 하는 IP SSL 주소를 필요로 합니다. 이를 위해, ASE를 만들 때 1개의 IP SSL 주소가 있지만 더 추가할 수 있습니다. 요금이 청구 됩니다 추가 IP SSL 주소에 대 한 에서처럼 [앱 서비스 가격 책정] [ AppServicePricing] (hello 섹션의 SSL 연결에). hello 추가 가격은 hello IP SSL 가격입니다.

**설정** > **프런트 엔드 풀** / **작업자 풀**: 해당 리소스 풀에 대해서만 hello 기능 toosee 정보를 제공 하는 각 이러한 리소스 풀 블레이드 또한 tooproviding 크기를 조정 toofully 해당 리소스 풀.  

각 리소스 풀에 대 한 기본 블레이드 hello 해당 리소스 풀에 대 한 메트릭이 있는 차트를 제공합니다. 마찬가지로 hello ASE 블레이드에서 hello 차트와 hello 차트로 돌아가서 필요에 따라 경고를 설정 합니다. Hello ASE 블레이드에서 특정 리소스 풀에 대 한 경고를 설정 하는 hello 리소스 풀에서 작업와 같은 작업을 hello지 않습니다. Hello 작업자 풀에서 **설정을** 블레이드에서 앱 액세스 tooall hello 또는이 작업자 풀에서 실행 되는 앱 서비스 계획 합니다.

![작업자 풀 설정 UI][5]

### <a name="portal-scale-capabilities"></a>포털 확장 기능
세 가지 규모 작업이 있습니다.

* IP SSL 사용에 사용할 수 있는 IP 주소 hello ASE hello 번호를 변경 합니다.
* 리소스 풀에 사용 되는 hello 계산 리소스의 hello 크기를 변경 합니다.
* 수동으로 또는 자동 크기 조정을 통해 리소스 풀에 사용 되는 계산 리소스의 hello 번호를 변경 합니다.

Hello 포털에는 세 가지 방법으로 toocontrol 리소스 풀에 있는 서버 수

* Hello 위쪽 hello 주 ASE 블레이드에서 배율 작업 합니다. 여러 확장을 만들 수 있습니다 toohello 프런트 엔드 및 작업자 풀 구성을 변경 합니다. 이 변경 내용은 단일 작업으로 모두 적용됩니다.
* Hello 개별 리소스 풀에서 수동 크기 조정 작업이 **배율** 아래 있는 블레이드 **설정을**합니다.
* 자동 크기 조정, hello 개별 리소스 풀에서 설정한 **배율** 블레이드입니다.

hello ASE 블레이드에서 toouse hello 배율 작업을 저장에 hello 슬라이더 toohello quantity를 끌어 옵니다. 또한이 UI 변경 hello 크기를 지원합니다.  

![크기 조정 UI][6]

특정 리소스 풀의 toouse hello 수동 또는 자동 크기 조정 기능 이동 너무**설정** > **프런트 엔드 풀** / **작업자 풀** 으로 적절 한 합니다. 다음 열 hello 풀 toochange 되도록 합니다. 너무 이동**설정** > **스케일 아웃** 또는 **설정** > **크기 확장**합니다. hello **스케일 아웃** 블레이드 toocontrol 인스턴스 수량을 수 있습니다. **크기 확장** toocontrol 리소스 크기를 사용 하면 됩니다.  

![크기 조정 설정 UI][7]

## <a name="fault-tolerance-considerations"></a>내결함성 고려 사항
앱 서비스 환경 toouse too55 총 계산 리소스를 구성할 수 있습니다. 이러한 55 계산 리소스의 50만 사용 되는 toohost 워크 로드 될 수 있습니다. hello 이유는 다음과 같이 두 가지입니다. 최소 2개의 프런트 엔드 계산 리소스가 있습니다.  Too53 toosupport hello 작업자 풀 할당을 남았습니다. 순서 tooprovide 내결함성 toohave toohello 규칙에 따라 할당 되는 추가 계산 리소스를 필요 합니다.

* 각 작업자 풀 사용 가능한 toobe 작업 할당 되지 않은 추가 계산 리소스를 하나 이상 필요 합니다.
* 작업자 풀의 계산 리소스의 hello 수량 특정 값이 되 면 다른 계산 리소스는 결함 허용을 위해 필요 합니다. Hello 프런트 엔드 풀의 hello 그렇지는 않습니다.

모든 단일 작업자 풀 내에서 지정 된 값 x 자원을 배정 tooa 작업자 풀에 hello 내결함성을 요구 사항:

* X 2에서 20 사이 있으면 hello 워크 로드에 사용할 수 있는 사용 가능한 계산 리소스 용량은 수준은 x-1입니다.
* X 21에서 40 사이 있으면 hello 워크 로드에 사용할 수 있는 사용 가능한 계산 리소스 용량은 X-2 합니다.
* X 41 사이의 53 이면 hello 워크 로드에 사용할 수 있는 사용 가능한 계산 리소스 용량은 X-3 합니다.

hello 최소 사용 공간에 2 프런트 엔드 서버와 2 명 작업 자가 있습니다.  위에 다음 문 hello, 몇 가지 예제 tooclarify가 같습니다.  

* 30 작업자 하나의 풀이 있는 경우 그 중 28 toohost 사용 되는 워크 로드 될 수 있습니다.
* 2 명 작업 자가 단일 풀에 있으면 1 toohost 사용 되는 작업을 수 있습니다.
* 20 작업자는 단일 풀에 있으면 19 toohost 사용 되는 워크 로드 될 수 있습니다.  
* 에 있는 경우 21 작업자는 단일 풀 하면 여전히 유일한 19 toohost 사용 되는 워크 로드 될 수 있습니다.  

hello 내결함성을 측면 중요 하지만 tookeep 특정 임계값 보다 높은 확장 하는 것에 때 주의 해야 합니다. 하려면 tooadd 20 개의 인스턴스로 이동 too22에서 이동 용량 더 이상 21 용량을 추가로 추가 하지 않습니다. hello 용량을 추가 하는 hello 다음 숫자 42 인 40, 위에 것도 마찬가지입니다.  

## <a name="deleting-an-app-service-environment"></a>앱 서비스 환경 삭제
앱 서비스 환경 toodelete 원하는 hello 사용 하면 **삭제** hello hello 앱 서비스 환경 블레이드 위쪽에는 작업입니다. 이렇게 하면 실제로 되도록 toodo이 앱 서비스 환경 tooconfirm 프로그램의 증명된 tooenter hello 이름이 됩니다. 앱 서비스 환경 삭제 하면 삭제 하면 모든 hello 내용에도 note 합니다.  

![앱 서비스 환경 삭제 UI][9]  

## <a name="getting-started"></a>시작
앱 서비스 환경 시작 tooget 참조 [어떻게 toocreate 앱 서비스 환경](app-service-web-how-to-create-an-app-service-environment.md)합니다.

Azure 앱 서비스 플랫폼 hello에 대 한 자세한 내용은 참조 [Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md)합니다.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-web-configure-an-app-service-environment/ase-icon.png
[2]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-aseblade.png
[3]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolchart.png
[4]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-properties.png
[5]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolblade.png
[6]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-scalecommand.png
[7]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolscale.png
[8]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-pricingtiers.png
[9]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-deletease.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoScale]: http://azure.microsoft.com/documentation/articles/app-service-web-scale-a-web-app-in-an-app-service-environment/
[ControlInbound]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ExpressRoute]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[ILBASE]: http://azure.microsoft.com/documentation/articles/app-service-environment-with-internal-load-balancer/
