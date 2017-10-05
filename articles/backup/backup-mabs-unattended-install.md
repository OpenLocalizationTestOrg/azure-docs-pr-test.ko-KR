---
title: "Azure Backup Server v2 자동 설치 | Microsoft Docs"
description: "PowerShell 스크립트를 사용하여 Azure Backup Server v2를 자동으로 설치할 수 있습니다. 이런 종류의 설치를 무인 설치라고도 합니다."
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
ms.openlocfilehash: 91778a67f9ef523aa87b7918197e0d0ded0f5702
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a><span data-ttu-id="9dbcc-104">Azure Backup Server v2의 무인 설치 실행</span><span class="sxs-lookup"><span data-stu-id="9dbcc-104">Run an unattended installation of Azure Backup Server v2</span></span>

<span data-ttu-id="9dbcc-105">Azure Backup Server v2의 무인 설치를 실행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9dbcc-105">Learn how to run an unattended installation of Azure Backup Server v2.</span></span> 

<span data-ttu-id="9dbcc-106">Azure Backup Server v1을 설치할 경우에는 이러한 단계가 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9dbcc-106">These steps do not apply if you are installing Azure Backup Server v1.</span></span>

## <a name="install-backup-server-v2"></a><span data-ttu-id="9dbcc-107">Backup Server v2 설치</span><span class="sxs-lookup"><span data-stu-id="9dbcc-107">Install Backup Server v2</span></span>

1. <span data-ttu-id="9dbcc-108">Azure Backup Server v2를 호스트하는 서버에서 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9dbcc-108">On the server that hosts Azure Backup Server v2, create a text file.</span></span> <span data-ttu-id="9dbcc-109">메모장이나 다른 텍스트 편집기에서 파일을 만들 수 있습니다. 파일을 MABSSetup.ini로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9dbcc-109">(You can create the file in Notepad or in another text editor.) Save the file as MABSSetup.ini.</span></span> 

2. <span data-ttu-id="9dbcc-110">MABSSetup.ini 파일에 다음 코드를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9dbcc-110">Paste the following code in the MABSSetup.ini file.</span></span> <span data-ttu-id="9dbcc-111">대괄호(\< \>) 내부의 텍스트를 사용자 환경의 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9dbcc-111">Replace the text inside the brackets (\< \>) with values from your environment.</span></span> <span data-ttu-id="9dbcc-112">다음 텍스트는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="9dbcc-112">The following text is an example:</span></span>

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

3. <span data-ttu-id="9dbcc-113">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9dbcc-113">Save the file.</span></span> <span data-ttu-id="9dbcc-114">그다음에 설치 서버의 관리자 권한 명령 프롬프트에서 이 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9dbcc-114">Then, at an elevated command prompt on the installation server, enter this command:</span></span>

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

<span data-ttu-id="9dbcc-115">설치에 다음 플래그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dbcc-115">You can use these flags for the installation:</span></span></br><span data-ttu-id="9dbcc-116">
**/f**: .ini 파일 경로</span><span class="sxs-lookup"><span data-stu-id="9dbcc-116">
**/f**: .ini file path</span></span></br><span data-ttu-id="9dbcc-117">
**/l**: 로그 경로</span><span class="sxs-lookup"><span data-stu-id="9dbcc-117">
**/l**: Log path</span></span></br><span data-ttu-id="9dbcc-118">
**/i**: 설치 경로</span><span class="sxs-lookup"><span data-stu-id="9dbcc-118">
**/i**: Installation path</span></span></br><span data-ttu-id="9dbcc-119">
**/x**: 제거 경로</span><span class="sxs-lookup"><span data-stu-id="9dbcc-119">
**/x**: Uninstall path</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="9dbcc-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9dbcc-120">Next steps</span></span>
<span data-ttu-id="9dbcc-121">Backup Server를 설치한 후 서버를 준비하는 방법을 알아보거나 워크로드 보호를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9dbcc-121">After you install Backup Server, learn how to prepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="9dbcc-122">Backup Server 워크로드 준비</span><span class="sxs-lookup"><span data-stu-id="9dbcc-122">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="9dbcc-123">Backup Server를 사용하여 VMware 서버 백업</span><span class="sxs-lookup"><span data-stu-id="9dbcc-123">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="9dbcc-124">Backup Server를 사용하여 SQL Server 백업</span><span class="sxs-lookup"><span data-stu-id="9dbcc-124">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="9dbcc-125">Backup Server에 Modern Backup Storage 추가</span><span class="sxs-lookup"><span data-stu-id="9dbcc-125">Add Modern Backup Storage to Backup Server</span></span>](backup-mabs-add-storage.md)
