---
title: ".NET을 사용 하 여 aaaAzure 저장소 샘플 | Microsoft Docs"
description: "Azure 저장소에 대한 샘플 코드 및 응용 프로그램을 확인하고 다운로드하여 실행합니다. Hello.NET 저장소 클라이언트 라이브러리를 사용 하 여 blob, 큐, 테이블 및 파일에 대 한 샘플 시작을 검색 합니다."
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: 9a7055645b0f0658b850f024b8b19ab19840330e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-net"></a><span data-ttu-id="e4743-104">.NET을 사용한 Azure Storage 샘플</span><span class="sxs-lookup"><span data-stu-id="e4743-104">Azure Storage samples using .NET</span></span>

## <a name="net-sample-index"></a><span data-ttu-id="e4743-105">.NET 샘플 인덱스</span><span class="sxs-lookup"><span data-stu-id="e4743-105">.NET sample index</span></span>

<span data-ttu-id="e4743-106">hello 다음 표에 간략하게 샘플 리포지토리 및 hello 시나리오 각 샘플에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4743-106">hello following table provides an overview of our samples repository and hello scenarios covered in each sample.</span></span> <span data-ttu-id="e4743-107">Hello 링크 tooview hello 해당 샘플 코드에 GitHub에서 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4743-107">Click on hello links tooview hello corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="e4743-108">끝점</span><span class="sxs-lookup"><span data-stu-id="e4743-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="e4743-109">시나리오</span><span class="sxs-lookup"><span data-stu-id="e4743-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="e4743-110">샘플 코드</span><span class="sxs-lookup"><span data-stu-id="e4743-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="e4743-111"><b>Blob</b></span><span class="sxs-lookup"><span data-stu-id="e4743-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="e4743-112">Blob 추가</span><span class="sxs-lookup"><span data-stu-id="e4743-112">Append Blob</span></span></td> 
<td><span data-ttu-id="e4743-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference 메서드 예제</a></span><span class="sxs-lookup"><span data-stu-id="e4743-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference Method Example</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e4743-114">블록 Blob</span><span class="sxs-lookup"><span data-stu-id="e4743-114">Block Blob</span></span></td>
<td><span data-ttu-id="e4743-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob 저장소 사진 갤러리 웹 응용 프로그램</a></span><span class="sxs-lookup"><span data-stu-id="e4743-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e4743-116">클라이언트 쪽 암호화</span><span class="sxs-lookup"><span data-stu-id="e4743-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="e4743-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">BLOB 암호화 샘플</a></span><span class="sxs-lookup"><span data-stu-id="e4743-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Blob Encryption Samples</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e4743-118">Blob 복사</span><span class="sxs-lookup"><span data-stu-id="e4743-118">Copy Blob</span></span></td>
<td><span data-ttu-id="e4743-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">BLOB 시작</a></span><span class="sxs-lookup"><span data-stu-id="e4743-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e4743-120">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="e4743-120">Create Container</span></span></td>
<td><span data-ttu-id="e4743-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob 저장소 사진 갤러리 웹 응용 프로그램</a></span><span class="sxs-lookup"><span data-stu-id="e4743-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e4743-122">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="e4743-122">Delete Blob</span></span></td>
<td><span data-ttu-id="e4743-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob 저장소 사진 갤러리 웹 응용 프로그램</a></span><span class="sxs-lookup"><span data-stu-id="e4743-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e4743-124">컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="e4743-124">Delete Container</span></span></td>
<td><span data-ttu-id="e4743-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">BLOB 시작</a></span><span class="sxs-lookup"><span data-stu-id="e4743-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e4743-126">BLOB 메타데이터/속성/통계</span><span class="sxs-lookup"><span data-stu-id="e4743-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="e4743-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">BLOB 시작</a></span><span class="sxs-lookup"><span data-stu-id="e4743-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e4743-128">컨테이너 ACL/메타데이터/속성</span><span class="sxs-lookup"><span data-stu-id="e4743-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="e4743-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob 저장소 사진 갤러리 웹 응용 프로그램</a></span><span class="sxs-lookup"><span data-stu-id="e4743-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e4743-130">페이지 범위 가져오기</span><span class="sxs-lookup"><span data-stu-id="e4743-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="e4743-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">BLOB 시작</a></span><span class="sxs-lookup"><span data-stu-id="e4743-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e4743-132">BLOB/컨테이너 임대</span><span class="sxs-lookup"><span data-stu-id="e4743-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="e4743-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">BLOB 시작</a></span><span class="sxs-lookup"><span data-stu-id="e4743-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e4743-134">BLOB/컨테이너 나열</span><span class="sxs-lookup"><span data-stu-id="e4743-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="e4743-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">BLOB 시작</a></span><span class="sxs-lookup"><span data-stu-id="e4743-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e4743-136">페이지 Blob</span><span class="sxs-lookup"><span data-stu-id="e4743-136">Page Blob</span></span></td>
<td><span data-ttu-id="e4743-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">BLOB 시작</a></span><span class="sxs-lookup"><span data-stu-id="e4743-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="e4743-138">SAS</span><span class="sxs-lookup"><span data-stu-id="e4743-138">SAS</span></span></td>
<td><span data-ttu-id="e4743-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">BLOB 시작</a></span><span class="sxs-lookup"><span data-stu-id="e4743-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="e4743-140">서비스 속성</span><span class="sxs-lookup"><span data-stu-id="e4743-140">Service Properties</span></span></td>
<td><span data-ttu-id="e4743-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">BLOB 시작</a></span><span class="sxs-lookup"><span data-stu-id="e4743-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="e4743-142">Blob 스냅숏</span><span class="sxs-lookup"><span data-stu-id="e4743-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="e4743-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">증분 스냅숏을 사용하여 Azure 가상 컴퓨터 디스크 백업</a></span><span class="sxs-lookup"><span data-stu-id="e4743-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="e4743-144"><b>파일</b></span><span class="sxs-lookup"><span data-stu-id="e4743-144"><b>File</b></span></span></td>
<td><span data-ttu-id="e4743-145">공유/디렉터리/파일 만들기</span><span class="sxs-lookup"><span data-stu-id="e4743-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="e4743-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage 샘플</a></span><span class="sxs-lookup"><span data-stu-id="e4743-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="e4743-147">공유/디렉터리/파일 삭제</span><span class="sxs-lookup"><span data-stu-id="e4743-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="e4743-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">.NET에서 Azure 파일 서비스 시작</a></span><span class="sxs-lookup"><span data-stu-id="e4743-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e4743-149">디렉터리 속성/메타데이터</span><span class="sxs-lookup"><span data-stu-id="e4743-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="e4743-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage 샘플</a></span><span class="sxs-lookup"><span data-stu-id="e4743-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e4743-151">파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="e4743-151">Download Files</span></span></td> 
<td><span data-ttu-id="e4743-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage 샘플</a></span><span class="sxs-lookup"><span data-stu-id="e4743-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e4743-153">파일 속성/메타데이터/메트릭</span><span class="sxs-lookup"><span data-stu-id="e4743-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="e4743-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage 샘플</a></span><span class="sxs-lookup"><span data-stu-id="e4743-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e4743-155">파일 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="e4743-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="e4743-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage 샘플</a></span><span class="sxs-lookup"><span data-stu-id="e4743-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e4743-157">디렉터리 및 파일 나열</span><span class="sxs-lookup"><span data-stu-id="e4743-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="e4743-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage 샘플</a></span><span class="sxs-lookup"><span data-stu-id="e4743-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="e4743-159">공유 나열</span><span class="sxs-lookup"><span data-stu-id="e4743-159">List Shares</span></span></td> 
<td><span data-ttu-id="e4743-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage 샘플</a></span><span class="sxs-lookup"><span data-stu-id="e4743-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="e4743-161">속성/메타데이터/통계 공유</span><span class="sxs-lookup"><span data-stu-id="e4743-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="e4743-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage 샘플</a></span><span class="sxs-lookup"><span data-stu-id="e4743-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="e4743-163"><b>큐</b></span><span class="sxs-lookup"><span data-stu-id="e4743-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="e4743-164">메시지 추가</span><span class="sxs-lookup"><span data-stu-id="e4743-164">Add Message</span></span></td> 
<td><span data-ttu-id="e4743-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">.NET에서 Azure 큐 서비스 시작</a></span><span class="sxs-lookup"><span data-stu-id="e4743-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e4743-166">클라이언트 쪽 암호화</span><span class="sxs-lookup"><span data-stu-id="e4743-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="e4743-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET 큐 클라이언트 쪽 암호화</a></span><span class="sxs-lookup"><span data-stu-id="e4743-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET Queue Client-Side Encryption</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e4743-168">큐 만들기</span><span class="sxs-lookup"><span data-stu-id="e4743-168">Create Queues</span></span></td> 
<td><span data-ttu-id="e4743-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">.NET에서 Azure 큐 서비스 시작</a></span><span class="sxs-lookup"><span data-stu-id="e4743-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e4743-170">메시지/큐 삭제</span><span class="sxs-lookup"><span data-stu-id="e4743-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="e4743-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">.NET에서 Azure 큐 서비스 시작</a></span><span class="sxs-lookup"><span data-stu-id="e4743-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e4743-172">메시지 보기</span><span class="sxs-lookup"><span data-stu-id="e4743-172">Peek Message</span></span></td> 
<td><span data-ttu-id="e4743-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">.NET에서 Azure 큐 서비스 시작</a></span><span class="sxs-lookup"><span data-stu-id="e4743-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e4743-174">큐 ACL/메타데이터/통계</span><span class="sxs-lookup"><span data-stu-id="e4743-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="e4743-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">.NET에서 Azure 큐 서비스 시작</a></span><span class="sxs-lookup"><span data-stu-id="e4743-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e4743-176">큐 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="e4743-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="e4743-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">.NET에서 Azure 큐 서비스 시작</a></span><span class="sxs-lookup"><span data-stu-id="e4743-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e4743-178">메시지 업데이트</span><span class="sxs-lookup"><span data-stu-id="e4743-178">Update Message</span></span></td> 
<td><span data-ttu-id="e4743-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">.NET에서 Azure 큐 서비스 시작</a></span><span class="sxs-lookup"><span data-stu-id="e4743-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="e4743-180"><b>테이블</b></span><span class="sxs-lookup"><span data-stu-id="e4743-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="e4743-181">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="e4743-181">Create Table</span></span></td> 
<td><span data-ttu-id="e4743-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Azure 저장소를 사용하여 동시성 관리 - 샘플 응용 프로그램</a></span><span class="sxs-lookup"><span data-stu-id="e4743-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e4743-183">엔터티/테이블 삭제</span><span class="sxs-lookup"><span data-stu-id="e4743-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="e4743-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">.NET에서 Azure Table Storage 시작</a></span><span class="sxs-lookup"><span data-stu-id="e4743-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e4743-185">엔터티 삽입/병합/바꾸기</span><span class="sxs-lookup"><span data-stu-id="e4743-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="e4743-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Azure 저장소를 사용하여 동시성 관리 - 샘플 응용 프로그램</a></span><span class="sxs-lookup"><span data-stu-id="e4743-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e4743-187">엔터티 쿼리</span><span class="sxs-lookup"><span data-stu-id="e4743-187">Query Entities</span></span></td> 
<td><span data-ttu-id="e4743-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">.NET에서 Azure Table Storage 시작</a></span><span class="sxs-lookup"><span data-stu-id="e4743-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e4743-189">쿼리 테이블</span><span class="sxs-lookup"><span data-stu-id="e4743-189">Query Tables</span></span></td> 
<td><span data-ttu-id="e4743-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">.NET에서 Azure Table Storage 시작</a></span><span class="sxs-lookup"><span data-stu-id="e4743-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e4743-191">테이블 ACL/속성</span><span class="sxs-lookup"><span data-stu-id="e4743-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="e4743-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">.NET에서 Azure Table Storage 시작</a></span><span class="sxs-lookup"><span data-stu-id="e4743-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e4743-193">엔터티 업데이트</span><span class="sxs-lookup"><span data-stu-id="e4743-193">Update Entity</span></span></td> 
<td><span data-ttu-id="e4743-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Azure 저장소를 사용하여 동시성 관리 - 샘플 응용 프로그램</a></span><span class="sxs-lookup"><span data-stu-id="e4743-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="e4743-195">Azure 코드 샘플 라이브러리</span><span class="sxs-lookup"><span data-stu-id="e4743-195">Azure Code Samples library</span></span>

