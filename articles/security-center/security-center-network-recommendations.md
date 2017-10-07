---
title: "aaaProtecting 네트워크의 Azure 보안 센터 | Microsoft Docs"
description: "이 문서에서는 Azure 네트워크를 보호하고 보안 정책을 준수하는 데 도움이 되는 Azure 보안 센터의 권장 사항에 대해 설명합니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 96c55a02-afd6-478b-9c1f-039528f3dea0
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: terrylan
ms.openlocfilehash: 053738da432edf13b40172fb44d2044702dd8211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a>Azure 보안 센터에서 네트워크 보호
Azure 보안 센터 리소스를 Azure의 hello 보안 상태를 분석합니다. 보안 센터 잠재적인 보안 문제를 식별 하는 경우 필요한 hello 컨트롤 구성 hello 과정을 안내 하는 권장 구성을 만듭니다.  권장 사항이 적용 tooAzure 리소스 종류: 가상 컴퓨터 (Vm), 네트워킹, SQL, 및 응용 프로그램입니다.

이 문서에서는 tooyour 네트워크 적용 되는 권장 합니다.  네트워크 권장 사항은 차세대 방화벽, 네트워크 보안 그룹, 인바운드 트래픽 규칙 구성 등에 초점을 둡니다.  Hello 사용 가능한 네트워크 권장 사항 및 각 용도 적용 하는 경우 참조 toohelp으로 아래 hello 테이블 사용 이해 합니다.

## <a name="available-network-recommendations"></a>제공되는 네트워크 권장 사항
| 권장 사항 | 설명 |
| --- | --- |
| [차세대 방화벽 추가](security-center-add-next-generation-firewall.md) |추가 하는 다음 세대 방화벽 (NGFW)에서 Microsoft 파트너 tooincrease 보안 보호 하는 것이 좋습니다. |
| [NGFW를 통해서만 트래픽 라우팅](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |인바운드 트래픽을 tooyour 프로그램 NGFW 통해 VM을 강제 하는 네트워크 보안 그룹 (NSG) 규칙을 구성 하는 것이 좋습니다. |
| [서브넷 또는 가상 컴퓨터에서 네트워크 보안 그룹 활성화](security-center-enable-network-security-groups.md) |서브넷 또는 VM에서 NSG를 활성화하는 것이 좋습니다. |
| [인터넷 끝점을 통한 액세스 제한](security-center-restrict-access-through-internet-facing-endpoints.md) |NSG에 대한 인바운드 트래픽 규칙을 구성하라는 권장 사항입니다. |

## <a name="see-also"></a>참고 항목
tooother Azure 리소스 유형에 적용 되는 권장 사항에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure 보안 센터에서 가상 컴퓨터 보호](security-center-virtual-machine-recommendations.md)
* [Azure 보안 센터에서 응용 프로그램 보호](security-center-application-recommendations.md)
* [Azure 보안 센터에서 Azure SQL 서비스 보호](security-center-sql-service-recommendations.md)

보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.
* [Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
