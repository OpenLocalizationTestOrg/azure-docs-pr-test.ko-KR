---
title: "Azure Data Catalog에서 데이터 원본을 aaaSupported | Microsoft Docs"
description: "이 문서에서는 현재 지원 되는 hello 데이터 원본의 사양을 나열 합니다."
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
ms.openlocfilehash: 4bfcabf31bf9fd781c939a5026abc42a5407df32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="supported-data-sources-in-azure-data-catalog"></a><span data-ttu-id="4ab9e-103">Azure Data Catalog에서 지원되는 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="4ab9e-103">Supported data sources in Azure Data Catalog</span></span>

<span data-ttu-id="4ab9e-104">한 번의 클릭 또는 공용 API를 사용 하 여 메타 데이터를 게시할 수 있습니다-한 번 등록 도구 또는 Azure Data Catalog toohello 웹 포털에 직접 정보를 수동으로 입력 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ab9e-104">You can publish metadata by using a public API or a click-once registration tool, or by manually entering information directly toohello Azure Data Catalog web portal.</span></span> <span data-ttu-id="4ab9e-105">hello 다음 표에 요약 되어 오늘 hello 카탈로그에서 지 원하는 및 게시 기능을 각각에 대 한 hello 하는 모든 데이터 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="4ab9e-105">hello following table summarizes all data sources that are supported by hello catalog today, and hello publishing capabilities for each.</span></span> <span data-ttu-id="4ab9e-106">에 hello 각 데이터 원본 "오픈의" 포털 경험에서 실행할 수 있는 외부 데이터 도구가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ab9e-106">Also listed are hello external data tools that each data source can launch from our portal "open-in" experience.</span></span> <span data-ttu-id="4ab9e-107">hello 두 번째 테이블에는 각 데이터 원본 연결 속성에 대 한 자세한 기술 사양 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ab9e-107">hello second table contains a more technical specification of each data-source connection property.</span></span>


## <a name="list-of-supported-data-sources"></a><span data-ttu-id="4ab9e-108">지원되는 데이터 원본 목록</span><span class="sxs-lookup"><span data-stu-id="4ab9e-108">List of supported data sources</span></span>

