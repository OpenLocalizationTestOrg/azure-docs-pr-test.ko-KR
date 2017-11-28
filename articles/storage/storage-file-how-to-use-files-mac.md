---
title: "macOS에서 SMB를 통해 Azure 파일 공유 탑재 | Microsoft Docs"
description: "macOS를 사용하여 SMB를 통해 Azure 파일 공유를 탑재하는 방법을 알아봅니다."
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
ms.openlocfilehash: 428086910273d10a68cb8193df377a4db267d6a3
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a><span data-ttu-id="5c25c-103">macOS에서 SMB를 통해 Azure 파일 공유 탑재</span><span class="sxs-lookup"><span data-stu-id="5c25c-103">Mount Azure File share over SMB with macOS</span></span>
<span data-ttu-id="5c25c-104">[Azure File Storage](storage-dotnet-how-to-use-files.md)는 업계 표준을 사용하여 Azure에서 네트워크 파일 공유를 만들고 사용할 수 있게 해주는 Microsoft 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5c25c-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's service that enables you to create and use network file shares in the Azure using the industry standard.</span></span> <span data-ttu-id="5c25c-105">Azure 파일 공유는 macOS Sierra(10.12) 및 El Capitan(10.11)에서 탑재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c25c-105">Azure File shares can be mounted in macOS Sierra (10.12) and El Capitan (10.11).</span></span> <span data-ttu-id="5c25c-106">이 문서에서는 두 가지 방법, 즉 찾기(Finder) UI 및 터미널을 사용하여 macOS에 Azure 파일 공유를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="5c25c-106">This article shows two different ways to mount an Azure File share on macOS with the Finder UI and using the Terminal.</span></span>

