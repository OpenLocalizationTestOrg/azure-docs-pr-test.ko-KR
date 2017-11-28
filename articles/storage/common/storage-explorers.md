---
title: "Azure Storage 작업을 위한 도구 | Microsoft Docs"
description: "Azure 저장소 데이터를 보고 상호 작용할 수 있는 도구 목록입니다."
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
ms.openlocfilehash: 620efda06d8225b21b6bb9b104b79061ebb6515c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-client-tools"></a><span data-ttu-id="d763b-103">Azure 저장소 클라이언트 도구</span><span class="sxs-lookup"><span data-stu-id="d763b-103">Azure Storage Client Tools</span></span>
<span data-ttu-id="d763b-104">Azure 저장소의 사용자는 Azure 저장소 클라이언트 도구를 사용하여 데이터를 보기/상호 작용하려는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="d763b-104">Users of Azure Storage frequently want to be able to view/interact with their data using an Azure Storage client tool.</span></span> <span data-ttu-id="d763b-105">아래 표에는 이 작업을 수행할 수 있게 해 주는 여러 도구가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d763b-105">In the tables below, we list a number of tools that allow you to do this.</span></span> <span data-ttu-id="d763b-106">해당 도구가 데이터 추상화를 열거 및/또는 액세스할 수 있는 기능을 제공하는 경우 각 블록에 “X” 표시를 합니다.</span><span class="sxs-lookup"><span data-stu-id="d763b-106">We put an "X" in each block if it provides the ability to either enumerate and/or access the data abstraction.</span></span> <span data-ttu-id="d763b-107">또한 도구가 무료인지 여부도 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d763b-107">The table also shows if the tools is free or not.</span></span> <span data-ttu-id="d763b-108">“평가판”은 무료 평가판이 있음을 나타내지만 정품은 무료가 아님을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d763b-108">"Trial" indicates that there is a free trial, but the full product is not free.</span></span> <span data-ttu-id="d763b-109">“Y/N”는 특정 버전은 무료로 제공되지만 다른 버전은 구매할 수 있는지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d763b-109">"Y/N" indicates that a version is available for free, while a different version is available for purchase.</span></span>

<span data-ttu-id="d763b-110">사용 가능한 Azure 저장소 클라이언트 도구의 스냅숏만 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d763b-110">We've only provided a snapshot of the available Azure Storage client tools.</span></span> <span data-ttu-id="d763b-111">이러한 도구의 기능은 계속 개선 및 확장될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d763b-111">These tools may continue to evolve and grow in functionality.</span></span> <span data-ttu-id="d763b-112">수정 사항이나 업데이트가 있는 경우 의견을 남겨주세요.</span><span class="sxs-lookup"><span data-stu-id="d763b-112">If there are corrections or updates, please leave a comment to let us know.</span></span> <span data-ttu-id="d763b-113">여기에 포함해야 할 도구가 있는 경우에도 알려주시면 추가해 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d763b-113">The same is true if you know of tools that ought to be here - we'd be happy to add them.</span></span>

