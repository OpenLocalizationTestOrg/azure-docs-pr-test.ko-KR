---
title: "aaaDiscover를 식별 하 고, Microsoft Azure에서 개인 데이터를 분류 | Microsoft Docs"
description: "데이터를 검색, 분류, 검색, 식별하는 방법에 대해 자세히 알아보기"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: af4ced1c57699dc751d55cfdf3229c7d294648a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="discover-identify-and-classify-personal-data-in-microsoft-azure"></a>Microsoft Azure에서 개인 데이터 검색, 식별 및 분류

이 문서에서는 toodiscover,이 식별 하 고 여러 Azure 도구와 서비스, Azure, Azure HDInsight의 Hadoop 클러스터에 대 한 Azure Data Catalog, Azure Active Directory, SQL 데이터베이스, 파워 쿼리를 사용 하는 등의 개인 데이터를 분류 하는 방법에 지침 제공 Azure Cosmos DB에 대 한 정보 보호, Azure 검색 및 SQL 쿼리 합니다.

## <a name="scenario-problem-statement-and-goal"></a>시나리오, 문제 설명 및 목표

미국 기반 스포츠 회사는 다양한 개인 데이터 및 기타 데이터를 수집합니다. 고객 및 직원 데이터를 포함합니다. 여러 데이터베이스에 유지 하 고 자신의 Azure 환경에서 여러 다른 위치에 저장 하는 hello 회사입니다. 또한 tooselling 스포츠 장비, 또한를 호스트 하 고, EU hello에 포함 하는 hello world 정예 운동 이벤트에 대 한 등록을 관리 및 일부의 경우 hello에 수집 된 고객 데이터는 의료 보험 정보를 포함 합니다.

Hello 회사 많은 국제 bicycling tours 매년 호스트 많고 hello 전 세계 여러 위치에 임시 직원, 이후 몇 가지 hello 데이터 집합은 매우 큽니다. hello 회사에서 고객 및 직원을 모두 사용 되는 개발자 빌드된 응용 프로그램에 있습니다.

hello 사는 문제 다음 tooaddress hello:

- 개인 고객 및 직원 데이터 hello에서 분류/구별 해야 순서 tooensure 적절 한 액세스 및 보안에서 다른 데이터 hello 회사를 수집 합니다.
- hello 데이터 관리자 야 합니다. tooeasily 다양 한 영역 hello Azure 환경에 걸쳐 hello 위치의 고객 개인 데이터를 검색 합니다.
- 고객 및 직원 개인 데이터에 표시 되는 공유 문서 및 전자 메일 통신으로 표시 되어야 합니다 toohelp 확인을 안전 하 게 보호 됩니다.
- hello 회사의 응용 프로그램 개발자가 웹 및 모바일 앱에서 개인 데이터를 고객 및 직원에 대 한 방식으로 tooeasily 검색을 해야합니다.
- 또한 개발자 tooquery 자신의 문서 데이터베이스 개인 데이터에 대 한 합니다.

### <a name="company-goals"></a>회사 목표

- 모든 고객 및 직원 개인 데이터를 쉽게 찾을 수 있도록 Azure Data Catalog에서 태그가 지정되거나 주석이 추가되어야 합니다. 이상적으로 고객 및 직원 개인 데이터는 별도로 태그가 지정되거나 주석이 추가됩니다.
- 고객 및 직원 사용자 프로필의 개인 데이터 및 Azure Active Directory에 있는 작업 정보는 쉽게 찾을 수 있어야 합니다.
- 여러 SQL Databases에 있는 개인 데이터를 쉽게 쿼리할 수 있어야 합니다. 
- Hello 회사의 큰 데이터 집합의 일부 Azure HDInsight를 통해 관리 되 고 Hadoop에 저장 합니다. 해당 데이터는 개인 데이터를 쿼리할 수 있도록 Excel로 가져올 수 있어야 합니다.
- 문서 및 전자 메일 통신에서 공유된 개인 데이터는 Azure Information Protection에서 분류되고 레이블이 지정되고 안전하게 보호됩니다.
- hello 회사의 응용 프로그램 개발자 해야 수 toodiscover 고객 및 직원 개인 앱에서 데이터 hello 빌드되기 했으므로 Azure 검색 작업을 수행할 수 있는 합니다.
- 개발자가 자신의 문서 데이터베이스에서 개인 데이터 수 toofind 이어야 합니다.

