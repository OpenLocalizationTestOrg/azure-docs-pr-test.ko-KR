---
title: "Azure 파일 공유를 탑재하고 Windows에서 공유에 액세스 | Microsoft Docs"
description: "Azure 파일 공유를 탑재하고 Windows에서 공유에 액세스합니다."
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
ms.openlocfilehash: 67b8e2e0039c8bc63f50f177e3c0d18b07df45e6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="mount-an-azure-file-share-and-access-the-share-in-windows"></a><span data-ttu-id="657f2-103">Azure 파일 공유를 탑재하고 Windows에서 공유에 액세스</span><span class="sxs-lookup"><span data-stu-id="657f2-103">Mount an Azure File share and access the share in Windows</span></span>
<span data-ttu-id="657f2-104">[Azure File Storage](../storage-dotnet-how-to-use-files.md)는 사용하기 쉬운 Microsoft 클라우드 파일 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="657f2-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) is Microsoft's easy to use cloud file system.</span></span> <span data-ttu-id="657f2-105">Azure 파일 공유는 Windows 및 Windows Server에 탑재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="657f2-105">Azure File shares can be mounted in Windows and Windows Server.</span></span> <span data-ttu-id="657f2-106">이 문서에서는 세 가지 방법, 즉 파일 탐색기 UI, PowerShell 및 명령 프롬프트를 사용하여 Windows에 Azure File 공유를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="657f2-106">This article shows three different ways to mount an Azure File share on Windows: with the File Explorer UI, via PowerShell, and via the Command Prompt.</span></span> 

<span data-ttu-id="657f2-107">온-프레미스 또는 다른 Azure 지역에서 호스팅되는 Azure 지역의 외부에 Azure 파일 공유를 탑재하려면 OS에서 SMB 3.0을 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="657f2-107">In order to mount an Azure File share outside of the Azure region it is hosted in, such as on-premises or in a different Azure region, the OS must support SMB 3.0.</span></span> 

<span data-ttu-id="657f2-108">Azure 파일 공유는 OS 버전에 따라 온-프레미스 또는 Azure VM의 Windows 컴퓨터에 탑재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="657f2-108">Azure File share can be mounted on Windows machine either on-premises or in Azure VM depending on OS version.</span></span> <span data-ttu-id="657f2-109">다음 표에서 자세히 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="657f2-109">Below table illustrates the</span></span> 

| <span data-ttu-id="657f2-110">Windows 버전</span><span class="sxs-lookup"><span data-stu-id="657f2-110">Windows Version</span></span>        | <span data-ttu-id="657f2-111">SMB 버전</span><span class="sxs-lookup"><span data-stu-id="657f2-111">SMB Version</span></span> |<span data-ttu-id="657f2-112">Azure VM에 탑재 가능</span><span class="sxs-lookup"><span data-stu-id="657f2-112">Mountable On Azure VM</span></span>|<span data-ttu-id="657f2-113">온-프레미스에 탑재 가능</span><span class="sxs-lookup"><span data-stu-id="657f2-113">Mountable On-Premise</span></span>|
|------------------------|-------------|---------------------|---------------------|
| <span data-ttu-id="657f2-114">윈도우 7</span><span class="sxs-lookup"><span data-stu-id="657f2-114">Windows 7</span></span>              | <span data-ttu-id="657f2-115">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="657f2-115">SMB 2.1</span></span>     | <span data-ttu-id="657f2-116">예</span><span class="sxs-lookup"><span data-stu-id="657f2-116">Yes</span></span>                 | <span data-ttu-id="657f2-117">아니요</span><span class="sxs-lookup"><span data-stu-id="657f2-117">No</span></span>                  |
| <span data-ttu-id="657f2-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="657f2-118">Windows Server 2008 R2</span></span> | <span data-ttu-id="657f2-119">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="657f2-119">SMB 2.1</span></span>     | <span data-ttu-id="657f2-120">예</span><span class="sxs-lookup"><span data-stu-id="657f2-120">Yes</span></span>                 | <span data-ttu-id="657f2-121">아니요</span><span class="sxs-lookup"><span data-stu-id="657f2-121">No</span></span>                  |
| <span data-ttu-id="657f2-122">Windows 8</span><span class="sxs-lookup"><span data-stu-id="657f2-122">Windows 8</span></span>              | <span data-ttu-id="657f2-123">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="657f2-123">SMB 3.0</span></span>     | <span data-ttu-id="657f2-124">예</span><span class="sxs-lookup"><span data-stu-id="657f2-124">Yes</span></span>                 | <span data-ttu-id="657f2-125">예</span><span class="sxs-lookup"><span data-stu-id="657f2-125">Yes</span></span>                 |
| <span data-ttu-id="657f2-126">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="657f2-126">Windows Server 2012</span></span>    | <span data-ttu-id="657f2-127">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="657f2-127">SMB 3.0</span></span>     | <span data-ttu-id="657f2-128">예</span><span class="sxs-lookup"><span data-stu-id="657f2-128">Yes</span></span>                 | <span data-ttu-id="657f2-129">예</span><span class="sxs-lookup"><span data-stu-id="657f2-129">Yes</span></span>                 |
| <span data-ttu-id="657f2-130">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="657f2-130">Windows Server 2012 R2</span></span> | <span data-ttu-id="657f2-131">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="657f2-131">SMB 3.0</span></span>     | <span data-ttu-id="657f2-132">예</span><span class="sxs-lookup"><span data-stu-id="657f2-132">Yes</span></span>                 | <span data-ttu-id="657f2-133">예</span><span class="sxs-lookup"><span data-stu-id="657f2-133">Yes</span></span>                 |
| <span data-ttu-id="657f2-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="657f2-134">Windows 10</span></span>             | <span data-ttu-id="657f2-135">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="657f2-135">SMB 3.0</span></span>     | <span data-ttu-id="657f2-136">예</span><span class="sxs-lookup"><span data-stu-id="657f2-136">Yes</span></span>                 | <span data-ttu-id="657f2-137">예</span><span class="sxs-lookup"><span data-stu-id="657f2-137">Yes</span></span>                 |

