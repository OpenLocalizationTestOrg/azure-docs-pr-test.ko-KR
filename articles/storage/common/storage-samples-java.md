---
title: "Java를 사용한 Azure Storage 샘플 | Microsoft Docs"
description: "Azure 저장소에 대한 샘플 코드 및 응용 프로그램을 확인하고 다운로드하여 실행합니다. Java 저장소 클라이언트 라이브러리를 사용하여 BLOB, 큐, 테이블 및 파일에 대한 예제 시작을 검색합니다."
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: fd27e1ac9a773e7b0f5245aa74acdb0521cd098c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-samples-using-java"></a><span data-ttu-id="f015a-104">Java를 사용한 Azure Storage 샘플</span><span class="sxs-lookup"><span data-stu-id="f015a-104">Azure Storage samples using Java</span></span>

## <a name="java-sample-index"></a><span data-ttu-id="f015a-105">Java 샘플 인덱스</span><span class="sxs-lookup"><span data-stu-id="f015a-105">Java sample index</span></span>

<span data-ttu-id="f015a-106">다음 테이블에서는 샘플 리포지토리 및 각 샘플에서 다루는 시나리오에 대한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f015a-106">The following table provides an overview of our samples repository and the scenarios covered in each sample.</span></span> <span data-ttu-id="f015a-107">GitHub에서 해당 샘플 코드를 보려면 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f015a-107">Click on the links to view the corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="f015a-108">끝점</span><span class="sxs-lookup"><span data-stu-id="f015a-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="f015a-109">시나리오</span><span class="sxs-lookup"><span data-stu-id="f015a-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="f015a-110">샘플 코드</span><span class="sxs-lookup"><span data-stu-id="f015a-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="f015a-111"><b>Blob</b></span><span class="sxs-lookup"><span data-stu-id="f015a-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="f015a-112">Blob 추가</span><span class="sxs-lookup"><span data-stu-id="f015a-112">Append Blob</span></span></td> 
<td><span data-ttu-id="f015a-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f015a-114">블록 Blob</span><span class="sxs-lookup"><span data-stu-id="f015a-114">Block Blob</span></span></td>
<td><span data-ttu-id="f015a-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f015a-116">클라이언트 쪽 암호화</span><span class="sxs-lookup"><span data-stu-id="f015a-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="f015a-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Java에서 Azure 클라이언트 쪽 암호화 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Getting Started with Azure Client Side Encryption in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f015a-118">Blob 복사</span><span class="sxs-lookup"><span data-stu-id="f015a-118">Copy Blob</span></span></td>
<td><span data-ttu-id="f015a-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f015a-120">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="f015a-120">Create Container</span></span></td>
<td><span data-ttu-id="f015a-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f015a-122">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="f015a-122">Delete Blob</span></span></td>
<td><span data-ttu-id="f015a-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f015a-124">컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="f015a-124">Delete Container</span></span></td>
<td><span data-ttu-id="f015a-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f015a-126">BLOB 메타데이터/속성/통계</span><span class="sxs-lookup"><span data-stu-id="f015a-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="f015a-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f015a-128">컨테이너 ACL/메타데이터/속성</span><span class="sxs-lookup"><span data-stu-id="f015a-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="f015a-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f015a-130">페이지 범위 가져오기</span><span class="sxs-lookup"><span data-stu-id="f015a-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="f015a-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">페이지 BLOB 테스트 샘플</a></span><span class="sxs-lookup"><span data-stu-id="f015a-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Page Blob Tests Sample</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f015a-132">BLOB/컨테이너 임대</span><span class="sxs-lookup"><span data-stu-id="f015a-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="f015a-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f015a-134">BLOB/컨테이너 나열</span><span class="sxs-lookup"><span data-stu-id="f015a-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="f015a-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="f015a-136">페이지 Blob</span><span class="sxs-lookup"><span data-stu-id="f015a-136">Page Blob</span></span></td>
<td><span data-ttu-id="f015a-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="f015a-138">SAS</span><span class="sxs-lookup"><span data-stu-id="f015a-138">SAS</span></span></td>
<td><span data-ttu-id="f015a-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS 테스트 샘플</a></span><span class="sxs-lookup"><span data-stu-id="f015a-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS Tests Sample</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="f015a-140">서비스 속성</span><span class="sxs-lookup"><span data-stu-id="f015a-140">Service Properties</span></span></td>
<td><span data-ttu-id="f015a-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="f015a-142">Blob 스냅숏</span><span class="sxs-lookup"><span data-stu-id="f015a-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="f015a-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="f015a-144"><b>파일</b></span><span class="sxs-lookup"><span data-stu-id="f015a-144"><b>File</b></span></span></td>
<td><span data-ttu-id="f015a-145">공유/디렉터리/파일 만들기</span><span class="sxs-lookup"><span data-stu-id="f015a-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="f015a-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="f015a-147">공유/디렉터리/파일 삭제</span><span class="sxs-lookup"><span data-stu-id="f015a-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="f015a-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f015a-149">디렉터리 속성/메타데이터</span><span class="sxs-lookup"><span data-stu-id="f015a-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="f015a-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f015a-151">파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="f015a-151">Download Files</span></span></td> 
<td><span data-ttu-id="f015a-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f015a-153">파일 속성/메타데이터/메트릭</span><span class="sxs-lookup"><span data-stu-id="f015a-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="f015a-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f015a-155">파일 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="f015a-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="f015a-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f015a-157">디렉터리 및 파일 나열</span><span class="sxs-lookup"><span data-stu-id="f015a-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="f015a-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="f015a-159">공유 나열</span><span class="sxs-lookup"><span data-stu-id="f015a-159">List Shares</span></span></td> 
<td><span data-ttu-id="f015a-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="f015a-161">속성/메타데이터/통계 공유</span><span class="sxs-lookup"><span data-stu-id="f015a-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="f015a-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="f015a-163"><b>큐</b></span><span class="sxs-lookup"><span data-stu-id="f015a-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="f015a-164">메시지 추가</span><span class="sxs-lookup"><span data-stu-id="f015a-164">Add Message</span></span></td> 
<td><span data-ttu-id="f015a-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java 클라이언트 라이브러리 샘플</a></span><span class="sxs-lookup"><span data-stu-id="f015a-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f015a-166">클라이언트 쪽 암호화</span><span class="sxs-lookup"><span data-stu-id="f015a-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="f015a-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java 클라이언트 라이브러리 샘플</a></span><span class="sxs-lookup"><span data-stu-id="f015a-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f015a-168">큐 만들기</span><span class="sxs-lookup"><span data-stu-id="f015a-168">Create Queues</span></span></td> 
<td><span data-ttu-id="f015a-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java에서 Azure Queue Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f015a-170">메시지/큐 삭제</span><span class="sxs-lookup"><span data-stu-id="f015a-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="f015a-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java에서 Azure Queue Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f015a-172">메시지 보기</span><span class="sxs-lookup"><span data-stu-id="f015a-172">Peek Message</span></span></td> 
<td><span data-ttu-id="f015a-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java에서 Azure Queue Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f015a-174">큐 ACL/메타데이터/통계</span><span class="sxs-lookup"><span data-stu-id="f015a-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="f015a-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Java에서 Azure Queue Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f015a-176">큐 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="f015a-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="f015a-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Java에서 Azure Queue Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f015a-178">메시지 업데이트</span><span class="sxs-lookup"><span data-stu-id="f015a-178">Update Message</span></span></td> 
<td><span data-ttu-id="f015a-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java에서 Azure Queue Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="f015a-180"><b>테이블</b></span><span class="sxs-lookup"><span data-stu-id="f015a-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="f015a-181">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="f015a-181">Create Table</span></span></td> 
<td><span data-ttu-id="f015a-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Java에서 Azure Table Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f015a-183">엔터티/테이블 삭제</span><span class="sxs-lookup"><span data-stu-id="f015a-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="f015a-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Java에서 Azure Table Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f015a-185">엔터티 삽입/병합/바꾸기</span><span class="sxs-lookup"><span data-stu-id="f015a-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="f015a-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java 클라이언트 라이브러리 샘플</a></span><span class="sxs-lookup"><span data-stu-id="f015a-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f015a-187">엔터티 쿼리</span><span class="sxs-lookup"><span data-stu-id="f015a-187">Query Entities</span></span></td> 
<td><span data-ttu-id="f015a-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Java에서 Azure Table Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f015a-189">쿼리 테이블</span><span class="sxs-lookup"><span data-stu-id="f015a-189">Query Tables</span></span></td> 
<td><span data-ttu-id="f015a-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Java에서 Azure Table Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f015a-191">테이블 ACL/속성</span><span class="sxs-lookup"><span data-stu-id="f015a-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="f015a-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Java에서 Azure Table Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="f015a-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="f015a-193">엔터티 업데이트</span><span class="sxs-lookup"><span data-stu-id="f015a-193">Update Entity</span></span></td> 
<td><span data-ttu-id="f015a-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java 클라이언트 라이브러리 샘플</a></span><span class="sxs-lookup"><span data-stu-id="f015a-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="f015a-195">Azure 코드 샘플 라이브러리</span><span class="sxs-lookup"><span data-stu-id="f015a-195">Azure Code Samples library</span></span>

