---
title: "Microsoft Azure Data Lake 분석의 aaaOverview | Microsoft Docs"
description: "Data Lake 분석에는 크기에 관계 없이 hello 클라우드의 데이터에서 얻은 정보를 사용 하 여 비즈니스 데이터 toodrive를 사용할 수 있는 경우 또는 Azure의 빅 데이터 서비스입니다."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 1e1d443a-48a2-47fb-bc00-bf88274222de
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/23/2017
ms.author: saveenr
ms.openlocfilehash: 15bcd549c5aeb167da1338f253270ad57f8c5123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-microsoft-azure-data-lake-analytics"></a>Microsoft Azure Data Lake Analytics 개요
## <a name="what-is-azure-data-lake-analytics"></a>Azure Data Lake Analytics이란?
Azure Data Lake 분석 주문형으로 분석 작업 서비스 toosimplify 빅 데이터 분석 이며 분산된 인프라 작업보다는 작업 작성, 실행 및 관리에 초점을 맞출 수 있습니다. 배포, 구성 및 하드웨어를 튜닝 하는 대신 쿼리 tootransform 데이터를 작성 하 고 귀중 한 통찰력을 추출 합니다. hello 분석 서비스 필요한 능력에 대 한 hello 전화를 설정 하 여 모든 규모의 작업을 즉시 처리할 수 있습니다. 실행할 때 작업 기준으로 비용이 부과되므로 비용 효과적일 수 있습니다. hello 분석 서비스는 Azure Active Directory를 액세스 및 역할 관리, 온-프레미스 id 시스템과 통합할 수 있도록 지원 합니다. 또한 U-SQL, 사용자 코드의 역대 hello sql hello 혜택을 통합 하는 언어를 포함 합니다. U-SQL의 확장 가능한 분산된 런타임을 사용 하면 tooefficiently hello 저장소에서 및 Azure, Azure SQL 데이터베이스 및 Azure SQL 데이터 웨어하우스 SQL Server 간에 데이터를 분석 합니다.

## <a name="key-capabilities"></a>주요 기능
* **동적 크기 조정**
  
    Data Lake Analytics은 클라우드 규모 및 성능에 맞게 설계되었습니다.  이 서비스를 통해 리소스를 동적으로 프로비전하고 테라바이트 또는 심지어 엑사바이트 단위의 데이터도 분석할 수 있습니다. Hello 작업이 완료 되 면 자동으로 리소스 아래로 강풍 및 처리 능력을 사용 하는 hello에 대해서만 비용을 지불 합니다. Hello 저장 된 데이터 크기를 늘리려면 줄이거나 사용 하는 계산 리소스의 양을 hello 대로 toorewrite 코드가 필요는 없습니다. 대용량 데이터 집합을 처리하고 저장하는 방법 대신 비즈니스 논리에만 집중할 수 있습니다.
* **친숙한 도구를 사용하여 더 빠르게 개발하고 더 스마트하게 디버그 및 최적화 수행**
  
    데이터 레이크 분석에는 Visual Studio와 완벽 한 통합, toorun 친숙 한 도구를 사용할 수 있도록 디버그 및 코드를 조정 합니다. U-SQL 작업의 시각화를 통해 코드가 실행되는 방식을 전체적으로 확인할 수 있으므로 성능 병목 현상을 쉽게 식별하고 비용을 최적화할 수 있습니다.
* **U-SQL: 간편하고 친숙하면서도 강력하고 확장 가능**
  
    Data Lake 분석 U-SQL, C#의 역대 hello와 SQL의의 hello 친숙 한 간단 하 고 선언적 특성을 확장 하는 쿼리 언어를 포함 합니다. hello U SQL 언어는 기반으로 hello distributed 동일 Microsoft 내부 hello 빅 데이터 시스템을 구동 하는 런타임입니다. 이제 수많은 SQL 및.NET 개발자가 처리 하 고 이미 있는 hello 기술 함께 해당 데이터를 분석할 수 있습니다.
* **기존 IT 투자에 원활하게 통합**
  
    Data Lake Analytics은 ID, 관리, 보안 및 데이터 웨어하우징에 대한 기존 IT 투자를 사용할 수 있습니다. 이 방법은 데이터 거 버 넌 스를 단순화 하 고 쉽게 tooextend를 사용 하면 현재 데이터 응용 프로그램입니다. Data Lake Analytics은 사용자 관리 및 권한에 대해 Active Directory와 통합되고 기본 제공 모니터링 및 감사와 함께 제공됩니다.
* **저렴하고 경제적**
  
    Data Lake Analytics은 빅 데이터 작업을 실행하기 위한 경제적인 솔루션입니다. 데이터가 처리될 때 작업 단위로 비용을 지불합니다. 하드웨어, 라이선스 또는 서비스별 지원 계약이 필요하지 않습니다. hello 시스템을 자동으로 조정 위로 또는 아래로 hello 작업이 시작 되 고 완료 되 면 필요한 것 보다 더 하지 지불 하므로 합니다.
* **모든 Azure 데이터 작업**
  
    Data Lake 분석은 최적화 toowork와 Azure 데이터 레이크-hello 최고 수준의 성능과 처리량, 빅 데이터 작업에 대 한 병렬 처리 기능을 제공 합니다.  또한 Data Lake Analytics는 Azure Blob Storage 및 Azure SQL Database에서 작업할 수도 있습니다.

## <a name="next-steps"></a>다음 단계
 
  * [Azure Portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI](data-lake-analytics-get-started-cli2.md)를 사용하여 Data Lake Analytics 시작
  * [Azure Portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md) | [Azure .NET SDK](data-lake-analytics-manage-use-dotnet-sdk.md) | [Node.js](data-lake-analytics-manage-use-nodejs.md)를 사용하여 Azure Data Lake Analytics 관리
  * [Azure Portal을 사용하여 Azure Data Lake Analytics 작업 모니터링 및 문제 해결](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md) 