## <a name="azure-active-directory-data-discovery"></a>Azure Active Directory: 데이터 검색

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/)는 Microsoft의 클라우드 기반, 다중 테넌트 디렉터리 및 ID 관리 서비스입니다. 고객 및 직원에 해당 하는 사용자의 프로필 및 개인 데이터를 포함 하는 사용자 작업 정보를 찾을 수 있습니다 프로그램 [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) hello를 사용 하 여 (AAD) 환경 [Azure 포털](https://portal.azure.com/)합니다.

Toofind 하거나 특정 사용자에 대 한 개인 데이터를 변경 하는 경우 특히 유용 합니다. 또한 사용자 프로필 및 작업 정보를 추가하거나 변경할 수 있습니다. Hello 디렉터리에 대 한 전역 관리자 인 계정으로 로그인 해야 합니다.

### <a name="how-do-i-locate-or-view-user-profile-and-work-information"></a>사용자 프로필 및 작업 정보를 찾고 보려면 어떻게 할까요?

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.

2. 선택 **더 많은 서비스**, 입력 **사용자 및 그룹** 에 hello 텍스트 상자를 선택한 후 **Enter**합니다.

   ![사용자 프로필 및 작업 정보를 찾으려면 어떻게 할까요?](media/how-to-discover-classify-personal-data-azure/user-profile.png)

3. Hello에 **사용자 및 그룹** 블레이드를 **사용자**합니다.

  ![사용자 및 그룹 열기](media/how-to-discover-classify-personal-data-azure/users-groups.png)

4. Hello에 **사용자 및 그룹-사용자가** 블레이드를 hello 목록에서 사용자를 선택한 다음 선택 hello 선택한 사용자에 대 한 hello 블레이드에서 **프로필** tooview 개인 데이터가 포함 될 수 있는 사용자 프로필 정보 .

  ![사용자 선택](media/how-to-discover-classify-personal-data-azure/select-user.png)

5. 작업을 하 고 다음 hello 명령 모음에서 선택 수를 tooadd 필요 하거나 사용자 프로필 정보를 변경 하는 경우 **저장 합니다.**
6. Hello 선택한 사용자에 대 한 hello 블레이드에서 선택 **작업 정보** tooview 개인 데이터를 포함할 수 있는 사용자 작업 정보입니다.

 ![작업 정보 보기](media/how-to-discover-classify-personal-data-azure/work-info.png)

7. 작업을 하 고 다음 hello 명령 모음에서 선택 수를 tooadd 필요 하거나 사용자 작업 정보를 변경 하는 경우 **저장 합니다.**

## <a name="azure-sql-database-data-discovery"></a>Azure SQL Database: 데이터 검색

[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50)는 개발자가 응용 프로그램을 빌드하고 유지하는 데 유용한 클라우드 데이터베이스입니다. 표준 SQL 쿼리를 사용하여 개인 데이터를 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50)에서 찾을 수 있습니다. Azure SQL 탄력적 쿼리 (미리 보기)를 사용 하면 사용자가 tooperform 데이터베이스 간 쿼리 합니다.

자세한 [SQL 데이터베이스](../sql-database/sql-database-technical-overview.md) 자습서의 SQL 데이터베이스를 사용 하 여 많은 측면을 설명 합니다. 방법을 비롯 하 여 하나 toobuild 방법과 toorun 데이터 쿼리 합니다. hello 다음은 링크 toospecific 섹션이 포함 된 hello 자습서에서 사용할 수 있는 hello 정보의 요약입니다.

### <a name="how-do-i-build-a-sql-database"></a>SQL Database를 빌드하려면 어떻게 할까요?

세 가지 방법으로 toodo 하기:

