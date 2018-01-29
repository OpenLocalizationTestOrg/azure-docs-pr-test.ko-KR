---
title: "Hyper-V에서 Azure로 Azure Site Recovery Deployment Planner | Microsoft Docs"
description: "이 문서는 Hyper-V에서 Azure로 시나리오에 대해 생성된 Azure Site Recovery Deployment Planner 보고서에 대한 분석을 설명합니다."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: garavd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/02/2017
ms.author: nisoneji
ms.openlocfilehash: 9340fe48c1da874d6c0cf02c026e5dec6ddabbe7
ms.sourcegitcommit: 357afe80eae48e14dffdd51224c863c898303449
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/15/2017
---
# <a name="analyze-the-azure-site-recovery-deployment-planner-report"></a>Azure Site Recovery Deployment Planner 보고서 분석
생성된 Microsoft Excel 보고서에는 다음과 같은 시트가 포함되어 있습니다.

## <a name="on-premises-summary"></a>온-프레미스 요약
온-프레미스 요약 워크시트에는 프로파일링된 Hyper-V 환경에 대한 개요가 제공됩니다. ![온-프레미스 요약](media/site-recovery-hyper-v-deployment-planner-analyze-report/on-premises-summary-h2a.png)

**시작 날짜** 및 **종료 날짜**: 보고서를 생성하도록 고려된 데이터 프로파일링의 시작 날짜와 종료 날짜입니다. 기본적으로 시작 날짜는 프로파일링을 시작한 날짜이고, 종료 날짜는 프로파일링을 중지한 날짜입니다. 'StartDate' 및 'EndDate' 매개 변수를 사용하여 보고서를 생성하는 경우 이는 해당 매개 변수의 값일 수 있습니다.

**총 프로파일링 일 수**: 보고서를 생성한 시작 날짜와 종료 날짜 사이에 프로파일링한 총 날짜 수입니다.

**호환되는 가상 머신 수**: 필요한 네트워크 대역폭, 필요한 저장소 계정 수, Microsoft Azure 코어가 계산되는 호환 가능한 VM의 총 수입니다.

**호환되는 모든 가상 머신의 총 디스크 수**: 호환되는 모든 VM의 총 디스크 수입니다.

**호환되는 가상 머신당 평균 디스크 수**: 호환되는 모든 VM에서 계산된 평균 디스크 수입니다.

**평균 디스크 크기(GB)**: 호환되는 모든 VM에서 계산된 평균 디스크 크기입니다.

**원하는 RPO(분)**: 기본 복구 지점 목표이거나 필요한 대역폭을 추정하기 위해 보고서 생성 시 'DesiredRPO' 매개 변수에 전달한 값입니다.

**원하는 대역폭(Mbps)**: 달성 가능한 RPO를 추정하기 위해 보고서 생성 시 'Bandwidth' 매개 변수에 대해 전달한 값입니다.

**관찰된 일반적 일일 데이터 변동량(GB)**: 모든 프로파일링 일 수 동안 관찰된 평균 데이터 변동량입니다.

## <a name="recommendations"></a>권장 사항  
Hyper-V에서 Azure로 보고서의 권장 사항 시트에는 선택된 원하는 RPO에 따라 다음과 같은 세부 정보가 포함됩니다.

![Hyper-V에서 Azure로 보고서에 대한 권장 사항](media/site-recovery-hyper-v-deployment-planner-analyze-report/Recommendations-h2a.png)

### <a name="profile-data"></a>데이터 프로파일링
![데이터 프로파일링](media/site-recovery-hyper-v-deployment-planner-analyze-report/profile-data-h2a.png)

**프로파일링된 데이터 기간**: 프로파일링이 실행된 기간입니다. 기본적으로 도구는 프로파일링된 모든 데이터를 계산에 포함합니다. 보고서 생성에 StartDate 및 EndDate 옵션을 사용하면 특정 기간에 대한 보고서를 생성합니다. 

**프로파일링된 Hyper-V 서버 수**: VM 보고서가 생성된 Hyper-V 서버 수입니다. 숫자를 클릭하면 Hyper-V 서버의 이름을 볼 수 있습니다. 모든 서버가 서버의 저장소 요구 사항과 함께 나열되어 있는 온-프레미스 저장소 요구 사항 시트가 열립니다.    

**원하는 RPO**: 배포를 위한 복구 지점 목표입니다. 기본적으로 필요한 네트워크 대역폭은 15, 30 및 60분의 RPO 값에 대해 계산됩니다. 선택에 따라 영향을 받은 값이 시트에서 업데이트됩니다. 보고서를 생성하는 동안 DesiredRPOinMin 매개 변수를 사용한 경우 이 값은 원하는 RPO 결과에 표시됩니다.

### <a name="profiling-overview"></a>프로파일링 개요
![프로파일링 개요](media/site-recovery-hyper-v-deployment-planner-analyze-report/profiling-overview-h2a.png)

**총 프로파일링된 Virtual Machines 수**는 프로파일링된 데이터를 사용할 수 있는 VM의 총 수입니다. VMListFile에 프로파일링되지 않은 VM의 이름이 있는 경우 해당 VM은 보고서 생성에서 고려되지 않고 프로파일링된 VM의 총 수에서 제외됩니다.

**호환되는 Virtual Machines 수**는 Azure Site Recovery를 사용하여 Azure에 보호할 수 있는 VM 수입니다. 필요한 네트워크 대역폭, 저장소 계정 수, Azure 코어 수가 계산되는 호환되는 VM의 총 수입니다. 모든 호환되는 VM의 세부 정보는 "호환 VM" 섹션에서 사용할 수 있습니다.

