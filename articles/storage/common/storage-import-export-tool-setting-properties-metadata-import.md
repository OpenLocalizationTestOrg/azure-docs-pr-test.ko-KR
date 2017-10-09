---
title: "aaaSetting 속성 및 메타 데이터를 사용 하 여 Azure 가져오기/내보내기 | Microsoft Docs"
description: "Hello Azure 가져오기/내보내기 도구 tooprepare 드라이브를 실행할 때 toospecify 속성 및 메타 데이터 toobe hello 대상 blob에 대 한 설정 방법에 대해 알아봅니다."
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
ms.openlocfilehash: c763237160f0e4b72ce88fd31e2958994bfe8e50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a><span data-ttu-id="1daed-103">속성 설정 및 hello 중에 메타 데이터 가져오기 프로세스</span><span class="sxs-lookup"><span data-stu-id="1daed-103">Setting properties and metadata during hello import process</span></span>

<span data-ttu-id="1daed-104">Microsoft Azure 가져오기/내보내기 도구 tooprepare hello 드라이브를 실행 하면 속성 및 메타 데이터 toobe hello 대상 blob에 대 한 설정에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1daed-104">When you run hello Microsoft Azure Import/Export Tool tooprepare your drives, you can specify properties and metadata toobe set on hello destination blobs.</span></span> <span data-ttu-id="1daed-105">다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="1daed-105">Follow these steps:</span></span>

1.  <span data-ttu-id="1daed-106">tooset blob 속성, 속성 이름 및 값을 지정 하는 로컬 컴퓨터에 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1daed-106">tooset blob properties, create a text file on your local computer that specifies property names and values.</span></span>
2.  <span data-ttu-id="1daed-107">tooset blob 메타 데이터, 메타 데이터 이름 및 값을 지정 하는 로컬 컴퓨터에 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1daed-107">tooset blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>
3.  <span data-ttu-id="1daed-108">Hello 전체 경로 tooone 중 또는 둘 다 이러한 파일 toohello Azure 가져오기/내보내기 도구 hello의 일부로 전달 `PrepImport` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="1daed-108">Pass hello full path tooone or both of these files toohello Azure Import/Export Tool as part of hello `PrepImport` operation.</span></span>

> [!NOTE]
>  <span data-ttu-id="1daed-109">속성 또는 메타데이터 파일을 복사 세션의 일부로 지정하면 해당 복사 세션의 일부로 가져오는 모든 Blob에 대해 해당 속성 또는 메타데이터가 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1daed-109">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="1daed-110">가져올 hello blob 중 일부에 대해 toospecify 다양 한 속성이 나 메타 데이터를 원하는 toocreate 별도 세션 다른 속성이 나 메타 데이터 파일을 복사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1daed-110">If you want toospecify a different set of properties or metadata for some of hello blobs being imported, you'll need toocreate a separate copy session with different properties or metadata files.</span></span>

## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="1daed-111">텍스트 파일에서 Blob 속성 지정</span><span class="sxs-lookup"><span data-stu-id="1daed-111">Specify blob properties in a text file</span></span>

<span data-ttu-id="1daed-112">toospecify blob 속성 로컬 텍스트 파일을 만들고으로 요소 및 속성 값을 값으로 속성 이름을 지정 하는 XML을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1daed-112">toospecify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="1daed-113">다음은 몇 가지 속성 값을 지정하는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="1daed-113">Here's an example that specifies some property values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

<span data-ttu-id="1daed-114">Hello 파일 tooa와 같은 로컬 위치에 저장 `C:\WAImportExport\ImportProperties.txt`합니다.</span><span class="sxs-lookup"><span data-stu-id="1daed-114">Save hello file tooa local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>

## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="1daed-115">텍스트 파일에서 Blob 메타데이터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1daed-115">Specify blob metadata in a text file</span></span>

<span data-ttu-id="1daed-116">마찬가지로, toospecify blob 메타 데이터, 메타 데이터 이름으로 요소 및 메타 데이터 값을 값으로 지정 하는 로컬 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1daed-116">Similarly, toospecify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="1daed-117">다음은 몇 가지 메타데이터 값을 지정하는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="1daed-117">Here's an example that specifies some metadata values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="1daed-118">Hello 파일 tooa와 같은 로컬 위치에 저장 `C:\WAImportExport\ImportMetadata.txt`합니다.</span><span class="sxs-lookup"><span data-stu-id="1daed-118">Save hello file tooa local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>

## <a name="add-hello-path-tooproperties-and-metadata-files-in-datasetcsv"></a><span data-ttu-id="1daed-119">Dataset.csv에 hello 경로 tooproperties 및 메타 데이터 파일 추가</span><span class="sxs-lookup"><span data-stu-id="1daed-119">Add hello path tooproperties and metadata files in dataset.csv</span></span>

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,https://mystorageaccount.blob.core.windows.net/video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,https://mystorageaccount.blob.core.windows.net/photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,https://mystorageaccount.blob.core.windows.net/music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

## <a name="next-steps"></a><span data-ttu-id="1daed-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1daed-120">Next steps</span></span>

* [<span data-ttu-id="1daed-121">가져오기-내보내기 서비스 메타데이터 및 속성 파일 형식</span><span class="sxs-lookup"><span data-stu-id="1daed-121">Import/Export service metadata and properties file format</span></span>](../storage-import-export-file-format-metadata-and-properties.md)
