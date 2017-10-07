---
title: "Azure 백업 서버 v 2의 aaaSilent 설치 | Microsoft Docs"
description: "Azure 백업 서버 v 2를 설치 하는 PowerShell 스크립트 toosilently 사용 합니다. 이런 종류의 설치를 무인 설치라고도 합니다."
services: backup
documentationcenter: " "
author: markgalioto
manager: carmonm
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/30/2017
ms.author: markgal;masaran
ms.openlocfilehash: 6b94b4a278bfcd5f8c5c363cb811bd8eec984243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a><span data-ttu-id="be307-104">Azure Backup Server v2의 무인 설치 실행</span><span class="sxs-lookup"><span data-stu-id="be307-104">Run an unattended installation of Azure Backup Server v2</span></span>

<span data-ttu-id="be307-105">자세한 내용은 방법 toorun Azure 백업 서버 v 2의 무인된 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="be307-105">Learn how toorun an unattended installation of Azure Backup Server v2.</span></span> 

<span data-ttu-id="be307-106">Azure Backup Server v1을 설치할 경우에는 이러한 단계가 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="be307-106">These steps do not apply if you are installing Azure Backup Server v1.</span></span>

## <a name="install-backup-server-v2"></a><span data-ttu-id="be307-107">Backup Server v2 설치</span><span class="sxs-lookup"><span data-stu-id="be307-107">Install Backup Server v2</span></span>

1. <span data-ttu-id="be307-108">Azure 백업 서버 v 2를 호스팅하는 hello 서버에서 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="be307-108">On hello server that hosts Azure Backup Server v2, create a text file.</span></span> <span data-ttu-id="be307-109">(만들 수 있습니다 hello 파일 메모장 또는 다른 텍스트 편집기.) MABSSetup.ini로 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="be307-109">(You can create hello file in Notepad or in another text editor.) Save hello file as MABSSetup.ini.</span></span> 

2. <span data-ttu-id="be307-110">Hello를 hello MABSSetup.ini 파일에서 코드 다음에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="be307-110">Paste hello following code in hello MABSSetup.ini file.</span></span> <span data-ttu-id="be307-111">Hello 대괄호 hello 텍스트 바꾸기 (\< \>)를 사용자 환경 값으로.</span><span class="sxs-lookup"><span data-stu-id="be307-111">Replace hello text inside hello brackets (\< \>) with values from your environment.</span></span> <span data-ttu-id="be307-112">hello 텍스트 다음은 예입니다.</span><span class="sxs-lookup"><span data-stu-id="be307-112">hello following text is an example:</span></span>

  ```
  [OPTIONS]
  UserName=administrator
  CompanyName=<Microsoft Corporation>
  SQLMachineName=localhost
  SQLInstanceName=<SQL instance name>
  SQLMachineUserName=administrator
  SQLMachinePassword=<admin password>
  SQLMachineDomainName=<machine domain>
  ReportingMachineName=localhost
  ReportingInstanceName=<reporting instance name>
  SqlAccountPassword=<admin password>
  ReportingMachineUserName=<username>
  ReportingMachinePassword=<reporting admin password>
  ReportingMachineDomainName=<domain>
  VaultCredentialFilePath=<vault credential full path and complete name>
  SecurityPassphrase=<passphrase>
  PassphraseSaveLocation=<passphrase save location>
  UseExistingSQL=<1/0 use or do not use existing SQL>
  ```

3. <span data-ttu-id="be307-113">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="be307-113">Save hello file.</span></span> <span data-ttu-id="be307-114">그런 다음 hello 설치 서버에서 관리자 권한 명령 프롬프트를에서이 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="be307-114">Then, at an elevated command prompt on hello installation server, enter this command:</span></span>

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

<span data-ttu-id="be307-115">Hello 설치에 대 한 이러한 플래그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be307-115">You can use these flags for hello installation:</span></span></br><span data-ttu-id="be307-116">
**/f**: .ini 파일 경로</span><span class="sxs-lookup"><span data-stu-id="be307-116">
**/f**: .ini file path</span></span></br><span data-ttu-id="be307-117">
**/l**: 로그 경로</span><span class="sxs-lookup"><span data-stu-id="be307-117">
**/l**: Log path</span></span></br><span data-ttu-id="be307-118">
**/i**: 설치 경로</span><span class="sxs-lookup"><span data-stu-id="be307-118">
**/i**: Installation path</span></span></br><span data-ttu-id="be307-119">
**/x**: 제거 경로</span><span class="sxs-lookup"><span data-stu-id="be307-119">
**/x**: Uninstall path</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="be307-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="be307-120">Next steps</span></span>
<span data-ttu-id="be307-121">백업 서버를 설치한 후에 대해 알아봅니다 어떻게 tooprepare 서버의 작업 보호를 시작 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="be307-121">After you install Backup Server, learn how tooprepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="be307-122">Backup Server 워크로드 준비</span><span class="sxs-lookup"><span data-stu-id="be307-122">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="be307-123">백업 서버 tooback VMware 서버를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="be307-123">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="be307-124">SQL Server를 tooback 백업 서버를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="be307-124">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="be307-125">최신 백업 저장소 tooBackup 서버 추가</span><span class="sxs-lookup"><span data-stu-id="be307-125">Add Modern Backup Storage tooBackup Server</span></span>](backup-mabs-add-storage.md)
