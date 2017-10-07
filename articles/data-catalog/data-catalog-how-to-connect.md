---
title: "aaaHow tooconnect toodata 소스 | Microsoft Docs"
description: "방법-tooarticle tooconnect toodata 원본을 Azure Data Catalog에 검색 하는 방법을 강조 표시 합니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 4e6b27a5-cf75-4012-b88c-333c1fe638e8
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 01d659510c8e67c1238ed488f4eebf511aab7217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-toodata-sources"></a>어떻게 tooconnect toodata 원본
## <a name="introduction"></a>소개
**Microsoft Azure 데이터 카탈로그**는 등록 시스템 및 기업 데이터 원본을 위한 검색 시스템 역할을 하는 완전히 관리되는 클라우드 서비스입니다. 즉, **Azure Data Catalog** 수 있도록 지 원하는 사용자에 대 한 모든 검색, 이해 하 고, 데이터 원본을 사용 하 고 기존 데이터에서 더 값 조직 tooget 수 있도록 지원 됩니다. 이 시나리오의 중요 한 측면에서 사용자 데이터를 검색 한 후 데이터 원본 및의 용도 이해 하는 hello를 사용 하는, tooconnect toohello 데이터 원본 tooput 데이터 toouse 해당 하는 hello 다음 단계입니다.

## <a name="data-source-locations"></a>데이터 원본 위치
데이터 원본 등록 하는 동안 **Azure Data Catalog** hello 데이터 원본에 대 한 메타 데이터를 받습니다. 이 메타 데이터는 hello 데이터 소스 위치의 hello 세부 정보를 포함합니다. hello 위치의 hello 세부 정보 데이터 원본 toodata 원본의 다르지만 hello 필요한 정보 tooconnect을 항상 포함 됩니다. 예를 들어 SQL Server 테이블에 대 한 hello 위치 포함 hello 서버 이름, 데이터베이스 이름, 스키마 이름 및 테이블 이름 hello 위치는 SQL Server Reporting Services 보고서에 대 한 hello 서버 이름 및 hello 경로 toohello 보고서를 포함 하는 동안 합니다. 다른 데이터 원본 유형을 hello 구조와 hello 원본 시스템의 기능을 반영 하는 위치를 갖습니다.

## <a name="integrated-client-tools"></a>통합된 클라이언트 도구
hello 가장 간단한 방법은 tooconnect tooa 데이터 소스는 toouse hello "에 열려 있습니다. …" hello에 메뉴 **Azure Data Catalog** 포털입니다. 이 메뉴 toohello 선택한 데이터 자산에 연결 하기 위한 옵션 목록이 표시 됩니다.
이 메뉴는 사용할 수 있는 기본 타일 보기 hello를 사용 하는 경우 각 타일에 hello 합니다.

 ![Hello 데이터 자산 타일에서 SQL Server 테이블을 Excel에서 열기](./media/data-catalog-how-to-connect/data-catalog-how-to-connect1.png)

Hello 목록 보기를 사용할 때는 hello 메뉴는 hello 창의 위쪽에 hello 포털 hello 검색 창에서 사용할 수 있습니다.

 ![Hello 검색 창에서 SQL Server Reporting Services 보고서를 보고서 관리자에서 열기](./media/data-catalog-how-to-connect/data-catalog-how-to-connect2.png)

## <a name="supported-client-applications"></a>지원되는 클라이언트 응용 프로그램
Hello를 사용 하는 경우 "에 열려 있습니다. …" hello Azure Data Catalog 포털에 원본 데이터에 대 한 메뉴, hello 올바른 클라이언트 응용 프로그램 hello 클라이언트 컴퓨터에 설치 해야 합니다.

