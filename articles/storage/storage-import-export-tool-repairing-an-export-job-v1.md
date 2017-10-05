---
title: "Azure Import/Export 내보내기 작업 복구 - v1 | Microsoft Docs"
description: "Azure Import/Export 서비스를 사용하여 생성 및 실행된 내보내기 작업을 복구하는 방법을 알아봅니다."
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
ms.openlocfilehash: 30ca0f8d06cb1927c19e66035ff485db0fc09e5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="repairing-an-export-job"></a><span data-ttu-id="252c6-103">내보내기 작업 복구</span><span class="sxs-lookup"><span data-stu-id="252c6-103">Repairing an export job</span></span>
<span data-ttu-id="252c6-104">내보내기 작업이 완료된 후에 온-프레미스에서 Microsoft Azure Import/Export 도구를 실행하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-104">After an export job has completed, you can run the Microsoft Azure Import/Export Tool on-premises to:</span></span>  
  
1.  <span data-ttu-id="252c6-105">Azure Import/Export 서비스로 내보낼 수 없는 모든 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-105">Download any files that the Azure Import/Export service was unable to export.</span></span>  
  
2.  <span data-ttu-id="252c6-106">드라이브의 파일이 제대로 내보내졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-106">Validate that the files on the drive were correctly exported.</span></span>  
  
<span data-ttu-id="252c6-107">이 기능을 사용하려면 Azure Storage에 연결되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-107">You must have connectivity to Azure Storage to use this functionality.</span></span>  
  
<span data-ttu-id="252c6-108">가져오기 작업을 복구하는 명령은 **RepairExport**입니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-108">The command for repairing an import job is **RepairExport**.</span></span>

## <a name="repairexport-parameters"></a><span data-ttu-id="252c6-109">RepairExport 매개 변수</span><span class="sxs-lookup"><span data-stu-id="252c6-109">RepairExport parameters</span></span>

<span data-ttu-id="252c6-110">**RepairExport**와 함께 다음 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-110">The following parameters can be specified with **RepairExport**:</span></span>  
  
