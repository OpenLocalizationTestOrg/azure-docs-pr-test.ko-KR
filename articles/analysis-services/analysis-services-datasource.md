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
# <a name="data-sources-supported-in-azure-analysis-services"></a><span data-ttu-id="bb514-103">Azure Analysis Services에서 지원되는 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="bb514-103">Data sources supported in Azure Analysis Services</span></span>
<span data-ttu-id="bb514-104">Azure Analysis Services 서버 hello 클라우드 및 온-프레미스 조직에서 toodata 원본 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bb514-104">Azure Analysis Services servers support connecting toodata sources in hello cloud and on-premises in your organization.</span></span> <span data-ttu-id="bb514-105">지원 되는 데이터 원본은 추가로 hello 항상 추가 되 고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb514-105">Additional supported data sources are being added all hello time.</span></span> <span data-ttu-id="bb514-106">자주 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="bb514-106">Check back often.</span></span> 

<span data-ttu-id="bb514-107">데이터 원본 hello는 현재 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb514-107">hello following data sources are currently supported:</span></span>

| <span data-ttu-id="bb514-108">클라우드</span><span class="sxs-lookup"><span data-stu-id="bb514-108">Cloud</span></span>  |
|---|
| <span data-ttu-id="bb514-109">Azure Blob Storage*</span><span class="sxs-lookup"><span data-stu-id="bb514-109">Azure Blob Storage*</span></span>  |
| <span data-ttu-id="bb514-110">Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="bb514-110">Azure SQL Database</span></span>  |
| <span data-ttu-id="bb514-111">Azure Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="bb514-111">Azure Data Warehouse</span></span> |


| <span data-ttu-id="bb514-112">온-프레미스</span><span class="sxs-lookup"><span data-stu-id="bb514-112">On-premises</span></span>  |   |   |   |
|---|---|---|---|
| <span data-ttu-id="bb514-113">Access 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="bb514-113">Access Database</span></span>  | <span data-ttu-id="bb514-114">폴더*</span><span class="sxs-lookup"><span data-stu-id="bb514-114">Folder*</span></span> | <span data-ttu-id="bb514-115">Oracle 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="bb514-115">Oracle Database</span></span>  | <span data-ttu-id="bb514-116">Teradata 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="bb514-116">Teradata Database</span></span> |
| <span data-ttu-id="bb514-117">Active Directory*</span><span class="sxs-lookup"><span data-stu-id="bb514-117">Active Directory*</span></span>  | <span data-ttu-id="bb514-118">JSON 문서*</span><span class="sxs-lookup"><span data-stu-id="bb514-118">JSON document*</span></span>  | <span data-ttu-id="bb514-119">Postgre SQL Database*</span><span class="sxs-lookup"><span data-stu-id="bb514-119">Postgre SQL Database*</span></span>  |<span data-ttu-id="bb514-120">XML 테이블*</span><span class="sxs-lookup"><span data-stu-id="bb514-120">XML table*</span></span> |
| <span data-ttu-id="bb514-121">Analysis Services</span><span class="sxs-lookup"><span data-stu-id="bb514-121">Analysis Services</span></span>  | <span data-ttu-id="bb514-122">이진의 줄*</span><span class="sxs-lookup"><span data-stu-id="bb514-122">Lines from binary*</span></span>  | <span data-ttu-id="bb514-123">SAP HANA*</span><span class="sxs-lookup"><span data-stu-id="bb514-123">SAP HANA*</span></span>  |
| <span data-ttu-id="bb514-124">분석 플랫폼 시스템</span><span class="sxs-lookup"><span data-stu-id="bb514-124">Analytics Platform System</span></span>  | <span data-ttu-id="bb514-125">MySQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="bb514-125">MySQL Database</span></span>  | <span data-ttu-id="bb514-126">SAP Business Warehouse*</span><span class="sxs-lookup"><span data-stu-id="bb514-126">SAP Business Warehouse*</span></span>  | |
| <span data-ttu-id="bb514-127">Dynamics CRM*</span><span class="sxs-lookup"><span data-stu-id="bb514-127">Dynamics CRM*</span></span>  | <span data-ttu-id="bb514-128">OData 피드*</span><span class="sxs-lookup"><span data-stu-id="bb514-128">OData Feed*</span></span>  | <span data-ttu-id="bb514-129">SharePoint*</span><span class="sxs-lookup"><span data-stu-id="bb514-129">SharePoint*</span></span>  |
| <span data-ttu-id="bb514-130">Excel 통합 문서</span><span class="sxs-lookup"><span data-stu-id="bb514-130">Excel workbook</span></span>  | <span data-ttu-id="bb514-131">ODBC 쿼리</span><span class="sxs-lookup"><span data-stu-id="bb514-131">ODBC query</span></span>  | <span data-ttu-id="bb514-132">SQL Database</span><span class="sxs-lookup"><span data-stu-id="bb514-132">SQL Database</span></span>  |
| <span data-ttu-id="bb514-133">Exchange*</span><span class="sxs-lookup"><span data-stu-id="bb514-133">Exchange*</span></span>  | <span data-ttu-id="bb514-134">OLE DB</span><span class="sxs-lookup"><span data-stu-id="bb514-134">OLE DB</span></span>  | <span data-ttu-id="bb514-135">Sybase 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="bb514-135">Sybase Database</span></span>  |

