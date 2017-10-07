---
title: "데이터 카탈로그 용어 aaaAzure | Microsoft Docs"
description: "이 문서에서는 소개 tooconcepts 및 Azure Data Catalog 설명서에서 사용 되는 용어를 제공 합니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6fec74d9-4a3c-4b4b-88ba-cad5ad143331
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: b5f071db4f62c914d2c1cdef9aa686b18d5297d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-terminology"></a>Azure 데이터 카탈로그 용어
## <a name="catalog"></a>카탈로그
hello Azure Data Catalog는 클라우드 기반 메타 데이터 저장소는 데이터에서 원본 및 데이터 자산을 등록할 수 있습니다. hello 카탈로그는 사용자가 추가한 설명 메타 데이터 및 데이터 원본에서 추출 된 구조적 메타 데이터에 대 한 중앙 저장소 위치로 사용 됩니다.

## <a name="data-source"></a>데이터 원본
데이터 원본은 데이터 자산을 관리하는 시스템 또는 컨테이너입니다. SQL Server 데이터베이스, Oracle 데이터베이스, SQL Server Analysis Services 데이터베이스(테이블 형식 또는 다차원) 및 SQL Server Reporting Services 서버를 예로 들 수 있습니다.

## <a name="data-asset"></a>데이터 자산
데이터 자산은 hello catalog에 등록할 수 있는 데이터 원본 내에 포함 된 개체입니다. SQL Server 테이블 및 뷰, Oracle 테이블 및 뷰, SQL Server Analysis Services 측정값, 차원 및 KPI, SQL Server Reporting Services 보고서를 예로 들 수 있습니다.

## <a name="data-asset-location"></a>데이터 자산 위치
hello 카탈로그 저장 hello 위치 데이터 원본 또는 데이터 자산 사용된 tooconnect toohello 될 수 있는 클라이언트 응용 프로그램을 사용 하 여 원본입니다. hello 형식과 hello 위치에 대 한 세부 정보 hello 데이터 원본 유형에 따라 다릅니다. 예를 들어, SQL Server Reporting Services 보고서가 URL로 식별되는 반면, SQL Server 테이블은 네 부분의 이름(서버 이름, 데이터베이스 이름, 스키마 이름, 개체 이름)으로 식별됩니다.

## <a name="structural-metadata"></a>구조적 메타데이터
구조적 메타 데이터는 데이터 자산의 hello 구조를 설명 하는 데이터 원본에서 추출 된 hello 메타 데이터입니다. 여기에 hello 자산 위치, 개체 이름 및 형식 및 형식 관련 특성을 추가 합니다. 예를 들어, 테이블 및 뷰에 대 한 구조적 메타 데이터가 hello hello 이름과 hello 개체의 열에 대 한 데이터 형식을 포함합니다.