<table>
    <tr>
       <td><span data-ttu-id="4ab9e-109"><b>데이터 원본 개체</b></span><span class="sxs-lookup"><span data-stu-id="4ab9e-109"><b>Data source object</b></span></span></td>
       <td><span data-ttu-id="4ab9e-110"><b>API</b></span><span class="sxs-lookup"><span data-stu-id="4ab9e-110"><b>API</b></span></span></td>
       <td><span data-ttu-id="4ab9e-111"><b>수동 입력</b></span><span class="sxs-lookup"><span data-stu-id="4ab9e-111"><b>Manual entry</b></span></span></td>
       <td><span data-ttu-id="4ab9e-112"><b>등록 도구</b></span><span class="sxs-lookup"><span data-stu-id="4ab9e-112"><b>Registration tool</b></span></span></td>
       <td><span data-ttu-id="4ab9e-113"><b>도구에서 열기</b></span><span class="sxs-lookup"><span data-stu-id="4ab9e-113"><b>Open-in tools</b></span></span></td>
       <td><span data-ttu-id="4ab9e-114"><b>참고 사항</b></span><span class="sxs-lookup"><span data-stu-id="4ab9e-114"><b>Notes</b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-115">Azure Data Lake Store 디렉터리</span><span class="sxs-lookup"><span data-stu-id="4ab9e-115">Azure Data Lake Store directory</span></span></td>
      <td><span data-ttu-id="4ab9e-116">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-116">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-117">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-117">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-118">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-118">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-119">Azure Data Lake Store 파일</span><span class="sxs-lookup"><span data-stu-id="4ab9e-119">Azure Data Lake Store file</span></span></td>
      <td><span data-ttu-id="4ab9e-120">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-120">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-121">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-121">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-122">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-122">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-123">Azure Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="4ab9e-123">Azure Blob storage</span></span></td>
      <td><span data-ttu-id="4ab9e-124">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-124">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-125">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-125">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-126">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-126">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-127"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-127"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-128">Azure Storage 디렉터리</span><span class="sxs-lookup"><span data-stu-id="4ab9e-128">Azure Storage directory</span></span></td>
      <td><span data-ttu-id="4ab9e-129">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-129">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-130">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-130">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-131">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-131">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-132"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-132"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-133">Azure Storage 테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-133">Azure Storage table</span></span></td>
      <td><span data-ttu-id="4ab9e-134">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-134">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-135">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-135">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-136">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-136">✓</span></span></td>
      <td>
        <font size="2"></font>
      </td>
      <td>
        <font size="2"></font>
      </td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-137">HDFS 디렉터리</span><span class="sxs-lookup"><span data-stu-id="4ab9e-137">HDFS directory</span></span></td>
      <td><span data-ttu-id="4ab9e-138">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-138">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-139">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-139">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-140">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-140">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-141">HDFS 파일</span><span class="sxs-lookup"><span data-stu-id="4ab9e-141">HDFS file</span></span></td>
      <td><span data-ttu-id="4ab9e-142">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-142">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-143">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-143">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-144">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-144">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-145">Hive 테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-145">Hive table</span></span></td>
      <td><span data-ttu-id="4ab9e-146">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-146">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-147">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-147">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-148">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-148">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-149"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-149"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-150">Hive 보기</span><span class="sxs-lookup"><span data-stu-id="4ab9e-150">Hive view</span></span></td>
      <td><span data-ttu-id="4ab9e-151">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-151">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-152">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-152">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-153">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-153">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-154"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-154"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-155">MySQL 테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-155">MySQL table</span></span></td>
      <td><span data-ttu-id="4ab9e-156">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-156">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-157">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-157">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-158">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-158">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-159"><font size=2>Excel, 파워 BI</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-159"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-160">MySQL 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-160">MySQL view</span></span></td>
      <td><span data-ttu-id="4ab9e-161">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-161">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-162">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-162">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-163">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-163">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-164"><font size=2>Excel, 파워 BI</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-164"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-165">Oracle 데이터베이스 테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-165">Oracle Database table</span></span></td>
      <td><span data-ttu-id="4ab9e-166">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-166">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-167">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-167">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-168">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-168">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-169"><font size=2>Excel, 파워 BI</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-169"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-170">Oracle 데이터베이스 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-170">Oracle Database view</span></span></td>
      <td><span data-ttu-id="4ab9e-171">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-171">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-172">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-172">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-173">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-173">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-174"><font size=2>Excel, 파워 BI</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-174"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-175">기타(일반 자산)</span><span class="sxs-lookup"><span data-stu-id="4ab9e-175">Other (generic asset)</span></span></td>
      <td><span data-ttu-id="4ab9e-176">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-176">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-177">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-177">✓</span></span></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-178">Azure SQL Data Warehouse 테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-178">Azure SQL Data Warehouse table</span></span></td>
      <td><span data-ttu-id="4ab9e-179">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-179">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-180">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-180">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-181">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-181">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-182"><font size=2>Excel, PowerBI, SQL Server 데이터 도구</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-182"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-183">SQL Data Warehouse 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-183">SQL Data Warehouse view</span></span></td>
      <td><span data-ttu-id="4ab9e-184">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-184">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-185">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-185">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-186">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-186">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-187"><font size=2>Excel, PowerBI, SQL Server 데이터 도구</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-187"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-188">SQL Server Analysis Services 차원</span><span class="sxs-lookup"><span data-stu-id="4ab9e-188">SQL Server Analysis Services dimension</span></span></td>
      <td><span data-ttu-id="4ab9e-189">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-189">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-190">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-190">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-191">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-191">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-192"><font size=2>Excel, 파워 BI</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-192"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-193">SQL Server Analysis Services KPI</span><span class="sxs-lookup"><span data-stu-id="4ab9e-193">SQL Server Analysis Services KPI</span></span></td>
      <td><span data-ttu-id="4ab9e-194">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-194">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-195">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-195">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-196">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-196">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-197"><font size=2>Excel, 파워 BI</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-197"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-198">SQL Server Analysis Services 측정값</span><span class="sxs-lookup"><span data-stu-id="4ab9e-198">SQL Server Analysis Services measure</span></span></td>
      <td><span data-ttu-id="4ab9e-199">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-199">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-200">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-200">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-201">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-201">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-202"><font size=2>Excel, 파워 BI</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-202"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-203">SQL Server Analysis Services 테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-203">SQL Server Analysis Services table</span></span></td>
      <td><span data-ttu-id="4ab9e-204">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-204">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-205">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-205">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-206">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-206">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-207"><font size=2>Excel, 파워 BI</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-207"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-208">SQL Server Reporting Services 보고서</span><span class="sxs-lookup"><span data-stu-id="4ab9e-208">SQL Server Reporting Services report</span></span></td>
      <td><span data-ttu-id="4ab9e-209">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-209">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-210">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-210">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-211">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-211">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-212"><font size=2>브라우저</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-212"><font size=2>Browser</font></span></span></td>
      <td><span data-ttu-id="4ab9e-213"><font size=2>기본 모드 서버에만 해당. SharePoint 모드는 지원되지 않음.</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-213"><font size=2>Native mode servers only. SharePoint mode is not supported.</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-214">SQL Server 테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-214">SQL Server table</span></span></td>
      <td><span data-ttu-id="4ab9e-215">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-215">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-216">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-216">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-217">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-217">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-218"><font size=2>Excel, PowerBI, SQL Server 데이터 도구</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-218"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-219">SQL Server 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-219">SQL Server view</span></span></td>
      <td><span data-ttu-id="4ab9e-220">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-220">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-221">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-221">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-222">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-222">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-223"><font size=2>Excel, PowerBI, SQL Server 데이터 도구</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-223"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-224">Teradata 테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-224">Teradata table</span></span></td>
      <td><span data-ttu-id="4ab9e-225">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-225">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-226">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-226">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-227">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-227">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-228"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-228"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-229">Teradata 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-229">Teradata view</span></span></td>
      <td><span data-ttu-id="4ab9e-230">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-230">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-231">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-231">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-232">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-232">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-233"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-233"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-234">SAP HANA 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-234">SAP HANA view</span></span></td>
      <td><span data-ttu-id="4ab9e-235">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-235">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-236">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-236">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-237">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-237">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-238"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-238"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-239">DB2 테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-239">DB2 table</span></span></td>
      <td><span data-ttu-id="4ab9e-240">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-240">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-241">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-241">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-242">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-242">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-243">DB2 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-243">DB2 view</span></span></td>
      <td><span data-ttu-id="4ab9e-244">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-244">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-245">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-245">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-246">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-246">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-247">파일 시스템 파일</span><span class="sxs-lookup"><span data-stu-id="4ab9e-247">File system file</span></span></td>
      <td><span data-ttu-id="4ab9e-248">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-248">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-249">FTP 디렉터리</span><span class="sxs-lookup"><span data-stu-id="4ab9e-249">FTP directory</span></span></td>
      <td><span data-ttu-id="4ab9e-250">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-250">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-251">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-251">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-252">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-252">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-253">FTP 파일</span><span class="sxs-lookup"><span data-stu-id="4ab9e-253">FTP file</span></span></td>
      <td><span data-ttu-id="4ab9e-254">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-254">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-255">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-255">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-256">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-256">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-257">HTTP 보고서</span><span class="sxs-lookup"><span data-stu-id="4ab9e-257">HTTP report</span></span></td>
      <td><span data-ttu-id="4ab9e-258">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-258">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-259">HTTP 끝점</span><span class="sxs-lookup"><span data-stu-id="4ab9e-259">HTTP endpoint</span></span></td>
      <td><span data-ttu-id="4ab9e-260">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-260">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-261">HTTP 파일</span><span class="sxs-lookup"><span data-stu-id="4ab9e-261">HTTP file</span></span></td>
      <td><span data-ttu-id="4ab9e-262">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-262">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-263">OData 엔터티 집합</span><span class="sxs-lookup"><span data-stu-id="4ab9e-263">OData entity set</span></span></td>
      <td><span data-ttu-id="4ab9e-264">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-264">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-265">OData 함수</span><span class="sxs-lookup"><span data-stu-id="4ab9e-265">OData function</span></span></td>
      <td><span data-ttu-id="4ab9e-266">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-266">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-267">PostgreSQL 테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-267">PostgreSQL table</span></span></td>
      <td><span data-ttu-id="4ab9e-268">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-268">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-269">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-269">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-270">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-270">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-271">PostgreSQL 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-271">PostgreSQL view</span></span></td>
      <td><span data-ttu-id="4ab9e-272">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-272">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-273">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-273">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-274">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-274">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-275">SAP HANA 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-275">SAP HANA view</span></span></td>
      <td><span data-ttu-id="4ab9e-276">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-276">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td> <span data-ttu-id="4ab9e-277">Salesforce 개체</span><span class="sxs-lookup"><span data-stu-id="4ab9e-277">Salesforce object</span></span></td>
      <td><span data-ttu-id="4ab9e-278">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-278">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-279">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-279">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-280">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-280">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-281">SharePoint 목록</span><span class="sxs-lookup"><span data-stu-id="4ab9e-281">SharePoint list</span></span> </td>
      <td><span data-ttu-id="4ab9e-282">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-282">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-283">Azure Cosmos DB 컬렉션</span><span class="sxs-lookup"><span data-stu-id="4ab9e-283">Azure Cosmos DB collection</span></span></td>
      <td><span data-ttu-id="4ab9e-284">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-284">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-285">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-285">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-286">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-286">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-287">일반 ODBC 테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-287">Generic ODBC table</span></span></td>
      <td><span data-ttu-id="4ab9e-288">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-288">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-289">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-289">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-290">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-290">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-291">일반 ODBC 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-291">Generic ODBC view</span></span></td>
      <td><span data-ttu-id="4ab9e-292">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-292">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-293">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-293">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-294">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-294">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-295">Cassandra 테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-295">Cassandra table</span></span></td>
      <td><span data-ttu-id="4ab9e-296">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-296">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-297">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-297">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-298">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-298">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="4ab9e-299"><font size=2>일반 ODBC 자산으로 게시</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-299"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-300">Cassandra 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-300">Cassandra view</span></span></td>
      <td><span data-ttu-id="4ab9e-301">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-301">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-302">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-302">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-303">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-303">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="4ab9e-304"><font size=2>일반 ODBC 자산으로 게시</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-304"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-305">Sybase 테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-305">Sybase table</span></span></td>
      <td><span data-ttu-id="4ab9e-306">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-306">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-307">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-307">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-308">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-308">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-309">Sybase 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-309">Sybase view</span></span></td>
      <td><span data-ttu-id="4ab9e-310">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-310">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-311">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-311">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-312">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-312">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-313">MongoDB 테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-313">MongoDB table</span></span></td>
      <td><span data-ttu-id="4ab9e-314">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-314">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-315">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-315">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-316">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-316">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="4ab9e-317"><font size=2>일반 ODBC 자산으로 게시</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-317"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-318">MongoDB 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-318">MongoDB view</span></span></td>
      <td><span data-ttu-id="4ab9e-319">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-319">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-320">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-320">✓</span></span></td>
      <td><span data-ttu-id="4ab9e-321">✓</span><span class="sxs-lookup"><span data-stu-id="4ab9e-321">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="4ab9e-322"><font size=2>일반 ODBC 자산으로 게시</font></span><span class="sxs-lookup"><span data-stu-id="4ab9e-322"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
</table>