| 응용 프로그램에서 열기 | 파일 확장명 / 프로토콜 | 지원되는 응용 프로그램 버전 |
| --- | --- | --- |
| Excel |.odc |Excel 2010 이상 |
| Excel (상위 1000) |.odc |Excel 2010 이상 |
| 파워 쿼리 |.xlsx |Excel 2016 또는 Excel 2010 또는 Excel 추가 기능에 대 한 파워 쿼리 hello로 Excel 2013 설치 |
| Power BI Desktop |.pbix |Power BI Desktop 2016년 7월 이상 |
| SQL Server Data Tools |vsweb:// |SQL Server 도구가 설치된 Visual Studio 2013 업데이트 4 이상 |
| 보고서 관리자 |http:// |[SQL Server Reporting Services에 대한 브라우저 요구 사항](https://technet.microsoft.com/en-us/library/ms156511.aspx)을 참조하세요. |

## <a name="your-data-your-tools"></a>데이터, 도구
hello 옵션 hello 메뉴에서 사용할 수 있는 현재 선택 된 데이터 자산의 hello 종류에 따라 달라 집니다. 모든 가능한 도구 hello에 포함 됩니다는 물론, "에서 열기. …" 메뉴 않은 모든 클라이언트 도구를 사용 하 여 아직 쉬울 tooconnect toohello 데이터 원본입니다. 데이터 자산 hello에서 선택 되 면 **Azure Data Catalog** 포털 hello 전체 위치 hello 속성 창에 표시 됩니다.

 ![SQL Server 테이블에 대한 연결 정보](./media/data-catalog-how-to-connect/data-catalog-how-to-connect3.png)

데이터 원본 유형 toodata 소스 형식이 아니라 hello 포털에 포함 된 hello 정보에서 세부 정보가 다 합니다 hello 연결 정보를 제공 합니다 tooconnect toohello 데이터 원본 클라이언트 도구에서 필요한 모든. 사용자가 사용 하 여 검색 하는 hello 데이터 원본에 대 한 hello 연결 세부 정보를 복사할 수 **Azure Data Catalog**, 선택한 해당 도구에서 hello 데이터로 toowork 수 있게 합니다.

## <a name="connecting-and-data-source-permissions"></a>연결 및 데이터 원본 사용 권한
하지만 **Azure Data Catalog** 데이터 소스를 검색 가능한 액세스를 사용 하면 toohello 데이터 자체 hello 데이터 원본 소유자 또는 관리자의 hello 제어에서 사용 중인 상태로 유지 됩니다. 데이터 원본을 검색 **Azure Data Catalog** 사용자 자체 모든 사용 권한을 tooaccess hello 데이터 소스를 제공 하지 않습니다.

toomake 쉽게 사용자에 게는 데이터를 검색할 원본 되지만 하지 않은 권한을 tooaccess 해당 데이터를 사용자가 정보를 제공할 수 hello 속성 액세스 요청에 데이터 원본에 주석 지정 하는 경우. 링크 toohello 프로세스 또는 데이터 원본 액세스에 대 한 연결 지점--포함 여기에 제공 된 정보는 hello 포털에서 데이터 원본 위치 정보 hello와 함께 제공 됩니다.

 ![제공된 액세스 요청 지침을 사용한 연결 정보](./media/data-catalog-how-to-connect/data-catalog-how-to-connect4.png)

## <a name="summary"></a>요약
데이터 원본으로 등록 **Azure Data Catalog** hello 카탈로그 서비스에 hello 데이터 원본의 구조 및 설명이 포함 된 메타 데이터를 복사 하 여 해당 데이터를 검색할 수 있도록 합니다. 데이터 원본 등록 되었으며 발견 되 면 사용자가 toohello 데이터 원본을 연결 hello에서 **Azure Data Catalog** 포털 "에서 열기..." " 데이터 원본에 연결할 수 있습니다.

## <a name="see-also"></a>참고 항목
* [Azure Data Catalog 시작](data-catalog-get-started.md) 방법에 대 한 단계별 정보에 대 한 자습서 tooconnect toodata 원본입니다.
