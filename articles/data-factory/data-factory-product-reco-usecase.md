---
title: "aaaData 팩터리 사용 사례-제품 권장 사항"
description: "Azure Data Factory 및 기타 서비스로 구현한 사용 사례에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 6f1523c7-46c3-4b8d-9ed6-b847ae5ec4ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: d7912965fe4762d64e8ca3c28381ea6187f36631
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-case---product-recommendations"></a>사용 사례 - 제품 추천
Azure Data Factory에는 많은 사용 되는 서비스 tooimplement hello Cortana Intelligence solution accelerator 제품군 중 하나입니다.  이 제품군에 대한 자세한 내용은 [Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics) 페이지를 참조하세요. 이 문서에서는 Azure 사용자가 Azure Data Factory 및 기타 Cortana Intelligence 구성 요소 서비스를 사용하여 이미 해결하고 구현한 경험이 있는 일반적인 사용 사례를 설명합니다.

## <a name="scenario"></a>시나리오
온라인 소매상 일반적으로 원하는 tooentice 고객 toopurchase 제품에서 원하는 가장 가능성이 높은 toobe 및 따라서 가장 가능성이 높은 toobuy는 제품과 함께 제공 하 여 합니다. tooaccomplish이 온라인 소매상 toocustomize 해당 사용자의 온라인 환경을 사용 하 여 필요한 개인 설정 된 제품을 추천 해당 특정 사용자에 대 한 합니다. 개인 설정 된 권장 되는 현재 및 기록 쇼핑 동작 데이터를 제품 정보에 따라 결정 toobe 새로 도입 된 브랜드, 및 제품 및 고객 분할 데이터입니다.  또한 hello 사용자 제품 기반으로 권장 사항을 결합 하는 모든 사용자의 전반적인 사용량 동작의 분석을 제공할 수 있습니다.

이러한 소매점의 hello 목표 toooptimize 클릭 판매 변환의 사용자 이며 더 높은 판매 수익을 달성 합니다.  고객의 관심사와 작업을 기반으로 상황에 맞는 동작 기반 제품 추천을 제공하여 이러한 변환을 달성합니다. 이 사용 사례에 대 한 고객에 게 toooptimize를 사용할 수 있는 비즈니스용의 예를 들어 온라인 소매상 사용 합니다. 그러나 이러한 원칙 tooengage가 원하는 tooany 비즈니스 해당 고객의 제품 및 서비스에 게 적용 및 고객 구매 환경을 개인 설정 된 제품 권장 사항과 향상 합니다.

## <a name="challenges"></a>과제
있는 경우 많은 문제 온라인 소매상 얼굴 동안 tooimplement이이 유형의 사용 사례 

여러 데이터 원본의 데이터 크기와 셰이프를 ingested 해야는 첫째, 온-프레미스 및 클라우드 hello 합니다. 이 데이터는 hello 사용자가 hello 온라인 소매상 사이트를 탐색 하는 대로 제품 데이터, 기록 고객 동작 데이터 및 사용자 데이터를 포함 합니다. 

둘째, 개인 설정된 제품 추천을 합리적이고 정확하게 계산 및 예측해야 합니다. 또한 온라인 소매상 tooproduct, 브랜드, 및 고객 동작 및 브라우저 데이터는 hello 사용자에 대 한 과거 구매 toofactor hello hello 제품 최선의 결정에에 대 한 고객 피드백 tooinclude도 필요 했습니다. 

셋째, hello 권장 사항을 즉시 결과물 toohello 사용자 tooprovide 원활 하 게 검색 및 구매, 고 hello 가장 최근 하 고 관련 권장 사항을 제공 합니다. 

마지막으로, 소매 업체 전반적인 상향 판매를 추적 하 여 해당 접근 방식의 toomeasure hello 효율성 필요 교차 판매 클릭 변환 판매 성공 및 tootheir 이후 권장 사항을 조정 합니다.

