---
title: "VPN Gateway 구성: 클래식 포털: Azure | Microsoft Docs"
description: "이 문서에서는 가상 네트워크 VPN 게이트웨이 구성하고 게이트웨이 VPN 라우팅 형식을 변경하는 방법을 안내합니다. 이러한 단계는 toohello 클래식 배포 모델 및 hello 클래식 포털을 적용 합니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fbe59ba8-b11f-4d21-9bb1-225ec6c6d351
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/04/2017
ms.author: cherylmc
ms.openlocfilehash: 00d2fa18bab6eb24b33ddb18113f2a557db638d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vpn-gateway-in-hello-classic-portal"></a>Hello 클래식 포털에서 VPN 게이트웨이 구성 합니다. 
Toocreate Azure 및 온-프레미스 위치 간 보안 크로스-프레미스 연결을 원하는 경우 가상 네트워크 게이트웨이 toocreate를 해야 합니다. VPN Gateway는 특정 유형의 가상 네트워크 게이트웨이입니다. Hello 클래식 배포 모델에서 VPN 게이트웨이 중 하나일 수 있습니다 두 VPN 라우팅 유형: 정적 또는 동적입니다. hello VPN 유형을 선택 하면 네트워크 디자인 계획 및 toouse 원하는 hello 온-프레미스 VPN 장치 둘 다에 따라 달라 집니다. VPN 장치에 대한 자세한 내용은 [VPN 장치 정보](vpn-gateway-about-vpn-devices.md)를 참조하세요.

**Azure 배포 모델 정보**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-overview"></a>구성 개요
hello 다음 단계에 관한 hello 클래식 포털에서 VPN 게이트웨이 구성 합니다. 이러한 단계는 toogateways hello 클래식 배포 모델을 사용 하 여 만든 가상 네트워크에 적용 됩니다. 현재 gateway에 대 한 hello 구성 설정의 일부는 hello Azure 포털에서에서 사용할 수 있습니다. 이 새로운 Azure 포털 toohello 적용 되는 지침 집합이 만듭니다.

### <a name="before-you-begin"></a>시작하기 전에
게이트웨이 구성 하기 전에 먼저 toocreate 가상 네트워크가 됩니다. 단계 toocreate 크로스-프레미스 연결에 대 한 가상 네트워크에 대 한 참조 [가상 네트워크는 사이트 간 VPN 연결으로 구성](vpn-gateway-site-to-site-create.md), 또는 [는지점-사이트VPN연결으로가상네트워크구성](vpn-gateway-point-to-site-create.md). 다음 단계 tooconfigure hello VPN 게이트웨이 hello를 사용 하 여 이동한 tooconfigure VPN 장치를 해야 하는 hello 정보를 수집 합니다. 

VPN 게이트웨이 이미 있는 경우 toochange hello VPN 라우팅 유형을 참조 [어떻게 toochange hello VPN 게이트웨이 라우팅 유형을](#how-to-change-the-vpn-routing-type-for-your-gateway)합니다.

## <a name="create-a-vpn-gateway"></a>VPN 게이트웨이 만들기
1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com), hello에 **네트워크** 페이지에서 가상 네트워크에 대 한 해당 hello 상태 열을 확인 **Created**합니다.
2. Hello에 **이름** 열에서 가상 네트워크의 hello 이름을 클릭 합니다.
3. Hello에 **대시보드** 페이지에서는이 VNet에 게이트웨이가 아직 구성 되어 있지 않습니다. 이 상태 진행할 때 hello 단계 tooconfigure 게이트웨이가 표시 됩니다.

![게이트웨이가 만들어지지 않음](./media/vpn-gateway-configure-vpn-gateway-mp/IC717025.png)

