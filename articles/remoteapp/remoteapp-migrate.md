---
title: "Azure RemoteApp에서 사용자 데이터 마이그레이션 | Microsoft Docs"
description: "Azure RemoteApp 내부/외부로 사용자 데이터를 마이그레이션하는 방법을 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d7e4fbf1-cb42-4430-94a0-ed6d4676fc86
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ba3cf4c6834279bbd7f94d666fd8abbb7ac05bf0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-migrate-data-into-and-out-of-azure-remoteapp"></a><span data-ttu-id="4e221-103">Azure RemoteApp 내부/외부로 데이터를 마이그레이션하는 방법</span><span class="sxs-lookup"><span data-stu-id="4e221-103">How to migrate data into and out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4e221-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="4e221-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="4e221-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="4e221-106">[사용자 데이터](remoteapp-upd.md) 를 Azure RemoteApp 내부/외부로 전송하기 위해 여러 다양한 도구 및 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-106">You can use many different tools and methods to transfer [user data](remoteapp-upd.md) into and out of Azure RemoteApp.</span></span> <span data-ttu-id="4e221-107">몇 가지 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-107">Here are a few methods:</span></span>

* <span data-ttu-id="4e221-108">클립보드 공유를 사용하여 복사 및 붙여넣기</span><span class="sxs-lookup"><span data-stu-id="4e221-108">Copy and paste using clipboard sharing</span></span>
* <span data-ttu-id="4e221-109">파일 및 데이터를 파일 서버에 복사</span><span class="sxs-lookup"><span data-stu-id="4e221-109">Copy files and data to a file server</span></span>
* <span data-ttu-id="4e221-110">브라우저를 통해 비즈니스용 OneDrive에 파일 복사</span><span class="sxs-lookup"><span data-stu-id="4e221-110">Copy files to OneDrive for Business through a browser</span></span>
* <span data-ttu-id="4e221-111">리디렉션을 사용하여 파일 복사</span><span class="sxs-lookup"><span data-stu-id="4e221-111">Copy files using redirection</span></span>

> [!NOTE]
> <span data-ttu-id="4e221-112">비즈니스용 또는 소비자용 OneDrive 동기화 에이전트는 사용하도록 설정할 수 없습니다. 이러한 두 에이전트는 Azure RemoteApp에서 [지원되지 않습니다](remoteapp-onedrive.md).</span><span class="sxs-lookup"><span data-stu-id="4e221-112">You cannot enable the OneDrive for Business or Consumer sync agents - they [are not supported](remoteapp-onedrive.md) in Azure RemoteApp.</span></span>
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a><span data-ttu-id="4e221-113">파일 탐색기에서 복사 및 붙여넣기 사용</span><span class="sxs-lookup"><span data-stu-id="4e221-113">Use copy and paste in File Explorer</span></span>
<span data-ttu-id="4e221-114">클립보드를 사용하는 복사 및 붙여넣기는 [기본적으로](remoteapp-redirection.md) RemoteApp 배포에서 사용하도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-114">Copy and paste using the clipboard is enabled in RemoteApp deployments [by default](remoteapp-redirection.md).</span></span> <span data-ttu-id="4e221-115">따라서 로컬 PC와 RemoteApp 앱 간에 파일을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-115">This lets users copy files between their local PC and RemoteApp apps.</span></span> <span data-ttu-id="4e221-116">종종 RemoteApp에서 앱을 사용하는 일반적인 과정을 통해 파일이 UPD에 저장됩니다. 따라서 RemoteApp에서 데이터를 쉽게 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-116">Often, through the normal course of using apps in RemoteApp, users have saved files to their UPDs - moving that data out of RemoteApp is easy:</span></span>