<span data-ttu-id="bb514-136">\* 테이블 형식 1400 모델에만 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="bb514-136">\* Tabular 1400 models only.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="bb514-137">Tooon 온-프레미스 데이터 원본을 사용 하려면 연결 된 [온-프레미스 데이터 게이트웨이](analysis-services-gateway.md) 사용자 환경에서 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb514-137">Connecting tooon-premises data sources require an [On-premises data gateway](analysis-services-gateway.md) installed on a computer in your environment.</span></span>

## <a name="data-providers"></a><span data-ttu-id="bb514-138">데이터 공급자</span><span class="sxs-lookup"><span data-stu-id="bb514-138">Data providers</span></span>

<span data-ttu-id="bb514-139">Azure Analysis Services에서 데이터 모델 toocertain 데이터 원본에 연결할 때 서로 다른 데이터 공급자를 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb514-139">Data models in Azure Analysis Services may require different data providers when connecting toocertain data sources.</span></span> <span data-ttu-id="bb514-140">경우에 따라 테이블 형식 모델 SQL Server Native Client (SQLNCLI11)와 같은 네이티브 공급자를 사용 하 여 toodata 원본 연결 오류를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb514-140">In some cases, tabular models connecting toodata sources using native providers such as SQL Server Native Client (SQLNCLI11) may return an error.</span></span>

<span data-ttu-id="bb514-141">Tooa 클라우드 데이터를 연결 하는 데이터 모델에 대 한 Azure SQL 데이터베이스 같은 원본, SQLOLEDB 이외의 네이티브 공급자를 사용 하면 오류 메시지가 표시 될 수 있습니다: **"hello provider 'SQLNCLI11.1' 등록 되지 않았습니다."**</span><span class="sxs-lookup"><span data-stu-id="bb514-141">For data models that connect tooa cloud data source such as Azure SQL Database, if you use native providers other than SQLOLEDB, you may see error message: **“hello provider 'SQLNCLI11.1' is not registered.”**</span></span> <span data-ttu-id="bb514-142">네이티브 공급자를 사용 하는 경우 DirectQuery 모델 tooon 온-프레미스 데이터 원본 연결에 있는 경우 오류 메시지가 표시 될 수 있습니다 또는: **"OLE DB 행 집합을 만드는 오류가 발생 했습니다. 'LIMIT' 가까이에 잘못된 구문이 있습니다."**라는 오류 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb514-142">Or, if you have a DirectQuery model connecting tooon-premises data sources, if you use native providers you may see error message: **“Error creating OLE DB row set. Incorrect syntax near 'LIMIT'”**.</span></span>

<span data-ttu-id="bb514-143">데이터 원본 공급자에 따라 hello hello 클라우드 또는 온-프레미스에 연결 toodata 소스는 경우 메모리 내 또는 DirectQuery 데이터 모델에 대 한 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb514-143">hello following datasource providers are supported for in-memory or DirectQuery data models when connecting toodata sources in hello cloud or on-premises:</span></span>

### <a name="cloud"></a><span data-ttu-id="bb514-144">클라우드</span><span class="sxs-lookup"><span data-stu-id="bb514-144">Cloud</span></span>
| <span data-ttu-id="bb514-145">**데이터 원본**</span><span class="sxs-lookup"><span data-stu-id="bb514-145">**Datasource**</span></span> | <span data-ttu-id="bb514-146">**메모리 내**</span><span class="sxs-lookup"><span data-stu-id="bb514-146">**In-memory**</span></span> | <span data-ttu-id="bb514-147">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="bb514-147">**DirectQuery**</span></span> |
|  --- | --- | --- |
| <span data-ttu-id="bb514-148">Azure SQL 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="bb514-148">Azure SQL Data Warehouse</span></span> |<span data-ttu-id="bb514-149">SQL Server용 .NET Framework 데이터 공급자</span><span class="sxs-lookup"><span data-stu-id="bb514-149">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="bb514-150">SQL Server용 .NET Framework 데이터 공급자</span><span class="sxs-lookup"><span data-stu-id="bb514-150">.NET Framework Data Provider for SQL Server</span></span> |
| <span data-ttu-id="bb514-151">Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="bb514-151">Azure SQL Database</span></span> |<span data-ttu-id="bb514-152">SQL Server용 .NET Framework 데이터 공급자</span><span class="sxs-lookup"><span data-stu-id="bb514-152">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="bb514-153">SQL Server용 .NET Framework 데이터 공급자</span><span class="sxs-lookup"><span data-stu-id="bb514-153">.NET Framework Data Provider for SQL Server</span></span> | |

