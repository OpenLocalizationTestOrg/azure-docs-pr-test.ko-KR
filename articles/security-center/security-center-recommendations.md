---
title: "Azure 보안 센터에서 aaaManaging 보안 권장 사항 | Microsoft Docs"
description: "이 문서에서는 Azure 보안 센터의 권장 사항이 Azure 리소스를 보호하고 보안 정책을 준수하는 데 어떤 도움이 되는지 알아봅니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 86c50c9f-eb6b-4d97-acb3-6d599c06133e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: terrylan
ms.openlocfilehash: f6bbe36a7a5636095b339b3e9765b87cc0ab669a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-security-recommendations-in-azure-security-center"></a>Azure 보안 센터에서 보안 권장 사항 관리
이 문서에서는 Azure 보안 센터 toohelp toouse 권장 사항을 보호 방법을 통해 Azure 리소스입니다.

> [!NOTE]
> 이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.  이 문서는 단계별 가이드가 아닙니다.
>
>

## <a name="what-are-security-recommendations"></a>보안 권장 사항이란?
보안 센터 리소스를 Azure의 hello 보안 상태를 정기적으로 분석합니다. 보안 센터가 잠재적인 보안 취약점을 식별하는 경우 권장 사항을 만듭니다. hello 권장 사항이 필요한 hello 컨트롤 구성의 hello 프로세스를 안내 합니다.

## <a name="implementing-security-recommendations"></a>보안 권장 사항 구현
### <a name="set-recommendations"></a>권장 사항 설정
[Azure 보안 센터의 보안 정책 설정](security-center-policies.md)에서 다음을 배울 수 있습니다.

* 보안 정책 구성.
* 데이터 수집 사용.
* 보안 정책의 일부로 서 권장 사항을 toosee를 선택 합니다.

현재 정책 권장 사항은 시스템 업데이트, 기준 규칙, 맬웨어 방지 프로그램, 서브넷 및 네트워크 인터페이스의 [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md) , SQL 데이터베이스 감사, SQL 데이터베이스 투명한 데이터 암호화 및 웹 응용 프로그램 방화벽에 중점을 두고 있습니다.  [보안 정책 설정](security-center-policies.md) 은 각 권장 사항 옵션에 대한 설명을 제공합니다.

### <a name="monitor-recommendations"></a>권장 사항 모니터링
보안 정책으로 설정한 후 보안 센터 리소스 tooidentify 잠재적인 취약점의 hello 보안 상태를 분석 합니다. hello **권장 사항을** hello 타일 **보안 센터** 블레이드 hello 보안 센터로 식별 되는 권장 구성의 총 수 알 수 있습니다.

![권장 사항 타일][1]

각 권장 사항은의 toosee hello 세부 정보:

선택 hello **권장 사항을 타일** hello에 **보안 센터** 블레이드입니다. hello **권장 사항을** 블레이드를 엽니다.

hello 권장 여기서 각 줄은 한 가지 특정 권장 하는 테이블 형식으로 표시 됩니다. 이 테이블의 열이 hello 됩니다.

* **설명**: hello 권장 사항 및 tooaddress 수행 toobe는 사항에 대해 설명 것입니다.
* **리소스**:이 권장 사항을 적용 하는 hello 리소스 toowhich를 나열 합니다.
* **상태**: hello hello 권장 구성의 현재 상태에 설명 합니다.
  * **열기**: hello 권장 아직 해결 되지 않았습니다.
  * **진행 중인**: hello 권장 구성이 현재 적용 된 toohello 리소스를 생성할 수 있으며 사용자가 아무 작업도 필요 합니다.
  * **해결**: hello 권장 구성이 이미 완료 되었습니다 (이 경우 hello 줄은 회색으로 표시).
* **심각도**: hello 심각도입니다. 해당 특정 권장 사항 설명 합니다.
  * **높음**: 중요한 리소스(응용 프로그램, VM, 네트워크 또는 보안 그룹 등)에 취약점이 있으며 주의가 필요합니다.
  * **보통**: 취약성이 존재 하 고 중요 하지 않은 또는 추가 단계는 필요한 tooeliminate 또는 toocomplete 프로세스입니다.
  * **낮음**: 해결해야 하지만 즉시 조치하지 않아도 되는 취약점이 있습니다. (기본적으로 낮은 권장 구성이 제시 하지 않지만 toosee 하려는 경우 낮은 권장 사항에 필터링 할 수 있습니다 이러한.)

Hello 사용할 수 있는 권장 사항 및 각 용도 적용 하는 경우 참조 toohelp으로 아래 hello 테이블 사용 이해 합니다.

> [!NOTE]
> Toounderstand hello 원하는 [클래식 및 리소스 관리자 배포 모델](../azure-classic-rm.md) Azure 리소스에 대 한 합니다.
>
>

