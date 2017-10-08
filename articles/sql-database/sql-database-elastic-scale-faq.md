---
title: "SQL 탄력적인 크기 조정 FAQ aaaAzure | Microsoft Docs"
description: "Azure SQL 데이터베이스의 탄력적인 확장에 대한 질문과 대답을 제공합니다."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: e60dde9c-bb7b-4f2f-b52c-bdb506d49fcb
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 8c77902e8ce9cbbc5e081cd9d2c911d4c8dc9e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-faq"></a>탄력적 데이터베이스 도구 FAQ
#### <a name="if-i-have-a-single-tenant-per-shard-and-no-sharding-key-how-do-i-populate-hello-sharding-key-for-hello-schema-info"></a>단일 테 넌 트 당 분할 된 데이터베이스 및 분할 키를 있으면 hello 스키마 정보에 대 한 분할 키 hello 어떻게 채울 합니까?
hello 스키마 정보 개체에만 사용 되는 toosplit 병합 시나리오입니다. 기본적으로 단일-테 넌 트 응용 프로그램을 사용 하는 경우 hello 분할 병합 도구 하지 않아도 하 고 없기 때문에 필요 toopopulate hello 스키마 정보 개체가 없습니다.

#### <a name="ive-provisioned-a-database-and-i-already-have-a-shard-map-manager-how-do-i-register-this-new-database-as-a-shard"></a>데이터베이스를 프로비전했으며 분할된 데이터베이스 맵 관리자가 이미 있습니다. 이 새로운 데이터베이스를 분할로 등록하려면 어떻게 해야 하나요?
참조 하십시오  **[hello 탄력적 데이터베이스 클라이언트 라이브러리를 사용 하 여 분할 tooan 응용 프로그램을 추가](sql-database-elastic-scale-add-a-shard.md)**합니다. 

#### <a name="how-much-do-elastic-database-tools-cost"></a>탄력적 데이터베이스 도구의 비용은 얼마인가요?
Hello 탄력적 데이터베이스 클라이언트 라이브러리를 사용 하 여 모든 비용 발생 하지 않습니다. 비용은은 hello 분할 병합 도구에 대 한 프로 비전 hello 웹/작업자 역할 뿐만 아니라 분할 영역 및 Shard Map Manager hello에 대 한 사용 하는 hello Azure SQL 데이터베이스에 대해서만 계산 됩니다.

#### <a name="why-are-my-credentials-not-working-when-i-add-a-shard-from-a-different-server"></a>다른 서버에서 분할을 추가할 경우 내 자격 증명이 작동하지 않는 것은 무엇 때문인가요?
Hello 형태의 자격 증명을 사용 하지 않는 "사용자 ID =username@servername"를 대신 사용 하 여 "사용자 ID 사용자 이름 =".  또한 해당 hello "username" 로그인에 대 한 권한이 hello 분할 해야 합니다.

#### <a name="do-i-need-toocreate-a-shard-map-manager-and-populate-shards-every-time-i-start-my-applications"></a>Shard Map Manager toocreate 필요 하 고 하는 내 응용 프로그램을 시작할 때마다 분할 영역을 채우는?
더-hello Shard Map Manager 만들 hello (예를 들어  **[ShardMapManagerFactory.CreateSqlShardMapManager](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)**) 작업은 일회성 작업입니다.  응용 프로그램 hello 호출을 사용 해야  **[ShardMapManagerFactory.TryGetSqlShardMapManager()](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)**  응용 프로그램 시작 시.  이러한 호출은 응용 프로그램 도메인당 하나만 있어야 합니다.

#### <a name="i-have-questions-about-using-elastic-database-tools-how-do-i-get-them-answered"></a>탄력적 데이터베이스 도구 사용과 관련된 질문이 있는 경우 답변을 받으려면 어떻게 해야 하나요?
에 게 연락 하세요 hello에 toous [Azure SQL 데이터베이스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)합니다.

#### <a name="when-i-get-a-database-connection-using-a-sharding-key-i-can-still-query-data-for-other-sharding-keys-on-hello-same-shard--is-this-by-design"></a>분할 키를 사용 하 여 데이터베이스 연결을 받으면 볼 수 있습니다. 여전히 데이터를 쿼리 hello에 다른 분할 키 동일 분할 합니다.  의도한 동작인가요?
hello 탄력적인 확장 Api 분할 키에 대 한 연결 toohello 올바른 데이터베이스를 제공 하지만 분할 키 필터링을 제공 하지 않습니다.  추가 **여기서** 필요한 경우 절 tooyour 쿼리 toorestrict hello 범위 toohello 분할 키를 제공 합니다.

#### <a name="can-i-use-a-different-azure-database-edition-for-each-shard-in-my-shard-set"></a>내 분할 집합의 각 분할에 대해 다른 Azure 데이터베이스 버전을 사용할 수 있나요?
예, 분할은 개별 데이터베이스이므로 한 분할은 Premium Edition이고 다른 버전은 Standard Edition일 수 있습니다. 또한 분할 영역이 hello 에디션의 hello 분할의 hello 수명 동안 여러 번 위나 아래로 확장할 수 있습니다.

#### <a name="does-hello-split-merge-tool-provision-or-delete-a-database-during-a-split-or-merge-operation"></a>가 분할 병합 도구 프로 비전 hello (또는 삭제) 분할 또는 병합 작업 중에 데이터베이스?
아니요. 에 대 한 **분할** 작업 hello 대상 데이터베이스 hello 적절 한 스키마와 함께 존재 해야 하며 hello Shard Map Manager에 등록 합니다.  에 대 한 **병합** 작업 hello shard map manager에서 hello 분할 된 데이터베이스를 삭제 한 다음 hello 데이터베이스를 삭제 해야 합니다.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

