---
title: "Azure 저장소를 사용 하기 위한 aaaTools | Microsoft Docs"
description: "목록 Azure 저장소 데이터와 tooview/상호 작용할 수 있는 도구입니다."
services: storage
documentationcenter: 
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: e4748642-98c4-437e-b0ed-4f9641c2e894
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: dineshmurthy
ms.openlocfilehash: 3308de2153099a05a676ab1d76426bd932e8a96c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-client-tools"></a><span data-ttu-id="e7d53-103">Azure 저장소 클라이언트 도구</span><span class="sxs-lookup"><span data-stu-id="e7d53-103">Azure Storage Client Tools</span></span>
<span data-ttu-id="e7d53-104">사용자가 Azure 저장소의 자주 원하는 toobe 수 tooview/상호 작용는 Azure 저장소 클라이언트 도구를 사용 하 여 해당 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d53-104">Users of Azure Storage frequently want toobe able tooview/interact with their data using an Azure Storage client tool.</span></span> <span data-ttu-id="e7d53-105">Hello 테이블 아래에 나열 다양 한 toodo 할 수 있도록 도구가이 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d53-105">In hello tables below, we list a number of tools that allow you toodo this.</span></span> <span data-ttu-id="e7d53-106">Hello 기능을 제공 하는 경우 각 블록에 "X" 입력 tooeither 열거 및/또는 액세스 hello 데이터 추상화 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d53-106">We put an "X" in each block if it provides hello ability tooeither enumerate and/or access hello data abstraction.</span></span> <span data-ttu-id="e7d53-107">hello 테이블에는 hello 도구 무료 인지 인지 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e7d53-107">hello table also shows if hello tools is free or not.</span></span> <span data-ttu-id="e7d53-108">"평가판" 무료 평가판을는 있지만 hello 정식 제품은 무료를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e7d53-108">"Trial" indicates that there is a free trial, but hello full product is not free.</span></span> <span data-ttu-id="e7d53-109">“Y/N”는 특정 버전은 무료로 제공되지만 다른 버전은 구매할 수 있는지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e7d53-109">"Y/N" indicates that a version is available for free, while a different version is available for purchase.</span></span>

<span data-ttu-id="e7d53-110">Azure 저장소 클라이언트 도구를 사용할 수 있는 hello에 대 한 스냅숏을 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d53-110">We've only provided a snapshot of hello available Azure Storage client tools.</span></span> <span data-ttu-id="e7d53-111">이러한 도구는 tooevolve 계속 하 고 기능이 증가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d53-111">These tools may continue tooevolve and grow in functionality.</span></span> <span data-ttu-id="e7d53-112">가 있는 경우에 수정 사항이 나 업데이트 알려주세요 주석 toolet를 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="e7d53-112">If there are corrections or updates, please leave a comment toolet us know.</span></span> <span data-ttu-id="e7d53-113">hello 같은 기준이 만족도 매우 tooadd 하겠습니다-toobe 여기에 포함 해야 하는 도구가 알고 있는 경우 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d53-113">hello same is true if you know of tools that ought toobe here - we'd be happy tooadd them.</span></span>