1. <span data-ttu-id="4e221-117">[파일 탐색기를 앱으로 게시](remoteapp-publish.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-117">[Publish File Explorer as an app](remoteapp-publish.md) in a RemoteApp collection.</span></span> <span data-ttu-id="4e221-118">(이 작업은 관리 작업입니다.)</span><span class="sxs-lookup"><span data-stu-id="4e221-118">(Note that this is an administrative task.)</span></span>
2. <span data-ttu-id="4e221-119">사용자에게 게시한 파일 탐색기 앱을 시작하고 자신의 UPD 내부/외부로 파일을 복사하고 붙여넣는 데 사용하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-119">Direct your users to launch the File Explorer app you published and to use that to copy and paste files both into their UPD and out of it.</span></span>

## <a name="upload-files-and-data-to-a-file-server-by-using-standard-network-file-copy"></a><span data-ttu-id="4e221-120">표준 네트워크 파일 복사를 사용하여 파일 서버에 파일 및 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="4e221-120">Upload files and data to a file server by using standard network file copy</span></span>
<span data-ttu-id="4e221-121">조직은 종종 파일 서버를 사용하여 일반 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-121">Often organizations use file servers to store general data.</span></span> <span data-ttu-id="4e221-122">서버 이름이나 위치를 알고 있는 경우 사용자는 로컬 네트워크에서 서버를 검색한 다음, 위에 나온 것처럼 파일을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-122">If you know the server name or location, your users can browse the local network for the server and then copy their files there, much like they did above.</span></span> <span data-ttu-id="4e221-123">다시 RemoteApp에 파일 탐색기를 게시하고 사용자와 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-123">Again you'll want to publish File Explorer to RemoteApp and then share it with your users.</span></span>

> [!NOTE]
> <span data-ttu-id="4e221-124">파일 서버는 RemoteApp이 배포된 라우팅 가능 네트워크에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-124">The file server must be on the routable network that RemoteApp was deployed into.</span></span>
> 
> 

## <a name="copy-files-to-onedrive-for-business"></a><span data-ttu-id="4e221-125">비즈니스용 OneDrive에 파일 복사</span><span class="sxs-lookup"><span data-stu-id="4e221-125">Copy files to OneDrive for Business</span></span>
<span data-ttu-id="4e221-126">RemoteApp에서 비즈니스용 OneDrive 동기화 에이전트를 사용하도록 설정할 수 없으나 여전히 브라우저를 통해.UPD의 파일을 비즈니스용 OneDrive에 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-126">Although you cannot enable the OneDrive for Business sync agent in RemoteApp, you can still copy files from your UPD to OneDrive for Business through a browser.</span></span> 

1. <span data-ttu-id="4e221-127">파일 탐색기를 RemoteApp에 게시하고 사용자에게 해당 앱을 통해 파일에 액세스하도록 지시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-127">Publish File Explorer to RemoteApp and then tell users to access the files through that app.</span></span> 
2. <span data-ttu-id="4e221-128">파일은 압축했을 때 전송하기가 가장 쉬우므로 사용자는 비즈니스용 OneDrive로 이동할 모든 파일을 포함하는 .zip 파일을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-128">It's easiest to transfer files if they are compressed, so users should create a .zip file that contains all of the files to move to OneDrive for Business.</span></span>
3. <span data-ttu-id="4e221-129">사용자에게 Office 365 포털로 이동한 후 OneDrive로 간 다음 .zip 파일을 업로드하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-129">Ask users to go to the Office 365 portal, and then go to OneDrive and upload the .zip file.</span></span>

## <a name="copy-files-by-using-drive-redirection"></a><span data-ttu-id="4e221-130">드라이브 리디렉션을 사용하여 파일 복사</span><span class="sxs-lookup"><span data-stu-id="4e221-130">Copy files by using drive redirection</span></span>
<span data-ttu-id="4e221-131">[드라이브 리디렉션](remoteapp-redirection.md)을 사용하도록 설정했으면 사용자에 대해 매핑된 드라이브를 이미 만들었을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-131">If you have enabled [drive redirection](remoteapp-redirection.md), you have already created a mapped drive for your users.</span></span> <span data-ttu-id="4e221-132">이 경우 리디렉션된 드라이브에 파일을 zip으로 압축한 다음 로컬 PC에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-132">In this case, they can zip their files on the redirected drive and then save them to their local PC.</span></span>

## <a name="how-administrators-can-export-data"></a><span data-ttu-id="4e221-133">관리자가 데이터를 내보내는 방법</span><span class="sxs-lookup"><span data-stu-id="4e221-133">How administrators can export data</span></span>

<span data-ttu-id="4e221-134">Azure RemoteApp 관리자는 Azure PowerShell cmdlet, Export-AzureRemoteAppUserDisk를 사용하여 구독 내의 모든 컬렉션에 대한 모든 UPD(사용자 프로필 디스크)를 Azure Storage로 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-134">Administers for Azure RemoteApp can export all user profile disks (UPD) for all collections within a subscription to Azure Storage using Azure PowerShell cmdlet, Export-AzureRemoteAppUserDisk.</span></span>  <span data-ttu-id="4e221-135">개별 UPD를 선택하는 기능은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-135">There is no ability to select individual UPD's.</span></span>  <span data-ttu-id="4e221-136">PowerShell 명령이 실행되면 각 사용자 디스크는 50gb의 고정 디스크 크기로 Azure Storage에 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-136">When the PowerShell command is executed, each user disk will be a 50gb in fixed disk size and be exported to Azure storage.</span></span>  <span data-ttu-id="4e221-137">이 저장소에 대한 바로 Azure Storage 비용이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-137">Costs of Azure storage will incur immediately for this storage.</span></span>  <span data-ttu-id="4e221-138">이 명령을 실행하는 경우 세션이 없는지 확인해야 합니다. 세션이 있으면 내보내기가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-138">When running this command ensure there are no sessions otherwise the export will fail.</span></span>

<span data-ttu-id="4e221-139">도메인에 가입된 Azure RemoteApp 배포에 대한 UPD는 RDS 배포에만 다시 사용될 수 있으며 도메인에 가입되지 않은 배포는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-139">UPD's for domain joined Azure RemoteApp deployments can only be used again in an RDS deployment, non-domain joined deployments cannot be used.</span></span>  <span data-ttu-id="4e221-140">이러한 디스크가 RDS 배포에 사용될 경우 UPD를 내보내고 변환하고 RDS 배포로 가져오는 [자동화 스크립트](https://github.com/arcadiahlyy/aramigration)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4e221-140">If these disks will be used in an RDS deployment we recommend to use our [automated scripts](https://github.com/arcadiahlyy/aramigration) that will export, convert, and import the UPD's into an RDS deployment.</span></span>

