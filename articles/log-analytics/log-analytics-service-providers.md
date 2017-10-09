---
title: "서비스 공급자의 분석 기능 aaaLog | Microsoft Docs"
description: "Log Analytics는 MSP(Managed Service Providers), 대기업, ISV(Independent Software Vendor)를 지원하며 호스팅 서비스 공급자가 고객의 온-프레미스 또는 클라우드 인프라에서 서버를 관리하고 모니터링할 수 있도록 합니다."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: c07f0b9f-ec37-480d-91ec-d9bcf6786464
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: richrund
ms.openlocfilehash: 3c0a93232293f90385c6c724be436cee1cf855f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-features-for-service-providers"></a>서비스 공급자에 대한 Log Analytics 기능
Log Analytics는 MSP(Managed Service Providers), 대기업, ISV(Independent Software Vendor)를 지원하며 호스팅 서비스 공급자가 고객의 온-프레미스 또는 클라우드 인프라에서 서버를 관리하고 모니터링할 수 있도록 합니다. 

대기업은 서비스 공급자와 많은 유사성을 공유하는데, 특히 중앙 IT 팀이 다양한 사업부의 IT 관리를 담당한다는 점이 그렇습니다. 간단한 설명을 위해이 문서에서는 hello 용어 *서비스 공급자* hello 동일한 기능 뿐만 아니라 다른 고객과 기업에 사용할 수 있습니다.