<span data-ttu-id="e7d53-114">**Microsoft Azure 저장소 클라이언트 도구**</span><span class="sxs-lookup"><span data-stu-id="e7d53-114">**Microsoft Azure Storage Client Tools**</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="e7d53-115">Azure 저장소 클라이언트 도구</span><span class="sxs-lookup"><span data-stu-id="e7d53-115">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="e7d53-116">블록 Blob</span><span class="sxs-lookup"><span data-stu-id="e7d53-116">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="e7d53-117">페이지 Blob</span><span class="sxs-lookup"><span data-stu-id="e7d53-117">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="e7d53-118">Blob 추가</span><span class="sxs-lookup"><span data-stu-id="e7d53-118">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="e7d53-119">테이블</span><span class="sxs-lookup"><span data-stu-id="e7d53-119">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="e7d53-120">큐</span><span class="sxs-lookup"><span data-stu-id="e7d53-120">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="e7d53-121">파일</span><span class="sxs-lookup"><span data-stu-id="e7d53-121">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="e7d53-122">무료</span><span class="sxs-lookup"><span data-stu-id="e7d53-122">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="e7d53-123">플랫폼</span><span class="sxs-lookup"><span data-stu-id="e7d53-123">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="e7d53-124">웹</span><span class="sxs-lookup"><span data-stu-id="e7d53-124">Web</span></span></td>
    <td><span data-ttu-id="e7d53-125">Windows</span><span class="sxs-lookup"><span data-stu-id="e7d53-125">Windows</span></span></td>
    <td><span data-ttu-id="e7d53-126">OSX</span><span class="sxs-lookup"><span data-stu-id="e7d53-126">OSX</span></span></td>
    <td><span data-ttu-id="e7d53-127">Linux</span><span class="sxs-lookup"><span data-stu-id="e7d53-127">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e7d53-128"><a href="https://azure.microsoft.com/features/azure-portal/">Microsoft Azure Portal</a></span><span class="sxs-lookup"><span data-stu-id="e7d53-128"><a href="https://azure.microsoft.com/features/azure-portal/">Microsoft Azure Portal</a></span></span></td>
    <td><span data-ttu-id="e7d53-129">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-129">X</span></span></td>
    <td><span data-ttu-id="e7d53-130">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-130">X</span></span></td>
    <td><span data-ttu-id="e7d53-131">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-131">X</span></span></td>
    <td><span data-ttu-id="e7d53-132">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-132">X</span></span></td>
    <td><span data-ttu-id="e7d53-133">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-133">X</span></span></td>
    <td><span data-ttu-id="e7d53-134">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-134">X</span></span></td>
    <td><span data-ttu-id="e7d53-135">Y</span><span class="sxs-lookup"><span data-stu-id="e7d53-135">Y</span></span></td>
    <td><span data-ttu-id="e7d53-136">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-136">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e7d53-137"><a href="http://storageexplorer.com/">Microsoft Azure Storage Explorer</a></span><span class="sxs-lookup"><span data-stu-id="e7d53-137"><a href="http://storageexplorer.com/">Microsoft Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="e7d53-138">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-138">X</span></span></td>
    <td><span data-ttu-id="e7d53-139">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-139">X</span></span></td>
    <td><span data-ttu-id="e7d53-140">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-140">X</span></span></td>
    <td><span data-ttu-id="e7d53-141">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-141">X</span></span></td>
    <td><span data-ttu-id="e7d53-142">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-142">X</span></span></td>
    <td><span data-ttu-id="e7d53-143">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-143">X</span></span></td>
    <td><span data-ttu-id="e7d53-144">Y</span><span class="sxs-lookup"><span data-stu-id="e7d53-144">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="e7d53-145">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-145">X</span></span></td>
    <td><span data-ttu-id="e7d53-146">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-146">X</span></span></td>
    <td><span data-ttu-id="e7d53-147">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-147">X</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e7d53-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Microsoft Visual Studio 서버 탐색기</a></span><span class="sxs-lookup"><span data-stu-id="e7d53-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Microsoft Visual Studio Server Explorer</a></span></span></td>
    <td><span data-ttu-id="e7d53-149">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-149">X</span></span></td>
    <td><span data-ttu-id="e7d53-150">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-150">X</span></span></td>
    <td><span data-ttu-id="e7d53-151">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-151">X</span></span></td>
    <td><span data-ttu-id="e7d53-152">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-152">X</span></span></td>
    <td><span data-ttu-id="e7d53-153">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-153">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="e7d53-154">Y</span><span class="sxs-lookup"><span data-stu-id="e7d53-154">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="e7d53-155">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-155">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
</table>

<span data-ttu-id="e7d53-156">**타사 Azure 저장소 클라이언트 도구**</span><span class="sxs-lookup"><span data-stu-id="e7d53-156">**Third-Party Azure Storage Client Tools**</span></span>