<span data-ttu-id="d763b-114">**Microsoft Azure 저장소 클라이언트 도구**</span><span class="sxs-lookup"><span data-stu-id="d763b-114">**Microsoft Azure Storage Client Tools**</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="d763b-115">Azure 저장소 클라이언트 도구</span><span class="sxs-lookup"><span data-stu-id="d763b-115">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="d763b-116">블록 Blob</span><span class="sxs-lookup"><span data-stu-id="d763b-116">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="d763b-117">페이지 Blob</span><span class="sxs-lookup"><span data-stu-id="d763b-117">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="d763b-118">Blob 추가</span><span class="sxs-lookup"><span data-stu-id="d763b-118">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="d763b-119">테이블</span><span class="sxs-lookup"><span data-stu-id="d763b-119">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="d763b-120">큐</span><span class="sxs-lookup"><span data-stu-id="d763b-120">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="d763b-121">파일</span><span class="sxs-lookup"><span data-stu-id="d763b-121">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="d763b-122">무료</span><span class="sxs-lookup"><span data-stu-id="d763b-122">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="d763b-123">플랫폼</span><span class="sxs-lookup"><span data-stu-id="d763b-123">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="d763b-124">웹</span><span class="sxs-lookup"><span data-stu-id="d763b-124">Web</span></span></td>
    <td><span data-ttu-id="d763b-125">Windows</span><span class="sxs-lookup"><span data-stu-id="d763b-125">Windows</span></span></td>
    <td><span data-ttu-id="d763b-126">OSX</span><span class="sxs-lookup"><span data-stu-id="d763b-126">OSX</span></span></td>
    <td><span data-ttu-id="d763b-127">Linux</span><span class="sxs-lookup"><span data-stu-id="d763b-127">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="d763b-128"><a href="https://azure.microsoft.com/features/azure-portal/">Microsoft Azure Portal</a></span><span class="sxs-lookup"><span data-stu-id="d763b-128"><a href="https://azure.microsoft.com/features/azure-portal/">Microsoft Azure Portal</a></span></span></td>
    <td><span data-ttu-id="d763b-129">X</span><span class="sxs-lookup"><span data-stu-id="d763b-129">X</span></span></td>
    <td><span data-ttu-id="d763b-130">X</span><span class="sxs-lookup"><span data-stu-id="d763b-130">X</span></span></td>
    <td><span data-ttu-id="d763b-131">X</span><span class="sxs-lookup"><span data-stu-id="d763b-131">X</span></span></td>
    <td><span data-ttu-id="d763b-132">X</span><span class="sxs-lookup"><span data-stu-id="d763b-132">X</span></span></td>
    <td><span data-ttu-id="d763b-133">X</span><span class="sxs-lookup"><span data-stu-id="d763b-133">X</span></span></td>
    <td><span data-ttu-id="d763b-134">X</span><span class="sxs-lookup"><span data-stu-id="d763b-134">X</span></span></td>
    <td><span data-ttu-id="d763b-135">Y</span><span class="sxs-lookup"><span data-stu-id="d763b-135">Y</span></span></td>
    <td><span data-ttu-id="d763b-136">X</span><span class="sxs-lookup"><span data-stu-id="d763b-136">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="d763b-137"><a href="http://storageexplorer.com/">Microsoft Azure Storage Explorer</a></span><span class="sxs-lookup"><span data-stu-id="d763b-137"><a href="http://storageexplorer.com/">Microsoft Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="d763b-138">X</span><span class="sxs-lookup"><span data-stu-id="d763b-138">X</span></span></td>
    <td><span data-ttu-id="d763b-139">X</span><span class="sxs-lookup"><span data-stu-id="d763b-139">X</span></span></td>
    <td><span data-ttu-id="d763b-140">X</span><span class="sxs-lookup"><span data-stu-id="d763b-140">X</span></span></td>
    <td><span data-ttu-id="d763b-141">X</span><span class="sxs-lookup"><span data-stu-id="d763b-141">X</span></span></td>
    <td><span data-ttu-id="d763b-142">X</span><span class="sxs-lookup"><span data-stu-id="d763b-142">X</span></span></td>
    <td><span data-ttu-id="d763b-143">X</span><span class="sxs-lookup"><span data-stu-id="d763b-143">X</span></span></td>
    <td><span data-ttu-id="d763b-144">Y</span><span class="sxs-lookup"><span data-stu-id="d763b-144">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="d763b-145">X</span><span class="sxs-lookup"><span data-stu-id="d763b-145">X</span></span></td>
    <td><span data-ttu-id="d763b-146">X</span><span class="sxs-lookup"><span data-stu-id="d763b-146">X</span></span></td>
    <td><span data-ttu-id="d763b-147">X</span><span class="sxs-lookup"><span data-stu-id="d763b-147">X</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="d763b-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Microsoft Visual Studio 서버 탐색기</a></span><span class="sxs-lookup"><span data-stu-id="d763b-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Microsoft Visual Studio Server Explorer</a></span></span></td>
    <td><span data-ttu-id="d763b-149">X</span><span class="sxs-lookup"><span data-stu-id="d763b-149">X</span></span></td>
    <td><span data-ttu-id="d763b-150">X</span><span class="sxs-lookup"><span data-stu-id="d763b-150">X</span></span></td>
    <td><span data-ttu-id="d763b-151">X</span><span class="sxs-lookup"><span data-stu-id="d763b-151">X</span></span></td>
    <td><span data-ttu-id="d763b-152">X</span><span class="sxs-lookup"><span data-stu-id="d763b-152">X</span></span></td>
    <td><span data-ttu-id="d763b-153">X</span><span class="sxs-lookup"><span data-stu-id="d763b-153">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="d763b-154">Y</span><span class="sxs-lookup"><span data-stu-id="d763b-154">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="d763b-155">X</span><span class="sxs-lookup"><span data-stu-id="d763b-155">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
