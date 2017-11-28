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
ms.openlocfilehash: 98e6022062b4ef5b5c71b54a0e94775b925d216b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-samples-using-java"></a><span data-ttu-id="1b513-104">Java를 사용한 Azure Storage 샘플</span><span class="sxs-lookup"><span data-stu-id="1b513-104">Azure Storage samples using Java</span></span>

## <a name="java-sample-index"></a><span data-ttu-id="1b513-105">Java 샘플 인덱스</span><span class="sxs-lookup"><span data-stu-id="1b513-105">Java sample index</span></span>

<span data-ttu-id="1b513-106">다음 테이블에서는 샘플 리포지토리 및 각 샘플에서 다루는 시나리오에 대한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1b513-106">The following table provides an overview of our samples repository and the scenarios covered in each sample.</span></span> <span data-ttu-id="1b513-107">GitHub에서 해당 샘플 코드를 보려면 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b513-107">Click on the links to view the corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="1b513-108">끝점</span><span class="sxs-lookup"><span data-stu-id="1b513-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="1b513-109">시나리오</span><span class="sxs-lookup"><span data-stu-id="1b513-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="1b513-110">샘플 코드</span><span class="sxs-lookup"><span data-stu-id="1b513-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="1b513-111"><b>Blob</b></span><span class="sxs-lookup"><span data-stu-id="1b513-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="1b513-112">Blob 추가</span><span class="sxs-lookup"><span data-stu-id="1b513-112">Append Blob</span></span></td> 
<td><span data-ttu-id="1b513-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1b513-114">블록 Blob</span><span class="sxs-lookup"><span data-stu-id="1b513-114">Block Blob</span></span></td>
<td><span data-ttu-id="1b513-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="1b513-116">클라이언트 쪽 암호화</span><span class="sxs-lookup"><span data-stu-id="1b513-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="1b513-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Java에서 Azure 클라이언트 쪽 암호화 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Getting Started with Azure Client Side Encryption in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="1b513-118">Blob 복사</span><span class="sxs-lookup"><span data-stu-id="1b513-118">Copy Blob</span></span></td>
<td><span data-ttu-id="1b513-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="1b513-120">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="1b513-120">Create Container</span></span></td>
<td><span data-ttu-id="1b513-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="1b513-122">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="1b513-122">Delete Blob</span></span></td>
<td><span data-ttu-id="1b513-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="1b513-124">컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="1b513-124">Delete Container</span></span></td>
<td><span data-ttu-id="1b513-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="1b513-126">BLOB 메타데이터/속성/통계</span><span class="sxs-lookup"><span data-stu-id="1b513-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="1b513-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="1b513-128">컨테이너 ACL/메타데이터/속성</span><span class="sxs-lookup"><span data-stu-id="1b513-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="1b513-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="1b513-130">페이지 범위 가져오기</span><span class="sxs-lookup"><span data-stu-id="1b513-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="1b513-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">페이지 BLOB 테스트 샘플</a></span><span class="sxs-lookup"><span data-stu-id="1b513-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Page Blob Tests Sample</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="1b513-132">BLOB/컨테이너 임대</span><span class="sxs-lookup"><span data-stu-id="1b513-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="1b513-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="1b513-134">BLOB/컨테이너 나열</span><span class="sxs-lookup"><span data-stu-id="1b513-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="1b513-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="1b513-136">페이지 Blob</span><span class="sxs-lookup"><span data-stu-id="1b513-136">Page Blob</span></span></td>
<td><span data-ttu-id="1b513-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="1b513-138">SAS</span><span class="sxs-lookup"><span data-stu-id="1b513-138">SAS</span></span></td>
<td><span data-ttu-id="1b513-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS 테스트 샘플</a></span><span class="sxs-lookup"><span data-stu-id="1b513-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS Tests Sample</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="1b513-140">서비스 속성</span><span class="sxs-lookup"><span data-stu-id="1b513-140">Service Properties</span></span></td>
<td><span data-ttu-id="1b513-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="1b513-142">Blob 스냅숏</span><span class="sxs-lookup"><span data-stu-id="1b513-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="1b513-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java에서 Azure Blob Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="1b513-144"><b>파일</b></span><span class="sxs-lookup"><span data-stu-id="1b513-144"><b>File</b></span></span></td>
<td><span data-ttu-id="1b513-145">공유/디렉터리/파일 만들기</span><span class="sxs-lookup"><span data-stu-id="1b513-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="1b513-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="1b513-147">공유/디렉터리/파일 삭제</span><span class="sxs-lookup"><span data-stu-id="1b513-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="1b513-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1b513-149">디렉터리 속성/메타데이터</span><span class="sxs-lookup"><span data-stu-id="1b513-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="1b513-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1b513-151">파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="1b513-151">Download Files</span></span></td> 
<td><span data-ttu-id="1b513-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1b513-153">파일 속성/메타데이터/메트릭</span><span class="sxs-lookup"><span data-stu-id="1b513-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="1b513-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1b513-155">파일 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="1b513-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="1b513-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1b513-157">디렉터리 및 파일 나열</span><span class="sxs-lookup"><span data-stu-id="1b513-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="1b513-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="1b513-159">공유 나열</span><span class="sxs-lookup"><span data-stu-id="1b513-159">List Shares</span></span></td> 
<td><span data-ttu-id="1b513-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="1b513-161">속성/메타데이터/통계 공유</span><span class="sxs-lookup"><span data-stu-id="1b513-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="1b513-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java에서 Azure File Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="1b513-163"><b>큐</b></span><span class="sxs-lookup"><span data-stu-id="1b513-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="1b513-164">메시지 추가</span><span class="sxs-lookup"><span data-stu-id="1b513-164">Add Message</span></span></td> 
<td><span data-ttu-id="1b513-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java 클라이언트 라이브러리 샘플</a></span><span class="sxs-lookup"><span data-stu-id="1b513-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1b513-166">클라이언트 쪽 암호화</span><span class="sxs-lookup"><span data-stu-id="1b513-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="1b513-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java 클라이언트 라이브러리 샘플</a></span><span class="sxs-lookup"><span data-stu-id="1b513-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1b513-168">큐 만들기</span><span class="sxs-lookup"><span data-stu-id="1b513-168">Create Queues</span></span></td> 
<td><span data-ttu-id="1b513-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java에서 Azure Queue Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1b513-170">메시지/큐 삭제</span><span class="sxs-lookup"><span data-stu-id="1b513-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="1b513-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java에서 Azure Queue Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1b513-172">메시지 보기</span><span class="sxs-lookup"><span data-stu-id="1b513-172">Peek Message</span></span></td> 
<td><span data-ttu-id="1b513-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java에서 Azure Queue Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1b513-174">큐 ACL/메타데이터/통계</span><span class="sxs-lookup"><span data-stu-id="1b513-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="1b513-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Java에서 Azure Queue Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1b513-176">큐 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="1b513-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="1b513-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Java에서 Azure Queue Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1b513-178">메시지 업데이트</span><span class="sxs-lookup"><span data-stu-id="1b513-178">Update Message</span></span></td> 
<td><span data-ttu-id="1b513-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java에서 Azure Queue Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="1b513-180"><b>테이블</b></span><span class="sxs-lookup"><span data-stu-id="1b513-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="1b513-181">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="1b513-181">Create Table</span></span></td> 
<td><span data-ttu-id="1b513-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Java에서 Azure Table Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1b513-183">엔터티/테이블 삭제</span><span class="sxs-lookup"><span data-stu-id="1b513-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="1b513-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Java에서 Azure Table Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1b513-185">엔터티 삽입/병합/바꾸기</span><span class="sxs-lookup"><span data-stu-id="1b513-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="1b513-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java 클라이언트 라이브러리 샘플</a></span><span class="sxs-lookup"><span data-stu-id="1b513-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1b513-187">엔터티 쿼리</span><span class="sxs-lookup"><span data-stu-id="1b513-187">Query Entities</span></span></td> 
<td><span data-ttu-id="1b513-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Java에서 Azure Table Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1b513-189">쿼리 테이블</span><span class="sxs-lookup"><span data-stu-id="1b513-189">Query Tables</span></span></td> 
<td><span data-ttu-id="1b513-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Java에서 Azure Table Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1b513-191">테이블 ACL/속성</span><span class="sxs-lookup"><span data-stu-id="1b513-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="1b513-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Java에서 Azure Table Service 시작</a></span><span class="sxs-lookup"><span data-stu-id="1b513-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1b513-193">엔터티 업데이트</span><span class="sxs-lookup"><span data-stu-id="1b513-193">Update Entity</span></span></td> 
<td><span data-ttu-id="1b513-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java 클라이언트 라이브러리 샘플</a></span><span class="sxs-lookup"><span data-stu-id="1b513-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="1b513-195">Azure 코드 샘플 라이브러리</span><span class="sxs-lookup"><span data-stu-id="1b513-195">Azure Code Samples library</span></span>