- Hello에서 Azure SQL 데이터베이스를 만들 수 있습니다 [Azure 포털](https://portal.azure.com/)합니다. Hello 자습서에서는 특정 리소스 그룹 및 논리 서버 내에서 계산 및 저장소 리소스 집합을 사용 합니다. AdventureWorks라는 가상 회사의 샘플 데이터를 사용합니다. 서버 수준 방화벽 규칙도 만듭니다. toolearn 어떻게 toodo이, 방문 hello [hello Azure 포털에서에서 Azure SQL 데이터베이스를 만들](../sql-database/sql-database-get-started-portal.md) 자습서입니다.

  ![Azure SQL Database 만들기](media/how-to-discover-classify-personal-data-azure/create-database.png)
- Hello에 SQL 데이터베이스를 만들 수도 있습니다 [Azure 클라우드 셸](https://azure.microsoft.com/features/cloud-shell/) CLI, 브라우저 기반 명령줄 도구입니다. hello 도구 hello Azure 포털에서에서 사용할 수 있으며 여기에서 직접 실행할 수 있습니다. 이 자습서에서는 있습니다 hello 도구를 시작, 스크립트 변수를 정의 리소스 그룹을 만들고 논리 서버 및 서버 방화벽 규칙을 구성 합니다. 샘플 데이터로 데이터베이스를 만듭니다. toolearn 어떻게 toocreate 이러한 방식으로 데이터베이스 방문 hello [hello Azure CLI를 사용 하 여 단일 Azure SQL 데이터베이스 만들기](../sql-database/sql-database-get-started-cli.md) 자습서입니다.

  ![CLIT 자습서](media/how-to-discover-classify-personal-data-azure/cli-tutorial.png)

>[!NOTE]
Linux 관리자와 개발자는 일반적으로 Azure CLI를 사용합니다. 일부 사용자는 Azure CLI가 세 번째 옵션인 PowerShell보다 더 쉽고 직관적이라고 생각합니다.

- 마지막으로, 명령줄/스크립트 사용 되는 도구 toocreate PowerShell을 사용 하 여 SQL 데이터베이스를 만들고 Azure 및 기타 리소스를 관리할 수 있습니다. 이 자습서에서는 있습니다 hello 도구를 시작, 스크립트 변수를 정의 리소스 그룹을 만들고 논리 서버 및 서버 방화벽 규칙을 구성 합니다. 샘플 데이터로 데이터베이스를 만듭니다.

hello 자습서 hello Azure PowerShell 모듈 버전 4.0 이상이 필요합니다. Get-module-ListAvailable AzureRM toofind 버전을 실행 합니다. Tooinstall 또는 업그레이드를 할 경우 설치 하는 Azure PowerShell 모듈을 참조 하십시오.

```PowerShell
New-AzureRmSQLDatabase -ResourceGroupName $resourcegroupname `
-ServerName $servername `
-DatabaseName $databasename `
-RequestedServiceObjectiveName "s0"
```

toolearn 어떻게 toocreate 이러한 방식으로 데이터베이스 방문 hello [Powershell을 사용 하 여 단일 Azure SQL 데이터베이스 만들기](../sql-database/sql-database-get-started-powershell.md) 자습서입니다.

>[!Note]
Windows 관리자는 PowerShell toouse 경향이 해도 되지만 그 중 일부를 Azure CLI.

### <a name="how-do-i-search-for-personal-data-in-sql-database-in-hello-azure-portal"></a>SQL 데이터베이스 hello Azure 포털에서에서 개인 데이터를 검색 하려면 어떻게 해야 하나요? * *

개인 데이터에 대 한 hello Azure 포털 toosearch 내 hello 기본 제공 쿼리 편집기 도구를 사용할 수 있습니다. SQL server 관리자 로그인 및 암호를 사용 하 여 toohello 도구에 로그인 하 고 쿼리를 입력 합니다.

  ![hello 포털을 사용 하 여 sql를 검색 합니다.](media/how-to-discover-classify-personal-data-azure/search-sql-portal.png)

Hello 자습서의 5 단계 hello 쿼리 편집기 창에서 예제 쿼리 보여주지만 (또한 두 테이블의에서 데이터를 결합 하 고 반환 되는 hello 데이터 집합의 hello 원본 열에 대 한 별칭을 만듭니다) 개인 정보나 기밀 정보에 집중 하지 않습니다. hello 다음 스크린샷은 hello 쿼리 반환 되는 hello 결과 창와 5 단계에서:

  ![쿼리 편집기](media/how-to-discover-classify-personal-data-azure/query-editor.png)

데이터베이스가 MyTable이라고 하는 경우 개인 정보의 샘플 쿼리는 이름, 사회 보장 번호 및 ID 번호를 포함하고 다음과 같이 표시될 수 있습니다.

“SELECT Name, SSN, ID number FROM MyTable”

Hello 쿼리를 실행 하는 hello에서 hello 결과 확인 한 다음 **결과** 창.

SQL tooquery hello Azure 포털에서에서 데이터베이스 하는 방법에 대 한 자세한 내용은 방문 hello [hello SQL 데이터베이스 쿼리](../sql-database/sql-database-get-started-portal.md) hello 자습서의 섹션입니다.

### <a name="how-do-i-search-for-data-across-multiple-databases"></a>여러 데이터베이스 간에 데이터를 검색하려면 어떻게 할까요?

SQL 탄력적 쿼리 (미리 보기) 하면 tooperform 데이터베이스 간 및 데이터베이스 쿼리를 여러 개 있으며 단일 결과 반환 합니다. hello [자습서 개요](../sql-database/sql-database-elastic-query-overview.md) 시나리오에 대 한 자세한 설명 및 데이터베이스를 수직 및 수평 분할 hello 차이점에 설명 합니다. 행 분할은 “분할”이라고 합니다.

  ![수직 분할](media/how-to-discover-classify-personal-data-azure/vertical-partition.png)

  ![행 분할](media/how-to-discover-classify-personal-data-azure/horizontal.png)

시작 tooget 방문 hello [Azure SQL 데이터베이스 탄력적 쿼리 개요 (미리 보기)](../sql-database/sql-database-elastic-query-overview.md) 페이지.

#### <a name="power-query-for-importing-azure-hdinsight-hadoop-clusters-data-discovery-for-large-data-sets"></a>파워 쿼리(Azure HDInsight Hadoop 클러스터 가져오기): 큰 데이터 집합의 데이터 검색

Hadoop는 오픈 소스 Apache 저장소이며 Hadoop 클러스터에서 분석되고 저장되는 대규모 데이터 집합에 대한 처리 서비스입니다. [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/) 사용자 toowork Hadoop으로 Azure의 클러스터 수 있습니다. 파워 쿼리는 Excel 추가 기능으로 무엇보다도 사용자가 다양한 소스에서 데이터를 검색할 수 있도록 합니다.

Azure HDInsight의 Hadoop 클러스터와 연결 된 개인 데이터에는 파워 쿼리를 통해 가져온된 tooExcel 수 있습니다. Hello 데이터는 Excel에 사용 하 여 쿼리 tooidentify 것입니다.

#### <a name="how-do-i-use-excel-power-query-tooimport-hadoop-clusters-in-azure-hdinsight-into-excel"></a>사용 하는 방법 Excel 파워 쿼리 tooimport Hadoop 클러스터에서 Azure HDInsight를 Excel로?

HDInsight 자습서에서는 이 전체 과정을 설명합니다. 필수 구성 요소를 설명 하 고 링크 tooa 포함 [Azure HDInsight 시작](../hdinsight/hdinsight-hadoop-linux-tutorial-get-started.md) 자습서입니다. Excel 2016으로 2013 및 2010 지침은 (단계는 이전 버전의 Excel hello에 대 한 약간 다른). Hello Excel 파워 쿼리 추가 기능에 없다면 hello 자습서에서는 어떻게 tooget 것입니다. Excel에서는 hello 자습서를 시작 합니다 및 toohave 클러스터와 연결 된 Azure Blob 저장소 계정이 필요 합니다.

  ![Excel에서 쿼리](media/how-to-discover-classify-personal-data-azure/excel.png)

toolearn 어떻게 toodo이, 방문 hello [파워 쿼리를 사용 하 여 Excel 연결 tooHadoop](../hdinsight/hdinsight-connect-excel-power-query.md) 자습서입니다.

원본: [파워 쿼리를 사용 하 여 연결 Excel tooHadoop](../hdinsight/hdinsight-connect-excel-power-query.md)

## <a name="azure-information-protection-personal-data-classification-for-documents-and-email"></a>Azure Information Protection: 문서 및 전자 메일에 대한 개인 데이터 분류

[Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) Azure 고객 레이블을 tooclassify 적용 내부나 외부 공유 문서를 보호 하 고 통신을 전자 메일로 보낼 수 있습니다. 이러한 항목 중 일부는 고객 또는 직원 개인 정보를 포함할 수 있습니다. 관리자 또는 사용자가 자동 또는 수동으로 규칙 및 조건을 정의할 수 있습니다. 예를 들어 사용자가 신용 카드 정보를 포함 하는 문서를 저장 하는 경우 사용자는 볼 hello 관리자가 구성 된 레이블 권장 합니다.

### <a name="how-do-i-try-it"></a>시도하려면 어떻게 할까요?

Hello를 방문 하는 것이 조직에 적합 한 경우에 Azure Information Protection try toosee toogive 싶으면, [빠른 시작 자습서](https://docs.microsoft.com/information-protection/get-started/infoprotect-quick-start-tutorial)합니다. 기본적인 다섯 단계로 안내 합니다-설치 tooconfiguring 정책 tooseeing 분류, 레이블 지정 및 공유 하 고 작업에서에서-30 분 이내로 수행 하지 않아야 합니다.

### <a name="how-do-i-deploy-it"></a>배포하려면 어떻게 할까요?

조직에 대 한 Azure Information Protection toodeploy 싶으면, 방문 hello [분류, 레이블 지정 및 보호에 대 한 배포 로드맵을](https://docs.microsoft.com/information-protection/plan-design/deployment-roadmap)합니다.

### <a name="is-there-anything-else-i-should-know"></a>알아야 할 다른 항목이 있나요?

충분히 검토 방법 tooset 그 방문 하는 데 도움이 되는 상호 보완적인 정보에 대 한 hello [준비를 설정 하 고, 보호!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)
블로그 게시물을 방문합니다. 및 검사 hello Azure Information Protection에 대 한 자세한 아래에 나열 된 링크에 알아봅니다.

## <a name="azure-search-data-discovery-for-developer-apps"></a>Azure Search: 개발자 앱에 대한 데이터 검색

[Azure Search](https://azure.microsoft.com/services/search/)는 클라우드 검색 솔루션 개발자를 위한 기능이며 응용 프로그램에 다양한 데이터 검색 환경을 제공합니다. Azure 검색 간에 Azure Cosmo DB, Azure SQL 데이터베이스, Azure Blob 저장소, Azure 테이블 저장소 또는 사용자 지정 고객 JSON 데이터에서 제공 하는 사용자 지정 인덱스, toolocate 데이터가 있습니다. Azure 검색 REST API toosearch hello를 사용 하 여 개인 데이터 형식이 나 특정 개인의 개인 데이터 hello에 대 한 Lucene 쿼리를 구성할 수도 있습니다. 기능에는 전체 텍스트 검색, 단순 쿼리 구문 및 Lucene 쿼리 구문이 포함됩니다. 

## <a name="how-do-i-use-sql-tooquery-data"></a>SQL tooquery 데이터를 사용 하려면 어떻게 해야 합니까?

hello 기본 사항으로 toobegin 방문 hello [Azure CosmosD DB: 어떻게 SQL을 사용 하 여 tooquery](../cosmos-db/tutorial-query-documentdb.md) 자습서입니다. hello 자습서 샘플 문서 및 두 개의 샘플 SQL 쿼리 및 결과 제공합니다.

SQL 쿼리를 빌드하는 방법에 대한 자세한 지침은 [Azure Cosmos DB Document DB API에 대한 SQL 쿼리](../cosmos-db/documentdb-sql-query.md)를 방문합니다.

Toolearn 같은 toocreate 데이터베이스 컬렉션을 추가 하 고 데이터를 추가 하는 방법 방문 hello와 새 tooAzure Cosmos DB는 경우 [Azure Cosmos DB: DocumentDB API 웹 앱을 빌드할](../cosmos-db/create-documentdb-dotnet.md) 빠른 시작 자습서입니다. Toodo 원하는 경우.NET, Java, Python, 같은 다른 언어에서이 선택 선호 하는 언어 toohello 사이트를 가져오면 합니다.

## <a name="next-steps"></a>다음 단계

[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50)

[SQL Database 정의](../sql-database/sql-database-technical-overview.md)

[Azure Portal에서 사용할 수 있는 SQL Database 쿼리 편집기](https://azure.microsoft.com/blog/t-sql-query-editor-in-browser-azure-portal/)

[Azure Information Protection이란?](https://docs.microsoft.com/information-protection/understand-explore/what-is-information-protection)

[Azure Rights Management란?](https://docs.microsoft.com/information-protection/understand-explore/what-is-azure-rms)

[Azure Information Protection: 준비, 설정, 보호](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)
