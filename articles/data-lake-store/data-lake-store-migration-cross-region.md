---
title: "데이터 레이크 저장소 지역 간 마이그레이션 aaaAzure | Microsoft Docs"
description: "Azure Data Lake Store의 지역 간 마이그레이션에 대해 알아봅니다."
services: data-lake-store
documentationcenter: 
author: swums
manager: amitkul
editor: swums
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/27/2017
ms.author: stewu
ms.openlocfilehash: 561ac821c1bd555886035867678cb685997564eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-data-lake-store-across-regions"></a>지역 간 Data Lake Store 마이그레이션

Azure 데이터 레이크 저장소 새 지역에서 사용할 수 있게 됨, 일회성 마이그레이션 새 영역 hello tootake 활용 toodo를 선택할 수 있습니다. 계획 하 고 hello 마이그레이션을 완료할 때 어떤 tooconsider에 알아봅니다.

## <a name="prerequisites"></a>필수 조건

* **Azure 구독**. 자세한 내용은 [지금 무료 Azure 계정 만들기](https://azure.microsoft.com/pricing/free-trial/)를 참조하세요.
* **두 개의 다른 지역의 Data Lake Store 계정** 자세한 내용은 [Azure Data Lake Store 시작](data-lake-store-get-started-portal.md)을 참조하세요.
* **Azure Data Factory**. 자세한 내용은 참조 [소개 tooAzure Data Factory](../data-factory/data-factory-introduction.md)합니다.


## <a name="migration-considerations"></a>마이그레이션 고려 사항

먼저, 기록, 읽기, 또는 데이터 레이크 저장소의 데이터를 처리 하는 응용 프로그램에 가장 적합 한 hello 마이그레이션 전략을 식별 합니다. 전략을 선택 하는 경우 응용 프로그램의 가용성 요구 사항 및 마이그레이션 중에 발생 하는 hello 가동 중지 시간을 고려 합니다. 예를 들어 프로그램 가장 간단한 접근 toouse hello "리프트 시프트" 클라우드 마이그레이션 모델 수도 있습니다. 이 방법에서는 데이터를 모두 toohello 새 영역을 복사 하는 동안 기존 영역에 hello 응용 프로그램을 일시 합니다. Hello 복사 프로세스가 완료 되 면 hello 새 영역에서 응용 프로그램을 다시 시작 하 고 hello 이전 데이터 레이크 저장소 계정을 삭제 합니다. Hello 마이그레이션하는 동안 가동 중지 시간이 필요 합니다.

tooreduce 가동 중단 시간을 시작할 수 있습니다 즉시 hello 새 영역에 새 데이터를 수집 하는 방법. 필요한 최소 데이터 hello 있으면 hello 새 영역에 응용 프로그램을 실행 합니다. Hello 백그라운드에서 hello 새 지역에 toocopy hello 기존 데이터 레이크 저장소 계정 toohello 새 Data Lake 저장소 계정에서 오래 된 데이터를 계속 합니다. 이 방법을 사용 하 여 hello 스위치 toohello 거의 가동 중지 시간을 사용 하 여 새 영역을 만들 수 있습니다. 모든 hello 오래 된 데이터 복사 되 면 hello 이전 데이터 레이크 저장소 계정을 삭제 합니다.

마이그레이션을 계획할 때 다른 중요 한 세부 정보 tooconsider가 됩니다.

* **데이터 볼륨** hello (기가바이트 hello 수 파일 및 폴더, 등)에 데이터 양이 hello 시간과 hello 마이그레이션에 필요한 리소스에 영향을 줍니다.

* **Data Lake Store 계정 이름** hello 새 지역에 새 계정 이름 hello 전역적으로 고유 해야 합니다. 예를 들어 미국 동부 2에서에서 이전 데이터 레이크 저장소 계정 이름을 hello contosoeastus2.azuredatalakestore.net 수도 있습니다. 북유럽에 있는 Data Lake Store 계정의 이름을 contosonortheu.azuredatalakestore.net으로 지정할 수 있습니다.

* **도구** Hello를 사용 하는 것이 좋습니다 [Azure 데이터 팩터리 복사 활동](../data-factory/data-factory-azure-datalake-connector.md) toocopy 데이터 레이크 저장소 파일입니다. Data Factory는 데이터를 이동할 때 고성능 및 안정성을 지원합니다. 데이터 팩터리 hello 폴더 계층과 hello 파일의 콘텐츠를 복사 하는지 염두에서에 둬야 합니다. Toomanually 필요한 hello 이전 계정 toohello 새 계정에서 사용 하는 모든 액세스 제어 목록 (Acl)을 적용 합니다. 최상의 시나리오에 대 한 성능 목표를 비롯 한 자세한 내용은 참조 hello [복사 활동 성능 및 조정 가이드](../data-factory/data-factory-copy-activity-performance.md)합니다. 좀 더 빠르게 복사할 데이터를 원하는 경우 해야 toouse 클라우드 데이터 이동을 단위를 추가 합니다. AdlCopy와 같은 기타 도구는 지역 간에 데이터를 복사하도록 지원하지 않습니다.  

* **대역폭 요금** Azure 지역 외부에서 데이터를 전송하기 때문에 [대역폭 요금](https://azure.microsoft.com/en-us/pricing/details/bandwidth/)이 적용됩니다.

* **데이터에 대한 ACL** Acl toofiles 및 폴더를 적용 하 여 hello 새 영역에서 데이터를 보호 합니다. 자세한 내용은 [Azure Data Lake Store에 저장된 데이터 보안](data-lake-store-secure-data.md)을 참조하세요. 마이그레이션 tooupdate hello를 사용 하 여 Acl을 조정 하는 것이 좋습니다. Toouse 설정을 비슷한 tooyour 현재 설정을 할 수 있습니다. Hello Acl hello Azure 포털을 사용 하 여 적용 된 tooany 파일을 볼 수 있습니다 [PowerShell cmdlet](/powershell/module/azurerm.datalakestore/get-azurermdatalakestoreitempermission), 또는 Sdk입니다.  

* **분석 서비스의 위치** 최상의 성능을 위해 Azure 데이터 레이크 분석 또는 Azure HDInsight를 사용 하 여 분석 서비스를 hello에 있어야 데이터와 동일한 영역입니다.  

## <a name="next-steps"></a>다음 단계
* [Azure 데이터 레이크 저장소 개요](data-lake-store-overview.md)
