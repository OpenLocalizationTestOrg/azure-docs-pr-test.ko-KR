---
title: "Azure RemoteApp에서 사용자 데이터 aaaMigrate | Microsoft Docs"
description: "자세한 내용은 방법 toomigrate Azure RemoteApp에서 사용자 데이터입니다."
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
ms.openlocfilehash: aefc6ccc2c6173754acf6cad06102f27c8cb1d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-data-into-and-out-of-azure-remoteapp"></a><span data-ttu-id="3ed26-103">방법 및 Azure RemoteApp 외부로 toomigrate 데이터</span><span class="sxs-lookup"><span data-stu-id="3ed26-103">How toomigrate data into and out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3ed26-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3ed26-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3ed26-106">여러 다양 한 도구 및 tootransfer 메서드를 사용할 수 있습니다 [사용자 데이터](remoteapp-upd.md) 및 Azure RemoteApp 외부로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-106">You can use many different tools and methods tootransfer [user data](remoteapp-upd.md) into and out of Azure RemoteApp.</span></span> <span data-ttu-id="3ed26-107">몇 가지 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-107">Here are a few methods:</span></span>

* <span data-ttu-id="3ed26-108">클립보드 공유를 사용하여 복사 및 붙여넣기</span><span class="sxs-lookup"><span data-stu-id="3ed26-108">Copy and paste using clipboard sharing</span></span>
* <span data-ttu-id="3ed26-109">파일 및 데이터 tooa 파일 서버에 복사</span><span class="sxs-lookup"><span data-stu-id="3ed26-109">Copy files and data tooa file server</span></span>
* <span data-ttu-id="3ed26-110">브라우저를 통해 비즈니스에 대 한 파일 tooOneDrive 복사</span><span class="sxs-lookup"><span data-stu-id="3ed26-110">Copy files tooOneDrive for Business through a browser</span></span>
* <span data-ttu-id="3ed26-111">리디렉션을 사용하여 파일 복사</span><span class="sxs-lookup"><span data-stu-id="3ed26-111">Copy files using redirection</span></span>

