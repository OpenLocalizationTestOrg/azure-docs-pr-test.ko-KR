---
title: "Azure Data Catalog에서 지원되는 데이터 원본 | Microsoft Docs"
description: "이 문서에서는 현재 지원되는 데이터 원본의 사양을 나열합니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: jstevens
editor: 
tags: 
ms.assetid: fd4345ca-2ed8-4c5e-9c4b-f954be2fc9f9
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: d6867c73bc6ea3c238cceef8a68466d451f3365c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="supported-data-sources-in-azure-data-catalog"></a><span data-ttu-id="d4786-103">Azure Data Catalog에서 지원되는 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="d4786-103">Supported data sources in Azure Data Catalog</span></span>

<span data-ttu-id="d4786-104">사용자는 공용 API를 사용하거나 등록 도구 클릭 한 번으로 Azure Data Catalog 웹 포털에 정보를 직접 입력하여 메타데이터를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4786-104">You can publish metadata by using a public API or a click-once registration tool, or by manually entering information directly to the Azure Data Catalog web portal.</span></span> <span data-ttu-id="d4786-105">다음 테이블은 현재 카탈로그로 지원되는 모든 데이터 원본 및 각각에 대한 게시 기능을 요약합니다.</span><span class="sxs-lookup"><span data-stu-id="d4786-105">The following table summarizes all data sources that are supported by the catalog today, and the publishing capabilities for each.</span></span> <span data-ttu-id="d4786-106">또한 포털의 "열기" 경험에서 시작할 수 있는 각 데이터 원본에 대한 외부 데이터 도구가 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4786-106">Also listed are the external data tools that each data source can launch from our portal "open-in" experience.</span></span> <span data-ttu-id="d4786-107">두 번째 테이블에는 각 데이터 원본 연결 속성의 자세한 기술 사양이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4786-107">The second table contains a more technical specification of each data-source connection property.</span></span>


## <a name="list-of-supported-data-sources"></a><span data-ttu-id="d4786-108">지원되는 데이터 원본 목록</span><span class="sxs-lookup"><span data-stu-id="d4786-108">List of supported data sources</span></span>