<span data-ttu-id="4ab9e-323">추가 리소스에 대 한 지원이 필요한 경우 제출 기능 요청 toohello [Azure Data Catalog 포럼](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="4ab9e-323">If you need support for additional sources, submit a feature request toohello [Azure Data Catalog forum](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span></span>


## <a name="data-source-reference-specification"></a><span data-ttu-id="4ab9e-324">데이터 원본 참조 사양</span><span class="sxs-lookup"><span data-stu-id="4ab9e-324">Data-source reference specification</span></span>
> [!NOTE]
> <span data-ttu-id="4ab9e-325">hello **DSL 구조** 열 다음 표에 hello에 hello 연결 속성만 속성 모음에 "address"에 대 한 Azure 데이터 카탈로그에서 사용 되는 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ab9e-325">hello **DSL structure** column in hello following table lists only hello connection properties for "address" property bag that are used by Azure Data Catalog.</span></span> <span data-ttu-id="4ab9e-326">즉, "address" propertybag Azure Data Catalog는 지속 되지만 사용 하지 않는 hello 데이터 원본의 다른 연결 속성을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ab9e-326">That is, "address" property bag can contain other connection properties of hello data source which Azure Data Catalog persists, but does not use.</span></span>

<table>
    <tr>
       <td><span data-ttu-id="4ab9e-327"><b>원본 유형</b></span><span class="sxs-lookup"><span data-stu-id="4ab9e-327"><b>Source type</b></span></span></td>
       <td><span data-ttu-id="4ab9e-328"><b>자산 형식</b></span><span class="sxs-lookup"><span data-stu-id="4ab9e-328"><b>Asset type</b></span></span></td>
       <td><span data-ttu-id="4ab9e-329"><b>개체 유형</b></span><span class="sxs-lookup"><span data-stu-id="4ab9e-329"><b>Object types</b></span></span></td>
       <td><span data-ttu-id="4ab9e-330"><b>DSL 구조<b></span><span class="sxs-lookup"><span data-stu-id="4ab9e-330"><b>DSL structure<b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-331">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4ab9e-331">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="4ab9e-332">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-332">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-333">데이터 레이크</span><span class="sxs-lookup"><span data-stu-id="4ab9e-333">Data Lake</span></span></td>
      <td><span data-ttu-id="4ab9e-334">
        <font size=2> 프로토콜: webhdfs</span><span class="sxs-lookup"><span data-stu-id="4ab9e-334">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="4ab9e-335">인증: {기본, oauth}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-335">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="4ab9e-336">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-336">Address:</span></span> <br><span data-ttu-id="4ab9e-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-338">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4ab9e-338">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="4ab9e-339">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-339">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-340">디렉터리, 파일</span><span class="sxs-lookup"><span data-stu-id="4ab9e-340">Directory, file</span></span></td>
      <td><span data-ttu-id="4ab9e-341">
        <font size=2> 프로토콜: webhdfs</span><span class="sxs-lookup"><span data-stu-id="4ab9e-341">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="4ab9e-342">인증: {기본, oauth}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-342">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="4ab9e-343">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-343">Address:</span></span> <br><span data-ttu-id="4ab9e-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-345">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="4ab9e-345">Azure Storage</span></span></td>
      <td><span data-ttu-id="4ab9e-346">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-346">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-347">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-347">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-348">
        <font size=2> 프로토콜: azure-blobs</span><span class="sxs-lookup"><span data-stu-id="4ab9e-348">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="4ab9e-349">인증: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-349">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="4ab9e-350">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-350">Address:</span></span> <br><span data-ttu-id="4ab9e-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 도메인</span><span class="sxs-lookup"><span data-stu-id="4ab9e-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="4ab9e-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 계정</span><span class="sxs-lookup"><span data-stu-id="4ab9e-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="4ab9e-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 컨테이너 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-354">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="4ab9e-354">Azure Storage</span></span></td>
      <td><span data-ttu-id="4ab9e-355">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-355">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-356">Blob, 디렉터리</span><span class="sxs-lookup"><span data-stu-id="4ab9e-356">Blob, directory</span></span></td>
      <td><span data-ttu-id="4ab9e-357">
        <font size=2> 프로토콜: azure-blobs</span><span class="sxs-lookup"><span data-stu-id="4ab9e-357">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="4ab9e-358">인증: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-358">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="4ab9e-359">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-359">Address:</span></span> <br><span data-ttu-id="4ab9e-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 도메인</span><span class="sxs-lookup"><span data-stu-id="4ab9e-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="4ab9e-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 계정</span><span class="sxs-lookup"><span data-stu-id="4ab9e-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="4ab9e-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container</span></span> <br><span data-ttu-id="4ab9e-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 이름 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-364">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="4ab9e-364">Azure Storage</span></span></td>
      <td><span data-ttu-id="4ab9e-365">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-365">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-366">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-366">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-367">
        <font size=2> 프로토콜: azure-tables</span><span class="sxs-lookup"><span data-stu-id="4ab9e-367">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="4ab9e-368">인증: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-368">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="4ab9e-369">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-369">Address:</span></span> <br><span data-ttu-id="4ab9e-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 도메인</span><span class="sxs-lookup"><span data-stu-id="4ab9e-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="4ab9e-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 계정 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-372">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="4ab9e-372">Azure Storage</span></span></td>
      <td><span data-ttu-id="4ab9e-373">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-373">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-374">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-374">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-375">
        <font size=2> 프로토콜: azure-tables</span><span class="sxs-lookup"><span data-stu-id="4ab9e-375">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="4ab9e-376">인증: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-376">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="4ab9e-377">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-377">Address:</span></span> <br><span data-ttu-id="4ab9e-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 도메인</span><span class="sxs-lookup"><span data-stu-id="4ab9e-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="4ab9e-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 계정</span><span class="sxs-lookup"><span data-stu-id="4ab9e-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="4ab9e-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 이름 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-381">Cosmos</span><span class="sxs-lookup"><span data-stu-id="4ab9e-381">Cosmos</span></span></td>
      <td><span data-ttu-id="4ab9e-382">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-382">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-383">가상 클러스터</span><span class="sxs-lookup"><span data-stu-id="4ab9e-383">Virtual cluster</span></span></td>
      <td><span data-ttu-id="4ab9e-384">
        <font size=2> 프로토콜: cosmos</span><span class="sxs-lookup"><span data-stu-id="4ab9e-384">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="4ab9e-385">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-385">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="4ab9e-386">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-386">Address:</span></span> <br><span data-ttu-id="4ab9e-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-388">Cosmos</span><span class="sxs-lookup"><span data-stu-id="4ab9e-388">Cosmos</span></span></td>
      <td><span data-ttu-id="4ab9e-389">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-389">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-390">스트림, 스트림 집합, 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-390">Stream, stream set, view</span></span></td>
      <td><span data-ttu-id="4ab9e-391">
        <font size=2> 프로토콜: cosmos</span><span class="sxs-lookup"><span data-stu-id="4ab9e-391">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="4ab9e-392">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-392">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="4ab9e-393">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-393">Address:</span></span> <br><span data-ttu-id="4ab9e-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-395">Datazen</span><span class="sxs-lookup"><span data-stu-id="4ab9e-395">Datazen</span></span></td>
      <td><span data-ttu-id="4ab9e-396">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-396">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-397">사이트</span><span class="sxs-lookup"><span data-stu-id="4ab9e-397">Site</span></span></td>
      <td><span data-ttu-id="4ab9e-398">
        <font size=2> 프로토콜: http</span><span class="sxs-lookup"><span data-stu-id="4ab9e-398">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="4ab9e-399">인증: {없음, 기본, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-399">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="4ab9e-400">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-400">Address:</span></span> <br><span data-ttu-id="4ab9e-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-402">Datazen</span><span class="sxs-lookup"><span data-stu-id="4ab9e-402">Datazen</span></span></td>
      <td><span data-ttu-id="4ab9e-403">보고서</span><span class="sxs-lookup"><span data-stu-id="4ab9e-403">Report</span></span></td>
      <td><span data-ttu-id="4ab9e-404">보고서, 대시보드</span><span class="sxs-lookup"><span data-stu-id="4ab9e-404">Report, dashboard</span></span></td>
      <td><span data-ttu-id="4ab9e-405">
        <font size=2> 프로토콜: http</span><span class="sxs-lookup"><span data-stu-id="4ab9e-405">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="4ab9e-406">인증: {없음, 기본, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-406">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="4ab9e-407">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-407">Address:</span></span> <br><span data-ttu-id="4ab9e-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-409">DB2</span><span class="sxs-lookup"><span data-stu-id="4ab9e-409">DB2</span></span></td>
      <td><span data-ttu-id="4ab9e-410">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-410">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-411">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-411">Database</span></span></td>
      <td><span data-ttu-id="4ab9e-412">
        <font size=2> 프로토콜: db2</span><span class="sxs-lookup"><span data-stu-id="4ab9e-412">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="4ab9e-413">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-413">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="4ab9e-414">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-414">Address:</span></span> <br><span data-ttu-id="4ab9e-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-417">DB2</span><span class="sxs-lookup"><span data-stu-id="4ab9e-417">DB2</span></span></td>
      <td><span data-ttu-id="4ab9e-418">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-418">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-419">테이블, 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-419">Table, view</span></span></td>
      <td><span data-ttu-id="4ab9e-420">
        <font size=2> 프로토콜: db2</span><span class="sxs-lookup"><span data-stu-id="4ab9e-420">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="4ab9e-421">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-421">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="4ab9e-422">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-422">Address:</span></span> <br><span data-ttu-id="4ab9e-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체</span><span class="sxs-lookup"><span data-stu-id="4ab9e-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="4ab9e-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-427">파일 시스템</span><span class="sxs-lookup"><span data-stu-id="4ab9e-427">File system</span></span></td>
      <td><span data-ttu-id="4ab9e-428">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-428">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-429">파일</span><span class="sxs-lookup"><span data-stu-id="4ab9e-429">File</span></span></td>
      <td><span data-ttu-id="4ab9e-430">
        <font size=2> 프로토콜: 파일</span><span class="sxs-lookup"><span data-stu-id="4ab9e-430">
        <font size=2> Protocol: file</span></span> <br><span data-ttu-id="4ab9e-431">인증: {없음, 기본, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-431">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="4ab9e-432">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-432">Address:</span></span> <br><span data-ttu-id="4ab9e-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 경로 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-434">FTP</span><span class="sxs-lookup"><span data-stu-id="4ab9e-434">FTP</span></span></td>
      <td><span data-ttu-id="4ab9e-435">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-435">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-436">디렉터리, 파일</span><span class="sxs-lookup"><span data-stu-id="4ab9e-436">Directory, file</span></span></td>
      <td><span data-ttu-id="4ab9e-437">
        <font size=2> 프로토콜: ftp</span><span class="sxs-lookup"><span data-stu-id="4ab9e-437">
        <font size=2> Protocol: ftp</span></span> <br><span data-ttu-id="4ab9e-438">인증: {없음, 기본, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-438">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="4ab9e-439">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-439">Address:</span></span> <br><span data-ttu-id="4ab9e-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-441">Hadoop Distributed File System</span><span class="sxs-lookup"><span data-stu-id="4ab9e-441">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="4ab9e-442">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-442">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-443">프로비전</span><span class="sxs-lookup"><span data-stu-id="4ab9e-443">Cluster</span></span></td>
      <td><span data-ttu-id="4ab9e-444">
        <font size=2> 프로토콜: webhdfs</span><span class="sxs-lookup"><span data-stu-id="4ab9e-444">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="4ab9e-445">인증: {기본, oauth}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-445">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="4ab9e-446">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-446">Address:</span></span> <br><span data-ttu-id="4ab9e-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-448">Hadoop Distributed File System</span><span class="sxs-lookup"><span data-stu-id="4ab9e-448">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="4ab9e-449">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-449">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-450">디렉터리, 파일</span><span class="sxs-lookup"><span data-stu-id="4ab9e-450">Directory, file</span></span></td>
      <td><span data-ttu-id="4ab9e-451">
        <font size=2> 프로토콜: webhdfs</span><span class="sxs-lookup"><span data-stu-id="4ab9e-451">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="4ab9e-452">인증: {기본, oauth}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-452">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="4ab9e-453">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-453">Address:</span></span> <br><span data-ttu-id="4ab9e-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-455">Hive</span><span class="sxs-lookup"><span data-stu-id="4ab9e-455">Hive</span></span></td>
      <td><span data-ttu-id="4ab9e-456">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-456">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-457">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-457">Database</span></span></td>
      <td><span data-ttu-id="4ab9e-458">
        <font size=2> 프로토콜: hive</span><span class="sxs-lookup"><span data-stu-id="4ab9e-458">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="4ab9e-459">인증: {hdinsight, 기본, 사용자 이름, 없음}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-459">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="4ab9e-460">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-460">Address:</span></span> <br><span data-ttu-id="4ab9e-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-463">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-463">connectionProperties:</span></span> <br><span data-ttu-id="4ab9e-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-465">Hive</span><span class="sxs-lookup"><span data-stu-id="4ab9e-465">Hive</span></span></td>
      <td><span data-ttu-id="4ab9e-466">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-466">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-467">테이블, 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-467">Table, view</span></span></td>
      <td><span data-ttu-id="4ab9e-468">
        <font size=2> 프로토콜: hive</span><span class="sxs-lookup"><span data-stu-id="4ab9e-468">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="4ab9e-469">인증: {hdinsight, 기본, 사용자 이름, 없음}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-469">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="4ab9e-470">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-470">Address:</span></span> <br><span data-ttu-id="4ab9e-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체</span><span class="sxs-lookup"><span data-stu-id="4ab9e-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="4ab9e-474">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-474">connectionProperties:</span></span> <br><span data-ttu-id="4ab9e-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-476">http</span><span class="sxs-lookup"><span data-stu-id="4ab9e-476">HTTP</span></span></td>
      <td><span data-ttu-id="4ab9e-477">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-477">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-478">사이트</span><span class="sxs-lookup"><span data-stu-id="4ab9e-478">Site</span></span></td>
      <td><span data-ttu-id="4ab9e-479">
        <font size=2> 프로토콜: http</span><span class="sxs-lookup"><span data-stu-id="4ab9e-479">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="4ab9e-480">인증: {없음, 기본, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-480">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="4ab9e-481">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-481">Address:</span></span> <br><span data-ttu-id="4ab9e-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-483">http</span><span class="sxs-lookup"><span data-stu-id="4ab9e-483">HTTP</span></span></td>
      <td><span data-ttu-id="4ab9e-484">보고서</span><span class="sxs-lookup"><span data-stu-id="4ab9e-484">Report</span></span></td>
      <td><span data-ttu-id="4ab9e-485">보고서, 대시보드</span><span class="sxs-lookup"><span data-stu-id="4ab9e-485">Report, dashboard</span></span></td>
      <td><span data-ttu-id="4ab9e-486">
        <font size=2> 프로토콜: http</span><span class="sxs-lookup"><span data-stu-id="4ab9e-486">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="4ab9e-487">인증: {없음, 기본, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-487">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="4ab9e-488">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-488">Address:</span></span> <br><span data-ttu-id="4ab9e-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-490">http</span><span class="sxs-lookup"><span data-stu-id="4ab9e-490">HTTP</span></span></td>
      <td><span data-ttu-id="4ab9e-491">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-491">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-492">끝점, 파일</span><span class="sxs-lookup"><span data-stu-id="4ab9e-492">Endpoint, file</span></span></td>
      <td><span data-ttu-id="4ab9e-493">
        <font size=2> 프로토콜: http</span><span class="sxs-lookup"><span data-stu-id="4ab9e-493">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="4ab9e-494">인증: {없음, 기본, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-494">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="4ab9e-495">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-495">Address:</span></span> <br><span data-ttu-id="4ab9e-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-497">MySQL</span><span class="sxs-lookup"><span data-stu-id="4ab9e-497">MySQL</span></span></td>
      <td><span data-ttu-id="4ab9e-498">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-498">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-499">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-499">Database</span></span></td>
      <td><span data-ttu-id="4ab9e-500">
        <font size=2> 프로토콜: mysql</span><span class="sxs-lookup"><span data-stu-id="4ab9e-500">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="4ab9e-501">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-501">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="4ab9e-502">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-502">Address:</span></span> <br><span data-ttu-id="4ab9e-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-505">MySQL</span><span class="sxs-lookup"><span data-stu-id="4ab9e-505">MySQL</span></span></td>
      <td><span data-ttu-id="4ab9e-506">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-506">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-507">테이블, 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-507">Table, view</span></span></td>
      <td><span data-ttu-id="4ab9e-508">
        <font size=2> 프로토콜: mysql</span><span class="sxs-lookup"><span data-stu-id="4ab9e-508">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="4ab9e-509">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-509">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="4ab9e-510">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-510">Address:</span></span> <br><span data-ttu-id="4ab9e-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-514">OData</span><span class="sxs-lookup"><span data-stu-id="4ab9e-514">OData</span></span></td>
      <td><span data-ttu-id="4ab9e-515">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-515">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-516">엔터티 컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-516">Entity container</span></span></td>
      <td><span data-ttu-id="4ab9e-517">
        <font size=2> 프로토콜: odata</span><span class="sxs-lookup"><span data-stu-id="4ab9e-517">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="4ab9e-518">인증: {없음, 기본, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-518">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="4ab9e-519">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-519">Address:</span></span> <br><span data-ttu-id="4ab9e-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-521">OData</span><span class="sxs-lookup"><span data-stu-id="4ab9e-521">OData</span></span></td>
      <td><span data-ttu-id="4ab9e-522">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-522">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-523">엔터티 집합, 함수</span><span class="sxs-lookup"><span data-stu-id="4ab9e-523">Entity set, function</span></span></td>
      <td><span data-ttu-id="4ab9e-524">
        <font size=2> 프로토콜: odata</span><span class="sxs-lookup"><span data-stu-id="4ab9e-524">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="4ab9e-525">인증: {없음, 기본, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-525">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="4ab9e-526">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-526">Address:</span></span> <br><span data-ttu-id="4ab9e-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="4ab9e-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="4ab9e-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 리소스 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; resource </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-529">Oracle 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-529">Oracle Database</span></span></td>
      <td><span data-ttu-id="4ab9e-530">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-530">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-531">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-531">Database</span></span></td>
      <td><span data-ttu-id="4ab9e-532">
        <font size=2> 프로토콜: oracle</span><span class="sxs-lookup"><span data-stu-id="4ab9e-532">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="4ab9e-533">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-533">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="4ab9e-534">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-534">Address:</span></span> <br><span data-ttu-id="4ab9e-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-537">Oracle 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-537">Oracle Database</span></span></td>
      <td><span data-ttu-id="4ab9e-538">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-538">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-539">테이블, 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-539">Table, view</span></span></td>
      <td><span data-ttu-id="4ab9e-540">
        <font size=2> 프로토콜: oracle</span><span class="sxs-lookup"><span data-stu-id="4ab9e-540">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="4ab9e-541">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-541">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="4ab9e-542">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-542">Address:</span></span> <br><span data-ttu-id="4ab9e-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마</span><span class="sxs-lookup"><span data-stu-id="4ab9e-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="4ab9e-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-547">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="4ab9e-547">PostgreSQL</span></span></td>
      <td><span data-ttu-id="4ab9e-548">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-548">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-549">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-549">Database</span></span></td>
      <td><span data-ttu-id="4ab9e-550">
        <font size=2> 프로토콜: postgresql</span><span class="sxs-lookup"><span data-stu-id="4ab9e-550">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="4ab9e-551">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-551">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="4ab9e-552">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-552">Address:</span></span> <br><span data-ttu-id="4ab9e-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-555">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="4ab9e-555">PostgreSQL</span></span></td>
      <td><span data-ttu-id="4ab9e-556">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-556">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-557">테이블, 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-557">Table, view</span></span></td>
      <td><span data-ttu-id="4ab9e-558">
        <font size=2> 프로토콜: postgresql</span><span class="sxs-lookup"><span data-stu-id="4ab9e-558">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="4ab9e-559">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-559">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="4ab9e-560">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-560">Address:</span></span> <br><span data-ttu-id="4ab9e-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마</span><span class="sxs-lookup"><span data-stu-id="4ab9e-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="4ab9e-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-565">Power BI</span><span class="sxs-lookup"><span data-stu-id="4ab9e-565">Power BI</span></span></td>
      <td><span data-ttu-id="4ab9e-566">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-566">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-567">사이트</span><span class="sxs-lookup"><span data-stu-id="4ab9e-567">Site</span></span></td>
      <td><span data-ttu-id="4ab9e-568">
        <font size=2> 프로토콜: http</span><span class="sxs-lookup"><span data-stu-id="4ab9e-568">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="4ab9e-569">인증: {없음, 기본, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-569">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="4ab9e-570">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-570">Address:</span></span> <br><span data-ttu-id="4ab9e-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-572">Power BI</span><span class="sxs-lookup"><span data-stu-id="4ab9e-572">Power BI</span></span></td>
      <td><span data-ttu-id="4ab9e-573">보고서</span><span class="sxs-lookup"><span data-stu-id="4ab9e-573">Report</span></span></td>
      <td><span data-ttu-id="4ab9e-574">보고서, 대시보드</span><span class="sxs-lookup"><span data-stu-id="4ab9e-574">Report, dashboard</span></span></td>
      <td><span data-ttu-id="4ab9e-575">
        <font size=2> 프로토콜: http</span><span class="sxs-lookup"><span data-stu-id="4ab9e-575">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="4ab9e-576">인증: {없음, 기본, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-576">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="4ab9e-577">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-577">Address:</span></span> <br><span data-ttu-id="4ab9e-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-579">파워 쿼리</span><span class="sxs-lookup"><span data-stu-id="4ab9e-579">Power Query</span></span></td>
      <td><span data-ttu-id="4ab9e-580">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-580">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-581">데이터 매시업</span><span class="sxs-lookup"><span data-stu-id="4ab9e-581">Data mashup</span></span></td>
      <td><span data-ttu-id="4ab9e-582">
        <font size=2> 프로토콜: power-query</span><span class="sxs-lookup"><span data-stu-id="4ab9e-582">
        <font size=2> Protocol: power-query</span></span> <br><span data-ttu-id="4ab9e-583">인증: {oauth}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-583">Authentication: {oauth}</span></span> <br><span data-ttu-id="4ab9e-584">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-584">Address:</span></span> <br><span data-ttu-id="4ab9e-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-586">Salesforce</span><span class="sxs-lookup"><span data-stu-id="4ab9e-586">Salesforce</span></span></td>
      <td><span data-ttu-id="4ab9e-587">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-587">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-588">Object</span><span class="sxs-lookup"><span data-stu-id="4ab9e-588">Object</span></span></td>
      <td><span data-ttu-id="4ab9e-589">
        <font size=2> 프로토콜: salesforce-com</span><span class="sxs-lookup"><span data-stu-id="4ab9e-589">
        <font size=2> Protocol: salesforce-com</span></span> <br><span data-ttu-id="4ab9e-590">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-590">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="4ab9e-591">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-591">Address:</span></span> <br><span data-ttu-id="4ab9e-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span><span class="sxs-lookup"><span data-stu-id="4ab9e-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span></span> <br><span data-ttu-id="4ab9e-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span><span class="sxs-lookup"><span data-stu-id="4ab9e-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span></span> <br><span data-ttu-id="4ab9e-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-595">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="4ab9e-595">SAP HANA</span></span></td>
      <td><span data-ttu-id="4ab9e-596">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-596">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-597">서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-597">Server</span></span></td>
      <td><span data-ttu-id="4ab9e-598">
        <font size=2> 프로토콜: sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="4ab9e-598">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="4ab9e-599">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-599">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="4ab9e-600">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-600">Address:</span></span> <br><span data-ttu-id="4ab9e-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-602">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="4ab9e-602">SAP HANA</span></span></td>
      <td><span data-ttu-id="4ab9e-603">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-603">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-604">보기</span><span class="sxs-lookup"><span data-stu-id="4ab9e-604">View</span></span></td>
      <td><span data-ttu-id="4ab9e-605">
        <font size=2> 프로토콜: sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="4ab9e-605">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="4ab9e-606">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-606">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="4ab9e-607">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-607">Address:</span></span> <br><span data-ttu-id="4ab9e-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마</span><span class="sxs-lookup"><span data-stu-id="4ab9e-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="4ab9e-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-611">SharePoint</span><span class="sxs-lookup"><span data-stu-id="4ab9e-611">SharePoint</span></span></td>
      <td><span data-ttu-id="4ab9e-612">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-612">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-613">나열</span><span class="sxs-lookup"><span data-stu-id="4ab9e-613">List</span></span></td>
      <td><span data-ttu-id="4ab9e-614">
        <font size=2> 프로토콜: sharepoint-list</span><span class="sxs-lookup"><span data-stu-id="4ab9e-614">
        <font size=2> Protocol: sharepoint-list</span></span> <br><span data-ttu-id="4ab9e-615">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-615">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="4ab9e-616">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-616">Address:</span></span> <br><span data-ttu-id="4ab9e-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-618">SQL 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-618">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="4ab9e-619">명령</span><span class="sxs-lookup"><span data-stu-id="4ab9e-619">Command</span></span></td>
      <td><span data-ttu-id="4ab9e-620">저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="4ab9e-620">Stored procedure</span></span></td>
      <td><span data-ttu-id="4ab9e-621">
        <font size=2> 프로토콜: tds</span><span class="sxs-lookup"><span data-stu-id="4ab9e-621">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="4ab9e-622">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-622">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="4ab9e-623">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-623">Address:</span></span> <br><span data-ttu-id="4ab9e-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마</span><span class="sxs-lookup"><span data-stu-id="4ab9e-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="4ab9e-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-628">SQL 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-628">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="4ab9e-629">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="4ab9e-629">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="4ab9e-630">테이블 반환 함수</span><span class="sxs-lookup"><span data-stu-id="4ab9e-630">Table-valued function</span></span></td>
      <td><span data-ttu-id="4ab9e-631">
        <font size=2> 프로토콜: tds</span><span class="sxs-lookup"><span data-stu-id="4ab9e-631">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="4ab9e-632">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-632">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="4ab9e-633">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-633">Address:</span></span> <br><span data-ttu-id="4ab9e-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마</span><span class="sxs-lookup"><span data-stu-id="4ab9e-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="4ab9e-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-638">SQL 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-638">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="4ab9e-639">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-639">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-640">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-640">Database</span></span></td>
      <td><span data-ttu-id="4ab9e-641">
        <font size=2> 프로토콜: tds</span><span class="sxs-lookup"><span data-stu-id="4ab9e-641">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="4ab9e-642">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-642">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="4ab9e-643">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-643">Address:</span></span> <br><span data-ttu-id="4ab9e-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-646">SQL 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-646">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="4ab9e-647">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-647">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-648">테이블, 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-648">Table, view</span></span></td>
      <td><span data-ttu-id="4ab9e-649">
        <font size=2> 프로토콜: tds</span><span class="sxs-lookup"><span data-stu-id="4ab9e-649">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="4ab9e-650">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-650">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="4ab9e-651">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-651">Address:</span></span> <br><span data-ttu-id="4ab9e-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마</span><span class="sxs-lookup"><span data-stu-id="4ab9e-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="4ab9e-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-656">SQL Server</span><span class="sxs-lookup"><span data-stu-id="4ab9e-656">SQL Server</span></span></td>
      <td><span data-ttu-id="4ab9e-657">명령</span><span class="sxs-lookup"><span data-stu-id="4ab9e-657">Command</span></span></td>
      <td><span data-ttu-id="4ab9e-658">저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="4ab9e-658">Stored procedure</span></span></td>
      <td><span data-ttu-id="4ab9e-659">
        <font size=2> 프로토콜: tds</span><span class="sxs-lookup"><span data-stu-id="4ab9e-659">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="4ab9e-660">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-660">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="4ab9e-661">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-661">Address:</span></span> <br><span data-ttu-id="4ab9e-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마</span><span class="sxs-lookup"><span data-stu-id="4ab9e-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="4ab9e-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-666">SQL Server</span><span class="sxs-lookup"><span data-stu-id="4ab9e-666">SQL Server</span></span></td>
      <td><span data-ttu-id="4ab9e-667">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="4ab9e-667">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="4ab9e-668">테이블 반환 함수</span><span class="sxs-lookup"><span data-stu-id="4ab9e-668">Table-valued function</span></span></td>
      <td><span data-ttu-id="4ab9e-669">
        <font size=2> 프로토콜: tds</span><span class="sxs-lookup"><span data-stu-id="4ab9e-669">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="4ab9e-670">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-670">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="4ab9e-671">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-671">Address:</span></span> <br><span data-ttu-id="4ab9e-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마</span><span class="sxs-lookup"><span data-stu-id="4ab9e-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="4ab9e-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-676">SQL Server</span><span class="sxs-lookup"><span data-stu-id="4ab9e-676">SQL Server</span></span></td>
      <td><span data-ttu-id="4ab9e-677">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-677">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-678">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-678">Database</span></span></td>
      <td><span data-ttu-id="4ab9e-679">
        <font size=2> 프로토콜: tds</span><span class="sxs-lookup"><span data-stu-id="4ab9e-679">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="4ab9e-680">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-680">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="4ab9e-681">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-681">Address:</span></span> <br><span data-ttu-id="4ab9e-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-684">SQL Server</span><span class="sxs-lookup"><span data-stu-id="4ab9e-684">SQL Server</span></span></td>
      <td><span data-ttu-id="4ab9e-685">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-685">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-686">테이블, 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-686">Table, view</span></span></td>
      <td><span data-ttu-id="4ab9e-687">
        <font size=2> 프로토콜: tds</span><span class="sxs-lookup"><span data-stu-id="4ab9e-687">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="4ab9e-688">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-688">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="4ab9e-689">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-689">Address:</span></span> <br><span data-ttu-id="4ab9e-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마</span><span class="sxs-lookup"><span data-stu-id="4ab9e-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="4ab9e-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-694">SQL Server Analysis Services 다차원</span><span class="sxs-lookup"><span data-stu-id="4ab9e-694">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="4ab9e-695">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-695">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-696">모델</span><span class="sxs-lookup"><span data-stu-id="4ab9e-696">Model</span></span></td>
      <td><span data-ttu-id="4ab9e-697">
        <font size=2> 프로토콜: analysis-services</span><span class="sxs-lookup"><span data-stu-id="4ab9e-697">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="4ab9e-698">인증: {windows, 기본, 익명, 없음}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-698">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="4ab9e-699">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-699">Address:</span></span> <br><span data-ttu-id="4ab9e-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 모델 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-703">SQL Server Analysis Services 다차원</span><span class="sxs-lookup"><span data-stu-id="4ab9e-703">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="4ab9e-704">KPI</span><span class="sxs-lookup"><span data-stu-id="4ab9e-704">KPI</span></span></td>
      <td><span data-ttu-id="4ab9e-705">KPI</span><span class="sxs-lookup"><span data-stu-id="4ab9e-705">KPI</span></span></td>
      <td><span data-ttu-id="4ab9e-706">
        <font size=2> 프로토콜: analysis-services</span><span class="sxs-lookup"><span data-stu-id="4ab9e-706">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="4ab9e-707">인증: {windows, 기본, 익명, 없음}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-707">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="4ab9e-708">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-708">Address:</span></span> <br><span data-ttu-id="4ab9e-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 모델</span><span class="sxs-lookup"><span data-stu-id="4ab9e-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="4ab9e-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체</span><span class="sxs-lookup"><span data-stu-id="4ab9e-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="4ab9e-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-714">SQL Server Analysis Services 다차원</span><span class="sxs-lookup"><span data-stu-id="4ab9e-714">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="4ab9e-715">측정값</span><span class="sxs-lookup"><span data-stu-id="4ab9e-715">Measure</span></span></td>
      <td><span data-ttu-id="4ab9e-716">측정값</span><span class="sxs-lookup"><span data-stu-id="4ab9e-716">Measure</span></span></td>
      <td><span data-ttu-id="4ab9e-717">
        <font size=2> 프로토콜: analysis-services</span><span class="sxs-lookup"><span data-stu-id="4ab9e-717">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="4ab9e-718">인증: {windows, 기본, 익명, 없음}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-718">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="4ab9e-719">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-719">Address:</span></span> <br><span data-ttu-id="4ab9e-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 모델</span><span class="sxs-lookup"><span data-stu-id="4ab9e-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="4ab9e-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체</span><span class="sxs-lookup"><span data-stu-id="4ab9e-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="4ab9e-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {측정값} </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-725">SQL Server Analysis Services 다차원</span><span class="sxs-lookup"><span data-stu-id="4ab9e-725">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="4ab9e-726">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-726">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-727">차원</span><span class="sxs-lookup"><span data-stu-id="4ab9e-727">Dimension</span></span></td>
      <td><span data-ttu-id="4ab9e-728">
        <font size=2> 프로토콜: analysis-services</span><span class="sxs-lookup"><span data-stu-id="4ab9e-728">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="4ab9e-729">인증: {windows, 기본, 익명, 없음}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-729">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="4ab9e-730">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-730">Address:</span></span> <br><span data-ttu-id="4ab9e-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 모델</span><span class="sxs-lookup"><span data-stu-id="4ab9e-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="4ab9e-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체</span><span class="sxs-lookup"><span data-stu-id="4ab9e-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="4ab9e-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {차원} </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-736">SQL Server Analysis Services 테이블 형식</span><span class="sxs-lookup"><span data-stu-id="4ab9e-736">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="4ab9e-737">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-737">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-738">모델</span><span class="sxs-lookup"><span data-stu-id="4ab9e-738">Model</span></span></td>
      <td><span data-ttu-id="4ab9e-739">
        <font size=2> 프로토콜: analysis-services</span><span class="sxs-lookup"><span data-stu-id="4ab9e-739">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="4ab9e-740">인증: {windows, 기본, 익명, 없음}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-740">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="4ab9e-741">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-741">Address:</span></span> <br><span data-ttu-id="4ab9e-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 모델 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-745">SQL Server Analysis Services 테이블 형식</span><span class="sxs-lookup"><span data-stu-id="4ab9e-745">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="4ab9e-746">KPI</span><span class="sxs-lookup"><span data-stu-id="4ab9e-746">KPI</span></span></td>
      <td><span data-ttu-id="4ab9e-747">KPI</span><span class="sxs-lookup"><span data-stu-id="4ab9e-747">KPI</span></span></td>
      <td><span data-ttu-id="4ab9e-748">
        <font size=2> 프로토콜: analysis-services</span><span class="sxs-lookup"><span data-stu-id="4ab9e-748">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="4ab9e-749">인증: {windows, 기본, 익명, 없음}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-749">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="4ab9e-750">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-750">Address:</span></span> <br><span data-ttu-id="4ab9e-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 모델</span><span class="sxs-lookup"><span data-stu-id="4ab9e-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="4ab9e-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체</span><span class="sxs-lookup"><span data-stu-id="4ab9e-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="4ab9e-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-756">SQL Server Analysis Services 테이블 형식</span><span class="sxs-lookup"><span data-stu-id="4ab9e-756">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="4ab9e-757">측정값</span><span class="sxs-lookup"><span data-stu-id="4ab9e-757">Measure</span></span></td>
      <td><span data-ttu-id="4ab9e-758">측정값</span><span class="sxs-lookup"><span data-stu-id="4ab9e-758">Measure</span></span></td>
      <td><span data-ttu-id="4ab9e-759">
        <font size=2> 프로토콜: analysis-services</span><span class="sxs-lookup"><span data-stu-id="4ab9e-759">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="4ab9e-760">인증: {windows, 기본, 익명, 없음}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-760">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="4ab9e-761">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-761">Address:</span></span> <br><span data-ttu-id="4ab9e-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 모델</span><span class="sxs-lookup"><span data-stu-id="4ab9e-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="4ab9e-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체</span><span class="sxs-lookup"><span data-stu-id="4ab9e-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="4ab9e-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {측정값} </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-767">SQL Server Analysis Services 테이블 형식</span><span class="sxs-lookup"><span data-stu-id="4ab9e-767">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="4ab9e-768">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-768">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-769">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-769">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-770">
        <font size=2> 프로토콜: analysis-services</span><span class="sxs-lookup"><span data-stu-id="4ab9e-770">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="4ab9e-771">인증: {windows, 기본, 익명, 없음}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-771">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="4ab9e-772">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-772">Address:</span></span> <br><span data-ttu-id="4ab9e-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 모델</span><span class="sxs-lookup"><span data-stu-id="4ab9e-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="4ab9e-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체</span><span class="sxs-lookup"><span data-stu-id="4ab9e-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="4ab9e-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {테이블} </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-778">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="4ab9e-778">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="4ab9e-779">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-779">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-780">서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-780">Server</span></span></td>
      <td><span data-ttu-id="4ab9e-781">
        <font size=2> 프로토콜: reporting-services</span><span class="sxs-lookup"><span data-stu-id="4ab9e-781">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="4ab9e-782">인증: {windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-782">Authentication: {windows}</span></span> <br><span data-ttu-id="4ab9e-783">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-783">Address:</span></span> <br><span data-ttu-id="4ab9e-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 버전: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-786">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="4ab9e-786">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="4ab9e-787">보고서</span><span class="sxs-lookup"><span data-stu-id="4ab9e-787">Report</span></span></td>
      <td><span data-ttu-id="4ab9e-788">보고서</span><span class="sxs-lookup"><span data-stu-id="4ab9e-788">Report</span></span></td>
      <td><span data-ttu-id="4ab9e-789">
        <font size=2> 프로토콜: reporting-services</span><span class="sxs-lookup"><span data-stu-id="4ab9e-789">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="4ab9e-790">인증: {windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-790">Authentication: {windows}</span></span> <br><span data-ttu-id="4ab9e-791">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-791">Address:</span></span> <br><span data-ttu-id="4ab9e-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 경로</span><span class="sxs-lookup"><span data-stu-id="4ab9e-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path</span></span> <br><span data-ttu-id="4ab9e-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 버전: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-795">Teradata</span><span class="sxs-lookup"><span data-stu-id="4ab9e-795">Teradata</span></span></td>
      <td><span data-ttu-id="4ab9e-796">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-796">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-797">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-797">Database</span></span></td>
      <td><span data-ttu-id="4ab9e-798">
        <font size=2> 프로토콜: teradata</span><span class="sxs-lookup"><span data-stu-id="4ab9e-798">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="4ab9e-799">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-799">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="4ab9e-800">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-800">Address:</span></span> <br><span data-ttu-id="4ab9e-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-803">Teradata</span><span class="sxs-lookup"><span data-stu-id="4ab9e-803">Teradata</span></span></td>
      <td><span data-ttu-id="4ab9e-804">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-804">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-805">테이블, 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-805">Table, view</span></span></td>
      <td><span data-ttu-id="4ab9e-806">
        <font size=2> 프로토콜: teradata</span><span class="sxs-lookup"><span data-stu-id="4ab9e-806">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="4ab9e-807">인증: {프로토콜, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-807">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="4ab9e-808">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-808">Address:</span></span> <br><span data-ttu-id="4ab9e-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-812">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="4ab9e-812">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="4ab9e-813">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-813">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-814">모델</span><span class="sxs-lookup"><span data-stu-id="4ab9e-814">Model</span></span></td>
      <td><span data-ttu-id="4ab9e-815">
        <font size="2"> 프로토콜: mssql-mds</span><span class="sxs-lookup"><span data-stu-id="4ab9e-815">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="4ab9e-816">인증: {windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-816">Authentication: {windows}</span></span> <br><span data-ttu-id="4ab9e-817">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-817">Address:</span></span> <br><span data-ttu-id="4ab9e-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="4ab9e-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="4ab9e-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 모델</span><span class="sxs-lookup"><span data-stu-id="4ab9e-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="4ab9e-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 버전 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-821">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="4ab9e-821">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="4ab9e-822">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-822">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-823">엔터티</span><span class="sxs-lookup"><span data-stu-id="4ab9e-823">Entity</span></span></td>
      <td><span data-ttu-id="4ab9e-824">
        <font size="2"> 프로토콜: mssql-mds</span><span class="sxs-lookup"><span data-stu-id="4ab9e-824">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="4ab9e-825">인증: {windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-825">Authentication: {windows}</span></span> <br><span data-ttu-id="4ab9e-826">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-826">Address:</span></span> <br><span data-ttu-id="4ab9e-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="4ab9e-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="4ab9e-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 모델</span><span class="sxs-lookup"><span data-stu-id="4ab9e-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="4ab9e-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 버전</span><span class="sxs-lookup"><span data-stu-id="4ab9e-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version</span></span> <br><span data-ttu-id="4ab9e-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 엔터티 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entity </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-831">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4ab9e-831">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="4ab9e-832">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-832">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-833">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-833">Database</span></span></td>
      <td><span data-ttu-id="4ab9e-834">
        <font size=2> 프로토콜: document-db</span><span class="sxs-lookup"><span data-stu-id="4ab9e-834">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="4ab9e-835">인증: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-835">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="4ab9e-836">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-836">Address:</span></span> <br><span data-ttu-id="4ab9e-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="4ab9e-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="4ab9e-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-839">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4ab9e-839">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="4ab9e-840">컬렉션</span><span class="sxs-lookup"><span data-stu-id="4ab9e-840">Collection</span></span></td>
      <td><span data-ttu-id="4ab9e-841">컬렉션</span><span class="sxs-lookup"><span data-stu-id="4ab9e-841">Collection</span></span></td>
      <td><span data-ttu-id="4ab9e-842">
        <font size=2> 프로토콜: document-db</span><span class="sxs-lookup"><span data-stu-id="4ab9e-842">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="4ab9e-843">인증: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-843">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="4ab9e-844">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-844">Address:</span></span> <br><span data-ttu-id="4ab9e-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="4ab9e-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="4ab9e-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 컬렉션 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; collection </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-848">일반 ODBC</span><span class="sxs-lookup"><span data-stu-id="4ab9e-848">Generic ODBC</span></span></td>
      <td><span data-ttu-id="4ab9e-849">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-849">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-850">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-850">Database</span></span></td>
      <td><span data-ttu-id="4ab9e-851">
        <font size=2> 프로토콜: odbc</span><span class="sxs-lookup"><span data-stu-id="4ab9e-851">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="4ab9e-852">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-852">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="4ab9e-853">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-853">Address:</span></span> <br><span data-ttu-id="4ab9e-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 옵션</span><span class="sxs-lookup"><span data-stu-id="4ab9e-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="4ab9e-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-856">일반 ODBC</span><span class="sxs-lookup"><span data-stu-id="4ab9e-856">Generic ODBC</span></span></td>
      <td><span data-ttu-id="4ab9e-857">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-857">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-858">테이블, 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-858">Table, View</span></span></td>
      <td><span data-ttu-id="4ab9e-859">
        <font size=2> 프로토콜: odbc</span><span class="sxs-lookup"><span data-stu-id="4ab9e-859">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="4ab9e-860">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-860">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="4ab9e-861">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-861">Address:</span></span> <br><span data-ttu-id="4ab9e-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 옵션</span><span class="sxs-lookup"><span data-stu-id="4ab9e-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="4ab9e-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체</span><span class="sxs-lookup"><span data-stu-id="4ab9e-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="4ab9e-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-866">Sybase</span><span class="sxs-lookup"><span data-stu-id="4ab9e-866">Sybase</span></span></td>
      <td><span data-ttu-id="4ab9e-867">컨테이너</span><span class="sxs-lookup"><span data-stu-id="4ab9e-867">Container</span></span></td>
      <td><span data-ttu-id="4ab9e-868">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-868">Database</span></span></td>
      <td><span data-ttu-id="4ab9e-869">
        <font size=2> 프로토콜: sybase</span><span class="sxs-lookup"><span data-stu-id="4ab9e-869">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="4ab9e-870">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-870">authentication: {basic, windows}</span></span> <br><span data-ttu-id="4ab9e-871">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-871">address:</span></span> <br><span data-ttu-id="4ab9e-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-874">Sybase</span><span class="sxs-lookup"><span data-stu-id="4ab9e-874">Sybase</span></span></td>
      <td><span data-ttu-id="4ab9e-875">테이블</span><span class="sxs-lookup"><span data-stu-id="4ab9e-875">Table</span></span></td>
      <td><span data-ttu-id="4ab9e-876">테이블, 뷰</span><span class="sxs-lookup"><span data-stu-id="4ab9e-876">Table, View</span></span></td>
      <td><span data-ttu-id="4ab9e-877">
        <font size=2> 프로토콜: sybase</span><span class="sxs-lookup"><span data-stu-id="4ab9e-877">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="4ab9e-878">인증: {기본, windows}</span><span class="sxs-lookup"><span data-stu-id="4ab9e-878">authentication: {basic, windows}</span></span> <br><span data-ttu-id="4ab9e-879">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-879">address:</span></span> <br><span data-ttu-id="4ab9e-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 서버</span><span class="sxs-lookup"><span data-stu-id="4ab9e-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="4ab9e-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4ab9e-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="4ab9e-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 스키마</span><span class="sxs-lookup"><span data-stu-id="4ab9e-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="4ab9e-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 개체 </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="4ab9e-884">다른 (위의 hello의 없음)</span><span class="sxs-lookup"><span data-stu-id="4ab9e-884">Other (none of hello above)</span></span></td>
      <td>\*</td>
      <td>\*</td>
      <td><span data-ttu-id="4ab9e-885">
        <font size=2> 프로토콜: generic-asset</span><span class="sxs-lookup"><span data-stu-id="4ab9e-885">
        <font size=2> Protocol: generic-asset</span></span> <br><span data-ttu-id="4ab9e-886">주소:</span><span class="sxs-lookup"><span data-stu-id="4ab9e-886">Address:</span></span> <br><span data-ttu-id="4ab9e-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span><span class="sxs-lookup"><span data-stu-id="4ab9e-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span></span></td>
    </tr>
</table>
