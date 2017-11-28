---
title: "aaaUpdate Azure RemoteApp 컬렉션 | Microsoft Docs"
description: "자세한 내용은 방법 tooupdate Azure RemoteApp 컬렉션"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: e553d432-e581-48fe-b996-c432357eb64a
ms.service: remoteapp
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 849d7abfdfad4dbe6a235d2a28c71f7943eb812c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a><span data-ttu-id="7a1cb-103">Azure RemoteApp에서 컬렉션 업데이트</span><span class="sxs-lookup"><span data-stu-id="7a1cb-103">Update a collection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7a1cb-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1cb-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="7a1cb-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1cb-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="7a1cb-106">한 번 때을 중지 해야 tooupdate hello 앱 또는 이미지가 Azure RemoteApp 컬렉션에 옵니다.</span><span class="sxs-lookup"><span data-stu-id="7a1cb-106">There will come a time, inevitably, when you need tooupdate hello apps or image in your Azure RemoteApp collection.</span></span> <span data-ttu-id="7a1cb-107">Azure RemoteApp 구독, 클라우드 또는 하이브리드 컬렉션에 포함 된 hello 이미지 중 하나를 사용 하는 경우 쉽게 재설정할 수 있도록 모든 업데이트 자체를 Azure RemoteApp에서 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a1cb-107">If you are using one of hello images included with your Azure RemoteApp subscription, in either a cloud or hybrid collection, any and all updates are handled by Azure RemoteApp itself, so you can rest easy.</span></span>

<span data-ttu-id="7a1cb-108">그러나 사용자 지정 이미지 (처음부터 작성 된 또는 우리의 이미지 중 하나를 수정 하 여 만든)을 사용 하는 경우 담당 하는 hello 이미지 및 응용 프로그램 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1cb-108">However, if you are using a custom image (either that you built from scratch or that you created by modifying one of our images), you are in charge of maintaining hello image and apps.</span></span> <span data-ttu-id="7a1cb-109">이미지 또는 내부 hello 앱 tooupdate를 필요 하면 필요한 toocreate hello 이미지 및 바꾸기 hello 기존 이미지의 업데이트 된 새 버전이이 새로운 업데이트 된 이미지를 사용 하 여 사용자 컬렉션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1cb-109">If you need tooupdate your image or any of hello apps inside it, you need toocreate a new, updated version of hello image, and then replace hello existing image in your collection with this new updated image.</span></span>

<span data-ttu-id="7a1cb-110">그렇다면 컬렉션은 어떻게 업데이트할 수 있을까요?</span><span class="sxs-lookup"><span data-stu-id="7a1cb-110">So, how do you go about updating your collection?</span></span> <span data-ttu-id="7a1cb-111">방법은 상당히 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1cb-111">It's fairly straightforward:</span></span>

1. <span data-ttu-id="7a1cb-112">컬렉션에서 사용한 hello 이미지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1cb-112">Update hello image that you used in your collection.</span></span> <span data-ttu-id="7a1cb-113">필요한 모든 패치 또는 업데이트를 적용하고 새 이름으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1cb-113">Apply any patches or updates needed, and then save it with a new name.</span></span>
2. <span data-ttu-id="7a1cb-114">[업로드](remoteapp-uploadimage.md) 또는 [가져올](remoteapp-image-on-azurevm.md) 이미지 tooRemoteApp 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1cb-114">[Upload](remoteapp-uploadimage.md) or [import](remoteapp-image-on-azurevm.md) that image tooRemoteApp.</span></span>
3. <span data-ttu-id="7a1cb-115">이제 hello 모음 페이지에서 클릭 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1cb-115">Now, on hello collection page, click **Update**.</span></span>
4. <span data-ttu-id="7a1cb-116">Hello에서 hello 새 이미지를 선택 **템플릿 이미지** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="7a1cb-116">Choose hello new image from hello **Template Image** list.</span></span>
5. <span data-ttu-id="7a1cb-117">Hello 문제가 되는 부분은 다음과 같습니다-toodecide를 어떻게 필요 hello 컬렉션에 응용 프로그램 현재 사용 중인 모든 사용자와 toodeal 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1cb-117">Here's hello tricky part - you need toodecide how toodeal with any users that are currently using an app in hello collection.</span></span> <span data-ttu-id="7a1cb-118">선택 항목을 다음 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1cb-118">You have hello following choices:</span></span>
   
   * <span data-ttu-id="7a1cb-119">**사용자에 게 hello 업데이트 후 60 분 제공**합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1cb-119">**Give users 60 minutes after hello update**.</span></span> <span data-ttu-id="7a1cb-120">Hello 업데이트가 완료 되는 즉시 Azure RemoteApp의 작업 및 로그 오프 한 후 다시 로그인 toosave 인하 메시지 tooany 활성 사용자 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a1cb-120">As soon as hello update is finished, Azure RemoteApp will display a message tooany active users telling them toosave their work and log off and log back in.</span></span> <span data-ttu-id="7a1cb-121">60분이 지난 후에도 로그오프하지 않은 모든 사용자는 자동으로 로그오프됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a1cb-121">After 60 minutes, any active users who have not logged off will be automatically logged off.</span></span> <span data-ttu-id="7a1cb-122">사용자는 즉시 다시 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1cb-122">Users can immediately log back on.</span></span>
   * <span data-ttu-id="7a1cb-123">**사용자를 즉시 로그아웃**.</span><span class="sxs-lookup"><span data-stu-id="7a1cb-123">**Sign users out immediately**.</span></span> <span data-ttu-id="7a1cb-124">Hello 업데이트가 완료 되는 즉시 사용자 로그 오프 모든 경고 없이 자동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1cb-124">As soon as hello update is finished, log off all users automatically without any warning.</span></span> <span data-ttu-id="7a1cb-125">이 옵션을 선택하면 사용자가 데이터를 잃을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1cb-125">If you choose this option, users might lose data.</span></span> <span data-ttu-id="7a1cb-126">그러나 toohello 앱 즉시 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a1cb-126">However, they can reconnect toohello app immediately.</span></span>
6. <span data-ttu-id="7a1cb-127">Hello, toostart hello 업데이트 확인 표시를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a1cb-127">Click hello check mark toostart hello update.</span></span>