<table>
    <tr>
       <td><span data-ttu-id="d4786-109"><b>데이터 원본 개체</b></span><span class="sxs-lookup"><span data-stu-id="d4786-109"><b>Data source object</b></span></span></td>
       <td><span data-ttu-id="d4786-110"><b>API</b></span><span class="sxs-lookup"><span data-stu-id="d4786-110"><b>API</b></span></span></td>
       <td><span data-ttu-id="d4786-111"><b>수동 입력</b></span><span class="sxs-lookup"><span data-stu-id="d4786-111"><b>Manual entry</b></span></span></td>
       <td><span data-ttu-id="d4786-112"><b>등록 도구</b></span><span class="sxs-lookup"><span data-stu-id="d4786-112"><b>Registration tool</b></span></span></td>
       <td><span data-ttu-id="d4786-113"><b>도구에서 열기</b></span><span class="sxs-lookup"><span data-stu-id="d4786-113"><b>Open-in tools</b></span></span></td>
       <td><span data-ttu-id="d4786-114"><b>참고 사항</b></span><span class="sxs-lookup"><span data-stu-id="d4786-114"><b>Notes</b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-115">Azure Data Lake Store 디렉터리</span><span class="sxs-lookup"><span data-stu-id="d4786-115">Azure Data Lake Store directory</span></span></td>
      <td><span data-ttu-id="d4786-116">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-116">✓</span></span></td>
      <td><span data-ttu-id="d4786-117">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-117">✓</span></span></td>
      <td><span data-ttu-id="d4786-118">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-118">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-119">Azure Data Lake Store 파일</span><span class="sxs-lookup"><span data-stu-id="d4786-119">Azure Data Lake Store file</span></span></td>
      <td><span data-ttu-id="d4786-120">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-120">✓</span></span></td>
      <td><span data-ttu-id="d4786-121">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-121">✓</span></span></td>
      <td><span data-ttu-id="d4786-122">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-122">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-123">Azure Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="d4786-123">Azure Blob storage</span></span></td>
      <td><span data-ttu-id="d4786-124">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-124">✓</span></span></td>
      <td><span data-ttu-id="d4786-125">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-125">✓</span></span></td>
      <td><span data-ttu-id="d4786-126">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-126">✓</span></span></td>
      <td><span data-ttu-id="d4786-127"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="d4786-127"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-128">Azure Storage 디렉터리</span><span class="sxs-lookup"><span data-stu-id="d4786-128">Azure Storage directory</span></span></td>
      <td><span data-ttu-id="d4786-129">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-129">✓</span></span></td>
      <td><span data-ttu-id="d4786-130">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-130">✓</span></span></td>
      <td><span data-ttu-id="d4786-131">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-131">✓</span></span></td>
      <td><span data-ttu-id="d4786-132"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="d4786-132"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-133">Azure Storage 테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-133">Azure Storage table</span></span></td>
      <td><span data-ttu-id="d4786-134">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-134">✓</span></span></td>
      <td><span data-ttu-id="d4786-135">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-135">✓</span></span></td>
      <td><span data-ttu-id="d4786-136">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-136">✓</span></span></td>
      <td>
        <font size="2"></font>
      </td>
      <td>
        <font size="2"></font>
      </td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-137">HDFS 디렉터리</span><span class="sxs-lookup"><span data-stu-id="d4786-137">HDFS directory</span></span></td>
      <td><span data-ttu-id="d4786-138">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-138">✓</span></span></td>
      <td><span data-ttu-id="d4786-139">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-139">✓</span></span></td>
      <td><span data-ttu-id="d4786-140">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-140">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-141">HDFS 파일</span><span class="sxs-lookup"><span data-stu-id="d4786-141">HDFS file</span></span></td>
      <td><span data-ttu-id="d4786-142">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-142">✓</span></span></td>
      <td><span data-ttu-id="d4786-143">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-143">✓</span></span></td>
      <td><span data-ttu-id="d4786-144">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-144">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-145">Hive 테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-145">Hive table</span></span></td>
      <td><span data-ttu-id="d4786-146">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-146">✓</span></span></td>
      <td><span data-ttu-id="d4786-147">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-147">✓</span></span></td>
      <td><span data-ttu-id="d4786-148">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-148">✓</span></span></td>
      <td><span data-ttu-id="d4786-149"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="d4786-149"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-150">Hive 보기</span><span class="sxs-lookup"><span data-stu-id="d4786-150">Hive view</span></span></td>
      <td><span data-ttu-id="d4786-151">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-151">✓</span></span></td>
      <td><span data-ttu-id="d4786-152">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-152">✓</span></span></td>
      <td><span data-ttu-id="d4786-153">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-153">✓</span></span></td>
      <td><span data-ttu-id="d4786-154"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="d4786-154"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-155">MySQL 테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-155">MySQL table</span></span></td>
      <td><span data-ttu-id="d4786-156">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-156">✓</span></span></td>
      <td><span data-ttu-id="d4786-157">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-157">✓</span></span></td>
      <td><span data-ttu-id="d4786-158">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-158">✓</span></span></td>
      <td><span data-ttu-id="d4786-159"><font size=2>Excel, 파워 BI</font></span><span class="sxs-lookup"><span data-stu-id="d4786-159"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-160">MySQL 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-160">MySQL view</span></span></td>
      <td><span data-ttu-id="d4786-161">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-161">✓</span></span></td>
      <td><span data-ttu-id="d4786-162">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-162">✓</span></span></td>
      <td><span data-ttu-id="d4786-163">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-163">✓</span></span></td>
      <td><span data-ttu-id="d4786-164"><font size=2>Excel, 파워 BI</font></span><span class="sxs-lookup"><span data-stu-id="d4786-164"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-165">Oracle 데이터베이스 테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-165">Oracle Database table</span></span></td>
      <td><span data-ttu-id="d4786-166">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-166">✓</span></span></td>
      <td><span data-ttu-id="d4786-167">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-167">✓</span></span></td>
      <td><span data-ttu-id="d4786-168">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-168">✓</span></span></td>
      <td><span data-ttu-id="d4786-169"><font size=2>Excel, 파워 BI</font></span><span class="sxs-lookup"><span data-stu-id="d4786-169"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-170">Oracle 데이터베이스 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-170">Oracle Database view</span></span></td>
      <td><span data-ttu-id="d4786-171">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-171">✓</span></span></td>
      <td><span data-ttu-id="d4786-172">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-172">✓</span></span></td>
      <td><span data-ttu-id="d4786-173">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-173">✓</span></span></td>
      <td><span data-ttu-id="d4786-174"><font size=2>Excel, 파워 BI</font></span><span class="sxs-lookup"><span data-stu-id="d4786-174"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-175">기타(일반 자산)</span><span class="sxs-lookup"><span data-stu-id="d4786-175">Other (generic asset)</span></span></td>
      <td><span data-ttu-id="d4786-176">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-176">✓</span></span></td>
      <td><span data-ttu-id="d4786-177">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-177">✓</span></span></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-178">Azure SQL Data Warehouse 테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-178">Azure SQL Data Warehouse table</span></span></td>
      <td><span data-ttu-id="d4786-179">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-179">✓</span></span></td>
      <td><span data-ttu-id="d4786-180">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-180">✓</span></span></td>
      <td><span data-ttu-id="d4786-181">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-181">✓</span></span></td>
      <td><span data-ttu-id="d4786-182"><font size=2>Excel, PowerBI, SQL Server 데이터 도구</font></span><span class="sxs-lookup"><span data-stu-id="d4786-182"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-183">SQL Data Warehouse 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-183">SQL Data Warehouse view</span></span></td>
      <td><span data-ttu-id="d4786-184">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-184">✓</span></span></td>
      <td><span data-ttu-id="d4786-185">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-185">✓</span></span></td>
      <td><span data-ttu-id="d4786-186">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-186">✓</span></span></td>
      <td><span data-ttu-id="d4786-187"><font size=2>Excel, PowerBI, SQL Server 데이터 도구</font></span><span class="sxs-lookup"><span data-stu-id="d4786-187"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-188">SQL Server Analysis Services 차원</span><span class="sxs-lookup"><span data-stu-id="d4786-188">SQL Server Analysis Services dimension</span></span></td>
      <td><span data-ttu-id="d4786-189">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-189">✓</span></span></td>
      <td><span data-ttu-id="d4786-190">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-190">✓</span></span></td>
      <td><span data-ttu-id="d4786-191">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-191">✓</span></span></td>
      <td><span data-ttu-id="d4786-192"><font size=2>Excel, 파워 BI</font></span><span class="sxs-lookup"><span data-stu-id="d4786-192"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-193">SQL Server Analysis Services KPI</span><span class="sxs-lookup"><span data-stu-id="d4786-193">SQL Server Analysis Services KPI</span></span></td>
      <td><span data-ttu-id="d4786-194">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-194">✓</span></span></td>
      <td><span data-ttu-id="d4786-195">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-195">✓</span></span></td>
      <td><span data-ttu-id="d4786-196">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-196">✓</span></span></td>
      <td><span data-ttu-id="d4786-197"><font size=2>Excel, 파워 BI</font></span><span class="sxs-lookup"><span data-stu-id="d4786-197"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-198">SQL Server Analysis Services 측정값</span><span class="sxs-lookup"><span data-stu-id="d4786-198">SQL Server Analysis Services measure</span></span></td>
      <td><span data-ttu-id="d4786-199">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-199">✓</span></span></td>
      <td><span data-ttu-id="d4786-200">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-200">✓</span></span></td>
      <td><span data-ttu-id="d4786-201">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-201">✓</span></span></td>
      <td><span data-ttu-id="d4786-202"><font size=2>Excel, 파워 BI</font></span><span class="sxs-lookup"><span data-stu-id="d4786-202"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-203">SQL Server Analysis Services 테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-203">SQL Server Analysis Services table</span></span></td>
      <td><span data-ttu-id="d4786-204">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-204">✓</span></span></td>
      <td><span data-ttu-id="d4786-205">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-205">✓</span></span></td>
      <td><span data-ttu-id="d4786-206">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-206">✓</span></span></td>
      <td><span data-ttu-id="d4786-207"><font size=2>Excel, 파워 BI</font></span><span class="sxs-lookup"><span data-stu-id="d4786-207"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-208">SQL Server Reporting Services 보고서</span><span class="sxs-lookup"><span data-stu-id="d4786-208">SQL Server Reporting Services report</span></span></td>
      <td><span data-ttu-id="d4786-209">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-209">✓</span></span></td>
      <td><span data-ttu-id="d4786-210">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-210">✓</span></span></td>
      <td><span data-ttu-id="d4786-211">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-211">✓</span></span></td>
      <td><span data-ttu-id="d4786-212"><font size=2>브라우저</font></span><span class="sxs-lookup"><span data-stu-id="d4786-212"><font size=2>Browser</font></span></span></td>
      <td><span data-ttu-id="d4786-213"><font size=2>기본 모드 서버에만 해당. SharePoint 모드는 지원되지 않음.</font></span><span class="sxs-lookup"><span data-stu-id="d4786-213"><font size=2>Native mode servers only. SharePoint mode is not supported.</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-214">SQL Server 테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-214">SQL Server table</span></span></td>
      <td><span data-ttu-id="d4786-215">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-215">✓</span></span></td>
      <td><span data-ttu-id="d4786-216">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-216">✓</span></span></td>
      <td><span data-ttu-id="d4786-217">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-217">✓</span></span></td>
      <td><span data-ttu-id="d4786-218"><font size=2>Excel, PowerBI, SQL Server 데이터 도구</font></span><span class="sxs-lookup"><span data-stu-id="d4786-218"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-219">SQL Server 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-219">SQL Server view</span></span></td>
      <td><span data-ttu-id="d4786-220">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-220">✓</span></span></td>
      <td><span data-ttu-id="d4786-221">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-221">✓</span></span></td>
      <td><span data-ttu-id="d4786-222">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-222">✓</span></span></td>
      <td><span data-ttu-id="d4786-223"><font size=2>Excel, PowerBI, SQL Server 데이터 도구</font></span><span class="sxs-lookup"><span data-stu-id="d4786-223"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-224">Teradata 테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-224">Teradata table</span></span></td>
      <td><span data-ttu-id="d4786-225">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-225">✓</span></span></td>
      <td><span data-ttu-id="d4786-226">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-226">✓</span></span></td>
      <td><span data-ttu-id="d4786-227">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-227">✓</span></span></td>
      <td><span data-ttu-id="d4786-228"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="d4786-228"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-229">Teradata 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-229">Teradata view</span></span></td>
      <td><span data-ttu-id="d4786-230">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-230">✓</span></span></td>
      <td><span data-ttu-id="d4786-231">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-231">✓</span></span></td>
      <td><span data-ttu-id="d4786-232">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-232">✓</span></span></td>
      <td><span data-ttu-id="d4786-233"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="d4786-233"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-234">SAP HANA 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-234">SAP HANA view</span></span></td>
      <td><span data-ttu-id="d4786-235">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-235">✓</span></span></td>
      <td><span data-ttu-id="d4786-236">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-236">✓</span></span></td>
      <td><span data-ttu-id="d4786-237">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-237">✓</span></span></td>
      <td><span data-ttu-id="d4786-238"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="d4786-238"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-239">DB2 테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-239">DB2 table</span></span></td>
      <td><span data-ttu-id="d4786-240">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-240">✓</span></span></td>
      <td><span data-ttu-id="d4786-241">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-241">✓</span></span></td>
      <td><span data-ttu-id="d4786-242">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-242">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-243">DB2 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-243">DB2 view</span></span></td>
      <td><span data-ttu-id="d4786-244">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-244">✓</span></span></td>
      <td><span data-ttu-id="d4786-245">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-245">✓</span></span></td>
      <td><span data-ttu-id="d4786-246">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-246">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-247">파일 시스템 파일</span><span class="sxs-lookup"><span data-stu-id="d4786-247">File system file</span></span></td>
      <td><span data-ttu-id="d4786-248">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-248">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-249">FTP 디렉터리</span><span class="sxs-lookup"><span data-stu-id="d4786-249">FTP directory</span></span></td>
      <td><span data-ttu-id="d4786-250">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-250">✓</span></span></td>
      <td><span data-ttu-id="d4786-251">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-251">✓</span></span></td>
      <td><span data-ttu-id="d4786-252">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-252">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-253">FTP 파일</span><span class="sxs-lookup"><span data-stu-id="d4786-253">FTP file</span></span></td>
      <td><span data-ttu-id="d4786-254">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-254">✓</span></span></td>
      <td><span data-ttu-id="d4786-255">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-255">✓</span></span></td>
      <td><span data-ttu-id="d4786-256">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-256">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-257">HTTP 보고서</span><span class="sxs-lookup"><span data-stu-id="d4786-257">HTTP report</span></span></td>
      <td><span data-ttu-id="d4786-258">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-258">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-259">HTTP 끝점</span><span class="sxs-lookup"><span data-stu-id="d4786-259">HTTP endpoint</span></span></td>
      <td><span data-ttu-id="d4786-260">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-260">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-261">HTTP 파일</span><span class="sxs-lookup"><span data-stu-id="d4786-261">HTTP file</span></span></td>
      <td><span data-ttu-id="d4786-262">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-262">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-263">OData 엔터티 집합</span><span class="sxs-lookup"><span data-stu-id="d4786-263">OData entity set</span></span></td>
      <td><span data-ttu-id="d4786-264">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-264">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-265">OData 함수</span><span class="sxs-lookup"><span data-stu-id="d4786-265">OData function</span></span></td>
      <td><span data-ttu-id="d4786-266">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-266">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-267">PostgreSQL 테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-267">PostgreSQL table</span></span></td>
      <td><span data-ttu-id="d4786-268">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-268">✓</span></span></td>
      <td><span data-ttu-id="d4786-269">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-269">✓</span></span></td>
      <td><span data-ttu-id="d4786-270">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-270">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-271">PostgreSQL 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-271">PostgreSQL view</span></span></td>
      <td><span data-ttu-id="d4786-272">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-272">✓</span></span></td>
      <td><span data-ttu-id="d4786-273">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-273">✓</span></span></td>
      <td><span data-ttu-id="d4786-274">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-274">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-275">SAP HANA 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-275">SAP HANA view</span></span></td>
      <td><span data-ttu-id="d4786-276">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-276">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td> <span data-ttu-id="d4786-277">Salesforce 개체</span><span class="sxs-lookup"><span data-stu-id="d4786-277">Salesforce object</span></span></td>
      <td><span data-ttu-id="d4786-278">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-278">✓</span></span></td>
      <td><span data-ttu-id="d4786-279">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-279">✓</span></span></td>
      <td><span data-ttu-id="d4786-280">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-280">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-281">SharePoint 목록</span><span class="sxs-lookup"><span data-stu-id="d4786-281">SharePoint list</span></span> </td>
      <td><span data-ttu-id="d4786-282">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-282">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-283">Azure Cosmos DB 컬렉션</span><span class="sxs-lookup"><span data-stu-id="d4786-283">Azure Cosmos DB collection</span></span></td>
      <td><span data-ttu-id="d4786-284">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-284">✓</span></span></td>
      <td><span data-ttu-id="d4786-285">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-285">✓</span></span></td>
      <td><span data-ttu-id="d4786-286">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-286">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-287">일반 ODBC 테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-287">Generic ODBC table</span></span></td>
      <td><span data-ttu-id="d4786-288">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-288">✓</span></span></td>
      <td><span data-ttu-id="d4786-289">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-289">✓</span></span></td>
      <td><span data-ttu-id="d4786-290">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-290">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-291">일반 ODBC 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-291">Generic ODBC view</span></span></td>
      <td><span data-ttu-id="d4786-292">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-292">✓</span></span></td>
      <td><span data-ttu-id="d4786-293">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-293">✓</span></span></td>
      <td><span data-ttu-id="d4786-294">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-294">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-295">Cassandra 테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-295">Cassandra table</span></span></td>
      <td><span data-ttu-id="d4786-296">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-296">✓</span></span></td>
      <td><span data-ttu-id="d4786-297">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-297">✓</span></span></td>
      <td><span data-ttu-id="d4786-298">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-298">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="d4786-299"><font size=2>일반 ODBC 자산으로 게시</font></span><span class="sxs-lookup"><span data-stu-id="d4786-299"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-300">Cassandra 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-300">Cassandra view</span></span></td>
      <td><span data-ttu-id="d4786-301">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-301">✓</span></span></td>
      <td><span data-ttu-id="d4786-302">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-302">✓</span></span></td>
      <td><span data-ttu-id="d4786-303">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-303">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="d4786-304"><font size=2>일반 ODBC 자산으로 게시</font></span><span class="sxs-lookup"><span data-stu-id="d4786-304"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-305">Sybase 테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-305">Sybase table</span></span></td>
      <td><span data-ttu-id="d4786-306">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-306">✓</span></span></td>
      <td><span data-ttu-id="d4786-307">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-307">✓</span></span></td>
      <td><span data-ttu-id="d4786-308">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-308">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-309">Sybase 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-309">Sybase view</span></span></td>
      <td><span data-ttu-id="d4786-310">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-310">✓</span></span></td>
      <td><span data-ttu-id="d4786-311">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-311">✓</span></span></td>
      <td><span data-ttu-id="d4786-312">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-312">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-313">MongoDB 테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-313">MongoDB table</span></span></td>
      <td><span data-ttu-id="d4786-314">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-314">✓</span></span></td>
      <td><span data-ttu-id="d4786-315">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-315">✓</span></span></td>
      <td><span data-ttu-id="d4786-316">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-316">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="d4786-317"><font size=2>일반 ODBC 자산으로 게시</font></span><span class="sxs-lookup"><span data-stu-id="d4786-317"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-318">MongoDB 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-318">MongoDB view</span></span></td>
      <td><span data-ttu-id="d4786-319">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-319">✓</span></span></td>
      <td><span data-ttu-id="d4786-320">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-320">✓</span></span></td>
      <td><span data-ttu-id="d4786-321">✓</span><span class="sxs-lookup"><span data-stu-id="d4786-321">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="d4786-322"><font size=2>일반 ODBC 자산으로 게시</font></span><span class="sxs-lookup"><span data-stu-id="d4786-322"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
