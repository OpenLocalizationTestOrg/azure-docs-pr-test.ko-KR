---
title: "hello 포털에서 Azure 검색에 aaaImport 데이터 | Microsoft Docs"
description: "Azure Vm에서 hello Azure 포털 toocrawl NoSQL Azure Cosmos DB, Blob 저장소, 테이블 저장소, SQL 데이터베이스 및 SQL Server에서 데이터를 Azure의 hello Azure 검색 데이터 가져오기 마법사를 사용 합니다."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: Azure Portal
ms.assetid: f40fe07a-0536-485d-8dfa-8226eb72e2cd
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: 00b0e59594560c0cdaea748df196518e9fba3834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-tooazure-search-using-hello-portal"></a>가져올 데이터 tooAzure 검색 hello 포털을 사용 하 여
hello Azure 포털에서 제공 된 **데이터를 가져올** hello 인덱스에 데이터를 로드 하기 위한 대시보드 Azure 검색에서 마법사. 

  ![Hello 명령 모음에서 데이터 가져오기][1]

Hello 마법사를 구성 하 고 호출 하는 내부적으로 *인덱서*, hello 인덱싱 프로세스의 여러 단계를 자동화 합니다. 

* Hello에 tooan 외부 데이터 원본에 연결 동일한 Azure 구독
* Hello 원본 데이터 구조를 기반으로 수정할 수 있는 인덱스 스키마 생성
* JSON 문서 hello 데이터 원본에서 검색 하는 행 집합을 사용 하 여 인덱스에 로드

Azure Cosmos DB에서 샘플 데이터를 사용하여 이 워크플로를 시도해 볼 수 있습니다. 방문 [hello Azure 포털에서에서 Azure 검색 시작](search-get-started-portal.md) 지침에 대 한 합니다.

> [!NOTE]
> Hello를 시작할 수 있습니다 **데이터를 가져올** 마법사에서 해당 데이터 원본에 대 한 인덱싱을 hello Azure Cosmos DB 대시보드 toosimplify 합니다. 왼쪽 탐색 영역에서 이동 너무**컬렉션** > **Azure 검색 추가** tooget 시작 합니다.

## <a name="data-sources-supported-by-hello-import-data-wizard"></a>Hello 데이터 가져오기 마법사에서 지 원하는 데이터 원본
hello 데이터 가져오기 마법사는 데이터 원본 hello를 지원 합니다. 

* Azure SQL Database
* Azure VM에서 SQL Server 관계형 데이터
* Azure Cosmos DB
* Azure Blob 저장소
* Azure 테이블 저장소

일반 데이터 집합은 필수 입력입니다. 단일 테이블, 데이터베이스 뷰 또는 동등한 데이터 구조에서만 가져올 수 있습니다. Hello 마법사를 실행 하기 전에이 데이터 구조를 만들어야 합니다.

## <a name="connect-tooyour-data"></a>Tooyour 데이터에 연결
1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 및 열기 hello 서비스 대시보드 합니다. 클릭할 수 있는 **더 많은 서비스** 기존 "검색 서비스" hello 현재 구독에 대 한 hello 점프 표시줄 toosearch에 있습니다. 
2. 클릭 **데이터 가져오기** hello 명령 tooslide 열려 hello 데이터 가져오기 블레이드 모음에 있습니다.  
3. 클릭 **tooyour 데이터 연결** toospecify 인덱서가 사용 되는 데이터 원본 정의. 내 구독 데이터 원본에 대 한 hello 마법사는 검색 및 전체 구성 요구 사항을 최소화 연결 정보를 읽을 일반적으로 수 있습니다.

