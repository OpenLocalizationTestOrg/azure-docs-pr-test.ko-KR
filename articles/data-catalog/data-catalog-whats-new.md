---
title: "aaaWhat의 Azure Data Catalog에서 새로 만들기 | Microsoft Docs"
description: "이 문서에서는 새로운 기능에 대해 간략하게 tooAzure 데이터 카탈로그를 추가 합니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 1201f8d4-6f26-4182-af3f-91e758a12303
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/22/2017
ms.author: maroche
ms.openlocfilehash: f60130487ece39e110446b68544945089d2ab37e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="whats-new-in-azure-data-catalog"></a>Azure 데이터 카탈로그의 새로운 기능
너무 업데이트**Azure Data Catalog** 정기적으로 릴리스됩니다. 일부 릴리스에서 백 엔드 서비스 기능에 초점을 맞추므로 모든 릴리스는 새로운 사용자용 기능을 포함하지 않습니다. 이 페이지에는 새 사용자 용 기능 추가 toohello Azure Data Catalog 서비스 강조 표시합니다.

## <a name="whats-new-for-august-2017"></a>2017년 8월의 새로운 기능 
2017 년 1 년 8 월을 기준으로 다음 기능 hello 있는 tooAzure 데이터 카탈로그 추가 되었습니다.

