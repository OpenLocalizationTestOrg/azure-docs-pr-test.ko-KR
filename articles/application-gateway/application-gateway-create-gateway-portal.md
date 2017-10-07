---
title: "aaaCreate 응용 프로그램 게이트웨이-Azure 포털 | Microsoft Docs"
description: "사용 하 여 응용 프로그램 게이트웨이 toocreate 포털 hello 하는 방법에 대해 알아봅니다"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 54dffe95-d802-4f86-9e2e-293f49bd1e06
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 24c1d5701eae372cd233162ceb58dea36a3b6a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-hello-portal"></a>Hello 포털과 응용 프로그램 게이트웨이 만들기

[Application Gateway](application-gateway-introduction.md)는 ADC(응용 프로그램 배달 컨트롤러)를 서비스로 제공하여 다양한 7계층 부하 분산 기능을 제공하는 전용 가상 어플라이언스입니다. 이 문서에서는 하 hello 단계 toocreate 응용 프로그램 게이트웨이 hello Azure 포털을 사용 하 고 백 엔드 멤버인 기존 서버를 추가 합니다.

## <a name="log-in-tooazure"></a>TooAzure 로그인

Toohello Azure 포털에 로그인 [http://portal.azure.com](http://portal.azure.com)

## <a name="create-application-gateway"></a>응용 프로그램 게이트웨이 만들기

toocreate 응용 프로그램 게이트웨이 단계를 완료 하는 hello 합니다. Application Gateway에는 자체 서브넷이 필요합니다. 가상 네트워크를 만들 때 상태로 두고 충분 한 주소 공간 toohave 여러 서브넷을 확인 합니다. Hello 응용 프로그램 게이트웨이 배포 tooa 서브넷 되 면 다른 응용 프로그램 게이트웨이 tooit은 추가할 수 있습니다.

1. Hello 포털의 hello 즐겨찾기 창에서 클릭 **새로 만들기**
1. Hello에 **새로** 블레이드에서 클릭 **네트워킹**합니다. Hello에 **네트워킹** 블레이드에서 클릭 **응용 프로그램 게이트웨이**hello 다음 이미지에에서 나타난 것 처럼:

    ![Application Gateway 만들기][1]

1. Hello에 **기본 사항** 나타나는 블레이드 hello 다음 값을 입력 한 다음 클릭 **확인**:

   | **설정** | **값** | **세부 정보**|
   |---|---|---|
   |**Name**|AdatumAppGateway|hello 응용 프로그램 게이트웨이의 hello 이름|
   |**계층**|Standard|사용 가능한 값은 표준 또는 WAF입니다. 방문 [웹 응용 프로그램 방화벽](application-gateway-web-application-firewall-overview.md) toolearn WAF에 대 한 자세한 합니다.|
   |**SKU 크기**|중간|표준 계층을 선택할 때 제공되는 옵션으로 소형, 중형 및 대형이 있습니다. WAF 계층을 선택할 때 옵션은 중간 및 대형 뿐입니다.|
   |**인스턴스 수**|2|고가용성에 대 한 응용 프로그램 게이트웨이 hello의 인스턴스 수입니다. 인스턴스 수 1은 테스트 목적으로만 사용해야 합니다.|
   |**구독**|[구독 이름]|구독 toocreate hello 응용 프로그램 게이트웨이 선택 합니다.|
   |**리소스 그룹**|**새로 만들기:** AdatumAppGatewayRG|리소스 그룹을 만듭니다. hello 리소스 그룹 이름은 선택한 hello 구독 내에서 고유 해야 합니다. 리소스 그룹을 읽기 hello에 대 한 자세한 toolearn [리소스 관리자](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) 개요 문서.|
   |**위치**:|미국 서부||

1. Hello에 **설정** 아래에 나타나는 블레이드 **가상 네트워크**, 클릭 **가상 네트워크를 선택**합니다. hello **가상 네트워크 선택** 블레이드를 엽니다.  클릭 **새로 만들기** tooopen hello **가상 네트워크 만들기** 블레이드입니다.

   ![가상 네트워크 선택][2]

1. Hello에 **만들기 가상 네트워크 블레이드** hello 다음 값을 입력 한 다음 클릭 **확인**합니다. hello **가상 네트워크 만들기** 및 **가상 네트워크 선택** 블레이드를 닫습니다. 이 단계는 hello를 채웁니다 **서브넷** 필드 hello에 **설정** 블레이드 hello 서브넷을 선택 합니다.

   | **설정** | **값** | **세부 정보**|
   |---|---|---|
   |**Name**|AdatumAppGatewayVNET|Hello 응용 프로그램 게이트웨이의 이름|
   |**주소 공간**|10.0.0.0/16|이 hello hello 가상 네트워크 주소 공간|
   |**서브넷 이름**|AppGatewaySubnet|응용 프로그램 게이트웨이 hello에 대 한 hello 서브넷의 이름|
   |**서브넷 주소 범위**|10.0.0.0/28|이 서브넷이 백 엔드 풀 멤버에 대 한 hello 가상 네트워크의 서브넷을 더 추가 허용|

1. Hello에 **설정** 아래 블레이드 **프런트 엔드 IP 구성**, 선택 **공용** hello로 **IP 주소 유형**

1. Hello에 **설정** 아래 블레이드 **공용 IP 주소** 클릭 **공용 IP 주소 선택**, hello **공용 IP 주소 선택** 블레이드를 엽니다 를 클릭 하 여 **새로 만들기**합니다.

   ![공용 IP 선택][3]

1. Hello에 **공용 IP 주소 만들기** 블레이드에서 hello 기본값을 허용 하 고 클릭 **확인**합니다. hello 블레이드를 닫고 hello 채웁니다 **공용 IP 주소** hello 공용 IP 주소로 선택 합니다.

1. Hello에 **설정** 아래 블레이드 **수신기 구성**, 클릭 **HTTP** 아래 **프로토콜**합니다. Hello에 hello 포트 toouse 입력 **포트** 필드입니다.

2. 클릭 **확인** hello에 **설정을** 블레이드 toocontinue 합니다.

1. Hello에서 hello 설정을 검토 **요약** 블레이드에 대 한 클릭 **확인** hello 응용 프로그램 게이트웨이 toostart 생성 합니다. 응용 프로그램 게이트웨이 장기 실행 작업을 만들고 시간 toocomplete를 사용 합니다.

## <a name="add-servers-toobackend-pools"></a>서버 toobackend 풀 추가

Hello 응용 프로그램 게이트웨이 만든 후 hello 응용 프로그램 toobe 부하 분산을 호스트 하는 hello 시스템 toobe toohello 추가 된 응용 프로그램 게이트웨이 여전히 필요 합니다. hello IP 주소, FQDN 또는 이러한 서버의 Nic toohello 백 엔드 주소 풀에 추가 됩니다.

### <a name="ip-address-or-fqdn"></a>IP 주소 또는 FQDN

1. Hello Azure 포털에서에서 만든 hello 응용 프로그램 게이트웨이와 **즐겨찾기** 창에서 클릭 **모든 리소스**합니다. Hello 클릭 **AdatumAppGateway** 에 응용 프로그램 게이트웨이 모든 리소스 블레이드를 hello 합니다. 이미 선택한 hello 구독에 여러 자원이 인 경우 입력 하면 **AdatumAppGateway** hello에 **이름별으로 필터링...** 상자 tooeasily 액세스 hello 응용 프로그램 게이트웨이 합니다.

1. 만든 hello 응용 프로그램 게이트웨이 표시 됩니다. 클릭 **백 엔드 풀**, hello 현재 백 엔드 풀을 선택 하 고 **appGatewayBackendPool**, hello **appGatewayBackendPool** 블레이드를 엽니다.

   ![Application Gateway 백 엔드 풀][4]

1. 클릭 **대상 추가** FQDN 값의 tooadd IP 주소입니다. 선택 **IP 주소 또는 FQDN** hello로 **형식** hello 필드에 IP 주소 또는 FQDN을 입력 합니다. 추가 백 엔드 풀 멤버에 대해 이 단계를 반복합니다. 완료하면 **저장**을 클릭합니다.

### <a name="virtual-machine-and-nic"></a>가상 컴퓨터 및 NIC

백 엔드 풀 구성원으로 가상 컴퓨터 NIC를 추가할 수도 있습니다. 응용 프로그램 게이트웨이 hello와 동일한 가상 네트워크를 통해 사용할 수 있는 hello 내에서 가상 컴퓨터만 hello 드롭다운입니다.

1. Hello Azure 포털에서에서 만든 hello 응용 프로그램 게이트웨이와 **즐겨찾기** 창에서 클릭 **모든 리소스**합니다. Hello 클릭 **AdatumAppGateway** 에 응용 프로그램 게이트웨이 모든 리소스 블레이드를 hello 합니다. 이미 선택한 hello 구독에 여러 자원이 인 경우 입력 하면 **AdatumAppGateway** hello에 **이름별으로 필터링...** 상자 tooeasily 액세스 hello 응용 프로그램 게이트웨이 합니다.

1. 만든 hello 응용 프로그램 게이트웨이 표시 됩니다. 클릭 **백 엔드 풀**, hello 현재 백 엔드 풀을 선택 하 고 **appGatewayBackendPool**, hello **appGatewayBackendPool** 블레이드를 엽니다.

   ![Application Gateway 백 엔드 풀][5]

1. 클릭 **대상 추가** FQDN 값의 tooadd IP 주소입니다. 선택 **가상 컴퓨터** hello로 **형식** hello 가상 컴퓨터 및 NIC toouse 선택 합니다. 완료하면 **저장**을 클릭합니다.

   > [!NOTE]
   > 가상 컴퓨터에만 응용 프로그램 게이트웨이 hello hello 드롭다운 상자에서에서 사용할 수 있는 동일한 가상 네트워크를 hello 합니다.

## <a name="clean-up-resources"></a>리소스 정리

더 이상 필요 hello 리소스 그룹, 응용 프로그램 게이트웨이 및 모든 관련된 리소스를 삭제 합니다. 따라서 toodo hello 응용 프로그램 게이트웨이 블레이드를 클릭 hello 리소스 그룹을 선택 **삭제**합니다.

## <a name="next-steps"></a>다음 단계

이 시나리오에서는 응용 프로그램 게이트웨이 배포 및 서버 toohello 백 엔드를 추가 합니다. hello 다음 단계는 tooconfigure hello 응용 프로그램 게이트웨이 설정 수정 및 hello 게이트웨이의 조정 규칙입니다. 다음 문서는 hello를 방문 하 여 다음이 단계를 찾을 수 있습니다.

사용자 지정 상태 toocreate 방문 하 여 조사 하는 방법에 대해 알아봅니다 [만들 사용자 지정 상태 프로브](application-gateway-create-probe-portal.md)

어떻게 tooconfigure SSL 오프 로딩 및 take hello 비용이 많이 드는 SSL 암호 해독 해제 하면 웹 서버 방문 하 여 자세한 [SSL 오프 로드 구성](application-gateway-ssl-portal.md)

자세한 내용은 방법 tooprotect 응용 프로그램을 [웹 응용 프로그램 방화벽](application-gateway-webapplicationfirewall-overview.md) 응용 프로그램 게이트웨이의 기능입니다.

<!--Image references-->
[1]: ./media/application-gateway-create-gateway-portal/figure1.png
[2]: ./media/application-gateway-create-gateway-portal/figure2.png
[3]: ./media/application-gateway-create-gateway-portal/figure3.png
[4]: ./media/application-gateway-create-gateway-portal/figure4.png
[5]: ./media/application-gateway-create-gateway-portal/figure5.png
[scenario]: ./media/application-gateway-create-gateway-portal/scenario.png