<span data-ttu-id="f015a-196">코드 샘플 라이브러리를 보려면 다운로드하여 로컬로 실행할 수 있는 Azure Storage에 대한 샘플이 포함되어 있는 [Azure 코드 샘플](https://azure.microsoft.com/resources/samples/?service=storage) 라이브러리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f015a-196">To view the complete sample library, go to the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="f015a-197">코드 샘플 라이브러리에서 .zip 형식으로 샘플 코드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f015a-197">The Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="f015a-198">또는 각 샘플에 대한 GitHub 리포지토리를 찾아 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f015a-198">Alternatively, you can browse and clone the GitHub repository for each sample.</span></span>

[!INCLUDE [storage-java-samples-include](../../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="f015a-199">시작 가이드</span><span class="sxs-lookup"><span data-stu-id="f015a-199">Getting started guides</span></span>

<span data-ttu-id="f015a-200">Azure Storage 클라이언트 라이브러리를 설치하고 시작하는 방법에 대한 지침은 찾고 있는 경우 다음 가이드를 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="f015a-200">Check out the following guides if you are looking for instructions on how to install and get started with the Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="f015a-201">Java에서 Azure Blob Service 시작</span><span class="sxs-lookup"><span data-stu-id="f015a-201">Getting Started with Azure Blob Service in Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="f015a-202">Java에서 Azure Queue Service 시작</span><span class="sxs-lookup"><span data-stu-id="f015a-202">Getting Started with Azure Queue Service in Java</span></span>](../storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="f015a-203">Java에서 Azure Table Service 시작</span><span class="sxs-lookup"><span data-stu-id="f015a-203">Getting Started with Azure Table Service in Java</span></span>](../../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="f015a-204">Java에서 Azure File Service 시작</span><span class="sxs-lookup"><span data-stu-id="f015a-204">Getting Started with Azure File Service in Java</span></span>](../storage-java-how-to-use-file-storage.md)

## <a name="next-steps"></a><span data-ttu-id="f015a-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f015a-205">Next steps</span></span>

<span data-ttu-id="f015a-206">다른 언어용 샘플에 대한 정보:</span><span class="sxs-lookup"><span data-stu-id="f015a-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="f015a-207">.NET: [.NET을 사용한 Azure Storage 샘플](../storage-samples-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="f015a-207">.NET: [Azure Storage samples using .NET](../storage-samples-dotnet.md)</span></span>
* <span data-ttu-id="f015a-208">다른 모든 언어: [Azure Storage 샘플](../storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="f015a-208">All other languages: [Azure Storage samples](../storage-samples.md)</span></span>