*   만들고 hello 데이터 카탈로그 REST API를 사용 하 여 관계 메타 데이터를 관리 하기 위한 새 개발자 예제 ´ ù. hello *데이터 카탈로그로 관계 정보를 가져올* hello에서 사용할 수 있는 샘플은 [데이터 카탈로그 코드 샘플 페이지](https://azure.microsoft.com/resources/samples/?service=data-catalog&sort=0)합니다. 
* 추출에 대 한 지원 hello 데이터 원본 등록 도구를 사용 하 여 관련된 테이블을 등록할 때 Teradata 데이터 원본에서 관계 메타 데이터를 조인 합니다.
* 개체를 지원에 대 한 SQL Server 테이블 반환 함수 (TVF) hello 데이터 원본 등록 도구를 사용 하 여 SQL Server 데이터 원본을 등록 하는 경우.
* 여러 업데이트 및 상세 tooincrease hello 성능과 유용성 hello Data Catalog 포털의.

## <a name="whats-new-for-july-2017"></a>2017년 7월의 새로운 기능 
2017 년 1 월을 기준으로 다음 기능 hello 있는 tooAzure 데이터 카탈로그 추가 되었습니다.
*   다음과 같이 허용된 메타데이터 작업에 대한 보다 세분화된 제어 지원:
    - 카탈로그 관리자 제한할 수 있습니다 사용자의 기능 toocontribute 태그 및 관련된 메타 데이터 toohello 카탈로그, 읽기 전용 액세스 toohello 카탈로그를 사용 하도록 설정 합니다.
    - 카탈로그 관리자는 hello 카탈로그에서 사용자의 기능 tooregister 새 데이터 소스를 제한할 수 있습니다.
    - 카탈로그 관리자는 사용자의 기능 tootake 소유권 hello 카탈로그에서 데이터 자산 메타 데이터를 제한할 수 있습니다.
    - TooAzure Active Directory 보안 그룹 및 사용 권한 관리의 용이성에 대 한 사용자에는 사용 권한은 부여할 수 있습니다.
* 등록 된 데이터 자산과 hello Data Catalog 포털 검색 관련된 데이터 자산 간의 관계에 대 한 지원을 포함 하 여:
    - 추출 (Azure SQL 데이터베이스 포함)는 SQL Server, Oracle 및 MySQL에서 관계 메타 데이터의 데이터 원본을 사용 하는 경우 hello Data Catalog 데이터 원본 등록 도구입니다.
    - 관련된 데이터 자산 hello Data Catalog 포털에서 자산 메타 데이터를 볼 때 검색 합니다.
    - 작업 toodefine 찾아 hello 데이터 카탈로그 REST API를 사용 하 여 데이터 자산 간의 관계를 관리 합니다.

데이터 카탈로그에 대 한 사용 권한 관리에 대 한 자세한 내용은 참조 하십시오. [toosecure toodata 카탈로그 및 데이터 자산을 액세스 하는 방법을](data-catalog-how-to-secure-catalog.md)합니다.
데이터 카탈로그에는 관계에 대 한 자세한 내용은 참조 하십시오. [tooview Azure Data Catalog에서 데이터 자산을 연결 하는 방법을](data-catalog-how-to-view-related-data-assets.md)합니다.

## <a name="whats-new-for-june-2017"></a>2017년 6월의 새로운 기능 
2017 년 1 월을 기준으로 다음 기능 hello 있는 tooAzure 데이터 카탈로그 추가 되었습니다.
*   Sybase, Apache Cassandra 및 MongoDB 데이터 원본에 대한 지원 사용자는 이제 Cassandra 및 MongoDB 데이터베이스 및 테이블, Sybase 데이터베이스, 테이블 및 뷰를 등록 및 검색할 수 있습니다.

> [!NOTE]
> 때 등록 MongoDB 및 Cassandra 테이블 레코드 및 배열과 같은 복잡 한 데이터 형식의 열, 이러한 열을 포함 하는 포함 되지 않습니다 hello 메타 데이터에 tooData 카탈로그를 추가 합니다.

## <a name="whats-new-for-may-2017"></a>2017년 5월의 새로운 기능 
2017 년 1 월을 기준으로 다음 기능 hello 있는 tooAzure 데이터 카탈로그 추가 되었습니다.
*   새로운 개발자 샘플은 비즈니스 용어집 용어의 hello 대량 가져오기를 위해 사용할 수 있습니다. hello 용어집 대량 가져오기 샘플은 hello에서 사용할 수 있는 [데이터 카탈로그 개발자 예제 페이지](https://docs.microsoft.com/azure/data-catalog/data-catalog-samples)합니다. 
*   Hello Azure Data Catalog 포털에 ODBC 연결 정보를 편집할 수 있습니다. 데이터 자산 소유자가 데이터와 데이터 카탈로그 관리자 toore 레지스터 hello 데이터 원본 없이 등록 된 ODBC 데이터 원본에 대 한 hello 연결 정보를 편집할 이제 수 있습니다.
*   비즈니스 용어집 정의 및 설명에서 클릭할 수 있는 URL에 대한 지원 Url은 비즈니스 용어집 용어에 대 한 hello 설명과 정의 속성에 포함, hello Url hello Data Catalog 포털에서 하이퍼링크로 표시 됩니다.
*   전문가 표시 이름에 대 한 또한 tooexpert 메일 주소를 지원 합니다. 데이터 자산에 대 한 hello 속성 전문가 hello Data Catalog 포털에서을 볼 때 Azure Active Directory에서 hello 전문가 전체 이름은 hello 도구 설명에 표시 됩니다.

## <a name="whats-new-for-april-2017"></a>2017년 4월의 새로운 기능 
2017 년 1 월을 기준으로 다음 기능 hello 있는 tooAzure 데이터 카탈로그 추가 되었습니다.
*   ODBC 데이터 원본에 대한 지원 이제 사용자가 등록 및 ODBC 데이터베이스, 테이블 및 뷰를 hello 데이터 카탈로그 데이터 원본 등록 도구를 사용 하 여 검색할 수 있습니다.

## <a name="whats-new-for-march-2017"></a>2017년 3월의 새로운 기능 
2017 년 1 월을 기준으로 다음 기능 hello 있는 tooAzure 데이터 카탈로그 추가 되었습니다.
*   데이터 카탈로그 관리자를 위한 AAD 보안 그룹 사용에 대한 지원
*   이제 새로운 Azure 지역에서 Azure Data Catalog를 사용할 수 있습니다. 고객 hello 더하기 tooEast 미국, 미국 서 부, 서 부 유럽 및 오스트레일리아 동부, 유럽 북부, 및 동남 아시아에서는 hello 중앙 미국 서 부 지역에서 Azure 데이터 카탈로그 프로 비전 할 수 있습니다. 자세한 내용은 [Azure 지역](https://azure.microsoft.com/regions/)을 참조하세요.

## <a name="whats-new-for-february-2017"></a>2017년 2월의 새로운 기능 
2017 년 1 월을 기준으로 다음 기능 hello 있는 tooAzure 데이터 카탈로그 추가 되었습니다.
*   고급 설정에 hello Data Catalog 데이터 원본 등록 도구를 지원 합니다. 사용자는 대규모 데이터 원본을 등록할 때 명령 제한 시간 값을 지정할 수 있습니다.
*   FTP 및 PostgreSQL 데이터 원본에 대한 지원 사용자는 이제 FTP 파일 및 디렉터리 및 PostgreSQL 데이터베이스, 테이블 및 뷰를 등록 및 검색할 수 있습니다.

## <a name="whats-new-for-january-2017"></a>2017년 1월의 새로운 기능 
2017 년 1 월을 기준으로 다음 기능 hello 있는 tooAzure 데이터 카탈로그 추가 되었습니다.
*   Azure Data Catalog는 이제 [CSA STAR](https://www.microsoft.com/trustcenter/compliance/csa-star-certification) 규정을 준수합니다.
*   [Excel 2016 및 Excel용 파워 쿼리에서 가져오기 및 변환](https://support.office.com/article/Introduction-to-Microsoft-Power-Query-for-Excel-6E92E2F4-2079-4E1F-BAD5-89F6269CD605)과 통합 Excel 사용자는 Excel 내에서 Azure Data Catalog를 사용하여 쿼리를 공유하고 검색할 수 있습니다. 이 기능은 Power BI Pro 라이선스를 갖고 있는 toousers를 사용할 수 있습니다.

## <a name="whats-new-for-december-2016"></a>2016년 12월의 새로운 기능
2016 년 12 월을 기준으로 기능을 수행 하는 hello 있는 tooAzure 데이터 카탈로그 추가 되었습니다.
*   Azure Data Catalog는 이제 [HIPAA](https://www.microsoft.com/trustcenter/Compliance/HIPAA) 및 [EU 모델 조항](https://www.microsoft.com/TrustCenter/Compliance/EU-Model-Clauses) 규정을 준수합니다.
*   데이터 원본 연결 정보 편집에 대한 지원 데이터 자산 소유자가 데이터와 데이터 카탈로그 관리자 toore 레지스터 hello 데이터 원본 없이 등록 된 데이터 원본에 대 한 hello 연결 정보를 편집할 이제 수 있습니다.
*   Salesforce.com 데이터 원본에 대한 지원 사용자는 이제 Salesforce 개체를 등록하고 검색할 수 있습니다.


## <a name="whats-new-for-november-2016"></a>2016년 11월의 새로운 기능
2016 년 11 월을 기준으로 다음 기능 hello 있는 tooAzure 데이터 카탈로그 추가 되었습니다.
*   Azure Data Catalog는 이제 [ISO/IEC 27001](https://www.microsoft.com/trustcenter/compliance/iso-iec-27001) 및 [ISO/IEC 27018](https://www.microsoft.com/TrustCenter/Compliance/iso-iec-27018) 규정을 준수합니다.
*   Hello Data Catalog 포털 및 REST API를 사용 하 여 ODBC 데이터 원본의 hello 수동 등록을 지원 합니다.

## <a name="whats-new-for-september-2016"></a>2016년 9월의 새로운 기능
2016 년 9 월 기준으로 다음 기능 hello 있는 tooAzure 데이터 카탈로그 추가 되었습니다.

* IBM DB2 데이터 원본에 대한 지원입니다. 이제 사용자가 DB2 데이터베이스, 테이블 및 뷰를 등록하고 검색할 수 있습니다.
* Azure Cosmos DB 데이터 원본을 지원합니다. 이제 사용자가 Cosmos DB 데이터베이스 및 컬렉션을 등록하고 검색할 수 있습니다.
* Hello 카탈로그 이름 hello Data Catalog 포털에서 사용자 지정에 대 한 지원 합니다. 현재 카탈로그 관리자 hello 조직 이름 같은 hello 포털 제목에 표시 되는 텍스트를 제공할 수 있습니다.

## <a name="whats-new-for-august-2016"></a>2016년 8월의 새로운 기능
2016 년 8 월을 기준으로 다음 기능 hello 있는 tooAzure 데이터 카탈로그 추가 되었습니다.

* SQL Server Master Data Services (MDS) 데이터 원본 등록에 대한 개선. 이제 사용자는 hello 데이터 카탈로그 데이터 원본 등록 도구를 사용 하 여 MDS 엔터티를 등록할 때 미리 보기 및 데이터 프로필을 포함할 수 있습니다.
* 관리자 정의된 조직적으로 저장된 검색을 지원합니다. Hello Data Catalog 포털에서 검색을 저장할 때 데이터 카탈로그 관리자 이제 toosave 검색 개인용 또는 모든 사용자에 게 카탈로그를 선택할 수 있습니다. 조직적으로 저장된 검색은 모든 카탈로그 사용자와 공유되며, 데이터 원본 검색에 대한 표준화된 시작점을 제공할 수 있습니다.
* Hello Data Catalog 포털에서 toohello 속성 보기를 업데이트합니다. 모든 데이터 자산 속성 표시 되 고 보다 일관 되 고 검색 가능한 경험의 크기를 조정할 수를 단일 창 tooprovide에서 관리 되는.

## <a name="whats-new-for-july-2016"></a>2016년 7월의 새로운 기능
2016 년 7 월을 기준으로 다음 기능 hello 있는 tooAzure 데이터 카탈로그 추가 되었습니다.

* SQL Server Master Data Services (MDS) 데이터 원본에 대한 지원. 이제 사용자가 MDS 모델 및 엔터티를 등록하고 검색할 수 있습니다.
* SQL Server 저장 프로시저에 대한 지원. 이제 사용자는 SQL Server 데이터 원본에서 저장 프로시저 개체를 등록하고 검색할 수 있습니다.
* Hello Azure Data Catalog 포털 및 총 18 지원 되는 언어의 hello 데이터 원본 등록 도구에서 추가 언어를 지원 합니다. hello Azure Data Catalog 사용자 환경이 Windows hello 웹 브라우저에서 설정할 hello 언어 기본 설정에 따라 지역화 됩니다.
* 업데이트 및 hello Data Catalog 포털 홈 페이지에 대해 성능이 향상 되 고 간소화 된 사용자 환경을 포함 하 여 구체화 합니다.

## <a name="whats-new-for-june-2016"></a>2016년 6월의 새로운 기능
2016 년 6 월을 기준으로 다음 기능 hello 있는 tooAzure 데이터 카탈로그 추가 되었습니다.

* Hello Data Catalog 포털에서 데이터 자산을 검색할 때 hello 목록 보기에서 열 크기 조정 지원 합니다. 사용자가 쉽게 태그 및 설명과 같은 긴 자산 메타 데이터를 읽을 개별 열 toomore 크기를 조정할 수 있습니다.
* Excel 용 파워 쿼리는 hello Data Catalog 포털에서 toohello "열기" 메뉴를 추가 되었습니다. 사용자가 이제 열 수 지원 되는 데이터 원본 Excel 2016 또는 Excel 2010 및 Excel 2013 hello로 [Excel 용 파워 쿼리](https://support.office.com/article/Introduction-to-Microsoft-Power-Query-for-Excel-6E92E2F4-2079-4E1F-BAD5-89F6269CD605) 추가 기능을 설치 합니다.
* Azure Table Storage 데이터 원본에 대한 지원. 이제 사용자는 Azure Storage 데이터 원본에서 테이블 개체를 등록하고 검색할 수 있습니다.

## <a name="whats-new-for-may-2016"></a>2016년 5월의 새로운 기능
2016 년 5 월을 기준으로 다음 기능 hello 있는 tooAzure 데이터 카탈로그 추가 되었습니다.

* 비즈니스 용어집를 활용 toodefine 비즈니스 용어 및 계층 toocreate 공통적인 비즈니스 용어 모음 카탈로그 관리자에 있도록 합니다. 사용자가 용어집 용어 toomake 사용 하 여 등록 된 데이터 자산 태그를 지정할 수 것 보다 쉽게 toodiscover hello 카탈로그의 hello 내용을 이해 하 고 있습니다. 자세한 내용은 참조 [를 tooset 비즈니스 용어집를 활용 태그 지정 제어에 대 한 hello 하는 방법](data-catalog-how-to-business-glossary.md)  
* 향상 된 기능 toohello 데이터 카탈로그 비즈니스 용어집를 활용 한 번에 사용자가 tooupdate 여러 용어집 용어를 허용 하 합니다. 사용자 필드에 따라 여러 용어 tooedit hello를 선택할 수 있습니다.
  * 부모 어: hello 선택할 수 있는 새 부모 용어 및 선택 된 모든 용어는 업데이트 된 toobe 자식 선택한 hello 상위 용어입니다. Hello 모든 용어를 선택한 경우 hello 동일한 부모가 없으면 해당 부모는 hello 텍스트 상자에, 표시 hello 상위 용어 필드 집합 tooblank는.   
  * 태그 및 관련 자가: 사용자를 추가 하 고 태그 및 관련 자가 hello 관계 없이 동일한 환경을 사용 하 여 여러 데이터 자산 태그를 지정 하는 여러 개의 용어집 용어에 대 한 제거 수입니다.

> [!NOTE]
> hello 비즈니스 용어집를 활용 hello 표준 버전의 Azure Data Catalog만 제공 됩니다. hello 무료 버전에서는 관리 태깅 또는 비즈니스 용어집를 활용에 대 한 기능입니다.

## <a name="whats-new-for-march-2016"></a>2016년 3월의 새로운 기능
2016 년 3 월을 기준으로 다음 기능 hello 추가한 tooAzure 데이터 카탈로그: g:

* Hello 검색 기능 및 hello Azure 데이터 카탈로그 서비스의 카탈로그 자산 관리 기능을 프로그래밍 방식으로 액세스 하기 위한 통합된 REST API 끝점입니다. 이 검색 API 끝점 및 카탈로그 API 끝점은 더 이상 사용되지 않으며 2016년 3월 21일에 중단되었습니다. Hello API의 toohello 의미 체계는 변경 내용이 없습니다. Hello 끝점만 URI를 변경 합니다. 자세한 내용은 참조 hello [Azure 데이터 카탈로그 REST API 참조](https://msdn.microsoft.com/library/azure/mt267595.aspx)합니다. API 샘플을 보려면 [Azure Data Catalog 개발자 샘플](data-catalog-samples.md)을 참조하세요.

## <a name="whats-new-for-february-2016"></a>2016년 2월의 새로운 기능
2016 년 2 월을 기준으로 다음 기능 hello 있는 tooAzure 데이터 카탈로그 추가 되었습니다.

* 새로 디자인 된 데이터 원본 선택 hello Azure Data Catalog 데이터 원본 등록 도구에서 경험 합니다. hello 데이터 원본 등록 도구 되었습니다 업데이트 toomake it가 보다 쉽게 toolocate 하 고 선택 hello 데이터 원본에서 지 원하는 Azure 데이터 카탈로그에서 합니다.
* Hello Azure Data Catalog 포털 및 hello 데이터 원본 등록 도구에서 10 추가 언어를 지원 합니다. 또한 tooEnglish, hello Azure Data Catalog 경험은 현재 독일어, 스페인어, 프랑스어, 이탈리아어, 일본어, 한국어, 포르투갈어 (브라질), 러시아어, 중국어 간체 및 중국어 (번체). hello Azure Data Catalog 사용자 환경에 맞게 지역화 된 Windows hello 사용자의 웹 브라우저에서 설정할 hello 언어 기본 설정을 기반으로 합니다.
* 비즈니스 연속성 및 재해 복구를 위해 Azure Data Catalog 데이터에 대한 지역에서 복제가 지원됩니다. 데이터 원본 메타 데이터 및 crowdsourced 주석을 포함 하 여 모든 Azure 데이터 카탈로그 내용에 없는 추가 비용 toocustomers 두 Azure 지역 간 복제 이제 됩니다. hello Azure 지역 미리 쌍을 적어도 500 마일 떨어져 있는, 및에 설명 된 대로 hello 매핑을 따릅니다 [비즈니스 연속성 및 재해 복구 (BCDR): Azure 쌍을 이루는 지역](../best-practices-availability-paired-regions.md)합니다.
* 변경 hello Azure 데이터 카탈로그에서 사용 하는 Azure 구독에 대 한 지원 합니다. Azure 데이터 카탈로그 관리자는 요금 청구를 위해 hello Azure Data Catalog 포털 tooselect 다른 Azure 구독에서에서 hello 설정 페이지를 사용할 수 있습니다.

## <a name="whats-new-for-january-2016"></a>2016년 1월의 새로운 기능
2016 년 1 월을 기준으로 다음 기능 hello 있는 tooAzure 데이터 카탈로그 추가 되었습니다.

* 추가 데이터 원본의 수동 등록을 지원합니다. 이제 hello Azure Data Catalog 포털에서 "설명서 항목 만들기"를 사용 하거나 데이터 원본 hello Azure 데이터 카탈로그 REST API tooregister hello를 사용할 수 있습니다.
  * OData - 함수, 엔터티 집합 및 엔터티 컨테이너
  * HTTP - 파일, 끝점, 보고서 및 사이트
  * 파일 시스템 - 파일
  * SharePoint - 목록
  * FTP - 파일 및 디렉터리
  * Salesforce.com - 개체
  * DB2 - 테이블, 보기 및 데이터베이스
  * PostgreSQL - 테이블, 뷰 및 데이터베이스
* SQL Server(Azure SQL DB 및 Azure SQL 데이터 웨어하우스 포함) 데이터 원본에 대해 "SQL Server Data Tools에서 열기"가 지원됩니다.  
* SAP HANA 보기 및 패키지 등록 및 검색을 지원합니다. SAP HANA 데이터 hello Azure Data Catalog 데이터를 사용 하 여 원본 등록 도구 소스 주석을 추가 하 고 수 hello Azure Data Catalog 포털을 사용 하 여 등록 된 SAP HANA 데이터 원본 검색을 등록할 수 있습니다.
* 기능 toopin hello 및 hello Azure Data Catalog 포털에서 데이터 자산을 고정 해제 합니다. Toopin 데이터 자산 toomake를 선택할 수 있습니다 이러한 toorediscover 쉽고 다시 사용할 수 있도록 합니다.
* Hello Azure Data Catalog 포털에서 새로 디자인 된 홈 페이지 hello 새 홈 페이지를 전반적으로 hello 카탈로그에서에서 hello 현재 사용자가 활동-최근에 게시 된 자산을 포함 하 여 자산을 고정 및 저장 된 검색-에 대 한 정보 및 hello 활동에 대 한 정보를 포함 합니다.
* Hello Azure Data Catalog 포털에서 영구 사용자 설정 지원 합니다. 사용자 환경 설정-포함 하 여 표 또는 tile 보기 페이지 당 결과 수를 hello 및 방문 횟수 강조를 끄거나-사용자 세션 간에 유지 됩니다.
* 이제 새로운 Azure 지역 두 곳에서 Azure Data Catalog를 사용할 수 있습니다. 고객 hello hello 유럽 북부 및 동남 아시아, 영역에 추가 tooEast 미국, 미국 서 부, 서 부 유럽 및 동부 오스트레일리아의 경우에에서는 Azure 데이터 카탈로그 프로 비전 할 수 있습니다. 자세한 내용은 [Azure 지역](https://azure.microsoft.com/regions/)을 참조하세요.

> [!NOTE]
> "SQL Server Data Tools에서 열기" Visual Studio 2013 업데이트 4 및 SQL Server 도구가 toobe 설치와 필요 합니다. tooinstall hello 최신 버전의 SQL Server Data Tools, 방문 [다운로드 SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)합니다.


## <a name="whats-new-for-december-2015"></a>2015년 12월의 새로운 기능
2015 년 12 월을 기준으로 다음 기능 hello 있는 tooAzure 데이터 카탈로그 추가 되었습니다.

* Azure SQL 데이터 웨어하우스 데이터 원본에 대해 데이터 프로필을 지원합니다. Azure SQL 데이터 웨어하우스 테이블 및 뷰를 등록할 때 사용자 hello 데이터 원본에서 추출 된 hello 메타 데이터와 tooinclude 데이터 프로필 메트릭을 선택할 수 있습니다.
* MySQL 개체 및 데이터베이스 등록 및 검색을 지원합니다. 사용자가 MySQL 데이터 hello Azure Data Catalog 데이터를 사용 하 여 원본 등록 도구 소스 주석을 추가 하 고 수 hello Azure Data Catalog 포털을 사용 하 여 등록 된 MySQL 데이터 원본 검색을 등록할 수 있습니다.
* Teradata 데이터 원본에 대해 SPNEGO 및 Windows 인증이 지원됩니다. Teradata 테이블 및 뷰를 등록할 때 tooconnect tooTeradata SPNEGO 및 창 및 LDAP 및 t d 2 인증을 사용 하 여 선택할 수 있습니다.
* Azure 데이터 레이크 저장소 데이터 원본을 지원합니다. Azure 데이터 카탈로그를 사용하여 Azure 데이터 레이크 저장소 데이터 원본을 지금 등록하고 검색할 수 있습니다.
* 수동으로 hello Azure Data Catalog 데이터 원본 등록 도구에서 네트워크 프록시 설정을 지정 하기 위한 지원 합니다. 사용자는 "프록시 설정 수정" hello 도구 시작 페이지에서 선택 하 고 hello 프록시 주소와 포트 toobe hello 도구에서 사용 하는 지정할 수 있습니다.

## <a name="whats-new-for-november-2015"></a>2015년 11월의 새로운 기능
2015 년 11 월을 기준으로 다음 기능 hello 있는 tooAzure 데이터 카탈로그 추가 되었습니다.

* 기능 tooview hello 하 고 SQL Server (Azure SQL 데이터베이스 포함) 및 Oracle 데이터 원본에 대 한 hello Azure Data Catalog 포털 내에서 연결 문자열을 복사 합니다. 사용자가 SQL Server에 대 한 hello 연결 정보에서 "연결 문자열 보기" 링크를 클릭할 수 또는 Oracle 테이블, 뷰 또는 데이터베이스 toosee hello 연결 문자열 tooconnect toohello 데이터 원본을 사용 합니다. ADO.NET, ODBC, OLEDB 및 JDBC 연결 문자열은 SQL Server 데이터 원본에 대해 제공됩니다. ODBC 및 OLEDB 연결 문자열은 Oracle 데이터 원본에 대해 제공됩니다.
* Teradata 테이블 및 뷰를 등록할 때 데이터 프로필을 포함할 수 있습니다.
* SQL Server(Azure SQL DB 및 Azure SQL 데이터 웨어하우스 포함) 및 SQL Server Analysis Services, Azure 저장소 및 HDFS 원본에 대해 "Power BI Desktop에서 열기"가 지원됩니다.  
* Teradata 데이터 원본에 대해 LDAP 인증이 지원됩니다. Teradata 테이블 및 뷰를 등록할 때 사용자가 LDAP를 사용 하 여 tooconnect tooTeradata를 선택할 수 및 t d 2 인증 합니다.
* Teradata 데이터 원본에 대해 "Excel에서 열기"가 지원됩니다.
* Hello Azure Data Catalog 포털에 최근 검색 용어를 지원 합니다. Hello 포털에서 검색, 최근에 사용한 검색 용어 tooaccelerate hello 검색 환경에서 선택할 수 있습니다.
* Teradata 데이터 원본 미리 보기를 지원합니다. Teradata 테이블 및 뷰를 등록할 때 hello 데이터 원본에서 추출 된 hello 메타 데이터와 tooinclude 스냅숏 레코드를 선택할 수 있습니다.
* Azure SQL 데이터 웨어하우스 데이터 원본에 대해 "Excel에서 열기"를 지원합니다.
* 수동으로 등록된 자산 데이터에 대한 열 수준 스키마 정의 및 편집을 지원합니다. Hello Azure Data Catalog 포털을 사용 하 여 데이터 자산을 수동으로 만든 후 사용자가 hello 데이터 자산 속성의 열 정의 추가할 수 있습니다.
* Azure Data Catalog는 특정 메타 데이터를 소유 하는 등록 된 데이터 자산의 tooenable hello 검색을 검색할 때 "에" 쿼리에 대 한 지원 합니다. Azure Data Catalog 쿼리 구문은 이제 다음을 포함합니다.

| 쿼리 구문 | 목적 |
| --- | --- |
| `has:previews` |미리 보기를 포함하는 데이터 자산을 찾습니다. |
| `has:documentation` |설명서에 제공된 데이터 자산을 찾습니다. |
| `has:tableDataProfiles` |테이블 수준 데이터 프로필 정보를 사용하여 데이터 자산을 찾습니다. |
| `has:columnsDataProfiles` |열 수준 데이터 프로필 정보를 사용하여 데이터 자산을 찾습니다. |


> [!NOTE]
> "Power BI Desktop에서 열기" hello Power BI Desktop 응용 프로그램 toobe 설치의 현재 버전이 필요 합니다. 문제 또는이 기능을 사용 하 여 오류를 발생 하는 경우 hello 최신 버전의 Power BI Desktop에서 가졌는지 확인 [PowerBI.com](https://powerbi.com)합니다.


## <a name="whats-new-for-october-2015"></a>2015년 10월의 새로운 기능
2015 년 10 월을 기준으로 다음 기능 hello 있는 tooAzure 데이터 카탈로그 추가 되었습니다.

* 등록된 데이터 원본에 대한 데이터 미리 보기 및 데이터 프로필의 나머지에서 암호화가 지원됩니다. 데이터 프로필 카탈로그 관리자에 의해 키 관리에 대 한 필요 없이 hello 서비스에 등록 된 데이터 소스와 azure Data Catalog 미리 보기 레코드를 투명 하 게 암호화 됩니다.
* Teradata 데이터 원본에 대한 지원입니다. 이제 사용자가 Teradata 테이블 및 뷰를 등록하고 검색할 수 있습니다.
* 온-프레미스 Hive 데이터 원본에 대한 지원입니다. 사용자는 이제 Hadoop 온-프레미스 데이터 원본에서 Apache Hive에 대한 Hive 테이블을 등록하고 검색할 수 있습니다.
* Hello Azure Data Catalog 포털에서 저장 된 검색을 지원 합니다. 사용자가 검색 용어를 저장할 수 및 필터 선택 항목 tooeasily 이전 검색 결과 반복 하 고 hello 카탈로그 내용에 대 한 유용한 뷰를 정의 합니다. 또한 사용자는 저장된 검색을 자신의 기본 검색으로 표시할 수 있습니다. 사용자가 hello "돋보기" hello "시작" 페이지 또는 hello Azure Data Catalog 포털 홈 페이지에서 검색 아이콘을 클릭할 때 hello 사용자를 직접 저장 된 기본으로 플래그가 지정 된 검색 toohello를 만들어지며 합니다.
* 등록 된 데이터 자산 및 hello Azure Data Catalog 포털에 있는 컨테이너에 대 한 서식 있는 텍스트 설명서에 대 한 지원 합니다. 이제 사용자는 테이블, 뷰 및 보고서 같은 데이터 자산, 데이터베이스 및 모델 같은 컨테이너, 태그 및 설명이 충분하지 않은 시나리오에 대한 설명서를 제공할 수 있습니다.
* 알려진 데이터 원본 유형의 수동 등록을 지원합니다. 사용자가 Azure 데이터 카탈로그에서 지 원하는 모든 데이터 원본 유형에 대 한 hello Azure Data Catalog 포털을 사용 하 여 데이터 원본 정보를 수동으로 입력할 수 있습니다.
* Azure Active Directory 보안 그룹에 권한을 부여하도록 지원합니다. 카탈로그 액세스 toosecurity 그룹, 사용자 계정을 만들어 더 쉽게 toomanage 액세스 tooAzure 데이터 카탈로그를 사용 하 여 카탈로그 관리자입니다.
* Hello Azure Data Catalog 포털에서 Excel에서 하이브 데이터 소스를 열 수 있도록 지원 합니다.

> [!NOTE]
> 현재 릴리스에서 hello에 대 한 Teradata t d 2 인증만 지원 합니다. 추가 인증 메커니즘은 이후 릴리스에서 지원됩니다.

> [!NOTE]
> 하이브 데이터 원본에 대 한 toouse hello "열기에 Excel" 기능을 사용자가 설치 해야 hello ODBC 드라이버에 대 한 하이브.

## <a name="whats-new-for-september-2015"></a>2015년 9월의 새로운 기능
2015 년 9 월 기준으로 다음 기능 hello 있는 tooAzure 데이터 카탈로그 추가 되었습니다.

* Hive 데이터 원본을 등록하는 경우 데이터 프로필 포함을 지원합니다.
* 프로그래밍 방식으로 검색 하는 hello Azure Data Catalog에 응용 프로그램 toointegrate 더욱 쉽게 카탈로그 API를 지원 합니다.
* 새 "시작" 데이터 원본 hello Azure Data Catalog 포털에서 검색 환경입니다. 사용자가 검색 용어를 입력 하지 않고 hello hello Azure Data Catalog 포털의 페이지 "검색"을 입력 하면 가장 자주 사용 되는 hello 태그, 전문가, 데이터 원본 유형 및 개체 유형을 포함 하 여 hello 카탈로그 내용에 대 한 개요를 제공 하는 합니다.
* Azure SQL 데이터 웨어하우스 개체 및 데이터베이스 등록 및 검색을 지원합니다. Azure SQL 데이터 웨어하우스에 대한 추가 정보는 [SQL 데이터 웨어하우스](https://azure.microsoft.com/services/sql-data-warehouse/)를 참조하세요.
* SQL Server Analysis Services과 SQL Server Reporting Services 서버를 컨테이너로 등록하고 검색할 수 있게 지원합니다. SSAS 및 SSRS 개체를 등록할 때 Azure Data Catalog hello SSAS 모델 및 SSRS 서버에 대 한 및 hello 보고서 및 기타 개체에 대 한 항목을 만듭니다. hello 컨테이너를 검색할 수 있고 hello Azure Data Catalog 포털을 사용 하 여 주석이 지정 합니다. 사용자가 모델 또는 서버 추가 toosearching 및 hello 카탈로그의 hello 내용을 필터링의 검색 및 필터 hello 내용을 수도 있습니다.
* HTTP/HTTPS를 통한 SQL Server Analysis Services 개체 등록 및 검색에 대한 지원. 사용자는 URL (예: https://servername/olap/msmdpump.dll)를 사용 하 여 서버 이름 대신 tooSSAS 서버를 연결할 수와 추가 tooWindows 인증의 기본 인증 및 익명 연결을 사용할 수 있습니다. HTTP/HTTPS 연결 tooSSAS 대 한 추가 정보를 참조 하십시오. [HTTP 액세스 구성 tooAnalysis 서비스](https://msdn.microsoft.com/library/gg492140.aspx)합니다.
* HDInsight의 Hive 데이터 원본에 대한 지원. 사용자는 이제 HDInsight 데이터 원본의 Hadoop에서 Apache Hive에 대한 Hive 테이블을 등록하고 검색할 수 있습니다. HDInsight의 Hive에 자세한 내용은 참조 hello [HDInsight 설명서 센터](../hdinsight/hdinsight-use-hive.md)합니다.
* 컨테이너로 Oracle 데이터베이스 및 HDFS 클러스터 등록 및 검색에 대한 지원. Oracle 테이블 및 뷰 또는 HDFS를 등록할 때 Azure Data Catalog hello 데이터베이스, 테이블 및 뷰에 대 한 항목을 만듭니다. hello 데이터베이스를 검색할 수 있고 hello Azure Data Catalog 포털을 사용 하 여 주석이 지정 합니다. 사용자가 수도 있습니다 검색 및 필터는 데이터베이스의 내용을 hello 또는 클러스터 또한 toosearching 및 hello 카탈로그의 hello 내용을 필터링 합니다.
* 알 수 없는 데이터 원본 유형의 수동 등록 지원. 수동으로 사용자 수를 데이터 원본 등록 도구를 주석을 추가 하 고 발견 된 수의 hello에서 명시적으로 지 원하는 데이터 원본 hello Azure Data Catalog 포털을 사용 하 여 데이터 원본 정보를 입력 해야 합니다.
* 컨테이너로 SQL Server 데이터베이스 등록 및 검색 지원. SQL Server 테이블 및 뷰를 등록할 때 Azure Data Catalog hello 데이터베이스, 테이블 및 뷰에 대 한 항목을 만듭니다. hello 데이터베이스를 검색할 수 있고 hello Azure Data Catalog 포털을 사용 하 여 주석이 지정 합니다. 사용자가 더하기 toosearching 및 hello 카탈로그의 hello 내용을 필터링 데이터베이스의 검색 및 필터 hello 내용을 수도 있습니다.

> [!NOTE]
> SSAS 및 SSRS 개체 등록된 이전 toohello 18 년 9 월 릴리스는 hello 항목 모델 또는 서버를 추가 하기 전에 toohello 카탈로그 hello 데이터 원본 등록 도구를 사용 하 여 다시 등록 되어야 합니다. 데이터 소스를 다시 등록 해도 hello Azure Data Catalog 포털에서 사용자가 추가 된 주석이 영향을 주지 않습니다.

> [!NOTE]
> Oracle 테이블, 뷰 및 HDFS 파일 및 디렉터리에 등록 된 이전 toohello 11 년 9 월 릴리스는 다시 등록 해야 hello 항목 데이터베이스 또는 클러스터를 추가 하기 전에 toohello 카탈로그 hello 데이터 원본 등록 도구를 사용 합니다. 데이터 소스를 다시 등록 해도 hello Azure Data Catalog 포털에서 사용자가 추가 된 주석이 영향을 주지 않습니다.

> [!NOTE]
> SQL Server 테이블 및 뷰 된 등록 된 이전 toohello 4 년 9 월 릴리스를 다시 등록 해야 hello 데이터베이스 항목 toohello 카탈로그를 추가 하기 전에 hello 데이터 원본 등록 도구를 사용 합니다. 데이터 소스를 다시 등록 해도 hello Azure Data Catalog 포털에서 사용자가 추가 된 주석이 영향을 주지 않습니다.

## <a name="whats-new-for-august-2015"></a>2015년 8월의 새로운 기능
2015 년 8 월을 기준으로 다음 기능 hello 있는 tooAzure 데이터 카탈로그 추가 되었습니다.

* SQL Server와 Oracle 데이터 원본의 데이터 프로파일링 지원. SQL Server 및 Oracle 테이블 및 뷰를 등록할 때 사용자가 등록 되는 hello 개체에 대 한 tooinclude 데이터 프로필 정보를 선택할 수 있습니다. hello 데이터 프로필 개체 수준 추적과 열 수준 통계를 포함합니다.
* Hadoop HDFS 데이터 원본 지원. 이제 사용자가 HDFS 파일 및 디렉터리를 등록하고 검색할 수 있습니다.
* 등록된 데이터 원본에 대한 액세스 요청 정보 제공에 대한 지원. 모든 등록 된 데이터 자산에 대 한 사용자가 현재 Url 또는 전자 메일 링크를 포함 하 여 액세스를 요청에 대 한 지침을 제공할 수 있습니다, 그리고 tooeasily 기존 도구와 프로세스와 통합 합니다.
* 도구 설명 태그 및 전문가, toomake에 대 한 것 보다 쉽게 toodiscover 사용자가 등록 된 데이터 자산에 대 한 메타 데이터 제공 합니다.
* 새 "User" 단추와 메뉴 tooour 위쪽 탐색 모음을 추가 했습니다. 이 메뉴 hello 사용자를 원하는 경우 tooAzure 데이터 카탈로그에 사용 되는 계정 toolog hello 및 out toosign를 볼 수 있습니다. 이 메뉴는 중요 한 toodevelopers hello 카탈로그 이름도 표시 Azure 데이터 카탈로그 REST API를 hello를 사용 하 여 합니다.
* Standard Edition에만 해당: 소유자 toodata 자산을 추가할 때 Azure Data Catalog 이제 지원 사용자 계정 및 보안 그룹을 모두 소유자로 합니다. tooadd 소유자로 선택한 데이터 자산에 대 한 보안 그룹을 입력할 수 있습니다 어느 hello 그룹의 표시 이름 또는 전자 메일 주소를 UPN 하는 hello 그룹, 있는 경우.
* Azure Blob 저장소의 데이터 원본에 대한 지원입니다. 이제 사용자는 Azure 저장소 Blob 및 디렉터리를 등록하고 검색할 수 있습니다.

