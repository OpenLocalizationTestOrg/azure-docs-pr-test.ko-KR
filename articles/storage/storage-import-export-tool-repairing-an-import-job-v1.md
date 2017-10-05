---
title: "Azure Import/Export 가져오기 작업 복구 - v1 | Microsoft Docs"
description: "Azure Import/Export 서비스를 사용하여 생성 및 실행된 가져오기 작업을 복구하는 방법을 알아봅니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: b374eabcbafa6ffe64c639fb6c89be857ecfc221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="repairing-an-import-job"></a><span data-ttu-id="a25f6-103">가져오기 작업 복구</span><span class="sxs-lookup"><span data-stu-id="a25f6-103">Repairing an import job</span></span>
<span data-ttu-id="a25f6-104">Microsoft Azure Import/Export 서비스는 Microsoft Azure Blob Service에 파일 또는 파일의 일부를 복사하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-104">The Microsoft Azure Import/Export service may fail to copy some of your files or parts of a file to the Windows Azure Blob service.</span></span> <span data-ttu-id="a25f6-105">이 오류의 몇 가지 원인은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-105">Some reasons for failures include:</span></span>  
  
-   <span data-ttu-id="a25f6-106">손상된 파일</span><span class="sxs-lookup"><span data-stu-id="a25f6-106">Corrupted files</span></span>  
  
-   <span data-ttu-id="a25f6-107">손상된 드라이브</span><span class="sxs-lookup"><span data-stu-id="a25f6-107">Damaged drives</span></span>  
  
-   <span data-ttu-id="a25f6-108">파일이 전송되는 동안 저장소 계정 키가 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-108">The storage account key changed while the file was being transferred.</span></span>  
  
<span data-ttu-id="a25f6-109">가져오기 작업의 복사 로그 파일을 사용하여 Microsoft Azure Import/Export 도구를 실행할 수 있습니다. 이 도구는 누락된 파일(또는 파일의 일부)을 Microsoft Azure Storage 계정으로 업로드하여 가져오기 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-109">You can run the Microsoft Azure Import/Export Tool with the import job's copy log files, and the tool will upload the missing files (or parts of a file) to your Windows Azure storage account to complete import job.</span></span>  
  
## <a name="repairimport-parameters"></a><span data-ttu-id="a25f6-110">RepairImport 매개 변수</span><span class="sxs-lookup"><span data-stu-id="a25f6-110">RepairImport parameters</span></span>

<span data-ttu-id="a25f6-111">**RepairImport**와 함께 다음 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-111">The following parameters can be specified with **RepairImport**:</span></span> 
  