|  |  |
| --- | --- |
| **기존 데이터 원본** |검색 서비스에 정의된 인덱서가 이미 있는 경우 다른 가져오기에 기존 데이터 원본 정의를 선택할 수 있습니다. |
| **Azure SQL Database** |Hello 페이지 또는 ADO.NET 연결 문자열을 통해 서비스 이름, 읽기 권한이 있는 데이터베이스 사용자에 대 한 자격 증명 및 데이터베이스 이름을 지정할 수 있습니다. 연결 문자열 옵션 tooview hello를 선택 하거나 속성을 사용자 지정 합니다. <br/><br/>hello 테이블 또는 뷰의 hello 행 집합을 제공 하는 hello 페이지에 지정 되어야 합니다. 이 옵션 선택 영역을 만들 수 있도록 드롭 다운 목록 제공 hello 연결 성공 하면 나타납니다. |
| **Azure VM에서 SQL Server** |정규화된 서비스 이름, 사용자 ID와 암호 및 데이터베이스를 연결 문자열로 지정합니다. toouse이 데이터 소스를 이전에 설치 해야 인증서 hello 연결을 암호화 하는 hello 로컬 저장소에 있습니다. 자세한 내용은 [SQL VM 연결 tooAzure 검색](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md)합니다. <br/><br/>hello 테이블 또는 뷰의 hello 행 집합을 제공 하는 hello 페이지에 지정 되어야 합니다. 이 옵션 선택 영역을 만들 수 있도록 드롭 다운 목록 제공 hello 연결 성공 하면 나타납니다. |
| **Azure Cosmos DB** |요구 사항 hello 계정, 데이터베이스 및 컬렉션을 포함 합니다. Hello 컬렉션의 모든 문서 hello 인덱스에 포함 됩니다. Hello 행 집합을 필터링 하거나 쿼리 tooflatten 정의할 수 있습니다 또는 toodetect 다음 데이터 새로 고침 작업에 대 한 문서를 변경 합니다. |
| **Azure Blob Storage** |요구 사항 hello 저장소 계정 및 컨테이너를 포함 합니다. 필요에 따라 blob 이름은 그룹화를 위해 가상 명명 규칙을 따르지 컨테이너 아래의 폴더로 hello 이름의 hello 가상 디렉터리 부분을 지정할 수 있습니다. 자세한 내용은 [Blob Storage 인덱싱](search-howto-indexing-azure-blob-storage.md)을 참조하세요. |
| **Azure 테이블 저장소** |요구 사항에는 hello 저장소 계정 및 테이블 이름을 포함 합니다. 필요에 따라 쿼리 tooretrieve hello 테이블 하위 집합을 지정할 수 있습니다. 자세한 내용은 [Table Storage 인덱싱](search-howto-indexing-azure-tables.md)을 참조하세요. |

## <a name="customize-target-index"></a>대상 인덱스 사용자 지정
임시 인덱스는 일반적으로 hello 데이터 집합에서 유추 됩니다. 추가, 편집 또는 필드 toocomplete hello 스키마를 삭제 합니다. 또한 특성 설정 hello 필드 수준 toodetermine에서 다시 검색 동작.

1. **사용자 지정 대상 인덱스**, hello 이름 지정 및 **키** toouniquely 사용 되는 각 문서를 식별 합니다. hello 키 문자열 이어야 합니다. 필드 값 공백이 나 대시를 포함 하는 경우 수 있는지 tooset 고급 옵션에서 **가져올지** toosuppress hello 이러한 문자에 대 한 유효성 검사 합니다.
2. 검토 하 고 hello 남은 필드를 수정 합니다. 필드 이름 및 형식은 일반적으로 채워집니다. Hello 인덱스가 생성 될 때까지 hello 데이터 형식을 변경할 수 있습니다. 나중에 변경하면 다시 빌드해야 합니다.
3. 다음과 같이 각 필드에 대한 인덱스 특성을 설정합니다.
   
   * 검색할 검색 결과에 hello 필드를 반환합니다.
   * 필터 식에서 참조 된 hello 필드 toobe Filterable 허용 합니다.
   * 정렬에 사용 된 hello 필드 toobe를 정렬할 수 있습니다.
   * Facetable 패싯 탐색에 대 한 hello 필드를 수 있습니다.
   * 검색 가능을 통해 전체 텍스트를 검색할 수 있습니다.
4. Hello 클릭 **분석기** toospecify hello 필드 수준에서 언어 분석기 하려는 경우를 탭 합니다. 언어 분석기만이 이번에 지정될 수 있습니다. 사용자 지정 분석기 또는 키워드, 패턴, 등과 같은 비언어 분석기를 사용하려면 코드가 필요합니다.
   
   * 클릭 **Searchable** toodesignate 전체 텍스트 검색 hello 필드 및 hello 분석기 드롭 다운 목록을 사용 하도록 설정 합니다.
   * 원하는 hello 분석기를 선택 합니다. 자세한 내용은 [여러 언어의 문서에 대한 인덱스 만들기](search-language-support.md)를 참조하세요.