<span data-ttu-id="e7d53-157">Hello 기능 또는 품질 hello 타사 도구 및 해당 목록에서 Microsoft의 보증을 의미 하지 않습니다 확인 하지 않았으며 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d53-157">We have not verified hello functionality or quality claimed by hello following third-party tools and their listing does not imply an endorsement by Microsoft.</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="e7d53-158">Azure 저장소 클라이언트 도구</span><span class="sxs-lookup"><span data-stu-id="e7d53-158">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="e7d53-159">블록 Blob</span><span class="sxs-lookup"><span data-stu-id="e7d53-159">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="e7d53-160">페이지 Blob</span><span class="sxs-lookup"><span data-stu-id="e7d53-160">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="e7d53-161">Blob 추가</span><span class="sxs-lookup"><span data-stu-id="e7d53-161">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="e7d53-162">테이블</span><span class="sxs-lookup"><span data-stu-id="e7d53-162">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="e7d53-163">큐</span><span class="sxs-lookup"><span data-stu-id="e7d53-163">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="e7d53-164">파일</span><span class="sxs-lookup"><span data-stu-id="e7d53-164">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="e7d53-165">무료</span><span class="sxs-lookup"><span data-stu-id="e7d53-165">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="e7d53-166">플랫폼</span><span class="sxs-lookup"><span data-stu-id="e7d53-166">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="e7d53-167">웹</span><span class="sxs-lookup"><span data-stu-id="e7d53-167">Web</span></span></td>
    <td><span data-ttu-id="e7d53-168">Windows</span><span class="sxs-lookup"><span data-stu-id="e7d53-168">Windows</span></span></td>
    <td><span data-ttu-id="e7d53-169">OSX</span><span class="sxs-lookup"><span data-stu-id="e7d53-169">OSX</span></span></td>
    <td><span data-ttu-id="e7d53-170">Linux</span><span class="sxs-lookup"><span data-stu-id="e7d53-170">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e7d53-171"><a href="http://www.cloudportam.com/">Cloud Portam</a></span><span class="sxs-lookup"><span data-stu-id="e7d53-171"><a href="http://www.cloudportam.com/">Cloud Portam</a></span></span></td>
    <td><span data-ttu-id="e7d53-172">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-172">X</span></span></td>
    <td><span data-ttu-id="e7d53-173">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-173">X</span></span></td>
    <td><span data-ttu-id="e7d53-174">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-174">X</span></span></td>
    <td><span data-ttu-id="e7d53-175">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-175">X</span></span></td>
    <td><span data-ttu-id="e7d53-176">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-176">X</span></span></td>
    <td><span data-ttu-id="e7d53-177">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-177">X</span></span></td>
    <td><span data-ttu-id="e7d53-178">평가판</span><span class="sxs-lookup"><span data-stu-id="e7d53-178">Trial</span></span></td>
    <td><span data-ttu-id="e7d53-179">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-179">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e7d53-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span><span class="sxs-lookup"><span data-stu-id="e7d53-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span></span></td>
    <td><span data-ttu-id="e7d53-181">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-181">X</span></span></td>
    <td><span data-ttu-id="e7d53-182">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-182">X</span></span></td>
    <td><span data-ttu-id="e7d53-183">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-183">X</span></span></td>
    <td><span data-ttu-id="e7d53-184">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-184">X</span></span></td>
    <td><span data-ttu-id="e7d53-185">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-185">X</span></span></td>
    <td><span data-ttu-id="e7d53-186">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-186">X</span></span></td>
    <td><span data-ttu-id="e7d53-187">평가판</span><span class="sxs-lookup"><span data-stu-id="e7d53-187">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="e7d53-188">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-188">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e7d53-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Azure Explorer</a></span><span class="sxs-lookup"><span data-stu-id="e7d53-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Azure Explorer</a></span></span></td>
    <td><span data-ttu-id="e7d53-190">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-190">X</span></span></td>
    <td><span data-ttu-id="e7d53-191">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-191">X</span></span></td>
    <td><span data-ttu-id="e7d53-192">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-192">X</span></span></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="e7d53-193">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-193">X</span></span></td>
    <td><span data-ttu-id="e7d53-194">Y</span><span class="sxs-lookup"><span data-stu-id="e7d53-194">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="e7d53-195">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-195">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e7d53-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Azure 저장소 탐색기</a></span><span class="sxs-lookup"><span data-stu-id="e7d53-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="e7d53-197">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-197">X</span></span></td>
    <td><span data-ttu-id="e7d53-198">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-198">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="e7d53-199">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-199">X</span></span></td>
    <td><span data-ttu-id="e7d53-200">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-200">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="e7d53-201">Y</span><span class="sxs-lookup"><span data-stu-id="e7d53-201">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="e7d53-202">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-202">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e7d53-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry Explorer</a></span><span class="sxs-lookup"><span data-stu-id="e7d53-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry Explorer</a></span></span></td>
    <td><span data-ttu-id="e7d53-204">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-204">X</span></span></td>
    <td><span data-ttu-id="e7d53-205">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-205">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="e7d53-206">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-206">X</span></span></td>
    <td><span data-ttu-id="e7d53-207">Y/N</span><span class="sxs-lookup"><span data-stu-id="e7d53-207">Y/N</span></span></td>
    <td></td>
    <td><span data-ttu-id="e7d53-208">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-208">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e7d53-209"><a href="http://www.gapotchenko.com/cloudcombine">Cloud Combine</a></span><span class="sxs-lookup"><span data-stu-id="e7d53-209"><a href="http://www.gapotchenko.com/cloudcombine">Cloud Combine</a></span></span></td>
    <td><span data-ttu-id="e7d53-210">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-210">X</span></span></td>
    <td><span data-ttu-id="e7d53-211">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-211">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="e7d53-212">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-212">X</span></span></td>
    <td><span data-ttu-id="e7d53-213">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-213">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="e7d53-214">평가판</span><span class="sxs-lookup"><span data-stu-id="e7d53-214">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="e7d53-215">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-215">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e7d53-216"><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></span><span class="sxs-lookup"><span data-stu-id="e7d53-216"><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></span></span></td>
    <td><span data-ttu-id="e7d53-217">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-217">X</span></span></td>
    <td><span data-ttu-id="e7d53-218">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-218">X</span></span></td>
    <td><span data-ttu-id="e7d53-219">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-219">X</span></span></td>
    <td><span data-ttu-id="e7d53-220">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-220">X</span></span></td>
    <td><span data-ttu-id="e7d53-221">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-221">X</span></span></td>
    <td><span data-ttu-id="e7d53-222">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-222">X</span></span></td>
    <td><span data-ttu-id="e7d53-223">Y</span><span class="sxs-lookup"><span data-stu-id="e7d53-223">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="e7d53-224">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-224">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e7d53-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet Cloud</a></span><span class="sxs-lookup"><span data-stu-id="e7d53-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet Cloud</a></span></span></td>
    <td><span data-ttu-id="e7d53-226">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-226">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="e7d53-227">평가판</span><span class="sxs-lookup"><span data-stu-id="e7d53-227">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="e7d53-228">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-228">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e7d53-229"><a href="http://storageexplorer.codeplex.com/">Azure Web Storage Explorer</a></span><span class="sxs-lookup"><span data-stu-id="e7d53-229"><a href="http://storageexplorer.codeplex.com/">Azure Web Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="e7d53-230">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-230">X</span></span></td>
    <td><span data-ttu-id="e7d53-231">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-231">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="e7d53-232">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-232">X</span></span></td>
    <td><span data-ttu-id="e7d53-233">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-233">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="e7d53-234">Y</span><span class="sxs-lookup"><span data-stu-id="e7d53-234">Y</span></span></td>
    <td><span data-ttu-id="e7d53-235">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-235">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="e7d53-236"><a href="https://zudio.co/">Zudio</a></span><span class="sxs-lookup"><span data-stu-id="e7d53-236"><a href="https://zudio.co/">Zudio</a></span></span></td>
    <td><span data-ttu-id="e7d53-237">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-237">X</span></span></td>
    <td><span data-ttu-id="e7d53-238">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-238">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="e7d53-239">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-239">X</span></span></td>
    <td><span data-ttu-id="e7d53-240">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-240">X</span></span></td>
    <td><span data-ttu-id="e7d53-241">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-241">X</span></span></td>
    <td><span data-ttu-id="e7d53-242">평가판</span><span class="sxs-lookup"><span data-stu-id="e7d53-242">Trial</span></span></td>
    <td><span data-ttu-id="e7d53-243">X</span><span class="sxs-lookup"><span data-stu-id="e7d53-243">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>