**호환되지 않는 Virtual Machines 수**는 Azure Site Recovery로 보호에 대해 호환되지 않는 프로파일링된 VM의 수입니다. 비호환성에 대한 이유는 "호환되지 않는 VM" 섹션에서 설명하고 있습니다. VMListFile에 프로파일링되지 않는 VM의 이름이 있는 경우 해당 VM은 호환되지 않는 VM 수에서 제외됩니다. 이러한 VM은 "호환되지 않는 VM" 섹션의 끝에 "데이터를 찾을 수 없음"으로 나열됩니다.

**원하는 RPO**: 원하는 복구 지점 목표(분)입니다. 세 개의 RPO 값: 15(기본값), 30 및 60분에 대해 보고서가 생성됩니다. 보고서의 대역폭 권장 사항은 시트의 오른쪽 위에 있는 원하는 RPO 드롭다운 목록의 선택에 따라 변경됩니다. 사용자 지정 값을 포함한 -DesiredRPO 매개 변수를 사용하여 보고서를 생성한 경우 이 사용자 지정 값은 원하는 RPO 드롭다운 목록에 기본값으로 표시됩니다.

### <a name="required-network-bandwidth-mbps"></a>필요한 네트워크 대역폭(Mbps)
![필요한 네트워크 대역폭](media/site-recovery-hyper-v-deployment-planner-analyze-report/required-network-bandwidth-h2a.png)

**RPO 시간 100% 충족**: 원하는 RPO 시간을 100% 충족하는 데 할당되는 권장 대역폭(Mbps)입니다. 이 양의 대역폭은 RPO 위반을 방지하는 데 호환되는 모든 VM의 안정적인 상태 델타 복제 전용이어야 합니다.

**RPO 시간 90% 충족**: 광대역 가격 책정 또는 다른 이유로 인해 원하는 RPO 시간 100%를 충족시키는 데 필요한 대역폭을 설정할 수 없는 경우 원하는 RPO 시간 90%를 충족할 수 있는 더 낮은 대역폭을 설정하도록 선택할 수 있습니다. 이 낮은 대역폭을 설정하는 의미를 이해하기 위해 보고서에서 예상되는 RPO 위반 횟수 및 기간에 대한 가상(what-if) 분석을 제공합니다.

**달성된 처리량:** GetThroughput 명령을 실행한 서버에서 저장소 계정이 있는 Azure 지역으로의 처리량입니다. 이 처리량 숫자는 Hyper-V 서버 저장소 및 네트워크 특성이 도구를 실행한 서버의 해당 항목과 동일하게 유지된다는 조건 하에 Azure Site Recovery를 사용하여 호환되는 VM을 보호할 때 달성할 수 있는 예상되는 수준을 나타냅니다.

