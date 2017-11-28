---
title: "Azure RemoteApp 라이선스 요구 사항 | Microsoft Docs"
description: "Azure RemoteApp의 라이선스 작동 방식에 대해 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: ff8ebd20-61a1-4f10-87a6-234a170534c9
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 4c1ad1657ab628283f071afbc9361d67cc301417
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-does-licensing-work-in-azure-remoteapp"></a><span data-ttu-id="f6814-103">Azure RemoteApp의 라이선스 작동 방식</span><span class="sxs-lookup"><span data-stu-id="f6814-103">How does licensing work in Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f6814-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f6814-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f6814-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="f6814-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f6814-106">이제 Azure RemoteApp 서비스를 설정하고 템플릿을 만들었으며 사용자에게 앱을 게시할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f6814-106">So you've set up your Azure RemoteApp service, created your templates, and are ready to publish apps to your users.</span></span> <span data-ttu-id="f6814-107">하지만 마지막으로 확인해야 할 사항이 있습니다. 바로 라이선스입니다.</span><span class="sxs-lookup"><span data-stu-id="f6814-107">But there's still one last thing to figure out: licensing.</span></span> <span data-ttu-id="f6814-108">RemoteApp 및 RemoteApp을 통해 공유하는 앱에 대해 라이선스는 어떻게 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="f6814-108">Just how does licensing work for RemoteApp and for the apps you share through RemoteApp?</span></span>

<span data-ttu-id="f6814-109">RemoteApp에는 Windows 라이선스 또는 원격 데스크톱 CAL이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f6814-109">RemoteApp does not require any Windows licenses or Remote Desktop CALs.</span></span> <span data-ttu-id="f6814-110">구독은 RemoteApp 쪽 자체를 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="f6814-110">Your subscription takes care of the RemoteApp side itself.</span></span> <span data-ttu-id="f6814-111">( [가격 계획](https://azure.microsoft.com/pricing/details/remoteapp)의 세부 정보를 확인하세요.)</span><span class="sxs-lookup"><span data-stu-id="f6814-111">(Check out the details of the [pricing plans](https://azure.microsoft.com/pricing/details/remoteapp).)</span></span>

<span data-ttu-id="f6814-112">구독에 포함된 이미지 중 하나를 사용하는 경우 별도의 라이선스 없이 해당 이미지에 설치된 모든 앱을 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6814-112">If you use one of the images that is included in your subscription, you can share any of the apps installed on that image without needing a separate license.</span></span> <span data-ttu-id="f6814-113">예를 들어 Windows Server 2012 R2 템플릿 이미지를 사용하여 컬렉션을 빌드하는 경우 System Center Endpoint Protection을 사용자와 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6814-113">For example, if you use the Windows Server 2012 R2 template image to build your collection, you can share System Center Endpoint Protection with your users.</span></span> <span data-ttu-id="f6814-114">이 규칙에 대한 유일한 예외는 Office 365 ProPlus의 경우 별도 구독이 필요하고 Office 2013의 경우 프로덕션 컬렉션에서 공유할 수 없다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="f6814-114">The only exceptions to this rule are Office 365 ProPlus, which requires a separate subscription, and Office 2013, which cannot be shared in a production collection.</span></span>

<span data-ttu-id="f6814-115">Azure RemoteApp과 함께 제공된 Office 365 템플릿 이미지를 사용하려면 *기존* Office 365 ProPlus 계획이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6814-115">If you want to use the Office 365 template image that comes with RemoteApp, you must have an *existing* Office 365 ProPlus plan.</span></span> <span data-ttu-id="f6814-116">사용자 지정 템플릿을 사용하여 게시하는 Office 365 앱의 경우도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="f6814-116">The same is true for any Office 365 app that you publish using a custom template.</span></span> <span data-ttu-id="f6814-117">소유한 구독으로 앱을 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6814-117">You need to activate the apps with your own subscription.</span></span> <span data-ttu-id="f6814-118">이 내용은 평가판 및 유료 구독 둘 다에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6814-118">This is true for both trial and paid subscriptions.</span></span> <span data-ttu-id="f6814-119">평가판 사용 중 Office 365 템플릿 이미지를 사용하려는 경우 *구독이 아직 없으면*Office 365 페이지로 이동하여 평가판 구독을 [등록](https://go.microsoft.com/fwlink/p/?LinkID=403802) 하세요.</span><span class="sxs-lookup"><span data-stu-id="f6814-119">If you want to use the Office 365 template image during the trial, *and you don't already have a subscription*, go to the Office 365 page to [sign up](https://go.microsoft.com/fwlink/p/?LinkID=403802) for a trial subscription.</span></span> <span data-ttu-id="f6814-120">자세한 내용은 [RemoteApp과 Office가 함께 작동하는 방식](remoteapp-o365.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6814-120">See [How do RemoteApp and Office work together?](remoteapp-o365.md) for more information.</span></span>

<span data-ttu-id="f6814-121">평가 기간 중 Office 365 평가판 구독을 가져오지 않으려면 RemoteApp과 함께 제공된 Office 2013 Professional Plus 템플릿 이미지를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="f6814-121">If, during the trial period, you don't want to get an Office 365 trial subscription, use the Office 2013 Professional Plus template image that comes with RemoteApp.</span></span> <span data-ttu-id="f6814-122">이 템플릿 이미지는 30일 동안만 사용할 수 있으며 유료 컬렉션으로 변환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f6814-122">This template image can only be used for 30 days and cannot be converted into a paid collection.</span></span>

<span data-ttu-id="f6814-123">다른 앱의 경우, 앱을 공유하기 위한 라이선스가 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6814-123">For other apps, you need to make sure that you have the license to share the app.</span></span>

<span data-ttu-id="f6814-124">참 합리적이지 않은가요?</span><span class="sxs-lookup"><span data-stu-id="f6814-124">That makes sense, right?</span></span> <span data-ttu-id="f6814-125">법적으로 공유할 자격이 있는 모든 앱을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6814-125">You can publish any app that you are legally entitled to share.</span></span> <span data-ttu-id="f6814-126">또한 프로그램을 공유할 자격이 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6814-126">And you need to make sure you really are entitled to share your programs.</span></span>

<span data-ttu-id="f6814-127">클라우드 컬렉션의 CAL 또는 볼륨 라이선스 계약은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f6814-127">Please note that you cannot use a CAL or Volume License agreement in a cloud collection.</span></span> <span data-ttu-id="f6814-128">볼륨 라이선스 계약을 사용하여 하이브리드 컬렉션의 응용 프로그램을 활성화할 *수 있습니다* (Office 제외).</span><span class="sxs-lookup"><span data-stu-id="f6814-128">You *can* use a Volume License agreement to activate applications in your hybrid collection (except for Office).</span></span> <span data-ttu-id="f6814-129">볼륨 라이선스 미디어에서 해당 템플릿 이미지에 설치하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6814-129">You just need to install them on your template image from the Volume License media.</span></span> <span data-ttu-id="f6814-130">응용 프로그램 공급업체의 정보에 따라 원격 데스크톱 환경에 라이선스를 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="f6814-130">Follow the information from the application vendor to install licenses in a Remote Desktop environment.</span></span>

