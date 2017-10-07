---
title: "aaaUse Redgate tooload 데이터 tooyour Azure 데이터 웨어하우스 | Microsoft Docs"
description: "자세한 내용은 방법의 데이터 웨어하우징 시나리오에 대 한 데이터 플랫폼 Studio toouse Redgate 합니다."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 670aef98-31f7-4436-86c0-cc989a39fe7f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 6082390c07c8ffa73ebd8ab272ace00ba8bb1897
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a>Redgate Data Platform Studio를 사용하여 데이터 로드
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)
> * [데이터 팩터리](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

이 자습서에서는 어떻게 toouse [Redgate의 데이터 플랫폼 Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DP) toomove 데이터는 온-프레미스 SQL Server tooAzure SQL 데이터 웨어하우스를에서 합니다. 데이터 플랫폼 Studio hello 가장 적합 한 호환성 픽스를 적용 하 고 최적화, 아니므로 quickest hello 방식으로 tooget SQL 데이터 웨어하우스를 시작 합니다.

> [!NOTE]
> [Redgate](http://www.red-gate.com)는 다양한 SQL Server 도구를 제공하는 오래된 Microsoft 파트너입니다. Data Platform Studio의 이 기능은 상업 및 비상업적 용도 모두에서 무료로 제공됩니다.
> 
> 

## <a name="before-you-begin"></a>시작하기 전에
### <a name="create-or-identify-resources"></a>리소스 만들기 또는 식별
이 자습서를 시작 하기 전에 toohave가 필요 합니다.

* **온-프레미스 SQL Server 데이터베이스**: tooimport tooSQL 데이터 웨어하우스 toocome 온-프레미스 SQL Server에서 필요한 데이터를 hello (버전 2008 r2 이상)입니다. Data Platform Studio는 Azure SQL Database 또는 텍스트 파일에서 직접 가져올 수 없습니다.
* **Azure 저장소 계정**: 데이터 플랫폼 Studio SQL 데이터 웨어하우스에 로드 하기 전에 hello Azure Blob 저장소에는 데이터를 준비 합니다. hello 저장소 계정 hello "클래식" 배포 모델 대신 hello "리소스 관리자" 배포 모델 (hello 기본값) 사용 해야 합니다. 저장소 계정이 없는 경우에 대해 배울 방법 tooCreate 저장소 계정입니다. 
* **SQL 데이터 웨어하우스**:이 자습서 hello 데이터 이동 온-프레미스 SQL Server 데이터 웨어하우스 tooSQL에서 toohave 필요는 온라인 데이터 웨어하우스 합니다. 데이터 웨어하우스 아직 없는 경우에 대해 배울 방법 tooCreate Azure SQL 데이터 웨어하우스 합니다.

> [!NOTE]
> Hello 저장소 계정 및 데이터 웨어하우스 hello에에서 만들어집니다 hello 동일 하면 성능이 향상 됩니다 영역입니다.
> 
> 

## <a name="step-1-sign-in-toodata-platform-studio-with-your-azure-account"></a>1 단계: Azure 계정으로 tooData 플랫폼 Studio에 로그인
웹 브라우저를 열고 탐색 toohello [데이터 플랫폼 Studio](https://www.dataplatformstudio.com/) 웹 사이트입니다. 동일한 Azure 계정 해당 하면 사용한 toocreate hello 저장소 계정 및 데이터 웨어하우스를 hello 하는으로 로그인 합니다. 전자 메일 주소와 회사 또는 학교 계정 및 Microsoft 계정을 연결 된 경우에 tooyour 리소스에 액세스할 수 있는 있는지 toochoose hello 계정 이어야 합니다.

> [!NOTE]
> 데이터 플랫폼 Studio를 사용 하 여 처음으로 이면 toogrant hello 응용 프로그램 사용 권한 toomanage Azure 리소스를 요청 합니다.
> 
> 

## <a name="step-2-start-hello-import-wizard"></a>2 단계: hello 가져오기 마법사 시작
Hello DP 기본 화면에서 hello 가져오기 tooAzure SQL 데이터 웨어하우스 링크 toostart hello 가져오기 마법사를 선택 합니다.

![][1]

## <a name="step-3-install-hello-data-platform-studio-gateway"></a>3 단계: hello 데이터 플랫폼 Studio 게이트웨이 설치
tooconnect tooyour 온-프레미스 SQL Server 데이터베이스 tooinstall hello DP 게이트웨이가 필요합니다. hello 게이트웨이 액세스 tooyour 온-프레미스 환경, hello 데이터를 추출 및 tooyour 저장소 계정에 업로드 제공 하는 클라이언트 에이전트입니다. 데이터는 Redgate 서버를 통과하지 않습니다. tooinstall hello 게이트웨이:

1. Hello 클릭 **게이트웨이 만들기** 링크
2. 다운로드 및 사용 하 여 설치 hello 게이트웨이 hello 제공 된 설치 관리자

![][2]

> [!NOTE]
> hello 게이트웨이 네트워크 액세스 toohello 원본 SQL Server 데이터베이스를 사용 하 여 컴퓨터에 설치할 수 있습니다. Windows 인증을 사용 하 여 hello 현재 사용자의 hello 자격 증명 hello SQL Server 데이터베이스에 액세스 합니다.
> 
> 

설치 되 면에 게이트웨이 상태 변경 내용을 tooConnected hello च े ं 수 있습니다.

## <a name="step-4-identify-hello-source-database"></a>4 단계: hello 원본 데이터베이스를 식별 합니다.
Hello에 *서버 이름 입력* hello 데이터베이스를 호스팅하는 hello 서버 이름을 입력 하 고 선택 하는 텍스트 상자 **다음**합니다. 그런 다음 hello 드롭 다운 메뉴에서의 tooimport 데이터 hello 데이터베이스를 선택 합니다.

![][3]

DP은 tooimport 테이블에 대 한 hello 선택한 데이터베이스를 검사합니다. 기본적으로 DP hello 데이터베이스의 모든 hello 테이블을 가져옵니다. 선택할 수도 있고 모든 테이블에 연결 하는 hello를 확장 하 여 테이블을 선택 취소 합니다. Hello 다음 단추 toomove 앞으로 선택 합니다.

## <a name="step-5-choose-a-storage-account-toostage-hello-data"></a>5 단계: 저장소 계정 toostage hello 데이터 선택
DP 위치 toostage hello 데이터에 대 한 라는 메시지를 표시 합니다. 구독에서 기존 저장소 계정을 선택하고 **다음**을 선택합니다.

> [!NOTE]
> DP은 hello 선택한 저장소 계정에서에서 새 blob 컨테이너를 만들고 각 가져오기에 대 한 별도 폴더를 사용 하 여 됩니다.
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a>6단계: 데이터 웨어하우스 선택
다음으로, 온라인 선택 하면 [Azure SQL 데이터 웨어하우스](http://aka.ms/sqldw) tooimport hello 데이터를 데이터베이스입니다. Tooenter hello 자격 증명 tooconnect toohello 필요한 데이터베이스를 선택한 후 선택한 데이터베이스 **다음**합니다.

![][5]

> [!NOTE]
> DP은 hello 데이터 웨어하우스로 hello 원본 데이터 테이블을 병합합니다. DP 경우 hello 테이블 이름이 필요한 toooverwrite hello 데이터 웨어하우스에 있는 기존 테이블 경고 메시지를 표시 합니다. 가져오기 전에 모든 기존 개체 삭제 틱 하 여 hello 데이터 웨어하우스의 모든 기존 개체를 선택적으로 삭제할 수 있습니다.
> 
> 

## <a name="step-7-import-hello-data"></a>7 단계: hello 데이터 가져오기
DP 싶다는 의사를 tooimport hello 데이터를 확인 합니다. Hello 시작 가져오기 단추 toobegin hello 데이터 가져오기를 클릭 하면 됩니다.

![][6]

DP은 hello 추출 하 고 hello hello 온-프레미스 SQL Server 및 hello hello 가져오기 진행률이 SQL 데이터 웨어하우스로 데이터를 업로드 하는 중 진행 상황을 보여 주는 시각적으로 표시 합니다.

![][7]

Hello 가져오기가 완료 되 면 DP hello 데이터 가져오기에 대 한 요약 및의 hello 호환성 수정 수행 된 변경 내용 보고서를 표시 합니다.

![][8]

## <a name="next-steps"></a>다음 단계
tooexplore SQL 데이터 웨어하우스 내에서 데이터 확인 하 여 시작 합니다.

* [Azure SQL Data Warehouse 쿼리(Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]
* [Power BI를 사용하여 데이터 시각화][Visualize data with Power BI]

toolearn Redgate의 데이터 플랫폼 Studio에 대 한 자세한:

* [Hello DP 홈 페이지를 방문 합니다.](http://www.dataplatformstudio.com/)
* [Channel9에서 DPS 데모 보기](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

다른 방법으로 toomigrate 및 부하의 개요에 대 한 SQL 데이터 웨어하우스에 데이터 참조:

* [사용자 솔루션 tooSQL 데이터 웨어하우스 마이그레이션][Migrate your solution tooSQL Data Warehouse]
* [Azure SQL 데이터 웨어하우스에 데이터 로드](sql-data-warehouse-overview-load.md)

더 많은 개발 팁에 대 한 참조 hello [SQL 데이터 웨어하우스 개발 개요](sql-data-warehouse-overview-develop.md)합니다.

<!--Image references-->
[1]: media/sql-data-warehouse-redgate/2016-10-05_15-59-56.png
[2]: media/sql-data-warehouse-redgate/2016-10-05_11-16-07.png
[3]: media/sql-data-warehouse-redgate/2016-10-05_11-17-46.png
[4]: media/sql-data-warehouse-redgate/2016-10-05_11-20-41.png
[5]: media/sql-data-warehouse-redgate/2016-10-05_11-31-24.png
[6]: media/sql-data-warehouse-redgate/2016-10-05_11-32-20.png
[7]: media/sql-data-warehouse-redgate/2016-10-05_11-49-53.png
[8]: media/sql-data-warehouse-redgate/2016-10-05_12-57-10.png

<!--Article references-->
[Query Azure SQL Data Warehouse (Visual Studio)]: ./sql-data-warehouse-query-visual-studio.md
[Visualize data with Power BI]: ./sql-data-warehouse-get-started-visualize-with-power-bi.md
[Migrate your solution tooSQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
