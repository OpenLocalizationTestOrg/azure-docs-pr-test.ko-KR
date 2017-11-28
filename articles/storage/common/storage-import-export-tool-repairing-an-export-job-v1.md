---
title: "Azure 가져오기/내보내기 내보내기 작업-v1 aaaRepairing | Microsoft Docs"
description: "Toorepair 생성 되어 사용 하 여 실행 하는 내보내기 작업의 경우 Azure 가져오기/내보내기 hello 하는 방법에 대해 알아봅니다 서비스입니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 728e2a42-04ce-4be8-9375-e9e2bc6827a5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: e54bc66495c8a3473b8ec51bb254bce8bdc9eab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-export-job"></a><span data-ttu-id="d1815-103">내보내기 작업 복구</span><span class="sxs-lookup"><span data-stu-id="d1815-103">Repairing an export job</span></span>
<span data-ttu-id="d1815-104">내보내기 작업이 완료 되 면 hello Microsoft Azure 가져오기/내보내기 도구 온-프레미스를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-104">After an export job has completed, you can run hello Microsoft Azure Import/Export Tool on-premises to:</span></span>  
  
1.  <span data-ttu-id="d1815-105">Hello Azure 가져오기/내보내기 서비스에서 없습니다 tooexport는 모든 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-105">Download any files that hello Azure Import/Export service was unable tooexport.</span></span>  
  
2.  <span data-ttu-id="d1815-106">Hello 파일 hello 드라이브에 올바르게 내보냈는지 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-106">Validate that hello files on hello drive were correctly exported.</span></span>  
  
<span data-ttu-id="d1815-107">이 기능은 연결 tooAzure 저장소 toouse 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-107">You must have connectivity tooAzure Storage toouse this functionality.</span></span>  
  
<span data-ttu-id="d1815-108">가져오기 작업 복구 hello 명령은 **RepairExport**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-108">hello command for repairing an import job is **RepairExport**.</span></span>

## <a name="repairexport-parameters"></a><span data-ttu-id="d1815-109">RepairExport 매개 변수</span><span class="sxs-lookup"><span data-stu-id="d1815-109">RepairExport parameters</span></span>

<span data-ttu-id="d1815-110">hello 다음 매개 변수 지정 될 수 있습니다 **RepairExport**:</span><span class="sxs-lookup"><span data-stu-id="d1815-110">hello following parameters can be specified with **RepairExport**:</span></span>  
  