|||  
|-|-|  
|<span data-ttu-id="a25f6-112">**/r:**<RepairFile\></span><span class="sxs-lookup"><span data-stu-id="a25f6-112">**/r:**<RepairFile\></span></span>|<span data-ttu-id="a25f6-113">**필수**</span><span class="sxs-lookup"><span data-stu-id="a25f6-113">**Required.**</span></span> <span data-ttu-id="a25f6-114">복구의 진행 상황을 추적하고 중단된 복구를 다시 시작할 수 있도록 하는 복구 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-114">Path to the repair file, which tracks the progress of the repair, and allows you to resume an interrupted repair.</span></span> <span data-ttu-id="a25f6-115">각 드라이브에는 하나의 복구 파일만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-115">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="a25f6-116">지정된 드라이브의 복구를 시작할 때 아직 존재하지 않는 복구 파일의 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-116">When you start a repair for a given drive, you will pass in the path to a repair file which does not yet exist.</span></span> <span data-ttu-id="a25f6-117">중단된 복구를 다시 시작하려면 기존 복구 파일의 이름을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-117">To resume an interrupted repair, you should pass in the name of an existing repair file.</span></span> <span data-ttu-id="a25f6-118">대상 드라이브에 해당하는 복구 파일을 항상 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-118">The repair file corresponding to the target drive must always be specified.</span></span>|  
|<span data-ttu-id="a25f6-119">**/logdir:**<LogDirectory\></span><span class="sxs-lookup"><span data-stu-id="a25f6-119">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="a25f6-120">**선택**</span><span class="sxs-lookup"><span data-stu-id="a25f6-120">**Optional.**</span></span> <span data-ttu-id="a25f6-121">로그 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-121">The log directory.</span></span> <span data-ttu-id="a25f6-122">이 디렉터리에 자세한 로그 파일이 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-122">Verbose log files will be written to this directory.</span></span> <span data-ttu-id="a25f6-123">로그 디렉터리를 지정하지 않는 경우 현재 디렉터리가 로그 디렉터리로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-123">If no log directory is specified, the current directory will be used as the log directory.</span></span>|  
|<span data-ttu-id="a25f6-124">**/d:**<TargetDirectories\></span><span class="sxs-lookup"><span data-stu-id="a25f6-124">**/d:**<TargetDirectories\></span></span>|<span data-ttu-id="a25f6-125">**필수**</span><span class="sxs-lookup"><span data-stu-id="a25f6-125">**Required.**</span></span> <span data-ttu-id="a25f6-126">가져온 원본 파일을 포함하는 하나 이상의 세미콜론으로 구분된 디렉터리.</span><span class="sxs-lookup"><span data-stu-id="a25f6-126">One or more semicolon-separated directories that contain the original files that were imported.</span></span> <span data-ttu-id="a25f6-127">가져오기 드라이브도 사용할 수 있으나 원본 파일의 대체 위치를 사용할 수 있는 경우 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-127">The import drive may also be used, but is not required if alternate locations of original files are available.</span></span>|  
|<span data-ttu-id="a25f6-128">**/bk:**<BitLockerKey\></span><span class="sxs-lookup"><span data-stu-id="a25f6-128">**/bk:**<BitLockerKey\></span></span>|<span data-ttu-id="a25f6-129">**선택**</span><span class="sxs-lookup"><span data-stu-id="a25f6-129">**Optional.**</span></span> <span data-ttu-id="a25f6-130">이 도구를 사용하여 원본 파일을 사용할 수 있는 암호화된 드라이브의 잠금을 해제하려면 BitLocker 키를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-130">You should specify the BitLocker key if you want the tool to unlock an encrypted drive where the original files are available.</span></span>|  
|<span data-ttu-id="a25f6-131">**/sn:**<StorageAccountName\></span><span class="sxs-lookup"><span data-stu-id="a25f6-131">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="a25f6-132">**필수**</span><span class="sxs-lookup"><span data-stu-id="a25f6-132">**Required.**</span></span> <span data-ttu-id="a25f6-133">가져오기 작업에 대한 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-133">The name of the storage account for the import job.</span></span>|  
|<span data-ttu-id="a25f6-134">**/sk:**<StorageAccountKey\></span><span class="sxs-lookup"><span data-stu-id="a25f6-134">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="a25f6-135">컨테이너 SAS가 지정되지 않은 경우에만 **필수**입니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-135">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="a25f6-136">가져오기 작업에 대한 저장소 계정의 계정 키입니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-136">The account key for the storage account for the import job.</span></span>|  
|<span data-ttu-id="a25f6-137">**/csas:**<ContainerSas\></span><span class="sxs-lookup"><span data-stu-id="a25f6-137">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="a25f6-138">저장소 계정 키가 지정되지 않은 경우에만 **필수**입니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-138">**Required** if and only if the storage account key is not specified.</span></span> <span data-ttu-id="a25f6-139">가져오기 작업과 연결된 blob에 액세스하기 위한 컨테이너 SAS입니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-139">The container SAS for accessing the blobs associated with the import job.</span></span>|  
|<span data-ttu-id="a25f6-140">**/CopyLogFile:**<DriveCopyLogFile\></span><span class="sxs-lookup"><span data-stu-id="a25f6-140">**/CopyLogFile:**<DriveCopyLogFile\></span></span>|<span data-ttu-id="a25f6-141">**필수**</span><span class="sxs-lookup"><span data-stu-id="a25f6-141">**Required.**</span></span> <span data-ttu-id="a25f6-142">드라이브 복사 로그 파일(자세한 로그 또는 오류 로그)의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-142">Path to the drive copy log file (either verbose log or error log).</span></span> <span data-ttu-id="a25f6-143">이 파일은 Microsoft Azure Import/Export 서비스에 의해 생성되고 작업과 연결된 Blob Storage에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-143">The file is generated by the Windows Azure Import/Export service and can be downloaded from the blob storage associated with the job.</span></span> <span data-ttu-id="a25f6-144">복사 로그 파일에는 복구해야 하는 실패한 blob 또는 파일에 대한 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-144">The copy log file contains information about failed blobs or files which are to be repaired.</span></span>|  
|<span data-ttu-id="a25f6-145">**/PathMapFile:**<DrivePathMapFile\></span><span class="sxs-lookup"><span data-stu-id="a25f6-145">**/PathMapFile:**<DrivePathMapFile\></span></span>|<span data-ttu-id="a25f6-146">**선택**</span><span class="sxs-lookup"><span data-stu-id="a25f6-146">**Optional.**</span></span> <span data-ttu-id="a25f6-147">같은 작업에서 가져오는 여러 파일이 같은 이름을 갖는 경우 모호성을 해결하기 위해 사용할 수 있는 텍스트 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-147">Path to a text file that can be used to resolve ambiguities if you have multiple files with the same name that you were importing in the same job.</span></span> <span data-ttu-id="a25f6-148">이 도구는 처음 실행될 때 모호한 모든 이름으로 이 파일을 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-148">The first time the tool is run, it can populate this file with all of the ambiguous names.</span></span> <span data-ttu-id="a25f6-149">이 도구를 이후에 실행하면 이 파일이 모호성을 해결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-149">Subsequent runs of the tool will use this file to resolve the ambiguities.</span></span>|  
  
