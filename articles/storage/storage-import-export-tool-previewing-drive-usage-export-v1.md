---
title: "Azure 가져오기/내보내기 내보내기 작업-v 1의 드라이브 사용 aaaPreviewing | Microsoft Docs"
description: "어떻게 blob toopreview hello 목록 선택한 hello Azure 가져오기/내보내기 서비스에서 내보내기 작업에 대해 알아봅니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 7707d744-7ec7-4de8-ac9b-93a18608dc9a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 88495f921371458c0451da6878fd7cc9a45d20cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a><span data-ttu-id="891f5-103">내보내기 작업에 대한 드라이브 사용량 미리 보기</span><span class="sxs-lookup"><span data-stu-id="891f5-103">Previewing drive usage for an export job</span></span>
<span data-ttu-id="891f5-104">내보내기 작업을 만들기 전에 내보낼 blob toobe 집합이 toochoose를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="891f5-104">Before you create an export job, you need toochoose a set of blobs toobe exported.</span></span> <span data-ttu-id="891f5-105">Microsoft Azure 가져오기/내보내기 서비스 hello 있습니다 toouse blob 경로 목록을 또는 blob 접두사 toorepresent hello blob를 선택 했습니다.</span><span class="sxs-lookup"><span data-stu-id="891f5-105">hello Microsoft Azure Import/Export service allows you toouse a list of blob paths or blob prefixes toorepresent hello blobs you've selected.</span></span>  
  
<span data-ttu-id="891f5-106">다음으로, 해야 toodetermine 드라이브 수 toosend 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="891f5-106">Next, you need toodetermine how many drives you need toosend.</span></span> <span data-ttu-id="891f5-107">가져오기/내보내기 도구 hello 제공 hello `PreviewExport` hello 드라이브의 hello 크기에 따라 보아야 toouse를 선택 하면는 hello blob에 대 한 명령 toopreview 드라이브 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="891f5-107">hello Import/Export Tool provides hello `PreviewExport` command toopreview drive usage for hello blobs you selected, based on hello size of hello drives you are going toouse.</span></span>

## <a name="command-line-parameters"></a><span data-ttu-id="891f5-108">명령줄 매개 변수</span><span class="sxs-lookup"><span data-stu-id="891f5-108">Command-line parameters</span></span>

<span data-ttu-id="891f5-109">Hello hello를 사용 하는 경우 매개 변수 뒤에 사용할 수 있습니다 `PreviewExport` 의 가져오기/내보내기 도구 hello 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="891f5-109">You can use hello following parameters when using hello `PreviewExport` command of hello Import/Export Tool.</span></span>

