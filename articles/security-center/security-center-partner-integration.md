---
title: "Azure 보안 센터에서 aaaPartner 통합 | Microsoft Docs"
description: "Azure 보안 센터 파트너 tooenhance로 통합 하는 방법에 대 한 자세한 내용은 Azure 리소스의 전반적인 보안 합니다."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 6af354da-f27a-467a-8b7e-6cbcf70fdbcb
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: yurid
ms.openlocfilehash: 3621335730a076721cb3c23788a47be50aa8fc73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="partner-integration-in-azure-security-center"></a>Azure Security Center에서 파트너 통합

이 문서에서는 Azure 보안 센터 파트너 toohelp와 통합 하는 방법을 설명 전반적인 보안을 강화 합니다. 보안 센터는 Azure에서 통합된 환경을 제공 하 고 인증 및 요금 청구는 파트너에 대 한 Azure 마켓플레이스 hello 활용 합니다.

> [!NOTE] 
> 보안 센터 2017 년 1 월을 기준으로 hello Microsoft Monitoring Agent toocollect 및 저장소 데이터를 사용합니다. 자세한 내용은 [Azure Security Center 플랫폼 마이그레이션](security-center-platform-migration.md)을 참조하세요. 이 문서의 정보 hello 전환 toohello Microsoft Monitoring Agent 후 보안 센터 기능을 나타냅니다.
>

## <a name="why-deploy-partner-solutions-from-security-center"></a>Security Center에서 파트너 솔루션을 배포하는 이유는 무엇입니까?

보안 센터에서 4 개의 주요 이유 tooleverage 파트너 통합이 됩니다.

- **배포의 용이성** 다음 hello 보안 센터 권장 구성 하 여 파트너 솔루션을 배포 하는 것이 훨씬 쉽습니다. 기본 설정 및 네트워크 토폴로지를 사용 하 여 hello 배포 프로세스를 완벽 하 게 자동화할 수 있습니다. 또는 고객은 유연성 및 사용자 지정을 위한 반자동화된 옵션을 선택할 수 있습니다.
- **통합된 감지** 파트너 솔루션의 보안 이벤트는 자동으로 수집, 집계되며 Security Center 알림 및 사고의 일부로 표시됩니다. 또한 이러한 이벤트 고급 위협 요소 탐지 기능 다른 소스 tooprovide의 검색으로 결합 합니다.
- **통합 상태 모니터링 및 관리** 고객을 한 눈에 통합 된 상태 이벤트 toomonitor 모든 파트너 솔루션으로 사용할 수 있습니다. 기본 관리는 hello 업체 솔루션을 사용 하 여 쉽게 액세스할 수 있도록 tooadvanced 설치 프로그램을 사용할 수 있습니다.
- **TooSIEM 내보내기**합니다. 고객 모든 보안 센터를 내보낼 수 및 파트너 공통 이벤트 형식 (CEF) tooon 온-프레미스 보안 정보 및 이벤트 관리 SIEM () 시스템 경고 Azure 로그 통합 (미리 보기)를 사용 하 여 합니다.


## <a name="partners-that-integrate-with-security-center"></a>Security Center와 통합되는 파트너

Security Center는 현재 다음과 같은 솔루션과 통합합니다.

- 끝점 보호([Trend Micro](https://help.deepsecurity.trendmicro.com/azure-marketplace-getting-started-with-deep-security.html), Symantec 및 [Azure Cloud Services와 Virtual Machines용 Microsoft 맬웨어 방지 프로그램](https://docs.microsoft.com/azure/security/azure-security-antimalware)) 
- 웹 응용 프로그램 방화벽([Barracuda](https://www.barracuda.com/products/webapplicationfirewall), [F5](https://support.f5.com/kb/en-us/products/big-ip_asm/manuals/product/bigip-ve-web-application-firewall-microsoft-azure-12-0-0.html), [Imperva](https://www.imperva.com/Products/WebApplicationFirewall-WAF), [Fortinet](https://www.fortinet.com/resources.html?limit=10&search=&document-type=data-sheets) 및 [Azure Application Gateway](https://azure.microsoft.com/blog/azure-web-application-firewall-waf-generally-available/)) 
- 차세대 방화벽([Check Point](https://www.checkpoint.com/products/vsec-microsoft-azure/), [Barracuda](https://campus.barracuda.com/product/nextgenfirewallf/article/NGF/AzureDeployment/), [Fortinet](http://docs.fortinet.com/d/fortigate-fortios-handbook-the-complete-guide-to-fortios-5.2) 및 [Cisco](http://www.cisco.com/c/en/us/td/docs/security/firepower/quick_start/azure/ftdv-azure-qsg.html)) 
- 취약성 평가([Qualys](https://www.qualys.com/public-clouds/microsoft-azure/))  

시간이 지남에 따라 보안 센터 hello 수가 이러한 범주 내에서 파트너를 확장 하 고 새 항목을 추가 합니다. 

## <a name="deploy-a-partner-solution"></a>파트너 솔루션 배포

Azure 환경 및 hello 보안 정책을 정의한 hello 설정을 기준으로 보안 센터 파트너 솔루션을 배포 하면 권장할 수도 있습니다. 보안 센터 권장 hello hello 선택 하 고 파트너 솔루션 설치 과정을 안내 합니다. hello 전반적인 배포 환경을 따라 달라 hello 형식의 솔루션 및 파트너를 사용 합니다. 자세한 내용은 다음 문서는 hello 참조:

- [Endpoint Protection 설치](security-center-install-endpoint-protection.md)
- [웹 응용 프로그램 방화벽 추가](security-center-add-web-application-firewall.md)
- [차세대 방화벽 추가](security-center-add-next-generation-firewall.md)
- [취약점 평가 설치되지 않음](security-center-vulnerability-assessment-recommendations.md)

## <a name="manage-partner-solutions"></a>파트너 솔루션 관리

배포 후 tooview hello 솔루션의 상태를 hello 및 대해서 hello에서 기본 관리 작업을 수행할 **보안 센터** 블레이드, 선택 hello **파트너 솔루션** 옵션입니다. Security Center에서 파트너 솔루션을 관리하는 방법에 대한 자세한 내용은 [Azure Security Center로 파트너 솔루션 모니터링](security-center-partner-solutions.md)을 참조하세요.

![파트너 통합](./media/security-center-partner-integration/security-center-partner-integration-fig1-new2.png)

> [!NOTE]
> Symantec endpoint protection 지원 제한 toodiscovery입니다. 상태 경고는 사용할 수 없습니다.
>

## <a name="see-also"></a>참고 항목

이 문서에서는 toointegrate 파트너 Azure 보안 센터에서 솔루션 하는 방법을 배웠습니다. 보안 센터에 대해 자세히 toolearn hello 다음 문서 참조:

* [Security Center 계획 및 작업 가이드](security-center-planning-and-operations-guide.md)
* [관리 및 보안 센터에서 toosecurity 경고에 응답](security-center-managing-and-responding-alerts.md)
* [Azure Security Center에서 유형별 보안 경고](security-center-alerts-type.md)
* [Security Center에서 보안 상태 모니터링](security-center-monitoring.md) Toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Security Center를 사용하여 파트너 솔루션 모니터링](security-center-partner-solutions.md) Toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure Security Center FAQ](security-center-faq.md) Hello 서비스를 사용 하는 방법에 대 한 질문과 대답 toofrequently를 가져옵니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.