### <a name="on-premises-via-gateway"></a><span data-ttu-id="bb514-154">온-프레미스(게이트웨이 사용)</span><span class="sxs-lookup"><span data-stu-id="bb514-154">On-premises (via Gateway)</span></span>
|<span data-ttu-id="bb514-155">**데이터 원본**</span><span class="sxs-lookup"><span data-stu-id="bb514-155">**Datasource**</span></span> | <span data-ttu-id="bb514-156">**메모리 내**</span><span class="sxs-lookup"><span data-stu-id="bb514-156">**In-memory**</span></span> | <span data-ttu-id="bb514-157">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="bb514-157">**DirectQuery**</span></span> |
|  --- | --- | --- |
| <span data-ttu-id="bb514-158">SQL Server</span><span class="sxs-lookup"><span data-stu-id="bb514-158">SQL Server</span></span> |<span data-ttu-id="bb514-159">SQL Server Native Client 11.0</span><span class="sxs-lookup"><span data-stu-id="bb514-159">SQL Server Native Client 11.0</span></span> |<span data-ttu-id="bb514-160">SQL Server용 .NET Framework 데이터 공급자</span><span class="sxs-lookup"><span data-stu-id="bb514-160">.NET Framework Data Provider for SQL Server</span></span> |
| <span data-ttu-id="bb514-161">SQL Server</span><span class="sxs-lookup"><span data-stu-id="bb514-161">SQL Server</span></span> |<span data-ttu-id="bb514-162">SQL Server용 Microsoft OLE DB Provider</span><span class="sxs-lookup"><span data-stu-id="bb514-162">Microsoft OLE DB Provider for SQL Server</span></span> |<span data-ttu-id="bb514-163">SQL Server용 .NET Framework 데이터 공급자</span><span class="sxs-lookup"><span data-stu-id="bb514-163">.NET Framework Data Provider for SQL Server</span></span> | |
| <span data-ttu-id="bb514-164">SQL Server</span><span class="sxs-lookup"><span data-stu-id="bb514-164">SQL Server</span></span> |<span data-ttu-id="bb514-165">SQL Server용 .NET Framework 데이터 공급자</span><span class="sxs-lookup"><span data-stu-id="bb514-165">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="bb514-166">SQL Server용 .NET Framework 데이터 공급자</span><span class="sxs-lookup"><span data-stu-id="bb514-166">.NET Framework Data Provider for SQL Server</span></span> | |
| <span data-ttu-id="bb514-167">Oracle</span><span class="sxs-lookup"><span data-stu-id="bb514-167">Oracle</span></span> |<span data-ttu-id="bb514-168">Oracle용 Microsoft OLE DB Provider</span><span class="sxs-lookup"><span data-stu-id="bb514-168">Microsoft OLE DB Provider for Oracle</span></span> |<span data-ttu-id="bb514-169">.NET용 Oracle Data Provider</span><span class="sxs-lookup"><span data-stu-id="bb514-169">Oracle Data Provider for .NET</span></span> | |
| <span data-ttu-id="bb514-170">Oracle</span><span class="sxs-lookup"><span data-stu-id="bb514-170">Oracle</span></span> |<span data-ttu-id="bb514-171">.NET용 Oracle Data Provider</span><span class="sxs-lookup"><span data-stu-id="bb514-171">Oracle Data Provider for .NET</span></span> |<span data-ttu-id="bb514-172">.NET용 Oracle Data Provider</span><span class="sxs-lookup"><span data-stu-id="bb514-172">Oracle Data Provider for .NET</span></span> | |
| <span data-ttu-id="bb514-173">Teradata</span><span class="sxs-lookup"><span data-stu-id="bb514-173">Teradata</span></span> |<span data-ttu-id="bb514-174">Teradata용 OLE DB Provider</span><span class="sxs-lookup"><span data-stu-id="bb514-174">OLE DB Provider for Teradata</span></span> |<span data-ttu-id="bb514-175">.NET용 Teradata Data Provider</span><span class="sxs-lookup"><span data-stu-id="bb514-175">Teradata Data Provider for .NET</span></span> | |
| <span data-ttu-id="bb514-176">Teradata</span><span class="sxs-lookup"><span data-stu-id="bb514-176">Teradata</span></span> |<span data-ttu-id="bb514-177">.NET용 Teradata Data Provider</span><span class="sxs-lookup"><span data-stu-id="bb514-177">Teradata Data Provider for .NET</span></span> |<span data-ttu-id="bb514-178">.NET용 Teradata Data Provider</span><span class="sxs-lookup"><span data-stu-id="bb514-178">Teradata Data Provider for .NET</span></span> | |
| <span data-ttu-id="bb514-179">분석 플랫폼 시스템</span><span class="sxs-lookup"><span data-stu-id="bb514-179">Analytics Platform System</span></span> |<span data-ttu-id="bb514-180">SQL Server용 .NET Framework 데이터 공급자</span><span class="sxs-lookup"><span data-stu-id="bb514-180">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="bb514-181">SQL Server용 .NET Framework 데이터 공급자</span><span class="sxs-lookup"><span data-stu-id="bb514-181">.NET Framework Data Provider for SQL Server</span></span> | |