|<span data-ttu-id="252c6-111">매개 변수</span><span class="sxs-lookup"><span data-stu-id="252c6-111">Parameter</span></span>|<span data-ttu-id="252c6-112">설명</span><span class="sxs-lookup"><span data-stu-id="252c6-112">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="252c6-113">**/r:<RepairFile\>**</span><span class="sxs-lookup"><span data-stu-id="252c6-113">**/r:<RepairFile\>**</span></span>|<span data-ttu-id="252c6-114">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-114">Required.</span></span> <span data-ttu-id="252c6-115">복구의 진행 상황을 추적하고 중단된 복구를 다시 시작할 수 있도록 하는 복구 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-115">Path to the repair file, which tracks the progress of the repair, and allows you to resume an interrupted repair.</span></span> <span data-ttu-id="252c6-116">각 드라이브에는 하나의 복구 파일만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-116">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="252c6-117">지정된 드라이브의 복구를 시작할 때 아직 존재하지 않는 복구 파일의 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-117">When you start a repair for a given drive, you will pass in the path to a repair file which does not yet exist.</span></span> <span data-ttu-id="252c6-118">중단된 복구를 다시 시작하려면 기존 복구 파일의 이름을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-118">To resume an interrupted repair, you should pass in the name of an existing repair file.</span></span> <span data-ttu-id="252c6-119">대상 드라이브에 해당하는 복구 파일을 항상 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-119">The repair file corresponding to the target drive must always be specified.</span></span>|  
|<span data-ttu-id="252c6-120">**/logdir:<LogDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="252c6-120">**/logdir:<LogDirectory\>**</span></span>|<span data-ttu-id="252c6-121">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-121">Optional.</span></span> <span data-ttu-id="252c6-122">로그 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-122">The log directory.</span></span> <span data-ttu-id="252c6-123">이 디렉터리에 자세한 로그 파일이 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-123">Verbose log files will be written to this directory.</span></span> <span data-ttu-id="252c6-124">로그 디렉터리를 지정하지 않는 경우 현재 디렉터리가 로그 디렉터리로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-124">If no log directory is specified, the current directory will be used as the log directory.</span></span>|  
|<span data-ttu-id="252c6-125">**/d:<TargetDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="252c6-125">**/d:<TargetDirectory\>**</span></span>|<span data-ttu-id="252c6-126">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-126">Required.</span></span> <span data-ttu-id="252c6-127">유효성을 검사하고 복구할 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-127">The directory to validate and repair.</span></span> <span data-ttu-id="252c6-128">일반적으로는 내보내기 드라이브의 루트 디렉터리이지만 내보낸 파일의 복사본을 포함하는 네트워크 파일 공유일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-128">This is usually the root directory of the export drive, but could also be a network file share containing a copy of the exported files.</span></span>|  
|<span data-ttu-id="252c6-129">**/bk:<BitLockerKey\>**</span><span class="sxs-lookup"><span data-stu-id="252c6-129">**/bk:<BitLockerKey\>**</span></span>|<span data-ttu-id="252c6-130">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-130">Optional.</span></span> <span data-ttu-id="252c6-131">내보낸 파일이 저장되는 암호화된 위치의 잠금을 해제하려면 BitLocker 키를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-131">You should specify the BitLocker key if you want the tool to unlock an encrypted where the exported files are stored.</span></span>|  
|<span data-ttu-id="252c6-132">**/sn:<StorageAccountName\>**</span><span class="sxs-lookup"><span data-stu-id="252c6-132">**/sn:<StorageAccountName\>**</span></span>|<span data-ttu-id="252c6-133">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-133">Required.</span></span> <span data-ttu-id="252c6-134">내보내기 작업에 대한 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-134">The name of the storage account for the export job.</span></span>|  
|<span data-ttu-id="252c6-135">**/sk:<StorageAccountKey\>**</span><span class="sxs-lookup"><span data-stu-id="252c6-135">**/sk:<StorageAccountKey\>**</span></span>|<span data-ttu-id="252c6-136">컨테이너 SAS가 지정되지 않은 경우에만 **필수**입니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-136">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="252c6-137">내보내기 작업에 대한 저장소 계정의 계정 키입니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-137">The account key for the storage account for the export job.</span></span>|  
|<span data-ttu-id="252c6-138">**/csas:<ContainerSas\>**</span><span class="sxs-lookup"><span data-stu-id="252c6-138">**/csas:<ContainerSas\>**</span></span>|<span data-ttu-id="252c6-139">저장소 계정 키가 지정되지 않은 경우에만 **필수**입니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-139">**Required** if and only if the storage account key is not specified.</span></span> <span data-ttu-id="252c6-140">내보내기 작업과 연결된 blob에 액세스하기 위한 컨테이너 SAS입니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-140">The container SAS for accessing the blobs associated with the export job.</span></span>|  
|<span data-ttu-id="252c6-141">**/CopyLogFile:<DriveCopyLogFile\>**</span><span class="sxs-lookup"><span data-stu-id="252c6-141">**/CopyLogFile:<DriveCopyLogFile\>**</span></span>|<span data-ttu-id="252c6-142">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-142">Required.</span></span> <span data-ttu-id="252c6-143">드라이브 복사 로그 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-143">The path to the drive copy log file.</span></span> <span data-ttu-id="252c6-144">이 파일은 Microsoft Azure Import/Export 서비스에 의해 생성되고 작업과 연결된 Blob Storage에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-144">The file is generated by the Windows Azure Import/Export service and can be downloaded from the blob storage associated with the job.</span></span> <span data-ttu-id="252c6-145">복사 로그 파일에는 복구해야 하는 실패한 blob 또는 파일에 대한 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-145">The copy log file contains information about failed blobs or files which are to be repaired.</span></span>|  
|<span data-ttu-id="252c6-146">**/ManifestFile:<DriveManifestFile\>**</span><span class="sxs-lookup"><span data-stu-id="252c6-146">**/ManifestFile:<DriveManifestFile\>**</span></span>|<span data-ttu-id="252c6-147">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-147">Optional.</span></span> <span data-ttu-id="252c6-148">내보내기 드라이브의 매니페스트 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-148">The path to the export drive's manifest file.</span></span> <span data-ttu-id="252c6-149">이 파일은 Microsoft Azure Import/Export 서비스에서 생성되고 내보내기 드라이브 및 경우에 따라 작업과 연결된 저장소 계정의 blob에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-149">This file is generated by the Windows Azure Import/Export service and stored on the export drive, and optionally in a blob in the storage account associated with the job.</span></span><br /><br /> <span data-ttu-id="252c6-150">내보내기 드라이브에 있는 파일의 내용은 이 파일에 포함된 MD5 해시를 사용해서 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-150">The content of the files on the export drive will be verified with the MD5 hashes contained in this file.</span></span> <span data-ttu-id="252c6-151">손상된 것으로 확인된 모든 파일은 다운로드된 후 대상 디렉터리에 다시 써집니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-151">Any files that are determined to be corrupted will be downloaded and rewritten to the target directories.</span></span>|  
  
