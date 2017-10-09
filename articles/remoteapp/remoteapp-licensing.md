---
title: "aaaAzure RemoteApp 라이선스 | Microsoft Docs"
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
ms.openlocfilehash: dfa808a65ea6b1a78bf74f3daddb9a84e186eebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-licensing-work-in-azure-remoteapp"></a><span data-ttu-id="ab454-103">Azure RemoteApp의 라이선스 작동 방식</span><span class="sxs-lookup"><span data-stu-id="ab454-103">How does licensing work in Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ab454-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ab454-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ab454-106">따라서 프로그램 서식 파일을 만든 사용자가 Azure RemoteApp 서비스를 설정 및 준비 toopublish 앱 tooyour 사용자가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-106">So you've set up your Azure RemoteApp service, created your templates, and are ready toopublish apps tooyour users.</span></span> <span data-ttu-id="ab454-107">하지만 여전히 아웃 한 마지막 작업 toofigure: 라이선스입니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-107">But there's still one last thing toofigure out: licensing.</span></span> <span data-ttu-id="ab454-108">방금 RemoteApp을 통해 공유 하는 hello 앱에 대 한 RemoteApp에 대 한 라이선스 작업은 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="ab454-108">Just how does licensing work for RemoteApp and for hello apps you share through RemoteApp?</span></span>

<span data-ttu-id="ab454-109">RemoteApp에는 Windows 라이선스 또는 원격 데스크톱 CAL이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-109">RemoteApp does not require any Windows licenses or Remote Desktop CALs.</span></span> <span data-ttu-id="ab454-110">구독 자체 RemoteApp 쪽 hello 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-110">Your subscription takes care of hello RemoteApp side itself.</span></span> <span data-ttu-id="ab454-111">(Hello의 hello 세부 정보를 확인해 보세요 [가격 책정 모델](https://azure.microsoft.com/pricing/details/remoteapp).)</span><span class="sxs-lookup"><span data-stu-id="ab454-111">(Check out hello details of hello [pricing plans](https://azure.microsoft.com/pricing/details/remoteapp).)</span></span>

<span data-ttu-id="ab454-112">구독에 포함 된 hello 이미지 중 하나를 사용 하는 경우 한 별도 라이선스가 필요 없이 해당 이미지에 설치 하는 hello 앱 중 하나를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-112">If you use one of hello images that is included in your subscription, you can share any of hello apps installed on that image without needing a separate license.</span></span> <span data-ttu-id="ab454-113">예를 들어 hello Windows Server 2012 R2 템플릿 이미지 toobuild 컬렉션을 사용 하면 System Center Endpoint Protection 사용자와 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-113">For example, if you use hello Windows Server 2012 R2 template image toobuild your collection, you can share System Center Endpoint Protection with your users.</span></span> <span data-ttu-id="ab454-114">hello만 예외 toothis 규칙은 Office 365 ProPlus, 별도 구독을 요구 하 고 Office 2013 프로덕션 컬렉션에서 공유할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-114">hello only exceptions toothis rule are Office 365 ProPlus, which requires a separate subscription, and Office 2013, which cannot be shared in a production collection.</span></span>

<span data-ttu-id="ab454-115">RemoteApp과 함께 제공 된 toouse hello Office 365 템플릿 이미지를 원하는 경우이 있어야는 *기존* Office 365 ProPlus 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-115">If you want toouse hello Office 365 template image that comes with RemoteApp, you must have an *existing* Office 365 ProPlus plan.</span></span> <span data-ttu-id="ab454-116">hello 사용자 지정 템플릿을 사용 하 여 게시 하는 모든 Office 365 앱에도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-116">hello same is true for any Office 365 app that you publish using a custom template.</span></span> <span data-ttu-id="ab454-117">사용자 고유의 구독과 tooactivate hello 앱 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-117">You need tooactivate hello apps with your own subscription.</span></span> <span data-ttu-id="ab454-118">이 내용은 평가판 및 유료 구독 둘 다에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-118">This is true for both trial and paid subscriptions.</span></span> <span data-ttu-id="ab454-119">Hello 평가판 시 toouse hello Office 365 템플릿 이미지를 원하는 경우 *구독이 아직 없는 및*, 너무 toohello Office 365 페이지로 이동[등록](https://go.microsoft.com/fwlink/p/?LinkID=403802) 평가판 구독에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-119">If you want toouse hello Office 365 template image during hello trial, *and you don't already have a subscription*, go toohello Office 365 page too[sign up](https://go.microsoft.com/fwlink/p/?LinkID=403802) for a trial subscription.</span></span> <span data-ttu-id="ab454-120">자세한 내용은 [RemoteApp과 Office가 함께 작동하는 방식](remoteapp-o365.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ab454-120">See [How do RemoteApp and Office work together?](remoteapp-o365.md) for more information.</span></span>

<span data-ttu-id="ab454-121">Hello 평가 기간 중 tooget Office 365 평가판 구독을 않도록 하는 경우 RemoteApp과 함께 제공 되는 hello Office 2013 Professional 더하기 템플릿 이미지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-121">If, during hello trial period, you don't want tooget an Office 365 trial subscription, use hello Office 2013 Professional Plus template image that comes with RemoteApp.</span></span> <span data-ttu-id="ab454-122">이 템플릿 이미지는 30일 동안만 사용할 수 있으며 유료 컬렉션으로 변환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-122">This template image can only be used for 30 days and cannot be converted into a paid collection.</span></span>

<span data-ttu-id="ab454-123">다른 앱에 대 한 toomake hello 라이선스 tooshare hello 앱 한지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-123">For other apps, you need toomake sure that you have hello license tooshare hello app.</span></span>

<span data-ttu-id="ab454-124">참 합리적이지 않은가요?</span><span class="sxs-lookup"><span data-stu-id="ab454-124">That makes sense, right?</span></span> <span data-ttu-id="ab454-125">Tooshare 자격이 합법적으로 모든 앱을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-125">You can publish any app that you are legally entitled tooshare.</span></span> <span data-ttu-id="ab454-126">Toomake 실제로 선택 되어 있는지 필요 하 고 권한을 부여 받은 tooshare 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-126">And you need toomake sure you really are entitled tooshare your programs.</span></span>

<span data-ttu-id="ab454-127">클라우드 컬렉션의 CAL 또는 볼륨 라이선스 계약은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-127">Please note that you cannot use a CAL or Volume License agreement in a cloud collection.</span></span> <span data-ttu-id="ab454-128">하면 *수* 사무실) (제외 하이브리드 컬렉션의 볼륨 라이선스 계약 tooactivate 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-128">You *can* use a Volume License agreement tooactivate applications in your hybrid collection (except for Office).</span></span> <span data-ttu-id="ab454-129">Hello 볼륨 라이선스 미디어에서에서 이미지 서식 파일에 해당 하는 tooinstall을 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-129">You just need tooinstall them on your template image from hello Volume License media.</span></span> <span data-ttu-id="ab454-130">원격 데스크톱 환경에서 응용 프로그램 공급 업체 tooinstall 라이선스 hello에서에서 hello 정보에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-130">Follow hello information from hello application vendor tooinstall licenses in a Remote Desktop environment.</span></span>

