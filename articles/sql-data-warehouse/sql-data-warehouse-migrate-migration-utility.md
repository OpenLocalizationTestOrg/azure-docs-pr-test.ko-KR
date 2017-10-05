---
title: "마이그레이션: 데이터 웨어하우스 마이그레이션 유틸리티 | Microsoft Docs"
description: "SQL 데이터 웨어하우스로 마이그레이션합니다."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 4d7ad981-ef31-4513-b337-50bdc4709c09
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 2466e823c448ada4dc7bc5769b1b7f10bbb5dc7d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="data-warehouse-migration-utility-preview"></a><span data-ttu-id="db250-103">데이터 웨어하우스 마이그레이션 유틸리티(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="db250-103">Data Warehouse Migration Utility (Preview)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="db250-104">[마이그레이션 유틸리티 다운로드][Download Migration Utility]</span><span class="sxs-lookup"><span data-stu-id="db250-104">[Download Migration Utility][Download Migration Utility]</span></span>
> 
> 

<span data-ttu-id="db250-105">데이터 웨어하우스 마이그레이션 유틸리티는 SQL 서버 및 Azure SQL 데이터베이스에서 Azure SQL 데이터 웨어하우스로 스키마와 데이터를 마이그레이션하기 위해 설계된 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="db250-105">The Data Warehouse Migration Utility is a tool designed to migrate schema and data from SQL Server and Azure SQL Database to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="db250-106">스키마를 마이그레이션하는 동안 이 도구는 해당 스키마를 소스에서 대상으로 자동으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="db250-106">During schema migration, the tool automatically maps the corresponding schema from source to destination.</span></span> <span data-ttu-id="db250-107">스키마가 마이그레이션된 후 이 도구는 자동으로 생성된 스크립트를 사용하여 데이터를 이동하는 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="db250-107">After the schema has been migrated, the tools provides the option to move data with automatically generated scripts.</span></span>

<span data-ttu-id="db250-108">이 도구는 스키마 및 데이터 마이그레이션 외에도, 효율적인 마이그레이션을 방해하는 대상 및 소스 간 비호환성을 요약하는 호환성 보고서를 생성하는 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="db250-108">In addition to schema and data migration, this tool gives you the option to generate compatibility reports which summarize incompatibilities between the target and source instances which would prevent streamlined migration.</span></span>

## <a name="get-started"></a><span data-ttu-id="db250-109">시작</span><span class="sxs-lookup"><span data-stu-id="db250-109">Get started</span></span>
<span data-ttu-id="db250-110">설치를 위한 필수 요소로 마이그레이션 스크립트를 실행하기 위한 BCP 명령줄 유틸리티와 호환성 보고서를 보기 위한 Office가 필요합니다</span><span class="sxs-lookup"><span data-stu-id="db250-110">As a prerequisite for installation, you will need the BCP command-line utility to run migration scripts and Office to view the compatibility report.</span></span> <span data-ttu-id="db250-111">다운로드한 실행 파일을 실행하면 도구를 설치하기 전에 표준 EULA에 동의하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="db250-111">After launching the executable that is downloaded you will be prompted to accept a standard EULA before the tool will be installed.</span></span>

<span data-ttu-id="db250-112">또한 마이그레이션 유틸리티를 실행하려면 마이그레이션하려는 데이터베이스에서 CREATE DATABASE, ALTER ANY DATABASE 또는 VIEW ANY DEFINITION 권한 중 하나가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db250-112">In addition, to run the Migration Utiliy, you will need the one following permissions on the database that you are looking to migrate: CREATE DATABASE, ALTER ANY DATABASE or VIEW ANY DEFINITION.</span></span>

### <a name="launching-the-tool-and-connecting"></a><span data-ttu-id="db250-113">도구 시작 및 연결</span><span class="sxs-lookup"><span data-stu-id="db250-113">Launching the tool and connecting</span></span>
<span data-ttu-id="db250-114">설치 후 나타나는 바탕 화면 아이콘을 클릭하여 도구를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="db250-114">Launch the tool by clicking on the desktop icon which appears post install.</span></span> <span data-ttu-id="db250-115">도구를 열면 초기 연결 페이지가 표시됩니다. 여기에서 마이그레이션 도구의 원본 및 대상을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db250-115">Upon opening the tool, you will be prompted with an initial connection page where you can choose your source and destination for the migration tool.</span></span> <span data-ttu-id="db250-116">현재는 원본으로 SQL Server 및 Azure SQL 데이터베이스를, 대상으로 SQL 데이터 웨어하우스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="db250-116">At this time, we support SQL Server and Azure SQL Database as sources and SQL Data Warehouse as a destination.</span></span> <span data-ttu-id="db250-117">선택한 후에는 서버 이름을 입력하고 인증한 후 '연결'을 클릭하여 소스 서버에 연결하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="db250-117">After selecting this you will be asked to connect to your source server by filling in server name and authenticating and then clicking ‘Connect’.</span></span>

<span data-ttu-id="db250-118">인증한 후 도구는 연결된 서버에 있는 데이터베이스 목록을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="db250-118">After authenticating, the tool will show a list of databases that are present in the server which you are connected to.</span></span> <span data-ttu-id="db250-119">마이그레이션할 데이터베이스를 선택한 후 '마이그레이션 선택됨'을 클릭하여 마이그레이션을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db250-119">You can begin the migration by selecting a database that you would like to migrate and then clicking on ‘Migrate selected’.</span></span>

## <a name="migration-report"></a><span data-ttu-id="db250-120">마이그레이션 보고서</span><span class="sxs-lookup"><span data-stu-id="db250-120">Migration report</span></span>
<span data-ttu-id="db250-121">도구에서 '데이터베이스 호환성 검사'를 선택하면 마이그레이션하려는 데이터베이스에서 모든 개체 비호환성을 요약하는 보고서가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="db250-121">Selecting ‘Check Database Compatibility’ in the tool will generate a report summarizing all object incompatibilities in the database you requested to migrate.</span></span> <span data-ttu-id="db250-122">SQL Data Warehouse에 없는 SQL Server 기능에 대한 광범위한 목록은 [마이그레이션 설명서][migration documentation]에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db250-122">A broader list of some of the SQL Server functionality that is not present in SQL Data Warehouse can be found in our [migration documentation][migration documentation].</span></span> <span data-ttu-id="db250-123">보고서가 생성되면 Excel에서 보고서를 저장하고 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db250-123">After the report is generated you will be able to save and open the report in Excel.</span></span>

<span data-ttu-id="db250-124">마이그레이션 스키마를 생성할 때는 '개체'로 식별되는 대부분의 문제가 해당 데이터의 즉각적인 마이그레이션을 허용하기 위해 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="db250-124">Please note that when generating the migration schema, most issues identified as ‘Object’ will be adjusted in order to allow immediate migration of that data.</span></span> <span data-ttu-id="db250-125">해당 스키마가 적용되기 전에 추가로 조정되지 않도록 변경 내용을 검토하십시오.</span><span class="sxs-lookup"><span data-stu-id="db250-125">Please review the changes to ensure you do not want to make additional adjustments before applying the schema.</span></span>

## <a name="migrate-schema"></a><span data-ttu-id="db250-126">마이그레이션 스키마</span><span class="sxs-lookup"><span data-stu-id="db250-126">Migrate schema</span></span>
<span data-ttu-id="db250-127">연결한 후에는 '스키마 마이그레이션'을 선택하면 선택한 테이블에 대한 스키마 마이그레이션 스크립트가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="db250-127">After connecting, selecting ‘Migrate Schema’ will generate a schema migration script for the selected tables.</span></span> <span data-ttu-id="db250-128">이 스크립트는 테이블 구조를 포팅하고 호환되지 않는 데이터 형식을 보다 호환 가능한 양식으로 매핑하며 마이그레이션 설정에서 사용자가 표시한 경우 보안 자격 증명 및 스키마를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="db250-128">This script ports the structure of the table, maps incompatible data types to more compatible forms, and creates security credentials and schema if this is indicated by the user in the migration settings.</span></span> <span data-ttu-id="db250-129">이 코드는 대상 SQL 데이터 웨어하우스 인스턴스에 대해 실행할 수 있으며 파일로 저장하고 클립보드에 복사하거나 추가 작업을 수행하기 전에 인라인으로 편집할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db250-129">This code can be run against the targeted SQL Data Warehouse instance, saved to a file, copied to your clipboard, or even edited in-line before taking further action.</span></span>  

<span data-ttu-id="db250-130">위에 언급된 것처럼 스키마를 마이그레이션할 때는 도구에서 마이그레이션 변경 내용을 검토하여 완전히 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db250-130">As noted above, when migrating schema review the migration changes that the tool has made in order to ensure that that you fully understand them.</span></span>  

## <a name="migrate-data"></a><span data-ttu-id="db250-131">데이터 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="db250-131">Migrate data</span></span>
<span data-ttu-id="db250-132">'데이터 마이그레이션' 옵션을 클릭하여 먼저 데이터를 서버의 플랫 파일로 이동한 후 SQL 데이터 웨어하우스로 직접 이동하는 BCP 스크립트를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db250-132">By clicking the ‘Migrate Data’ option you can generate BCP scripts that will move your data first to flat files on your server, and then directly into your SQL Data Warehouse.</span></span> <span data-ttu-id="db250-133">다시 시도가 기본 제공되지 않고 네트워크 연결이 끊길 경우 오류가 발생할 수 있으므로 적은 양의 데이터 이동에는 이 프로세스를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="db250-133">We recommend this process for moving small amounts of data and, as retries are not built-in and failures may occur if there is a loss of the network connection.</span></span> <span data-ttu-id="db250-134">이를 실행하기 위해서는 BCP 명령줄 유틸리티가 설치되어 있어야 하며 데이터에 대한 스키마가 이미 생성되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db250-134">In order to run this, you will need to have the BCP command-line utility installed and the schema for the data must already have been created.</span></span>

<span data-ttu-id="db250-135">위의 매개 변수를 입력한 후 마이그레이션 실행을 클릭하기만 하면 두 패키지 집합이 지정된 위치에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="db250-135">After you have filled out the parameters above you simply need to click run migration and a set of two packages will be generated to your specified location.</span></span> <span data-ttu-id="db250-136">마이그레이션 소스에서 플랫 파일로 데이터를 내보내려면 파일 내보내기를 실행하고 데이터를 SQL 데이터 웨어하우스로 가져오려면 파일 가져오기를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="db250-136">Run the export file in order to export data from your migration source into flat files, and run the import file in order to import your data into SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db250-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="db250-137">Next steps</span></span>
<span data-ttu-id="db250-138">일부 데이터를 마이그레이션했으니 [개발][develop] 방법을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="db250-138">Now that you've migrated some data, check out how to [develop][develop].</span></span>

<!--Image references-->

<!--Article references-->
[migration documentation]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md

<!--Other Web references--> 
[Download Migration Utility]: https://migrhoststorage.blob.core.windows.net/sqldwsample/DataWarehouseMigrationUtility.zip
