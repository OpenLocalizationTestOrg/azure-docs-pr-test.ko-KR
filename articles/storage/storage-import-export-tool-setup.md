---
title: "hello Azure 가져오기/내보내기 도구를 aaaSetting | Microsoft Docs"
description: "준비 및 복구 도구 hello Azure 가져오기/내보내기 서비스에 대 한 hello tooset 드라이브 하는 방법에 대해 알아봅니다."
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
ms.date: 06/29/2017
ms.author: muralikk
ms.openlocfilehash: ee5bb99bd84ea5ee2f6b6e99c5a375b215e94ea8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-hello-azure-importexport-tool"></a><span data-ttu-id="51a45-103">Hello Azure 가져오기/내보내기 도구 설정</span><span class="sxs-lookup"><span data-stu-id="51a45-103">Setting up hello Azure Import/Export Tool</span></span>

<span data-ttu-id="51a45-104">hello Microsoft Azure 가져오기/내보내기 도구는 hello 드라이브 준비 및 Microsoft Azure 가져오기/내보내기 서비스 hello로 사용할 수 있는 복구 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="51a45-104">hello Microsoft Azure Import/Export Tool is hello drive preparation and repair tool that you can use with hello Microsoft Azure Import/Export service.</span></span> <span data-ttu-id="51a45-105">다음 함수 hello에 대 한 hello 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51a45-105">You can use hello tool for hello following functions:</span></span>

* <span data-ttu-id="51a45-106">가져오기 작업을 만들기 전에이 도구 toocopy 데이터 toohello 하드 드라이브 tooship tooan Azure 데이터 센터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51a45-106">Before creating an import job, you can use this tool toocopy data toohello hard drives you are going tooship tooan Azure data center.</span></span>
* <span data-ttu-id="51a45-107">가져오기 작업이 완료 된 후 사용할 수 있습니다이 도구 toorepair 손상 된, 누락 된 또는 충돌 하는 모든 blob 다른 blob과.</span><span class="sxs-lookup"><span data-stu-id="51a45-107">After an import job has completed, you can use this tool toorepair any blobs that were corrupted, were missing, or conflicted with other blobs.</span></span>
* <span data-ttu-id="51a45-108">완료 된 내보내기 작업에서 hello 드라이브를 받은 후에 손상 된 파일 또는 hello 드라이브에 없기 때문에이 도구 toorepair를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51a45-108">After you receive hello drives from a completed export job, you can use this tool toorepair any files that were corrupted or missing on hello drives.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51a45-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="51a45-109">Prerequisites</span></span>

<span data-ttu-id="51a45-110">있다면 **드라이브 준비** 가져오기 작업에 대 한 필수 구성 요소를 다음 hello 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51a45-110">If you are **preparing drives** for an import job, hello following prerequisites must be met:</span></span>

* <span data-ttu-id="51a45-111">활성 Azure 구독이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51a45-111">You must have an active Azure subscription.</span></span>
* <span data-ttu-id="51a45-112">구독에 저장소 계정을 포함 해야 충분 한 사용 가능한 공간 toostore hello 파일과 함께 tooimport는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="51a45-112">Your subscription must include a storage account with enough available space toostore hello files you are going tooimport.</span></span>
* <span data-ttu-id="51a45-113">Hello 저장소 계정 액세스 키 중 하나 이상을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="51a45-113">You need at least one of hello storage account access keys.</span></span>
* <span data-ttu-id="51a45-114">Windows 7, Windows Server 2008 R2 또는 최신 Windows 운영 체제가 설치 된 컴퓨터 ("복사 컴퓨터" hello) 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51a45-114">You need a computer (hello "copy machine") with Windows 7, Windows Server 2008 R2, or a newer Windows operating system installed.</span></span>
* <span data-ttu-id="51a45-115">.NET Framework 4 hello hello 복사 컴퓨터에 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51a45-115">hello .NET Framework 4 must be installed on hello copy machine.</span></span>
* <span data-ttu-id="51a45-116">Hello 복사 컴퓨터에서 BitLocker는 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51a45-116">BitLocker must be enabled on hello copy machine.</span></span>
* <span data-ttu-id="51a45-117">하나 필요 하거나 더 많은 빈 3.5 인치 SATA 하드 드라이브 toohello 복사 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="51a45-117">You need one or more empty 3.5-inch SATA hard drives connected toohello copy machine.</span></span>
* <span data-ttu-id="51a45-118">네트워크 공유 나 로컬 하드 드라이브에 있는지 여부를 tooimport hello 파일 hello 복사 컴퓨터에서 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51a45-118">hello files you plan tooimport must be accessible from hello copy machine, whether they are on a network share or a local hard drive.</span></span>