|<span data-ttu-id="891f5-110">명령줄 매개 변수</span><span class="sxs-lookup"><span data-stu-id="891f5-110">Command-line parameter</span></span>|<span data-ttu-id="891f5-111">설명</span><span class="sxs-lookup"><span data-stu-id="891f5-111">Description</span></span>|  
|--------------------------|-----------------|  
|<span data-ttu-id="891f5-112">**/logdir:**<LogDirectory\></span><span class="sxs-lookup"><span data-stu-id="891f5-112">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="891f5-113">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="891f5-113">Optional.</span></span> <span data-ttu-id="891f5-114">hello 로그 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="891f5-114">hello log directory.</span></span> <span data-ttu-id="891f5-115">자세한 로그 파일 디렉터리 toothis 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="891f5-115">Verbose log files will be written toothis directory.</span></span> <span data-ttu-id="891f5-116">없는 로그 디렉터리를 지정 하는 경우 현재 디렉터리 hello hello 로그 디렉터리로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="891f5-116">If no log directory is specified, hello current directory will be used as hello log directory.</span></span>|  
|<span data-ttu-id="891f5-117">**/sn:**<StorageAccountName\></span><span class="sxs-lookup"><span data-stu-id="891f5-117">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="891f5-118">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="891f5-118">Required.</span></span> <span data-ttu-id="891f5-119">hello hello 저장소 계정의 이름으로 hello에 대 한 내보내기 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="891f5-119">hello name of hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="891f5-120">**/sk:**<StorageAccountKey\></span><span class="sxs-lookup"><span data-stu-id="891f5-120">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="891f5-121">컨테이너 SAS가 지정되지 않은 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="891f5-121">Required if and only if a container SAS is not specified.</span></span> <span data-ttu-id="891f5-122">hello에 대 한 hello 저장소 계정에 대 한 hello 계정 키 내보내기 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="891f5-122">hello account key for hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="891f5-123">**/csas:**<ContainerSas\></span><span class="sxs-lookup"><span data-stu-id="891f5-123">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="891f5-124">저장소 계정 키가 지정되지 않은 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="891f5-124">Required if and only if a storage account key is not specified.</span></span> <span data-ttu-id="891f5-125">hello blob toobe 목록에 대 한 hello 컨테이너 SAS hello 내보내기 작업에서 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="891f5-125">hello container SAS for listing hello blobs toobe exported in hello export job.</span></span>|  
|<span data-ttu-id="891f5-126">**/ExportBlobListFile:**<ExportBlobListFile\></span><span class="sxs-lookup"><span data-stu-id="891f5-126">**/ExportBlobListFile:**<ExportBlobListFile\></span></span>|<span data-ttu-id="891f5-127">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="891f5-127">Required.</span></span> <span data-ttu-id="891f5-128">경로 toohello XML blob 경로 목록을 포함 파일 접두사 또는 blob 경로 hello blob toobe 내보낸에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="891f5-128">Path toohello XML file containing list of blob paths or blob path prefixes for hello blobs toobe exported.</span></span> <span data-ttu-id="891f5-129">hello에 사용 되는 hello 파일 형식 `BlobListBlobPath` hello 요소 [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) hello 가져오기/내보내기 서비스 REST API의 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="891f5-129">hello file format used in hello `BlobListBlobPath` element in hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation of hello Import/Export service REST API.</span></span>|  
|<span data-ttu-id="891f5-130">**/DriveSize:**<DriveSize\></span><span class="sxs-lookup"><span data-stu-id="891f5-130">**/DriveSize:**<DriveSize\></span></span>|<span data-ttu-id="891f5-131">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="891f5-131">Required.</span></span> <span data-ttu-id="891f5-132">내보내기 작업에 대 한 드라이브 toouse의 크기를 hello *예:*, 500GB, 1.5 t B.</span><span class="sxs-lookup"><span data-stu-id="891f5-132">hello size of drives toouse for an export job, *e.g.*, 500GB, 1.5TB.</span></span>|  

## <a name="command-line-example"></a><span data-ttu-id="891f5-133">명령줄 예제</span><span class="sxs-lookup"><span data-stu-id="891f5-133">Command-line example</span></span>

<span data-ttu-id="891f5-134">hello 다음 예제에서는 hello `PreviewExport` 명령:</span><span class="sxs-lookup"><span data-stu-id="891f5-134">hello following example demonstrates hello `PreviewExport` command:</span></span>  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
<span data-ttu-id="891f5-135">hello blob 목록 내보내기 파일 수 blob 이름이 포함 및 blob 접두사를 다음과 같이:</span><span class="sxs-lookup"><span data-stu-id="891f5-135">hello export blob list file may contain blob names and blob prefixes, as shown here:</span></span>  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

<span data-ttu-id="891f5-136">hello Azure 가져오기/내보내기 도구는 내보낼 모든 blob toobe를 나열 하 고 어떻게 toopack hello의 드라이브에 지정 된 크기, 필요한 오버 헤드를 고려 hello 드라이브 수를 예측 합니다 임의 toohold hello blob 및 드라이브 사용을 계산 합니다. 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="891f5-136">hello Azure Import/Export Tool lists all blobs toobe exported and calculates how toopack them into drives of hello specified size, taking into account any necessary overhead, then estimates hello number of drives needed toohold hello blobs and drive usage information.</span></span>  
  
<span data-ttu-id="891f5-137">다음은 정보 로그가 생략 된 hello 출력의 예가입니다.</span><span class="sxs-lookup"><span data-stu-id="891f5-137">Here is an example of hello output, with informational logs omitted:</span></span>  
  
```  
Number of unique blob paths/prefixes:   3  
Number of duplicate blob paths/prefixes:        0  
Number of nonexistent blob paths/prefixes:      1  
  
Drive size:     500.00 GB  
Number of blobs that can be exported:   6  
Number of blobs that cannot be exported:        2  
Number of drives needed:        3  
        Drive #1:       blobs = 1, occupied space = 454.74 GB  
        Drive #2:       blobs = 3, occupied space = 441.37 GB  
        Drive #3:       blobs = 2, occupied space = 131.28 GB    
```  
  
## <a name="next-steps"></a><span data-ttu-id="891f5-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="891f5-138">Next steps</span></span>

* [<span data-ttu-id="891f5-139">Azure Import/Export 도구 참조</span><span class="sxs-lookup"><span data-stu-id="891f5-139">Azure Import/Export Tool reference</span></span>](storage-import-export-tool-how-to-v1.md)
