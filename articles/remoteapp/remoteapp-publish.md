---
title: "Azure RemoteApp에 앱 aaaPublish | Microsoft Docs"
description: "자세한 내용은 방법 toopublish 응용 프로그램 및 Azure RemoteApp에서 리소스입니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c7e1a2cd-8e1f-4a33-bd43-8032ec9ac952
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d7d92187e9ed999ac79554c9bb61f56a8eceeb31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopublish-an-app-in-remoteapp"></a><span data-ttu-id="dcdd0-103">어떻게 toopublish RemoteApp에서 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="dcdd0-103">How toopublish an app in RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="dcdd0-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dcdd0-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="dcdd0-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcdd0-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="dcdd0-106">RemoteApp 컬렉션을 만든 후 toopublish hello 앱 이나 사용자를 위해 사용할 수 있는 toomake 되도록 리소스 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcdd0-106">After you create your RemoteApp collection, you need toopublish hello apps or resources that you want toomake available for your users.</span></span> <span data-ttu-id="dcdd0-107">hello 구독에서 제공 하는 템플릿 이미지를 하나만 몇 가지 앱-기본적으로 게시 tooshare hello 다른 앱, toopublish 해야 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcdd0-107">hello template images provided with your subscription only have a few apps published by default - tooshare hello other apps, you need toopublish them.</span></span>

> [!NOTE]
> <span data-ttu-id="dcdd0-108">응용 프로그램 tooupdate 필요 한가요?</span><span class="sxs-lookup"><span data-stu-id="dcdd0-108">Do you need tooupdate an app?</span></span> <span data-ttu-id="dcdd0-109">너무 해야[업데이트 hello 이미지](remoteapp-update.md) 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="dcdd0-109">You'll need too[update hello image](remoteapp-update.md) first.</span></span>
> 
> 

<span data-ttu-id="dcdd0-110">Hello에 **게시** hello 포털에서 탭을 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="dcdd0-110">On hello **Publishing** tab in hello portal, click **Publish**.</span></span> <span data-ttu-id="dcdd0-111">템플릿 이미지의에서 응용 프로그램을 추가 하거나 **시작** 메뉴 하거나 hello 경로 toowhere hello 앱 hello 템플릿 이미지에 설치 되어 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcdd0-111">You can either add an app from your template image's **Start** menu or provide hello path toowhere hello app is installed on hello template image.</span></span> <span data-ttu-id="dcdd0-112">Hello에서 tooadd를 선택 하면 **시작** 메뉴 hello 앱 toopublish hello 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcdd0-112">If you choose tooadd from hello **Start** menu, choose hello app toopublish from hello list.</span></span> <span data-ttu-id="dcdd0-113">Tooprovide hello 경로 toohello 앱을 선택 하면 hello 경로 toohello 앱과 hello 앱에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcdd0-113">If you choose tooprovide hello path toohello app, enter a name for hello app and hello path toohello app.</span></span> <span data-ttu-id="dcdd0-114">대신 hello 경로-예를 들어, "%systemdrive%"의 변수를 사용 하 여 "c:\"합니다.</span><span class="sxs-lookup"><span data-stu-id="dcdd0-114">Use variables in hello path - for example, "%systemdrive%" instead of "c:\".</span></span>

> [!NOTE]
> <span data-ttu-id="dcdd0-115">Tooadd hello에서 응용 프로그램을 원하는 경우 **시작** 메뉴 toohave 필요 *해당 앱 toohello 추가 **시작** 템플릿 이미지에 대 한 메뉴입니다.*</span><span class="sxs-lookup"><span data-stu-id="dcdd0-115">If you want tooadd your app from hello **Start** menu, you need toohave *added that app toohello **Start** menu on your template image.*</span></span> <span data-ttu-id="dcdd0-116">그렇지 않은 경우 RemoteApp 볼 기능 *은* hello에 **시작** 메뉴 하 고 혼동 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcdd0-116">Otherwise, RemoteApp will only see what *is* on hello **Start** menu, and you will be confused.</span></span> 
> 
> <span data-ttu-id="dcdd0-117">hello toomake 있는지 앱이 **시작** 메뉴 바로 가기 파일- **.lnk** -hello %systemdrive%\ProgramData\Microsoft\Windows\Start 메뉴 \ 프로그램 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="dcdd0-117">toomake sure your app is in hello **Start** menu, place a shortcut file - **.lnk** - inside hello %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs folder.</span></span>
> 
> <span data-ttu-id="dcdd0-118">Tooadd hello 앱 toohello 잊은 경우 **시작** hello 템플릿을 만들 때 메뉴 tooadd hello 경로 toohello 앱을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcdd0-118">If you forgot tooadd hello app toohello **Start** menu when you created hello template, choose tooadd hello path toohello app.</span></span> <span data-ttu-id="dcdd0-119">(또는 템플릿 이미지를 다시 만듭니다. 하지만 작업이 훨씬 더 복잡 합니다.)</span><span class="sxs-lookup"><span data-stu-id="dcdd0-119">(Or recreate your template image, but that's quite a bit more work.)</span></span>
> 
> 