## <a name="using-the-repairimport-command"></a><span data-ttu-id="a25f6-150">RepairImport 명령 사용</span><span class="sxs-lookup"><span data-stu-id="a25f6-150">Using the RepairImport command</span></span>  
<span data-ttu-id="a25f6-151">네트워크를 통해 데이터를 스트리밍하여 가져오기 데이터를 복구하려면 `/d` 매개 변수를 사용하여 가져오는 원본 파일을 포함하는 디렉터리를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-151">To repair import data by streaming the data over the network, you must specify the directories that contain the original files you were importing using the `/d` parameter.</span></span> <span data-ttu-id="a25f6-152">또한 저장소 계정에서 다운로드한 복사 로그 파일도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-152">You must also specify the copy log file that you downloaded from your storage account.</span></span> <span data-ttu-id="a25f6-153">부분적으로 실패한 가져오기 작업을 복구하는 일반적인 명령줄은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-153">A typical command line to repair an import job with partial failures looks like:</span></span>  
  
```  
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log  
```  
  
<span data-ttu-id="a25f6-154">다음은 복사 로그 파일 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-154">The following is an example of a copy log file.</span></span> <span data-ttu-id="a25f6-155">이 경우 가져오기 작업용으로 전송된 드라이브에서 64K의 파일 조각이 손상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-155">In this case, one 64K piece of a file was corrupted on the drive that was shipped for the import job.</span></span> <span data-ttu-id="a25f6-156">이것이 명시된 유일한 문제이므로 작업의 나머지 blob은 성공적으로 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-156">Since this is the only failure indicated, the rest of the blobs in the job were successfully imported.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
 <DriveId>9WM35C2V</DriveId>  
 <Blob Status="CompletedWithErrors">  
 <BlobPath>pictures/animals/koala.jpg</BlobPath>  
 <FilePath>\animals\koala.jpg</FilePath>  
 <Length>163840</Length>  
 <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
 <PageRangeList>  
  <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted" />  
 </PageRangeList>  
 </Blob>  
 <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
<span data-ttu-id="a25f6-157">이 복사 로그가 Azure Import/Export 도구로 전달될 때 도구는 네트워크를 통해 누락된 콘텐츠를 복사하여 이 파일에 대한 가져오기를 완료하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-157">When this copy log is passed to the Azure Import/Export Tool, the tool will try to finish the import for this file by copying the missing contents across the network.</span></span> <span data-ttu-id="a25f6-158">위의 예제에서 도구는 두 디렉터리 `C:\Users\bob\Pictures` 및 `X:\BobBackup\photos` 내에서 원본 파일 `\animals\koala.jpg`를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-158">Following the example above, the tool will look for the original file `\animals\koala.jpg` within the two directories `C:\Users\bob\Pictures` and `X:\BobBackup\photos`.</span></span> <span data-ttu-id="a25f6-159">파일 `C:\Users\bob\Pictures\animals\koala.jpg`가 있는 경우 Azure Import/Export 도구는 해당 blob `http://bobmediaaccount.blob.core.windows.net/pictures/animals/koala.jpg`에 누락된 데이터 범위를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-159">If the file `C:\Users\bob\Pictures\animals\koala.jpg` exists, the Azure Import/Export Tool will copy the missing range of data to the corresponding blob `http://bobmediaaccount.blob.core.windows.net/pictures/animals/koala.jpg`.</span></span>  
  
## <a name="resolving-conflicts-when-using-repairimport"></a><span data-ttu-id="a25f6-160">RepairImport를 사용할 경우의 충돌 해결</span><span class="sxs-lookup"><span data-stu-id="a25f6-160">Resolving conflicts when using RepairImport</span></span>  
<span data-ttu-id="a25f6-161">상황에 따라 이 도구는 파일을 찾을 수 없거나, 파일에 액세스할 수 없거나, 파일 이름이 모호하거나, 파일 내용이 더 이상 올바르지 않는 등의 이유로 인해 필요한 파일을 찾거나 열지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-161">In some situations, the tool may not be able to find or open the necessary file for one of the following reasons: the file could not be found, the file is not accessible, the file name is ambiguous, or the content of the file is no longer correct.</span></span>  
  