모든 엔터프라이즈 Azure Site Recovery 배포의 경우 [ExpressRoute](https://aka.ms/expressroute)를 사용하는 것이 좋습니다.

### <a name="required-storage-accounts"></a>필요한 저장소 계정
다음 차트에서는 호환되는 모든 VM을 보호하는 데 필요한 저장소 계정(표준 및 프리미엄)의 총 수를 보여 줍니다. 각 VM에 사용할 저장소 계정에 대해 알아보려면 "VM 저장소 배치" 섹션을 참조하세요.

![필요한 저장소 계정](media/site-recovery-hyper-v-deployment-planner-analyze-report/required-storage-accounts-h2a.png)

### <a name="required-number-of-azure-cores"></a>필요한 Azure 코어 수
이 결과는 호환되는 모든 VM의 장애 조치 또는 테스트 장애 조치 전에 설정할 코어의 총 수입니다. 구독에서 사용할 수 있는 코어 수가 너무 적은 경우 Azure Site Recovery에서 테스트 장애 조치 또는 장애 조치 시 VM을 만들지 못합니다.
![필요한 Azure 코어 수](media/site-recovery-hyper-v-deployment-planner-analyze-report/required-number-of-azure-cores-h2a.png)


### <a name="additional-on-premises-storage-requirement"></a>추가적인 온-프레미스 저장소 요구 사항

성공적인 초기 복제 및 델타 복제를 위해 Hyper-V 서버에 필요한 전체 사용 가능한 저장소이며, VM 복제로 인해 프로덕션 응용 프로그램에 바람직하지 않은 가동 중지 시간이 발생하지 않도록 합니다. 각 볼륨 요구 사항에 대한 자세한 내용은 [온-프레미스 저장소 요구 사항](#on-premises-storage-requirement)을 참조하세요. 

복제를 위해 사용 가능한 공간이 필요한 이유를 이해하려면 [온-프레미스 저장소 요구 사항](#why-do-i-need-free-space-on-the-hyper-v-server-for-the-replication) 섹션을 참조하세요.

![온-프레미스 저장소 요구 사항 및 복사 빈도](media/site-recovery-hyper-v-deployment-planner-analyze-report/on-premises-storage-and-copy-frequency-h2a.png)

### <a name="maximum-copy-frequency"></a>최대 복사 빈도
원하는 RPO를 달성하려면 복제에 대해 권장되는 최대 복사 빈도를 설정해야 합니다. 기본값은 5분입니다. 더 높은 RPO를 달성하려면 30초 복사 빈도를 설정할 수 있습니다.

### <a name="what-if-analysis"></a>가상 분석
![가상 분석](media/site-recovery-hyper-v-deployment-planner-analyze-report/what-if-analysis-h2a.png) 이 분석은 원하는 RPO 시간 90%만 충족하도록 낮은 대역폭을 설정할 때 프로파일링 기간 동안 발생할 수 있는 위반의 수를 설명합니다. 지정한 날짜에 하나 이상의 RPO 위반이 발생할 수 있습니다. 그래프는 해당 날짜의 최대 RPO를 보여줍니다. 이 분석에 따라 일일 RPO 위반 횟수와 일일 RPO 최고 적중 횟수를 지정된 낮은 대역폭으로 허용할 수 있는지 결정할 수 있습니다. 허용되는 경우 복제를 위해 더 낮은 대역폭을 할당할 수 있으며, 그렇지 않고 원하는 RPO 시간 100%를 충족하려면 제안된 대로 더 높은 대역폭을 할당합니다. 

### <a name="recommendation-for-successful-initial-replication"></a>성공적인 초기 복제를 위한 권장 사항
이 섹션에서는 VM을 보호할 일괄 처리 수와 IR(초기 복제)을 성공적으로 완료하는 데 필요한 최소 대역폭을 권장합니다. 

![IR 일괄 처리](media/site-recovery-hyper-v-deployment-planner-analyze-report/ir-batching-h2a.png)

VM은 주어진 일괄 처리 순서로 보호되어야 합니다. 각 일괄 처리에는 구체적인 VM 목록이 있습니다. 일괄 처리 1 VM은 일괄 처리 2보다 먼저 보호되어야 합니다. 일괄 처리 2 VM은 일괄 처리 3보다 먼저 보호되는 방식으로 계속되어야 합니다. 일괄 처리 1 VM에 대한 초기 복제가 완료되면 일괄 처리 2 VM에 대한 복제를 사용하도록 설정할 수 있습니다. 이와 유사하게 일괄 처리 2 VM에 대한 초기 복제가 완료되면 일괄 처리 3 VM에 대한 복제를 사용하도록 설정하는 방식으로 계속됩니다. 일괄 처리 순서를 따르지 않으면 나중에 보호되는 VM의 초기 복제를 위한 대역폭이 충분하지 않을 수 있습니다. 결과적으로 VM이 초기 복제를 완료할 수 없거나 보호된 VM이 동기화 모드로 거의 전환되지 않게 됩니다. 선택한 RPO 시트에 대한 IR 일괄 처리에는 각 일괄 처리에 포함해야 하는 VM에 대해 자세한 정보가 있습니다.

다음 그래프는 일괄 처리 전체에 대한 초기 복제 및 델타 복제를 위한 대역폭 분포를 주어진 일괄 처리 순서로 보여줍니다. 첫 번째 일괄 처리의 VM을 보호하는 경우 초기 복제에 전체 대역폭을 사용할 수 있습니다. 첫 번째 일괄 처리에 대한 초기 복제가 끝나면 일부 대역폭이 델타 복제에 필요합니다. 나머지 대역폭은 두 번째 일괄 처리의 VM 복제에 사용할 수 있게 됩니다. 일괄 처리 2 막대에 일괄 처리 1에 필요한 델타 복제 대역폭과 일괄 처리 2 VM의 초기 복제에 사용할 수 있는 대역폭이 표시됩니다. 이와 유사하게 일괄 처리 3 막대에 이전 일괄 처리(일괄 처리1 및 2 VM)의 델타 복제에 필요한 대역폭과 일괄 처리 3의 초기 복제에 사용할 수 있는 대역폭이 표시됩니다.  모든 일괄 작업의 초기 복제가 끝나면 마지막 막대에 보호되는 모든 VM의 델타 복제에 필요한 대역폭이 표시됩니다. 

**초기 복제 일괄 처리가 왜 필요한가요?**
초기 복제 완료 시간은 VM 디스크 크기, 사용된 디스크 공간 및 사용 가능한 네트워크 처리량에 기반합니다. 자세한 내용은 선택한 RPO 시트의 IR 일괄 작업에 제공됩니다.

### <a name="cost-estimation"></a>비용 예측
이 그래프는 사용자가 선택한 대상 지역에 대해 예측한 총 DR(재해 복구) 비용 및 사용자가 보고서 생성을 위해 지정한 통화의 요약 보기를 보여줍니다.
![비용 예측 요약](media/site-recovery-hyper-v-deployment-planner-analyze-report/cost-estimation-summary-h2a.png) 이 요약은 Azure Site Recovery를 사용하여 호환 가능한 모든 VM을 Azure로 보호할 때 저장소, 계산, 네트워크 및 라이선스에 대해 지불해야 하는 비용을 이해하는 데 도움이 됩니다. 비용은 프로파일링된 모든 VM이 아닌 호환 가능한 VM에 대해 계산됩니다.  
 
월별 또는 연도별 비용을 볼 수 있습니다. [지원되는 대상 지역](./site-recovery-hyper-v-deployment-planner-cost-estimation.md#supported-target-regions) 및 [지원되는 통화](./site-recovery-hyper-v-deployment-planner-cost-estimation.md#supported-currencies)에 대해 자세히 알아보세요.

**구성 요소별 비용** 총 DR 비용은 계산, 저장소, 네트워크 및 Azure Site Recovery 라이선스 비용이라는 4가지 구성 요소로 나뉩니다. 비용은 복제 중에 발생하는 사용량 및 DR 드릴 시간에 계산, 저장소(프리미엄 및 표준), 온-프레미스 사이트와 Azure 사이에 구성된 ExpressRoute/VPN 및 Azure Site Recovery 라이선스에 대해 발생하는 사용량을 기반으로 계산됩니다.

**상태별 비용**: 총 DR(재해 복구) 비용은 복제 및 DR 드릴이라는 두 가지 다른 상태를 기반으로 분류됩니다. 

**복제 비용**: 복제 중에 발생하는 비용입니다. 저장소, 네트워크 및 Azure Site Recovery 라이선스 비용이 포함됩니다. 

**DR 드릴 비용**: 테스트 장애 조치(failover) 중에 발생하는 비용입니다. Azure Site Recovery는 테스트 장애 조치(failover) 중에 VM을 작동합니다. DR 드릴 비용은 VM의 계산 및 저장소를 실행하는 비용을 포함합니다. 

**월간/연간 Azure 저장소 비용**: 복제 및 DR 드릴을 위해 프리미엄 및 표준 저장소에 대해 발생할 총 저장소 비용을 보여줍니다.
VM당 자세한 비용 분석은 [비용 예측](site-recovery-hyper-v-deployment-planner-cost-estimation.md) 시트에서 볼 수 있습니다.

### <a name="growth-factor-and-percentile-values-used"></a>사용된 증가율 및 백분위 수 값
시트 아래쪽의 이 섹션에는 프로파일링된 VM의 모든 성능 카운터에 사용된 백분위수 값(기본값: 95번째 백분위수)과 모든 계산에 사용된 증가율(기본값: 30%)이 표시됩니다.

![사용된 증가율 및 백분위 수 값](media/site-recovery-hyper-v-deployment-planner-run/growth-factor-max-percentile-value.png)

## <a name="recommendations-with-available-bandwidth-as-input"></a>입력으로 사용 가능한 대역폭을 사용하는 권장 사항
![대역폭 입력을 통한 프로파일링 개요](media/site-recovery-hyper-v-deployment-planner-analyze-report/profiling-overview-bandwidth-input-h2a.png)

Azure Site Recovery 복제에 대해 대역폭을 x Mbps 이상 설정할 수 없는 경우가 있을 수 있습니다. 이 도구를 사용하면 사용 가능한 대역폭을 입력하고(보고서 생성 중에 -Bandwidth 매개 변수 사용), 달성 가능한 RPO(분)를 가져올 수 있습니다. 이처럼 달성 가능한 RPO 값을 사용하여 추가 대역폭을 프로비전해야 하는지 또는 이 RPO로 재해 복구 솔루션을 사용하는 것이 좋은지 여부를 결정할 수 있습니다.

![달성 가능한 RPO](media/site-recovery-hyper-v-deployment-planner-analyze-report/achivable-rpo-h2a.PNG)

## <a name="vm-storage-placement-recommendation"></a>VM-저장소 배치 권장 사항 

![VM-Storage 배치](media/site-recovery-hyper-v-deployment-planner-analyze-report/vm-storage-placement-h2a.png)

**디스크 저장소 유형**: **배치할 VM** 열에 언급된 해당 가상 컴퓨터를 모두 복제하는 데 사용되는 표준 또는 프리미엄 Storage 계정입니다.

**제안된 접두사**: 저장소 계정 이름을 지정하는 데 사용할 수 있는 3자로 구성된 접두사입니다. 고유한 접두사를 사용할 수 있지만 도구의 제안은 [저장소 계정에 대 한 파티션 명명 규칙](https://aka.ms/storage-performance-checklist)을 따릅니다.

**제안된 계정 이름**: 제안된 접두사를 포함한 후 저장소 계정 이름입니다. 꺾쇠 괄호(< 및 >) 안의 이름을 사용자 지정 입력으로 바꿉니다.

**로그 Storage 계정**: 모든 복제 로그는 Standard Storage 계정에 저장됩니다. 프리미엄 저장소 계정에 복제하는 VM의 경우 로그 저장소에 대한 추가 표준 저장소 계정을 설정합니다. 여러 프리미엄 복제 저장소 계정에서 단일 표준 로그 저장소 계정을 사용할 수 있습니다. 표준 저장소 계정에 복제된 VM은 로그에 대해 동일한 저장소 계정을 사용합니다.

**제안된 로그 계정 이름**: 제안된 접두사를 포함한 후 저장소 로그 계정 이름입니다. 꺾쇠 괄호(< 및 >) 안의 이름을 사용자 지정 입력으로 바꿉니다.

**배치 요약**: 복제 및 테스트 장애 조치 또는 장애 조치 시 저장소 계정의 총 VM 부하에 대한 요약입니다. 저장소 계정에 매핑된 총 VM 수, 이 저장소 계정에 배치되는 모든 VM의 총 읽기/쓰기 IOPS, 총 쓰기(복제) IOPS, 모든 디스크에 설정된 총 크기 및 총 디스크 수를 포함합니다.

**배치할 Virtual Machines**: 최적의 성능과 사용을 위해 지정된 저장소 계정에 배치해야 하는 VM을 모두 나열합니다.

## <a name="compatible-vms"></a>호환되는 VM
Azure Site Recovery Deployment Planner에서 생성된 Microsoft Excel 보고서의 "호환되는 VM" 시트에 호환되는 모든 VM의 세부 정보가 제공됩니다.

![호환되는 VM](media/site-recovery-hyper-v-deployment-planner-analyze-report/compatible-vms-h2a.png)

**VM 이름**: 보고서가 생성될 때 VMListFile에 사용되는 VM 이름입니다. 또한 이 열에는 VM에 연결된 디스크(VHD)가 나열됩니다. 이 이름에는 프로파일링 기간 동안 VM이 도구를 검색했을 때 VM이 있었던 Hyper-V 호스트 이름이 포함됩니다.

**VM 호환성**: 값은 **예** 및 **예**\*입니다. **예**\*는 VM이 [Azure Premium Storage](https://aka.ms/premium-storage-workload)에 적합한 인스턴스에 대한 값입니다. 여기서 프로파일링된 높은 변동 또는 IOPS 디스크는 디스크에 매핑된 크기 보다 높은 프리미엄 디스크 크기에 적합합니다. 저장소 계정 크기에 따라 디스크를 매핑할 프리미엄 저장소 디스크 유형이 결정됩니다. 
* 128GB 미만은 P10입니다.
* 128GB ~ 256GB는 P15입니다.
* 256GB ~ 512GB는 P20입니다.
* 512GB ~ 1,024GB는 P30입니다.
* 1,025GB ~ 2,048GB는 P40입니다.
* 2,049GB ~ 4,095GB는 P50입니다.

예를 들어, 디스크의 워크로드 특성이 P20 또는 P30 범주에 속하지만 크기가 더 낮은 프리미엄 저장소 디스크 유형에 낮게 매핑되는 경우 도구에서 해당 VM이 **예**\*로 표시됩니다. 또한 도구에서는 원본 디스크 크기를 권장 프리미엄 저장소 디스크 유형에 맞게 변경하거나 대상 디스크 유형 사후 장애 조치를 변경할 것을 권장합니다.

**저장소 유형**: 표준 또는 프리미엄입니다.

**제안된 접두사**: 3자로 구성된 저장소 계정 접두사입니다.

**Storage 계정**: 제안된 Storage 계정 접두사를 사용하는 이름입니다.

**최고 읽기/쓰기 IOPS(증가율 포함)**: 향후 증가율(기본값: 30%)을 포함한 디스크의 최고 워크로드 읽기/쓰기 IOPS(기본값: 95번째 백분위수)입니다. 참고로 VM의 최고 읽기/쓰기 IOPS는 프로파일링 기간의 매분마다 개별 디스크의 읽기/쓰기 IOPS를 합친 최고값이기 때문에 VM의 총 읽기/쓰기 IOPS가 항상 VM에 속한 개별 디스크의 읽기/쓰기 IOPS 합계가 되는 것은 아닙니다.

**최고 데이터 변동률(MB/s)(증가율 포함)**: 향후 증가율(기본값: 30%)을 포함한 디스크의 최고 변동률(기본값: 95번째 백분위수)입니다. VM의 총 데이터 변동은 프로파일링 기간의 매분마다 개별 디스크 변동 합계의 최고값이기 때문에 VM의 총 데이터 변동이 항상 VM에 속한 개별 디스크의 데이터 변동 합계가 되는 것은 아닙니다.

**Azure VM 크기**: 이 온-프레미스 VM에 대해 이상적으로 매핑된 Azure Cloud Services 가상 컴퓨터 크기입니다. 매핑은 온-프레미스 VM의 메모리, 디스크/코어/NIC 수 및 읽기/쓰기 IOPS를 기반으로 합니다. 항상 모든 온-프레미스 VM 특성과 일치하는 가장 낮은 Azure VM 크기를 권장합니다.

**디스크 수**: VM의 총 가상 머신 디스크 수(VHD)입니다.

**디스크 크기(GB)**: VM에 속한 모든 디스크의 총 크기입니다. 또한 도구에서는 VM의 개별 디스크에 대한 디스크 크기도 보여 줍니다.

**코어 수**: VM의 CPU 코어 수입니다.

**메모리(MB)**: VM의 RAM 크기입니다.

**NIC 수**: VM의 NIC 수입니다.

**부팅 유형**: VM의 부팅 유형입니다. BIOS 또는 EFI일 수 있습니다.

## <a name="incompatible-vms"></a>호환되지 않는 VM
Azure Site Recovery Deployment Planner에서 생성된 Microsoft Excel 보고서의 "호환되지 않는 VM" 시트에 호환되지 않는 모든 VM의 세부 정보가 제공됩니다.

![호환되지 않는 VM](media/site-recovery-hyper-v-deployment-planner-analyze-report/incompatible-vms-h2a.png)

**VM 이름**: 보고서가 생성될 때 VMListFile에 사용되는 VM 이름입니다. 또한 이 열에는 VM에 연결된 디스크(VHD)가 나열됩니다. 이 이름에는 프로파일링 기간 동안 VM이 도구를 검색했을 때 VM이 있었던 Hyper-V 호스트 이름이 포함됩니다.

**VM 호환성**: 지정된 VM을 Azure Site Recovery에서 사용할 수 없는 이유를 나타냅니다. 이유는 게시된 [저장소 한도](https://aka.ms/azure-storage-scalbility-performance)를 기반으로 VM의 각 호환되지 않는 디스크에 대해 설명되며 다음 중 하나일 수 있습니다.

* 디스크 크기가 4,095GB보다 큽니다. Azure Storage는 현재 4,095GB보다 큰 디스크 크기를 지원하지 않습니다.

* OS 디스크가 1세대(BIOS 부팅 유형) VM에 대한 2047GB보다 큽니다.  Azure Site Recovery는 1세대 VM에 대해 2047GB를 초과하는 OS 디스크 크기를 지원하지 않습니다.

* OS 디스크가 2세대(EFI 부팅 유형) VM에 대한 300GB보다 큽니다. Azure Site Recovery는 2세대 VM에 대해 300GB를 초과하는 OS 디스크 크기를 지원하지 않습니다.

* VM 이름에 다음 문자 중 일부가 포함되며 “” [] `는 지원되지 않습니다.  VM 이름에 이러한 문자 중 일부가 포함되면 도구에서 VM의 프로파일링된 데이터를 가져올 수 없습니다. 

* VHD는 둘 이상의 VM에 의해 공유됩니다. Azure는 공유 VHD가 있는 VM을 지원하지 않습니다.

* 가상 파이버 채널이 있는 VM은 지원되지 않습니다. Azure Site Recovery는 가상 파이버 채널이 있는 VM을 지원하지 않습니다.

* Hyper-V 클러스터는 복제 broker를 포함하지 않습니다. Azure Site Recovery는 Hyper-V 복제본 broker가 클러스터에 대해 구성되어 있지 않으면 Hyper-V 클러스터의 VM을 지원하지 않습니다.

* VM은 고가용성이 아닙니다. Azure Site Recovery는 VHD가 클러스터 디스크가 아닌 로컬 디스크에 저장되어 있으면 Hyper-V 클러스터 노드의 VM을 지원하지 않습니다. 

* 총 VM 크기(복제 + TFO)가 지원되는 프리미엄 저장소 계정 크기 한도(35TB)를 초과합니다. 이러한 비호환성은 일반적으로 VM의 단일 디스크가 표준 저장소에 대해 지원되는 최대 Azure 또는 Azure Site Recovery 한도를 초과하는 성능 특성을 가지고 있는 경우에 발생합니다. 이러한 인스턴스는 VM을 프리미엄 저장소 영역에 푸시합니다. 그러나 프리미엄 저장소 계정의 최대 지원 크기는 35TB이며, 보호된 단일 VM을 여러 저장소 계정에서 보호할 수 없습니다. 관리되지 않는 디스크가 테스트 장애 조치(failover)용으로 구성된 경우, 보호되는 VM에 대해 테스트 장애 조치를 실행하면, 복제가 진행 중인 저장소 계정과 동일한 계정에서 실행된다는 점에 유의해야 합니다. 이런 경우 복제와 동일한 추가 저장소 공간이 필요합니다. 그러면 병렬로 복제가 진행되고 테스트 장애 조치(failover)가 성공할 수 있습니다. 관리 디스크가 테스트 장애 조치(failover)용으로 구성된 경우, 테스트 장애 조치 VM을 위해 추가 공간을 고려할 필요가 없습니다.

* 원본 IOPS가 디스크당 지원되는 저장소 IOPS 한도(7500)를 초과합니다.

* 원본 IOPS가 VM당 지원되는 저장소 IOPS 한도(80,000)를 초과합니다.

* 원본 VM 평균 데이터 변동률이 디스크의 평균 I/O 크기에 대해 지원되는 Azure Site Recovery 데이터 변동률 한도(10MB/s)를 초과합니다.

* 원본 VM 평균 유효 쓰기 IOPS가 지원되는 Azure Site Recovery IOPS 제한(840)을 초과합니다.

* 계산된 스냅숏 저장소가 지원되는 스냅숏 저장소 한도(10TB)를 초과합니다.

**최고 읽기/쓰기 IOPS(증가율 포함)**: 향후 증가율(기본값: 30%)을 포함한 디스크의 최고 워크로드 IOPS(기본값: 95번째 백분위수)입니다. 참고로 VM의 최고 읽기/쓰기 IOPS는 프로파일링 기간의 매분마다 개별 디스크의 읽기/쓰기 IOPS를 합친 최고값이기 때문에 VM의 총 읽기/쓰기 IOPS가 항상 VM에 속한 개별 디스크의 읽기/쓰기 IOPS 합계가 되는 것은 아닙니다.

**최고 데이터 변동률(MB/s)(증가율 포함)**: 향후 증가율(기본값: 30%)을 포함한 디스크의 최고 변동률(기본값: 95번째 백분위수)입니다. VM의 총 데이터 변동은 프로파일링 기간의 매분마다 개별 디스크 변동 합계의 최고값이기 때문에 VM의 총 데이터 변동이 항상 VM에 속한 개별 디스크의 데이터 변동 합계가 되는 것은 아닙니다.

**디스크 수**: VM의 총 VHD 수입니다.

**디스크 크기 (GB)**: VM에 속한 모든 디스크의 총 설정 크기입니다. 또한 도구에서는 VM의 개별 디스크에 대한 디스크 크기도 보여 줍니다.

**코어 수**: VM의 CPU 코어 수입니다.

**메모리(MB)**: VM의 RAM 양입니다.

**NIC 수**: VM의 NIC 수입니다.

**부팅 유형**: VM의 부팅 유형입니다. BIOS 또는 EFI일 수 있습니다.

## <a name="azure-site-recovery-limits"></a>Azure Site Recovery 제한
다음 테이블에는 Azure Site Recovery 제한이 제공됩니다. 이러한 한도는 테스트를 기반으로 하지만 모든 가능한 응용 프로그램 I/O 조합을 다룰 수는 없습니다. 실제 결과는 응용 프로그램 I/O 조합에 따라 달라질 수 있습니다. 최상의 결과를 얻으려면 배포를 계획한 후에도 항상 테스트 장애 조치를 통해 광범위한 응용 프로그램 테스트를 수행하여 응용 프로그램의 진정한 성능 상황을 이해하는 것이 좋습니다.
 
**복제 저장소 대상** | **원본 VM 평균 I/O 크기** |**원본 VM 평균 데이터 변동** | **일일 총 원본 VM 데이터 변동**
---|---|---|---
Standard Storage | 8KB | VM당 2MB/s | VM당 168GB
Premium Storage | 8KB  | VM당 5MB/s | VM당 421GB
Premium Storage | 16KB 이상| VM당 10MB/s | VM당 842GB

이러한 한도는 I/O가 30% 겹친다고 가정하는 평균 숫자입니다. Azure Site Recovery는 중첩 비율, 더 큰 쓰기 크기 및 실제 워크로드 I/O 동작에 따라 더 높은 처리량을 다룰 수 있습니다. 앞의 숫자는 약 5분의 일반적인 백로그가 있다고 가정합니다. 즉, 데이터를 업로드한 후에 처리되며 5분 내에 복구 지점이 생성됩니다.

## <a name="on-premises-storage-requirement"></a>온-프레미스 저장소 요구 사항

워크시트에 성공적인 초기 복제 및 델타 복제를 위해 Hyper-V 서버(VHD가 상주하는)의 각 볼륨에 대해 사용 가능한 총 저장소 공간 요구 사항이 제공됩니다. 복제를 사용하도록 설정하기 전에 복제로 인해 프로덕션 응용 프로그램에 바람직하지 않은 가동 중단 시간이 발생하지 않도록 볼륨에 필요한 저장소 공간을 추가합니다. 

Azure Site Recovery Deployment Planner는 VHD 크기 및 복제에 사용되는 네트워크 대역폭에 기반하여 최적의 저장소 공간 요구 사항을 파악합니다.

![온-프레미스 저장소 요구 사항](media/site-recovery-hyper-v-deployment-planner-analyze-report/on-premises-storage-requirement-h2a.png)

### <a name="why-do-i-need-free-space-on-the-hyper-v-server-for-the-replication"></a>복제를 위해 Hyper-V 서버에 여유 공간이 필요한 이유가 무엇인가요?
* VM 복제를 사용하도록 설명하면 Azure Site Recovery는 IR(초기 복제)을 위해 VM의 각 VHD에 대한 스냅숏을 생성합니다. 초기 복제를 수행하는 동안 응용 프로그램에 의해 새로운 변경 내용이 디스크에 기록됩니다. Azure Site Recovery는 이러한 델타 변경 내용을 로그 파일로 추적하며, 이를 위해 추가 저장소 공간이 필요합니다.  초기 복제가 완료될 때까지 로그 파일은 로컬에 저장됩니다. 로그 파일과 스냅숏(AVHDX)을 위한 여유 공간이 충분하지 않으면 복제가 다시 동기화 모드가 되면서 완료되지 않습니다. 최악의 경우 초기 복제를 위해 VHD 크기의 100%에 달하는 추가 여유 공간이 필요합니다.
* 초기 복제가 끝나면 델타 복제가 시작됩니다. Azure Site Recovery는 이러한 델타 변경 내용을 로그 파일로 추적하며, 이 파일은 VM의 VHD가 상주하는 볼륨에 저장됩니다. 이러한 로그 파일은 구성된 복사 빈도로 Azure에 복제됩니다. 사용 가능한 네트워크 대역폭에 따라, 로그 파일이 Azure에 복제되는데 어느 정도 시간이 소요됩니다. 로그 파일을 저장할만한 여유 공간이 충분하지 않으면 복제가 일시 중지되고 VM의 복제 상태가 다시 동기화가 필요한 상태가 됩니다.
* 로그 파일을 Azure로 푸시하기 위한 네트워크 대역폭이 충분하지 않으면 로그 파일이 볼륨에 쌓입니다. 최악의 경우, 로그 파일 크기가 VHD 크기의 50%로 증가하면 VM 복제가 다시 동기화가 필요한 상태가 됩니다. 최악의 경우 델타 복제를 위해 VHD 크기의 50%에 달하는 추가 여유 공간이 필요합니다.

**Hyper-V 호스트**: 프로파일링된 Hyper-V 서버의 목록입니다. 서버가 Hyper-V 클러스터의 일부이면 모든 클러스터 노드가 함께 그룹화됩니다.

**볼륨(VHD 경로)**: VHD/VHDX가 있는 Hyper-V 호스트의 각 볼륨입니다. 

**사용 가능한 여유 공간(GB)**: 볼륨에서 사용 가능한 여유 공간입니다.

**볼륨에 필요한 총 저장소 공간(GB**: 성공적인 초기 복제 및 델타 복제를 위해 볼륨에 필요한 사용 가능한 총 저장소 공간입니다. 

**성공적인 복제를 위해 볼륨에 프로비전될 총 추가 저장소**: 성공적인 초기 복제 및 델타 복제를 위해 볼륨에 반드시 프로비전되도록 권장하는 총 추가 공간입니다.

## <a name="initial-replication-batching"></a>초기 복제 일괄 처리 

### <a name="why-do-i-need-initial-replication-ir-batching"></a>IR(초기 복제) 일괄 처리가 왜 필요한가요?
모든 VM이 동시에 보호되는 경우 사용 가능한 저장소 요구 사항이 훨씬 높아지며, 저장소가 충분하지 않으면 VM 복제가 다시 동기화 모드가 됩니다. 또한 모든 VM의 초기 복제를 한꺼번에 성공적으로 완료하려면 네트워크 대역폭 요구 사항도 훨씬 높아집니다. 

### <a name="initial-replication-batching-for-a-selected-rpo"></a>선택한 RPO를 위한 초기 복제 일괄 처리
이 워크시트에는 IR(초기 복제)을 위해 각 일괄 처리에 대한 자세한 보기가 제공됩니다. 각 RPO에 대해 별도의 IR 일괄 처리 시트가 만들어집니다. 

각 볼륨에 권장되는 온-프레미스 저장소 요구 사항을 따른 경우 복제해야 하는 주요 정보는 병렬로 보호할 수 있는 VM 목록입니다. 이러한 VM은 일괄 처리에 함께 그룹화됩니다. 다수의 일괄 처리가 있을 수 있습니다. VM은 반드시 주어진 일괄 처리 순서로 보호해야 합니다. 먼저 일괄 처리 1 VM을 보호하고 초기 복제가 완료되고 나면 일괄 처리 2 VM 순서로 보호합니다. 일괄 처리 목록과 해당 VM은 이 시트에 제공됩니다. 

![IR 일괄 처리 세부 정보1](media/site-recovery-hyper-v-deployment-planner-analyze-report/ir-batching-for-rpo-h2a.png)
![IR 일괄 처리 세부 정보2](media/site-recovery-hyper-v-deployment-planner-analyze-report/ir-batching-for-rpo2-h2a.png)

### <a name="each-batch-provides-the-following-information"></a>각 일괄 처리에는 다음 정보가 제공됩니다. 
**Hyper-V 호스트**: 보호할 VM의 Hyper-V 호스트입니다.
가상 머신: 보호할 VM입니다. 

**설명**: VM의 특정 볼륨에 작업이 필요한 경우 설명이 여기에 제공됩니다.  예를 들어 볼륨에 여유 공간이 충분하지 않은 경우에는 VM을 보호하려면 추가 저장소를 추가하라는 내용이 설명에 언급됩니다.

**볼륨(VHD 경로)**: VM의 VHD가 상주하는 볼륨 이름입니다. 볼륨에 사용 가능한 여유 공간(GB): VM에 대한 볼륨에 사용할 수 있는 여유 디스크 공간입니다. 볼륨에서 사용 가능한 여유 공간이 계산되는 동안, VHD가 동일한 볼륨에 있는 이전 일괄 처리의 VM이 델타 복제에 사용하는 디스크 공간이 고려됩니다.  

예를 들어, VM1, VM2 및 VM3은 E:\VHDpath 볼륨에 상주합니다. 복제 전에 볼륨의 여유 공간 500GB입니다. VM1은 일괄 처리 1의 일부이고, VM2는 일괄 처리 2의 일부이며, VM3은 일괄 처리 3의 일부입니다.  VM1에 사용할 수 있는 여유 공간은 500GB입니다. VM2에 사용할 수 있는 여유 공간은 500GB가 되며 VM1의 델타 복제에 필요한 디스크 공간입니다.  델타 복제를 위해 VM1에 300GB의 공간이 필요한 경우 VM2에 사용할 수 있는 여유 공간은 500GB – 300GB = 200GB가 됩니다.  이와 유사하게, VM2는 델타 복제를 위해 300GB가 필요합니다. VM3에 사용할 수 있는 여유 공간은 200GB - 300GB = -100GB가 됩니다.

**초기 복제를 위해 볼륨에 필요한 저장소(GB)**: 초기 복제를 위해 VM의 볼륨에 필요한 사용 가능한 저장소 공간입니다.

**델타 복제를 위해 볼륨에 필요한 저장소(GB)**: 델타 복제를 위해 VM의 볼륨에 필요한 사용 가능한 저장소 공간입니다.

**복제 오류를 방지하기 위해 부족에 따라 필요한 추가 저장소(GB)**: VM의 볼륨에 필요한 추가 저장소 공간입니다.  초기 복제 및 델타 복제 저장소 공간 요구 사항(볼륨에 사용할 수 있는 여유 공간)의 최대값입니다.

**초기 복제에 필요한 최소 대역폭(Mbps)**: VM의 초기 복제에 필요한 최소 대역폭입니다.

**델타 복제에 필요한 최소 대역폭(Mbps)**: VM의 델타 복제에 필요한 최소 대역폭입니다.

### <a name="network-utilization-details-for-each-batch"></a>각 일괄 처리에 대한 네트워크 이용률 세부 정보 
각 일괄 처리 테이블에는 일괄 처리의 네트워크 이용률에 대한 요약이 제공됩니다.

**일괄 처리에 사용할 수 있는 대역폭**: 이전 일괄 처리의 델타 복제 대역폭을 고려한 후 일괄 처리에 사용할 수 있는 대역폭입니다.

**일괄 처리의 초기 복제에 사용할 수 있는 대략적인 대역폭**: 일괄 처리의 VM에 대한 초기 복제에 사용할 수 있는 대역폭입니다. 

**일괄 처리의 델타 복제에 사용된 대략적인 대역폭**: 일괄 처리의 VM에 대한 델타 복제에 필요한 대역폭입니다. 

**일괄 처리에 예상되는 초기 복제 시간(HH:MM)**: 시간:분 단위로 예상되는 초기 복제 시간입니다.

## <a name="cost-estimation"></a>비용 예측
[비용 예측](site-recovery-hyper-v-deployment-planner-cost-estimation.md)에 대해 자세히 알아봅니다. 

## <a name="next-steps"></a>다음 단계
[비용 예측](site-recovery-hyper-v-deployment-planner-cost-estimation.md)에 대해 자세히 알아봅니다.