|<span data-ttu-id="d1815-111">매개 변수</span><span class="sxs-lookup"><span data-stu-id="d1815-111">Parameter</span></span>|<span data-ttu-id="d1815-112">설명</span><span class="sxs-lookup"><span data-stu-id="d1815-112">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="d1815-113">**/r:<RepairFile\>**</span><span class="sxs-lookup"><span data-stu-id="d1815-113">**/r:<RepairFile\>**</span></span>|<span data-ttu-id="d1815-114">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-114">Required.</span></span> <span data-ttu-id="d1815-115">경로 toohello 복구는 파일 hello 복구 hello 진행 상태를 추적 하 고 중단된 된 복구 tooresume 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-115">Path toohello repair file, which tracks hello progress of hello repair, and allows you tooresume an interrupted repair.</span></span> <span data-ttu-id="d1815-116">각 드라이브에는 하나의 복구 파일만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-116">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="d1815-117">지정 된 드라이브의 복구를 시작할 때 아직 존재 하지 않는 hello 경로 tooa 복구 파일에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-117">When you start a repair for a given drive, you will pass in hello path tooa repair file which does not yet exist.</span></span> <span data-ttu-id="d1815-118">중단된 된 복구 tooresume 기존 복구 파일의 hello 이름에 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-118">tooresume an interrupted repair, you should pass in hello name of an existing repair file.</span></span> <span data-ttu-id="d1815-119">hello 복구 파일 해당 toohello 대상 드라이브를 항상 지정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-119">hello repair file corresponding toohello target drive must always be specified.</span></span>|  
|<span data-ttu-id="d1815-120">**/logdir:<LogDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="d1815-120">**/logdir:<LogDirectory\>**</span></span>|<span data-ttu-id="d1815-121">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-121">Optional.</span></span> <span data-ttu-id="d1815-122">hello 로그 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-122">hello log directory.</span></span> <span data-ttu-id="d1815-123">자세한 로그 파일 디렉터리 toothis 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-123">Verbose log files will be written toothis directory.</span></span> <span data-ttu-id="d1815-124">없는 로그 디렉터리를 지정 하는 경우 현재 디렉터리 hello hello 로그 디렉터리로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-124">If no log directory is specified, hello current directory will be used as hello log directory.</span></span>|  
|<span data-ttu-id="d1815-125">**/d:<TargetDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="d1815-125">**/d:<TargetDirectory\>**</span></span>|<span data-ttu-id="d1815-126">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-126">Required.</span></span> <span data-ttu-id="d1815-127">hello 디렉터리 toovalidate 및 복구 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-127">hello directory toovalidate and repair.</span></span> <span data-ttu-id="d1815-128">일반적으로 hello 내보내기 드라이브의 루트 디렉터리 hello 이지만 수 될 네트워크 파일 공유 포함 된 hello 내보낸 파일의 복사본입니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-128">This is usually hello root directory of hello export drive, but could also be a network file share containing a copy of hello exported files.</span></span>|  
|<span data-ttu-id="d1815-129">**/bk:<BitLockerKey\>**</span><span class="sxs-lookup"><span data-stu-id="d1815-129">**/bk:<BitLockerKey\>**</span></span>|<span data-ttu-id="d1815-130">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-130">Optional.</span></span> <span data-ttu-id="d1815-131">Hello 도구 toounlock 암호화 된 hello 내보낸 파일은 저장 하려는 경우에 hello BitLocker 키를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-131">You should specify hello BitLocker key if you want hello tool toounlock an encrypted where hello exported files are stored.</span></span>|  
|<span data-ttu-id="d1815-132">**/sn:<StorageAccountName\>**</span><span class="sxs-lookup"><span data-stu-id="d1815-132">**/sn:<StorageAccountName\>**</span></span>|<span data-ttu-id="d1815-133">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-133">Required.</span></span> <span data-ttu-id="d1815-134">hello hello 저장소 계정의 이름으로 hello에 대 한 내보내기 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-134">hello name of hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="d1815-135">**/sk:<StorageAccountKey\>**</span><span class="sxs-lookup"><span data-stu-id="d1815-135">**/sk:<StorageAccountKey\>**</span></span>|<span data-ttu-id="d1815-136">컨테이너 SAS가 지정되지 않은 경우에만 **필수**입니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-136">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="d1815-137">hello에 대 한 hello 저장소 계정에 대 한 hello 계정 키 내보내기 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-137">hello account key for hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="d1815-138">**/csas:<ContainerSas\>**</span><span class="sxs-lookup"><span data-stu-id="d1815-138">**/csas:<ContainerSas\>**</span></span>|<span data-ttu-id="d1815-139">**필요한** hello 저장소 계정 키를 지정 하지 않으면 하는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-139">**Required** if and only if hello storage account key is not specified.</span></span> <span data-ttu-id="d1815-140">hello 내보내기 작업과 연결 된 hello blob에 액세스 하기 위한 hello 컨테이너 SAS입니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-140">hello container SAS for accessing hello blobs associated with hello export job.</span></span>|  
|<span data-ttu-id="d1815-141">**/CopyLogFile:<DriveCopyLogFile\>**</span><span class="sxs-lookup"><span data-stu-id="d1815-141">**/CopyLogFile:<DriveCopyLogFile\>**</span></span>|<span data-ttu-id="d1815-142">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-142">Required.</span></span> <span data-ttu-id="d1815-143">hello 경로 toohello 드라이브 복사 로그 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-143">hello path toohello drive copy log file.</span></span> <span data-ttu-id="d1815-144">hello 파일 hello Windows Azure 가져오기/내보내기 서비스에서 생성 되 고 hello 작업과 연결 된 hello blob 저장소에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-144">hello file is generated by hello Windows Azure Import/Export service and can be downloaded from hello blob storage associated with hello job.</span></span> <span data-ttu-id="d1815-145">hello 복사 로그 파일을 사용 하면 실패 한 blob 또는 파일은 toobe 복구 하는 방법에 대 한 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-145">hello copy log file contains information about failed blobs or files which are toobe repaired.</span></span>|  
|<span data-ttu-id="d1815-146">**/ManifestFile:<DriveManifestFile\>**</span><span class="sxs-lookup"><span data-stu-id="d1815-146">**/ManifestFile:<DriveManifestFile\>**</span></span>|<span data-ttu-id="d1815-147">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-147">Optional.</span></span> <span data-ttu-id="d1815-148">hello 경로 toohello 내보내기 드라이브 매니페스트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-148">hello path toohello export drive's manifest file.</span></span> <span data-ttu-id="d1815-149">이 파일은 hello Windows Azure 가져오기/내보내기 서비스에서 생성 하며 및 필요에 따라 hello 작업과 연결 된 hello 저장소 계정의 blob에에서 hello 내보내기 드라이브에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-149">This file is generated by hello Windows Azure Import/Export service and stored on hello export drive, and optionally in a blob in hello storage account associated with hello job.</span></span><br /><br /> <span data-ttu-id="d1815-150">hello 콘텐츠의 hello hello 내보내기 드라이브에 파일을이 파일에 포함 된 hello MD5 해시와 함께 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-150">hello content of hello files on hello export drive will be verified with hello MD5 hashes contained in this file.</span></span> <span data-ttu-id="d1815-151">결정된 toobe 손상 된 파일에 다운로드 하 고 다시 작성 toohello 대상 디렉터리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-151">Any files that are determined toobe corrupted will be downloaded and rewritten toohello target directories.</span></span>|  
  
