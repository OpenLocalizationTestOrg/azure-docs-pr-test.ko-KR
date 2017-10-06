---
title: "온-프레미스 네트워크 tooan Azure 가상 네트워크 연결: 사이트 간 VPN: 포털 | Microsoft Docs"
description: "온-프레미스에서 IPsec 연결을 통해 Azure 가상 네트워크 tooan 네트워크 단계 toocreate hello 공용 인터넷 합니다. 다음이 단계를 사용 하면 hello 포털을 사용 하는 크로스-프레미스 사이트 간 VPN 게이트웨이 연결을 만들 수 있습니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 827a4db7-7fa5-4eaf-b7e1-e1518c51c815
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 6f0acbaf1bf016026cefade048a116e94686103d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-in-hello-azure-portal"></a>Hello Azure 포털에서에서 사이트 간 연결을 만들려면

이 문서에서는 어떻게 toouse hello Azure 포털 toocreate 온-프레미스 네트워크 toohello VNet에서에서 사이트 간 VPN 게이트웨이 연결 합니다. 이 문서의 단계 hello toohello 리소스 관리자 배포 모델을 적용합니다. 또한 서로 다른 배포 도구 또는 배포 모델을 사용 하 여 hello 다음 목록에서에서 다른 옵션을 선택 하 여이 구성을 만들 수 있습니다.