다음으로 hello 페이지의 맨 아래 hello에 클릭 **게이트웨이 만들기**합니다. *고정 라우팅* 또는 *동적 라우팅*을 선택할 수 있습니다. hello VPN 라우팅 유형을 선택 하면 몇 가지 요인에 따라 달라 집니다. 예를 들어 VPN 장치에서 지 원하는 작업 및 toosupport 지점 및 사이트 연결 해야 하는지 여부입니다. 확인 [VPN 장치에 대 한 가상 네트워크 연결을 위한](vpn-gateway-about-vpn-devices.md) tooverify hello 해야 하는 VPN 라우팅 유형입니다. Hello 게이트웨이 만든 후에 VPN 게이트웨이 삭제 하 고 hello 게이트웨이 다시 만들지 않고 라우팅 유형을 변경할 수 없습니다. 때 hello 시스템 묻는 hello 게이트웨이 생성, 클릭 하 여 원하는 tooconfirm **예**합니다.

![게이트웨이 VPN 라우팅 유형](./media/vpn-gateway-configure-vpn-gateway-mp/IC717026.png)

게이트웨이 만들 때 확인 hello 페이지 hello 게이트웨이 그래픽이 tooyellow 바뀌고에 따르면 *게이트웨이 만들기*합니다. Hello 게이트웨이 toocreate too45 분이 걸릴 수도 있습니다. 다른 구성 설정을 진행 하려면 hello 게이트웨이가 완료 될 때까지 기다립니다.

![게이트웨이 만들기](./media/vpn-gateway-configure-vpn-gateway-mp/IC717027.png)

경우 게이트웨이 변경 내용을 너무 hello*연결*, VPN 장치에 필요한 hello 정보를 수집할 수 있습니다.

![게이트웨이 연결](./media/vpn-gateway-configure-vpn-gateway-mp/IC717028.png)

## <a name="site-to-site-connections"></a>사이트 간 연결

### <a name="step-1-gather-information-for-your-vpn-device-configuration"></a>1단계. VPN 장치 구성에 대한 정보 수집
Hello 게이트웨이 만든 후 사이트 간 연결을 만드는 경우에 VPN 장치 구성에 대 한 정보를 수집 합니다. 이 정보 hello에 위치한 **대시보드** 가상 네트워크에 대 한 페이지:

1. **게이트웨이 IP 주소-** hello에서 hello IP 주소를 확인할 수 있습니다 **대시보드** 페이지. 수 toosee 게이트웨이 지날 때까지 완료 만들 수 없습니다.
2. **공유 된 키-** 클릭 **키 관리** hello hello 화면 맨 아래에 있습니다. Hello 아이콘 다음 toohello 키 toocopy 클릭 것 tooyour 클립보드에 붙여 넣을 고 hello 키를 저장 합니다. 이 단추는 S2S VPN 터널이 하나인 경우에만 작동합니다. 여러 S2S VPN 터널을 사용 하는 경우 사용 하 여 hello *가상 네트워크 게이트웨이 공유 키 가져오기* API 또는 PowerShell cmdlet.

![키 관리](./media/vpn-gateway-configure-vpn-gateway-mp/IC717029.png)

### <a name="step-2--configure-your-vpn-device"></a>2단계.  VPN 장치 구성
사이트 간 연결 tooan 온-프레미스 네트워크는 VPN 장치가 필요 합니다. 모든 VPN 장치에 대 한 구성 단계를 제공 하지 않는 것, 유용한 링크를 따라 hello에 hello 정보를 볼 수 있습니다.

