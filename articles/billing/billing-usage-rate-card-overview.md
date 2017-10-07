---
title: "청구 Api aaaAzure | Microsoft Docs"
description: "Azure 리소스 소비 및 추세에 대 한 tooprovide 사용 되는 정보는 Azure 청구 사용량 및 RateCard Api에 알아봅니다."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/18/2017
ms.author: mobandyo;bryanla
ms.openlocfilehash: b3214996cc3279f76fdc7f0dbd2059c3ae7bb15c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-billing-apis-tooprogrammatically-get-insight-into-your-azure-usage"></a>사용 하 여 Azure 청구 Api tooprogrammatically 있고 Azure 사용에 대 한 정보 가져오기
Azure 청구 Api toopull 사용 및 리소스 데이터를 사용 하 여 기본 설정된 된 데이터 분석 도구입니다. hello Azure 리소스 사용량 및 RateCard Api 유용 정확 하 게 예상 하 고 비용을 관리 합니다. 리소스 공급자와 hello 제품군 hello Azure 리소스 관리자에 의해 노출 되는 Api의 일부 hello Api 구현 됩니다.  

## <a name="azure-invoice-download-api-preview"></a>Azure 청구서 다운로드 API(미리 보기)
한 번 hello [옵트인 된 전체](billing-manage-access.md#opt-in), 미리 보기 버전의 hello를 사용 하 여 다운로드 송장 [송장 API](/rest/api/billing)합니다. hello 기능은 다음과 같습니다.

* **Azure 역할 기반 액세스 제어** -액세스 구성 hello에 정책을 [Azure 포털](https://portal.azure.com) 또는 [Azure PowerShell cmdlet](/powershell/azure/overview) toospecify 있는 사용자 또는 응용 프로그램 액세스 권한을 얻을 수 toohello 구독 사용 현황 데이터입니다. 호출자가 인증에 대한 표준 Azure Active Directory 토큰을 사용해야 합니다. Hello 호출자 tooeither hello 판독기 대금 청구, 판독기, 소유자 또는 참가자 역할 tooget 액세스 toohello 사용 현황 데이터는 특정 Azure 구독에 대 한 추가 합니다.
* **필터링 날짜** -사용 하 여 hello `$filter` 매개 변수 tooget hello 하 여 시간 순서 대로 모든 hello 송장 송장 기간 종료 날짜입니다. 

> [!NOTE]
> 이 기능은 미리 보기의 첫 번째 버전 중 이며 제목 toobackward-호환 되지 않는 변경 될 수 있습니다. 현재 특정 구독 제품(EA, CSP, AIO는 지원되지 않음) 및 Azure Germany에서 사용할 수 없습니다.

## <a name="azure-resource-usage-api-preview"></a>Azure 리소스 사용량 API(미리 보기)
사용 하 여 hello Azure [리소스 사용량 API](https://msdn.microsoft.com/library/azure/mt219003) tooget 예상된 Azure 사용량 데이터입니다. hello API에는 다음이 포함 됩니다.

* **Azure 역할 기반 액세스 제어** -액세스 구성 hello에 정책을 [Azure 포털](https://portal.azure.com) 또는 [Azure PowerShell cmdlet](/powershell/azure/overview) toospecify 있는 사용자 또는 응용 프로그램 액세스 권한을 얻을 수 toohello 구독 사용 현황 데이터입니다. 호출자가 인증에 대한 표준 Azure Active Directory 토큰을 사용해야 합니다. Hello 호출자 tooeither hello 판독기 대금 청구, 판독기, 소유자 또는 참가자 역할 tooget 액세스 toohello 사용 현황 데이터는 특정 Azure 구독에 대 한 추가 합니다.
* **매시간 또는 매일 집계** -호출자는 Azure 사용 데이터를 매시간 버킷 또는 매일 버킷으로 할지 지정할 수 있습니다. hello 기본값은 매일입니다.
* **(리소스 태그가 포함)의 인스턴스 메타 데이터** – 정규화 된 리소스 uri hello와 같은 인스턴스 수준의 세부 사항을 가져옵니다 (/subscriptions/ {구독 id} /..), 리소스 그룹 정보 및 리소스 태그 hello 합니다. 이 메타 데이터를 사용 하면 명확 하 게 하 고 프로그래밍 방식으로 hello 태그로 간 충전 같은 사용 사례에 대 한 사용을 할당 합니다.
* **리소스 메타 데이터** -hello 미터 이름, 측정기 범주, 측정기 하위 범주, 단위, 지역 등 리소스 정보를 사용 된 작업의 hello 호출자에 게 제공 합니다. 또한 tooalign 리소스 메타 데이터 용어 hello Azure 포털, Azure 사용량 CSV, EA CSV, 청구 및 기타 공용 환경, 환경에서 데이터를 상관 성을 toolet 걸친 협력 합니다.
* **모든 사용 유형에 대한 사용** – 종량제, MSDN, 약정 금액, 금액 크레딧 및 EA와 같은 모든 사용 유형에 대한 사용 데이터가 제공됩니다.

## <a name="azure-resource-ratecard-api-preview"></a>Azure 리소스 RateCard API(미리 보기)
사용 하 여 hello [Azure 리소스 RateCard API](https://msdn.microsoft.com/library/azure/mt219005) tooget hello 목록을 사용할 수 있는 Azure 리소스와 각각에 대 한 예상된 가격 정보. hello API에는 다음이 포함 됩니다.

* **Azure 역할 기반 액세스 제어** -hello에 대 한 액세스 정책 구성 [Azure 포털](https://portal.azure.com) 또는 [Azure PowerShell cmdlet](/powershell/azure/overview) toospecify 있는 사용자 또는 응용 프로그램 액세스 권한을 얻을 수 toohello RateCard 데이터입니다. 호출자가 인증에 대한 표준 Azure Active Directory 토큰을 사용해야 합니다. Hello 호출자 tooeither hello 판독기, 소유자 또는 참가자 역할 tooget 액세스 toohello 사용 현황 데이터는 특정 Azure 구독에 대 한 추가 합니다.
* **종량제, MSDN, 금액 약정 및 금액 크레딧 제공(EA은 지원되지 않음)** - 이 API는 Azure 제공 수준 환율 정보를 제공합니다.  이 API의 hello 호출자 hello 제공 tooget 리소스 세부 정보 및 속도 전달 해야 합니다. 여러분 EA 제안 등록 당 속도 사용자 지정한 때문에 현재 없습니다 tooprovide EA 세요. 

## <a name="scenarios"></a>시나리오
다음은 몇 가지 가능한 hello 사용량 및 RateCard Api hello hello 조합 하 여 적용 된 hello 시나리오입니다.

* **Hello (월) 동안 azure 지출** -hello 사용량 및 RateCard Api tooget 통찰력에 클라우드로의 hello 조합을 사용 하 여 hello (월) 동안 소비 합니다. 일별 사용 현황 및 요금 청구 버킷 예상 및 매시간 hello를 분석할 수 있습니다.
* **경고를 설정** – hello 사용을 사용 하 고 hello RateCard Api tooget 클라우드 사용 및 요금, 예상 리소스 또는 통화 기반 경고를 설정 합니다.
* **청구서 예측** – Get 예상된 소비와 클라우드를 보내며 기계 학습 알고리즘 toopredict 어떤 hello bill 청구 주기 hello hello 끝에 있는 것을 적용 합니다.
* **사전 소비 비용 분석** – hello RateCard API toopredict 작업 tooAzure 이동할 때 예상 되는 용도 대 한 청구 금액이 것을 사용 합니다. 기존 작업에서 다른 클라우드 또는 사설 클라우드를 설정한 경우 Azure의 보다 정확한 예상치 지출 hello Azure 속도 tooget와 사용량을 매핑할 수도 있습니다. 제안 및 비교 및 대비 종 량 제, 초과 hello 각 제안 유형에 사이 기능 toopivot hello이 예상 값 제공 현금 약정 및 화폐 성 차변을 같은입니다. 또한 제공 hello API hello 기능 toosee 비용 차이 지역별 및 toodo 배포 결정을 내린 가상 비용 분석 toohelp 있습니다.
* **가상 분석** -
  
  * 다른 지역에 또는 hello Azure 리소스의 다른 구성에 더 많은 비용 효율적인 toorun 작업 인지를 확인할 수 있습니다. 사용 중인 Azure 지역 hello에 기반 azure 리소스 비용 다를 수 있습니다.
  * 다른 Azure 제품 유형에서 Azure 리소스에 더 나은 속도를 제공하는지 결정할 수도 있습니다.
  
## <a name="partner-solutions"></a>파트너 솔루션
[Microsoft Azure 사용량 및 RateCard Api를 사용 하도록 설정 Cloudyn tooProvide 고객에 대 한 ITFM](billing-usage-rate-card-partner-solution-cloudyn.md) Azure 청구 API 파트너에서 제공 하는 hello 통합 환경에 설명 [Cloudyn](https://www.cloudyn.com/microsoft-azure/)합니다. 이 문서 경험에 대 한 고 Cloudyn를 사용 하 여 hello Azure 청구 Api tooget 데이터 로부터 이해를 Azure 소비 하는 방법을 보여 주는 비디오를 포함 합니다.

[클라우드 크루저 및 Microsoft Azure 청구 API 통합](billing-usage-rate-card-partner-solution-cloudcruiser.md) 설명 방법을 [Azure 팩용 클라우드 크루저 Express](http://www.cloudcruiser.com/partners/microsoft/) hello Windows Azure 팩 WAP () 포털에서 직접 작동 합니다. 단일 사용자 인터페이스에서 원활 하 게 hello Microsoft Azure 개인 또는 호스 티 드 공용 클라우드 둘 다 hello operational 및 금융 측면을 관리할 수 있습니다.   

## <a name="next-steps"></a>다음 단계
* GitHub의 코드 샘플 hello 확인해 보세요.
  * [청구서 API 코드 샘플](https://go.microsoft.com/fwlink/?linkid=845124)

  * [사용량 API 코드 샘플](https://github.com/Azure-Samples/billing-dotnet-usage-api)

  * [RateCard API 코드 샘플](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)

* toolearn hello Azure 리소스 관리자에 대 한 자세한 참조 [Azure 리소스 관리자 개요](../azure-resource-manager/resource-group-overview.md)합니다. 

* 클라우드의 파악할 수 필요한 toohelp 지출 도구의 hello suite에 자세한 내용은 참조 hello Gartner 문서 [IT 재무 관리 (ITFM) 도구에 대 한 시장 가이드](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb)합니다.