## <a name="using-repairexport-mode-toocorrect-failed-exports"></a><span data-ttu-id="d1815-152">RepairExport를 사용 하 여 모드 toocorrect 내보내기가 실패</span><span class="sxs-lookup"><span data-stu-id="d1815-152">Using RepairExport mode toocorrect failed exports</span></span>  
<span data-ttu-id="d1815-153">Tooexport 실패 한 hello Azure 가져오기/내보내기 도구 toodownload 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-153">You can use hello Azure Import/Export Tool toodownload files that failed tooexport.</span></span> <span data-ttu-id="d1815-154">hello 복사 로그 파일 tooexport 못한 파일 목록이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-154">hello copy log file will contain a list of files that failed tooexport.</span></span>  
  
<span data-ttu-id="d1815-155">내보내기 실패의 원인은 hello hello를 가능성에 따라 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-155">hello causes of export failures include hello following possibilities:</span></span>  
  
-   <span data-ttu-id="d1815-156">손상된 드라이브</span><span class="sxs-lookup"><span data-stu-id="d1815-156">Damaged drives</span></span>  
  
-   <span data-ttu-id="d1815-157">hello 전송 프로세스 중에 변경 하는 hello 저장소 계정 키</span><span class="sxs-lookup"><span data-stu-id="d1815-157">hello storage account key changed during hello transfer process</span></span>  
  
<span data-ttu-id="d1815-158">toorun hello 도구에서 **RepairExport** 모드에서는 먼저 hello 내보낸된 파일 tooyour 컴퓨터를 포함 하는 tooconnect hello 드라이브입니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-158">toorun hello tool in **RepairExport** mode, you first need tooconnect hello drive containing hello exported files tooyour computer.</span></span> <span data-ttu-id="d1815-159">다음으로 실행 하는 Azure 가져오기/내보내기 도구를 hello로 hello 경로 toothat 드라이브를 지정 하면 hello `/d` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-159">Next, run hello Azure Import/Export Tool, specifying hello path toothat drive with hello `/d` parameter.</span></span> <span data-ttu-id="d1815-160">또한 toospecify hello 경로 toohello 드라이브 복사 로그 파일 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-160">You also need toospecify hello path toohello drive's copy log file that you downloaded.</span></span> <span data-ttu-id="d1815-161">hello 다음 명령줄 예에서는 실행 hello 도구 toorepair tooexport 실패 한 모든 파일:</span><span class="sxs-lookup"><span data-stu-id="d1815-161">hello following command line example below runs hello tool toorepair any files that failed tooexport:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
<span data-ttu-id="d1815-162">hello 다음은 hello 실패 blob tooexport에 하나의 해당 블록을 보여 주는 복사 로그 파일의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-162">hello following is an example of a copy log file that shows that one block in hello blob failed tooexport:</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/desert.jpg</BlobPath>  
    <FilePath>\pictures\wild\desert.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList>  
      <Block Offset="65536" Length="65536" Id="AQAAAA==" Status="Failed" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