> [!Note]  
> <span data-ttu-id="657f2-138">사용자의 Windows 버전에 대해 가장 최근의 KB를 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="657f2-138">We always recommend taking the most recent KB for your version of Windows.</span></span>

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a><span data-ttu-id="657f2-139"></a>Windows에 Azure 파일 공유를 탑재하기 위한 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="657f2-139"></a>Prerequisites for Mounting Azure File Share with Windows</span></span> 
* <span data-ttu-id="657f2-140">**저장소 계정 이름**: Azure 파일 공유를 탑재하려면 저장소 계정의 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="657f2-140">**Storage Account Name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="657f2-141">**저장소 계정 키**: Azure 파일 공유를 탑재하려면 기본(또는 보조) 저장소 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="657f2-141">**Storage Account Key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="657f2-142">SAS 키는 현재 탑재를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="657f2-142">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="657f2-143">**445 포트가 열려 있는지 확인**: Azure File Storage는 SMB 프로토콜을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="657f2-143">**Ensure port 445 is open**: Azure File storage uses SMB protocol.</span></span> <span data-ttu-id="657f2-144">SMB는 445 TCP 포트를 통해 통신합니다. 클라이언트 컴퓨터에서 방화벽이 445 TCP 포트를 차단하고 있지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="657f2-144">SMB communicates over TCP port 445 - check to see if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-the-azure-file-share-with-file-explorer"></a><span data-ttu-id="657f2-145">파일 탐색기를 통해 Azure 파일 공유 탑재</span><span class="sxs-lookup"><span data-stu-id="657f2-145">Mount the Azure File share with File Explorer</span></span>
> [!Note]  
> <span data-ttu-id="657f2-146">다음 지침은 Windows 10에서 보여 주는 것이며, 이전 릴리스와 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="657f2-146">Note that the following instructions are shown on Windows 10 and may differ slightly on older releases.</span></span> 

1. <span data-ttu-id="657f2-147">**파일 탐색기를 엽니다**. 이 작업은 [시작] 메뉴에서 열거나 Win+E 바로 가기 키를 눌러 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="657f2-147">**Open File Explorer**: This can be done by opening from the Start Menu, or by pressing Win+E shortcut.</span></span>

2. <span data-ttu-id="657f2-148">**창 왼쪽에 있는 "이 PC" 항목으로 이동합니다. 이렇게 하면 리본에서 사용할 수 있는 메뉴가 변경됩니다. [컴퓨터] 메뉴 아래에서 "네트워크 드라이브 연결"을 선택합니다**.</span><span class="sxs-lookup"><span data-stu-id="657f2-148">**Navigate to the "This PC" item on the left-hand side of the window. This will change the menus available in the ribbon. Under the Computer menu, select "Map Network Drive"**.</span></span>
    
    !["네트워크 드라이브 연결" 드롭다운 메뉴의 스크린샷](./media/storage-how-to-use-files-windows/1_MountOnWindows10.png)

