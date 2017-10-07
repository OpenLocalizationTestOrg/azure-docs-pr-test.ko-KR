---
title: "Windows에서 aaaMount Azure 파일 공유 및 액세스 hello 공유 | Microsoft Docs"
description: "Azure 파일 공유와 windows에서 hello 공유 액세스를 탑재 합니다."
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 15ac468d9d7b8e0a195b024926ed4dd9790360d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-an-azure-file-share-and-access-hello-share-in-windows"></a><span data-ttu-id="30c30-103">Azure 파일 공유 및 액세스 hello 공유 창에 탑재</span><span class="sxs-lookup"><span data-stu-id="30c30-103">Mount an Azure File share and access hello share in Windows</span></span>
<span data-ttu-id="30c30-104">[Azure 파일 저장소](storage-dotnet-how-to-use-files.md) 는 Microsoft의 쉬운 toouse 클라우드 파일 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy toouse cloud file system.</span></span> <span data-ttu-id="30c30-105">Azure 파일 공유는 Windows 및 Windows Server에 탑재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-105">Azure File shares can be mounted in Windows and Windows Server.</span></span> <span data-ttu-id="30c30-106">이 문서에서는 세 가지 방법으로 toomount Azure 파일 공유에서 Windows: PowerShell을 통해 및 hello 명령 프롬프트를 통해 파일 탐색기 UI hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-106">This article shows three different ways toomount an Azure File share on Windows: with hello File Explorer UI, via PowerShell, and via hello Command Prompt.</span></span> 

<span data-ttu-id="30c30-107">Azure 파일 공유 hello 외부, 같은 온-프레미스 또는 다른 Azure 지역에 호스팅되는 Azure 지역 순서 toomount에서 OS hello SMB 3.0을 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-107">In order toomount an Azure File share outside of hello Azure region it is hosted in, such as on-premises or in a different Azure region, hello OS must support SMB 3.0.</span></span> 

<span data-ttu-id="30c30-108">Azure 파일 공유는 OS 버전에 따라 온-프레미스 또는 Azure VM의 Windows 컴퓨터에 탑재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-108">Azure File share can be mounted on Windows machine either on-premises or in Azure VM depending on OS version.</span></span> <span data-ttu-id="30c30-109">아래 표에서 hello를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-109">Below table illustrates hello</span></span> 

| <span data-ttu-id="30c30-110">Windows 버전</span><span class="sxs-lookup"><span data-stu-id="30c30-110">Windows Version</span></span>        | <span data-ttu-id="30c30-111">SMB 버전</span><span class="sxs-lookup"><span data-stu-id="30c30-111">SMB Version</span></span> |<span data-ttu-id="30c30-112">Azure VM에 탑재 가능</span><span class="sxs-lookup"><span data-stu-id="30c30-112">Mountable On Azure VM</span></span>|<span data-ttu-id="30c30-113">온-프레미스에 탑재 가능</span><span class="sxs-lookup"><span data-stu-id="30c30-113">Mountable On-Premise</span></span>|
|------------------------|-------------|---------------------|---------------------|
| <span data-ttu-id="30c30-114">윈도우 7</span><span class="sxs-lookup"><span data-stu-id="30c30-114">Windows 7</span></span>              | <span data-ttu-id="30c30-115">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="30c30-115">SMB 2.1</span></span>     | <span data-ttu-id="30c30-116">예</span><span class="sxs-lookup"><span data-stu-id="30c30-116">Yes</span></span>                 | <span data-ttu-id="30c30-117">아니요</span><span class="sxs-lookup"><span data-stu-id="30c30-117">No</span></span>                  |
| <span data-ttu-id="30c30-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="30c30-118">Windows Server 2008 R2</span></span> | <span data-ttu-id="30c30-119">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="30c30-119">SMB 2.1</span></span>     | <span data-ttu-id="30c30-120">예</span><span class="sxs-lookup"><span data-stu-id="30c30-120">Yes</span></span>                 | <span data-ttu-id="30c30-121">아니요</span><span class="sxs-lookup"><span data-stu-id="30c30-121">No</span></span>                  |
| <span data-ttu-id="30c30-122">Windows 8</span><span class="sxs-lookup"><span data-stu-id="30c30-122">Windows 8</span></span>              | <span data-ttu-id="30c30-123">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="30c30-123">SMB 3.0</span></span>     | <span data-ttu-id="30c30-124">예</span><span class="sxs-lookup"><span data-stu-id="30c30-124">Yes</span></span>                 | <span data-ttu-id="30c30-125">예</span><span class="sxs-lookup"><span data-stu-id="30c30-125">Yes</span></span>                 |
| <span data-ttu-id="30c30-126">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="30c30-126">Windows Server 2012</span></span>    | <span data-ttu-id="30c30-127">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="30c30-127">SMB 3.0</span></span>     | <span data-ttu-id="30c30-128">예</span><span class="sxs-lookup"><span data-stu-id="30c30-128">Yes</span></span>                 | <span data-ttu-id="30c30-129">예</span><span class="sxs-lookup"><span data-stu-id="30c30-129">Yes</span></span>                 |
| <span data-ttu-id="30c30-130">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="30c30-130">Windows Server 2012 R2</span></span> | <span data-ttu-id="30c30-131">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="30c30-131">SMB 3.0</span></span>     | <span data-ttu-id="30c30-132">예</span><span class="sxs-lookup"><span data-stu-id="30c30-132">Yes</span></span>                 | <span data-ttu-id="30c30-133">예</span><span class="sxs-lookup"><span data-stu-id="30c30-133">Yes</span></span>                 |
| <span data-ttu-id="30c30-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="30c30-134">Windows 10</span></span>             | <span data-ttu-id="30c30-135">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="30c30-135">SMB 3.0</span></span>     | <span data-ttu-id="30c30-136">예</span><span class="sxs-lookup"><span data-stu-id="30c30-136">Yes</span></span>                 | <span data-ttu-id="30c30-137">예</span><span class="sxs-lookup"><span data-stu-id="30c30-137">Yes</span></span>                 |

