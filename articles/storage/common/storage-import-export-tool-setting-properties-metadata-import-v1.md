---
title: "aaaSetting 속성 및 메타 데이터 Azure 가져오기/내보내기-v 1을 사용 하 여 | Microsoft Docs"
description: "Hello Azure 가져오기/내보내기 도구 tooprepare 드라이브를 실행할 때 toospecify 속성 및 메타 데이터 toobe hello 대상 blob에 대 한 설정 방법에 대해 알아봅니다. 이 toov1의 hello 가져오기/내보내기 도구를 가리킵니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: e8541695-bcfb-4bf0-84d9-72c9de32a0a8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 5b7b1c346ecde8a26d985bd5de7efcf7d86eb9e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a><span data-ttu-id="9f440-104">속성 설정 및 hello 중에 메타 데이터 가져오기 프로세스</span><span class="sxs-lookup"><span data-stu-id="9f440-104">Setting properties and metadata during hello import process</span></span>
<span data-ttu-id="9f440-105">Microsoft Azure 가져오기/내보내기 도구 tooprepare hello 드라이브를 실행 하면 속성 및 메타 데이터 toobe hello 대상 blob에 대 한 설정에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f440-105">When you run hello Microsoft Azure Import/Export Tool tooprepare your drives, you can specify properties and metadata toobe set on hello destination blobs.</span></span> <span data-ttu-id="9f440-106">다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="9f440-106">Follow these steps:</span></span>  
  
1.  <span data-ttu-id="9f440-107">tooset blob 속성, 속성 이름 및 값을 지정 하는 로컬 컴퓨터에 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f440-107">tooset blob properties, create a text file on your local computer that specifies property names and values.</span></span>  
  
2.  <span data-ttu-id="9f440-108">tooset blob 메타 데이터, 메타 데이터 이름 및 값을 지정 하는 로컬 컴퓨터에 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f440-108">tooset blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>  
  
3.  <span data-ttu-id="9f440-109">Hello 전체 경로 tooone 중 또는 둘 다 이러한 파일 toohello Azure 가져오기/내보내기 도구 hello의 일부로 전달 `PrepImport` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f440-109">Pass hello full path tooone or both of these files toohello Azure Import/Export Tool as part of hello `PrepImport` operation.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="9f440-110">속성 또는 메타데이터 파일을 복사 세션의 일부로 지정하면 해당 복사 세션의 일부로 가져오는 모든 Blob에 대해 해당 속성 또는 메타데이터가 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f440-110">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="9f440-111">가져올 hello blob 중 일부에 대해 toospecify 다양 한 속성이 나 메타 데이터를 원하는 toocreate 별도 세션 다른 속성이 나 메타 데이터 파일을 복사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f440-111">If you want toospecify a different set of properties or metadata for some of hello blobs being imported, you'll need toocreate a separate copy session with different properties or metadata files.</span></span>  
  
## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="9f440-112">텍스트 파일에서 Blob 속성 지정</span><span class="sxs-lookup"><span data-stu-id="9f440-112">Specify Blob Properties in a Text File</span></span>  
<span data-ttu-id="9f440-113">toospecify blob 속성 로컬 텍스트 파일을 만들고으로 요소 및 속성 값을 값으로 속성 이름을 지정 하는 XML을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f440-113">toospecify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="9f440-114">다음은 몇 가지 속성 값을 지정하는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="9f440-114">Here's an example that specifies some property values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="9f440-115">Hello 파일 tooa와 같은 로컬 위치에 저장 `C:\WAImportExport\ImportProperties.txt`합니다.</span><span class="sxs-lookup"><span data-stu-id="9f440-115">Save hello file tooa local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>  
  
## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="9f440-116">텍스트 파일에서 Blob 메타데이터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9f440-116">Specify Blob Metadata in a Text File</span></span>  
<span data-ttu-id="9f440-117">마찬가지로, toospecify blob 메타 데이터, 메타 데이터 이름으로 요소 및 메타 데이터 값을 값으로 지정 하는 로컬 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f440-117">Similarly, toospecify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="9f440-118">다음은 몇 가지 메타데이터 값을 지정하는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="9f440-118">Here's an example that specifies some metadata values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="9f440-119">Hello 파일 tooa와 같은 로컬 위치에 저장 `C:\WAImportExport\ImportMetadata.txt`합니다.</span><span class="sxs-lookup"><span data-stu-id="9f440-119">Save hello file tooa local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>  
  
## <a name="create-a-copy-session-including-hello-properties-or-metadata-files"></a><span data-ttu-id="9f440-120">포함 하 여 복사 세션 hello 속성 또는 메타 데이터 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="9f440-120">Create a Copy Session Including hello Properties or Metadata Files</span></span>  
<span data-ttu-id="9f440-121">Hello Azure 가져오기/내보내기 도구 tooprepare hello 가져오기 작업을 실행 하면 hello를 사용 하 여 hello 명령줄에서 hello 속성 파일을 지정 합니다. `PropertyFile` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="9f440-121">When you run hello Azure Import/Export Tool tooprepare hello import job, specify hello properties file on hello command line using hello `PropertyFile` parameter.</span></span> <span data-ttu-id="9f440-122">Hello를 사용 하 여 hello 명령줄에서 hello 메타 데이터 파일을 지정 `/MetadataFile` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="9f440-122">Specify hello metadata file on hello command line using hello `/MetadataFile` parameter.</span></span> <span data-ttu-id="9f440-123">다음은 두 파일을 지정하는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="9f440-123">Here's an example that specifies both files:</span></span>  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a><span data-ttu-id="9f440-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9f440-124">Next steps</span></span>

* [<span data-ttu-id="9f440-125">가져오기-내보내기 서비스 메타데이터 및 속성 파일 형식</span><span class="sxs-lookup"><span data-stu-id="9f440-125">Import/Export service metadata and properties file format</span></span>](../storage-import-export-file-format-metadata-and-properties.md)