3. <span data-ttu-id="657f2-150">**Azure Portal의 "연결" 창에서 UNC 경로 복사합니다**. 이 정보를 찾는 방법에 대한 자세한 설명은 [여기서](storage-how-to-use-files-portal.md#connect-to-file-share) 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="657f2-150">**Copy the UNC path from the "Connect" pane in the Azure portal**: A detailed description of how to find this information can be found [here](storage-how-to-use-files-portal.md#connect-to-file-share).</span></span>

    ![Azure File Storage 연결 창의 UNC 경로](./media/storage-how-to-use-files-windows/portal_netuse_connect.png)

4. <span data-ttu-id="657f2-152">**드라이브 문자를 선택하고 UNC 경로를 입력합니다.**</span><span class="sxs-lookup"><span data-stu-id="657f2-152">**Select the Drive letter and enter the UNC path.**</span></span> 
    
    !["네트워크 드라이브 연결" 대화 상자의 스크린샷](./media/storage-how-to-use-files-windows/2_MountOnWindows10.png)

5. <span data-ttu-id="657f2-154">**사용자 이름으로 `Azure\`가 앞에 붙은 저장소 계정 이름을 사용하고, 암호로 저장소 계정 키를 사용합니다.**</span><span class="sxs-lookup"><span data-stu-id="657f2-154">**Use the Storage Account Name prepended with `Azure\` as the username and a Storage Account Key as the password.**</span></span>
    
    ![네트워크 자격 증명 대화 상자의 스크린샷](./media/storage-how-to-use-files-windows/3_MountOnWindows10.png)

6. <span data-ttu-id="657f2-156">**Azure 파일 공유를 원하는 대로 사용합니다**.</span><span class="sxs-lookup"><span data-stu-id="657f2-156">**Use Azure File share as desired**.</span></span>
    
    ![현재 탑재된 Azure 파일 공유](./media/storage-how-to-use-files-windows/4_MountOnWindows10.png)

7. <span data-ttu-id="657f2-158">**Azure 파일 공유를 분리(또는 연결 해제)할 준비가 되면 파일 탐색기의 "네트워크 위치" 아래에서 공유 항목을 마우스 오른쪽 단추로 클릭하고 "연결 해제"를 선택하여 Azure 파일 공유를 탑재 해제할 수 있습니다**.</span><span class="sxs-lookup"><span data-stu-id="657f2-158">**When you are ready to dismount (or disconnect) the Azure File share, you can do so by right clicking on the entry for the share under the "Network locations" in File Explorer and selecting "Disconnect"**.</span></span>

## <a name="mount-the-azure-file-share-with-powershell"></a><span data-ttu-id="657f2-159">PowerShell을 통해 Azure 파일 공유 탑재</span><span class="sxs-lookup"><span data-stu-id="657f2-159">Mount the Azure File share with PowerShell</span></span>
1. <span data-ttu-id="657f2-160">**다음 명령을 사용하여 Azure 파일 공유를 탑재합니다**. `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>`를 적절한 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="657f2-160">**Use the following command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with the proper information.</span></span>

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. <span data-ttu-id="657f2-161">**Azure 파일 공유를 원하는 대로 사용합니다**.</span><span class="sxs-lookup"><span data-stu-id="657f2-161">**Use the Azure File share as desired**.</span></span>

3. <span data-ttu-id="657f2-162">**완료되면 다음 명령을 사용하여 Azure 파일 공유를 연결 해제합니다**.</span><span class="sxs-lookup"><span data-stu-id="657f2-162">**When you are finished, dismount the Azure File share using the following command**.</span></span>

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> <span data-ttu-id="657f2-163">Azure 파일 공유를 탑재하는 동안 나머지 OS에서 볼 수 있도록 `New-PSDrive`에서 `-Persist` 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="657f2-163">You may use the `-Persist` parameter on `New-PSDrive` to make the Azure File share visible to the rest of the OS while mounted.</span></span>

## <a name="mount-the-azure-file-share-with-command-prompt"></a><span data-ttu-id="657f2-164">명령 프롬프트를 통해 Azure 파일 공유 탑재</span><span class="sxs-lookup"><span data-stu-id="657f2-164">Mount the Azure File share with Command Prompt</span></span>
1. <span data-ttu-id="657f2-165">**다음 명령을 사용하여 Azure 파일 공유를 탑재합니다**. `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>`를 적절한 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="657f2-165">**Use the following command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with the proper information.</span></span>

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. <span data-ttu-id="657f2-166">**Azure 파일 공유를 원하는 대로 사용합니다**.</span><span class="sxs-lookup"><span data-stu-id="657f2-166">**Use the Azure File share as desired**.</span></span>

3. <span data-ttu-id="657f2-167">**완료되면 다음 명령을 사용하여 Azure 파일 공유를 연결 해제합니다**.</span><span class="sxs-lookup"><span data-stu-id="657f2-167">**When you are finished, dismount the Azure File share using the following command**.</span></span>

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> <span data-ttu-id="657f2-168">Windows에서 자격 증명을 유지하여 다시 부팅할 때 Azure 파일 공유가 자동으로 다시 연결되도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="657f2-168">You can configure the Azure File share to automatically reconnect on reboot by persisting the credentials in Windows.</span></span> <span data-ttu-id="657f2-169">자격 증명을 유지하기 위한 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="657f2-169">The following command will persist the credentials:</span></span>
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a><span data-ttu-id="657f2-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="657f2-170">Next steps</span></span>
<span data-ttu-id="657f2-171">Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="657f2-171">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="657f2-172">FAQ</span><span class="sxs-lookup"><span data-stu-id="657f2-172">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="657f2-173">Windows에서 문제 해결</span><span class="sxs-lookup"><span data-stu-id="657f2-173">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="657f2-174">개념 문서 및 비디오</span><span class="sxs-lookup"><span data-stu-id="657f2-174">Conceptual articles and videos</span></span>
* [<span data-ttu-id="657f2-175">Azure File Storage: 원활한 Windows 및 Linux용 클라우드 SMB 파일 시스템(영문)</span><span class="sxs-lookup"><span data-stu-id="657f2-175">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="657f2-176">Linux에서 Azure File Storage 사용 방법</span><span class="sxs-lookup"><span data-stu-id="657f2-176">How to use Azure File storage with Linux</span></span>](../storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a><span data-ttu-id="657f2-177">Azure File Storage용 도구 지원</span><span class="sxs-lookup"><span data-stu-id="657f2-177">Tooling support for Azure File storage</span></span>
* [<span data-ttu-id="657f2-178">Microsoft Azure 저장소와 함께 AzCopy를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="657f2-178">How to use AzCopy with Microsoft Azure Storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="657f2-179">Azure 저장소에서 Azure CLI 사용</span><span class="sxs-lookup"><span data-stu-id="657f2-179">Using the Azure CLI with Azure Storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [<span data-ttu-id="657f2-180">Azure File Storage 문제 해결 - Windows</span><span class="sxs-lookup"><span data-stu-id="657f2-180">Troubleshooting Azure File storage problems - Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)
* [<span data-ttu-id="657f2-181">Azure File Storage 문제 해결 - Linux</span><span class="sxs-lookup"><span data-stu-id="657f2-181">Troubleshooting Azure File storage problems - Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)

### <a name="blog-posts"></a><span data-ttu-id="657f2-182">블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="657f2-182">Blog posts</span></span>
* [<span data-ttu-id="657f2-183">Azure 파일 저장소 일반적으로 사용 가능(영문)</span><span class="sxs-lookup"><span data-stu-id="657f2-183">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="657f2-184">Azure File Storage 내부 구조(영문)</span><span class="sxs-lookup"><span data-stu-id="657f2-184">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="657f2-185">Microsoft Azure 파일 서비스 소개</span><span class="sxs-lookup"><span data-stu-id="657f2-185">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="657f2-186">Azure 파일로 데이터 마이그레이션(영문)</span><span class="sxs-lookup"><span data-stu-id="657f2-186">Migrating data to Azure File </span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="657f2-187">참조</span><span class="sxs-lookup"><span data-stu-id="657f2-187">Reference</span></span>
* [<span data-ttu-id="657f2-188">Storage Client Library for .NET 참조</span><span class="sxs-lookup"><span data-stu-id="657f2-188">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="657f2-189">파일 서비스 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="657f2-189">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
