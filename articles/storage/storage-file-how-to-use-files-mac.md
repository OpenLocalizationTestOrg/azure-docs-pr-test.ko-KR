---
title: "SMB 통한 macOS aaaMount Azure 파일 공유 | Microsoft Docs"
description: "Azure 파일 toomount SMB를 통한 macOS와 공유 하는 방법을 알아봅니다."
services: storage
documentationcenter: 
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
ms.openlocfilehash: 7b4924cb42247470521c1ae8b9d03ab1756996e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a><span data-ttu-id="4bfdf-103">macOS에서 SMB를 통해 Azure 파일 공유 탑재</span><span class="sxs-lookup"><span data-stu-id="4bfdf-103">Mount Azure File share over SMB with macOS</span></span>
<span data-ttu-id="4bfdf-104">[Azure 파일 저장소](storage-dotnet-how-to-use-files.md) 업계 표준 hello를 사용 하 여 hello Azure에서에서 toocreate 및 사용 하 여 네트워크 파일 공유를 사용 하면 Microsoft의 서비스는 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bfdf-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's service that enables you toocreate and use network file shares in hello Azure using hello industry standard.</span></span> <span data-ttu-id="4bfdf-105">Azure 파일 공유는 macOS Sierra(10.12) 및 El Capitan(10.11)에서 탑재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bfdf-105">Azure File shares can be mounted in macOS Sierra (10.12) and El Capitan (10.11).</span></span> <span data-ttu-id="4bfdf-106">이 문서 hello Finder UI 및 터미널 hello를 사용 하 여와 macOS에서 두 가지 방법으로 toomount Azure 파일 공유를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bfdf-106">This article shows two different ways toomount an Azure File share on macOS with hello Finder UI and using hello Terminal.</span></span>

> [!Note]  
> <span data-ttu-id="4bfdf-107">SMB를 통해 Azure 파일 공유를 탑재하기 전에 SMB 패킷 서명을 사용하지 않도록 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4bfdf-107">Before mounting an Azure File share over SMB, we recommend disabling SMB packet signing.</span></span> <span data-ttu-id="4bfdf-108">이렇게 하지 않으면 macOS에서 hello Azure 파일 공유에 액세스할 때 성능이 저하 얻을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bfdf-108">Not doing so may yield poor performance when accessing hello Azure File share from macOS.</span></span> <span data-ttu-id="4bfdf-109">이 연결의 hello 보안에는 영향을 주지 않는 하므로 SMB 연결이 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bfdf-109">Your SMB connection will be encrypted, so this does not affect hello security of your connection.</span></span> <span data-ttu-id="4bfdf-110">Hello 터미널에서 hello 다음 명령이 비활성화 됩니다 SMB 패킷 서명에서 설명한 대로 [Apple 지원 문서 SMB 패킷 서명 사용 하지 않도록 설정에](https://support.apple.com/HT205926):</span><span class="sxs-lookup"><span data-stu-id="4bfdf-110">From hello terminal, hello following commands will disable SMB packet signing, as described by this [Apple support article on disabling SMB packet signing](https://support.apple.com/HT205926):</span></span>  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a><span data-ttu-id="4bfdf-111">macOS에 Azure 파일 공유를 탑재하기 위한 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="4bfdf-111">Prerequisites for mounting an Azure File share on macOS</span></span>
* <span data-ttu-id="4bfdf-112">**저장소 계정 이름**: toomount Azure 파일 공유, hello 저장소 계정의 이름을 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bfdf-112">**Storage account name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="4bfdf-113">**저장소 계정 키**: toomount Azure 파일 공유, 기본 (또는 보조) 저장소 키 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bfdf-113">**Storage account key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="4bfdf-114">SAS 키는 현재 탑재를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4bfdf-114">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="4bfdf-115">**445 포트가 열려 있는지 확인**: SMB는 445 TCP 포트를 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="4bfdf-115">**Ensure port 445 is open**: SMB communicates over TCP port 445.</span></span> <span data-ttu-id="4bfdf-116">클라이언트 컴퓨터 (hello Mac)에서 toomake 방화벽 TCP 포트 445를 차단 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bfdf-116">On your client machine (hello Mac), check toomake sure your firewall is not blocking TCP port 445.</span></span>

