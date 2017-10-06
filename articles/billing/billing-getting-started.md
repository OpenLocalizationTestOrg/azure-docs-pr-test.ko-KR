---
title: "aaaPrevent 예상치 못한 비용 청구-Azure 관리 | Microsoft Docs"
description: "자세한 내용은 방법 tooavoid, Azure 청구서에 예기치 않은 요금입니다. Microsoft Azure 구독에 대한 비용 추적 및 관리 기능을 사용합니다."
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.assetid: 482191ac-147e-4eb6-9655-c40c13846672
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/10/2017
ms.author: tonguyen
experimental_id: a2b2579c-cd2e-41
ms.openlocfilehash: 4827c65a55fe953c329ab26cc4e882266073c60a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prevent-unexpected-costs-with-azure-billing-and-cost-management"></a>Azure 청구 및 비용 관리를 사용하여 예상치 못한 비용 방지

Azure에 등록할 때 몇 가지 방법으로 사용자 지출 잘 알 tooget를 수행할 수 있습니다. Hello에 [Azure 포털](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)hello 구독을 선택 하는 경우 현재 비용 분석을 사용 하 여 확인 하 고 진행 속도 수 있습니다. [과거 송장 및 자세한 사용 현황 파일도 다운로드](billing-download-azure-invoice-daily-usage-date.md)할 수 있습니다. 서로 다른 프로젝트 또는 팀에 사용 되는 리소스에 대 한 toogroup 비용을 원하는 경우 확인 [리소스 태그 지정](../azure-resource-manager/resource-group-using-tags.md)합니다. 조직에 toouse 선호 하는 보고 시스템을 체크 아웃 hello [Api 청구](billing-usage-rate-card-overview.md)합니다. 

일간 사용 현황에 대한 자세한 내용은 [Microsoft Azure 청구서 이해](billing-understand-your-bill.md)를 참조하세요.

