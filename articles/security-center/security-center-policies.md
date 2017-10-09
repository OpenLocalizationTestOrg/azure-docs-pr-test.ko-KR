---
title: "Azure 보안 센터에서 aaaSet 보안 정책 | Microsoft Docs"
description: "이 문서에서는 Azure 보안 센터에서 tooconfigure 보안 정책을 하면 있습니다."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 3b9e1c15-3cdb-4820-b678-157e455ceeba
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: yurid
ms.openlocfilehash: 59226dd84a1c66a2d8367417060ab10a1ff73848
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-security-policies-in-azure-security-center"></a>Azure Security Center에서 보안 정책 설정
이 문서를 사용 하면 tooconfigure 보안 정책 보안 센터에서 안내 하는 데 필요한 단계 tooperform hello이이 작업으로 합니다.

>[!NOTE] 
>보안 센터 초기 년 6 월 2017 년 부터는 hello Microsoft Monitoring Agent toocollect 및 저장소 데이터를 사용 합니다. 참조 [Azure 보안 센터 플랫폼 마이그레이션](security-center-platform-migration.md) toolearn 더 합니다. 이 문서의 정보 hello 전환 toohello Microsoft Monitoring Agent 후 보안 센터 기능을 나타냅니다.
>

## <a name="what-are-security-policies"></a>보안 정책이란?
지정 된 hello 내의 리소스에 대 한 권장 되는 컨트롤의 hello 집합을 정의 하는 보안 정책을 구독 합니다. 보안 센터 tooyour 회사 보안 요구 사항과 hello 응용 프로그램 종류 또는 hello 데이터 각 구독에서의 민감도 따라 Azure 구독에 대 한 정책을 정의 합니다.

예를 들어 개발 또는 테스트에 사용되는 리소스는 프로덕션 응용 프로그램에 사용되는 리소스와 보안 요구 사항이 다릅니다. 마찬가지로 PII(Personally Identifiable Information) 같은 규제된 데이터를 가진 응용 프로그램에는 더 높은 수준의 보안이 필요할 수 있습니다. Azure 보안 센터 드라이브에 대 한 보안 권장 사항 및 잠재적인 보안 문제를 식별 한 위협을 완화 모니터링 toohelp에 설정 된 보안 정책입니다. 읽기 [Azure 보안 센터 계획 및 운영 가이드](security-center-planning-and-operations-guide.md) toodetermine hello 옵션 하 하는 방법에 대 한 자세한 내용은 자신에 게 적합 합니다.

## <a name="set-security-policies"></a>보안 정책 설정
각 구독에 대한 보안 정책을 구성할 수 있습니다. 보안 정책 toomodify 소유자나 해당 구독에 대 한 참가자 여야 합니다. Toohello Azure 포털에에서 로그인 하 고 보안 센터에서 tooconfigure 보안 정책을 단계 다음에 나오는 hello를 따릅니다.

1. Hello 클릭 **정책** hello 보안 센터 대시보드에서 타일입니다.
2. 열리면 hello 보안 정책 블레이드에서 tooenable hello 보안 정책을 원하는 hello 구독을 선택 합니다.

    ![정책 정의](./media/security-center-policies/security-center-policies-fig1-ga.png)
3. hello **보안 정책** 블레이드 hello 선택한 구독에 대 한 옵션 집합이 열립니다. 이 블레이드에 hello 사용할 수 있는 옵션은 같습니다.

   * **방지 정책**: 구독에 대해이 옵션 tooconfigure 정책을 사용 합니다.  
   * **전자 메일 알림**: hello 첫 번째 일별 항목 경고의 심각도 높은 경고에 대 한에서이 옵션 tooconfigure 전송 된 전자 메일 알림을 사용 합니다. 전자 메일 기본 설정은 구독 정책에 대해서만 구성할 수 있습니다. 읽기 [Azure 보안 센터에서 보안 연락처 세부 정보를 제공](security-center-provide-security-contact-details.md) 방법에 대 한 자세한 내용은 전자 메일 알림 tooconfigure 합니다.
   * **가격 책정 계층**: 선택한 계층의 가격 책정 옵션 tooupgrade hello이를 사용 합니다. 참조 [보안 센터 가격](security-center-pricing.md) toolearn 옵션 가격에 대 한 자세한 합니다.