> [!Note]  
> <span data-ttu-id="30c30-138">항상 기록 권장 사용자의 Windows 버전에 대 한 가장 최근의 KB hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-138">We always recommend taking hello most recent KB for your version of Windows.</span></span>

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a><span data-ttu-id="30c30-139"></a>Windows에 Azure 파일 공유를 탑재하기 위한 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="30c30-139"></a>Prerequisites for Mounting Azure File Share with Windows</span></span> 
* <span data-ttu-id="30c30-140">**저장소 계정 이름**: toomount Azure 파일 공유, hello 저장소 계정의 이름을 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-140">**Storage Account Name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="30c30-141">**저장소 계정 키**: toomount Azure 파일 공유, 기본 (또는 보조) 저장소 키 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-141">**Storage Account Key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="30c30-142">SAS 키는 현재 탑재를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-142">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="30c30-143">**445 포트가 열려 있는지 확인**: Azure File Storage는 SMB 프로토콜을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-143">**Ensure port 445 is open**: Azure File storage uses SMB protocol.</span></span> <span data-ttu-id="30c30-144">Toosee 방화벽이 클라이언트 컴퓨터에서 TCP 포트 445를 차단 하지 않는지 선택 SMB TCP 포트 445-를 통해 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-144">SMB communicates over TCP port 445 - check toosee if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-hello-azure-file-share-with-file-explorer"></a><span data-ttu-id="30c30-145">파일 탐색기로 hello Azure 파일 공유를 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-145">Mount hello Azure File share with File Explorer</span></span>
> [!Note]  
> <span data-ttu-id="30c30-146">지침에 따라 hello는 Windows 10에서 표시 되 고 이전 버전에서 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-146">Note that hello following instructions are shown on Windows 10 and may differ slightly on older releases.</span></span> 

1. <span data-ttu-id="30c30-147">**파일 탐색기를 열고**: hello 시작 메뉴에서에서 열어 또는 Win + E 바로 가기 키를 눌러이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-147">**Open File Explorer**: This can be done by opening from hello Start Menu, or by pressing Win+E shortcut.</span></span>