EA (기업 계약), 클라우드 솔루션 공급자 (CSP) 또는 Azure 스폰서쉽을 통해 구독이 있는 경우이 문서에 많은 기능 tooyou를 적용 하지 않습니다. 대신 비용 관리에 사용할 수 있는 다른 도구 집합이 있습니다. See [EA, CSP 및 스폰서쉽에 대한 추가 리소스](#other-offers)를 참조하세요.

가입 되어 무료 평가판을 [Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)열기 (AIO) 또는 BizSpark, Azure, 다음에 대 한 자세한 내용은 [지출 한도](#spending-limit) tooavoid unexpectantly 사용 하지 않도록 설정 하 여 구독 합니다. 

## <a name="day-0-before-you-add-azure-services"></a>0일차: Azure 서비스를 추가하기 전에

### <a name="estimate-cost-online-using-hello-pricing-calculator"></a>예상 비용 온라인 hello 가격 계산기를 사용 하 여

체크 아웃 hello [가격 계산기](https://azure.microsoft.com/pricing/calculator/) 및 [총 비용 소유권 계산기의](https://aka.ms/azure-tco-calculator) tooget에 관심이 hello 서비스는 예상 hello 월별 비용입니다. 예를 들어 A1 Windows 가상 컴퓨터 (VM)은 예상된 toocost hello 전체 시간에 실행 파일을 그대로 둘 경우 $66.96 USD/월에 시간 계산입니다.

![Hello 가격 계산기 A1 Windows VM 매달 예상된 toocost $66.96 USD 임을 보여 주는 스크린샷](./media/billing-getting-started/pricing-calcVM.png)

자세한 내용은 [가격 책정 FAQ](https://azure.microsoft.com/pricing/faq/)를 참조하세요. 또는 tootalk tooa 사람 1-800-867-1389를 호출 합니다.

### <a name="check-your-subscription-and-access"></a>구독 및 액세스 권한 확인

보기 비용 필요 [구독 액세스 toobilling 정보](billing-manage-access.md), 계정 관리자만 hello hello에 액세스할 수 있지만 [r e 계정 센터](https://account.windowsazure.com/Home/Index), 대금 청구 정보를 변경 하 고 구독을 관리 합니다. admin 님 안녕하세요 계정은 hello 등록 프로세스 진행 hello 사람입니다. 자세한 내용은 참조 [hello 구독 또는 서비스를 관리 하는 Azure 관리자 역할을 추가 또는 변경](billing-add-change-azure-subscription-administrator.md)합니다.

toosee 계정 관리자 hello 하는 경우 이동 toohello [hello Azure 포털에서에서 구독 블레이드](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) hello 목록에 액세스할 수 있는 구독을 확인 합니다. **내 역할** 아래에서 확인합니다. *계정 관리자*가 표시되면 문제가 없는 것입니다. *소유자* 등이 표시되면 모든 권한이 있는 것은 아닙니다.

![Hello hello Azure 포털에서에서 구독 보기의에서 사용자 역할의 스크린 샷](./media/billing-getting-started/sub-blade-view.PNG)

계정 관리자 hello 하지 하는 경우 다른 사람이 아마도 제공한 통해 부분적인 액세스 권한을 [Azure Active Directory 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md) (RBAC). toomanage 구독 및 청구 정보를 변경 [계정 admin 님 안녕하세요 찾을](billing-subscription-transfer.md#whoisaa) tooperform hello 작업을 요청 하십시오 또는 [hello 구독 tooyou 전송](billing-subscription-transfer.md)합니다.

계정 관리자는 더 이상 사용자의 조직과 toomanage 요금 청구서 주소, 필요한 경우 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)합니다. 

### <a name="spending-limit"></a> 지출 한도가 설정되어 있는지 확인

크레딧을 사용 하는 구독을 사용 하는 경우 다음 hello 지출 한도 대해 켜져 있습니다 기본적으로 합니다. 이러한 방식으로 모든 크레딧을 지출하면 신용 카드에 요금이 청구되지 않습니다. Hello 참조 [전체 목록은 Azure 혜택 및 지출 한도의 가용성을 hello](https://azure.microsoft.com/support/legal/offer-details/)합니다.

그러나 지출 한도에 도달하면 서비스는 사용되지 않도록 설정됩니다. 즉, VM이 할당 취소됩니다. tooavoid 서비스 가동 중지 시간이 꺼야 hello 지출 한도입니다. 초과분이 파일의 신용 카드에 부과됩니다. 

하 한 (를) 가져왔습니다 지출 한도를 경우 toosee 이동 toohello [구독 보기는 hello r e 계정 센터에서에서](https://account.windowsazure.com/Subscriptions)합니다. 지출 한도가 켜져 있으면 배너가 표시됩니다.

![지출 한도 hello r e 계정 센터에 있는 것에 대 한 경고를 보여 주는 스크린샷](./media/billing-getting-started/spending-limit-banner.PNG)

Hello 배너를 클릭 하 고 프롬프트 tooremove hello 지출 한도 수행 합니다. 등록할 때 신용 카드 정보를 입력 하지 않은 tooremove hello 지출 한도 입력 해야 합니다. 자세한 내용은 참조 [Azure 지출 한도-작동 방식과 tooenable 제거](https://azure.microsoft.com/pricing/spending-limits/)합니다.

### <a name="set-up-billing-alerts"></a>청구 경고 설정

청구 경고 설정 tooget 전자 메일 사용 비용 지정 하는 금액을 초과 하는 경우. 월별 크레딧이 있는 경우 지정된 금액을 다 사용하는 경우에 대해 경고를 설정합니다. 자세한 내용은 [Microsoft Azure 구독에 대한 청구 경고 설정](billing-set-up-alerts.md)을 참조하세요.

![청구 경고 전자 메일 스크린 샷](./media/billing-getting-started/billing-alert.png)

> [!NOTE]
> 이 기능은 미리 보기 상태이므로 정기적으로 사용 현황을 확인해야 합니다.

Toouse hello hello 첫 번째 경고에 대 한 지침으로 가격 계산기에서에서 예상 비용을 할 수 있습니다.

### <a name="understand-limits-and-quotas-for-your-subscription"></a>구독에 대한 한도 및 할당량 이해

Hello CPU 코어 수와 IP 주소 등을 위한 tooeach 구독은 기본 제한. 이러한 한도에 주의해야 합니다. 자세한 내용은 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)을 참조하세요. 증가 tooyour 제한 또는 할당량을 요청할 수 [지원 팀에 연락](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)합니다.

## <a name="day-1-as-you-add-services"></a>1일차: 서비스 추가 시

### <a name="review-hello-estimated-cost-in-hello-portal"></a>검토 hello 예상 비용 hello 포털에서

일반적으로 hello Azure 포털에서에서 서비스를 추가 하면 매달 유사한 예상된 비용을 표시 하는 보기는 합니다. 예를 들어 Windows VM의 hello 크기를 선택 하면 hello hello 계산 시간에 대 한 월별 비용을 예상 표시:

![예: A1 Windows VM은 매달 예상된 toocost $66.96 USD](./media/billing-getting-started/vm-size-cost.PNG)

### <a name="tags"></a>태그 tooyour 리소스 toogroup 청구 데이터 추가

지원 되는 서비스에 대 한 태그 toogroup 청구 데이터를 사용할 수 있습니다. 예를 들어 서로 다른 팀에 대 한 여러 Vm을 실행 하는 경우 태그 toocategorize 비용 비용 센터 (마케팅, 재무 HR) 또는 (프로덕션, 사전 프로덕션 테스트) 환경에서 사용할 수 있습니다. 

![Hello 포털에 태그를 설정을 보여 주는 스크린샷](./media/billing-getting-started/tags.PNG)

hello 태그가 서로 다른 비용이 보고 보기에서 표시 합니다. 예를 들어 지금 바로 [비용 분석 보기](#costs)에 표시되거나 첫 번째 청구 기간 후에 [상세 사용 현황 .csv](#invoice-and-usage)에 표시됩니다.

자세한 내용은 참조 [를 사용 하 여 Azure 리소스를 tooorganize 태그](../azure-resource-manager/resource-group-using-tags.md)합니다.

### <a name="consider-enabling-cost-cutting-features-like-auto-shutdown-for-vms"></a>VM에 대한 자동 종료와 같은 비용 절감에 기능 사용 고려

시나리오에 따라 hello Azure 포털에서에서 Vm에 대 한 자동 종료를 구성할 수 있습니다. 자세한 내용은 [Azure Resource Manager를 사용한 VM에 대한 자동 종료](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/)를 참조하세요.

![Hello 포털에서 자동 종료 옵션의 스크린 샷](./media/billing-getting-started/auto-shutdown.PNG)

자동 종료 내에서 종료 하면 VM 전원 옵션으로 hello와 같을 hello 되지 않습니다. 자동 종료 중지 하 고 자세한 사용 요금 Vm toostop 할당을 취소 합니다. 자세한 내용은 VM 상태에 대한 [Linux VM](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) 및 [Windows VM](https://azure.microsoft.com/pricing/details/virtual-machines/windows/)의 가격 책정 FAQ를 참조하세요.

개발 및 테스트 환경에 대한 추가 비용 절감에 기능에 대해서는 [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab/)를 확인하세요.

## <a name="cost-reporting"></a> 2일차 이후: 서비스를 사용한 후 사용 현황 보기

### <a name="costs"></a>정기적으로 hello 비용 분석 포털에서 확인 및 진행 속도

서비스가 실행 중일 때 부과되는 요금을 정기적으로 확인합니다. Hello 현재 볼 수 있습니다 지출 및 Azure 포털에서 진행 되는 속도입니다. 

1. Hello 방문 [Azure 포털에서 구독 블레이드](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)합니다.

2. Toosee 원하는 구독을 선택 합니다. 하나의 tooselect만 있을 수 있습니다.

3. Hello 비용 분석 결과 볼 하 고 hello 팝업 블레이드에서 진행 속도 해야 합니다. (Hello 맨 위 근처에 경고가 표시는) 자신의 구독에 지원 되지 않을 수 있습니다. 데이터 toopopulate hello에 대 한 서비스를 추가한 후 24 시간 동안 기다립니다.
    
    ![진행 속도 및 hello Azure 포털에서에서 분할의 스크린 샷](./media/billing-getting-started/burn-rate.PNG)

4. Toopin hello view tooyour 대시보드를 할 수 있습니다.

    ![보기 toohello 대시보드에 고정 스크린 샷](./media/billing-getting-started/pin.PNG)

5. 클릭 **비용 분석** hello 목록 toohello 왼쪽된 toosee hello 비용 별로 분석 리소스에에서 있습니다.

    ![Azure 포털에서 hello 비용 분석 보기의 스크린샷](./media/billing-getting-started/cost-analysis.PNG)

6. [태그](#tags), 리소스 그룹 및 시간 간격 등의 다양한 속성별로 필터링할 수 있습니다. 클릭 **적용** tooconfirm hello 필터 및 **다운로드** tooexport hello tooa 쉼표로 구분 된 값 (.csv) 파일 보기.

7. 자원을 toosee 지출 기록과 얼마나 것 된 비용 계산 하면 각 날짜입니다.

    ![Hello 스크린샷 지출 Azure 포털에서 기록 보기](./media/billing-getting-started/costhistory.PNG)

Hello 비용 hello 예상치 hello 서비스 선택한 때 참조를 확인 하는 것이 좋습니다. Hello 비용 예측에서 크게 다른 경우 리소스에 대해 선택한 계획 (A1 vs A0 VM 예를 들어) 가격 hello를 다시 확인 합니다. 

#### <a name="view-costs-for-all-your-subscriptions-in-hello-billing-blade"></a>결제 블레이드 hello에서에서 모든 구독에 대 한 비용 보기

Hello에서 모든 구독에 대 한 hello 집계 청구 금액 및 분석 계정 관리자 hello 처럼 여러 구독을 관리 하는 경우 볼 수 있습니다 [결제 블레이드](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade)합니다. 

<!-- Add screenshots of multiple subs each with billed usage -->

### <a name="turn-on-and-check-out-azure-advisor-recommendations"></a>Azure Advisor 권장 지침 설정 및 확인

[Azure Advisor](../advisor/advisor-overview.md)는 사용량이 낮은 리소스를 식별하여 비용을 절감하는 데 도움을 주는 미리 보기 기능입니다. 켜십시오 hello Azure 포털에서:

![Azure Portal의 Azure Advisor 단추 스크린 샷](./media/billing-getting-started/advisor-button.PNG)

그런 다음 권장 hello에 볼 수 있습니다 **비용** hello 관리자 대시보드 탭:

![Advisor cost 권장 지침 예제 스크린 샷](./media/billing-getting-started/advisor-action.PNG)

자세한 내용은 [Advisor 비용 권장 사항](../advisor/advisor-cost-recommendations.md)을 참조하세요.

### <a name="invoice-and-usage"></a> 첫 번째 청구 기간 후 청구서 및 세부 사용 현황 받기

첫 번째 청구 기간이 지난 후 Portable Document Format(.pdf) 송장 및 쉼표로 구분된 값(.csv) 사용 현황 세부 정보를 다운로드할 수 있습니다. 또한에 선택할 수 있습니다 toohave 청구서 tooyou 전자 메일로 전송 합니다. 이러한 파일 궁극적으로 청구 tooyou 세금, 할인 및 크레딧 후 이란 toounderstand 데 도움이 됩니다. 지불 연결 된 메서드 tooyour 구독을 보유 하지 않은 이러한 파일을 사용할 수 없습니다. 자세한 내용은 참조 [어떻게 tooget 프로그램 Azure 청구 청구서 및 일일 사용량 데이터](billing-download-azure-invoice-daily-usage-date.md) 및 [Microsoft azure 청구서 이해](billing-understand-your-bill.md)합니다.

![.pdf 송장 스크린 샷](./media/billing-getting-started/invoice.png)

이전에 설정 하는 hello 태그가 hello 세부 사용 현황.csv 파일에 표시 합니다.

![Hello 사용.csv에 태그를 보여 주는 스크린샷](./media/billing-getting-started/csv.png)

### <a name="billing-api"></a>청구 API

청구 API tooprogrammatically get 사용 현황 데이터를 사용 합니다. Hello RateCard API 및 hello 사용량 API 함께 tooget 청구 사용량을 사용 합니다. 자세한 내용은 [Microsoft Azure 리소스 소비에 대한 통찰력 얻기](billing-usage-rate-card-overview.md)를 참조하세요.

## <a name="other-offers"></a> EA, CSP 및 스폰서쉽에 대한 추가 리소스

Tooyour 계정 관리자 또는 Azure 파트너 tooget 시작에 게 문의 하십시오.

| 제안 | 리소스 |
|-------------------------------|-----------------------------------------------------------------------------------|
| EA(기업 계약) | [EA 포털](https://ea.azure.com/), [도움말 문서](https://ea.azure.com/helpdocs) 및 [Power BI 보고서](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-enterprise/) |
| CSP(클라우드 솔루션 공급자) | Tooyour 공급자와 통신 |
| Azure 스폰서쉽 | [스폰서쉽 포털](https://www.microsoftazuresponsorships.com/) |

관리 하는 경우 IT 읽기 대규모 조직에 대 한 권장 [Azure enterprise 스 캐 폴드](../azure-resource-manager/resource-manager-subscription-governance.md) 및 hello [엔터프라이즈 IT 백서](http://download.microsoft.com/download/F/F/F/FFF60E6C-DBA1-4214-BEFD-3130C340B138/Azure_Onboarding_Guide_for_IT_Organizations_EN_US.pdf) (.pdf 다운로드를 영어로 제공).

## <a name="need-help-contact-support"></a>도움이 필요하세요? 지원에 문의

도움이 필요 하면 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget 문제가 해결 신속 하 게 합니다.