</table>

<span data-ttu-id="d4786-323">추가적인 원본에 대한 지원이 필요하면, [Azure Data Catalog 포럼](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409)에 기능 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="d4786-323">If you need support for additional sources, submit a feature request to the [Azure Data Catalog forum](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span></span>


## <a name="data-source-reference-specification"></a><span data-ttu-id="d4786-324">데이터 원본 참조 사양</span><span class="sxs-lookup"><span data-stu-id="d4786-324">Data-source reference specification</span></span>
> [!NOTE]
> <span data-ttu-id="d4786-325">다음 테이블의 **DSL 구조** 열에서는 Azure Data Catalog에서 사용되는 "address" 속성 모음에 대한 연결 속성을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="d4786-325">The **DSL structure** column in the following table lists only the connection properties for "address" property bag that are used by Azure Data Catalog.</span></span> <span data-ttu-id="d4786-326">즉, "address" 속성 모음에는 Azure Data Catalog에서 지속하지만 사용하지 않는 데이터 원본의 다른 연결 속성이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4786-326">That is, "address" property bag can contain other connection properties of the data source which Azure Data Catalog persists, but does not use.</span></span>

<table>
    <tr>
       <td><span data-ttu-id="d4786-327"><b>원본 유형</b></span><span class="sxs-lookup"><span data-stu-id="d4786-327"><b>Source type</b></span></span></td>
       <td><span data-ttu-id="d4786-328"><b>자산 형식</b></span><span class="sxs-lookup"><span data-stu-id="d4786-328"><b>Asset type</b></span></span></td>
       <td><span data-ttu-id="d4786-329"><b>개체 유형</b></span><span class="sxs-lookup"><span data-stu-id="d4786-329"><b>Object types</b></span></span></td>
       <td><span data-ttu-id="d4786-330"><b>DSL 구조<b></span><span class="sxs-lookup"><span data-stu-id="d4786-330"><b>DSL structure<b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-331">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d4786-331">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="d4786-332">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-332">Container</span></span></td>
      <td><span data-ttu-id="d4786-333">데이터 레이크</span><span class="sxs-lookup"><span data-stu-id="d4786-333">Data Lake</span></span></td>
      <td><span data-ttu-id="d4786-334">
        <font size=2> 프로토콜: webhdfs</span><span class="sxs-lookup"><span data-stu-id="d4786-334">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="d4786-335">인증: {기본, oauth}</span><span class="sxs-lookup"><span data-stu-id="d4786-335">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="d4786-336">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-336">Address:</span></span> <br><span data-ttu-id="d4786-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-338">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d4786-338">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="d4786-339">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-339">Table</span></span></td>
      <td><span data-ttu-id="d4786-340">디렉터리, 파일</span><span class="sxs-lookup"><span data-stu-id="d4786-340">Directory, file</span></span></td>
      <td><span data-ttu-id="d4786-341">
        <font size=2> 프로토콜: webhdfs</span><span class="sxs-lookup"><span data-stu-id="d4786-341">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="d4786-342">인증: {기본, oauth}</span><span class="sxs-lookup"><span data-stu-id="d4786-342">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="d4786-343">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-343">Address:</span></span> <br><span data-ttu-id="d4786-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-345">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="d4786-345">Azure Storage</span></span></td>
      <td><span data-ttu-id="d4786-346">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-346">Container</span></span></td>
      <td><span data-ttu-id="d4786-347">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-347">Container</span></span></td>
      <td><span data-ttu-id="d4786-348">
        <font size=2> 프로토콜: azure-blobs</span><span class="sxs-lookup"><span data-stu-id="d4786-348">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="d4786-349">인증: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="d4786-349">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="d4786-350">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-350">Address:</span></span> <br><span data-ttu-id="d4786-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 도메인</span><span class="sxs-lookup"><span data-stu-id="d4786-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="d4786-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 계정</span><span class="sxs-lookup"><span data-stu-id="d4786-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="d4786-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 컨테이너 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-354">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="d4786-354">Azure Storage</span></span></td>
      <td><span data-ttu-id="d4786-355">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-355">Table</span></span></td>
      <td><span data-ttu-id="d4786-356">Blob, 디렉터리</span><span class="sxs-lookup"><span data-stu-id="d4786-356">Blob, directory</span></span></td>
      <td><span data-ttu-id="d4786-357">
        <font size=2> 프로토콜: azure-blobs</span><span class="sxs-lookup"><span data-stu-id="d4786-357">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="d4786-358">인증: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="d4786-358">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="d4786-359">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-359">Address:</span></span> <br><span data-ttu-id="d4786-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 도메인</span><span class="sxs-lookup"><span data-stu-id="d4786-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="d4786-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 계정</span><span class="sxs-lookup"><span data-stu-id="d4786-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="d4786-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container</span></span> <br><span data-ttu-id="d4786-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 이름 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-364">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="d4786-364">Azure Storage</span></span></td>
      <td><span data-ttu-id="d4786-365">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-365">Container</span></span></td>
      <td><span data-ttu-id="d4786-366">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-366">Container</span></span></td>
      <td><span data-ttu-id="d4786-367">
        <font size=2> 프로토콜: azure-tables</span><span class="sxs-lookup"><span data-stu-id="d4786-367">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="d4786-368">인증: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="d4786-368">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="d4786-369">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-369">Address:</span></span> <br><span data-ttu-id="d4786-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 도메인</span><span class="sxs-lookup"><span data-stu-id="d4786-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="d4786-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 계정 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-372">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="d4786-372">Azure Storage</span></span></td>
      <td><span data-ttu-id="d4786-373">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-373">Table</span></span></td>
      <td><span data-ttu-id="d4786-374">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-374">Table</span></span></td>
      <td><span data-ttu-id="d4786-375">
        <font size=2> 프로토콜: azure-tables</span><span class="sxs-lookup"><span data-stu-id="d4786-375">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="d4786-376">인증: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="d4786-376">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="d4786-377">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-377">Address:</span></span> <br><span data-ttu-id="d4786-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 도메인</span><span class="sxs-lookup"><span data-stu-id="d4786-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="d4786-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 계정</span><span class="sxs-lookup"><span data-stu-id="d4786-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="d4786-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 이름 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-381">Cosmos</span><span class="sxs-lookup"><span data-stu-id="d4786-381">Cosmos</span></span></td>
      <td><span data-ttu-id="d4786-382">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-382">Container</span></span></td>
      <td><span data-ttu-id="d4786-383">가상 클러스터</span><span class="sxs-lookup"><span data-stu-id="d4786-383">Virtual cluster</span></span></td>
      <td><span data-ttu-id="d4786-384">
        <font size=2> 프로토콜: cosmos</span><span class="sxs-lookup"><span data-stu-id="d4786-384">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="d4786-385">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-385">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="d4786-386">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-386">Address:</span></span> <br><span data-ttu-id="d4786-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-388">Cosmos</span><span class="sxs-lookup"><span data-stu-id="d4786-388">Cosmos</span></span></td>
      <td><span data-ttu-id="d4786-389">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-389">Table</span></span></td>
      <td><span data-ttu-id="d4786-390">스트림, 스트림 집합, 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-390">Stream, stream set, view</span></span></td>
      <td><span data-ttu-id="d4786-391">
        <font size=2> 프로토콜: cosmos</span><span class="sxs-lookup"><span data-stu-id="d4786-391">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="d4786-392">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-392">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="d4786-393">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-393">Address:</span></span> <br><span data-ttu-id="d4786-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-395">Datazen</span><span class="sxs-lookup"><span data-stu-id="d4786-395">Datazen</span></span></td>
      <td><span data-ttu-id="d4786-396">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-396">Container</span></span></td>
      <td><span data-ttu-id="d4786-397">사이트</span><span class="sxs-lookup"><span data-stu-id="d4786-397">Site</span></span></td>
      <td><span data-ttu-id="d4786-398">
        <font size=2> 프로토콜: http</span><span class="sxs-lookup"><span data-stu-id="d4786-398">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="d4786-399">인증: {없음, 기본, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="d4786-399">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="d4786-400">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-400">Address:</span></span> <br><span data-ttu-id="d4786-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-402">Datazen</span><span class="sxs-lookup"><span data-stu-id="d4786-402">Datazen</span></span></td>
      <td><span data-ttu-id="d4786-403">보고서</span><span class="sxs-lookup"><span data-stu-id="d4786-403">Report</span></span></td>
      <td><span data-ttu-id="d4786-404">보고서, 대시보드</span><span class="sxs-lookup"><span data-stu-id="d4786-404">Report, dashboard</span></span></td>
      <td><span data-ttu-id="d4786-405">
        <font size=2> 프로토콜: http</span><span class="sxs-lookup"><span data-stu-id="d4786-405">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="d4786-406">인증: {없음, 기본, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="d4786-406">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="d4786-407">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-407">Address:</span></span> <br><span data-ttu-id="d4786-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-409">DB2</span><span class="sxs-lookup"><span data-stu-id="d4786-409">DB2</span></span></td>
      <td><span data-ttu-id="d4786-410">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-410">Container</span></span></td>
      <td><span data-ttu-id="d4786-411">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-411">Database</span></span></td>
      <td><span data-ttu-id="d4786-412">
        <font size=2> 프로토콜: db2</span><span class="sxs-lookup"><span data-stu-id="d4786-412">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="d4786-413">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-413">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="d4786-414">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-414">Address:</span></span> <br><span data-ttu-id="d4786-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-417">DB2</span><span class="sxs-lookup"><span data-stu-id="d4786-417">DB2</span></span></td>
      <td><span data-ttu-id="d4786-418">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-418">Table</span></span></td>
      <td><span data-ttu-id="d4786-419">테이블, 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-419">Table, view</span></span></td>
      <td><span data-ttu-id="d4786-420">
        <font size=2> 프로토콜: db2</span><span class="sxs-lookup"><span data-stu-id="d4786-420">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="d4786-421">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-421">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="d4786-422">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-422">Address:</span></span> <br><span data-ttu-id="d4786-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체</span><span class="sxs-lookup"><span data-stu-id="d4786-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="d4786-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-427">파일 시스템</span><span class="sxs-lookup"><span data-stu-id="d4786-427">File system</span></span></td>
      <td><span data-ttu-id="d4786-428">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-428">Table</span></span></td>
      <td><span data-ttu-id="d4786-429">파일</span><span class="sxs-lookup"><span data-stu-id="d4786-429">File</span></span></td>
      <td><span data-ttu-id="d4786-430">
        <font size=2> 프로토콜: 파일</span><span class="sxs-lookup"><span data-stu-id="d4786-430">
        <font size=2> Protocol: file</span></span> <br><span data-ttu-id="d4786-431">인증: {없음, 기본, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-431">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="d4786-432">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-432">Address:</span></span> <br><span data-ttu-id="d4786-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 경로 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-434">FTP</span><span class="sxs-lookup"><span data-stu-id="d4786-434">FTP</span></span></td>
      <td><span data-ttu-id="d4786-435">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-435">Table</span></span></td>
      <td><span data-ttu-id="d4786-436">디렉터리, 파일</span><span class="sxs-lookup"><span data-stu-id="d4786-436">Directory, file</span></span></td>
      <td><span data-ttu-id="d4786-437">
        <font size=2> 프로토콜: ftp</span><span class="sxs-lookup"><span data-stu-id="d4786-437">
        <font size=2> Protocol: ftp</span></span> <br><span data-ttu-id="d4786-438">인증: {없음, 기본, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-438">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="d4786-439">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-439">Address:</span></span> <br><span data-ttu-id="d4786-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-441">Hadoop Distributed File System</span><span class="sxs-lookup"><span data-stu-id="d4786-441">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="d4786-442">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-442">Container</span></span></td>
      <td><span data-ttu-id="d4786-443">프로비전</span><span class="sxs-lookup"><span data-stu-id="d4786-443">Cluster</span></span></td>
      <td><span data-ttu-id="d4786-444">
        <font size=2> 프로토콜: webhdfs</span><span class="sxs-lookup"><span data-stu-id="d4786-444">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="d4786-445">인증: {기본, oauth}</span><span class="sxs-lookup"><span data-stu-id="d4786-445">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="d4786-446">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-446">Address:</span></span> <br><span data-ttu-id="d4786-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-448">Hadoop Distributed File System</span><span class="sxs-lookup"><span data-stu-id="d4786-448">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="d4786-449">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-449">Table</span></span></td>
      <td><span data-ttu-id="d4786-450">디렉터리, 파일</span><span class="sxs-lookup"><span data-stu-id="d4786-450">Directory, file</span></span></td>
      <td><span data-ttu-id="d4786-451">
        <font size=2> 프로토콜: webhdfs</span><span class="sxs-lookup"><span data-stu-id="d4786-451">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="d4786-452">인증: {기본, oauth}</span><span class="sxs-lookup"><span data-stu-id="d4786-452">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="d4786-453">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-453">Address:</span></span> <br><span data-ttu-id="d4786-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-455">Hive</span><span class="sxs-lookup"><span data-stu-id="d4786-455">Hive</span></span></td>
      <td><span data-ttu-id="d4786-456">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-456">Container</span></span></td>
      <td><span data-ttu-id="d4786-457">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-457">Database</span></span></td>
      <td><span data-ttu-id="d4786-458">
        <font size=2> 프로토콜: hive</span><span class="sxs-lookup"><span data-stu-id="d4786-458">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="d4786-459">인증: {hdinsight, 기본, 사용자 이름, 없음}</span><span class="sxs-lookup"><span data-stu-id="d4786-459">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="d4786-460">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-460">Address:</span></span> <br><span data-ttu-id="d4786-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-463">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="d4786-463">connectionProperties:</span></span> <br><span data-ttu-id="d4786-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-465">Hive</span><span class="sxs-lookup"><span data-stu-id="d4786-465">Hive</span></span></td>
      <td><span data-ttu-id="d4786-466">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-466">Table</span></span></td>
      <td><span data-ttu-id="d4786-467">테이블, 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-467">Table, view</span></span></td>
      <td><span data-ttu-id="d4786-468">
        <font size=2> 프로토콜: hive</span><span class="sxs-lookup"><span data-stu-id="d4786-468">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="d4786-469">인증: {hdinsight, 기본, 사용자 이름, 없음}</span><span class="sxs-lookup"><span data-stu-id="d4786-469">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="d4786-470">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-470">Address:</span></span> <br><span data-ttu-id="d4786-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체</span><span class="sxs-lookup"><span data-stu-id="d4786-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="d4786-474">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="d4786-474">connectionProperties:</span></span> <br><span data-ttu-id="d4786-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-476">http</span><span class="sxs-lookup"><span data-stu-id="d4786-476">HTTP</span></span></td>
      <td><span data-ttu-id="d4786-477">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-477">Container</span></span></td>
      <td><span data-ttu-id="d4786-478">사이트</span><span class="sxs-lookup"><span data-stu-id="d4786-478">Site</span></span></td>
      <td><span data-ttu-id="d4786-479">
        <font size=2> 프로토콜: http</span><span class="sxs-lookup"><span data-stu-id="d4786-479">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="d4786-480">인증: {없음, 기본, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="d4786-480">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="d4786-481">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-481">Address:</span></span> <br><span data-ttu-id="d4786-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-483">http</span><span class="sxs-lookup"><span data-stu-id="d4786-483">HTTP</span></span></td>
      <td><span data-ttu-id="d4786-484">보고서</span><span class="sxs-lookup"><span data-stu-id="d4786-484">Report</span></span></td>
      <td><span data-ttu-id="d4786-485">보고서, 대시보드</span><span class="sxs-lookup"><span data-stu-id="d4786-485">Report, dashboard</span></span></td>
      <td><span data-ttu-id="d4786-486">
        <font size=2> 프로토콜: http</span><span class="sxs-lookup"><span data-stu-id="d4786-486">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="d4786-487">인증: {없음, 기본, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="d4786-487">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="d4786-488">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-488">Address:</span></span> <br><span data-ttu-id="d4786-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-490">http</span><span class="sxs-lookup"><span data-stu-id="d4786-490">HTTP</span></span></td>
      <td><span data-ttu-id="d4786-491">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-491">Table</span></span></td>
      <td><span data-ttu-id="d4786-492">끝점, 파일</span><span class="sxs-lookup"><span data-stu-id="d4786-492">Endpoint, file</span></span></td>
      <td><span data-ttu-id="d4786-493">
        <font size=2> 프로토콜: http</span><span class="sxs-lookup"><span data-stu-id="d4786-493">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="d4786-494">인증: {없음, 기본, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="d4786-494">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="d4786-495">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-495">Address:</span></span> <br><span data-ttu-id="d4786-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-497">MySQL</span><span class="sxs-lookup"><span data-stu-id="d4786-497">MySQL</span></span></td>
      <td><span data-ttu-id="d4786-498">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-498">Container</span></span></td>
      <td><span data-ttu-id="d4786-499">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-499">Database</span></span></td>
      <td><span data-ttu-id="d4786-500">
        <font size=2> 프로토콜: mysql</span><span class="sxs-lookup"><span data-stu-id="d4786-500">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="d4786-501">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-501">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="d4786-502">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-502">Address:</span></span> <br><span data-ttu-id="d4786-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-505">MySQL</span><span class="sxs-lookup"><span data-stu-id="d4786-505">MySQL</span></span></td>
      <td><span data-ttu-id="d4786-506">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-506">Table</span></span></td>
      <td><span data-ttu-id="d4786-507">테이블, 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-507">Table, view</span></span></td>
      <td><span data-ttu-id="d4786-508">
        <font size=2> 프로토콜: mysql</span><span class="sxs-lookup"><span data-stu-id="d4786-508">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="d4786-509">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-509">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="d4786-510">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-510">Address:</span></span> <br><span data-ttu-id="d4786-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-514">OData</span><span class="sxs-lookup"><span data-stu-id="d4786-514">OData</span></span></td>
      <td><span data-ttu-id="d4786-515">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-515">Container</span></span></td>
      <td><span data-ttu-id="d4786-516">엔터티 컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-516">Entity container</span></span></td>
      <td><span data-ttu-id="d4786-517">
        <font size=2> 프로토콜: odata</span><span class="sxs-lookup"><span data-stu-id="d4786-517">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="d4786-518">인증: {없음, 기본, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-518">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="d4786-519">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-519">Address:</span></span> <br><span data-ttu-id="d4786-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-521">OData</span><span class="sxs-lookup"><span data-stu-id="d4786-521">OData</span></span></td>
      <td><span data-ttu-id="d4786-522">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-522">Table</span></span></td>
      <td><span data-ttu-id="d4786-523">엔터티 집합, 함수</span><span class="sxs-lookup"><span data-stu-id="d4786-523">Entity set, function</span></span></td>
      <td><span data-ttu-id="d4786-524">
        <font size=2> 프로토콜: odata</span><span class="sxs-lookup"><span data-stu-id="d4786-524">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="d4786-525">인증: {없음, 기본, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-525">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="d4786-526">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-526">Address:</span></span> <br><span data-ttu-id="d4786-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="d4786-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="d4786-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 리소스 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; resource </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-529">Oracle 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-529">Oracle Database</span></span></td>
      <td><span data-ttu-id="d4786-530">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-530">Container</span></span></td>
      <td><span data-ttu-id="d4786-531">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-531">Database</span></span></td>
      <td><span data-ttu-id="d4786-532">
        <font size=2> 프로토콜: oracle</span><span class="sxs-lookup"><span data-stu-id="d4786-532">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="d4786-533">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-533">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="d4786-534">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-534">Address:</span></span> <br><span data-ttu-id="d4786-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-537">Oracle 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-537">Oracle Database</span></span></td>
      <td><span data-ttu-id="d4786-538">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-538">Table</span></span></td>
      <td><span data-ttu-id="d4786-539">테이블, 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-539">Table, view</span></span></td>
      <td><span data-ttu-id="d4786-540">
        <font size=2> 프로토콜: oracle</span><span class="sxs-lookup"><span data-stu-id="d4786-540">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="d4786-541">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-541">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="d4786-542">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-542">Address:</span></span> <br><span data-ttu-id="d4786-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마</span><span class="sxs-lookup"><span data-stu-id="d4786-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="d4786-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-547">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="d4786-547">PostgreSQL</span></span></td>
      <td><span data-ttu-id="d4786-548">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-548">Container</span></span></td>
      <td><span data-ttu-id="d4786-549">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-549">Database</span></span></td>
      <td><span data-ttu-id="d4786-550">
        <font size=2> 프로토콜: postgresql</span><span class="sxs-lookup"><span data-stu-id="d4786-550">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="d4786-551">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-551">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="d4786-552">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-552">Address:</span></span> <br><span data-ttu-id="d4786-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-555">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="d4786-555">PostgreSQL</span></span></td>
      <td><span data-ttu-id="d4786-556">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-556">Table</span></span></td>
      <td><span data-ttu-id="d4786-557">테이블, 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-557">Table, view</span></span></td>
      <td><span data-ttu-id="d4786-558">
        <font size=2> 프로토콜: postgresql</span><span class="sxs-lookup"><span data-stu-id="d4786-558">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="d4786-559">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-559">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="d4786-560">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-560">Address:</span></span> <br><span data-ttu-id="d4786-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마</span><span class="sxs-lookup"><span data-stu-id="d4786-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="d4786-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-565">Power BI</span><span class="sxs-lookup"><span data-stu-id="d4786-565">Power BI</span></span></td>
      <td><span data-ttu-id="d4786-566">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-566">Container</span></span></td>
      <td><span data-ttu-id="d4786-567">사이트</span><span class="sxs-lookup"><span data-stu-id="d4786-567">Site</span></span></td>
      <td><span data-ttu-id="d4786-568">
        <font size=2> 프로토콜: http</span><span class="sxs-lookup"><span data-stu-id="d4786-568">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="d4786-569">인증: {없음, 기본, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="d4786-569">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="d4786-570">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-570">Address:</span></span> <br><span data-ttu-id="d4786-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-572">Power BI</span><span class="sxs-lookup"><span data-stu-id="d4786-572">Power BI</span></span></td>
      <td><span data-ttu-id="d4786-573">보고서</span><span class="sxs-lookup"><span data-stu-id="d4786-573">Report</span></span></td>
      <td><span data-ttu-id="d4786-574">보고서, 대시보드</span><span class="sxs-lookup"><span data-stu-id="d4786-574">Report, dashboard</span></span></td>
      <td><span data-ttu-id="d4786-575">
        <font size=2> 프로토콜: http</span><span class="sxs-lookup"><span data-stu-id="d4786-575">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="d4786-576">인증: {없음, 기본, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="d4786-576">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="d4786-577">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-577">Address:</span></span> <br><span data-ttu-id="d4786-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-579">파워 쿼리</span><span class="sxs-lookup"><span data-stu-id="d4786-579">Power Query</span></span></td>
      <td><span data-ttu-id="d4786-580">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-580">Table</span></span></td>
      <td><span data-ttu-id="d4786-581">데이터 매시업</span><span class="sxs-lookup"><span data-stu-id="d4786-581">Data mashup</span></span></td>
      <td><span data-ttu-id="d4786-582">
        <font size=2> 프로토콜: power-query</span><span class="sxs-lookup"><span data-stu-id="d4786-582">
        <font size=2> Protocol: power-query</span></span> <br><span data-ttu-id="d4786-583">인증: {oauth}</span><span class="sxs-lookup"><span data-stu-id="d4786-583">Authentication: {oauth}</span></span> <br><span data-ttu-id="d4786-584">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-584">Address:</span></span> <br><span data-ttu-id="d4786-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-586">Salesforce</span><span class="sxs-lookup"><span data-stu-id="d4786-586">Salesforce</span></span></td>
      <td><span data-ttu-id="d4786-587">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-587">Table</span></span></td>
      <td><span data-ttu-id="d4786-588">Object</span><span class="sxs-lookup"><span data-stu-id="d4786-588">Object</span></span></td>
      <td><span data-ttu-id="d4786-589">
        <font size=2> 프로토콜: salesforce-com</span><span class="sxs-lookup"><span data-stu-id="d4786-589">
        <font size=2> Protocol: salesforce-com</span></span> <br><span data-ttu-id="d4786-590">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-590">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="d4786-591">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-591">Address:</span></span> <br><span data-ttu-id="d4786-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span><span class="sxs-lookup"><span data-stu-id="d4786-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span></span> <br><span data-ttu-id="d4786-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span><span class="sxs-lookup"><span data-stu-id="d4786-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span></span> <br><span data-ttu-id="d4786-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-595">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="d4786-595">SAP HANA</span></span></td>
      <td><span data-ttu-id="d4786-596">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-596">Container</span></span></td>
      <td><span data-ttu-id="d4786-597">서버</span><span class="sxs-lookup"><span data-stu-id="d4786-597">Server</span></span></td>
      <td><span data-ttu-id="d4786-598">
        <font size=2> 프로토콜: sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="d4786-598">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="d4786-599">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-599">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="d4786-600">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-600">Address:</span></span> <br><span data-ttu-id="d4786-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-602">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="d4786-602">SAP HANA</span></span></td>
      <td><span data-ttu-id="d4786-603">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-603">Table</span></span></td>
      <td><span data-ttu-id="d4786-604">보기</span><span class="sxs-lookup"><span data-stu-id="d4786-604">View</span></span></td>
      <td><span data-ttu-id="d4786-605">
        <font size=2> 프로토콜: sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="d4786-605">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="d4786-606">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-606">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="d4786-607">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-607">Address:</span></span> <br><span data-ttu-id="d4786-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마</span><span class="sxs-lookup"><span data-stu-id="d4786-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="d4786-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-611">SharePoint</span><span class="sxs-lookup"><span data-stu-id="d4786-611">SharePoint</span></span></td>
      <td><span data-ttu-id="d4786-612">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-612">Table</span></span></td>
      <td><span data-ttu-id="d4786-613">나열</span><span class="sxs-lookup"><span data-stu-id="d4786-613">List</span></span></td>
      <td><span data-ttu-id="d4786-614">
        <font size=2> 프로토콜: sharepoint-list</span><span class="sxs-lookup"><span data-stu-id="d4786-614">
        <font size=2> Protocol: sharepoint-list</span></span> <br><span data-ttu-id="d4786-615">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-615">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="d4786-616">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-616">Address:</span></span> <br><span data-ttu-id="d4786-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-618">SQL 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="d4786-618">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="d4786-619">명령</span><span class="sxs-lookup"><span data-stu-id="d4786-619">Command</span></span></td>
      <td><span data-ttu-id="d4786-620">저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="d4786-620">Stored procedure</span></span></td>
      <td><span data-ttu-id="d4786-621">
        <font size=2> 프로토콜: tds</span><span class="sxs-lookup"><span data-stu-id="d4786-621">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="d4786-622">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-622">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="d4786-623">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-623">Address:</span></span> <br><span data-ttu-id="d4786-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마</span><span class="sxs-lookup"><span data-stu-id="d4786-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="d4786-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-628">SQL 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="d4786-628">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="d4786-629">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="d4786-629">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="d4786-630">테이블 반환 함수</span><span class="sxs-lookup"><span data-stu-id="d4786-630">Table-valued function</span></span></td>
      <td><span data-ttu-id="d4786-631">
        <font size=2> 프로토콜: tds</span><span class="sxs-lookup"><span data-stu-id="d4786-631">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="d4786-632">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-632">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="d4786-633">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-633">Address:</span></span> <br><span data-ttu-id="d4786-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마</span><span class="sxs-lookup"><span data-stu-id="d4786-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="d4786-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-638">SQL 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="d4786-638">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="d4786-639">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-639">Container</span></span></td>
      <td><span data-ttu-id="d4786-640">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-640">Database</span></span></td>
      <td><span data-ttu-id="d4786-641">
        <font size=2> 프로토콜: tds</span><span class="sxs-lookup"><span data-stu-id="d4786-641">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="d4786-642">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-642">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="d4786-643">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-643">Address:</span></span> <br><span data-ttu-id="d4786-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-646">SQL 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="d4786-646">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="d4786-647">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-647">Table</span></span></td>
      <td><span data-ttu-id="d4786-648">테이블, 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-648">Table, view</span></span></td>
      <td><span data-ttu-id="d4786-649">
        <font size=2> 프로토콜: tds</span><span class="sxs-lookup"><span data-stu-id="d4786-649">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="d4786-650">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-650">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="d4786-651">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-651">Address:</span></span> <br><span data-ttu-id="d4786-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마</span><span class="sxs-lookup"><span data-stu-id="d4786-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="d4786-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-656">SQL Server</span><span class="sxs-lookup"><span data-stu-id="d4786-656">SQL Server</span></span></td>
      <td><span data-ttu-id="d4786-657">명령</span><span class="sxs-lookup"><span data-stu-id="d4786-657">Command</span></span></td>
      <td><span data-ttu-id="d4786-658">저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="d4786-658">Stored procedure</span></span></td>
      <td><span data-ttu-id="d4786-659">
        <font size=2> 프로토콜: tds</span><span class="sxs-lookup"><span data-stu-id="d4786-659">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="d4786-660">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-660">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="d4786-661">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-661">Address:</span></span> <br><span data-ttu-id="d4786-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마</span><span class="sxs-lookup"><span data-stu-id="d4786-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="d4786-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-666">SQL Server</span><span class="sxs-lookup"><span data-stu-id="d4786-666">SQL Server</span></span></td>
      <td><span data-ttu-id="d4786-667">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="d4786-667">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="d4786-668">테이블 반환 함수</span><span class="sxs-lookup"><span data-stu-id="d4786-668">Table-valued function</span></span></td>
      <td><span data-ttu-id="d4786-669">
        <font size=2> 프로토콜: tds</span><span class="sxs-lookup"><span data-stu-id="d4786-669">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="d4786-670">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-670">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="d4786-671">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-671">Address:</span></span> <br><span data-ttu-id="d4786-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마</span><span class="sxs-lookup"><span data-stu-id="d4786-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="d4786-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-676">SQL Server</span><span class="sxs-lookup"><span data-stu-id="d4786-676">SQL Server</span></span></td>
      <td><span data-ttu-id="d4786-677">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-677">Container</span></span></td>
      <td><span data-ttu-id="d4786-678">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-678">Database</span></span></td>
      <td><span data-ttu-id="d4786-679">
        <font size=2> 프로토콜: tds</span><span class="sxs-lookup"><span data-stu-id="d4786-679">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="d4786-680">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-680">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="d4786-681">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-681">Address:</span></span> <br><span data-ttu-id="d4786-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-684">SQL Server</span><span class="sxs-lookup"><span data-stu-id="d4786-684">SQL Server</span></span></td>
      <td><span data-ttu-id="d4786-685">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-685">Table</span></span></td>
      <td><span data-ttu-id="d4786-686">테이블, 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-686">Table, view</span></span></td>
      <td><span data-ttu-id="d4786-687">
        <font size=2> 프로토콜: tds</span><span class="sxs-lookup"><span data-stu-id="d4786-687">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="d4786-688">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-688">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="d4786-689">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-689">Address:</span></span> <br><span data-ttu-id="d4786-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마</span><span class="sxs-lookup"><span data-stu-id="d4786-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="d4786-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-694">SQL Server Analysis Services 다차원</span><span class="sxs-lookup"><span data-stu-id="d4786-694">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="d4786-695">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-695">Container</span></span></td>
      <td><span data-ttu-id="d4786-696">모델</span><span class="sxs-lookup"><span data-stu-id="d4786-696">Model</span></span></td>
      <td><span data-ttu-id="d4786-697">
        <font size=2> 프로토콜: analysis-services</span><span class="sxs-lookup"><span data-stu-id="d4786-697">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="d4786-698">인증: {windows, 기본, 익명, 없음}</span><span class="sxs-lookup"><span data-stu-id="d4786-698">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="d4786-699">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-699">Address:</span></span> <br><span data-ttu-id="d4786-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 모델 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-703">SQL Server Analysis Services 다차원</span><span class="sxs-lookup"><span data-stu-id="d4786-703">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="d4786-704">KPI</span><span class="sxs-lookup"><span data-stu-id="d4786-704">KPI</span></span></td>
      <td><span data-ttu-id="d4786-705">KPI</span><span class="sxs-lookup"><span data-stu-id="d4786-705">KPI</span></span></td>
      <td><span data-ttu-id="d4786-706">
        <font size=2> 프로토콜: analysis-services</span><span class="sxs-lookup"><span data-stu-id="d4786-706">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="d4786-707">인증: {windows, 기본, 익명, 없음}</span><span class="sxs-lookup"><span data-stu-id="d4786-707">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="d4786-708">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-708">Address:</span></span> <br><span data-ttu-id="d4786-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 모델</span><span class="sxs-lookup"><span data-stu-id="d4786-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="d4786-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체</span><span class="sxs-lookup"><span data-stu-id="d4786-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="d4786-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-714">SQL Server Analysis Services 다차원</span><span class="sxs-lookup"><span data-stu-id="d4786-714">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="d4786-715">측정값</span><span class="sxs-lookup"><span data-stu-id="d4786-715">Measure</span></span></td>
      <td><span data-ttu-id="d4786-716">측정값</span><span class="sxs-lookup"><span data-stu-id="d4786-716">Measure</span></span></td>
      <td><span data-ttu-id="d4786-717">
        <font size=2> 프로토콜: analysis-services</span><span class="sxs-lookup"><span data-stu-id="d4786-717">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="d4786-718">인증: {windows, 기본, 익명, 없음}</span><span class="sxs-lookup"><span data-stu-id="d4786-718">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="d4786-719">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-719">Address:</span></span> <br><span data-ttu-id="d4786-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 모델</span><span class="sxs-lookup"><span data-stu-id="d4786-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="d4786-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체</span><span class="sxs-lookup"><span data-stu-id="d4786-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="d4786-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {측정값} </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-725">SQL Server Analysis Services 다차원</span><span class="sxs-lookup"><span data-stu-id="d4786-725">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="d4786-726">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-726">Table</span></span></td>
      <td><span data-ttu-id="d4786-727">차원</span><span class="sxs-lookup"><span data-stu-id="d4786-727">Dimension</span></span></td>
      <td><span data-ttu-id="d4786-728">
        <font size=2> 프로토콜: analysis-services</span><span class="sxs-lookup"><span data-stu-id="d4786-728">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="d4786-729">인증: {windows, 기본, 익명, 없음}</span><span class="sxs-lookup"><span data-stu-id="d4786-729">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="d4786-730">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-730">Address:</span></span> <br><span data-ttu-id="d4786-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 모델</span><span class="sxs-lookup"><span data-stu-id="d4786-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="d4786-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체</span><span class="sxs-lookup"><span data-stu-id="d4786-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="d4786-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {차원} </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-736">SQL Server Analysis Services 테이블 형식</span><span class="sxs-lookup"><span data-stu-id="d4786-736">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="d4786-737">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-737">Container</span></span></td>
      <td><span data-ttu-id="d4786-738">모델</span><span class="sxs-lookup"><span data-stu-id="d4786-738">Model</span></span></td>
      <td><span data-ttu-id="d4786-739">
        <font size=2> 프로토콜: analysis-services</span><span class="sxs-lookup"><span data-stu-id="d4786-739">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="d4786-740">인증: {windows, 기본, 익명, 없음}</span><span class="sxs-lookup"><span data-stu-id="d4786-740">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="d4786-741">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-741">Address:</span></span> <br><span data-ttu-id="d4786-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 모델 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-745">SQL Server Analysis Services 테이블 형식</span><span class="sxs-lookup"><span data-stu-id="d4786-745">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="d4786-746">KPI</span><span class="sxs-lookup"><span data-stu-id="d4786-746">KPI</span></span></td>
      <td><span data-ttu-id="d4786-747">KPI</span><span class="sxs-lookup"><span data-stu-id="d4786-747">KPI</span></span></td>
      <td><span data-ttu-id="d4786-748">
        <font size=2> 프로토콜: analysis-services</span><span class="sxs-lookup"><span data-stu-id="d4786-748">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="d4786-749">인증: {windows, 기본, 익명, 없음}</span><span class="sxs-lookup"><span data-stu-id="d4786-749">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="d4786-750">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-750">Address:</span></span> <br><span data-ttu-id="d4786-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 모델</span><span class="sxs-lookup"><span data-stu-id="d4786-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="d4786-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체</span><span class="sxs-lookup"><span data-stu-id="d4786-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="d4786-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-756">SQL Server Analysis Services 테이블 형식</span><span class="sxs-lookup"><span data-stu-id="d4786-756">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="d4786-757">측정값</span><span class="sxs-lookup"><span data-stu-id="d4786-757">Measure</span></span></td>
      <td><span data-ttu-id="d4786-758">측정값</span><span class="sxs-lookup"><span data-stu-id="d4786-758">Measure</span></span></td>
      <td><span data-ttu-id="d4786-759">
        <font size=2> 프로토콜: analysis-services</span><span class="sxs-lookup"><span data-stu-id="d4786-759">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="d4786-760">인증: {windows, 기본, 익명, 없음}</span><span class="sxs-lookup"><span data-stu-id="d4786-760">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="d4786-761">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-761">Address:</span></span> <br><span data-ttu-id="d4786-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 모델</span><span class="sxs-lookup"><span data-stu-id="d4786-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="d4786-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체</span><span class="sxs-lookup"><span data-stu-id="d4786-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="d4786-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {측정값} </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-767">SQL Server Analysis Services 테이블 형식</span><span class="sxs-lookup"><span data-stu-id="d4786-767">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="d4786-768">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-768">Table</span></span></td>
      <td><span data-ttu-id="d4786-769">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-769">Table</span></span></td>
      <td><span data-ttu-id="d4786-770">
        <font size=2> 프로토콜: analysis-services</span><span class="sxs-lookup"><span data-stu-id="d4786-770">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="d4786-771">인증: {windows, 기본, 익명, 없음}</span><span class="sxs-lookup"><span data-stu-id="d4786-771">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="d4786-772">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-772">Address:</span></span> <br><span data-ttu-id="d4786-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 모델</span><span class="sxs-lookup"><span data-stu-id="d4786-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="d4786-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체</span><span class="sxs-lookup"><span data-stu-id="d4786-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="d4786-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {테이블} </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-778">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="d4786-778">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="d4786-779">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-779">Container</span></span></td>
      <td><span data-ttu-id="d4786-780">서버</span><span class="sxs-lookup"><span data-stu-id="d4786-780">Server</span></span></td>
      <td><span data-ttu-id="d4786-781">
        <font size=2> 프로토콜: reporting-services</span><span class="sxs-lookup"><span data-stu-id="d4786-781">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="d4786-782">인증: {windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-782">Authentication: {windows}</span></span> <br><span data-ttu-id="d4786-783">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-783">Address:</span></span> <br><span data-ttu-id="d4786-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 버전: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-786">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="d4786-786">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="d4786-787">보고서</span><span class="sxs-lookup"><span data-stu-id="d4786-787">Report</span></span></td>
      <td><span data-ttu-id="d4786-788">보고서</span><span class="sxs-lookup"><span data-stu-id="d4786-788">Report</span></span></td>
      <td><span data-ttu-id="d4786-789">
        <font size=2> 프로토콜: reporting-services</span><span class="sxs-lookup"><span data-stu-id="d4786-789">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="d4786-790">인증: {windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-790">Authentication: {windows}</span></span> <br><span data-ttu-id="d4786-791">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-791">Address:</span></span> <br><span data-ttu-id="d4786-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 경로</span><span class="sxs-lookup"><span data-stu-id="d4786-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path</span></span> <br><span data-ttu-id="d4786-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 버전: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-795">Teradata</span><span class="sxs-lookup"><span data-stu-id="d4786-795">Teradata</span></span></td>
      <td><span data-ttu-id="d4786-796">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-796">Container</span></span></td>
      <td><span data-ttu-id="d4786-797">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-797">Database</span></span></td>
      <td><span data-ttu-id="d4786-798">
        <font size=2> 프로토콜: teradata</span><span class="sxs-lookup"><span data-stu-id="d4786-798">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="d4786-799">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-799">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="d4786-800">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-800">Address:</span></span> <br><span data-ttu-id="d4786-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-803">Teradata</span><span class="sxs-lookup"><span data-stu-id="d4786-803">Teradata</span></span></td>
      <td><span data-ttu-id="d4786-804">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-804">Table</span></span></td>
      <td><span data-ttu-id="d4786-805">테이블, 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-805">Table, view</span></span></td>
      <td><span data-ttu-id="d4786-806">
        <font size=2> 프로토콜: teradata</span><span class="sxs-lookup"><span data-stu-id="d4786-806">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="d4786-807">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-807">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="d4786-808">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-808">Address:</span></span> <br><span data-ttu-id="d4786-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-812">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="d4786-812">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="d4786-813">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-813">Container</span></span></td>
      <td><span data-ttu-id="d4786-814">모델</span><span class="sxs-lookup"><span data-stu-id="d4786-814">Model</span></span></td>
      <td><span data-ttu-id="d4786-815">
        <font size="2"> 프로토콜: mssql-mds</span><span class="sxs-lookup"><span data-stu-id="d4786-815">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="d4786-816">인증: {windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-816">Authentication: {windows}</span></span> <br><span data-ttu-id="d4786-817">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-817">Address:</span></span> <br><span data-ttu-id="d4786-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="d4786-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="d4786-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 모델</span><span class="sxs-lookup"><span data-stu-id="d4786-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="d4786-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 버전 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-821">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="d4786-821">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="d4786-822">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-822">Table</span></span></td>
      <td><span data-ttu-id="d4786-823">엔터티</span><span class="sxs-lookup"><span data-stu-id="d4786-823">Entity</span></span></td>
      <td><span data-ttu-id="d4786-824">
        <font size="2"> 프로토콜: mssql-mds</span><span class="sxs-lookup"><span data-stu-id="d4786-824">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="d4786-825">인증: {windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-825">Authentication: {windows}</span></span> <br><span data-ttu-id="d4786-826">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-826">Address:</span></span> <br><span data-ttu-id="d4786-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="d4786-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="d4786-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 모델</span><span class="sxs-lookup"><span data-stu-id="d4786-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="d4786-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 버전</span><span class="sxs-lookup"><span data-stu-id="d4786-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version</span></span> <br><span data-ttu-id="d4786-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 엔터티 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entity </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-831">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d4786-831">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="d4786-832">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-832">Container</span></span></td>
      <td><span data-ttu-id="d4786-833">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-833">Database</span></span></td>
      <td><span data-ttu-id="d4786-834">
        <font size=2> 프로토콜: document-db</span><span class="sxs-lookup"><span data-stu-id="d4786-834">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="d4786-835">인증: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="d4786-835">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="d4786-836">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-836">Address:</span></span> <br><span data-ttu-id="d4786-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="d4786-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="d4786-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-839">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d4786-839">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="d4786-840">컬렉션</span><span class="sxs-lookup"><span data-stu-id="d4786-840">Collection</span></span></td>
      <td><span data-ttu-id="d4786-841">컬렉션</span><span class="sxs-lookup"><span data-stu-id="d4786-841">Collection</span></span></td>
      <td><span data-ttu-id="d4786-842">
        <font size=2> 프로토콜: document-db</span><span class="sxs-lookup"><span data-stu-id="d4786-842">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="d4786-843">인증: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="d4786-843">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="d4786-844">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-844">Address:</span></span> <br><span data-ttu-id="d4786-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="d4786-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="d4786-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 컬렉션 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; collection </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-848">일반 ODBC</span><span class="sxs-lookup"><span data-stu-id="d4786-848">Generic ODBC</span></span></td>
      <td><span data-ttu-id="d4786-849">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-849">Container</span></span></td>
      <td><span data-ttu-id="d4786-850">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-850">Database</span></span></td>
      <td><span data-ttu-id="d4786-851">
        <font size=2> 프로토콜: odbc</span><span class="sxs-lookup"><span data-stu-id="d4786-851">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="d4786-852">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-852">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="d4786-853">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-853">Address:</span></span> <br><span data-ttu-id="d4786-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 옵션</span><span class="sxs-lookup"><span data-stu-id="d4786-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="d4786-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-856">일반 ODBC</span><span class="sxs-lookup"><span data-stu-id="d4786-856">Generic ODBC</span></span></td>
      <td><span data-ttu-id="d4786-857">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-857">Table</span></span></td>
      <td><span data-ttu-id="d4786-858">테이블, 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-858">Table, View</span></span></td>
      <td><span data-ttu-id="d4786-859">
        <font size=2> 프로토콜: odbc</span><span class="sxs-lookup"><span data-stu-id="d4786-859">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="d4786-860">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-860">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="d4786-861">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-861">Address:</span></span> <br><span data-ttu-id="d4786-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 옵션</span><span class="sxs-lookup"><span data-stu-id="d4786-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="d4786-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체</span><span class="sxs-lookup"><span data-stu-id="d4786-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="d4786-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-866">Sybase</span><span class="sxs-lookup"><span data-stu-id="d4786-866">Sybase</span></span></td>
      <td><span data-ttu-id="d4786-867">컨테이너</span><span class="sxs-lookup"><span data-stu-id="d4786-867">Container</span></span></td>
      <td><span data-ttu-id="d4786-868">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-868">Database</span></span></td>
      <td><span data-ttu-id="d4786-869">
        <font size=2> 프로토콜: sybase</span><span class="sxs-lookup"><span data-stu-id="d4786-869">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="d4786-870">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-870">authentication: {basic, windows}</span></span> <br><span data-ttu-id="d4786-871">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-871">address:</span></span> <br><span data-ttu-id="d4786-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-874">Sybase</span><span class="sxs-lookup"><span data-stu-id="d4786-874">Sybase</span></span></td>
      <td><span data-ttu-id="d4786-875">테이블</span><span class="sxs-lookup"><span data-stu-id="d4786-875">Table</span></span></td>
      <td><span data-ttu-id="d4786-876">테이블, 뷰</span><span class="sxs-lookup"><span data-stu-id="d4786-876">Table, View</span></span></td>
      <td><span data-ttu-id="d4786-877">
        <font size=2> 프로토콜: sybase</span><span class="sxs-lookup"><span data-stu-id="d4786-877">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="d4786-878">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="d4786-878">authentication: {basic, windows}</span></span> <br><span data-ttu-id="d4786-879">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-879">address:</span></span> <br><span data-ttu-id="d4786-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="d4786-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="d4786-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d4786-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="d4786-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마</span><span class="sxs-lookup"><span data-stu-id="d4786-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="d4786-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="d4786-884">기타(위에 해당 없음)</span><span class="sxs-lookup"><span data-stu-id="d4786-884">Other (none of the above)</span></span></td>
      <td>\*</td>
      <td>\*</td>
      <td><span data-ttu-id="d4786-885">
        <font size=2> 프로토콜: generic-asset</span><span class="sxs-lookup"><span data-stu-id="d4786-885">
        <font size=2> Protocol: generic-asset</span></span> <br><span data-ttu-id="d4786-886">주소:</span><span class="sxs-lookup"><span data-stu-id="d4786-886">Address:</span></span> <br><span data-ttu-id="d4786-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span><span class="sxs-lookup"><span data-stu-id="d4786-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span></span></td>
    </tr>
</table>
