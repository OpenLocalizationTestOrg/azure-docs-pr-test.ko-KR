---
title: "데이터베이스 도구 용어집 aaaElastic | Microsoft Docs"
description: "탄력적 데이터베이스 도구에 쓰이는 용어 설명."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: a23a4e81-6706-452d-afc1-a550e5e47af9
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: d6573aad9a097e07135b0a64d1dafec19bb8cc7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-glossary"></a>탄력적 데이터베이스 도구 용어집
hello 다음 용어에 대해 정의 된 hello [탄력적 데이터베이스 도구](sql-database-elastic-scale-introduction.md), Azure SQL 데이터베이스의 기능입니다. hello 도구를 사용 하는 toomanage [분할 맵](sql-database-elastic-scale-shard-map-management.md), hello 등과 [클라이언트 라이브러리](sql-database-elastic-database-client-library.md), hello [분할 / 병합 도구](sql-database-elastic-scale-overview-split-and-merge.md), [탄력적 풀](sql-database-elastic-pool.md), 및 [쿼리](sql-database-elastic-query-overview.md)합니다. 

이러한 용어에 사용 되는 [탄력적 데이터베이스 도구를 사용 하 여 분할 영역이 추가](sql-database-elastic-scale-add-a-shard.md) 및 [hello RecoveryManager 클래스 toofix 분할 맵 문제를 사용 하 여](sql-database-elastic-database-recovery-manager.md)합니다.

![탄력적인 확장 용어][1]

**데이터베이스**: Azure SQL 데이터베이스 

**데이터 종속 라우팅**: hello를 특정 분할 키를 제공 하는 응용 프로그램 tooconnect tooa 분할을 사용 합니다. [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md)을 참조하세요. 너무 비교**[다중 분할 된 데이터베이스 쿼리](sql-database-elastic-scale-multishard-querying.md)**합니다.

**전역 분할 맵은**: hello 맵에 분할 키와 내에서 각 해당 분할 영역 간에 **분할 집합**합니다. hello 글로벌 분할 맵은 hello에 저장 된 **shard map manager**합니다. 너무 비교**로컬 분할 맵은**합니다.

**목록 분할된 데이터베이스 맵**: 분할 키가 개별적으로 매핑되는 분할된 데이터베이스 맵입니다. 너무 비교**범위 분할 맵은**합니다.   

**로컬 분할 맵은**: hello 분할 된 데이터베이스에 상주 하는 hello shardlet에 대 한 매핑이 포함 되어 hello 로컬 분할 맵은 분할 영역에 저장 합니다.

**여러 분할 영역 쿼리**: hello 기능 tooissue 여러 분할 영역에 대 한 쿼리, UNION ALL 의미 체계 (또한 "팬 아웃 쿼리")를 사용 하 여 결과 집합이 반환 됩니다. 너무 비교**데이터 종속 라우팅**합니다.

**다중 테넌트** 및 **단일 테넌트**: 단일 테넌트 데이터베이스 및 다중 테넌트 데이터베이스를 보여 줍니다.

![단일 및 다중 테넌트 데이터베이스](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

여기에 대표적인 **분할된** 단일 및 다중 테넌트 데이터베이스가 있습니다. 

![단일 및 다중 테넌트 데이터베이스](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

**범위 분할 맵은**:는 hello에 분할 된 데이터베이스 배포 전략은 기반 연속 값의 범위가 여러 분할 맵을 합니다. 

**참조 테이블**: 분할되지 않았지만 여러 분할된 데이터베이스에 걸쳐 복제되는 테이블입니다. 예를 들어, 우편번호는 참조 테이블에 저장할 수 있습니다. 

**분할된 데이터베이스**: 분할된 데이터 집합의 데이터를 저장하는 Azure SQL 데이터베이스입니다. 

**분할 된 데이터베이스 탄력성**: 기능 tooperform hello **수평적 확장** 및 **세로 배율**합니다.

**분할된 데이터베이스 테이블**: 분할되는 테이블, 즉 해당 데이터가 분할 키 값을 기준으로 여러 분할된 데이터베이스 간에 분산되는 테이블입니다. 

**분할된 데이터베이스 키**: 분할된 데이터베이스 간에 데이터를 배포하는 방법을 결정하는 열 값입니다. hello 값 형식 중 하나일 수 있습니다 hello 다음: **int**, **bigint**, **varbinary**, 또는 **uniqueidentifier**합니다. 

**분할 집합**: 특성 사용된 toohello 있는 분할 된 데이터베이스의 컬렉션을 hello hello shard map manager에서 동일한 분할 맵을 합니다.  

**Shardlet**: hello 연결 된 모든 데이터가 단일 분할 영역에 분할 키 값입니다. Shardlet은 데이터 이동 가능한 가장 작은 단위 hello 때 분할 된 테이블을 재배포 합니다. 

**분할 맵은**: hello 분할 키와 해당 각 분할 영역 간의 매핑 집합이 있습니다.

**Shard map manager**: hello 분할 맵과, 분할 영역 위치 및 하나 이상의 분할 집합에 대 한 매핑을 포함 하는 관리 개체 및 데이터 저장소입니다.

![매핑][2]

## <a name="verbs"></a>동사
**수평적 확장**: hello act 아웃 (또는) 확장을 추가 하거나 아래와 같이 분할 영역 tooa 분할 맵을 제거 하 여 분할 된 데이터베이스의 컬렉션입니다.

![수평 및 수직적 크기 조정][3]

**병합**: hello act tooone 분할 두 개의 분할 된 데이터베이스에서에서 shardlet을 이동 하 고 hello 분할 맵은 적절 하 게 업데이트 합니다.

**Shardlet 이동**: hello act 단일 shardlet tooa 다른 분할 영역을 이동 합니다. 

**분할**: 분할 키에 따라 여러 데이터베이스 간에 구조화 된 데이터를 가로로 동일 하 게 분할의 hello 작동 합니다.

**분할**: hello act 하나의 분할 tooanother (일반적으로 새) 분할 영역에서 여러 shardlet을 이동 합니다. 분할 키 hello 분할 지점으로 hello 사용자가 제공 됩니다.

**세로 배율**: hello 작업 확장 (또는 축소)는 개별 분할 된 데이터베이스의 성능 수준을 hello 합니다. 예를 들어 표준 tooPremium (결과적 더욱 많은 컴퓨팅 리소스)에서 분할 영역을 변경 합니다. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