## <a name="using-repairexport-mode-to-correct-failed-exports"></a><span data-ttu-id="252c6-152">RepairExport 모드를 사용하여 실패한 내보내기 수정</span><span class="sxs-lookup"><span data-stu-id="252c6-152">Using RepairExport mode to correct failed exports</span></span>  
<span data-ttu-id="252c6-153">Azure Import/Export 도구를 사용하여 내보내기에 실패한 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-153">You can use the Azure Import/Export Tool to download files that failed to export.</span></span> <span data-ttu-id="252c6-154">복사 로그 파일에는 내보내기에 실패한 파일 목록이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-154">The copy log file will contain a list of files that failed to export.</span></span>  
  
<span data-ttu-id="252c6-155">내보내기 실패의 원인에는 다음 가능성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-155">The causes of export failures include the following possibilities:</span></span>  
  
-   <span data-ttu-id="252c6-156">손상된 드라이브</span><span class="sxs-lookup"><span data-stu-id="252c6-156">Damaged drives</span></span>  
  
-   <span data-ttu-id="252c6-157">전송 프로세스 중에 변경된 저장소 계정 키</span><span class="sxs-lookup"><span data-stu-id="252c6-157">The storage account key changed during the transfer process</span></span>  
  
<span data-ttu-id="252c6-158">이 도구를 **RepairExport** 모드로 실행하려면 먼저 내보낸 파일을 포함하는 드라이브를 사용자 컴퓨터에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-158">To run the tool in **RepairExport** mode, you first need to connect the drive containing the exported files to your computer.</span></span> <span data-ttu-id="252c6-159">다음에는 Azure Import/Export 도구를 실행하고, `/d` 매개 변수를 사용하여 해당 드라이브의 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-159">Next, run the Azure Import/Export Tool, specifying the path to that drive with the `/d` parameter.</span></span> <span data-ttu-id="252c6-160">또한 다운로드한 드라이브의 복사 로그 파일 경로를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-160">You also need to specify the path to the drive's copy log file that you downloaded.</span></span> <span data-ttu-id="252c6-161">아래의 명령줄 예제에서는 이 도구를 실행하여 내보내기에 실패한 모든 파일을 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-161">The following command line example below runs the tool to repair any files that failed to export:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
<span data-ttu-id="252c6-162">다음은 blob의 한 블록을 내보내지 못했음을 보여 주는 복사 로그 파일의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-162">The following is an example of a copy log file that shows that one block in the blob failed to export:</span></span>  
  
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
  
<span data-ttu-id="252c6-163">이 복사 로그 파일은 Microsoft Azure Import/Export 서비스가 blob 블록 중 하나를 내보내기 드라이브의 파일에 다운로드하는 동안 오류가 발생했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-163">The copy log file indicates that a failure occurred while the Windows Azure Import/Export service was downloading one of the blob's blocks to the file on the export drive.</span></span> <span data-ttu-id="252c6-164">파일의 다른 구성 요소는 성공적으로 다운로드되었으며 파일 길이도 올바르게 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-164">The other components of the file downloaded successfully, and the file length was correctly set.</span></span> <span data-ttu-id="252c6-165">이 경우 도구는 드라이브의 파일을 열고 저장소 계정에서 블록을 다운로드한 후 길이가 65536이고 오프셋 65536부터 시작하는 파일 범위에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-165">In this case, the tool will open the file on the drive, download the block from the storage account, and write it to the file range starting from offset 65536 with length 65536.</span></span>  
  
