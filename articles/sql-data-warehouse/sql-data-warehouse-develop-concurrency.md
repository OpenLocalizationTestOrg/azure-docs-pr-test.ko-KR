---
title: "SQL 데이터 웨어하우스에 aaaConcurrency 및 작업 관리 | Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 동시성 및 워크로드 관리를 이해합니다."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 08/23/2017
ms.author: joeyong;barbkess;kavithaj
ms.openlocfilehash: 7f7e77aa687760252aed16573b609817ed9111c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a>SQL 데이터 웨어하우스의 동시성 및 워크로드 관리
Microsoft Azure SQL 데이터 웨어하우스 규모에 예측 가능한 성능을 toodeliver를 사용 하면 메모리 및 CPU 우선 순위와 같은 리소스 할당 및 동시성 수준을 제어 합니다. 이 문서는 두 기능이 모두 방법을 구현한 데이터 웨어하우스에서 해당를 제어 하는 방법에 대해 동시성 및 작업 관리 toohello 개념을 소개 합니다. SQL 데이터 웨어하우스 작업 관리는 의도 한 toohelp 다중 사용자 환경을 지원 합니다. 다중 테넌트 워크로드용은 아닙니다.

## <a name="concurrency-limits"></a>동시성 한도
SQL 데이터 웨어하우스 too1, 024 동시 연결을 허용합니다. 1,024개의 모든 연결을 통해 동시에 쿼리를 제출할 수 있습니다. 그러나 toooptimize 처리량, SQL 데이터 웨어하우스는 각 쿼리는 최소 메모리 부여를 받을 일부 쿼리 tooensure를 대기할 수 있습니다. 쿼리 실행 시 큐에 대기하기가 발생합니다. 큐 쿼리 별 총 처리량을 활성 쿼리 가져올 액세스 toocritically 되도록 하 여 동시성 제한에 도달 하면 SQL 데이터 웨어하우스를 늘릴 수 메모리 리소스를 필요 합니다.  

동시성 한도는 *동시 쿼리 수* 및 *동시성 슬롯 수*라는 두 개념에 의해 제어됩니다. 쿼리 tooexecute에 대 한 것 hello 동시성 슬롯 할당와 hello 쿼리 동시성 제한 내에서 실행 해야 합니다.