<span data-ttu-id="d1815-163">hello 복사 로그 파일 hello 내보내기 드라이브에 hello blob의 블록 toohello 파일 중 하나는 hello Windows Azure 가져오기/내보내기 서비스를 다운로드 하는 동안 오류가 발생 했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-163">hello copy log file indicates that a failure occurred while hello Windows Azure Import/Export service was downloading one of hello blob's blocks toohello file on hello export drive.</span></span> <span data-ttu-id="d1815-164">성공적으로 다운로드 하는 hello 파일의 다른 구성 요소를 hello 및 hello 파일 길이 잘못 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-164">hello other components of hello file downloaded successfully, and hello file length was correctly set.</span></span> <span data-ttu-id="d1815-165">이 경우 hello 도구는 hello 드라이브에 hello 파일을 열, hello 블록 hello 저장소 계정에서 다운로드 및 길이가 65536 인 65536 오프셋에서 시작 하는 파일 범위 toohello 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-165">In this case, hello tool will open hello file on hello drive, download hello block from hello storage account, and write it toohello file range starting from offset 65536 with length 65536.</span></span>  
  
## <a name="using-repairexport-toovalidate-drive-contents"></a><span data-ttu-id="d1815-166">RepairExport toovalidate 드라이브 콘텐츠를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="d1815-166">Using RepairExport toovalidate drive contents</span></span>  
<span data-ttu-id="d1815-167">Azure 가져오기/내보내기 hello로 사용할 수도 있습니다 **RepairExport** 옵션 toovalidate hello hello 드라이브의 내용이 올바른 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-167">You can also use Azure Import/Export with hello **RepairExport** option toovalidate hello contents on hello drive are correct.</span></span> <span data-ttu-id="d1815-168">각 내보내기 드라이브에 hello 매니페스트 파일에 hello 드라이브의 hello 내용 m d 5가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-168">hello manifest file on each export drive contains MD5s for hello contents of hello drive.</span></span>  
  
<span data-ttu-id="d1815-169">Azure 가져오기/내보내기 서비스 hello 저장할 수도 hello 매니페스트 파일 tooa 저장소 계정 hello 내보내기 프로세스 중.</span><span class="sxs-lookup"><span data-stu-id="d1815-169">hello Azure Import/Export service can also save hello manifest files tooa storage account during hello export process.</span></span> <span data-ttu-id="d1815-170">hello hello 매니페스트 파일의 위치는 hello를 통해 사용할 수 있는 [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) hello 작업이 완료 될 때 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-170">hello location of hello manifest files is available via hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation when hello job has completed.</span></span> <span data-ttu-id="d1815-171">참조 [가져오기/내보내기 서비스 매니페스트 파일 형식](storage-import-export-file-format-metadata-and-properties.md) 드라이브 매니페스트 파일의 hello 형식에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-171">See [Import/Export service Manifest File Format](storage-import-export-file-format-metadata-and-properties.md) for more information about hello format of a drive manifest file.</span></span>  
  