## <a name="using-repairexport-to-validate-drive-contents"></a><span data-ttu-id="252c6-166">RepairExport를 사용하여 드라이브 내용의 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="252c6-166">Using RepairExport to validate drive contents</span></span>  
<span data-ttu-id="252c6-167">**RepairExport** 옵션과 Azure Import/Export를 함께 사용하여 드라이브 내용이 올바른지 검사할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-167">You can also use Azure Import/Export with the **RepairExport** option to validate the contents on the drive are correct.</span></span> <span data-ttu-id="252c6-168">각 내보내기 드라이브에 있는 매니페스트 파일에는 드라이브 내용에 대한 MD5가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-168">The manifest file on each export drive contains MD5s for the contents of the drive.</span></span>  
  
<span data-ttu-id="252c6-169">Azure Import/Export 서비스는 내보내기 프로세스 동안 저장소 계정에 이 매니페스트 파일을 저장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-169">The Azure Import/Export service can also save the manifest files to a storage account during the export process.</span></span> <span data-ttu-id="252c6-170">매니페스트 파일의 위치는 작업이 완료될 때 [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 작업을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-170">The location of the manifest files is available via the [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation when the job has completed.</span></span> <span data-ttu-id="252c6-171">드라이브 매니페스트 파일의 형식에 대한 자세한 내용은 [Import/Export 서비스 매니페스트 파일 형식](storage-import-export-file-format-metadata-and-properties.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="252c6-171">See [Import/Export service Manifest File Format](storage-import-export-file-format-metadata-and-properties.md) for more information about the format of a drive manifest file.</span></span>  
  
<span data-ttu-id="252c6-172">다음 예제에서는 **/ManifestFile** 및 **/CopyLogFile** 매개 변수를 사용하여 Azure Import/Export 도구를 실행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-172">The following example shows how to run the Azure Import/Export Tool with the **/ManifestFile** and **/CopyLogFile** parameters:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
<span data-ttu-id="252c6-173">다음은 매니페스트 파일의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-173">The following is an example of a manifest file:</span></span>  
  
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
  
<span data-ttu-id="252c6-174">복구 프로세스를 마친 후 이 도구는 매니페스트 파일에 참조된 각 파일을 읽고 MD5 해시를 사용하여 파일 무결성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-174">After finishing the repair process, the tool will read through each file referenced in the manifest file and verify the file's integrity with the MD5 hashes.</span></span> <span data-ttu-id="252c6-175">위에 있는 매니페스트의 경우 다음 구성 요소가 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-175">For the manifest above, it will go through the following components.</span></span>  

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

<span data-ttu-id="252c6-176">확인에 실패한 모든 구성 요소는 도구를 통해 다운로드된 후 드라이브의 동일한 파일에 다시 써집니다.</span><span class="sxs-lookup"><span data-stu-id="252c6-176">Any component failing the verification will be downloaded by the tool and rewritten to the same file on the drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="252c6-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="252c6-177">Next steps</span></span>
 
* [<span data-ttu-id="252c6-178">Azure Import/Export 도구 설정</span><span class="sxs-lookup"><span data-stu-id="252c6-178">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="252c6-179">가져오기 작업을 위한 하드 드라이브 준비</span><span class="sxs-lookup"><span data-stu-id="252c6-179">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="252c6-180">복사 로그 파일을 사용하여 작업 상태 검토</span><span class="sxs-lookup"><span data-stu-id="252c6-180">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="252c6-181">가져오기 작업 복구</span><span class="sxs-lookup"><span data-stu-id="252c6-181">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="252c6-182">Azure Import/Export 도구 문제 해결</span><span class="sxs-lookup"><span data-stu-id="252c6-182">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