<span data-ttu-id="51a45-119">너무 시도 하는 경우**한 가져오기를 복구** 를 부분적으로 실패 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51a45-119">If you are attempting too**repair an import** that has partially failed, you need:</span></span>

* <span data-ttu-id="51a45-120">hello 복사 로그 파일</span><span class="sxs-lookup"><span data-stu-id="51a45-120">hello copy log files</span></span>
* <span data-ttu-id="51a45-121">hello 저장소 계정 키</span><span class="sxs-lookup"><span data-stu-id="51a45-121">hello storage account key</span></span>

<span data-ttu-id="51a45-122">너무 시도 하는 경우**한 내보내기를 복구** 를 부분적으로 실패 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51a45-122">If you are attempting too**repair an export**  that has partially failed, you need:</span></span>

* <span data-ttu-id="51a45-123">hello 복사 로그 파일</span><span class="sxs-lookup"><span data-stu-id="51a45-123">hello copy log files</span></span>
* <span data-ttu-id="51a45-124">hello 매니페스트 파일 (선택 사항)</span><span class="sxs-lookup"><span data-stu-id="51a45-124">hello manifest files (optional)</span></span>
* <span data-ttu-id="51a45-125">hello 저장소 계정 키</span><span class="sxs-lookup"><span data-stu-id="51a45-125">hello storage account key</span></span>

## <a name="installing-hello-azure-importexport-tool"></a><span data-ttu-id="51a45-126">Hello Azure 가져오기/내보내기 도구 설치</span><span class="sxs-lookup"><span data-stu-id="51a45-126">Installing hello Azure Import/Export Tool</span></span>