## <a name="mount-an-azure-file-share-via-finder"></a><span data-ttu-id="4bfdf-117">찾기를 통해 Azure 파일 공유 탑재</span><span class="sxs-lookup"><span data-stu-id="4bfdf-117">Mount an Azure File share via Finder</span></span>
1. <span data-ttu-id="4bfdf-118">**파인더를 열고**: 검색기는 기본적으로 macOS에서 열려 있지만 hello에서 현재 선택한 응용 프로그램 hello "macOS 맞서게 아이콘"를 클릭 하 여 hello 도킹은 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bfdf-118">**Open Finder**: Finder is open on macOS by default, but you can ensure it is hello currently selected application by clicking hello "macOS face icon" on hello dock:</span></span>  
    <span data-ttu-id="4bfdf-119">![hello macOS 맞서게 아이콘](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span><span class="sxs-lookup"><span data-stu-id="4bfdf-119">![hello macOS face icon](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span></span>

2. <span data-ttu-id="4bfdf-120">**"연결 tooServer" hello "Go" 메뉴에서에서 선택**: hello에서 hello UNC 경로 사용 하 여 [필수 구성 요소](#preq), hello 시작 부분에 이중 백슬래시를 변환 (`\\`) 너무`smb://` 및 다른 모든 백슬래시 (`\`) tooforwards 슬래시 (`/`).</span><span class="sxs-lookup"><span data-stu-id="4bfdf-120">**Select "Connect tooServer" from hello "Go" Menu**: Using hello UNC path from hello [prerequisites](#preq), convert hello beginning double backslash (`\\`) too`smb://` and all other backslashes (`\`) tooforwards slashes (`/`).</span></span> <span data-ttu-id="4bfdf-121">링크 hello 다음과 같습니다: ![hello "tooServer 연결" 대화 상자](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span><span class="sxs-lookup"><span data-stu-id="4bfdf-121">Your link should look like hello following: ![hello "Connect tooServer" dialog](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span></span>

3. <span data-ttu-id="4bfdf-122">**사용 하 여 hello 공유 이름 및 저장소 계정 키가 사용자 이름과 암호를 묻는 메시지가 나타나면**: "연결" hello "tooServer 연결" 대화 상자를 클릭 하면 hello 사용자 이름 및 암호 (됩니다 프로그램 macOS와 autopopulated 메시지가 메시지가 표시 됩니다 사용자 이름)입니다.</span><span class="sxs-lookup"><span data-stu-id="4bfdf-122">**Use hello share name and storage account key when prompted for a username and password**: When you click "Connect" on hello "Connect tooServer" dialog, you will be prompted for hello username and password (This will be autopopulated with your macOS username).</span></span> <span data-ttu-id="4bfdf-123">프로그램 macOS 키 집합에에서 hello 공유 이름/저장소 계정 키를 배치의 hello 선택할을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bfdf-123">You have hello option of placing hello share name/storage account key in your macOS Keychain.</span></span>

4. <span data-ttu-id="4bfdf-124">**필요에 따라 사용 하 여 hello Azure 파일 공유**: hello 공유 이름과 저장소 계정 키를 hello 사용자 이름 및 암호를 대체 한 후 hello 공유 탑재 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bfdf-124">**Use hello Azure File share as desired**: After substituting hello share name and storage account key in for hello username and password, hello share will be mounted.</span></span> <span data-ttu-id="4bfdf-125">이 작업은 일반적으로 파일을 끌어다 놓는 hello 파일 공유를 포함 하 여 로컬 폴더/파일 공유를 사용할 때 처럼 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bfdf-125">You may use this as you would normally use a local folder/file share, including dragging and dropping files into hello file share:</span></span>

    ![탑재된 Azure 파일 공유의 스냅숏](./media/storage-file-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a><span data-ttu-id="4bfdf-127">터미널을 통해 Azure 파일 공유 탑재</span><span class="sxs-lookup"><span data-stu-id="4bfdf-127">Mount an Azure File share via Terminal</span></span>
1. <span data-ttu-id="4bfdf-128">대체 `<storage-account-name>` hello 저장소 계정 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bfdf-128">Replace `<storage-account-name>` with hello name of your storage account.</span></span> <span data-ttu-id="4bfdf-129">메시지가 표시되면 저장소 계정 키를 암호로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4bfdf-129">Provide Storage Account Key as password when prompted.</span></span> 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. <span data-ttu-id="4bfdf-130">**필요에 따라 사용 하 여 hello Azure 파일 공유**: hello Azure 파일 공유 hello 이전 명령에 의해 지정 된 hello 탑재 지점에서 탑재 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bfdf-130">**Use hello Azure File share as desired**: hello Azure File share will be mounted at hello mount point specified by hello previous command.</span></span>  

    ![Hello에 대 한 스냅숏을 탑재 Azure 파일 공유](./media/storage-file-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a><span data-ttu-id="4bfdf-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4bfdf-132">Next steps</span></span>
<span data-ttu-id="4bfdf-133">Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="4bfdf-133">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="4bfdf-134">Apple 지원 문서-어떻게 Mac에서 파일 공유를 사용한 tooconnect</span><span class="sxs-lookup"><span data-stu-id="4bfdf-134">Apple Support Article - How tooconnect with File Sharing on your Mac</span></span>](https://support.apple.com/HT204445)
* [<span data-ttu-id="4bfdf-135">FAQ</span><span class="sxs-lookup"><span data-stu-id="4bfdf-135">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="4bfdf-136">문제 해결</span><span class="sxs-lookup"><span data-stu-id="4bfdf-136">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)