## <a name="descriptive-metadata"></a>설명이 포함된 메타데이터
설명이 포함 된 메타 데이터는 hello 용도나 데이터 자산의 의도 설명 하는 메타 데이터입니다. 카탈로그 사용자 hello Azure Data Catalog 포털을 사용 하 여 설명 메타 데이터는 추가 하는 일반적으로 되지만 추출할 수 있습니다 hello 데이터 원본의 등록 중입니다. 예를 들어 hello Azure Data Catalog 등록 추출 됩니다 설명 hello 및 SQL Server Analysis Services 및 SQL Server Reporting Services의 Description 속성 hello에서 [확장 속성ms_description](https://technet.microsoft.com/library/ms190243.aspx)이러한 속성 값으로 채워진 경우 SQL Server 데이터베이스에 있습니다.

## <a name="request-access"></a>액세스 요청
설명이 포함 된 메타 데이터는 데이터 자산 toorequest toohello 데이터 자산 또는 데이터 원본 액세스 하는 방법에 대 한 정보를 포함할 수 있습니다. 이 정보 hello 데이터 자산 배치 표시 되 고 hello 다음 옵션 중 하나 이상을 포함할 수 있습니다.

* hello hello 사용자 또는 toohello 데이터 원본 액세스 권한 부여를 담당 하는 팀의 전자 메일 주소입니다.
* hello의 hello URL 사용자 toogain access toohello 데이터 소스를 수행 해야 하는 프로세스를 문서화 합니다.
* id 및 액세스 관리 도구 (예: Microsoft Identity Manager) 사용 하는 toogain access toohello 데이터 소스 일 수 있는의 hello URL입니다.
* 사용자가 액세스 toohello 데이터 소스를 사용할 수는 방법을 설명 하는 자유 텍스트 항목입니다.

## <a name="preview"></a>미리 보기
Azure 데이터 카탈로그에서 미리 보기는 too20 레코드만 등록 하는 동안 hello 데이터 원본에서 추출 하 고 hello 데이터 자산 메타 데이터와 hello 카탈로그에 저장 된 수의 한 스냅숏입니다. hello 미리 보기의 활용 데이터 자산을 검색 하는 사용자는 해당 기능 및 용도 더 잘 이해 합니다. 즉, 샘플 데이터를 보지 방금 hello 열 이름과 데이터 형식을 표시 하는 보다 더욱 중요할 수 있습니다.
미리 보기 테이블 및 뷰와에 지원 됩니다 및 등록 하는 동안 hello 사용자가 명시적으로 선택할 수 있어야 합니다.

## <a name="data-profile"></a>데이터 프로필
Azure Data Catalog에서 데이터 프로필은 등록 중 hello 데이터 원본에서 추출 하 고 hello 데이터 자산 메타 데이터와 hello 카탈로그에 저장 된 수 있는 등록 된 데이터 자산에 대 한 테이블 수준 추적과 열 수준 메타 데이터의 스냅숏입니다. 데이터 프로필 hello 도와 데이터 자산을 검색 하는 사용자는 해당 기능 및 용도 더 잘 이해 합니다. 등록 하는 동안 hello 사용자가 비슷한 toopreviews, 데이터 프로필을 명시적으로 선택할 수 해야 합니다.

> [!NOTE]
> 수 크게 증가 hello 필요한 시간 tooregister 데이터 소스 있으며 데이터 프로필을 추출 합니다. 큰 테이블 뷰에 대 한 비용이 많이 드는 작업 수 있습니다.
>
>

## <a name="user-perspective"></a>사용자 관점
Azure 데이터 카탈로그에서 모든 사용자가 등록된 데이터 자산에 대해 설명이 포함된 메타데이터를 제공할 수 있습니다. 각 사용자에 게 hello 데이터와 해당 사용에 대해 고유한 관점입니다. 예를 들어 서버 담당 관리자에 게 해당 서비스 수준 계약 (SLA) 또는 백업 기간;의 hello 세부 정보를 제공할 수 있습니다. 데이터 관리자 hello 비즈니스에 대 한 링크 toodocumentation hello 데이터 지원; 처리를 제공할 수 있습니다. 그리고 분석가 관련성이 가장 높은 tooother 분석가 있으며 가장 중요 한 toothose 사용자에 게 toodiscover 필요 하 고 hello 데이터 이해 수 있는 hello 조건에 설명을 제공할 수 있습니다.

각각의 이러한 큐브 뷰는 기본적으로 유용 하 고 Azure Data Catalog 각 사용자 hello 정보 모든 사용자가 해당 정보 toounderstand hello 데이터와 해당 용도 사용할 수 있지만 의미 있는 toothem를 제공할 수 있습니다.

## <a name="expert"></a>전문가
전문가는 데이터 자산에 대해 잘 아는 “전문가” 관점이 있는 사용자입니다. 모든 사용자는 사용자 자신을 추가하거나 다른 사용자를 자산에 대한 전문가로 추가할 수 있습니다. 전문가로 나열 되 고 Azure Data Catalog;에 추가 권한이 나타내지 않습니다. 사용자가 수 tooeasily 자산 설명 메타 데이터를 검토할 때 유용할 가능성이 가장 높은 toobe 있는 해당 큐브 뷰를 찾습니다.

## <a name="owner"></a>소유자
소유자는 Azure 데이터 카탈로그에서 데이터 자산을 관리하기 위한 추가 권한이 있는 사용자입니다. 사용자는 등록된 자산 데이터의 소유권을 가져올 수 있으며 소유자는 다른 사용자를 공동 소유자로 추가할 수 있습니다. 자세한 내용은 참조 [어떻게 toomanage 데이터 자산](data-catalog-how-to-manage.md)  

> [!NOTE]
> 소유권 및 관리는 hello 표준 버전의 Azure Data Catalog에만 사용할 수 있습니다.
>
>

## <a name="registration"></a>등록
등록은 hello 데이터 원본에서 데이터 자산 메타 데이터를 추출 하 고 작업입니다 toohello Azure Data Catalog 서비스를 복사 합니다. 등록된 데이터 자산은 주석을 첨부하고 검색할 수 있습니다.

## <a name="see-also"></a>참고 항목
* [Azure 데이터 카탈로그란?](data-catalog-what-is-data-catalog.md) -이 문서는 hello Azure Data Catalog 서비스, hello 값을 제공 및 지원 hello 시나리오의 개요를 제공 합니다.
* [Azure Data Catalog 시작](data-catalog-get-started.md) -이 문서에서는 어떻게 toouse Azure 데이터는 데이터 원본 검색에 대 한을 카탈로그를 보여 주는 종단 간 자습서를 제공 합니다.  