> [!div class="op_single_selector"]
> * [Azure 포털](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Azure Portal(클래식)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

사이트 간 VPN 게이트웨이 연결에 사용 되는 tooconnect는 온-프레미스 IPsec/IKE (IKEv1 또는 IKEv2) VPN 터널을 통해 Azure 가상 네트워크 tooan 네트워크입니다. 이러한 종류의 연결에는 VPN 장치에 있는 온-프레미스 외부와 접한 공용 IP 주소 할당 tooit가 필요 합니다. VPN Gateway에 대한 자세한 내용은 [VPN Gateway 정보](vpn-gateway-about-vpngateways.md)를 참조하세요.

![사이트 간 VPN Gateway 크로스-프레미스 연결 다이어그램](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a>시작하기 전에

Hello 조건을 구성을 시작 하기 전에 다음을 충족 하는지 확인 합니다.

* 호환 되는 VPN 장치 및 수 tooconfigure 장애가 있는 사용자를 완료 했는지 확인 것입니다. 호환되는 VPN 장치 및 장치 구성에 대한 자세한 내용은 [VPN 장치 정보](vpn-gateway-about-vpn-devices.md)를 참조하세요.
* VPN 장치에 대한 외부 연결 공용 IPv4 주소가 있는지 확인합니다. 이 IP 주소는 NAT 뒤에 배치할 수 없습니다.
* 온-프레미스 네트워크 구성을 잘 모르는 hello IP 주소 범위에 있는 경우 해당 세부 정보를 제공할 수 있는 사용자와 toocoordinate를 해야 합니다. 이 구성을 만들 때 Azure tooyour 온-프레미스 위치를 라우팅하는 hello IP 주소 범위 접두사를 지정 해야 합니다. 온-프레미스 네트워크의 hello 서브넷 중 랩 tooconnect를 원하는 hello 가상 네트워크 서브넷을 통해 할 수 있습니다. 

### <a name="values"></a>예제 값

이 문서의 hello 예제는 다음 값에는 hello를 사용 합니다. 이러한 값 toocreate 테스트 환경을 사용 하거나 toothem 참조 toobetter hello이이 문서의 예제에서는 이해 합니다.

* **VNet 이름:** TestVNet1
* **주소 공간:** 
  * 10.11.0.0/16
  * 10.12.0.0/16(이 연습의 선택 사항)
* **서브넷:**
  * 프런트 엔드: 10.11.0.0/24
  * 백 엔드: 10.12.0.0/24(이 연습의 선택 사항)
* **게이트웨이 서브넷:** 10.11.255.0/27
* **리소스 그룹:** TestRG1
* **위치:** 미국 동부
* **DNS 서버:** 선택 사항입니다. hello DNS 서버의 IP 주소입니다.
* **Virtual Network 게이트웨이 이름:** VNet1GW
* **공용 IP:** VNet1GWIP
* **VPN 유형:** 경로 기반
* **연결 형식:** 사이트 간(IPsec)
* **게이트웨이 유형:** VPN
* **로컬 네트워크 게이트웨이 이름:** Site2
* **연결 이름:** VNet1toSite2

## <a name="CreatVNet"></a>1. 가상 네트워크 만들기

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <a name="dns"></a>2. DNS 서버 지정

DNS 필요한 toocreate 사이트-사이트 연결이 아닙니다. 그러나 tooyour 배포 된 가상 네트워크 리소스에 대 한 toohave 이름 확인 하려는 경우에 DNS 서버를 지정 해야 합니다. 이 설정을 사용 하면이 가상 네트워크에 대 한 이름 확인을 위해 toouse 되도록 hello DNS 서버를 지정할 수 있습니다. DNS 서버를 만들지 않습니다. 이름 확인에 대한 자세한 내용은 [VM에서 이름 확인 및 역할 인스턴스](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)를 참조하세요.

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>3. Hello 게이트웨이 서브넷 만들기

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <a name="VNetGateway"></a>4. Hello VPN 게이트웨이 만들기

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <a name="LocalNetworkGateway"></a>5. Hello 로컬 네트워크 게이트웨이 만들기

일반적으로 hello 로컬 네트워크 게이트웨이 tooyour 온-프레미스 위치를 나타냅니다. Hello 사이트 기준인 Azure 수 tooit를 참조 하십시오. 그런 다음 hello IP 주소를 지정 된 이름을 지정 hello 온-프레미스 VPN 장치 toowhich의 연결을 만듭니다. 또한 hello VPN 게이트웨이 toohello VPN 장치를 통해 라우팅되는 hello IP 주소 접두사를 지정 합니다. 지정 하는 hello 주소 접두사는 온-프레미스 네트워크에 있는 hello 접두사입니다. 온-프레미스 네트워크 변경 되거나 hello VPN 장치에 대 한 toochange hello 공용 IP 주소 필요, 나중에 hello 값을 업데이트할 쉽게 있습니다.

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <a name="VPNDevice"></a>6. VPN 장치 구성

사이트 간 연결 tooan 온-프레미스 네트워크는 VPN 장치가 필요 합니다. 이 단계에서는 VPN 장치를 구성합니다. VPN 장치를 구성할 때 hello 다음이 필요 합니다.

- 공유 키 - 동일한 공유 hello은이 사이트 간 VPN 연결을 만들 때 지정한 키입니다. 이 예제에서는 기본적인 공유 키를 사용합니다. 더 복잡 한 키 toouse를 생성 하는 것이 좋습니다.
- 가상 네트워크 게이트웨이의 공용 IP 주소 번호입니다. Hello Azure 포털, PowerShell 또는 CLI를 사용 하 여 hello 공용 IP 주소를 볼 수 있습니다. toofind hello hello Azure 포털을 사용 하 여 VPN 게이트웨이의 공용 IP 주소를 너무 탐색**가상 네트워크 게이트웨이**, 게이트웨이의 hello 이름을 클릭 합니다.

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>7. Hello VPN 연결 만들기

가상 네트워크 게이트웨이와 온-프레미스 VPN 장치 간의 hello 사이트 간 VPN 연결을 만듭니다.

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <a name="VerifyConnection"></a>8. Hello VPN 연결 확인

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="connectVM"></a>tooconnect tooa 가상 컴퓨터

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <a name="reset"></a>어떻게 tooreset VPN 게이트웨이

Azure VPN Gateway 재설정은 하나 이상의 사이트 간 VPN 터널에서 크로스-프레미스 VPN 연결이 손실되는 경우에 유용합니다. 이 경우 온-프레미스 VPN 장치는 모든 정상적으로 작동 하지만 수 없습니다. tooestablish IPsec 터널 hello Azure VPN 게이트웨이 사용 합니다. 자세한 단계는 [VPN 게이트웨이 다시 설정](vpn-gateway-resetgw-classic.md)을 참조하세요.

## <a name="resize"></a>어떻게 toochange 게이트웨이 SKU (게이트웨이 크기 조정)

Hello 게이트웨이 SKU toochange를 단계에 대 한 참조 [게이트웨이 Sku](vpn-gateway-about-vpn-gateway-settings.md#gwsku)합니다.

## <a name="next-steps"></a>다음 단계

* BGP에 대 한 정보를 참조 hello [BGP 개요](vpn-gateway-bgp-overview.md) 및 [어떻게 tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md)합니다.
* 강제 터널링에 대한 내용은 [강제 터널링 정보](vpn-gateway-forced-tunneling-rm.md)를 참조하세요.
* 항상 사용 가능한 활성/활성 연결에 대한 정보는 [항상 사용 가능한 크로스-프레미스 및 VNet 간 연결](vpn-gateway-highlyavailable.md)을 참조하세요.
