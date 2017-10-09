---
title: "Azure 검색의 aaaIndexers | Microsoft Docs"
description: "Azure SQL 데이터베이스, Azure Cosmos DB 또는 Azure 저장소 tooextract 검색 가능한 데이터 크롤링하고 Azure 검색 인덱스를 채웁니다."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 34a7694c-8fd9-46b1-8900-cefdd7236323
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: 6a816252ec5d6032491a12651c05cb1fe77d3d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="indexers-in-azure-search"></a>Azure 검색의 인덱서
> [!div class="op_single_selector"]
>
> * [개요](search-indexer-overview.md)
> * [포털](search-import-data-portal.md)
> * [Azure SQL](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
> * [Azure Cosmos DB](search-howto-index-documentdb.md)
> * [Azure Blob Storage](search-howto-indexing-azure-blob-storage.md)
> * [Azure 테이블 저장소](search-howto-indexing-azure-tables.md)
>
>

**인덱서** Azure 검색에는 외부 데이터 원본에서 검색할 수 있는 데이터와 메타 데이터를 추출 하 고 인덱스 정보를 표시 하는 크롤러가 필드를 간의 매핑을 기반으로 hello 인덱스 및 데이터 원본입니다. 사용 하는이 방법이 참조 tooas '끌어오기 모델' hello 서비스 데이터를 끌어온에 toowrite 필요 없이 tooan 인덱스 데이터를 푸시하는 모든 코드 때문에 있습니다.

데이터 수집에 대 한 유일한 hello로 인덱서를 사용 하거나 index에서 hello 필드의 일부만 로드 하기 위한 인덱서 hello 사용을 포함 하는 기술 함께 사용 하 여 수 있습니다.

요청 시 또는 15분 간격으로 반복되는 데이터 새로 고침 예약에 따라 인덱서를 실행할 수 있습니다. 더 자주 업데이트하려면 Azure 검색과 외부 데이터 소스의 데이터를 동시에 업데이트하는 푸시 모델이 필요합니다.

## <a name="approaches-for-creating-and-managing-indexers"></a>인덱서를 만들고 관리하는 접근 방식
Azure SQL 또는 Azure Cosmos DB와 같은 일반적으로 사용 가능한 인덱서의 경우 다음과 같은 방법을 사용하여 인덱서를 만들고 관리할 수 있습니다.

* [포털 > 데이터 가져오기 마법사](search-get-started-portal.md)
* [서비스 REST API](https://msdn.microsoft.com/library/azure/dn946891.aspx)
* [.NET SDK](https://msdn.microsoft.com/library/azure/microsoft.azure.search.iindexersoperations.aspx)

## <a name="basic-configuration-steps"></a>기본 구성 단계
인덱서는 고유 toohello 데이터 소스 기능을 제공할 수 있습니다. 이러한 점에서 인덱서 또는 데이터 원본 구성의 일부 측면은 인덱서 유형에 따라 달라집니다. 그러나 모든 인덱서 공유 hello 동일한 기본 컴퍼지션 및 요구 사항입니다. 인덱서는 아래에 자세히 설명 하는 일반적인 tooall 적용 되는 단계입니다.

### <a name="step-1-create-an-index"></a>1단계: 인덱스 만들기
인덱서는 일부 작업 관련된 toodata 수집 자동화 됩니다 하지 않으면이 인덱스를 만들면 둘 중 하나입니다. 필수 구성 요소로서 외부 데이터 원본의 인덱스와 일치하는 필드를 포함한 미리 정의된 인덱스가 있어야 합니다. 인덱스를 구성하는 방법에 대한 자세한 내용은 [인덱스 만들기(Azure 검색 REST API)](https://msdn.microsoft.com/library/azure/dn798941.aspx)를 참조하세요.

### <a name="step-2-create-a-data-source"></a>2단계: 데이터 원본 만들기
인덱서는 연결 문자열 등의 정보가 담긴 **데이터 원본** 에서 데이터를 가져옵니다. 현재 데이터 원본 hello 지원 됩니다.

* [Azure SQL 데이터베이스 또는 Azure 가상 컴퓨터의 SQL Server](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Azure Cosmos DB](search-howto-index-documentdb.md)
* [Azure Blob 저장소](search-howto-indexing-azure-blob-storage.md), 사용 되는 PDF, Office 문서, HTML 또는 XML에서 tooextract 텍스트
* [Azure 테이블 저장소](search-howto-indexing-azure-tables.md)

데이터 소스 구성 되 고 한 번에 인덱스 하나 이상 여러 인덱서 tooload에서 데이터 원본을 사용할 수 있는 의미 하 고 사용 하는 hello 인덱서 독립적으로 관리 합니다.

### <a name="step-3create-and-schedule-hello-indexer"></a>3 단계: 만들기 및 hello 인덱서 예약
hello 인덱서 정의 hello 인덱스, 데이터 원본 및 일정을 지정 하는 구문입니다. Hello에서 데이터 원본에는 인덱서 서비스가 다른 서비스에서 데이터 원본을 참조할 수 동일한 구독 합니다. 인덱서를 구성하는 방법에 대한 자세한 내용은 [인덱서 만들기(Azure 검색 REST API)](https://msdn.microsoft.com/library/azure/dn946899.aspx)를 참조하세요.

## <a name="next-steps"></a>다음 단계
기본 개념 hello를가지고 hello 다음 단계 tooreview 요구 사항 및 작업 특정 tooeach 데이터 원본 유형입니다.

* [Azure SQL 데이터베이스 또는 Azure 가상 컴퓨터의 SQL Server](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Azure Cosmos DB](search-howto-index-documentdb.md)
* [Azure Blob 저장소](search-howto-indexing-azure-blob-storage.md), 사용 되는 PDF, Office 문서, HTML 또는 XML에서 tooextract 텍스트
* [Azure 테이블 저장소](search-howto-indexing-azure-tables.md)
* [Hello Azure 검색 Blob 인덱서를 사용 하 여 인덱싱 CSV blob](search-howto-index-csv-blobs.md)
* [Azure Search Blob 인덱서를 사용하여 JSON Blob 인덱싱](search-howto-index-json-blobs.md)