2. <span data-ttu-id="30c30-148">**Hello 창의 hello 왼쪽에 toohello "이 PC" 항목을 이동 합니다. 이렇게 하면 hello 리본 메뉴에서 사용할 수 있는 hello 메뉴 변경 됩니다. Hello 컴퓨터 메뉴에서 "네트워크 드라이브 맵"를 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-148">**Navigate toohello "This PC" item on hello left-hand side of hello window. This will change hello menus available in hello ribbon. Under hello Computer menu, select "Map Network Drive"**.</span></span>
    
    ![Hello "네트워크 드라이브 맵" 드롭다운 메뉴의 스크린 샷](media/storage-file-how-to-use-files-windows/1_MountOnWindows10.png)

3. <span data-ttu-id="30c30-150">**Hello hello Azure 포털의에서 hello "연결" 창에서 UNC 경로 복사**: 자세한 설명은 어떻게 toofind이 내용은 [여기](storage-file-how-to-use-files-portal.md#connect-to-file-share)합니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-150">**Copy hello UNC path from hello "Connect" pane in hello Azure portal**: A detailed description of how toofind this information can be found [here](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span></span>

    ![hello Azure 파일 저장소 연결 창에서 hello UNC 경로](media/storage-file-how-to-use-files-windows/portal_netuse_connect.png)

4. <span data-ttu-id="30c30-152">**Hello 드라이브 문자를 선택 하 고 hello UNC 경로 입력 합니다.**</span><span class="sxs-lookup"><span data-stu-id="30c30-152">**Select hello Drive letter and enter hello UNC path.**</span></span> 
    
    ![Hello "네트워크 드라이브 맵" 대화 상자 스크린 샷](media/storage-file-how-to-use-files-windows/2_MountOnWindows10.png)

5. <span data-ttu-id="30c30-154">**앞에 추가 하는 저장소 계정 이름을 사용 하 여 hello `Azure\` hello 사용자 이름 및 암호 hello와 저장소 계정 키입니다.**</span><span class="sxs-lookup"><span data-stu-id="30c30-154">**Use hello Storage Account Name prepended with `Azure\` as hello username and a Storage Account Key as hello password.**</span></span>
    
    ![Hello 네트워크 자격 증명 대화 상자의 스크린 샷](media/storage-file-how-to-use-files-windows/3_MountOnWindows10.png)

6. <span data-ttu-id="30c30-156">**Azure 파일 공유를 원하는 대로 사용합니다**.</span><span class="sxs-lookup"><span data-stu-id="30c30-156">**Use Azure File share as desired**.</span></span>
    
    ![현재 탑재된 Azure 파일 공유](media/storage-file-how-to-use-files-windows/4_MountOnWindows10.png)

7. <span data-ttu-id="30c30-158">**준비 toodismount (하거나 때 연결 끊기) hello Azure 파일 공유를 하면 파일 탐색기에서 "네트워크 위치" hello 아래 hello 공유에 대 한 hello 항목을 마우스 오른쪽 단추로 클릭 하 고 "연결 끊기"를 선택 하 여**합니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-158">**When you are ready toodismount (or disconnect) hello Azure File share, you can do so by right clicking on hello entry for hello share under hello "Network locations" in File Explorer and selecting "Disconnect"**.</span></span>

## <a name="mount-hello-azure-file-share-with-powershell"></a><span data-ttu-id="30c30-159">PowerShell과 함께 hello Azure 파일 공유를 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-159">Mount hello Azure File share with PowerShell</span></span>
1. <span data-ttu-id="30c30-160">**사용 하 여 hello 다음 명령은 toomount hello Azure 파일 공유**: tooreplace 기억 `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` hello 적절 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-160">**Use hello following command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with hello proper information.</span></span>

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. <span data-ttu-id="30c30-161">**필요에 따라 사용 하 여 hello Azure 파일 공유**합니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-161">**Use hello Azure File share as desired**.</span></span>

3. <span data-ttu-id="30c30-162">**작업을 완료 하는 경우 다음 명령을 hello를 사용 하 여 hello Azure 파일 공유를 분리**합니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-162">**When you are finished, dismount hello Azure File share using hello following command**.</span></span>

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> <span data-ttu-id="30c30-163">Hello를 사용할 수 있습니다 `-Persist` 매개 변수와 `New-PSDrive` toomake hello Azure 파일 공유 표시 toohello 나머지 hello 탑재 하는 동안 운영 체제.</span><span class="sxs-lookup"><span data-stu-id="30c30-163">You may use hello `-Persist` parameter on `New-PSDrive` toomake hello Azure File share visible toohello rest of hello OS while mounted.</span></span>

## <a name="mount-hello-azure-file-share-with-command-prompt"></a><span data-ttu-id="30c30-164">명령 프롬프트와 hello Azure 파일 공유를 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-164">Mount hello Azure File share with Command Prompt</span></span>
1. <span data-ttu-id="30c30-165">**사용 하 여 hello 다음 명령은 toomount hello Azure 파일 공유**: tooreplace 기억 `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` hello 적절 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-165">**Use hello following command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with hello proper information.</span></span>

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. <span data-ttu-id="30c30-166">**필요에 따라 사용 하 여 hello Azure 파일 공유**합니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-166">**Use hello Azure File share as desired**.</span></span>

3. <span data-ttu-id="30c30-167">**작업을 완료 하는 경우 다음 명령을 hello를 사용 하 여 hello Azure 파일 공유를 분리**합니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-167">**When you are finished, dismount hello Azure File share using hello following command**.</span></span>

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> <span data-ttu-id="30c30-168">Windows에서 hello 자격 증명을 유지 하 여을 다시 시작할 때 hello Azure 파일 공유 tooautomatically 다시 연결을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-168">You can configure hello Azure File share tooautomatically reconnect on reboot by persisting hello credentials in Windows.</span></span> <span data-ttu-id="30c30-169">다음 명령을 hello hello 자격 증명을 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-169">hello following command will persist hello credentials:</span></span>
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a><span data-ttu-id="30c30-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="30c30-170">Next steps</span></span>
<span data-ttu-id="30c30-171">Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="30c30-171">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="30c30-172">FAQ</span><span class="sxs-lookup"><span data-stu-id="30c30-172">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="30c30-173">문제 해결</span><span class="sxs-lookup"><span data-stu-id="30c30-173">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="30c30-174">개념 문서 및 비디오</span><span class="sxs-lookup"><span data-stu-id="30c30-174">Conceptual articles and videos</span></span>
* [<span data-ttu-id="30c30-175">Azure File Storage: 원활한 Windows 및 Linux용 클라우드 SMB 파일 시스템(영문)</span><span class="sxs-lookup"><span data-stu-id="30c30-175">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="30c30-176">어떻게 toouse Linux로 Azure 파일 저장소</span><span class="sxs-lookup"><span data-stu-id="30c30-176">How toouse Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a><span data-ttu-id="30c30-177">Azure File Storage용 도구 지원</span><span class="sxs-lookup"><span data-stu-id="30c30-177">Tooling support for Azure File storage</span></span>
* [<span data-ttu-id="30c30-178">Azure 저장소와 함께 Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="30c30-178">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="30c30-179">어떻게 toouse AzCopy Microsoft Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="30c30-179">How toouse AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="30c30-180">Hello Azure CLI를 사용 하 여 Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="30c30-180">Using hello Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="30c30-181">Azure File Storage 문제 해결</span><span class="sxs-lookup"><span data-stu-id="30c30-181">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="blog-posts"></a><span data-ttu-id="30c30-182">블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="30c30-182">Blog posts</span></span>
* [<span data-ttu-id="30c30-183">Azure 파일 저장소 일반적으로 사용 가능(영문)</span><span class="sxs-lookup"><span data-stu-id="30c30-183">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="30c30-184">Azure File Storage 내부 구조(영문)</span><span class="sxs-lookup"><span data-stu-id="30c30-184">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="30c30-185">Microsoft Azure 파일 서비스 소개</span><span class="sxs-lookup"><span data-stu-id="30c30-185">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="30c30-186">마이그레이션 데이터 tooAzure 파일</span><span class="sxs-lookup"><span data-stu-id="30c30-186">Migrating data tooAzure File </span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="30c30-187">참조</span><span class="sxs-lookup"><span data-stu-id="30c30-187">Reference</span></span>
* [<span data-ttu-id="30c30-188">Storage Client Library for .NET 참조</span><span class="sxs-lookup"><span data-stu-id="30c30-188">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="30c30-189">파일 서비스 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="30c30-189">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