> [!Note]  
> <span data-ttu-id="5c25c-107">SMB를 통해 Azure 파일 공유를 탑재하기 전에 SMB 패킷 서명을 사용하지 않도록 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5c25c-107">Before mounting an Azure File share over SMB, we recommend disabling SMB packet signing.</span></span> <span data-ttu-id="5c25c-108">이렇게 하지 않으면 macOS에서 Azure 파일 공유에 액세스할 때 성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c25c-108">Not doing so may yield poor performance when accessing the Azure File share from macOS.</span></span> <span data-ttu-id="5c25c-109">SMB 연결이 암호화되므로 연결 보안에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5c25c-109">Your SMB connection will be encrypted, so this does not affect the security of your connection.</span></span> <span data-ttu-id="5c25c-110">[SMB 패킷 서명 비활성화 대한 Apple 지원 문서](https://support.apple.com/HT205926)에서 설명한 대로 다음 명령은 터미널에서 SMB 패킷 서명을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5c25c-110">From the terminal, the following commands will disable SMB packet signing, as described by this [Apple support article on disabling SMB packet signing](https://support.apple.com/HT205926):</span></span>  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a><span data-ttu-id="5c25c-111">macOS에 Azure 파일 공유를 탑재하기 위한 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="5c25c-111">Prerequisites for mounting an Azure File share on macOS</span></span>
* <span data-ttu-id="5c25c-112">**저장소 계정 이름**: Azure 파일 공유를 탑재하려면 저장소 계정의 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5c25c-112">**Storage account name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="5c25c-113">**저장소 계정 키**: Azure File 공유를 탑재하려면 기본(또는 보조) 저장소 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5c25c-113">**Storage account key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="5c25c-114">SAS 키는 현재 탑재를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5c25c-114">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="5c25c-115">**445 포트가 열려 있는지 확인**: SMB는 445 TCP 포트를 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="5c25c-115">**Ensure port 445 is open**: SMB communicates over TCP port 445.</span></span> <span data-ttu-id="5c25c-116">클라이언트 컴퓨터(Mac)에서 방화벽이 445 TCP 포트를 차단하고 있지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c25c-116">On your client machine (the Mac), check to make sure your firewall is not blocking TCP port 445.</span></span>

## <a name="mount-an-azure-file-share-via-finder"></a><span data-ttu-id="5c25c-117">찾기를 통해 Azure 파일 공유 탑재</span><span class="sxs-lookup"><span data-stu-id="5c25c-117">Mount an Azure File share via Finder</span></span>
1. <span data-ttu-id="5c25c-118">**찾기를 엽니다**. 찾기는 기본적으로 macOS에서 열리지만 도킹 스테이션에서 "macOS 얼굴 아이콘"을 클릭하여 현재 선택된 응용 프로그램인지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c25c-118">**Open Finder**: Finder is open on macOS by default, but you can ensure it is the currently selected application by clicking the "macOS face icon" on the dock:</span></span>  
    <span data-ttu-id="5c25c-119">![macOS 얼굴 아이콘](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span><span class="sxs-lookup"><span data-stu-id="5c25c-119">![The macOS face icon](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span></span>

2. <span data-ttu-id="5c25c-120">**"이동" 메뉴에서 "서버에 연결"을 선택합니다**. [필수 구성 요소](#preq)의 UNC 경로를 사용하여 시작 이중 백슬래시(`\\`)는 `smb://`로 변환하고, 다른 모든 백슬래시(`\`)는 슬래시(`/`)로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="5c25c-120">**Select "Connect to Server" from the "Go" Menu**: Using the UNC path from the [prerequisites](#preq), convert the beginning double backslash (`\\`) to `smb://` and all other backslashes (`\`) to forwards slashes (`/`).</span></span> <span data-ttu-id="5c25c-121">링크는 다음과 같습니다. !["서버에 연결" 대화 상자](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span><span class="sxs-lookup"><span data-stu-id="5c25c-121">Your link should look like the following: ![The "Connect to Server" dialog](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span></span>

3. <span data-ttu-id="5c25c-122">**사용자 이름과 암호를 묻는 메시지가 표시되면 공유 이름과 저장소 계정 키를 사용합니다**. "서버에 연결" 대화 상자에서 "연결"을 클릭하면 사용자 이름과 암호를 입력하라는 메시지가 표시됩니다. (이 경우 macOS 사용자 이름이 자동으로 채워져 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="5c25c-122">**Use the share name and storage account key when prompted for a username and password**: When you click "Connect" on the "Connect to Server" dialog, you will be prompted for the username and password (This will be autopopulated with your macOS username).</span></span> <span data-ttu-id="5c25c-123">macOS 키 집합에 공유 이름/저장소 계정 키를 배치할 수 있는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c25c-123">You have the option of placing the share name/storage account key in your macOS Keychain.</span></span>

4. <span data-ttu-id="5c25c-124">**Azure 파일 공유를 원하는 대로 사용합니다**. 공유 이름과 저장소 계정 키를 사용자 이름과 암호로 대체하면 해당 공유가 탑재됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c25c-124">**Use the Azure File share as desired**: After substituting the share name and storage account key in for the username and password, the share will be mounted.</span></span> <span data-ttu-id="5c25c-125">일반적으로 파일 공유로 파일 끌어 놓기를 포함하여 로컬 폴더/파일 공유를 사용하는 것처럼 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c25c-125">You may use this as you would normally use a local folder/file share, including dragging and dropping files into the file share:</span></span>

    ![탑재된 Azure 파일 공유의 스냅숏](./media/storage-file-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a><span data-ttu-id="5c25c-127">터미널을 통해 Azure 파일 공유 탑재</span><span class="sxs-lookup"><span data-stu-id="5c25c-127">Mount an Azure File share via Terminal</span></span>
1. <span data-ttu-id="5c25c-128">`<storage-account-name>`을 저장소 계정 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5c25c-128">Replace `<storage-account-name>` with the name of your storage account.</span></span> <span data-ttu-id="5c25c-129">메시지가 표시되면 저장소 계정 키를 암호로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5c25c-129">Provide Storage Account Key as password when prompted.</span></span> 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. <span data-ttu-id="5c25c-130">**원하는 대로 Azure 파일 공유를 사용합니다**. Azure 파일 공유는 이전 명령으로 지정된 탑재 지점에 탑재됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c25c-130">**Use the Azure File share as desired**: The Azure File share will be mounted at the mount point specified by the previous command.</span></span>  

    ![탑재된 Azure 파일 공유의 스냅숏](./media/storage-file-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a><span data-ttu-id="5c25c-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5c25c-132">Next steps</span></span>
<span data-ttu-id="5c25c-133">Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="5c25c-133">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="5c25c-134">Apple 지원 문서 - Mac에서 파일 공유를 사용하여 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="5c25c-134">Apple Support Article - How to connect with File Sharing on your Mac</span></span>](https://support.apple.com/HT204445)
* [<span data-ttu-id="5c25c-135">FAQ</span><span class="sxs-lookup"><span data-stu-id="5c25c-135">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="5c25c-136">문제 해결</span><span class="sxs-lookup"><span data-stu-id="5c25c-136">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)