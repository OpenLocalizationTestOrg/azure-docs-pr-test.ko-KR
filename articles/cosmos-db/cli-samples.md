---
title: "Azure Cosmos DB에 대 한 샘플 CLI aaaAzure | Microsoft Docs"
description: "Azure CLI 샘플 - Azure Cosmos DB 계정, 데이터베이스, 컨테이너, 하위 지역 및 방화벽을 만들고 관리합니다."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: database
ms.date: 06/07/2017
ms.author: mimig
ms.openlocfilehash: d6eefc3274e0b66eec4e69166bb7d4ddd58a522e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a>Azure Cosmos DB에 대한 Azure CLI 샘플

hello 다음 표에서 링크 toosample Azure CLI 스크립트 Azure Cosmos DB에 대 한 합니다. 모든 Azure Cosmos DB CLI 명령에 대 한 참조 페이지 hello에서 사용할 수 있는 [Azure CLI 2.0 참조](https://docs.microsoft.com/cli/azure/cosmosdb)합니다.

| |  |
|---|---|
|**Azure Cosmos DB 계정, 데이터베이스 및 컨테이너 만들기**||
|[DocumentDB API, Graph 또는 Table API 계정 만들기](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| Hello DocumentDB, 그래프 또는 테이블 Api가 있는 단일 Azure Cosmos DB API 계정, 데이터베이스 및 사용에 대 한 컨테이너를 만듭니다. |
| [MongoDB API 계정 만들기](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | 단일 Azure Cosmos DB MongoDB API 계정, 데이터베이스 및 컬렉션을 만듭니다. |
|**Azure Cosmos DB 확장**||
| [컨테이너 처리량 확장](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | 변경 내용을 hello througput 컨테이너에서 프로 비전 합니다.|
|[Azure Cosmos DB 데이터베이스 계정을 여러 하위 지역에서 복제 및 장애 조치 우선 순위 구성](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|지정된 장애 조치 우선 순위를 사용해서 계정 데이터를 여러 하위 지역으로 전체적으로 복제합니다.|
|**Azure Cosmos DB 보안 유지**||
| [계정 키 가져오기](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Hello 마스터 쓰기 기본 및 보조 키와 hello 계정에 대 한 기본 및 보조 읽기 전용 키를 가져옵니다.|
| [MongoDB 연결 문자열 가져오기](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | 연결 문자열 tooconnect hello MongoDB 앱 tooyour를 Azure Cosmos DB 계정을 가져옵니다.|
|[계정 키 재생성](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Hello 마스터 또는 hello 계정에 대 한 읽기 전용 키 다시 생성합니다.|
|[방화벽 만들기](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| 컴퓨터 및/또는 클라우드 서비스의 승인 된 집합에서 인바운드 IP 액세스 제어 정책 toolimit 액세스 toohello 계정을 만듭니다.|
|**고가용성, 재해 복구, 백업 및 복원**||
|[장애 조치 정책 구성](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|집합에 있는 각 영역의 hello 계정이 복제 장애 조치 우선 순위를 hello 합니다.|
|**Azure Cosmos DB를 리소스에 연결**||
|[웹 앱 tooAzure Cosmos DB에 연결](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|Azure Cosmos DB 데이터베이스 및 Azure Web App을 만들고 연결합니다.|
|||