<span data-ttu-id="e4743-196">tooview hello 전체 예제 라이브러리를 이동 toohello [Azure 코드 예제](https://azure.microsoft.com/resources/samples/?service=storage) 다운로드 하 고 로컬로 실행할 수 있는 Azure 저장소에 대 한 샘플을 포함 하는 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="e4743-196">tooview hello complete sample library, go toohello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="e4743-197">코드 예제 라이브러리 hello.zip 형식에서 샘플 코드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4743-197">hello Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="e4743-198">또는 검색 하 고 각 샘플에 대 한 hello GitHub 리포지토리 복제 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4743-198">Alternatively, you can browse and clone hello GitHub repository for each sample.</span></span>

[!INCLUDE [storage-dotnet-samples-include](../../includes/storage-dotnet-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="e4743-199">시작 가이드</span><span class="sxs-lookup"><span data-stu-id="e4743-199">Getting started guides</span></span>

<span data-ttu-id="e4743-200">체크 아웃 방법에 대 한 원하는 경우 지침을 따라 hello tooinstall 및 Azure 저장소 클라이언트 라이브러리 hello로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4743-200">Check out hello following guides if you are looking for instructions on how tooinstall and get started with hello Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="e4743-201">.NET에서 Azure Blob 서비스 시작</span><span class="sxs-lookup"><span data-stu-id="e4743-201">Getting Started with Azure Blob Service in .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="e4743-202">.NET에서 Azure 큐 서비스 시작</span><span class="sxs-lookup"><span data-stu-id="e4743-202">Getting Started with Azure Queue Service in .NET</span></span>](storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="e4743-203">.NET에서 Azure 테이블 서비스 시작</span><span class="sxs-lookup"><span data-stu-id="e4743-203">Getting Started with Azure Table Service in .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="e4743-204">.NET에서 Azure 파일 서비스 시작</span><span class="sxs-lookup"><span data-stu-id="e4743-204">Getting Started with Azure File Service in .NET</span></span>](storage-dotnet-how-to-use-files.md)

## <a name="next-steps"></a><span data-ttu-id="e4743-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e4743-205">Next steps</span></span>

<span data-ttu-id="e4743-206">다른 언어용 샘플에 대한 정보:</span><span class="sxs-lookup"><span data-stu-id="e4743-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="e4743-207">Java: [Java를 사용한 Azure Storage 샘플](storage-samples-java.md)</span><span class="sxs-lookup"><span data-stu-id="e4743-207">Java: [Azure Storage samples using Java](storage-samples-java.md)</span></span>
* <span data-ttu-id="e4743-208">다른 모든 언어: [Azure Storage 샘플](storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="e4743-208">All other languages: [Azure Storage samples](storage-samples.md)</span></span>