4. **가상 컴퓨터에서 데이터 수집** 옵션을 **켜기**로 설정합니다. 이 옵션을 사용 하면 hello Microsoft Monitoring Agent를 사용 하 여 기존 및 새 리소스에 대 한 자동 로그 컬렉션 –이 hello 동일한 에이전트 hello Operations Management Suite 및 로그 분석 서비스에서 사용 합니다. 이 에이전트에서 수집 된 데이터는 계정 hello geography의 hello VM Azure 구독에 연결 된 하는 기존 로그 분석 중 또는 새 중에 저장 됩니다.

5. Hello에 **보안 정책** 블레이드에서 클릭 **방지 정책** toosee hello 사용할 수 있는 옵션입니다. 클릭 **에** 이 구독의 관련 된 tooenable hello 보안 권장 사항입니다.

    ![Hello 보안 정책 선택](./media/security-center-policies/security-center-policies-fig7.png)

다음 표 참조 toounderstand로 hello 각 옵션을 사용 합니다.

| 정책 | 상태가 켜진 경우 |
| --- | --- |
| 시스템 업데이트 |Windows 업데이트 또는 Windows Server Update Services에서 사용 가능한 보안 및 중요 업데이트의 일일 목록을 검색합니다. hello 검색된 목록 실행 hello 서비스가 해당 가상 컴퓨터에 대해 구성 되 고 hello 누락 된 업데이트를 적용 하는 것이 좋습니다. Linux 시스템에 대 한 hello 정책 hello distro 제공 패키지 관리 시스템 toodetermine 패키지를 사용 가능한 업데이트를 사용 합니다. 또한 [Azure Cloud Services](../cloud-services/cloud-services-how-to-configure.md) 가상 컴퓨터에서 보안 및 중요 업데이트를 확인합니다. |
| OS 취약성 |운영 체제 구성을 매일 toodetermine 문제 hello 가상 컴퓨터 취약 tooattack을 만들 수 있는 분석 합니다. hello 정책 권장 구성 변경 내용을 tooaddress 이러한 취약점 합니다. Hello 참조 [권장된 기준 목록](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335) hello 모니터링 되는 특정 구성에 대 한 자세한 내용은 합니다. (현재는 Windows Server 2016이 완전히 지원되지 않습니다.) |
| Endpoint Protection |끝점 보호 toobe toohelp 식별 하 고 바이러스, 스파이웨어 및 기타 악성 소프트웨어를 제거 합니다. 모든 Windows 가상 컴퓨터에 대 한 사용자를 프로 비전을 권장 합니다. |
| 디스크 암호화 |저장 된 상태의 모든 tooenhance 데이터 보호 가상 컴퓨터의에서 디스크 암호화를 사용 하도록 설정 하는 것이 좋습니다. |
| 네트워크 보안 그룹 |것을 권장 합니다 [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md) 인바운드 및 아웃 바운드 구성된 toocontrol 될 공용 끝점이 tooVMs 트래픽입니다. 별도로 지정하지 않는 한, 서브넷에 대해 구성된 네트워크 보안 그룹은 모든 가상 컴퓨터 네트워크 인터페이스에서 상속됩니다. 또한 toochecking 네트워크 보안 그룹 구성 되어 있는지,이 정책은 들어오는 트래픽을 허용 하는 인바운드 보안 규칙 tooidentify 규칙 평가 합니다. |
| 웹 응용 프로그램 방화벽 |가상 컴퓨터에서에 hello 다음 중 하나에 해당 하는 경우 웹 응용 프로그램 방화벽을 구축 하는 것이 좋습니다. </br></br>[인스턴스 수준 공용 IP](../virtual-network/virtual-networks-instance-level-public-ip.md) (ILPIP)가 사용 되며 hello hello 연결된 네트워크 보안 그룹에 대 한 인바운드 보안 규칙 구성된 tooallow 액세스 tooport 80/443입니다.</br></br>부하 분산 된 IP는 및 hello를 연결 된 부하 분산 및 인바운드 네트워크 주소 변환 (NAT) 규칙은 구성 된 tooallow 액세스 tooport 80/443 합니다. 자세한 내용은 [Load Balancer에 대한 Azure Resource Manager 지원](../load-balancer/load-balancer-arm.md)을 참조하세요. |
| 차세대 방화벽 |Azure에 기본 제공되는 네트워크 보안 그룹 외에도 네트워크 보호 기능을 확장합니다. 보안 센터를 다음 세대 방화벽 좋습니다 되었으며 tooprovision 가상 어플라이언스를 사용 하도록 설정 배포를 검색 합니다. |
| SQL 감사 및 위협 감지 |규정 준수에 대 한 사용 및 조사를 위해 위협 요소 탐지 고급 수 액세스 tooAzure 데이터베이스의 감사 하는 것이 좋습니다. |
| SQL 암호화 |Azure SQL Database, 연결된 백업 및 트랜잭션 로그 파일에 대해 휴지 상태의 암호화를 활성화하는 것이 좋습니다. 데이터 위반이 있더라도 데이터를 읽을 수 없습니다. |
| 취약점 평가 |VM에 취약점 평가 솔루션을 설치하는 것이 좋습니다. |
| Storage 암호화 |현재 이 기능은 Azure Blob 및 Files에서 사용할 수 있습니다. Storage 서비스 암호화를 사용하도록 설정하더라도 이후 새 데이터만 암호화되고 이 저장소 계정의 기존 파일은 암호화되지 않은 상태로 유지됩니다. |
| JIT 네트워크 액세스 |Just-in-time에서 활성화 되 면 NSG 규칙을 만들어 보안 센터 인바운드 트래픽 tooyour Azure Vm 아래로 잠급니다. Hello 포트 선택 hello VM toowhich에 인바운드 트래픽을 잠겨 야 합니다. 자세한 내용은 [Just-In-Time를 사용하여 가상 컴퓨터 액세스 관리](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)를 참조하세요. |