<span data-ttu-id="a25f6-162">이 도구가 `\animals\koala.jpg`를 찾으려고 하고 `C:\Users\bob\pictures` 및 `X:\BobBackup\photos`에 해당 이름의 파일이 있는 경우 모호성 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-162">An ambiguous error could occur if the tool is trying to locate `\animals\koala.jpg` and there is a file with that name under both `C:\Users\bob\pictures` and `X:\BobBackup\photos`.</span></span> <span data-ttu-id="a25f6-163">즉, `C:\Users\bob\pictures\animals\koala.jpg` 및 `X:\BobBackup\photos\animals\koala.jpg`가 둘 다 가져오기 작업 드라이브에 존재하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-163">That is, both `C:\Users\bob\pictures\animals\koala.jpg` and `X:\BobBackup\photos\animals\koala.jpg` exist on the import job drives.</span></span>  
  
<span data-ttu-id="a25f6-164">`/PathMapFile` 옵션을 사용하면 이러한 오류를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-164">The `/PathMapFile` option will allow you to resolve these errors.</span></span> <span data-ttu-id="a25f6-165">도구가 제대로 식별할 수 없는 파일 목록에 포함될 파일의 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-165">You can specify the name of the file which will contains the list of files that the tool was not able to correctly identify.</span></span> <span data-ttu-id="a25f6-166">다음은 `9WM35C2V_pathmap.txt`를 채우는 예제 명령줄입니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-166">The following is an example command line that would populate `9WM35C2V_pathmap.txt`:</span></span>  
  
```
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log /PathMapFile:C:\WAImportExport\9WM35C2V_pathmap.txt  
```
  
<span data-ttu-id="a25f6-167">도구는 문제가 있는 `9WM35C2V_pathmap.txt`의 파일 경로를 한 줄에 하나씩 씁니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-167">The tool will then write the problematic file paths to `9WM35C2V_pathmap.txt`, one on each line.</span></span> <span data-ttu-id="a25f6-168">예를 들어 이 명령을 실행하면 파일에 다음 항목이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-168">For instance, the file may contain the following entries after running the command:</span></span>  
 
```
\animals\koala.jpg  
\animals\kangaroo.jpg  
```
  
 <span data-ttu-id="a25f6-169">목록의 각 파일에 대해 도구에서 사용할 수 있는 파일을 찾아서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-169">For each file in the list, you should attempt to locate and open the file to ensure it is available to the tool.</span></span> <span data-ttu-id="a25f6-170">명시적으로 도구에 파일을 찾을 위치를 지정하려면 경로 맵 파일을 수정하고 같은 줄에 탭 문자로 구분해서 각 파일의 경로를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-170">If you wish to tell the tool explicitly where to find a file, you can modify the path map file and add the path to each file on the same line, separated by a tab character:</span></span>  
  
```
\animals\koala.jpg           C:\Users\bob\Pictures\animals\koala.jpg  
\animals\kangaroo.jpg        X:\BobBackup\photos\animals\kangaroo.jpg  
```
  
<span data-ttu-id="a25f6-171">도구에서 필요한 파일을 사용할 수 있게 만들거나 경로 맵 파일을 업데이트한 후에 도구를 다시 실행하여 가져오기 프로세스를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a25f6-171">After making the necessary files available to the tool, or updating the path map file, you can rerun the tool to complete the import process.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="a25f6-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a25f6-172">Next steps</span></span>
 
* [<span data-ttu-id="a25f6-173">Azure Import/Export 도구 설정</span><span class="sxs-lookup"><span data-stu-id="a25f6-173">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="a25f6-174">가져오기 작업을 위한 하드 드라이브 준비</span><span class="sxs-lookup"><span data-stu-id="a25f6-174">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="a25f6-175">복사 로그 파일을 사용하여 작업 상태 검토</span><span class="sxs-lookup"><span data-stu-id="a25f6-175">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="a25f6-176">내보내기 작업 복구</span><span class="sxs-lookup"><span data-stu-id="a25f6-176">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)   
* [<span data-ttu-id="a25f6-177">Azure Import/Export 도구 문제 해결</span><span class="sxs-lookup"><span data-stu-id="a25f6-177">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