## <a name="cloud-solution-provider"></a>클라우드 솔루션 공급자
파트너 및 hello의 일부인 서비스 공급자에 대 한 [클라우드 솔루션 공급자 (CSP)](https://partner.microsoft.com/Solutions/cloud-reseller-overview) 프로그램, 로그 분석 CSP 구독에서 사용할 수 있는 Azure 서비스는 hello 중 하나입니다. 

사용할 수 있는 기능을 수행 하는 hello 로그 분석에 대 한 *클라우드 솔루션 공급자* 구독 합니다.

*CSP(클라우드 솔루션 공급자)*는 다음을 수행할 수 있습니다.

* 테넌트(고객) 구독에 Log Analytics 작업 영역을 만듭니다.
* 테넌트에서 만든 작업 영역에 액세스합니다. 
* 추가 하 고 Azure 사용자 관리를 사용 하 여 사용자 액세스 toohello 작업을 제거 합니다. Hello OMS의에서 테 넌 트의 작업 영역에서 포털 hello 사용자 관리 페이지의 설정에서 사용할 수 없는 경우
  * 역할 기반 액세스 아직-사용자 지정 로그 분석 지원 하지 않습니다 `reader` hello Azure 포털에에서는 권한이 있도록 toomake 구성 변경 내용을 hello OMS 포털에서

tooa 테 넌 트의 구독에서 toolog, toospecify hello 테 넌 트 식별자가 필요합니다. hello 테 넌 트 식별자는 마지막 부분의에 hello 전자 메일 주소 사용 toosign 경우가 많습니다.

* Hello OMS 포털에서 추가 `?tenant=contoso.com` hello 포털에 대 한 hello url입니다. 예를 들어 `mms.microsoft.com/?tenant=contoso.com`
* PowerShell에서 hello를 사용 하 여 `-Tenant contoso.com` 매개 변수를 사용 하는 경우 `Add-AzureRmAccount` cmdlet
* hello 테 넌 트 식별자는 hello를 사용 하는 경우에 자동으로 추가 됩니다 `OMS portal` hello Azure 포털 tooopen에서에서에 연결 하 고 선택한 hello 작업 영역에 대 한 toohello OMS 포털에 로그인

CSP(클라우드 솔루션 공급자)의 *고객*은 다음을 수행할 수 있습니다.

* CSP 구독에서 Log Analytics 작업 영역 만들기
* Hello CSP 만든 액세스 작업 영역
  * 사용 하 여 hello `OMS portal` hello Azure 포털 tooopen에서에서에 연결 하 고 선택한 hello 작업 영역에 대 한 toohello OMS 포털에 로그인
* 보기 및 hello OMS 포털에서 설정 되는 hello 사용자 관리 페이지를 사용 합니다.

> [!NOTE]
> hello 포함 백업 및 로그 분석에 대 한 사이트 복구 솔루션은 수 tooconnect tooa 복구 서비스 자격 증명 모음 CSP 구독에서 구성할 수 없습니다. 
> 
> 

## <a name="managing-multiple-customers-using-log-analytics"></a>Log Analytics를 사용하여 여러 고객 관리
관리하는 고객마다 Log Analytics 작업 영역을 만드는 것이 좋습니다. Log Analytics 작업 영역이 제공하는 정보:

* 저장 된 데이터 toobe에 대 한 지리적 위치입니다. 
* 대금 청구에 대한 세분성 
* 데이터 격리 
* 고유한 구성

고객당 작업 영역을 만들면 수 tookeep 각 고객의 데이터를 별도 하는 또한 각 고객의 hello 사용을 추적 합니다.

시기 및 이유 toocreate 여러 작업 영역에서 설명 하는 대 한 자세한 내용은 [액세스 toolog 분석 관리](log-analytics-manage-access.md#determine-the-number-of-workspaces-you-need)합니다.

고객 작업의 생성 및 구성을 사용 하 여 자동화할 수 [PowerShell](log-analytics-powershell-workspace-configuration.md), [리소스 관리자 템플릿을](log-analytics-template-workspace-configuration.md), 또는 hello를 사용 하 여 [REST API](https://www.nuget.org/packages/Microsoft.Azure.Management.OperationalInsights/)합니다.

hello 템플릿 사용 하 여 리소스 관리자 작업 영역 구성에 대 한 사용된 toocreate 하 고 작업 영역을 구성할 수 있는 마스터 구성 toohave가 있습니다. 작업 영역에 대해 만들어지는 고객은 자동으로 구성 tooyour 요구 사항을 확신할 수 있습니다. 요구 사항 업데이트 하면 hello 템플릿을 업데이트 되 고 hello 기존 작업 영역 다시 적용 합니다. 이 프로세스는 기존 작업 영역이 새로운 표준을 충족하는지도 확인합니다.    

여러 개의 로그 분석 작업 영역을 관리 하는 경우 각 작업 영역의 기존 발권 시스템 통합는 것이 좋습니다  ¼ ײ hello를 사용 하 여 / [경고](log-analytics-alerts.md) 기능입니다. 기존 시스템에 통합 하 여 친숙 한 프로세스 지원부 toofollow 계속할 수 있습니다. 정기적으로 로그 분석은 사용자가 지정한 hello 경고 조건에 대 한 각 작업 영역을 확인 하 고 조치도 필요 하지 않으면 경고를 생성 합니다.

데이터의 개인 설정 된 보기에 대 한 hello를 사용 하 여 [대시보드](../azure-portal/azure-portal-dashboards.md) hello Azure 포털의에서 기능입니다.  

Executive 수준에 대 한 보고서 작업 영역에서는 전체에서 데이터를 요약 하는 로그 분석 간의 통합 hello 및 [PowerBI](log-analytics-powerbi.md)합니다. 보고 하는 다른 시스템과 toointegrate 해야 할 경우 hello 검색 API를 사용할 수 있습니다 (PowerShell을 통해 또는 [REST](log-analytics-log-search-api.md)) toorun 쿼리 및 내보내기에 대 한 검색 결과.

## <a name="next-steps"></a>다음 단계
* [Resource Manager 템플릿](log-analytics-template-workspace-configuration.md)을 사용하여 작업 영역 생성 및 구성 자동화
* [PowerShell](log-analytics-powershell-workspace-configuration.md)을 사용하여 작업 영역 생성 자동화 
* 사용 하 여 [경고](log-analytics-alerts.md) 기존 시스템과 toointegrate
* [PowerBI](log-analytics-powerbi.md)를 사용하여 요약 보고서 생성