</table>

<span data-ttu-id="d763b-156">**타사 Azure 저장소 클라이언트 도구**</span><span class="sxs-lookup"><span data-stu-id="d763b-156">**Third-Party Azure Storage Client Tools**</span></span>

<span data-ttu-id="d763b-157">다음의 타사 도구가 주장하는 기능이나 품질은 보장할 수 없으며 목록에 포함되었다고 해서 Microsoft가 보증한다는 것을 의미하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d763b-157">We have not verified the functionality or quality claimed by the following third-party tools and their listing does not imply an endorsement by Microsoft.</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="d763b-158">Azure 저장소 클라이언트 도구</span><span class="sxs-lookup"><span data-stu-id="d763b-158">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="d763b-159">블록 Blob</span><span class="sxs-lookup"><span data-stu-id="d763b-159">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="d763b-160">페이지 Blob</span><span class="sxs-lookup"><span data-stu-id="d763b-160">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="d763b-161">Blob 추가</span><span class="sxs-lookup"><span data-stu-id="d763b-161">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="d763b-162">테이블</span><span class="sxs-lookup"><span data-stu-id="d763b-162">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="d763b-163">큐</span><span class="sxs-lookup"><span data-stu-id="d763b-163">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="d763b-164">파일</span><span class="sxs-lookup"><span data-stu-id="d763b-164">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="d763b-165">무료</span><span class="sxs-lookup"><span data-stu-id="d763b-165">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="d763b-166">플랫폼</span><span class="sxs-lookup"><span data-stu-id="d763b-166">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="d763b-167">웹</span><span class="sxs-lookup"><span data-stu-id="d763b-167">Web</span></span></td>
    <td><span data-ttu-id="d763b-168">Windows</span><span class="sxs-lookup"><span data-stu-id="d763b-168">Windows</span></span></td>
    <td><span data-ttu-id="d763b-169">OSX</span><span class="sxs-lookup"><span data-stu-id="d763b-169">OSX</span></span></td>
    <td><span data-ttu-id="d763b-170">Linux</span><span class="sxs-lookup"><span data-stu-id="d763b-170">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="d763b-171"><a href="http://www.cloudportam.com/">Cloud Portam</a></span><span class="sxs-lookup"><span data-stu-id="d763b-171"><a href="http://www.cloudportam.com/">Cloud Portam</a></span></span></td>
    <td><span data-ttu-id="d763b-172">X</span><span class="sxs-lookup"><span data-stu-id="d763b-172">X</span></span></td>
    <td><span data-ttu-id="d763b-173">X</span><span class="sxs-lookup"><span data-stu-id="d763b-173">X</span></span></td>
    <td><span data-ttu-id="d763b-174">X</span><span class="sxs-lookup"><span data-stu-id="d763b-174">X</span></span></td>
    <td><span data-ttu-id="d763b-175">X</span><span class="sxs-lookup"><span data-stu-id="d763b-175">X</span></span></td>
    <td><span data-ttu-id="d763b-176">X</span><span class="sxs-lookup"><span data-stu-id="d763b-176">X</span></span></td>
    <td><span data-ttu-id="d763b-177">X</span><span class="sxs-lookup"><span data-stu-id="d763b-177">X</span></span></td>
    <td><span data-ttu-id="d763b-178">평가판</span><span class="sxs-lookup"><span data-stu-id="d763b-178">Trial</span></span></td>
    <td><span data-ttu-id="d763b-179">X</span><span class="sxs-lookup"><span data-stu-id="d763b-179">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="d763b-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span><span class="sxs-lookup"><span data-stu-id="d763b-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span></span></td>
    <td><span data-ttu-id="d763b-181">X</span><span class="sxs-lookup"><span data-stu-id="d763b-181">X</span></span></td>
    <td><span data-ttu-id="d763b-182">X</span><span class="sxs-lookup"><span data-stu-id="d763b-182">X</span></span></td>
    <td><span data-ttu-id="d763b-183">X</span><span class="sxs-lookup"><span data-stu-id="d763b-183">X</span></span></td>
    <td><span data-ttu-id="d763b-184">X</span><span class="sxs-lookup"><span data-stu-id="d763b-184">X</span></span></td>
    <td><span data-ttu-id="d763b-185">X</span><span class="sxs-lookup"><span data-stu-id="d763b-185">X</span></span></td>
    <td><span data-ttu-id="d763b-186">X</span><span class="sxs-lookup"><span data-stu-id="d763b-186">X</span></span></td>
    <td><span data-ttu-id="d763b-187">평가판</span><span class="sxs-lookup"><span data-stu-id="d763b-187">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="d763b-188">X</span><span class="sxs-lookup"><span data-stu-id="d763b-188">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="d763b-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Azure Explorer</a></span><span class="sxs-lookup"><span data-stu-id="d763b-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Azure Explorer</a></span></span></td>
    <td><span data-ttu-id="d763b-190">X</span><span class="sxs-lookup"><span data-stu-id="d763b-190">X</span></span></td>
    <td><span data-ttu-id="d763b-191">X</span><span class="sxs-lookup"><span data-stu-id="d763b-191">X</span></span></td>
    <td><span data-ttu-id="d763b-192">X</span><span class="sxs-lookup"><span data-stu-id="d763b-192">X</span></span></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="d763b-193">X</span><span class="sxs-lookup"><span data-stu-id="d763b-193">X</span></span></td>
    <td><span data-ttu-id="d763b-194">Y</span><span class="sxs-lookup"><span data-stu-id="d763b-194">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="d763b-195">X</span><span class="sxs-lookup"><span data-stu-id="d763b-195">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="d763b-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Azure 저장소 탐색기</a></span><span class="sxs-lookup"><span data-stu-id="d763b-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="d763b-197">X</span><span class="sxs-lookup"><span data-stu-id="d763b-197">X</span></span></td>
    <td><span data-ttu-id="d763b-198">X</span><span class="sxs-lookup"><span data-stu-id="d763b-198">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="d763b-199">X</span><span class="sxs-lookup"><span data-stu-id="d763b-199">X</span></span></td>
    <td><span data-ttu-id="d763b-200">X</span><span class="sxs-lookup"><span data-stu-id="d763b-200">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="d763b-201">Y</span><span class="sxs-lookup"><span data-stu-id="d763b-201">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="d763b-202">X</span><span class="sxs-lookup"><span data-stu-id="d763b-202">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="d763b-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry Explorer</a></span><span class="sxs-lookup"><span data-stu-id="d763b-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry Explorer</a></span></span></td>
    <td><span data-ttu-id="d763b-204">X</span><span class="sxs-lookup"><span data-stu-id="d763b-204">X</span></span></td>
    <td><span data-ttu-id="d763b-205">X</span><span class="sxs-lookup"><span data-stu-id="d763b-205">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="d763b-206">X</span><span class="sxs-lookup"><span data-stu-id="d763b-206">X</span></span></td>
    <td><span data-ttu-id="d763b-207">Y/N</span><span class="sxs-lookup"><span data-stu-id="d763b-207">Y/N</span></span></td>
    <td></td>
    <td><span data-ttu-id="d763b-208">X</span><span class="sxs-lookup"><span data-stu-id="d763b-208">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="d763b-209"><a href="http://www.gapotchenko.com/cloudcombine">Cloud Combine</a></span><span class="sxs-lookup"><span data-stu-id="d763b-209"><a href="http://www.gapotchenko.com/cloudcombine">Cloud Combine</a></span></span></td>
    <td><span data-ttu-id="d763b-210">X</span><span class="sxs-lookup"><span data-stu-id="d763b-210">X</span></span></td>
    <td><span data-ttu-id="d763b-211">X</span><span class="sxs-lookup"><span data-stu-id="d763b-211">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="d763b-212">X</span><span class="sxs-lookup"><span data-stu-id="d763b-212">X</span></span></td>
    <td><span data-ttu-id="d763b-213">X</span><span class="sxs-lookup"><span data-stu-id="d763b-213">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="d763b-214">평가판</span><span class="sxs-lookup"><span data-stu-id="d763b-214">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="d763b-215">X</span><span class="sxs-lookup"><span data-stu-id="d763b-215">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="d763b-216"><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></span><span class="sxs-lookup"><span data-stu-id="d763b-216"><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></span></span></td>
    <td><span data-ttu-id="d763b-217">X</span><span class="sxs-lookup"><span data-stu-id="d763b-217">X</span></span></td>
    <td><span data-ttu-id="d763b-218">X</span><span class="sxs-lookup"><span data-stu-id="d763b-218">X</span></span></td>
    <td><span data-ttu-id="d763b-219">X</span><span class="sxs-lookup"><span data-stu-id="d763b-219">X</span></span></td>
    <td><span data-ttu-id="d763b-220">X</span><span class="sxs-lookup"><span data-stu-id="d763b-220">X</span></span></td>
    <td><span data-ttu-id="d763b-221">X</span><span class="sxs-lookup"><span data-stu-id="d763b-221">X</span></span></td>
    <td><span data-ttu-id="d763b-222">X</span><span class="sxs-lookup"><span data-stu-id="d763b-222">X</span></span></td>
    <td><span data-ttu-id="d763b-223">Y</span><span class="sxs-lookup"><span data-stu-id="d763b-223">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="d763b-224">X</span><span class="sxs-lookup"><span data-stu-id="d763b-224">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="d763b-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet Cloud</a></span><span class="sxs-lookup"><span data-stu-id="d763b-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet Cloud</a></span></span></td>
    <td><span data-ttu-id="d763b-226">X</span><span class="sxs-lookup"><span data-stu-id="d763b-226">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="d763b-227">평가판</span><span class="sxs-lookup"><span data-stu-id="d763b-227">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="d763b-228">X</span><span class="sxs-lookup"><span data-stu-id="d763b-228">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="d763b-229"><a href="http://storageexplorer.codeplex.com/">Azure Web Storage Explorer</a></span><span class="sxs-lookup"><span data-stu-id="d763b-229"><a href="http://storageexplorer.codeplex.com/">Azure Web Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="d763b-230">X</span><span class="sxs-lookup"><span data-stu-id="d763b-230">X</span></span></td>
    <td><span data-ttu-id="d763b-231">X</span><span class="sxs-lookup"><span data-stu-id="d763b-231">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="d763b-232">X</span><span class="sxs-lookup"><span data-stu-id="d763b-232">X</span></span></td>
    <td><span data-ttu-id="d763b-233">X</span><span class="sxs-lookup"><span data-stu-id="d763b-233">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="d763b-234">Y</span><span class="sxs-lookup"><span data-stu-id="d763b-234">Y</span></span></td>
    <td><span data-ttu-id="d763b-235">X</span><span class="sxs-lookup"><span data-stu-id="d763b-235">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="d763b-236"><a href="https://zudio.co/">Zudio</a></span><span class="sxs-lookup"><span data-stu-id="d763b-236"><a href="https://zudio.co/">Zudio</a></span></span></td>
    <td><span data-ttu-id="d763b-237">X</span><span class="sxs-lookup"><span data-stu-id="d763b-237">X</span></span></td>
    <td><span data-ttu-id="d763b-238">X</span><span class="sxs-lookup"><span data-stu-id="d763b-238">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="d763b-239">X</span><span class="sxs-lookup"><span data-stu-id="d763b-239">X</span></span></td>
    <td><span data-ttu-id="d763b-240">X</span><span class="sxs-lookup"><span data-stu-id="d763b-240">X</span></span></td>
    <td><span data-ttu-id="d763b-241">X</span><span class="sxs-lookup"><span data-stu-id="d763b-241">X</span></span></td>
    <td><span data-ttu-id="d763b-242">평가판</span><span class="sxs-lookup"><span data-stu-id="d763b-242">Trial</span></span></td>
    <td><span data-ttu-id="d763b-243">X</span><span class="sxs-lookup"><span data-stu-id="d763b-243">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>