모든 옵션을 구성한 후 클릭 **확인** hello에 **보안 정책** 에 hello 권장 사항이 클릭 한 다음 블레이드 **저장** hello에 **보안 정책** 블레이드 hello에 초기 설정이 됩니다.

> [!NOTE]
> 가격 책정 계층 hello hello 리소스 그룹 수준에 계속 적용 됩니다. 자세한 내용은 방문 hello [가격 책정](https://azure.microsoft.com/pricing/details/security-center/) 페이지.
>
>

## <a name="see-also"></a>참고 항목
이 문서에서는 방법에 대해 배웠습니다 Azure 보안 센터에서 tooconfigure 보안 정책입니다. Azure 보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure Security Center planning and operations guide](security-center-planning-and-operations-guide.md)로 설정합니다. 자세한 내용은 방법 tooplan hello 디자인 고려 사항 tooadopt Azure 보안 센터를 이해 하 고 있습니다.
* [Azure Security Center에서 보안 상태 모니터링](security-center-monitoring.md). Toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md)합니다. 자세한 내용은 방법 toomanage 및 응답 toosecurity 경고 합니다.
* [Azure Security Center를 사용하여 파트너 솔루션 모니터링](security-center-partner-solutions.md). Toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure Security Center FAQ](security-center-faq.md)로 설정합니다. Hello 서비스를 사용 하는 방법에 대 한 질문과 대답을 찾습니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/). Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.