> [!NOTE]
> <span data-ttu-id="bb514-182">온-프레미스 게이트웨이를 사용할 때 64비트 공급자가 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bb514-182">Ensure 64-bit providers are installed when using On-premises gateway.</span></span>
> 
> 

<span data-ttu-id="bb514-183">온-프레미스 SQL Server Analysis Services 테이블 형식 모델 tooAzure Analysis Services를 마이그레이션하는 경우 필요한 toochange hello 공급자 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb514-183">When migrating an on-premises SQL Server Analysis Services tabular model tooAzure Analysis Services, it may be necessary toochange hello provider.</span></span>

<span data-ttu-id="bb514-184">**toospecify 데이터 원본 공급자**</span><span class="sxs-lookup"><span data-stu-id="bb514-184">**toospecify a datasource provider**</span></span>

1. <span data-ttu-id="bb514-185">SSDT > **테이블 형식 모델 탐색기** > **데이터 원본**에서 데이터 원본 연결을 마우스 오른쪽 단추로 클릭한 다음 **데이터 원본 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb514-185">In SSDT > **Tabular Model Explorer** > **Data Sources**, right-click a data source connection, and then click **Edit Data Source**.</span></span>
2. <span data-ttu-id="bb514-186">**연결 편집**, 클릭 **고급** tooopen hello 사전 속성 창.</span><span class="sxs-lookup"><span data-stu-id="bb514-186">In **Edit Connection**, click **Advanced** tooopen hello Advance properties window.</span></span>
3. <span data-ttu-id="bb514-187">**고급 속성 설정** > **공급자**, 선택 hello 적절 한 공급자가 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb514-187">In **Set Advanced Properties** > **Providers**, then select hello appropriate provider.</span></span>

## <a name="impersonation"></a><span data-ttu-id="bb514-188">가장</span><span class="sxs-lookup"><span data-stu-id="bb514-188">Impersonation</span></span>
<span data-ttu-id="bb514-189">경우에 따라 필요한 toospecify 다른 가장 계정 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb514-189">In some cases, it may be necessary toospecify a different impersonation account.</span></span> <span data-ttu-id="bb514-190">SSDT 또는 SSMS에서 가장 계정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb514-190">Impersonation account can be specified in SSDT or SSMS.</span></span>

<span data-ttu-id="bb514-191">온-프레미스 데이터 원본의 경우:</span><span class="sxs-lookup"><span data-stu-id="bb514-191">For on-premises data sources:</span></span>

* <span data-ttu-id="bb514-192">SQL 인증을 사용하는 경우 가장은 서비스 계정이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb514-192">If using SQL authentication, impersonation should be Service Account.</span></span>
* <span data-ttu-id="bb514-193">Windows 인증을 사용하는 경우 Windows 사용자/암호를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bb514-193">If using Windows authentication, set Windows user/password.</span></span> <span data-ttu-id="bb514-194">SQL Server의 경우 특정 가장 계정을 사용한 Windows 인증은 메모리 내 데이터 모델에 대해서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb514-194">For SQL Server, Windows authentication with a specific impersonation account is supported only for in-memory data models.</span></span>

<span data-ttu-id="bb514-195">클라우드 데이터 원본의 경우:</span><span class="sxs-lookup"><span data-stu-id="bb514-195">For cloud data sources:</span></span>

* <span data-ttu-id="bb514-196">SQL 인증을 사용하는 경우 가장은 서비스 계정이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb514-196">If using SQL authentication, impersonation should be Service Account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb514-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bb514-197">Next steps</span></span>
<span data-ttu-id="bb514-198">온-프레미스 데이터 소스를 설정한 경우 수 있는지 tooinstall hello [온-프레미스 게이트웨이](analysis-services-gateway.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bb514-198">If you have on-premises data sources, be sure tooinstall hello [On-premises gateway](analysis-services-gateway.md).</span></span>   
<span data-ttu-id="bb514-199">SSDT 또는 SSMS에서 서버 관리에 대 한 더 toolearn 참조 [서버를 관리할](analysis-services-manage.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bb514-199">toolearn more about managing your server in SSDT or SSMS, see [Manage your server](analysis-services-manage.md).</span></span>

