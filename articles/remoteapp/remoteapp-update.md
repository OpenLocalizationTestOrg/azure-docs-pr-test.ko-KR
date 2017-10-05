---
title: "Azure RemoteApp 컬렉션 업데이트 | Microsoft 문서"
description: "Azure RemoteApp 컬렉션 업데이트 방법"
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
ms.openlocfilehash: 454d78445d6092aec9eaa383e4c50cf15195848c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a><span data-ttu-id="234b6-103">Azure RemoteApp에서 컬렉션 업데이트</span><span class="sxs-lookup"><span data-stu-id="234b6-103">Update a collection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="234b6-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="234b6-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="234b6-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="234b6-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="234b6-106">때로 Azure RemoteApp 컬렉션의 앱이나 이미지를 업데이트해야 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="234b6-106">There will come a time, inevitably, when you need to update the apps or image in your Azure RemoteApp collection.</span></span> <span data-ttu-id="234b6-107">Azure RemoteApp 구독에 포함된 이미지(클라우드 또는 하이브리드 컬렉션) 중 하나를 사용한다면 모든 업데이트는 Azure RemoteApp 자체에서 처리되므로 신경 쓸 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="234b6-107">If you are using one of the images included with your Azure RemoteApp subscription, in either a cloud or hybrid collection, any and all updates are handled by Azure RemoteApp itself, so you can rest easy.</span></span>

<span data-ttu-id="234b6-108">하지만 처음부터 새로 만들었거나 기존 이미지를 수정하여 만든 사용자 지정 이미지를 사용할 경우, 이미지와 앱을 유지 관리하는 것은 사용자의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="234b6-108">However, if you are using a custom image (either that you built from scratch or that you created by modifying one of our images), you are in charge of maintaining the image and apps.</span></span> <span data-ttu-id="234b6-109">이미지 또는 이미지 안의 앱을 업데이트해야 하는 경우 업데이트된 새 버전의 이미지를 만든 다음 컬렉션의 기존 이미지를 업데이트된 이 새 이미지로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="234b6-109">If you need to update your image or any of the apps inside it, you need to create a new, updated version of the image, and then replace the existing image in your collection with this new updated image.</span></span>

<span data-ttu-id="234b6-110">그렇다면 컬렉션은 어떻게 업데이트할 수 있을까요?</span><span class="sxs-lookup"><span data-stu-id="234b6-110">So, how do you go about updating your collection?</span></span> <span data-ttu-id="234b6-111">방법은 상당히 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="234b6-111">It's fairly straightforward:</span></span>

1. <span data-ttu-id="234b6-112">컬렉션에 사용되는 이미지를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="234b6-112">Update the image that you used in your collection.</span></span> <span data-ttu-id="234b6-113">필요한 모든 패치 또는 업데이트를 적용하고 새 이름으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="234b6-113">Apply any patches or updates needed, and then save it with a new name.</span></span>
2. <span data-ttu-id="234b6-114">해당 이미지를 RemoteApp으로 [업로드](remoteapp-uploadimage.md) 또는 [가져오기](remoteapp-image-on-azurevm.md)를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="234b6-114">[Upload](remoteapp-uploadimage.md) or [import](remoteapp-image-on-azurevm.md) that image to RemoteApp.</span></span>
3. <span data-ttu-id="234b6-115">이제 컬렉션 페이지에서 **업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="234b6-115">Now, on the collection page, click **Update**.</span></span>
4. <span data-ttu-id="234b6-116">**템플릿 이미지** 목록에서 새 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="234b6-116">Choose the new image from the **Template Image** list.</span></span>
5. <span data-ttu-id="234b6-117">여기서 신경 쓸 부분이 하나 있습니다. 컬렉션의 앱을 현재 사용하고 있는 사용자를 어떻게 처리할까 하는 부분을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="234b6-117">Here's the tricky part - you need to decide how to deal with any users that are currently using an app in the collection.</span></span> <span data-ttu-id="234b6-118">다음 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="234b6-118">You have the following choices:</span></span>
   
   * <span data-ttu-id="234b6-119">**업데이트 후 사용자에게 60분의 시간 제공**.</span><span class="sxs-lookup"><span data-stu-id="234b6-119">**Give users 60 minutes after the update**.</span></span> <span data-ttu-id="234b6-120">업데이트가 완료되면 Azure RemoteApp에서 현재 앱을 사용 중인 사용자에게 작업을 저장하고 로그오프 했다가 다시 로그인하라는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="234b6-120">As soon as the update is finished, Azure RemoteApp will display a message to any active users telling them to save their work and log off and log back in.</span></span> <span data-ttu-id="234b6-121">60분이 지난 후에도 로그오프하지 않은 모든 사용자는 자동으로 로그오프됩니다.</span><span class="sxs-lookup"><span data-stu-id="234b6-121">After 60 minutes, any active users who have not logged off will be automatically logged off.</span></span> <span data-ttu-id="234b6-122">사용자는 즉시 다시 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="234b6-122">Users can immediately log back on.</span></span>
   * <span data-ttu-id="234b6-123">**사용자를 즉시 로그아웃**.</span><span class="sxs-lookup"><span data-stu-id="234b6-123">**Sign users out immediately**.</span></span> <span data-ttu-id="234b6-124">업데이트가 완료되면 경고 없이 모든 사용자를 자동으로 로그오프합니다.</span><span class="sxs-lookup"><span data-stu-id="234b6-124">As soon as the update is finished, log off all users automatically without any warning.</span></span> <span data-ttu-id="234b6-125">이 옵션을 선택하면 사용자가 데이터를 잃을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="234b6-125">If you choose this option, users might lose data.</span></span> <span data-ttu-id="234b6-126">그러나 즉시 앱에 다시 연결하는 것은 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="234b6-126">However, they can reconnect to the app immediately.</span></span>
6. <span data-ttu-id="234b6-127">확인 표시를 클릭하여 업데이트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="234b6-127">Click the check mark to start the update.</span></span>

