---
title: "Azure Analysis Services에서 지원 되는 aaaData 원본 | Microsoft Docs"
description: "Azure Analysis Services의 데이터 모델에 지원되는 데이터 원본에 대해 설명합니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 6ec63319-ff9b-4b01-a1cd-274481dc8995
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 2902d7d3c3bcf086419822fa826193bd247bde61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-sources-supported-in-azure-analysis-services"></a>Azure Analysis Services에서 지원되는 데이터 원본
Azure Analysis Services 서버 hello 클라우드 및 온-프레미스 조직에서 toodata 원본 연결을 지원합니다. 지원 되는 데이터 원본은 추가로 hello 항상 추가 되 고 됩니다. 자주 확인하세요. 

데이터 원본 hello는 현재 지원 됩니다.

| 클라우드  |
|---|
| Azure Blob Storage*  |
| Azure SQL 데이터베이스  |
| Azure Data Warehouse |


| 온-프레미스  |   |   |   |
|---|---|---|---|
| Access 데이터베이스  | 폴더* | Oracle 데이터베이스  | Teradata 데이터베이스 |
| Active Directory*  | JSON 문서*  | Postgre SQL Database*  |XML 테이블* |
| Analysis Services  | 이진의 줄*  | SAP HANA*  |
| 분석 플랫폼 시스템  | MySQL 데이터베이스  | SAP Business Warehouse*  | |
| Dynamics CRM*  | OData 피드*  | SharePoint*  |
| Excel 통합 문서  | ODBC 쿼리  | SQL Database  |
| Exchange*  | OLE DB  | Sybase 데이터베이스  |

\* 테이블 형식 1400 모델에만 해당합니다. 

> [!IMPORTANT]
> Tooon 온-프레미스 데이터 원본을 사용 하려면 연결 된 [온-프레미스 데이터 게이트웨이](analysis-services-gateway.md) 사용자 환경에서 컴퓨터에 설치 합니다.

## <a name="data-providers"></a>데이터 공급자

Azure Analysis Services에서 데이터 모델 toocertain 데이터 원본에 연결할 때 서로 다른 데이터 공급자를 필요할 수 있습니다. 경우에 따라 테이블 형식 모델 SQL Server Native Client (SQLNCLI11)와 같은 네이티브 공급자를 사용 하 여 toodata 원본 연결 오류를 반환할 수 있습니다.

Tooa 클라우드 데이터를 연결 하는 데이터 모델에 대 한 Azure SQL 데이터베이스 같은 원본, SQLOLEDB 이외의 네이티브 공급자를 사용 하면 오류 메시지가 표시 될 수 있습니다: **"hello provider 'SQLNCLI11.1' 등록 되지 않았습니다."** 네이티브 공급자를 사용 하는 경우 DirectQuery 모델 tooon 온-프레미스 데이터 원본 연결에 있는 경우 오류 메시지가 표시 될 수 있습니다 또는: **"OLE DB 행 집합을 만드는 오류가 발생 했습니다. 'LIMIT' 가까이에 잘못된 구문이 있습니다."**라는 오류 메시지가 나타날 수 있습니다.

데이터 원본 공급자에 따라 hello hello 클라우드 또는 온-프레미스에 연결 toodata 소스는 경우 메모리 내 또는 DirectQuery 데이터 모델에 대 한 지원 됩니다.

### <a name="cloud"></a>클라우드
| **데이터 원본** | **메모리 내** | **DirectQuery** |
|  --- | --- | --- |
| Azure SQL 데이터 웨어하우스 |SQL Server용 .NET Framework 데이터 공급자 |SQL Server용 .NET Framework 데이터 공급자 |
| Azure SQL 데이터베이스 |SQL Server용 .NET Framework 데이터 공급자 |SQL Server용 .NET Framework 데이터 공급자 | |

### <a name="on-premises-via-gateway"></a>온-프레미스(게이트웨이 사용)
|**데이터 원본** | **메모리 내** | **DirectQuery** |
|  --- | --- | --- |
| SQL Server |SQL Server Native Client 11.0 |SQL Server용 .NET Framework 데이터 공급자 |
| SQL Server |SQL Server용 Microsoft OLE DB Provider |SQL Server용 .NET Framework 데이터 공급자 | |
| SQL Server |SQL Server용 .NET Framework 데이터 공급자 |SQL Server용 .NET Framework 데이터 공급자 | |
| Oracle |Oracle용 Microsoft OLE DB Provider |.NET용 Oracle Data Provider | |
| Oracle |.NET용 Oracle Data Provider |.NET용 Oracle Data Provider | |
| Teradata |Teradata용 OLE DB Provider |.NET용 Teradata Data Provider | |
| Teradata |.NET용 Teradata Data Provider |.NET용 Teradata Data Provider | |
| 분석 플랫폼 시스템 |SQL Server용 .NET Framework 데이터 공급자 |SQL Server용 .NET Framework 데이터 공급자 | |

> [!NOTE]
> 온-프레미스 게이트웨이를 사용할 때 64비트 공급자가 설치되었는지 확인합니다.
> 
> 

온-프레미스 SQL Server Analysis Services 테이블 형식 모델 tooAzure Analysis Services를 마이그레이션하는 경우 필요한 toochange hello 공급자 수 있습니다.

**toospecify 데이터 원본 공급자**

1. SSDT > **테이블 형식 모델 탐색기** > **데이터 원본**에서 데이터 원본 연결을 마우스 오른쪽 단추로 클릭한 다음 **데이터 원본 편집**을 클릭합니다.
2. **연결 편집**, 클릭 **고급** tooopen hello 사전 속성 창.
3. **고급 속성 설정** > **공급자**, 선택 hello 적절 한 공급자가 다음 합니다.

## <a name="impersonation"></a>가장
경우에 따라 필요한 toospecify 다른 가장 계정 수도 있습니다. SSDT 또는 SSMS에서 가장 계정을 지정할 수 있습니다.

온-프레미스 데이터 원본의 경우:

* SQL 인증을 사용하는 경우 가장은 서비스 계정이어야 합니다.
* Windows 인증을 사용하는 경우 Windows 사용자/암호를 설정합니다. SQL Server의 경우 특정 가장 계정을 사용한 Windows 인증은 메모리 내 데이터 모델에 대해서만 지원됩니다.

클라우드 데이터 원본의 경우:

* SQL 인증을 사용하는 경우 가장은 서비스 계정이어야 합니다.

## <a name="next-steps"></a>다음 단계
온-프레미스 데이터 소스를 설정한 경우 수 있는지 tooinstall hello [온-프레미스 게이트웨이](analysis-services-gateway.md)합니다.   
SSDT 또는 SSMS에서 서버 관리에 대 한 더 toolearn 참조 [서버를 관리할](analysis-services-manage.md)합니다.