5. Hello 클릭 **확인 기** 선택한 필드에 tooenable 미리 입력 쿼리 제안 합니다.

## <a name="import-your-data"></a>데이터 가져오기
1. **가져올지**, hello 인덱서에 대 한 이름을 제공 합니다. 해당 hello 제품 회수의 hello 데이터 가져오기 마법사 인덱서입니다. 나중 tooview 이나 편집을 선택 합니다 것 대신 hello 마법사를 다시 실행 하 여 hello 포털에서. 
2. Hello hello 서비스 프로 비전 되는 지역 표준 시간대를 기반으로 하는 hello 일정을 지정 합니다.
3. 인덱싱 계속 수 여부 문서 놓이고에서 고급 옵션 toospecify 임계값을 설정 합니다. 또한 지정할 수 있는지 여부를 **키** 필드 toocontain 공백 및 슬래시를 사용할 수 있습니다.  
4. 클릭 **확인** toocreate 인덱스 hello 고 hello 데이터를 가져옵니다.

인덱싱 hello 포털에서 모니터링할 수 있습니다. 문서가 로드 되 면 hello 인덱스 정의 대 한 hello 문서 수 증가 합니다. 경우에 따라 hello 가장 최근의 업데이트를 포털 페이지 toopick hello에 대 한 몇 가지 분 걸립니다.

hello 인덱스가 준비 tooquery로 hello 문서의 모든 로드 됩니다.

## <a name="query-an-index-using-search-explorer"></a>검색 탐색기를 사용하여 인덱스 쿼리

hello 포털에 포함 되어 **탐색기 검색** toowrite 코드 필요 없이 인덱스를 쿼리할 수 있도록 합니다. 모든 인덱스에서 [검색 탐색기](search-explorer.md)를 사용할 수 있습니다.

hello 검색 환경을 기반으로 hello 같은 기본 설정 [간단한 구문](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 및 기본 [설정은 searchMode 쿼리 매개 변수 (https://docs.microsoft.com/rest/api/searchservice/search-documents). 

결과 hello 전체 문서를 검사할 수 있도록 자세한 형식에서 JSON에 반환 됩니다.

## <a name="edit-an-existing-indexer"></a>기존 인덱서 편집
설명한 것 처럼, 데이터 가져오기 마법사 hello 만듭니다는 **인덱서**, hello 포털에서 독립 실행형 구문과 수정할 수 있습니다.

Hello 서비스 대시보드에서 구독에 대해 만든 모든 인덱서 목록을 hello 인덱서 타일 tooslide을 두 번 클릭 합니다. Hello 인덱서 toorun 중 하나를 두 번 클릭 하 고 편집 하거나 삭제할 수 있습니다. Hello 인덱스로 대체할 기존, hello 데이터 소스를 인덱싱하는 동안 오류 임계값에 대 한 옵션을 설정 합니다.

## <a name="edit-an-existing-index"></a>기존 인덱스 편집
created hello 마법사는 **인덱스**합니다. Azure 검색에서 구조적 업데이트 tooan 인덱스는 해당 인덱스를 다시 빌드할이 필요 합니다. 빌드를 다시 삭제 hello 인덱스의 경우 데이터를 다시 로드 하 고 원하는 hello 변경 내용이 있는 수정 된 스키마를 사용 하 여 hello 인덱스를 다시 만드는 것을 수반 합니다. 구조적 업데이트에는 데이터 형식을 변경하고 필드 이름을 바꾸거나 삭제하는 과정이 포함됩니다.

다시 빌드가 필요하지 않는 편집에는 새 필드 추가, 점수 매기기 프로필 변경, 확인기 변경 또는 언어 분석기 변경이 포함됩니다. 자세한 내용은 [인덱스 업데이트](https://msdn.microsoft.com/library/azure/dn800964.aspx) 를 참조하세요.


## <a name="next-steps"></a>다음 단계
이러한 링크 toolearn 인덱서에 대 한 자세한를 검토 합니다.

* [Azure SQL Database 인덱싱](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Azure Cosmos DB 인덱싱](search-howto-index-documentdb.md)
* [Blob Storage 인덱싱](search-howto-indexing-azure-blob-storage.md)
* [Table Storage 인덱싱](search-howto-indexing-azure-tables.md)

<!--Image references-->
[1]: ./media/search-import-data-portal/search-import-data-command.png