## <a name="solution-overview"></a>솔루션 개요
이 사용 사례 예에서는 실제 Azure 사용자가 [HDInsight](https://azure.microsoft.com/services/hdinsight/) 및 [Power BI](https://powerbi.microsoft.com/)를 포함한 Azure Data Factory 및 기타 Cortana Intelligence 구성 요소 서비스를 사용하여 해결 및 구현했습니다.

hello 온라인 상점 hello 워크플로 전체에서 해당 데이터 저장소 옵션으로는 Azure Blob 저장소, 온-프레미스 SQL server, Azure SQL DB 및 관계형 데이터 마트를 사용합니다.  hello blob 저장소에는 고객 정보, 고객 동작 데이터 및 제품 정보 데이터가 포함 되어 있습니다. 온-프레미스 SQL 데이터 웨어하우스에 저장 하는 hello 제품 정보 데이터 제품 브랜드 정보 및 제품 카탈로그가 포함 됩니다. 

모든 hello 데이터 결합 및에 제품 추천 시스템 toodeliver 개인 설정에 따라 권장 사항을 고객의 관심 및 동작을 hello 사용자가 hello 웹 사이트에서 hello 카탈로그의 제품을 검색 하는 동안 제공 됩니다. hello 고객 toohello 제품에서 검색 하는 전체 웹 사이트 사용 패턴을 기반으로 관련된 tooany 하지 않은 한 명의 사용자와 관련 된 제품을 참조 하세요.

![사용 사례 다이어그램](./media/data-factory-product-reco-usecase/diagram-1.png)

기가바이트 원시 웹 로그 파일의는 반 구조화 된 파일로 hello 온라인 상점 웹 사이트에서 매일 생성 됩니다. 원시 웹 로그 파일을 hello 및 hello 고객 및 제품 카탈로그 정보는 수집 된 정기적으로 Data Factory 전체적으로 배포 된 데이터 이동 서비스로 사용 하는 Azure Blob 저장소에 있습니다. hello hello 날에 대 한 원시 로그 파일에 장기 저장을 위한 blob 저장소에 (연도 및 월)에서 분할 됩니다.  [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/) 모두 Hive 및 Pig 스크립트를 사용 하 여 규모에 hello 수집 된 로그 저장소와 처리 하는 hello blob에 사용 되는 toopartition hello 원시 로그 파일입니다. 분할 된 웹 로그 데이터는 hello 다음 처리 된 tooextract hello 기계 학습 추천 시스템 toogenerate 개인 설정 된 hello 제품 권장 사항에 대 한 입력 필요 합니다.

hello이 예에서 hello 기계 학습에 사용 되는 추천 시스템은 추천 플랫폼에서 학습 하는 오픈 소스 컴퓨터 [Apache Mahout](http://mahout.apache.org/)합니다.  모든 [Azure 기계 학습](https://azure.microsoft.com/services/machine-learning/) 되거나 사용자 지정 모델에 적용 된 toohello 시나리오 일 수 있습니다.  hello Mahout 모델은 전반적인 사용 패턴에 따라 hello 웹 사이트에 있는 항목 사이의 hello 개별 사용자에 따라 toogenerate hello 개인 설정 된 권장 구성을 사용 하는 toopredict hello 유사성입니다.

마지막으로 hello 결과 집합이 개인 설정 된 제품을 추천 하는 hello 소매 업체 웹 사이트에서 사용할 수 있도록 이동된 tooa 관계형 데이터 마트에입니다.  hello 결과 집합에는 다른 응용 프로그램에서 blob 저장소에서 직접 액세스할 수도 없습니다 또는 다른 소비자 및 사용 사례에 대 한 tooadditional 저장소를 이동 합니다.

## <a name="benefits"></a>이점
제품 권장 전략을 최적화 하 고 비즈니스 목표에 맞추어를 hello 솔루션 hello 온라인 상점 머천다이징, 마케팅 목표를 충족 해야 합니다. 또한 수 toooperationalize 된 및 관리 하는 hello 제품 권장 워크플로 효율적인 안정적이 고 비용 효율적인 방식입니다. hello 접근 방식을 쉽게을 tooupdate 자신의 모델 및 판매 클릭 변환 성공 hello 측정값에 따라 모델의 효율성을 미세 조정 합니다. Azure 데이터 팩터리를 사용 하 여 있습니다 수 tooabandon의 시간이 오래 걸리고 비용이 많이 드는 수동 클라우드 리소스 관리 했으며 tooon 요청 시 클라우드 리소스 관리를 이동 합니다. 따라서 있습니다 수 toosave 시간, 비용, 였으며 toosolution 배포 시간을 줄입니다. 데이터 계보 뷰 및 operational 서비스 상태 쉽게 toovisualize 차고 hello 직관적인 데이터 팩터리의 모니터링 및 관리 UI hello Azure 포털에서에서 사용할 수 있는 문제를 해결 합니다. 이제 솔루션을 예약 및 완료 된 데이터 안정적으로 생성 되 고 toousers, 배달 및 데이터 및 처리 종속성 사용자의 개입 없이 자동으로 관리 되도록를 관리 수 있습니다.

이 개인 설정 된 쇼핑 경험을 제공 하 여 hello 경쟁력 고 흥미로운 고객을 생성 하는 온라인 상점 환경 및 따라서 영업 및 전반적인 고객 만족도 높일.

