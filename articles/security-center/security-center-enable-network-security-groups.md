---
title: "Azure 보안 센터의 네트워크 보안 그룹 aaaEnable | Microsoft Docs"
description: "이 문서에서는 어떻게 tooimplement hello Azure 보안 센터 권장 * *를 사용 하도록 설정 네트워크 보안 그룹 * *입니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f53ed853-ffaf-4530-a019-1906ba6f341b
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 2f70fe432aa452f833a5c322d13102ebbd6dbb69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a>Azure 보안 센터의 네트워크 보안 그룹 활성화
Azure Security Center는 아직 활성화되지 않은 경우 NSG(네트워크 보안 그룹)를 활성화하는 것을 권장합니다. Nsg에 허용 하거나 거부할 네트워크 트래픽을 가상 네트워크에서 VM 인스턴스 tooyour 하는 액세스 제어 목록 (ACL) 규칙의 목록을 포함 합니다. NSG는 서브넷 또는 서브넷 내의 개별 VM 인스턴스 중 하나와 연결될 수 있습니다. NSG를 서브넷과 연결 하는 경우 해당 서브넷에 tooall hello VM 인스턴스 hello ACL 규칙에 적용 됩니다. 또한 트래픽 tooan 개별 VM을 제한할 수 NSG를 연결 하 여 추가 VM toothat 직접 합니다. toolearn 더 참조 [는 보안 그룹 NSG (네트워크) 이란?](../virtual-network/virtual-networks-nsg.md)

보안 센터 두 가지 권장 사항 tooyou 제공 활성화 Nsg가: 가상 컴퓨터에서 네트워크 보안 그룹을 사용 하도록 설정 하 고 서브넷에 네트워크 보안 그룹을 사용 하도록 설정 합니다. 어떤 수준, 서브넷 또는 VM에 Nsg tooapply 선택할 수 있습니다.

> [!NOTE]
> 이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.  단계별 가이드는 아닙니다.
>
>

## <a name="implement-hello-recommendation"></a>Hello 권장 구성 구현
1. Hello에 **권장 사항을** 블레이드를 **네트워크 보안 그룹 사용** 가상 컴퓨터 또는 서브넷에 있습니다.
   ![네트워크 보안 그룹 활성화][1]
2. Hello 블레이드가 열립니다 **누락 된 네트워크 보안 그룹 구성** 서브넷에 대 한 또는 선택한 hello 권장 사항에 따라 가상 컴퓨터에 대 한 합니다. 서브넷 또는 가상 컴퓨터 tooconfigure NSG 선택 합니다.

   ![서브넷에 대한 NSG 구성][2]

   ![VM에 대한 NSG 구성][3]
3. Hello에 **네트워크 보안 그룹 선택** 블레이드에서 기존 NSG를 선택 하거나 선택 **새로 만들기** toocreate NSG 합니다.

   ![네트워크 보안 그룹 선택][4]

NSG를 만들면 hello 단계에 따라 [어떻게 toomanage Nsg를 사용 하 여 Azure 포털을 hello](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate NSG 보안 규칙을 설정 합니다.

## <a name="see-also"></a>참고 항목
이 문서는 어떻게 tooimplement hello 보안 센터 권장 사항 "네트워크 보안 그룹 사용" 서브넷 또는 가상 컴퓨터에 대해 알아보았습니다. Nsg를 사용에 대 한 더 toolearn hello 다음을 참조 합니다.

* [NSG(네트워크 보안 그룹)란?](../virtual-network/virtual-networks-nsg.md)
* [Toomanage Nsg를 사용 하 여 Azure 포털을 hello 하는 방법](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.
* [Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.
* [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.
* [Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -hello 최신 Azure 보안 뉴스 및 정보를 가져옵니다.

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