| 권장 사항 | 설명 |
| --- | --- |
| [구독에 대해 데이터 수집 활성화](security-center-enable-data-collection.md) |구독에서 각 구독 하 고 모든 가상 컴퓨터 (Vm)에 대 한 hello 보안 정책에서 데이터 컬렉션 켜기 하는 것이 좋습니다. |
| [OS 취약성 해결](security-center-remediate-os-vulnerabilities.md) |구성 규칙 예를 들어 권장 hello 운영 체제 구성에 맞춰 암호 toobe 저장 하지 못하게 하는 것이 좋습니다. |
| [시스템 업데이트 적용](security-center-apply-system-updates.md) |누락 된 시스템 보안 및 중요 업데이트 tooVMs를 배포 하는 것이 좋습니다. |
| [Just-In-Time 네트워크 액세스 제어 적용](security-center-just-in-time.md) | Just-In-Time VM 액세스만 적용해야 합니다. 시간 기능에만 있는 hello 되며 미리 보기에서 hello 보안 센터의 표준 계층에 있습니다. 참조 [가격 책정](security-center-pricing.md) 보안 센터에 대해 자세히 toolearn 가격 책정 계층이 있습니다. |
| [시스템 업데이트 후 다시 부팅](security-center-apply-system-updates.md#reboot-after-system-updates) |시스템 업데이트를 적용 한 VM toocomplete hello 프로세스를 다시 부팅 하는 것이 좋습니다. |
| [웹 응용 프로그램 방화벽 추가](security-center-add-web-application-firewall.md) |웹 끝점에 WAF(웹 응용 프로그램 방화벽)를 배포하는 것이 좋습니다. 공개 인바운드 웹 포트(80,443)으로 연결된 네트워크 보안 그룹에 있는 모든 공용 연결 IP(인스턴스 수준 IP 또는 부하 분산된 IP)에 대해 WAF 권장 사항이 표시됩니다. </br>보안 센터 앱 서비스 환경 및 가상 컴퓨터에서 웹 응용 프로그램을 대상으로 하는 공격 방어 WAF toohelp 구축 하는 것이 좋습니다. ASE(App Service 환경)는 Azure App Service의 [프리미엄](https://azure.microsoft.com/pricing/details/app-service/) 서비스 계획 옵션으로, Azure App Service 앱의 안전한 실행을 위해 완전히 격리된 전용 환경을 제공합니다. toolearn ASE에 대 한 자세한 참조 hello [앱 서비스 환경 설명서](../app-service/app-service-app-service-environments-readme.md)합니다.</br>이러한 응용 프로그램 tooyour 기존 WAF 배포를 추가 하 여 보안 센터에서 여러 웹 응용 프로그램을 보호할 수 있습니다. |
| [응용 프로그램 보호 완료](security-center-add-web-application-firewall.md#finalize-application-protection) |toocomplete hello 구성을 WAF, 트래픽 다시 라우팅된 toohello WAF 기기 이어야 합니다. 이렇게 hello 필요한 설정 변경을 완료 합니다. |
| [차세대 방화벽 추가](security-center-add-next-generation-firewall.md) |추가 하는 다음 세대 방화벽 (NGFW)에서 Microsoft 파트너 tooincrease 보안 보호 하는 것이 좋습니다. |
| [NGFW를 통해서만 트래픽 라우팅](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |인바운드 트래픽을 tooyour 프로그램 NGFW 통해 VM을 강제 하는 네트워크 보안 그룹 (NSG) 규칙을 구성 하는 것이 좋습니다. |
| [Endpoint Protection 설치](security-center-install-endpoint-protection.md) |맬웨어 방지 프로그램 tooVMs (Windows Vm에만 해당)를 프로 비전 하는 것이 좋습니다. |
| [Endpoint Protection 상태 경고 해결](security-center-resolve-endpoint-protection-health-alerts.md) |끝점 보호 오류를 해결하는 것이 좋습니다. |
| [서브넷 또는 가상 컴퓨터에서 네트워크 보안 그룹 활성화](security-center-enable-network-security-groups.md) |서브넷 또는 VM에서 NSG를 활성화하는 것이 좋습니다. |
| [인터넷 끝점을 통한 액세스 제한](security-center-restrict-access-through-internet-facing-endpoints.md) |NSG에 대한 인바운드 트래픽 규칙을 구성하라는 권장 사항입니다. |
| [SQL Server에서 감사 및 위협 감지 사용](security-center-enable-auditing-on-sql-servers.md) |Azure SQL 서버에 대한 감사 및 위협 감지를 켜는 것이 좋습니다. (Azure SQL 서비스에만 해당됩니다. 가상 컴퓨터에서 실행 중인 SQL을 포함하지 않습니다.) |
| [SQL Database에서 감사 및 위협 감지 사용](security-center-enable-auditing-on-sql-databases.md) |Azure SQL Database에 대한 감사 및 위협 감지를 켜는 것이 좋습니다. (Azure SQL 서비스에만 해당됩니다. 가상 컴퓨터에서 실행 중인 SQL을 포함하지 않습니다.) |
| [SQL 데이터베이스에서 투명한 데이터 암호화 활성화](security-center-enable-transparent-data-encryption.md) |SQL Database에 대해 암호화를 활성화하는 것이 좋습니다. (Azure SQL 서비스에만 해당됩니다.) |
| [VM 에이전트 사용](security-center-enable-vm-agent.md) |하면 toosee Vm 해야 하는 hello VM 에이전트를 사용 합니다. hello VM 에이전트가 Vm tooprovision 패치 검사, 검색 기준 및 맬웨어 방지 프로그램에 설치 해야 합니다. hello Azure Marketplace에서에서 배포 되는 Vm에 대 한 hello VM 에이전트는 기본적으로 설치 됩니다. hello 문서 [VM 에이전트 및 확장-2 부](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) tooinstall VM 에이전트를 hello 하는 방법에 대해 설명 합니다. |
| [디스크 암호화 적용](security-center-apply-disk-encryption.md) |Azure 디스크 암호화(Windows 및 Linux VM)를 사용하여 VM 디스크를 암호화하는 것이 좋습니다. Hello OS와 VM에 데이터 볼륨에 대 한 암호화를 사용 하는 것이 좋습니다. |
| [보안 연락처 세부 정보 제공](security-center-provide-security-contact-details.md) |각 구독에 대한 보안 연락처 정보를 제공하는 것을 권장합니다. 연락처 정보는 전자 메일 주소 및 전화 번호입니다. hello 정보를 사용 하는 toocontact 사용자 리소스가 손상 되는 보안 팀 발견 있습니다. |
| [OS 버전 업데이트](security-center-update-os-version.md) |OS 제품군에 대 한 hello 운영 체제 (OS) 버전에 클라우드 서비스 toohello 사용 가능한 최신 버전에 대 한 업데이트 하는 것이 좋습니다.  클라우드 서비스에 대해 자세히 toolearn 참조 hello [클라우드 서비스 개요](../cloud-services/cloud-services-choose-me.md)합니다. |
| [취약점 평가 설치되지 않음](security-center-vulnerability-assessment-recommendations.md) |VM에 취약점 평가 솔루션을 설치하는 것이 좋습니다. |
| [취약점 해결](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |VM에 설치 하는 hello 취약점 평가 솔루션에 의해 검색 toosee 시스템 및 응용 프로그램 취약성이 있습니다. |
| [Azure Storage 계정에 암호화 사용](security-center-enable-encryption-for-storage-account.md) | 미사용 데이터에 대한 Azure Storage 서비스 암호화를 사용하도록 권장합니다. 저장소 서비스 암호화 (SSE) tooAzure 저장소 작성 하 고 검색 하기 전에 암호를 해독 하는 경우 hello 데이터를 암호화 하 여 작동 합니다. SSE는 hello Azure Blob 서비스에 대 한 현재 사용할 수 및 블록 blob의 페이지 blob 사용할 수 있으며 추가 blob입니다. toolearn 더 참조 [미사용 데이터에 대 한 저장소 서비스 암호화](../storage/common/storage-service-encryption.md)합니다.</br>SSE는 Resource Manager 저장소 계정에만 지원됩니다. |

필터링을 수행하고 권장 사항을 해제할 수 있습니다.

1. 선택 **필터** hello에 **권장 사항을** 블레이드입니다. hello **필터** 블레이드가 열리고 toosee 원하는 hello 심각도 및 상태 값을 선택 합니다.

    ![필터 권장 사항][2]
2. 권장 사항을 적용 가능 하지 않은 판단 되 면 hello 추천을 해제할 수 있으며 다음 보기 바깥 필터링 수 있습니다. 권장 사항을 두 가지 방법으로 toodismiss가 됩니다. 한 가지 방법은 tooright 클릭 된 항목을 선택 합니다 **Dismiss**합니다. 다른 hello toohover를 항목 위로 이므로 toohello 오른쪽으로 표시 한 다음 선택 하는 hello 세 점을 클릭 **Dismiss**합니다. **필터**를 클릭하고 **해제됨**을 선택하면 해제된 권장 사항을 볼 수 있습니다.

    ![권장 사항 해제][3]

### <a name="apply-recommendations"></a>권장 사항 적용
모든 권장 사항을 검토한 후에 가장 먼저 적용해야 할 권장 사항을 결정합니다. 어떤 권장 사항을 먼저 적용 해야 하는 주요 매개 변수 tooevaluate hello 대로 hello 심각도 등급을 사용 하는 것이 좋습니다.

위 권장 사항의 hello 표에 권장 사항을 선택 하 고 방법의 예를 들어 단계별로 tooapply 권장 합니다.

## <a name="next-steps"></a>다음 단계
이 문서에서는 있었습니다. 보안 센터에 도입 된 toosecurity 권장 사항입니다. 보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -학습 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.
* [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -학습 방법을 toomanage 및 응답 toosecurity 경고 합니다.
* [Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) - Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.

<!--Image references-->
[1]: ./media/security-center-recommendations/recommendations-tile.png
[2]: ./media/security-center-recommendations/filter-recommendations.png
[3]: ./media/security-center-recommendations/dismiss-recommendations.png