* 동시 쿼리는 hello hello에 동일한 실행 시간입니다. SQL 데이터 웨어하우스 DWU 크기가 더 커지면 hello에 too32 동시 쿼리를 지원합니다.
* 동시성 슬롯은 DWU를 기준으로 할당됩니다. 100개의 DWU마다 4개의 동시성 슬롯을 제공합니다. 예를 들어 DW100은 4개의 동시성 슬롯을 할당하고, DW1000은 40개를 할당합니다. 하나 이상의 동시성을 슬롯 hello에 종속를 사용 하는 각 쿼리 [리소스 클래스](#resource-classes) hello 쿼리 합니다. Hello smallrc 리소스 클래스에서 실행 되는 쿼리 동시성 슬롯 하나를 사용 합니다. 상위 리소스 클래스에서 실행되는 쿼리는 더 많은 동시성 슬롯을 사용합니다.

hello 다음 설명 동시 쿼리 및 동시성 슬롯 hello에 모두에 대 한 hello도 다양 한 DWU 크기입니다.

### <a name="concurrency-limits"></a>동시성 한도
| DWU | 최대 동시 쿼리 수 | 할당된 동시성 슬롯 수 |
|:--- |:---:|:---:|
| DW100 |4 |4 |
| DW200 |8 |8 |
| DW300 |12 |12 |
| DW400 |16 |16 |
| DW500 |20 |20 |
| DW600 |24 |24 |
| DW1000 |32 |40 |
| DW1200 |32 |48 |
| DW1500 |32 |60 |
| DW2000 |32 |80 |
| DW3000 |32 |120 |
| DW6000 |32 |240 |

이러한 임계값 중 하나가 충족되면 새 쿼리가 큐에 추가되고 선입선출 방식으로 실행됩니다.  쿼리를 완료 하 고 hello 쿼리 및 슬롯 이하가 hello 제한을 큐에 넣은 쿼리에 해제 됩니다. 

> [!NOTE]  
> *선택* 쿼리 실행에 동적 관리 뷰 (Dmv) 또는 카탈로그 뷰는 영향을 받지 않는 hello 동시성 제한 중 하나입니다. Hello에 실행 하는 쿼리 수에 관계 없이 hello 시스템을 모니터링할 수 있습니다.
> 
> 

## <a name="resource-classes"></a>리소스 클래스
리소스 클래스 메모리 할당 및 tooa 쿼리를 지정 하는 CPU 주기를 제어할 수 있습니다. 두 가지 유형의 데이터베이스 역할의 hello 형태로 클래스 tooa 사용자 리소스를 할당할 수 있습니다. hello 두 형식의 리소스 클래스는 다음과 같습니다.
1. 동적 리소스 클래스 (**smallrc, mediumrc, largerc, xlargerc**) 가변적인 양의 hello에 따라 메모리를 할당할 현재 DWU 합니다. 즉, tooa 수직 큰 DWU 쿼리에 더 많은 메모리가 자동으로 부여 합니다. 
2. 정적 리소스 클래스 (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) hello 할당 같은 크기에 관계 없이 메모리의 현재 DWU hello (있는 경우 자체 DWU hello 충분 한 메모리가). 즉, 더 큰 DWU에서는 각 리소스 클래스에서 동시에 더 많은 쿼리를 실행할 수 있습니다.

**smallrc** 및 **staticrc10**의 사용자에게 더 적은 양의 메모리가 주어져 더 높은 동시성을 활용할 수 있습니다. 반면, 너무 사용자에 게 할당**xlargerc** 또는 **staticrc80** 많은 양의 메모리를 제공 및 따라서 적은 수의 쿼리 동시에 실행할 수 있습니다.

기본적으로 각 사용자는 hello 작은 리소스 클래스의 멤버는 **smallrc**합니다. 프로시저 hello `sp_addrolemember` 은 tooincrease hello 리소스 클래스를 사용 하 고 `sp_droprolemember` 은 toodecrease hello 리소스 클래스를 사용 합니다. 예를 들어이 명령은 늘어나기 loaduser의 hello 리소스 클래스 너무**largerc**:

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a>리소스 클래스를 인식하지 않는 쿼리

더 큰 메모리를 할당해도 별로 도움이 되지 않는 일부 쿼리 형식이 있습니다. hello 시스템의 리소스 클래스 할당 건너뛰고 대신 hello 작은 리소스 클래스에서 이러한 쿼리를 항상 실행 합니다. 이러한 쿼리는 항상 hello 작은 리소스 클래스에서 실행 하는 경우 동시성 슬롯 압력을 받고 있기 하 고 필요한 것 보다 더 많은 슬롯이 사용 되지 않습니다은 실행할 수 있습니다. 자세한 내용은 [리소스 클래스 예외](#query-exceptions-to-concurrency-limits) 를 참조하세요.

## <a name="details-on-resource-class-assignment"></a>리소스 클래스 할당에 대한 세부 정보


리소스 클래스에 대한 추가적인 몇 가지 자세한 정보.

* *역할 alter* 권한이 필요 합니다는 사용자의 toochange hello 리소스 클래스입니다.
* 사용자 tooone 또는 그 이상의 hello 더 높은 리소스 클래스를 추가할 수 있지만 동적 리소스 클래스가 정적 리소스 클래스 보다 우선 합니다. 즉, 사용자 tooboth 지정 되 면 **mediumrc**(동적) 및 **staticrc80**(정적) **mediumrc** 적용 되므로 hello 리소스 클래스입니다.
 * 사용자는 특정 리소스 클래스 형식 (여러 개의 동적 리소스 클래스 또는 여러 개의 정적 리소스 클래스)에 자원 하나씩 클래스 보다 toomore에 할당 된 hello 가장 높은 리소스 클래스는 인식 됩니다. 즉, 사용자는 tooboth mediumrc 및 largerc 할당 되 면 hello 더 높은 리소스 클래스 (largerc) 적용 됩니다. 경우에 사용자가 할당 tooboth **staticrc20** 및 **statirc80**, **staticrc80** 적용 됩니다.
* hello 시스템 관리자가 사용자의 hello 리소스 클래스를 변경할 수 없습니다.

자세한 예제는 [사용자 리소스 클래스 변경 예제](#changing-user-resource-class-example)를 참조하세요.

## <a name="memory-allocation"></a>메모리 할당
사용자의 리소스 클래스 장점 및 단점 tooincreasing이 됩니다. 증가 하는 사용자에 대 한 리소스 클래스를 의미할 수 있습니다. 쿼리 실행 속도가 빨라집니다 액세스 toomore 메모리 쿼리를 제공 합니다.  그러나 더 높은 리소스 클래스 hello를 실행할 수 있는 동시 쿼리 수가 줄일 수도 있습니다. 이 hello 기능 손실을 절충 많은 양의 메모리 tooa 단일 쿼리를 할당 하거나 toorun 동시에 메모리 할당 해야 하는 다른 쿼리를 허용 합니다. 액세스 toothat 한 명의 사용자 높은 쿼리에 대 한 메모리 할당 인 경우 다른 사용자에 게는 없습니다 동일한 메모리 toorun 쿼리 합니다.

다음 표에서 hello tooeach 배포 DWU 및 리소스 클래스에 의해 할당 된 hello 메모리를 매핑합니다.

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a>동적 리소스 클래스에 대한 배포별 메모리 할당(MB)
| DWU | smallrc | mediumrc | largerc | xlargerc |
|:--- |:---:|:---:|:---:|:---:|
| DW100 |100 |100 |200 |400 |
| DW200 |100 |200 |400 |800 |
| DW300 |100 |200 |400 |800 |
| DW400 |100 |400 |800 |1,600 |
| DW500 |100 |400 |800 |1,600 |
| DW600 |100 |400 |800 |1,600 |
| DW1000 |100 |800 |1,600 |3,200 |
| DW1200 |100 |800 |1,600 |3,200 |
| DW1500 |100 |800 |1,600 |3,200 |
| DW2000 |100 |1,600 |3,200 |6,400 |
| DW3000 |100 |1,600 |3,200 |6,400 |
| DW6000 |100 |3,200 |6,400 |12,800 |

다음 표에서 hello hello 메모리를 할당 된 tooeach 배포 DWU 정적 리소스 클래스에 매핑합니다. 리소스 클래스 일수록 hello가 메모리 감소 toohonor hello 글로벌 DWU 제한 합니다.

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a>정적 리소스 클래스에 대한 배포별 메모리 할당(MB)
| DWU | staticrc10 | staticrc20 | staticrc30 | staticrc40 | staticrc50 | staticrc60 | staticrc70 | staticrc80 |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |100 |200 |400 |400 |400 |400 |400 |400 |
| DW200 |100 |200 |400 |800 |800 |800 |800 |800 |
| DW300 |100 |200 |400 |800 |800 |800 |800 |800 |
| DW400 |100 |200 |400 |800 |1,600 |1,600 |1,600 |1,600 |
| DW500 |100 |200 |400 |800 |1,600 |1,600 |1,600 |1,600 |
| DW600 |100 |200 |400 |800 |1,600 |1,600 |1,600 |1,600 |
| DW1000 |100 |200 |400 |800 |1,600 |3,200 |3,200 |3,200 |
| DW1200 |100 |200 |400 |800 |1,600 |3,200 |3,200 |3,200 |
| DW1500 |100 |200 |400 |800 |1,600 |3,200 |3,200 |3,200 |
| DW2000 |100 |200 |400 |800 |1,600 |3,200 |6,400 |6,400 |
| DW3000 |100 |200 |400 |800 |1,600 |3,200 |6,400 |6,400 |
| DW6000 |100 |200 |400 |800 |1,600 |3,200 |6,400 |12,800 |

Hello 앞에 테이블을 볼 수 있습니다는 hello에 DW2000에서 실행 되는 쿼리 **xlargerc** 리소스 클래스 액세스 too6, 각 hello 60 분산된 데이터베이스 내에서 메모리의 400MB 해야 합니다.  SQL 데이터 웨어하우스에는 배포가 60개 있습니다. 따라서 지정 된 리소스 클래스에서 쿼리를 값 위에 hello에 대 한 toocalculate hello 총 메모리 할당이 60을 곱합니다 수 해야 합니다.

### <a name="memory-allocations-system-wide-gb"></a>시스템 전체 메모리 할당(GB)
| DWU | smallrc | mediumrc | largerc | xlargerc |
|:--- |:---:|:---:|:---:|:---:|
| DW100 |6 |6 |12 |23 |
| DW200 |6 |12 |23 |47 |
| DW300 |6 |12 |23 |47 |
| DW400 |6 |23 |47 |94 |
| DW500 |6 |23 |47 |94 |
| DW600 |6 |23 |47 |94 |
| DW1000 |6 |47 |94 |188 |
| DW1200 |6 |47 |94 |188 |
| DW1500 |6 |47 |94 |188 |
| DW2000 |6 |94 |188 |375 |
| DW3000 |6 |94 |188 |375 |
| DW6000 |6 |188 |375 |750 |

이 테이블은 시스템 차원의 메모리 할당을 볼 수 있습니다 hello xlargerc 리소스 클래스에서 DW2000에서 실행 되는 쿼리는 총 메모리의 375 GB가 할당 되는 (6,400 MB * 60 분포 / 1, 024 tooconvert tooGB) hello 전체 SQL 데이터 웨어하우스를 통해 합니다.

hello 같은 계산 적용 toostatic 리소스 클래스입니다.
 
## <a name="concurrency-slot-consumption"></a>동시성 슬롯 사용량  
SQL 데이터 웨어하우스 더 높은 리소스 클래스에서 실행 되는 더 많은 메모리 tooqueries 권한을 부여 합니다. 메모리는 고정된 리소스입니다.  쿼리를 더 적은 수의 동시 쿼리를 실행할 수는 hello 당 더 많은 메모리 할당 번호 따라서입니다. hello 다음 표에서 reiterates 모든 hello DWU에서 사용할 수 있는 동시성 슬롯 및 각 리소스 클래스에서 사용 하는 hello 슬롯 수를 표시 하는 단일 뷰에서 hello 이전 개념입니다.  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a>동적 리소스 클래스에 대한 동시성 슬롯의 할당 및 사용량  
| DWU | 최대 동시 쿼리 수 | 할당된 동시성 슬롯 수 | smallrc에서 사용되는 슬롯 | mediumrc에서 사용되는 슬롯 | largerc에서 사용되는 슬롯 | xlargerc에서 사용되는 슬롯 |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |4 |4 |1 |1 |2 |4 |
| DW200 |8 |8 |1 |2 |4 |8 |
| DW300 |12 |12 |1 |2 |4 |8 |
| DW400 |16 |16 |1 |4 |8 |16 |
| DW500 |20 |20 |1 |4 |8 |16 |
| DW600 |24 |24 |1 |4 |8 |16 |
| DW1000 |32 |40 |1 |8 |16 |32 |
| DW1200 |32 |48 |1 |8 |16 |32 |
| DW1500 |32 |60 |1 |8 |16 |32 |
| DW2000 |32 |80 |1 |16 |32 |64 |
| DW3000 |32 |120 |1 |16 |32 |64 |
| DW6000 |32 |240 |1 |32 |64 |128 |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a>정적 리소스 클래스에 대한 동시성 슬롯의 할당 및 사용량  
| DWU | 최대 동시 쿼리 수 | 할당된 동시성 슬롯 수 |staticrc10 | staticrc20 | staticrc30 | staticrc40 | staticrc50 | staticrc60 | staticrc70 | staticrc80 |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |4 |4 |1 |2 |4 |4 |4 |4 |4 |4 |
| DW200 |8 |8 |1 |2 |4 |8 |8 |8 |8 |8 |
| DW300 |12 |12 |1 |2 |4 |8 |8 |8 |8 |8 |
| DW400 |16 |16 |1 |2 |4 |8 |16 |16 |16 |16 |
| DW500 | 20| 20| 1| 2| 4| 8| 16| 16| 16| 16|
| DW600 | 24| 24| 1| 2| 4| 8| 16| 16| 16| 16|
| DW1000 | 32| 40| 1| 2| 4| 8| 16| 32| 32| 32|
| DW1200 | 32| 48| 1| 2| 4| 8| 16| 32| 32| 32|
| DW1500 | 32| 60| 1| 2| 4| 8| 16| 32| 32| 32|
| DW2000 | 32| 80| 1| 2| 4| 8| 16| 32| 64| 64|
| DW3000 | 32| 120| 1| 2| 4| 8| 16| 32| 64| 64|
| DW6000 | 32| 240| 1| 2| 4| 8| 16| 32| 64| 128|

이러한 테이블에서 볼 수 있는 것처럼 DW1000으로 실행되는 SQL 데이터 웨어하우스는 최대 32개의 동시 쿼리 및 총 40개의 동시성 슬롯을 할당합니다. 모든 사용자가 smallrc에서 실행하는 경우 각 쿼리가 동시성 슬롯 1개를 소비하므로 32개의 동시성 쿼리가 허용됩니다. 모든 사용자는 DW1000에 mediumrc에서 실행 중이 던, 각 쿼리에 쿼리당 47 gb 전체 메모리 할당에 대 한 분포 당 800MB를 할당할 수는 동시성 개이고 경우 제한 too5 사용자 (40 동시성 슬롯 / mediumrc 사용자 당 8 슬롯이).

## <a name="selecting-proper-resource-class"></a>적절한 리소스 클래스 선택  
일반적으로 해당 리소스 클래스를 변경 하는 대신 toopermanently assign users tooa 리소스 클래스 됩니다. 예를 들어 로드 tooclustered columnstore 테이블 더 많은 메모리를 할당 하는 경우 더 높은 품질 인덱스를 만듭니다. tooensure 로드가 toohigher 메모리를 액세스, 사용자 데이터 로드에 맞게를 만들고이 사용자 tooa 더 높은 리소스 클래스를 영구적으로 할당 합니다.
모범 사례 toofollow 여기에 두 가지가 있습니다. 위에서 언급한 것처럼 SQL DW에서는 두 가지 유형의 리소스 클래스 형식, 즉 정적 리소스 클래스 및 동적 리소스 클래스를 지원합니다.
### <a name="loading-best-practices"></a>로드 모범 사례
1.  Hello 기대 일반 양의 데이터를 사용 하 여 로드 인 정적 리소스 클래스는 것이 좋습니다. 나중 더 많은 컴퓨팅 기능, 데이터 웨어하우스 hello tooget 수직 확장 수 없게 됩니다 toorun 더 많은 동시 쿼리 기본, 대로 hello 부하 사용자는 더 많은 메모리를 사용 하지 않습니다.
2.  Hello 기대 인 큰 부하 일부 경우에는 동적 리소스 클래스는 것이 좋습니다. 이상에서는 tooget, 더 많은 계산 능력이 늘릴 때 hello 부하 사용자가 알 더 많은 메모리-의-즉시 사용, 따라서 hello 부하 tooperform를 더 빠르게 허용.

hello 필요한 메모리 tooprocess 로드 효율적으로 hello 특성에 따라 결정 hello 테이블 로드 및 처리 된 데이터 양을 hello 합니다. 예를 들어, CCI 테이블로 데이터 로드 일부 메모리 toolet CCI rowgroup 한 최적 성을 도달 해야 합니다. 자세한 내용은 hello Columnstore 인덱스 데이터 로드 작업 지침을 참조 하십시오.

모범 사례로, 좋습니다 toouse 최소한 200MB의 메모리 로드를 합니다.

### <a name="querying-best-practices"></a>쿼리 모범 사례
쿼리마다 복잡성에 따라 다른 요구 사항을 갖습니다. 쿼리당 메모리를 늘리거나 hello 동시성은 증가 모두 올바른 방법 tooaugment hello 쿼리 요구에 따라 전체 처리량입니다.
1.  Hello 기대는 정기적이 고 복잡 한 쿼리 하는 경우 (예를 들어, toogenerate 매일 및 매주 보고서) 및 동시성 tootake 활용 필요 하지 않습니다, 동적 리소스 클래스는 것이 좋습니다. Hello 시스템에 더 많은 데이터 tooprocess 경우 hello 데이터 웨어하우스를 확장 합니다. 따라서을 자동으로 제공 더 많은 메모리 toohello 사용자 hello 쿼리를 실행 합니다.
2.  변수 또는 diurnal 동시성 패턴 hello 기대 하는 경우 (예를 들어 웹 광범위 하 게 액세스할 수 있는 UI 통해 hello 데이터베이스를 쿼리 하는 경우), 정적 리소스 클래스는 것이 좋습니다. 이상에서는 toodata 웨어하우스를 확장 하는 경우 hello 정적 리소스 클래스와 관련 된 hello 사용자가을 자동으로 더 많은 동시 쿼리가 수 toorun 될 합니다.

쿼리 hello 요구에 따라 적절 한 메모리 부여를 선택 하는 hello 테이블 스키마 및 다양 한 조인, 선택 영역 및 그룹 조건자의 hello 특성 hello 쿼리, 데이터 양 등의 많은 요인에 의존 하므로 간단한, 합니다. 쿼리 toocomplete 속도가 더 하면 있지만 높이면 더 많은 메모리 할당 하는 일반 관점에서 전반적인 동시성 hello 합니다. 동시성이 문제가 되지 않을 경우 메모리를 과도하게 할당해도 괜찮습니다. toofine 조정 처리량, 다양 한 리소스 클래스를 시도 필요할 수 있습니다.

Hello 다음 저장을 사용할 수 있습니다에 지정된 된 SLO 및 hello 가장 가까운 최상의 리소스 클래스에 대 한 메모리 집약적 CCI 작업에 지정 된 리소스 클래스 CCI 테이블 분할 되지 않은 리소스 클래스당 동시성 및 메모리 부여 아웃 toofigure 프로시저:

#### <a name="description"></a>설명:  
이 저장된 프로시저의 hello 용도 다음과 같습니다.  
1. 지정 된 SLO에 리소스 클래스당 동시성 및 메모리 부여 아웃 toohelp 사용자 그림입니다. 아래 hello 예에 나와 있는 것 처럼 사용자 tooprovide NULL 스키마와 테이블 이름에 대 한이 필요 합니다.  
2. 지정 된 리소스 클래스에서 아닌 분할된 CCI 테이블에 대해 CCI 작업 (로드, 테이블 복사 다시 인덱스 등 빌드) hello 가장 가까운 최상의 리소스에 대 한 클래스 hello 메모리 intensed toohelp 사용자 계산 합니다. 테이블 스키마 toofind 아웃 hello 필요한 메모리 부여를 사용 하 여이 대 한 hello 저장 프로시저.

#### <a name="dependencies--restrictions"></a>종속성 및 제한 사항:
- 이 저장된 프로시저 cci를 분할 된 테이블에 대 한 디자인 된 toocalculate 메모리 요구 사항이 아닙니다.    
- 이 저장된 프로시저의 SELECT/INSERT-CTAS hello SELECT 부분에 대 한 계정으로 메모리 요구 사항이 사용 하지 않습니다 및 toobe 간단한 SELECT를 가정 합니다.
- 이 저장된 프로시저를이 사용할 수 있도록 hello 세션에서이 저장된 프로시저가 생성 된 임시 테이블을 사용 합니다.    
- 이 저장된 프로시저를 hello 현재 제품 (예: 하드웨어 구성, DMS 구성)에 따라 달라 집니다 하 고는 식의 변경 되 면 다음이 저장된 프로시저를 올바르게 작동 하지 않습니다.  
- 이 저장 프로시저는 기존의 제공된 동시성 제한에 의존하므로 이러한 동시성 제한이 변경되면 이 저장 프로시저가 제대로 작동하지 않습니다.  
- 이 저장 프로시저는 기존에 제공된 리소스 클래스에 의존하므로 이러한 리소스 클래스가 변경되면 이 저장 프로시저가 제대로 작동하지 않습니다.  

>  [!NOTE]  
>  제공된 매개 변수로 저장 프로시저를 실행한 후에 출력이 표시되지 않으면 다음 2가지 경우로 가정할 수 있습니다. <br />1. DW 매개 변수 중 하나에 잘못된 SLO 값이 포함되어 있습니다. <br />2. 또는 테이블 이름이 제공된 경우 CCI 작업에 대해 일치하는 리소스 클래스가 없습니다. <br />예를 들어 DW100, 사용 가능한 가장 높은 메모리 부여 400MB 하 고 충분 한 toocross hello 요구 사항은 400mb 테이블 스키마는 넓은 경우.
      
#### <a name="usage-example"></a>사용법 예제:
구문  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. @DWU:NULL 매개 변수 tooextract 제공 하거나 hello DW DB에서에서 현재 DWU hello 또는 지원 되는 모든 DWU 'DW100' hello 형태로 제공 합니다.
2. @SCHEMA_NAME:Hello 테이블의 스키마 이름 제공
3. @TABLE_NAME:Hello 관심 있는 테이블 이름을 제공합니다

이 저장 프로시저 실행 예제:  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

아래와 같이 hello 위의 예제에서에서 사용 하는 표 1은 만들 수 있습니다.  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-hello-stored-procedure-definition"></a>Hello 저장 프로시저 정의 다음과 같습니다.
```sql  
-------------------------------------------------------------------------------
-- Dropping prc_workload_management_by_DWU procedure if it exists.
-------------------------------------------------------------------------------
IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'prc_workload_management_by_DWU')
DROP PROCEDURE dbo.prc_workload_management_by_DWU
GO

-------------------------------------------------------------------------------
-- Creating prc_workload_management_by_DWU.
-------------------------------------------------------------------------------
CREATE PROCEDURE dbo.prc_workload_management_by_DWU
(   @DWU VARCHAR(7),
      @SCHEMA_NAME VARCHAR(128),
       @TABLE_NAME VARCHAR(128)
)
AS
IF @DWU IS NULL
BEGIN
-- Selecting proper DWU for hello current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need toosupply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) toohold mapping info.
-- CREATE TABLE #ref
CREATE TABLE #ref
WITH (DISTRIBUTION = ROUND_ROBIN)
AS 
WITH
-- Creating concurrency slots mapping for various DWUs.
alloc
AS
(
  SELECT 'DW100' AS DWU, 4 AS max_queries, 4 AS max_slots, 1 AS slots_used_smallrc, 1 AS slots_used_mediumrc,
        2 AS slots_used_largerc, 4 AS slots_used_xlargerc, 1 AS slots_used_staticrc10, 2 AS slots_used_staticrc20,
        4 AS slots_used_staticrc30, 4 AS slots_used_staticrc40, 4 AS slots_used_staticrc50,
        4 AS slots_used_staticrc60, 4 AS slots_used_staticrc70, 4 AS slots_used_staticrc80
  UNION ALL
    SELECT 'DW200', 8, 8, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW300', 12, 12, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW400', 16, 16, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
     SELECT 'DW500', 20, 20, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW600', 24, 24, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW1000', 32, 40, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1200', 32, 48, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1500', 32, 60, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW2000', 32, 80, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
   SELECT 'DW3000', 32, 120, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
    SELECT 'DW6000', 32, 240, 1, 32, 64, 128, 1, 2, 4, 8, 16, 32, 64, 128
)
-- Creating workload mapping tootheir corresponding slot consumption and default memory grant.
,map
AS
(
  SELECT 'SloDWGroupC00' AS wg_name,1 AS slots_used,100 AS tgt_mem_grant_MB
  UNION ALL
    SELECT 'SloDWGroupC01',2,200
  UNION ALL
    SELECT 'SloDWGroupC02',4,400
  UNION ALL
    SELECT 'SloDWGroupC03',8,800
  UNION ALL
    SELECT 'SloDWGroupC04',16,1600
  UNION ALL
    SELECT 'SloDWGroupC05',32,3200
  UNION ALL
    SELECT 'SloDWGroupC06',64,6400
  UNION ALL
    SELECT 'SloDWGroupC07',128,12800
)
-- Creating ref based on current / asked DWU.
, ref
AS
(
  SELECT  a1.*
  ,       m1.wg_name          AS wg_name_smallrc
  ,       m1.tgt_mem_grant_MB AS tgt_mem_grant_MB_smallrc
  ,       m2.wg_name          AS wg_name_mediumrc
  ,       m2.tgt_mem_grant_MB AS tgt_mem_grant_MB_mediumrc
  ,       m3.wg_name          AS wg_name_largerc
  ,       m3.tgt_mem_grant_MB AS tgt_mem_grant_MB_largerc
  ,       m4.wg_name          AS wg_name_xlargerc
  ,       m4.tgt_mem_grant_MB AS tgt_mem_grant_MB_xlargerc
  ,       m5.wg_name          AS wg_name_staticrc10
  ,       m5.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc10
  ,       m6.wg_name          AS wg_name_staticrc20
  ,       m6.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc20
  ,       m7.wg_name          AS wg_name_staticrc30
  ,       m7.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc30
  ,       m8.wg_name          AS wg_name_staticrc40
  ,       m8.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc40
  ,       m9.wg_name          AS wg_name_staticrc50
  ,       m9.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc50
  ,       m10.wg_name          AS wg_name_staticrc60
  ,       m10.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc60
  ,       m11.wg_name          AS wg_name_staticrc70
  ,       m11.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc70
  ,       m12.wg_name          AS wg_name_staticrc80
  ,       m12.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc80
  FROM alloc a1
  JOIN map   m1  ON a1.slots_used_smallrc     = m1.slots_used
  JOIN map   m2  ON a1.slots_used_mediumrc    = m2.slots_used
  JOIN map   m3  ON a1.slots_used_largerc     = m3.slots_used
  JOIN map   m4  ON a1.slots_used_xlargerc    = m4.slots_used
  JOIN map   m5  ON a1.slots_used_staticrc10    = m5.slots_used
  JOIN map   m6  ON a1.slots_used_staticrc20    = m6.slots_used
  JOIN map   m7  ON a1.slots_used_staticrc30    = m7.slots_used
  JOIN map   m8  ON a1.slots_used_staticrc40    = m8.slots_used
  JOIN map   m9  ON a1.slots_used_staticrc50    = m9.slots_used
  JOIN map   m10  ON a1.slots_used_staticrc60    = m10.slots_used
  JOIN map   m11  ON a1.slots_used_staticrc70    = m11.slots_used
  JOIN map   m12  ON a1.slots_used_staticrc80    = m12.slots_used
-- WHERE   a1.DWU = @DWU
  WHERE   a1.DWU = UPPER(@DWU)
)
SELECT  DWU
,       max_queries
,       max_slots
,       slots_used
,       wg_name
,       tgt_mem_grant_MB
,       up1 as rc
,       (ROW_NUMBER() OVER(PARTITION BY DWU ORDER BY DWU)) as rc_id
FROM
(
    SELECT  DWU
    ,       max_queries
    ,       max_slots
    ,       slots_used
    ,       wg_name
    ,       tgt_mem_grant_MB
    ,       REVERSE(SUBSTRING(REVERSE(wg_names),1,CHARINDEX('_',REVERSE(wg_names),1)-1)) as up1
    ,       REVERSE(SUBSTRING(REVERSE(tgt_mem_grant_MBs),1,CHARINDEX('_',REVERSE(tgt_mem_grant_MBs),1)-1)) as up2
    ,       REVERSE(SUBSTRING(REVERSE(slots_used_all),1,CHARINDEX('_',REVERSE(slots_used_all),1)-1)) as up3
    FROM    ref AS r1
    UNPIVOT
    (
        wg_name FOR wg_names IN (wg_name_smallrc,wg_name_mediumrc,wg_name_largerc,wg_name_xlargerc,
        wg_name_staticrc10, wg_name_staticrc20, wg_name_staticrc30, wg_name_staticrc40, wg_name_staticrc50,
        wg_name_staticrc60, wg_name_staticrc70, wg_name_staticrc80)
    ) AS r2
    UNPIVOT
    (
        tgt_mem_grant_MB FOR tgt_mem_grant_MBs IN (tgt_mem_grant_MB_smallrc,tgt_mem_grant_MB_mediumrc,
        tgt_mem_grant_MB_largerc,tgt_mem_grant_MB_xlargerc, tgt_mem_grant_MB_staticrc10, tgt_mem_grant_MB_staticrc20,
        tgt_mem_grant_MB_staticrc30, tgt_mem_grant_MB_staticrc40, tgt_mem_grant_MB_staticrc50,
        tgt_mem_grant_MB_staticrc60, tgt_mem_grant_MB_staticrc70, tgt_mem_grant_MB_staticrc80)
    ) AS r3
    UNPIVOT
    (
        slots_used FOR slots_used_all IN (slots_used_smallrc,slots_used_mediumrc,slots_used_largerc,
        slots_used_xlargerc, slots_used_staticrc10, slots_used_staticrc20, slots_used_staticrc30,
        slots_used_staticrc40, slots_used_staticrc50, slots_used_staticrc60, slots_used_staticrc70,
        slots_used_staticrc80)
    ) AS r4
) a
WHERE   up1 = up2
AND     up1 = up3
;
-- Getting current info about workload groups.
WITH  
dmv  
AS  
(
  SELECT
          rp.name                                           AS rp_name
  ,       rp.max_memory_kb*1.0/1048576                      AS rp_max_mem_GB
  ,       (rp.max_memory_kb*1.0/1024)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_MB
  ,       (rp.max_memory_kb*1.0/1048576)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_GB
  ,       wg.name                                           AS wg_name
  ,       wg.importance                                     AS importance
  ,       wg.request_max_memory_grant_percent               AS request_max_memory_grant_percent
  FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
  JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    ON  wg.pdw_node_id  = rp.pdw_node_id
                                                                  AND wg.pool_id      = rp.pool_id
  WHERE   rp.name = 'SloDWPool'
  GROUP BY
          rp.name
  ,       rp.max_memory_kb
  ,       wg.name
  ,       wg.importance
  ,       wg.request_max_memory_grant_percent
)
-- Creating resource class name mapping.
,names
AS
(
  SELECT 'smallrc' as resource_class, 1 as rc_id
  UNION ALL
    SELECT 'mediumrc', 2
  UNION ALL
    SELECT 'largerc', 3
  UNION ALL
    SELECT 'xlargerc', 4
  UNION ALL
    SELECT 'staticrc10', 5
  UNION ALL
    SELECT 'staticrc20', 6
  UNION ALL
    SELECT 'staticrc30', 7
  UNION ALL
    SELECT 'staticrc40', 8
  UNION ALL
    SELECT 'staticrc50', 9
  UNION ALL
    SELECT 'staticrc60', 10
  UNION ALL
    SELECT 'staticrc70', 11
  UNION ALL
    SELECT 'staticrc80', 12
)
,base AS
(   SELECT  schema_name
    ,       table_name
    ,       SUM(column_count)                   AS column_count
    ,       ISNULL(SUM(short_string_column_count),0)   AS short_string_column_count
    ,       ISNULL(SUM(long_string_column_count),0)    AS long_string_column_count
    FROM    (   SELECT  sm.name                                             AS schema_name
                ,       tb.name                                             AS table_name
                ,       COUNT(co.column_id)                                 AS column_count
                           ,       CASE    WHEN co.system_type_id IN (36,43,106,108,165,167,173,175,231,239) 
                                AND  co.max_length <= 32 
                                THEN COUNT(co.column_id) 
                        END                                                 AS short_string_column_count
                ,       CASE    WHEN co.system_type_id IN (165,167,173,175,231,239) 
                                AND  co.max_length > 32 and co.max_length <=8000
                                THEN COUNT(co.column_id) 
                        END                                                 AS long_string_column_count
                FROM    sys.schemas AS sm
                JOIN    sys.tables  AS tb   on sm.[schema_id] = tb.[schema_id]
                JOIN    sys.columns AS co   ON tb.[object_id] = co.[object_id]
                           WHERE tb.name = @TABLE_NAME AND sm.name = @SCHEMA_NAME
                GROUP BY sm.name
                ,        tb.name
                ,        co.system_type_id
                ,        co.max_length            ) a
GROUP BY schema_name
,        table_name
)
, size AS
(
SELECT  schema_name
,       table_name
,       75497472                                            AS table_overhead

,       column_count*1048576*8                              AS column_size
,       short_string_column_count*1048576*32                       AS short_string_size,       (long_string_column_count*16777216) AS long_string_size
FROM    base
UNION
SELECT CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as schema_name
         ,CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as table_name
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as table_overhead
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as column_size
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as short_string_size

,CASE WHEN COUNT(*) = 0 THEN 0 END as long_string_size
FROM   base
)
, load_multiplier as 
(
SELECT  CASE 
                     WHEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) > 0 THEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) 
                     ELSE 1 
              END AS multipliplication_factor
) 
       SELECT  r1.DWU
       , schema_name
       , table_name
       , rc.resource_class as closest_rc_in_increasing_order
       , max_queries_at_this_rc = CASE
             WHEN (r1.max_slots / r1.slots_used > r1.max_queries)
                  THEN r1.max_queries
             ELSE r1.max_slots / r1.slots_used
                  END
       , r1.max_slots as max_concurrency_slots
       , r1.slots_used as required_slots_for_the_rc
       , r1.tgt_mem_grant_MB  as rc_mem_grant_MB
       , CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) AS est_mem_grant_required_for_cci_operation_MB       
       FROM    size, load_multiplier, #ref r1, names  rc
       WHERE r1.rc_id=rc.rc_id
                     AND CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) < r1.tgt_mem_grant_MB
       ORDER BY ABS(CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) - r1.tgt_mem_grant_MB)
GO
```

## <a name="query-importance"></a>쿼리 중요도
SQL 데이터 웨어하우스는 워크로드 그룹을 사용하여 리소스 클래스를 구현합니다. 다양 한 DWU 크기 hello에서 hello 리소스 클래스의 hello 동작을 제어 하는 8 개의 작업 그룹의 총 가지가 있습니다. 모든 DWU에 대 한 SQL 데이터 웨어하우스 hello 8 개의 작업 그룹의 4만 사용 합니다. 각 작업 그룹의 4 개 리소스 클래스 tooone 지정 되기 때문에 이렇게 하면 의미: smallrc, mediumrc, largerc, 또는 xlargerc 합니다. hello 이해 hello 작업 그룹의 중요도 이러한 작업 그룹의 일부 설정 된다는 점 toohigher *중요도*합니다. 중요도가 CPU 예약에 사용됩니다. 높은 중요도를 갖고 실행되는 쿼리는 중간 중요도의 쿼리보다 3배 더 많은 CPU 사이클을 받게 될 것입니다. 따라서 동시성 슬롯 매핑은 또한 CPU 우선 순위를 결정합니다. 쿼리가 16개 이상의 슬롯을 사용할 경우 중요도 높음으로 실행됩니다.

hello 다음 표에 각 작업 그룹에 대 한 hello 중요도 매핑이 있습니다.

### <a name="workload-group-mappings-tooconcurrency-slots-and-importance"></a>작업 그룹 매핑 tooconcurrency 슬롯 및 중요도
| 워크로드 그룹 | 동시성 슬롯 매핑 | MB/배포 | 중요도 매핑 |
|:--- |:---:|:---:|:--- |
| SloDWGroupC00 |1 |100 |중간 |
| SloDWGroupC01 |2 |200 |중간 |
| SloDWGroupC02 |4 |400 |중간 |
| SloDWGroupC03 |8 |800 |중간 |
| SloDWGroupC04 |16 |1,600 |높음 |
| SloDWGroupC05 |32 |3,200 |높음 |
| SloDWGroupC06 |64 |6,400 |높음 |
| SloDWGroupC07 |128 |12,800 |높음 |

Hello에서 **할당 및 동시성 슬롯의 소비** 차트는 DW500에서는 1, 4, 8 또는 16 동시성 슬롯 smallrc, mediumrc, largerc, 및 xlargerc, 각각을 볼 수 있습니다. 각 리소스 클래스에 대 한 차트 toofind hello 중요도 앞 hello에 해당 값을 조회할 수 있습니다.

### <a name="dw500-mapping-of-resource-classes-tooimportance"></a>리소스 클래스 tooimportance의 DW500 매핑
| 리소스 클래스 | 워크로드 그룹 | 사용된 동시성 슬롯 수 | MB/배포 | 중요도 |
|:--- |:--- |:---:|:---:|:--- |
| smallrc |SloDWGroupC00 |1 |100 |중간 |
| mediumrc |SloDWGroupC02 |4 |400 |중간 |
| largerc |SloDWGroupC03 |8 |800 |중간 |
| xlargerc |SloDWGroupC04 |16 |1,600 |높음 |
| staticrc10 |SloDWGroupC00 |1 |100 |중간 |
| staticrc20 |SloDWGroupC01 |2 |200 |중간 |
| staticrc30 |SloDWGroupC02 |4 |400 |중간 |
| staticrc40 |SloDWGroupC03 |8 |800 |중간 |
| staticrc50 |SloDWGroupC03 |16 |1,600 |높음 |
| staticrc60 |SloDWGroupC03 |16 |1,600 |높음 |
| staticrc70 |SloDWGroupC03 |16 |1,600 |높음 |
| staticrc80 |SloDWGroupC03 |16 |1,600 |높음 |

Hello hello 차이 hello 리소스 관리자의 hello 관점 또는 hello 작업 그룹의 현재 및 이제 까지의 사용 tooanalyze 자세히 메모리 리소스 할당에서 DMV 쿼리 toolook 문제를 해결 하려면 다음을 사용할 수 있습니다.

```sql
WITH rg
AS
(   SELECT  
     pn.name                        AS node_name
    ,pn.[type]                        AS node_type
    ,pn.pdw_node_id                    AS node_id
    ,rp.name                        AS pool_name
    ,rp.max_memory_kb*1.0/1024                AS pool_max_mem_MB
    ,wg.name                        AS group_name
    ,wg.importance                    AS group_importance
    ,wg.request_max_memory_grant_percent        AS group_request_max_memory_grant_pcnt
    ,wg.max_dop                        AS group_max_dop
    ,wg.effective_max_dop                AS group_effective_max_dop
    ,wg.total_request_count                AS group_total_request_count
    ,wg.total_queued_request_count            AS group_total_queued_request_count
    ,wg.active_request_count                AS group_active_request_count
    ,wg.queued_request_count                AS group_queued_request_count
    FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
    JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    
            ON  wg.pdw_node_id  = rp.pdw_node_id
            AND wg.pool_id      = rp.pool_id
    JOIN    sys.dm_pdw_nodes pn
            ON    wg.pdw_node_id    = pn.pdw_node_id
    WHERE   wg.name like 'SloDWGroup%'
        AND     rp.name = 'SloDWPool'
)
SELECT    pool_name
,        pool_max_mem_MB
,        group_name
,        group_importance
,        (pool_max_mem_MB/100)*group_request_max_memory_grant_pcnt AS max_memory_grant_MB
,        node_name
,        node_type
,       group_total_request_count
,       group_total_queued_request_count
,       group_active_request_count
,       group_queued_request_count
FROM    rg
ORDER BY
    node_name
,    group_request_max_memory_grant_pcnt
,    group_importance
;
```

## <a name="queries-that-honor-concurrency-limits"></a>동시성 한도를 적용하는 쿼리
대부분의 쿼리는 리소스 클래스에 의해 제어됩니다. 이러한 쿼리 hello 동시 쿼리와 동시성 슬롯 임계값 내에 맞아야 합니다. 사용자는 hello 동시성 슬롯 모델에서 tooexclude 쿼리를 선택할 수 없습니다.

tooreiterate, hello 다음 문은 인식 리소스 클래스:

* INSERT-SELECT
* UPDATE
* 삭제
* SELECT(사용자 테이블을 쿼리하는 경우)
* ALTER INDEX REBUILD
* ALTER INDEX REORGANIZE
* ALTER TABLE REBUILD
* CREATE INDEX
* CREATE CLUSTERED COLUMNSTORE INDEX
* CREATE TABLE AS SELECT (CTAS)
* 데이터 로드
* Hello 데이터 이동 서비스 (DMS)을 통해 수행 되는 데이터 이동 작업

## <a name="query-exceptions-tooconcurrency-limits"></a>쿼리 예외 tooconcurrency 제한
일부 쿼리 hello 리소스를 인식 하지 못합니다 클래스 toowhich hello 사용자에 게 할당 됩니다. 특정 명령에 필요한 hello 메모리 리소스가 부족 한지, 종종 hello 명령은 메타 데이터 작업 이므로 때 이러한 예외 toohello 동시성 제한은 적용 하는 합니다. hello 이들 예외의 ´ ֲ tooavoid 더 큰 메모리 할당에 대 한 쿼리를 활용 하지 것입니다. 이러한 경우 작은 리소스 클래스 (smallrc) hello 실제 리소스 클래스에 관계 없이 항상 사용 하는 hello 기본 toohello 사용자를 할당 합니다. 예를 들어, `CREATE LOGIN` 은 항상 smallrc에서 실행됩니다. hello 필요한 리소스 toofulfill이이 작업 되므로 매우 낮은 hello 동시성 슬롯 모델에서 의미 tooinclude hello 쿼리를 만들지 않습니다.  이러한 쿼리는 또한 hello 32 사용자 동시성 제한으로 제한 되지, 이러한 쿼리 무제한 toohello 세션 제한 1, 024 세션을 실행할 수 있습니다.

다음 조건 hello 리소스 클래스를 인식 하지 못합니다.

* CREATE 또는 DROP TABLE
* ALTER TABLE ... SWITCH, SPLIT 또는 MERGE PARTITION
* ALTER INDEX DISABLE
* DROP INDEX
* CREATE, UPDATE 또는 DROP STATISTICS
* TRUNCATE TABLE
* ALTER AUTHORIZATION
* CREATE LOGIN
* CREATE, ALTER 또는 DROP USER
* CREATE, ALTER 또는 DROP PROCEDURE
* CREATE 또는 DROP VIEW
* INSERT VALUES
* SELECT(시스템 뷰와 DMV에서)
* EXPLAIN
* DBCC

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <a name="changing-user-resource-class-example"></a> 사용자 리소스 클래스 변경 예제
1. **로그인을 만듭니다:** 연결 tooyour 열고 **마스터** SQL 데이터 웨어하우스 데이터베이스를 호스팅하는 hello SQL server에서 데이터베이스 및 hello 다음 명령을 실행 합니다.
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > Azure SQL 데이터 웨어하우스 사용자에 대 한 hello master 데이터베이스 좋습니다 toocreate 사용자입니다. Master에 사용자를 만들면 SSMS와 같은 도구를 사용 하 여 데이터베이스 이름을 지정 하지 않고 사용자 toologin이 있습니다.  또한 있게 toouse hello 개체 탐색기 tooview에 모든 데이터베이스를 SQL server.  사용자를 만들고 관리하는 방법에 대한 자세한 내용은 [SQL Data Warehouse에서 데이터베이스 보호][Secure a database in SQL Data Warehouse]를 참조하세요.
   > 
   > 
2. **SQL 데이터 웨어하우스 사용자 만들기:** 연결 toohello 열고 **SQL 데이터 웨어하우스** 데이터베이스 및 hello 다음 명령을 실행 합니다.
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. **권한 부여:** 예제 부여 다음 hello `CONTROL` hello에 **SQL 데이터 웨어하우스** 데이터베이스입니다. `CONTROL`hello에 데이터베이스 수준 db_owner SQL Server에서의 해당 하는 hello 됩니다.
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW toonewperson;
    ```
4. **리소스 클래스를 높일:** 사용 하 여 hello 다음 tooadd 사용자 tooa 높은 작업 관리 역할을 쿼리 합니다.
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. **리소스 클래스를 줄이려면:** 사용 하 여 hello 다음 tooremove 작업 관리 역할에서 사용자를 쿼리 합니다.
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > 가능한 tooremove smallrc에서 사용자는 없습니다.
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a>큐에 대기 중인 쿼리 검색 및 다른 DMV
Hello를 사용할 수 있습니다 `sys.dm_pdw_exec_requests` 동시성 큐에서 대기 하는 DMV tooidentify 쿼리 합니다. 동시성 슬롯을 대기하는 쿼리는 **일시 중단**상태가 됩니다.

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

워크로드 관리 역할은 `sys.database_principals`를 사용하여 확인할 수 있습니다.

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

다음 쿼리에서 hello에 할당 된 각 사용자 역할을 보여 줍니다.

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

SQL 데이터 웨어하우스 hello 다음을 대기 유형을 있습니다.

* **LocalQueriesConcurrencyResourceType**: hello 동시성 슬롯 프레임 워크 외부에서 앉아 쿼리 합니다. `SELECT @@VERSION` 과 같은 DMV 쿼리 및 시스템 함수는 로컬 쿼리의 예입니다.
* **UserConcurrencyResourceType**: hello 동시성 슬롯 프레임 워크 내을 쿼리 합니다. 최종 사용자 테이블에 대한 쿼리는 이 리소스 형식을 사용하는 예를 나타냅니다.
* **DmsConcurrencyResourceType**: 데이터 이동 작업으로 초래된 대기
* **BackupConcurrencyResourceType**: 이 대기는 데이터베이스가 백업 중임을 나타냅니다. 이 리소스 종류에 대 한 hello 최대 값은 1입니다. 여러 백업 hello에 요청 하는 경우 동일한 시간, hello 다른을 대기 합니다.

hello `sys.dm_pdw_waits` DMV는 리소스에 대 한 요청을 대기 하는 사용 되는 toosee 될 수 있습니다.

```sql
SELECT  w.[wait_id]
,       w.[session_id]
,       w.[type]            AS Wait_type
,       w.[object_type]
,       w.[object_name]
,       w.[request_id]
,       w.[request_time]
,       w.[acquire_time]
,       w.[state]
,       w.[priority]
,    SESSION_ID()            AS Current_session
,    s.[status]            AS Session_status
,    s.[login_name]
,    s.[query_count]
,    s.[client_id]
,    s.[sql_spid]
,    r.[command]            AS Request_command
,    r.[label]
,    r.[status]            AS Request_status
,    r.[submit_time]
,    r.[start_time]
,    r.[end_compile_time]
,    r.[end_time]
,    DATEDIFF(ms,r.[submit_time],r.[start_time])        AS Request_queue_time_ms
,    DATEDIFF(ms,r.[start_time],r.[end_compile_time])    AS Request_compile_time_ms
,    DATEDIFF(ms,r.[end_compile_time],r.[end_time])        AS Request_execution_time_ms
,    r.[total_elapsed_time]
FROM    sys.dm_pdw_waits w
JOIN    sys.dm_pdw_exec_sessions s  ON w.[session_id] = s.[session_id]
JOIN    sys.dm_pdw_exec_requests r  ON w.[request_id] = r.[request_id]
WHERE    w.[session_id] <> SESSION_ID();
```

hello `sys.dm_pdw_resource_waits` DMV에서 지정된 된 쿼리에 사용 hello 리소스 대기만 보여 줍니다. 리소스 대기 시간 측정 제공 하는 리소스 toobe 때까지 대기 하는 hello 시간, SQL 서버 tooschedule hello 쿼리 hello CPU에 기본 hello에 대 한 걸리는 것과 반대로 toosignal 시간 hello 시간을 대기 하는 대로 합니다.

```sql
SELECT  [session_id]
,       [type]
,       [object_type]
,       [object_name]
,       [request_id]
,       [request_time]
,       [acquire_time]
,       DATEDIFF(ms,[request_time],[acquire_time])  AS acquire_duration_ms
,       [concurrency_slots_used]                    AS concurrency_slots_reserved
,       [resource_class]
,       [wait_id]                                   AS queue_position
FROM    sys.dm_pdw_resource_waits
WHERE    [session_id] <> SESSION_ID();
```

hello `sys.dm_pdw_wait_stats` DMV 대기 작업의 기록 추세 분석에 사용할 수 있습니다.

```sql
SELECT    w.[pdw_node_id]
,        w.[wait_name]
,        w.[max_wait_time]
,        w.[request_count]
,        w.[signal_time]
,        w.[completed_count]
,        w.[wait_time]
FROM    sys.dm_pdw_wait_stats w;
```

## <a name="next-steps"></a>다음 단계
데이터베이스 사용자 및 보안을 관리하는 방법에 대한 자세한 내용은 [SQL Data Warehouse에서 데이터베이스 보호][Secure a database in SQL Data Warehouse]를 참조하세요. 큰 리소스 클래스에 대 한 자세한 내용은 클러스터형된 columnstore 인덱스 품질을 향상 시킬 수 있습니다, 참조 [tooimprove 세그먼트 품질 인덱스를 다시 작성]합니다.

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[tooimprove 세그먼트 품질 인덱스를 다시 작성]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->