<span data-ttu-id="1b513-196">코드 샘플 라이브러리를 보려면 다운로드하여 로컬로 실행할 수 있는 Azure Storage에 대한 샘플이 포함되어 있는 [Azure 코드 샘플](https://azure.microsoft.com/resources/samples/?service=storage) 라이브러리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1b513-196">To view the complete sample library, go to the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="1b513-197">코드 샘플 라이브러리에서 .zip 형식으로 샘플 코드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1b513-197">The Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="1b513-198">또는 각 샘플에 대한 GitHub 리포지토리를 찾아 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b513-198">Alternatively, you can browse and clone the GitHub repository for each sample.</span></span>

[!INCLUDE [storage-java-samples-include](../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="1b513-199">시작 가이드</span><span class="sxs-lookup"><span data-stu-id="1b513-199">Getting started guides</span></span>

<span data-ttu-id="1b513-200">Azure Storage 클라이언트 라이브러리를 설치하고 시작하는 방법에 대한 지침은 찾고 있는 경우 다음 가이드를 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="1b513-200">Check out the following guides if you are looking for instructions on how to install and get started with the Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="1b513-201">Java에서 Azure Blob Service 시작</span><span class="sxs-lookup"><span data-stu-id="1b513-201">Getting Started with Azure Blob Service in Java</span></span>](storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="1b513-202">Java에서 Azure Queue Service 시작</span><span class="sxs-lookup"><span data-stu-id="1b513-202">Getting Started with Azure Queue Service in Java</span></span>](storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="1b513-203">Java에서 Azure Table Service 시작</span><span class="sxs-lookup"><span data-stu-id="1b513-203">Getting Started with Azure Table Service in Java</span></span>](storage-java-how-to-use-table-storage.md)
* [<span data-ttu-id="1b513-204">Java에서 Azure File Service 시작</span><span class="sxs-lookup"><span data-stu-id="1b513-204">Getting Started with Azure File Service in Java</span></span>](storage-java-how-to-use-file-storage.md)

## <a name="next-steps"></a><span data-ttu-id="1b513-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1b513-205">Next steps</span></span>

<span data-ttu-id="1b513-206">다른 언어용 샘플에 대한 정보:</span><span class="sxs-lookup"><span data-stu-id="1b513-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="1b513-207">.NET: [.NET을 사용한 Azure Storage 샘플](storage-samples-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="1b513-207">.NET: [Azure Storage samples using .NET](storage-samples-dotnet.md)</span></span>
* <span data-ttu-id="1b513-208">다른 모든 언어: [Azure Storage 샘플](storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="1b513-208">All other languages: [Azure Storage samples](storage-samples.md)</span></span>