<span data-ttu-id="51a45-127">첫째, [hello Azure 가져오기/내보내기 도구를 다운로드](https://www.microsoft.com/download/details.aspx?id=55280) 압축을 풉니다 tooa 디렉터리 사용자의 컴퓨터에 예를 들어 `c:\WAImportExport`합니다.</span><span class="sxs-lookup"><span data-stu-id="51a45-127">First, [download hello Azure Import/Export Tool](https://www.microsoft.com/download/details.aspx?id=55280) and extract it tooa directory on your computer, for example `c:\WAImportExport`.</span></span>

<span data-ttu-id="51a45-128">hello Azure 가져오기/내보내기 도구는 다음 파일이 hello로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51a45-128">hello Azure Import/Export Tool consists of hello following files:</span></span>

* <span data-ttu-id="51a45-129">dataset.csv</span><span class="sxs-lookup"><span data-stu-id="51a45-129">dataset.csv</span></span>
* <span data-ttu-id="51a45-130">driveset.csv</span><span class="sxs-lookup"><span data-stu-id="51a45-130">driveset.csv</span></span>
* <span data-ttu-id="51a45-131">hddid.dll</span><span class="sxs-lookup"><span data-stu-id="51a45-131">hddid.dll</span></span>
* <span data-ttu-id="51a45-132">Microsoft.Data.Services.Client.dll</span><span class="sxs-lookup"><span data-stu-id="51a45-132">Microsoft.Data.Services.Client.dll</span></span>
* <span data-ttu-id="51a45-133">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="51a45-133">Microsoft.WindowsAzure.Storage.dll</span></span>
* <span data-ttu-id="51a45-134">Microsoft.WindowsAzure.Storage.pdb</span><span class="sxs-lookup"><span data-stu-id="51a45-134">Microsoft.WindowsAzure.Storage.pdb</span></span>
* <span data-ttu-id="51a45-135">Microsoft.WindowsAzure.Storage.xml</span><span class="sxs-lookup"><span data-stu-id="51a45-135">Microsoft.WindowsAzure.Storage.xml</span></span>
* <span data-ttu-id="51a45-136">WAImportExport.exe</span><span class="sxs-lookup"><span data-stu-id="51a45-136">WAImportExport.exe</span></span>
* <span data-ttu-id="51a45-137">WAImportExport.exe.config</span><span class="sxs-lookup"><span data-stu-id="51a45-137">WAImportExport.exe.config</span></span>
* <span data-ttu-id="51a45-138">WAImportExport.pdb</span><span class="sxs-lookup"><span data-stu-id="51a45-138">WAImportExport.pdb</span></span>
* <span data-ttu-id="51a45-139">WAImportExportCore.dll</span><span class="sxs-lookup"><span data-stu-id="51a45-139">WAImportExportCore.dll</span></span>
* <span data-ttu-id="51a45-140">WAImportExportCore.pdb</span><span class="sxs-lookup"><span data-stu-id="51a45-140">WAImportExportCore.pdb</span></span>
* <span data-ttu-id="51a45-141">WAImportExportRepair.dll</span><span class="sxs-lookup"><span data-stu-id="51a45-141">WAImportExportRepair.dll</span></span>
* <span data-ttu-id="51a45-142">WAImportExportRepair.pdb</span><span class="sxs-lookup"><span data-stu-id="51a45-142">WAImportExportRepair.pdb</span></span>

<span data-ttu-id="51a45-143">다음으로에서 명령 프롬프트 창을 열고 **관리자 모드**, 및 압축을 푼 파일 hello를 포함 하는 hello 디렉터리로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="51a45-143">Next, open a Command Prompt window in **Administrator mode**, and change into hello directory containing hello extracted files.</span></span>

<span data-ttu-id="51a45-144">hello 도구를 실행 하는 hello 명령에 대 한 toooutput 도움말 (`WAImportExport.exe`) 매개 변수 없이:</span><span class="sxs-lookup"><span data-stu-id="51a45-144">toooutput help for hello command, run hello tool (`WAImportExport.exe`) without parameters:</span></span>

```
WAImportExport, a client tool for Windows Azure Import/Export Service. Microsoft (c) 2013


Copy directories and/or files with a new copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>]
        [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>]
        DataSet:<dataset.csv>

Add more drives:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AdditionalDriveSet:<driveset.csv>

Abort an interrupted copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AbortSession

Resume an interrupted copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /ResumeSession

List drives:
    WAImportExport.exe PrepImport /j:<JournalFile> /ListDrives

List copy sessions:
    WAImportExport.exe PrepImport /j:<JournalFile> /ListCopySessions

Repair a Drive:
    WAImportExport.exe RepairImport | RepairExport
        /r:<RepairFile> [/logdir:<LogDirectory>]
        [/d:<TargetDirectories>] [/bk:<BitLockerKey>]
        /sn:<StorageAccountName> /sk:<StorageAccountKey>
        [/CopyLogFile:<DriveCopyLogFile>] [/ManifestFile:<DriveManifestFile>]
        [/PathMapFile:<DrivePathMapFile>]

Preview an Export Job:
    WAImportExport.exe PreviewExport
        [/logdir:<LogDirectory>]
        /sn:<StorageAccountName> /sk:<StorageAccountKey>
        /ExportBlobListFile:<ExportBlobListFile> /DriveSize:<DriveSize>

Parameters:

    /j:<JournalFile>
        - Required. Path toohello journal file. A journal file tracks a set of drives and
          records hello progress in preparing these drives. hello journal file must always
          be specified.
    /logdir:<LogDirectory>
        - Optional. hello log directory. Verbose log files as well as some temporary
          files will be written toothis directory. If not specified, current directory
          will be used as hello log directory. hello log directory can be specified only
          once for hello same journal file.
    /id:<SessionId>
        - Optional. hello session Id is used tooidentify a copy session. It is used to
          ensure accurate recovery of an interrupted copy session.
    /ResumeSession
        - Optional. If hello last copy session was terminated abnormally, this parameter
          can be specified tooresume hello session.
    /AbortSession
        - Optional. If hello last copy session was terminated abnormally, this parameter
          can be specified tooabort hello session.
    /sn:<StorageAccountName>
        - Required. Only applicable for RepairImport and RepairExport. hello name of
          hello storage account.
    /sk:<StorageAccountKey>
        - Required. hello key of hello storage account.
    /InitialDriveSet:<driveset.csv>
        - Required. A .csv file that contains a list of drives tooprepare.
    /AdditionalDriveSet:<driveset.csv>
        - Required. A .csv file that contains a list of additional drives toobe added.
    /r:<RepairFile>
        - Required. Only applicable for RepairImport and RepairExport.
          Path toohello file for tracking repair progress. Each drive must have one
          and only one repair file.
    /d:<TargetDirectories>
        - Required. Only applicable for RepairImport and RepairExport.
          For RepairImport, one or more semicolon-separated directories toorepair;
          For RepairExport, one directory toorepair, e.g. root directory of hello drive.
    /CopyLogFile:<DriveCopyLogFile>
        - Required. Only applicable for RepairImport and RepairExport. Path toothe
          drive copy log file (verbose or error).
    /ManifestFile:<DriveManifestFile>
        - Required. Only applicable for RepairExport. Path toohello drive manifest file.
    /PathMapFile:<DrivePathMapFile>
        - Optional. Only applicable for RepairImport. Path toohello file containing
          mappings of file paths relative toohello drive root toolocations of actual files
          (tab-delimited). When first specified, it will be populated with file paths
          with empty targets, which means either they are not found in TargetDirectories,
          access denied, with invalid name, or they exist in multiple directories. The
          path map file can be manually edited tooinclude hello correct target paths and
          specified again for hello tool tooresolve hello file paths correctly.
    /ExportBlobListFile:<ExportBlobListFile>
        - Required. Path toohello XML file containing list of blob paths or blob path
          prefixes for hello blobs toobe exported. hello file format is hello same as the
          blob list blob format in hello Put Job operation of hello Import/Export Service
          REST API.
    /DriveSize:<DriveSize>
        - Required. Size of drives toobe used for export. For example, 500GB, 1.5TB.
          Note: 1 GB = 1,000,000,000 bytes
                1 TB = 1,000,000,000,000 bytes
    /DataSet:<dataset.csv>
        - Required. A .csv file that contains a list of directories and/or a list files
          toobe copied tootarget drives.

    /silentmode
        - Optional. If not specified, it will remind you hello requirement of drives and
          need your confirmation toocontinue.

Examples:

    Copy a data set tooa drive:
    WAImportExport.exe PrepImport
        /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GEL
        xmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /InitialDriveSet:driveset1.csv
        /DataSet:data.csv

    Copy another dataset toohello same drive following hello above command:
    WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#2 /DataSet:dataset2.csv

    Preview how many 1.5 TB drives are needed for an export job:
    WAImportExport.exe PreviewExport
        /sn:mytestaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7K
        ysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\temp\myexportbloblist.xml
        /DriveSize:1.5TB

    Repair an finished import job:
    WAImportExport.exe RepairImport
        /r:9WM35C2V.rep /d:X:\ /bk:442926-020713-108086-436744-137335-435358-242242-2795
        98 /sn:mytestaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94
        f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\temp\9WM35C2V_error.log
```

## <a name="next-steps"></a><span data-ttu-id="51a45-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="51a45-145">Next steps</span></span>

* [<span data-ttu-id="51a45-146">가져오기 작업을 위한 하드 드라이브 준비</span><span class="sxs-lookup"><span data-stu-id="51a45-146">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import.md)
* [<span data-ttu-id="51a45-147">내보내기 작업에 대한 드라이브 사용량 미리 보기</span><span class="sxs-lookup"><span data-stu-id="51a45-147">Previewing drive usage for an export job</span></span>](storage-import-export-tool-previewing-drive-usage-export-v1.md)
* [<span data-ttu-id="51a45-148">복사 로그 파일을 사용하여 작업 상태 검토</span><span class="sxs-lookup"><span data-stu-id="51a45-148">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)
* [<span data-ttu-id="51a45-149">가져오기 작업 복구</span><span class="sxs-lookup"><span data-stu-id="51a45-149">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)
* [<span data-ttu-id="51a45-150">내보내기 작업 복구</span><span class="sxs-lookup"><span data-stu-id="51a45-150">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)
* [<span data-ttu-id="51a45-151">Hello Azure 가져오기/내보내기 도구 문제 해결</span><span class="sxs-lookup"><span data-stu-id="51a45-151">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