- 호환되는 VPN 장치에 대한 내용은 [VPN 장치](vpn-gateway-about-vpn-devices.md)를 참조하세요. 
- 링크 toodevice 구성 설정에 대 한 참조 [VPN 장치의 유효성을 검사할](vpn-gateway-about-vpn-devices.md#devicetable)합니다. 해당 링크가 가장 효율적으로 제공됩니다. 패턴은 항상 최상의 toocheck hello 최신 구성 정보에 대 한 장치 제조업체에 문의입니다.
- 장치 구성 샘플을 편집하는 방법에 대한 정보는 [샘플 편집](vpn-gateway-about-vpn-devices.md#editing)을 참조하세요.
- IPsec/IKE 매개 변수는 [매개 변수](vpn-gateway-about-vpn-devices.md#ipsec)를 참조하세요.
- VPN 장치를 구성 하기 전에 확인 [알려진 장치 호환성 문제](vpn-gateway-about-vpn-devices.md#known) toouse 원하는 hello VPN 장치에 대 한 합니다.

VPN 장치를 구성할 때 다음 항목 hello이 필요 합니다.

- 가상 네트워크 게이트웨이의 공용 IP 주소 번호입니다. Toohello 이동 하 여이 찾을 수 있습니다 **개요** 블레이드 가상 네트워크에 대 한 합니다.
- 공유 키 - 동일한 공유 hello은이 사이트 간 VPN 연결을 만들 때 지정한 키입니다. 이 예제에서는 매우 기본적인 공유 키를 사용합니다. 더 복잡 한 키 toouse를 생성 해야 합니다.

Hello VPN 장치 구성 된 후에 VNet에 대 한 hello 대시보드 페이지에서 업데이트 된 연결 정보를 볼 수 있습니다.

### <a name="step-3-verify-your-local-network-ranges-and-vpn-gateway-ip-address"></a>3단계. 로컬 네트워크 범위 및 VPN 게이트웨이 IP 주소 확인
#### <a name="verify-your-vpn-gateway-ip-address"></a>VPN 게이트웨이 IP 주소 확인
게이트웨이 tooconnect에 대 한 적절 하 게 VPN 장치에 대 한 hello IP 주소 구성 되어야 합니다 올바르게 hello 사용자 크로스-프레미스 구성에 지정 된 로컬 네트워크에 대 한. 일반적으로 hello 사이트 간 구성 프로세스 중 구성 됩니다. 그러나 이전이 로컬 네트워크는 다른 장치에 사용 된 hello IP 주소가이 로컬 네트워크에 대 한 변경 이나 hello 설정을 toospecify hello 올바른 게이트웨이 IP 주소를 편집 합니다.

1. tooverify 게이트웨이 IP 주소를 클릭 하 여 **네트워크** 왼쪽된 포털 창 hello 되 고 다음을 선택 **로컬 네트워크** hello hello 페이지 위쪽에 있습니다. 사용자가 만든 각 로컬 네트워크 VPN 게이트웨이 주소 hello를 볼 수 있습니다. tooedit hello IP 주소는 VNet hello를 선택 하 고 클릭 **편집** hello hello 페이지 맨 아래에 있습니다.
2. Hello에 **로컬 네트워크 정보 지정** 페이지 hello IP 주소를 편집 하 고 hello hello hello 페이지 맨 아래에 다음 화살표를 클릭 합니다.
3. Hello에 **hello 주소 공간 지정** 페이지에서 설정을 더 낮은 오른쪽 toosave hello에 hello 확인 표시를 클릭 합니다.

#### <a name="verify-hello-address-ranges-for-your-local-networks"></a>로컬 네트워크에 대 한 hello 주소 범위를 확인 합니다.
Hello hello 게이트웨이 tooyour 온-프레미스 위치를 통해 올바른 트래픽 tooflow, tooverify 각 IP 주소 범위 지정이 필요 합니다. 각 범위가 Azure **로컬 네트워크** 구성에 나열되어야 합니다. Hello 온-프레미스 위치의 네트워크 구성에 따라 다소 큰 작업을 수 있습니다. 나열 된 hello 범위 내에 포함 된 IP 주소에 대해 바인딩된 트래픽은 hello 가상 네트워크 VPN 게이트웨이 통해 전송 됩니다. hello 나열 toobe 비공개 범위 없는, 온-프레미스 구성을 받을 수 있는 tooverify 인바운드 트래픽을 hello 있지만 싶을 것까지 다양 합니다.

로컬 네트워크에 대 한 hello 범위 tooadd 또는 편집 단계를 수행 하는 hello를 사용 합니다.

1. 로컬 네트워크에 대 한 tooedit hello IP 주소 범위를 클릭 **네트워크** 왼쪽된 포털 창 hello 되 고 다음 선택 **로컬 네트워크** hello hello 페이지 위쪽에 있습니다. Hello 포털에서 목록으로 나열 된 hello 가장 쉬운 방법은 tooview hello 범위는 hello에 **편집** 페이지. 선택 범위, VNet hello 및 클릭 toosee **편집** hello hello 페이지 맨 아래에 있습니다.
2. Hello에 **로컬 네트워크 정보 지정** 페이지에서 변경 내용을 확인 하지 않습니다. Hello hello hello 페이지 맨 아래에 다음 화살표를 클릭 합니다.
3. Hello에 **hello 주소 공간 지정** 페이지에서 네트워크 주소 공간 변경 내용을 확인 합니다. 그런 다음 확인 표시 toosave hello 구성을 클릭 합니다.

## <a name="how-tooview-gateway-traffic"></a>어떻게 tooview 게이트웨이 트래픽
가상 네트워크 **대시보드** 에서 게이트웨이 및 게이트웨이 트래픽을 확인할 수 있습니다.

Hello에 **대시보드** 페이지 hello 다음을 확인할 수 있습니다.

* 에 데이터와 데이터 게이트웨이 통해 전달 되는 데이터의 hello 양입니다.
* 가상 네트워크에 대해 지정 된 된 hello DNS 서버 hello 이름입니다.
* 게이트웨이 및 VPN 장치 간의 hello 연결입니다.
* hello 키를 사용 하는 tooconfigure 게이트웨이 연결 tooyour VPN 장치를 공유 합니다.

## <a name="how-toochange-hello-vpn-routing-type-for-your-gateway"></a>Toochange는 VPN 게이트웨이 라우팅 유형을 hello 하는 방법
일부 연결 구성의 특정 게이트웨이 라우팅 유형에 사용할 수만 있으므로 toochange hello 게이트웨이 VPN 라우팅 유형을 기존 VPN 게이트웨이의 사용 해야 하는 경우가 있습니다. 예를 들어 tooadd 지점 및 사이트 연결 tooan 이미 기존 사이트 간 연결에 정적 게이트웨이가 있는 경우가 있습니다. 지점 및 사이트 간 연결에는 동적 게이트웨이가 필요합니다. 즉, tooconfigure P2S 연결 toochange 정적 toodynamic에서 게이트웨이 라우팅 유형을 VPN 해야 합니다.

게이트웨이 라우팅 유형 VPN toochange 해야 할 경우 hello 기존 게이트웨이 삭제 하 고 새 라우팅 유형의 hello와 새 게이트웨이 만들 합니다. Toodelete hello 전체 가상 네트워크 toochange hello 게이트웨이 라우팅 유형이 필요는 없습니다.

게이트웨이 VPN 라우팅 유형을 변경 하기 전에 수 있는지 tooverify VPN 장치 hello 라우팅 유형을 toouse 한다는 것을 지원 합니다. toodownload 새 라우팅 구성 샘플 및 검사 VPN 장치 요구 사항 참조 [VPN 장치에 대 한 가상 네트워크 연결을 위한](vpn-gateway-about-vpn-devices.md)합니다.

> [!IMPORTANT]
> 가상 네트워크 VPN 게이트웨이 삭제 하면 hello toohello 게이트웨이 할당 된 VIP가 해제 됩니다. Hello 게이트웨이 다시 만들면 새 VIP tooit을 할당 됩니다.
> 
> 

1. **Hello 기존 VPN 게이트웨이 삭제 합니다.**
   
    Hello에 **대시보드** 가상 네트워크에 대 한 페이지 toohello hello 페이지 아래쪽 탐색 하 고 클릭 **게이트웨이 삭제**합니다. 게이트웨이 hello hello 알림을 대기 삭제 되었습니다. 게이트웨이가 삭제 되었다는 hello 화면에 hello 알림이 표시 되 면 새 게이트웨이 만들 수 있습니다.
2. **새 VPN 게이트웨이 만들기**
   
    Hello 프로시저를 사용 하 여 hello 페이지 toocreate 새 게이트웨이의 hello 위쪽: [VPN 게이트웨이 만들기](#create-a-vpn-gateway)합니다.

## <a name="next-steps"></a>다음 단계
가상 컴퓨터 tooyour 가상 네트워크를 추가할 수 있습니다. 참조 [방법을 사용자 지정 가상 컴퓨터를 toocreate](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.

Tooconfigure 지점-사이트 VPN 연결 참조 [지점-사이트 VPN 연결 구성](vpn-gateway-point-to-site-create.md)합니다.