> [!NOTE]
> <span data-ttu-id="3ed26-112">동기화 에이전트-비즈니스 또는 소비자에 대 한 hello OneDrive를 사용할 수 없습니다 것 [는 지원 되지 않습니다](remoteapp-onedrive.md) Azure RemoteApp에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-112">You cannot enable hello OneDrive for Business or Consumer sync agents - they [are not supported](remoteapp-onedrive.md) in Azure RemoteApp.</span></span>
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a><span data-ttu-id="3ed26-113">파일 탐색기에서 복사 및 붙여넣기 사용</span><span class="sxs-lookup"><span data-stu-id="3ed26-113">Use copy and paste in File Explorer</span></span>
<span data-ttu-id="3ed26-114">복사 및 붙여넣기 hello 클립보드를 사용 하 여 RemoteApp 배포에서 활성화 되어 [기본적으로](remoteapp-redirection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-114">Copy and paste using hello clipboard is enabled in RemoteApp deployments [by default](remoteapp-redirection.md).</span></span> <span data-ttu-id="3ed26-115">따라서 로컬 PC와 RemoteApp 앱 간에 파일을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-115">This lets users copy files between their local PC and RemoteApp apps.</span></span> <span data-ttu-id="3ed26-116">종종 hello RemoteApp에 앱을 사용 하는 일반적인 과정을 통해 사용자가 저장 파일 tootheir Upd-데이터 RemoteApp에서 쉽게를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-116">Often, through hello normal course of using apps in RemoteApp, users have saved files tootheir UPDs - moving that data out of RemoteApp is easy:</span></span>

1. <span data-ttu-id="3ed26-117">[파일 탐색기를 앱으로 게시](remoteapp-publish.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-117">[Publish File Explorer as an app](remoteapp-publish.md) in a RemoteApp collection.</span></span> <span data-ttu-id="3ed26-118">(이 작업은 관리 작업입니다.)</span><span class="sxs-lookup"><span data-stu-id="3ed26-118">(Note that this is an administrative task.)</span></span>
2. <span data-ttu-id="3ed26-119">직접 게시 하는 사용자가 toolaunch hello 파일 탐색기 앱 및 toouse 해당 toocopy 및 붙여넣기 파일의 UPD 및 옵트아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-119">Direct your users toolaunch hello File Explorer app you published and toouse that toocopy and paste files both into their UPD and out of it.</span></span>

## <a name="upload-files-and-data-tooa-file-server-by-using-standard-network-file-copy"></a><span data-ttu-id="3ed26-120">표준 네트워크 파일 복사를 사용 하 여 파일 및 tooa 파일 서버 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="3ed26-120">Upload files and data tooa file server by using standard network file copy</span></span>
<span data-ttu-id="3ed26-121">조직에서는 자주 파일 서버 toostore 일반 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-121">Often organizations use file servers toostore general data.</span></span> <span data-ttu-id="3ed26-122">Hello 서버 이름이 나 위치를 알고 있는 사용자가 hello hello 서버에 대 한 로컬 네트워크 수 이동한 다음 위에 했다는 것 처럼, 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-122">If you know hello server name or location, your users can browse hello local network for hello server and then copy their files there, much like they did above.</span></span> <span data-ttu-id="3ed26-123">다시 toopublish 파일 탐색기 tooRemoteApp 원하는 하 고 사용자와 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-123">Again you'll want toopublish File Explorer tooRemoteApp and then share it with your users.</span></span>

> [!NOTE]
> <span data-ttu-id="3ed26-124">hello 파일 서버는 RemoteApp에 배포 된 hello 라우팅할 수 있는 네트워크에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-124">hello file server must be on hello routable network that RemoteApp was deployed into.</span></span>
> 
> 

## <a name="copy-files-tooonedrive-for-business"></a><span data-ttu-id="3ed26-125">비즈니스에 대 한 파일 tooOneDrive 복사</span><span class="sxs-lookup"><span data-stu-id="3ed26-125">Copy files tooOneDrive for Business</span></span>
<span data-ttu-id="3ed26-126">RemoteApp에서 비즈니스 동기화 에이전트에 대 한 hello OneDrive를 사용할 수 없습니다, 있지만 여전히 파일 복사할 수 있습니다 UPD tooOneDrive에서 비즈니스에 대 한 브라우저를 통해 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-126">Although you cannot enable hello OneDrive for Business sync agent in RemoteApp, you can still copy files from your UPD tooOneDrive for Business through a browser.</span></span> 

1. <span data-ttu-id="3ed26-127">파일 탐색기 tooRemoteApp 게시 하 고 그런 다음 사용자가 tooaccess hello 이러한 앱을 통해 파일을 지시할 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-127">Publish File Explorer tooRemoteApp and then tell users tooaccess hello files through that app.</span></span> 
2. <span data-ttu-id="3ed26-128">이므로 쉬운 tootransfer 파일을 압축 하는 경우 사용자 비즈니스에 대 한 hello 파일 toomove tooOneDrive 일부만 포함 하는.zip 파일을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-128">It's easiest tootransfer files if they are compressed, so users should create a .zip file that contains all of hello files toomove tooOneDrive for Business.</span></span>
3. <span data-ttu-id="3ed26-129">사용자가 toogo toohello Office 365 포털 및 묻고 tooOneDrive 이동 하 여 hello.zip 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-129">Ask users toogo toohello Office 365 portal, and then go tooOneDrive and upload hello .zip file.</span></span>

## <a name="copy-files-by-using-drive-redirection"></a><span data-ttu-id="3ed26-130">드라이브 리디렉션을 사용하여 파일 복사</span><span class="sxs-lookup"><span data-stu-id="3ed26-130">Copy files by using drive redirection</span></span>
<span data-ttu-id="3ed26-131">[드라이브 리디렉션](remoteapp-redirection.md)을 사용하도록 설정했으면 사용자에 대해 매핑된 드라이브를 이미 만들었을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-131">If you have enabled [drive redirection](remoteapp-redirection.md), you have already created a mapped drive for your users.</span></span> <span data-ttu-id="3ed26-132">이 경우 zip 파일에 리디렉션 hello 드라이브 수 및 다음 tootheir 저장 로컬 PC입니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-132">In this case, they can zip their files on hello redirected drive and then save them tootheir local PC.</span></span>

## <a name="how-administrators-can-export-data"></a><span data-ttu-id="3ed26-133">관리자가 데이터를 내보내는 방법</span><span class="sxs-lookup"><span data-stu-id="3ed26-133">How administrators can export data</span></span>

<span data-ttu-id="3ed26-134">관리 합니다. Azure RemoteApp에서 모든 사용자 프로필 디스크 (UPD)를 내보낼 수에 대 한 구독 tooAzure Azure PowerShell을 사용 하 여 저장소 내에서 모든 컬렉션에 대 한 내보내기 AzureRemoteAppUserDisk cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3ed26-134">Administers for Azure RemoteApp can export all user profile disks (UPD) for all collections within a subscription tooAzure Storage using Azure PowerShell cmdlet, Export-AzureRemoteAppUserDisk.</span></span>  <span data-ttu-id="3ed26-135">없는 능력 tooselect 개별 UPD의 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-135">There is no ability tooselect individual UPD's.</span></span>  <span data-ttu-id="3ed26-136">Hello PowerShell 명령을 실행 될 때 각 사용자 디스크의 고정된 디스크 크기가 50gb 되며 내보낸된 tooAzure 저장 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-136">When hello PowerShell command is executed, each user disk will be a 50gb in fixed disk size and be exported tooAzure storage.</span></span>  <span data-ttu-id="3ed26-137">이 저장소에 대한 바로 Azure Storage 비용이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-137">Costs of Azure storage will incur immediately for this storage.</span></span>  <span data-ttu-id="3ed26-138">이 명령을 실행 하는 경우에 세션이 그렇지 않으면 hello 내보내기가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-138">When running this command ensure there are no sessions otherwise hello export will fail.</span></span>

<span data-ttu-id="3ed26-139">도메인에 가입된 Azure RemoteApp 배포에 대한 UPD는 RDS 배포에만 다시 사용될 수 있으며 도메인에 가입되지 않은 배포는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-139">UPD's for domain joined Azure RemoteApp deployments can only be used again in an RDS deployment, non-domain joined deployments cannot be used.</span></span>  <span data-ttu-id="3ed26-140">Toouse RDS 배포에서이 디스크를 사용할 경우 좋습니다 우리의 [스크립트 자동화 된](https://github.com/arcadiahlyy/aramigration) 내보내기, 변환을 UPD의 hello는 RDS 배포로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3ed26-140">If these disks will be used in an RDS deployment we recommend toouse our [automated scripts](https://github.com/arcadiahlyy/aramigration) that will export, convert, and import hello UPD's into an RDS deployment.</span></span>