<span data-ttu-id="d1815-172">hello 다음 예제에서는 toorun hello로 Azure 가져오기/내보내기 도구를 hello 하는 방법을 **/ManifestFile** 및 **/CopyLogFile** 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="d1815-172">hello following example shows how toorun hello Azure Import/Export Tool with hello **/ManifestFile** and **/CopyLogFile** parameters:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
<span data-ttu-id="d1815-173">hello 다음은 매니페스트 파일의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-173">hello following is an example of a manifest file:</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveManifest Version="2011-10-01">  
  <Drive>  
    <DriveId>9WM35C3U</DriveId>  
    <ClientCreator>Windows Azure Import/Export service</ClientCreator>  
    <BlobList>
      <Blob>  
        <BlobPath>pictures/city/redmond.jpg</BlobPath>  
        <FilePath>\pictures\city\redmond.jpg</FilePath>  
        <Length>15360</Length>  
        <PageRangeList>  
          <PageRange Offset="0" Length="3584" Hash="72FC55ED9AFDD40A0C8D5C4193208416" />  
          <PageRange Offset="3584" Length="3584" Hash="68B28A561B73D1DA769D4C24AA427DB8" />  
          <PageRange Offset="7168" Length="512" Hash="F521DF2F50C46BC5F9EA9FB787A23EED" />  
        </PageRangeList>  
        <PropertiesPath Hash="E72A22EA959566066AD89E3B49020C0A">\pictures\city\redmond.jpg.properties</PropertiesPath>  
      </Blob>  
      <Blob>  
        <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
        <FilePath>\pictures\wild\canyon.jpg</FilePath>  
        <Length>10884</Length>  
        <BlockList>  
          <Block Offset="0" Length="2721" Id="AAAAAA==" Hash="263DC9C4B99C2177769C5EBE04787037" />  
          <Block Offset="2721" Length="2721" Id="AQAAAA==" Hash="0C52BAE2CC20EFEC15CC1E3045517AA6" />  
          <Block Offset="5442" Length="2721" Id="AgAAAA==" Hash="73D1CB62CB426230C34C9F57B7148F10" />  
          <Block Offset="8163" Length="2721" Id="AwAAAA==" Hash="11210E665C5F8E7E4F136D053B243E6A" />  
        </BlockList>  
        <PropertiesPath Hash="81D7F81B2C29F10D6E123D386C3A4D5A">\pictures\wild\canyon.jpg.properties</PropertiesPath>  
      </Blob> 
    </BlobList>  
 </Drive>  
</DriveManifest>  
``` 
  
<span data-ttu-id="d1815-174">Hello 복구 프로세스 완료 후 hello 도구 hello 매니페스트 파일에서 참조 된 각 파일을 통해 읽고 hello MD5 해시와 함께 hello 파일의 무결성을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d1815-174">After finishing hello repair process, hello tool will read through each file referenced in hello manifest file and verify hello file's integrity with hello MD5 hashes.</span></span> <span data-ttu-id="d1815-175">위의 hello 매니페스트의 경우 다음과 같은 구성 요소가 hello를 거치게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-175">For hello manifest above, it will go through hello following components.</span></span>  

```  
G:\pictures\city\redmond.jpg, offset 0, length 3584  
  
G:\pictures\city\redmond.jpg, offset 3584, length 3584  
  
G:\pictures\city\redmond.jpg, offset 7168, length 3584  
  
G:\pictures\city\redmond.jpg.properties  
  
G:\pictures\wild\canyon.jpg, offset 0, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 2721, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 5442, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 8163, length 2721  
  
G:\pictures\wild\canyon.jpg.properties  
```

<span data-ttu-id="d1815-176">Hello 확인에 실패 한 모든 구성 요소 hello 도구를 통해 다운로드 되 고 다시 작성 toohello hello 드라이브에 파일 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1815-176">Any component failing hello verification will be downloaded by hello tool and rewritten toohello same file on hello drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="d1815-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d1815-177">Next steps</span></span>
 
* [<span data-ttu-id="d1815-178">설정 hello Azure 가져오기/내보내기 도구</span><span class="sxs-lookup"><span data-stu-id="d1815-178">Setting Up hello Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="d1815-179">가져오기 작업을 위한 하드 드라이브 준비</span><span class="sxs-lookup"><span data-stu-id="d1815-179">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="d1815-180">복사 로그 파일을 사용하여 작업 상태 검토</span><span class="sxs-lookup"><span data-stu-id="d1815-180">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="d1815-181">가져오기 작업 복구</span><span class="sxs-lookup"><span data-stu-id="d1815-181">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="d1815-182">Hello Azure 가져오기/내보내기 도구 문제 해결</span><span class="sxs-lookup"><span data-stu-id="d1815-182">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
