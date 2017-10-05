---
title: "Azure Import/Export를 사용하여 속성 및 메타데이터 설정 | Microsoft Docs"
description: "Azure Import/Export 도구를 실행하여 드라이브를 준비할 때 대상 BLOB에 설정할 속성과 메타데이터를 지정하는 방법을 알아봅니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: bdc7a53f82d1fbbb726e2b1bd5d96678a8563566
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="setting-properties-and-metadata-during-the-import-process"></a><span data-ttu-id="7911d-103">가져오기 프로세스 중에 속성 및 메타데이터 설정</span><span class="sxs-lookup"><span data-stu-id="7911d-103">Setting properties and metadata during the import process</span></span>

<span data-ttu-id="7911d-104">Microsoft Azure Import/Export 도구를 실행하여 드라이브를 준비할 때 대상 BLOB에 설정할 속성과 메타데이터를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7911d-104">When you run the Microsoft Azure Import/Export Tool to prepare your drives, you can specify properties and metadata to be set on the destination blobs.</span></span> <span data-ttu-id="7911d-105">다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="7911d-105">Follow these steps:</span></span>

1.  <span data-ttu-id="7911d-106">Blob 속성을 설정하려면 속성 이름 및 값을 지정하는 텍스트 파일을 로컬 컴퓨터에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7911d-106">To set blob properties, create a text file on your local computer that specifies property names and values.</span></span>
2.  <span data-ttu-id="7911d-107">Blob 메타데이터를 설정하려면 메타데이터 이름 및 값을 지정하는 텍스트 파일을 로컬 컴퓨터에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7911d-107">To set blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>
3.  <span data-ttu-id="7911d-108">이러한 파일 중 하나 또는 둘 모두의 전체 경로를 `PrepImport` 작업의 일부로 Azure Import/Export 도구에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="7911d-108">Pass the full path to one or both of these files to the Azure Import/Export Tool as part of the `PrepImport` operation.</span></span>

> [!NOTE]
>  <span data-ttu-id="7911d-109">속성 또는 메타데이터 파일을 복사 세션의 일부로 지정하면 해당 복사 세션의 일부로 가져오는 모든 Blob에 대해 해당 속성 또는 메타데이터가 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7911d-109">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="7911d-110">가져올 일부 Blob에 대해 다른 속성 또는 메타데이터 집합을 지정하려면 다른 속성이나 메타데이터 파일을 사용하여 별도의 복사 세션을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7911d-110">If you want to specify a different set of properties or metadata for some of the blobs being imported, you'll need to create a separate copy session with different properties or metadata files.</span></span>

## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="7911d-111">텍스트 파일에서 Blob 속성 지정</span><span class="sxs-lookup"><span data-stu-id="7911d-111">Specify blob properties in a text file</span></span>

<span data-ttu-id="7911d-112">Blob 속성을 지정하려면 로컬 텍스트 파일을 만들고 속성 이름을 요소로, 속성 값을 값으로 지정하는 XML을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7911d-112">To specify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="7911d-113">다음은 몇 가지 속성 값을 지정하는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="7911d-113">Here's an example that specifies some property values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

<span data-ttu-id="7911d-114">`C:\WAImportExport\ImportProperties.txt` 같은 로컬 위치에 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7911d-114">Save the file to a local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>

## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="7911d-115">텍스트 파일에서 Blob 메타데이터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7911d-115">Specify blob metadata in a text file</span></span>

<span data-ttu-id="7911d-116">마찬가지로 Blob 메타데이터를 지정하려면 메타데이터 이름을 요소로, 메타데이터 값을 값으로 지정하는 로컬 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7911d-116">Similarly, to specify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="7911d-117">다음은 몇 가지 메타데이터 값을 지정하는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="7911d-117">Here's an example that specifies some metadata values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="7911d-118">`C:\WAImportExport\ImportMetadata.txt` 같은 로컬 위치에 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7911d-118">Save the file to a local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>

## <a name="add-the-path-to-properties-and-metadata-files-in-datasetcsv"></a><span data-ttu-id="7911d-119">dataset.csv의 속성 및 메타데이터 파일에 경로 추가</span><span class="sxs-lookup"><span data-stu-id="7911d-119">Add the path to properties and metadata files in dataset.csv</span></span>

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,https://mystorageaccount.blob.core.windows.net/video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,https://mystorageaccount.blob.core.windows.net/photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,https://mystorageaccount.blob.core.windows.net/music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

## <a name="next-steps"></a><span data-ttu-id="7911d-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7911d-120">Next steps</span></span>

* [<span data-ttu-id="7911d-121">가져오기-내보내기 서비스 메타데이터 및 속성 파일 형식</span><span class="sxs-lookup"><span data-stu-id="7911d-121">Import/Export service metadata and properties file format</span></span>](storage-import-export-file-format-metadata-and-properties.md)
