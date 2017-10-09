---
title: "aaaCreate 웹 응용 프로그램 방화벽으로 Azure 응용 프로그램 게이트웨이 업데이트 하거나 | Microsoft Docs"
description: "웹 응용 프로그램 방화벽을 사용 하 여 응용 프로그램 게이트웨이 toocreate 포털 hello 하는 방법에 대해 알아봅니다"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b561a210-ed99-4ab4-be06-b49215e3255a
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: 68d140fef14499da654ea251d1208e6a800f55a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-web-application-firewall-by-using-hello-portal"></a>Hello 포털을 사용 하 여 웹 응용 프로그램 방화벽 응용 프로그램 게이트웨이 만들기

> [!div class="op_single_selector"]
> * [Azure 포털](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Azure CLI](application-gateway-web-application-firewall-cli.md)

웹 응용 프로그램 방화벽 toocreate 응용 프로그램 게이트웨이 사용 하는 방법에 대해 알아봅니다.

hello 웹 응용 프로그램 방화벽 (WAF)에서 Azure 응용 프로그램 게이트웨이 SQL 삽입 같은 일반적인 웹 기반 공격, 사이트 간 스크립팅 공격이 및 도용 하는 세션에서 웹 응용 프로그램을 보호합니다. 웹 응용 프로그램 다양 한 hello OWASP 상위 10 개의 일반적인 웹 취약점 으로부터 보호합니다.

## <a name="scenarios"></a>시나리오

이 문서에는 두 가지 시나리오가 있습니다.

