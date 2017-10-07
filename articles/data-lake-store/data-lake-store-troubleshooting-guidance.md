---
title: "Azure 데이터 레이크 저장소에 대 한 질문과 aaaFrequently | Microsoft Docs"
description: "Azure Data Lake Store와 관련된 문제를 해결 또는 완화에 대한 지침"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf7fd555-3e30-43ce-b28c-c3ad0a241fdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: eeabdeef18f3b72901bd1a14283f85dd9c0ead44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-data-lake-store"></a>Azure Data Lake Store에 대한 질문과 대답
이 문서에 대 한 Faq 관련된 tooAzure 데이터 레이크 저장소는 방법을 배웁니다.

## <a name="how-can-i-further-protect-my-data-from-region-wide-disasters-or-accidental-deletions"></a>어떻게 영역 전체의 재해 또는 실수로 인한 삭제로부터 내 데이터를 추가로 보호할 수 있나요?
Azure Data Lake 저장소 계정이 hello 데이터는 자동화 된 복제본을 통해 영역 내에서 복원 tootransient 하드웨어 오류입니다. 이렇게 하면 내 구성과 고가용성 회의 hello Azure 데이터 레이크 저장소 SLA 합니다. Toofurther 드문 전체 지역 가동 중단 또는 실수로 인 한 삭제에서 데이터를 보호 하는 방법에 몇 가지 지침이입니다.

### <a name="disaster-recovery-guidance"></a>재해 복구 지침
모든 고객 tooprepare에는 자신의 재해 복구 계획 합니다. 재해 복구 계획 toohello toobuild 아래 Azure 문서 키를 읽어보십시오. 여기에는 고유한 계획을 직접 만들 수 있는 리소스가 있습니다.

* [Azure 응용 프로그램에 대한 재해 복구 및 고가용성](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)
* [Azure 복구력 기술 지침](../resiliency/resiliency-technical-guidance.md)

#### <a name="best-practices"></a>모범 사례
재해 복구 계획의 주파수 정렬 toohello 요구를 사용 하 여 다른 영역에 데이터 레이크 저장소 계정에 중요 한 데이터 tooanother을 복사 해야 하는 것이 좋습니다. 다양 한 메서드 toocopy 데이터 등 [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) 또는 [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)합니다. Azure Data Factory는 반복적으로 데이터 이동 파이프라인을 만들고 배포하기 위한 유용한 서비스입니다.

지역 가동 중단 발생 하는 경우 데이터 hello 데이터 복사 된 hello 영역에 액세스할 수 있습니다. Hello를 모니터링할 수 있습니다 [Azure 서비스 상태 대시보드에서](https://azure.microsoft.com/status/) toodetermine hello hello 전세계 Azure 서비스 상태입니다.

### <a name="data-corruption-or-accidental-deletion-recovery-guidance"></a>데이터 손상 또는 삭제 실수 복구 지침
Azure Data Lake Store가 자동화된 복제본을 통해 데이터 복원력을 제공하는 반면 이렇게 하더라도 응용 프로그램(또는 개발자/사용자)의 데이터를 손상시키거나 실수로 삭제하지 않도록 방지하지 않습니다.

#### <a name="best-practices"></a>모범 사례
tooprevent 실수로 삭제 데이터 레이크 저장소 계정에 대 한 hello 올바른 액세스 정책을 먼저 설정 하는 것이 좋습니다.  여기에 적용 [Azure 리소스 잠금을](../azure-resource-manager/resource-group-lock-resources.md) 으로 중요 한 리소스를 사용할 수 있는 hello를 사용 하 여 적용 계정 및 파일 수준 액세스 제어 아래로 toolock [데이터 레이크 저장소 보안 기능](data-lake-store-security-overview.md)합니다. 다른 Data Lake Store 계정, 폴더 또는 Azure 구독에서 [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) 또는 [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)를 사용하여 중요한 데이터의 복사본을 정기적으로 만드는 것이 좋습니다.  이 경우 데이터 손상 또는 삭제 인시던트에서 사용 되는 toorecover 수 있습니다. Azure Data Factory는 반복적으로 데이터 이동 파이프라인을 만들고 배포하기 위한 유용한 서비스입니다.

또한 조직에서는 사용할 수 [진단 로깅](data-lake-store-diagnostic-logs.md) 자신의 Azure 데이터 레이크 저장소 계정 toocollect 삭제 하거나 파일을 업데이트 수는 방법에 대 한 정보를 제공 하는 데이터 액세스 감사 내역은 대 한 합니다.

## <a name="next-steps"></a>다음 단계
* [Azure Data Lake Store 시작](data-lake-store-get-started-portal.md)
* [데이터 레이크 저장소의 데이터 보호](data-lake-store-secure-data.md)

