---
title: "Azure 리소스를 SIEM 시스템으로의 aaaIntegrate 로그 | Microsoft Docs"
description: "Azure 로그 통합, 주요 기능 및 작동 원리에 대해 알아봅니다."
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: 9c1346e1-baf8-4975-b2f2-42ae05b2dc0a
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/10/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: 4a59ce625702e5266a7c8eb020473cfeaf6b1964
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toomicrosoft-azure-log-integration"></a>소개 tooMicrosoft Azure 로그 통합
Azure 로그 통합, 주요 기능 및 작동 원리에 대해 알아봅니다.

## <a name="overview"></a>개요

Azure 로그 통합은 사용 가능한 솔루션 tooyour 온-프레미스 보안 정보 및 이벤트 관리 SIEM () 시스템에서 toointegrate 원시 로그 Azure 리소스를 사용 하면입니다.

Azure 로그 통합은 Azure 리소스에서 Windows 이벤트 뷰어 로그, [Azure 활동 로그](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md), [Azure Security Center 경고](../security-center/security-center-intro.md) 및 [Azure 진단 로그](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)로부터 Windows 이벤트를 수집합니다. 이 통합의 모든 자산에 대 한 통합 된 대시보드 제공 SIEM 솔루션을 사용 하면, 온-프레미스 또는 hello 클라우드에서 집계할 수 있도록 상관 관계를 설정, 분석 및 보안 이벤트에 대 한 경고입니다.

>[!NOTE]
이번에 지원 hello 클라우드는 상용 Azure 및 Azure Government입니다. 다른 클라우드는 지원되지 않습니다.

![Azure 로그 통합][1]

## <a name="what-logs-can-i-integrate"></a>어떤 로그와 통합할 수 있나요?
Azure에서는 모든 Azure 서비스에 대해 광범위한 로깅을 생성합니다. 이러한 로그는 세 가지 유형의 로그를 나타냅니다.

* **컨트롤/관리 로그** hello에 대 한 가시성을 제공 [Azure 리소스 관리자](../azure-resource-manager/resource-group-overview.md) 만들기, 업데이트 및 삭제 작업입니다. Azure 활동 로그가 이 로그 유형에 속합니다.
* **데이터 로그를 평면** hello Azure 리소스 사용의 일부로 발생 하는 hello 이벤트에 대 한 가시성을 제공 합니다. 이 유형의 로그의 예는 hello Windows 이벤트 뷰어 **시스템**, **보안**, 및 **응용 프로그램** Windows 가상 컴퓨터에 대 한 채널입니다. 또 다른 예는 Azure Monitor를 통해 구성된 진단 로깅입니다.
* **처리된 이벤트**는 사용자 대신 처리된 경고 정보 및 분석된 이벤트를 제공합니다. 이 유형의 이벤트의 예로 Azure 보안 센터 경고, Azure 보안 센터에 처리 하 고 구독 tooprovide 경고 관련 tooyour 현재 보안 상태를 분석 합니다.

Azure 로그 통합은 ArcSight, QRadar 및 Splunk를 지원합니다. 모든 경우에 문의 하십시오 SIEM 공급 업체 tooassess 기본 커넥터 있는지. 경우에 따라 필요가 없습니다 toouse Azure 로그 통합 전용 커넥터를 사용할 수 없는 경우. 대 한 자세한 내용은 지원 되는 로그 형식 방문 하십시오 hello FAQ입니다.

>[!NOTE]
Azure 로그 통합은 사용 가능한 솔루션, hello 로그 파일 정보 저장소에서 발생 하는 Azure 저장소 비용 있습니다.

커뮤니티 지원 hello를 통해 사용할 수는 [Azure 로그 통합 MSDN 포럼](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration)합니다. hello 포럼 제공 hello AzLog 커뮤니티 hello 기능 toosupport 서로 질문, 대답, 팁 및 요령 tooget 가장 Azure 로그 통합 hello 어떻게에 합니다. 또한 hello Azure 로그 통합 팀이이 포럼을 모니터링 하 고을 활용해 서 때마다는 데 도움이 됩니다.

[지원 요청](../azure-supportability/how-to-create-azure-support-request.md)을 열 수도 있습니다. toodo이,이 선택 **로그 통합** hello 서비스 지원을 요청 합니다.

## <a name="next-steps"></a>다음 단계
이 문서에 도입 된 tooAzure 로그 통합 되었습니다. Azure에 대 한 자세한 로그 통합 및 hello 유형의 지원 되는 로그 toolearn hello 다음을 참조 합니다.

* [Microsoft Azure 로그 통합](https://www.microsoft.com/download/details.aspx?id=53324) – Azure 로그 통합에 대한 세부 정보, 시스템 요구 사항 및 설치 지침을 다운로드할 수 있습니다.
* [Azure 로그 통합 시작](security-azure-log-integration-get-started.md) - 이 자습서에서는 Azure 로그 통합을 설치하고 Azure WAD 저장소, Azure 활동 로그, Azure Security Center 경고 및 의 Azure Active Directory 감사 로그의 로그를 통합하는 방법을 안내합니다.
* [구성 단계를 파트너](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) –이 블로그 게시물을 보면 tooconfigure Azure Splunk, HP ArcSight 및 IBM QRadar 파트너 솔루션과 통합 toowork를 로그 하는 방법은 합니다. 이 블로그 hello 파트너 솔루션 구성에 현재 위치를 나타냅니다. 모든 경우에 먼저 toopartner 솔루션 설명서를 참조 하십시오.
* [Syslog tooQRadar 통한 활동과 ASC 경고](https://blogs.msdn.microsoft.com/azuresecurity/2016/09/24/integrate-azure-logs-to-qradar/) –이 블로그 게시물 설명 hello toosend 활동 및 Azure 보안 센터 경고 syslog tooQRadar 통해
* [Azure 로그 통합 FAQ(질문과 대답)](security-azure-log-integration-faq.md) - 이 FAQ는 Azure 로그 통합에 대한 질문에 답변합니다.
* [보안 센터를 통합 합니다. Azure와 경고 로그 통합](../security-center/security-center-integrating-alerts-with-log-integration.md) -이 문서에서는 Azure 로그 통합와 toosync Azure 보안 센터 경고 하는 방법입니다.

<!--Image references-->
[1]: ./media/security-azure-log-integration-overview/azure-log-integration.png