Hello 첫 번째 시나리오에 알아봅니다 너무[웹 응용 프로그램 방화벽 응용 프로그램 게이트웨이 만들기](#create-an-application-gateway-with-web-application-firewall)

Hello 두 번째 시나리오에 알아봅니다 너무[추가 웹 응용 프로그램 방화벽 tooan 기존 응용 프로그램 게이트웨이](#add-web-application-firewall-to-an-existing-application-gateway)합니다.

![예제 시나리오][scenario]

> [!NOTE]
> 사용자 지정 상태를 포함 하 여 hello 응용 프로그램 게이트웨이 추가 구성 프로브를 통해 백 엔드 풀 주소 및 추가 규칙 hello 응용 프로그램 게이트웨이 구성한 후와 초기 배포 중이 아니라 구성 됩니다.

## <a name="before-you-begin"></a>시작하기 전에

Azure Application Gateway에는 자체 서브넷이 필요합니다. 가상 네트워크를 만들 때 상태로 두고 충분 한 주소 공간 toohave 여러 서브넷을 확인 합니다. 추가 응용 프로그램 게이트웨이 수 toobe 추가 응용 프로그램 게이트웨이 tooa 서브넷을 배포한 후 toohello 서브넷입니다.

##<a name="add-web-application-firewall-to-an-existing-application-gateway"></a>웹 응용 프로그램 방화벽 tooan 기존 응용 프로그램 게이트웨이 추가 합니다.

이 예에서는 기존 응용 프로그램 게이트웨이 toosupport 웹 응용 프로그램 방화벽 방지 모드에서를 업데이트합니다.

1. Hello Azure 포털에서에서 **즐겨찾기** 창에서 클릭 **모든 리소스**합니다. 클릭 하 여 hello hello에서 기존 응용 프로그램 게이트웨이 **모든 리소스** 블레이드입니다. 이미 선택한 hello 구독에 여러 자원이 인 경우 hello에 hello 이름을 입력할 수 있습니다 **이름별으로 필터링...** 상자 tooeasily 액세스 hello DNS 영역입니다.

   ![Application Gateway 만들기][1]

1. 클릭 **웹 응용 프로그램 방화벽** hello 응용 프로그램 게이트웨이 설정을 업데이트 합니다. 완료되면 **저장**

    hello 설정을 tooupdate 기존 응용 프로그램 게이트웨이 toosupport 웹 응용 프로그램 방화벽은:

   | **설정** | **값** | **세부 정보**
   |---|---|---|
   |**TooWAF 계층 업그레이드**| 선택 | Hello 응용 프로그램 게이트웨이 toohello WAF 계층의 hello 계층을 설정합니다.|
   |**방화벽 상태**| 사용 | 이 설정은 WAF hello에서 hello 방화벽을 사용 합니다.|
   |**방화벽 모드** | 방지 | 웹 응용 프로그램 방화벽이 악의적인 트래픽을 처리하는 방식에 대한 설정입니다. **검색** 모드 hello 이벤트 기록 여기서 **방지** 모드 hello 이벤트를 기록 하 고 중지 hello 악의적인 트래픽을 합니다.|
   |**규칙 집합**|3.0|이 설정은 결정 hello [규칙 집합 핵심](application-gateway-web-application-firewall-overview.md#core-rule-sets) 즉 사용 되는 tooprotect hello 백 엔드 풀 멤버입니다.|
   |**사용하지 않는 규칙 구성**|다름|tooprevent 가능한 가양성이이 설정을 통해 toodisable 특정 [규칙 및 규칙 그룹](application-gateway-crs-rulegroups-rules.md)합니다.|

    >[!NOTE]
    > 기존 응용 프로그램 게이트웨이 toohello WAF SKU로 업그레이드할 때 hello SKU 크기를 변경 너무**보통**합니다. 구성이 완료된 후 이 크기를 다시 구성할 수 있습니다.

    ![기본 설정이 표시된 블레이드][2-1]

    > [!NOTE]
    > tooview 웹 응용 프로그램 방화벽 로그, 진단 설정 해야 하 고 ApplicationGatewayFirewallLog 선택 합니다. 테스트 목적으로 인스턴스 수 1을 선택할 수 있습니다. 고 것이 중요에 모든 인스턴스 수의 두 인스턴스가 tooknow hello SLA에서 다루지 않는 권장 되지 않습니다. 웹 응용 프로그램 방화벽을 사용하는 경우 소형 게이트웨이를 사용할 수 없습니다.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>웹 응용 프로그램 방화벽을 사용하여 Application Gateway를 만드는 방법

이 시나리오에서는 다음을 수행합니다.

* 두 인스턴스를 사용하여 중형 웹 응용 프로그램 방화벽 Application Gateway를 만듭니다.
* 예약된 CIDR 블록이 10.0.0.0/16이고 이름이 AdatumAppGatewayVNET인 가상 네트워크를 만듭니다.
* CIDR 블록으로 10.0.0.0/28을 사용하는 Appgatewaysubnet이라고 하는 서브넷을 만듭니다.
* SSL 오프로드용 인증서를 구성합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다. 아직 계정이 없는 경우 [1개월 평가판](https://azure.microsoft.com/free)을 등록할 수 있습니다.
1. Hello 포털의 hello 즐겨찾기 창에서 클릭 **새로 만들기**
1. Hello에 **새로** 블레이드에서 클릭 **네트워킹**합니다. Hello에 **네트워킹** 블레이드에서 클릭 **응용 프로그램 게이트웨이**hello 다음 이미지에에서 나타난 것 처럼:
1. Azure 포털 toohello 탐색, 클릭 **새로** > **네트워킹** > **응용 프로그램 게이트웨이**

    ![Application Gateway 만들기][1]

1. Hello에 **기본 사항** 나타나는 블레이드 hello 다음 값을 입력 한 다음 클릭 **확인**:

   | **설정** | **값** | **세부 정보**
   |---|---|---|
   |**Name**|AdatumAppGateway|hello 응용 프로그램 게이트웨이의 hello 이름|
   |**계층**|WAF|사용 가능한 값은 표준 또는 WAF입니다. 방문 [웹 응용 프로그램 방화벽](application-gateway-web-application-firewall-overview.md) toolearn WAF에 대 한 자세한 합니다.|
   |**SKU 크기**|중간|표준 계층을 선택할 때 제공되는 옵션으로 소형, 중형 및 대형이 있습니다. WAF 계층을 선택할 때 옵션은 중간 및 대형 뿐입니다.|
   |**인스턴스 수**|2|고가용성에 대 한 응용 프로그램 게이트웨이 hello의 인스턴스 수입니다. 인스턴스 수 1은 테스트 목적으로만 사용해야 합니다.|
   |**구독**|[구독 이름]|구독 toocreate hello 응용 프로그램 게이트웨이 선택 합니다.|
   |**리소스 그룹**|**새로 만들기:** AdatumAppGatewayRG|리소스 그룹을 만듭니다. hello 리소스 그룹 이름은 선택한 hello 구독 내에서 고유 해야 합니다. 리소스 그룹을 읽기 hello에 대 한 자세한 toolearn [리소스 관리자](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) 개요 문서.|
   |**위치**:|미국 서부||

   ![기본 설정이 표시된 블레이드][2-2]

1. Hello에 **설정** 아래에 나타나는 블레이드 **가상 네트워크**, 클릭 **가상 네트워크를 선택**합니다. 이 단계 열립니다 입력 hello **가상 네트워크 선택** 블레이드입니다.  클릭 **새로 만들기** tooopen hello **가상 네트워크 만들기** 블레이드입니다.

   ![가상 네트워크 선택][2]

1. Hello에 **만들기 가상 네트워크 블레이드** hello 다음 값을 입력 한 다음 클릭 **확인**합니다. 이 단계는 hello 닫습니다 **가상 네트워크 만들기** 및 **가상 네트워크 선택** 블레이드입니다. 이렇게 hello 채워집니다 **서브넷** 필드 hello에 **설정** 블레이드 hello 서브넷을 선택 합니다.

   |**설정** | **값** | **세부 정보** |
   |---|---|---|
   |**Name**|AdatumAppGatewayVNET|Hello 응용 프로그램 게이트웨이의 이름|
   |**주소 공간**|10.0.0.0/16| 이 값은 hello hello 가상 네트워크 주소 공간|
   |**서브넷 이름**|AppGatewaySubnet|응용 프로그램 게이트웨이 hello에 대 한 hello 서브넷의 이름|
   |**서브넷 주소 범위**|10.0.0.0/28 | 이 서브넷이 백 엔드 풀 멤버에 대 한 hello 가상 네트워크의 서브넷을 더 추가 허용|

1. Hello에 **설정** 아래 블레이드 **프런트 엔드 IP 구성**, 선택 **공용** hello로 **IP 주소 유형**

1. Hello에 **설정** 아래 블레이드 **공용 IP 주소**, 클릭 **공용 IP 주소를 선택**,이 단계는 hello 엽니다 **공용IP주소선택**블레이드에서 클릭 **새로 만들기**합니다.

   ![공용 IP 선택][3]

1. Hello에 **공용 IP 주소 만들기** 블레이드에서 hello 기본값을 허용 하 고 클릭 **확인**합니다. 이 단계는 hello 닫습니다 **공용 IP 주소 선택** 블레이드, hello **공용 IP 주소 만들기** 블레이드에서 채웁니다 **공용 IP 주소** 선택 hello 공용 IP 주소와 합니다.

1. Hello에 **설정** 아래 블레이드 **수신기 구성**, 클릭 **HTTP** 아래 **프로토콜**합니다. toouse **https**는 인증서가 필요 합니다. hello 인증서의 개인 키 hello hello 인증서의.pfx 내보내기 toobe 제공 하며 hello 파일에 대 한 암호를 hello 하므로 필요 합니다.

1. Hello 구성 **WAF** 특정 설정 합니다.

   |**설정** | **값** | **세부 정보** |
   |---|---|---|
   |**방화벽 상태**| 사용| 이 설정은 WAF를 켜고 끕니다.|
   |**방화벽 모드** | 방지| 이 설정은 WAF 악의적인 트래픽을 수행 하는 hello 작업을 결정 합니다. **검색** 을 선택하면 트래픽이 기록되기만 합니다.  **방지**를 선택하면 트래픽이 기록되고 403 권한 없음 응답에 따라 중지됩니다.|


1. Hello 요약 페이지를 검토 하 고 클릭 **확인**합니다.  이제 hello 응용 프로그램 게이트웨이 대기 되 고 생성 합니다.

1. Hello 응용 프로그램 게이트웨이 만든 후 tooit hello 응용 프로그램 게이트웨이의 hello 포털 toocontinue 구성에서 이동 합니다.

    ![Application Gateway 리소스 보기][10]

다음이 단계는 hello 수신기, 백 엔드 풀, 백 엔드 http 설정 및 규칙에 대 한 기본 설정으로 기본 응용 프로그램 게이트웨이 만듭니다. 수정할 수 있습니다 이러한 설정을 toosuit 배포 hello를 프로 비전 하는 것은 성공 후

> [!NOTE]
> Hello 기본 웹 응용 프로그램 방화벽 구성을 사용 하 여 만든 응용 프로그램 게이트웨이 보호 기능에 대 한 CRS 3.0으로 구성 됩니다.

## <a name="next-steps"></a>다음 단계

다음에 대해 알아볼 수 있습니다 어떻게 tooconfigure hello에 대 한 사용자 지정 도메인 별칭 [공용 IP 주소](../dns/dns-custom-domain.md#public-ip-address) Azure DNS 또는 다른 DNS 공급자를 사용 하 여 합니다.

자세한 내용은 방법 tooconfigure 진단 로깅 toolog hello 되거나 되는 이벤트 검색 방문 하 여 웹 응용 프로그램 방화벽을 모두 방지할 [응용 프로그램 게이트웨이 진단](application-gateway-diagnostics.md)

사용자 지정 상태 toocreate 방문 하 여 조사 하는 방법에 대해 알아봅니다 [만들 사용자 지정 상태 프로브](application-gateway-create-probe-portal.md)

어떻게 tooconfigure SSL 오프 로딩 및 take hello 비용이 많이 드는 SSL 암호 해독 해제 하면 웹 서버 방문 하 여 자세한 [SSL 오프 로드 구성](application-gateway-ssl-portal.md)

<!--Image references-->
[1]: ./media/application-gateway-web-application-firewall-portal/figure1.png
[2]: ./media/application-gateway-web-application-firewall-portal/figure2.png
[2-1]: ./media/application-gateway-web-application-firewall-portal/figure2-1.png
[2-2]: ./media/application-gateway-web-application-firewall-portal/figure2-2.png
[3]: ./media/application-gateway-web-application-firewall-portal/figure3.png
[10]: ./media/application-gateway-web-application-firewall-portal/figure10.png
[scenario]: ./media/application-gateway-web-application-firewall-portal/scenario.png
