---
title: "Azure 검색의 aaaData 업로드 | Microsoft Docs"
description: "Azure 검색의 tooupload 데이터 tooan 인덱스 하는 방법에 대해 알아봅니다."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: aa8d47c1-4ae6-4209-a8ce-48d5a9474707
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: ashmaka
ms.openlocfilehash: a95eae94f72c1d0926804ff7e1152f21773fcabf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search"></a>검색 데이터 tooAzure 업로드
> [!div class="op_single_selector"]
> * [개요](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST (영문)](search-import-data-rest-api.md)
> 
> 

데이터와 인덱스는 두 가지 방법으로 toopopulate 합니다. hello 첫 번째 옵션은 hello Azure 검색을 사용 하 여 hello 인덱스로 데이터를 푸시하여 수동으로 [REST API](search-import-data-rest-api.md) 또는 [.NET SDK](search-import-data-dotnet.md)합니다. hello 두 번째 옵션은 너무[지원 되는 데이터 원본이 가리키도록](search-indexer-overview.md) tooyour 인덱싱하고 hello 데이터를 자동으로 가져오고 Azure 검색을 사용 합니다.

## <a name="push-data-tooan-index"></a>푸시 데이터 tooan 인덱스
이 방법을 사용 하면 데이터 tooAzure 검색 toomake 보내는 tooprogrammatically 참조 검색에 사용할 수 있게 합니다. 응용 프로그램 (예: 동적 인벤토리 데이터베이스와 동기화 하는 작업 toobe 검색 해야 하는 경우) 매우 짧은 대기 시간 요구 사항이 hello 밀어 넣기 모델은 유일한 해결 합니다.

Hello를 사용할 수 있습니다 [REST API](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) 또는 [.NET SDK](search-import-data-dotnet.md) toopush 데이터 tooan 인덱스입니다. 현재 hello 포털을 통해 데이터를 푸시에 대 한 도구 지원 되지 않습니다.

이 방법은 hello 끌어오기 모델 보다 더 유연 하므로 개별적으로 또는 일괄 처리에서 문서를 업로드할 수 있습니다 (일괄 처리 또는 16MB 당 too1000를 어떤 제한이 먼저 발생). hello 밀어 넣기 모델 위치에 관계 없이 데이터 tooupload 문서 tooAzure 검색 허용 합니다.

Azure 검색에서 인식 hello 데이터 형식은 JSON,이 고 hello 데이터 집합의 모든 문서에는 인덱스 스키마에 정의 된 toofields 매핑되는 필드가 포함 되어야 합니다. 

## <a name="pull-data-into-an-index"></a>인덱스로 데이터를 끌어오기
hello 끌어오기 모델 지원 되는 데이터 소스를 탐색 하 고 자동으로 인덱스로 hello 데이터를 업로드 합니다. Azure Search에서 이 기능은 *인덱서*를 통해 구현되며, 현재 [Blob Storage](search-howto-indexing-azure-blob-storage.md), [Table Storage](search-howto-indexing-azure-tables.md), [Azure Cosmos DB](http://aka.ms/documentdb-search-indexer), [Azure VM의 Azure SQL Database 및 SQL Server](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)에 사용할 수 있습니다. 

인덱서는 인덱스 tooa 데이터 원본 (일반적으로 테이블, 뷰 또는 해당 하는 구조)를 연결 하 고 원본 필드 tooequivalent 필드 hello 인덱스에 매핑합니다. 실행 하는 동안 hello 행 집합은 자동으로 변환 된 tooJSON 및 hello 지정 된 인덱스에 로드 합니다. 모든 인덱서 예약 hello 데이터가 toobe 새로 고칠된 빈도 지정할 수 있도록 지원 합니다. 대부분 인덱서 변경 hello 데이터 원본을 지 원하는 경우 추적을 제공 합니다. 변경 내용을 추적 및 삭제 하 여 tooexisting 문서 또한 toorecognizing 새 문서, 인덱서 hello 필요가 tooactively index에서 hello 데이터를 관리 합니다. 

인덱서 기능은 hello에 노출 되며 [Azure 포털](search-import-data-portal.md), hello [REST API](/rest/api/searchservice/Indexer-operations), 및 hello [.NET SDK](/dotnet/api/microsoft.azure.search.indexersoperations)합니다. 

장점은 toousing hello 포털은 Azure 검색 일반적으로 스키마를 생성할 수는 기본 인덱스 수에 대 한 hello 원본 데이터 집합의 hello 메타 데이터를 읽어입니다. Hello 인덱스 스키마 편집만는 hello 후은 인덱스를 다시 만들기를 필요로 하지 않는 것이 허용 처리 될 때까지 hello 생성 된 인덱스를 수정할 수 있습니다. Hello 변경할 때는 toomake 영향 스키마를 직접 hello, toorebuild hello 인덱스를 해야 합니다. 

사용할 수 있습니다 hello 인덱스는 채워진 후 **탐색기 검색** 확인 단계 hello 포털 명령 모음에서 합니다.

## <a name="query-an-index-using-search-explorer"></a>검색 탐색기를 사용하여 인덱스 쿼리

신속 하 게 tooperform hello 문서 업로드에 대 한 예비 확인은 toouse **탐색기 검색** hello 포털에서입니다. hello 탐색기를 사용 하면 모든 코드 toowrite 지 않고 인덱스를 쿼리할 수 있습니다. hello 검색 환경을 기반으로 hello 같은 기본 설정 [간단한 구문](/rest/api/searchservice/simple-query-syntax-in-azure-search) 및 기본 [쿼리 매개 변수 설정은 searchMode](/rest/api/searchservice/search-documents)합니다. Hello 전체 문서를 검사할 수 있도록 JSON에서 결과가 반환 됩니다.

> [!TIP]
> 다양 한 [Azure 검색 코드 샘플](https://github.com/Azure-Samples/?utf8=%E2%9C%93&query=search) 쉽게 사용할 수 또는 포함 된 데이터 집합을 쉽게 tooget 시작 제공를 포함 합니다. 또한 hello 포털 샘플 인덱서 및 부동산 작은 데이터 집합 (sample "realestate-미국-")로 구성 된 데이터 소스를 제공 합니다. Hello 샘플 데이터 소스에서 hello 미리 구성 된 인덱서를 실행할 때 인덱스 만들고 검색 탐색기 또는 코드를 작성 하 여 다음 쿼리할 수 있는 문서를 로드 합니다.
