---
title: "Azure RemoteApp에서 앱 게시 | Microsoft 문서"
description: "Azure RemoteApp에 응용 프로그램 및 리소스를 게시하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 4565fa498dbadd0601004c73bfee5171efe1fad1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-publish-an-app-in-remoteapp"></a><span data-ttu-id="aebbc-103">RemoteApp에 앱을 게시하는 방법</span><span class="sxs-lookup"><span data-stu-id="aebbc-103">How to publish an app in RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="aebbc-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="aebbc-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="aebbc-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="aebbc-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="aebbc-106">RemoteApp 컬렉션을 만든 후 사용자가 사용할 수 있게 하려는 앱이나 리소스를 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aebbc-106">After you create your RemoteApp collection, you need to publish the apps or resources that you want to make available for your users.</span></span> <span data-ttu-id="aebbc-107">구독과 함께 제공된 템플릿 이미지에는 기본적으로 몇 개의 앱만 게시되어 있습니다. 다른 앱을 공유하려면 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aebbc-107">The template images provided with your subscription only have a few apps published by default - to share the other apps, you need to publish them.</span></span>

> [!NOTE]
> <span data-ttu-id="aebbc-108">응용 프로그램을 업데이트해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="aebbc-108">Do you need to update an app?</span></span> <span data-ttu-id="aebbc-109">먼저 [이미지를 업데이트할](remoteapp-update.md) 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aebbc-109">You'll need to [update the image](remoteapp-update.md) first.</span></span>
> 
> 

<span data-ttu-id="aebbc-110">포털의 **게시** 탭에서 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aebbc-110">On the **Publishing** tab in the portal, click **Publish**.</span></span> <span data-ttu-id="aebbc-111">템플릿 이미지의 **시작** 메뉴에서 앱을 추가하거나 템플릿 이미지에서 앱이 설치되어 있는 경로를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="aebbc-111">You can either add an app from your template image's **Start** menu or provide the path to where the app is installed on the template image.</span></span> <span data-ttu-id="aebbc-112">**시작** 메뉴에서 추가하도록 선택하는 경우 목록에서 게시할 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aebbc-112">If you choose to add from the **Start** menu, choose the app to publish from the list.</span></span> <span data-ttu-id="aebbc-113">앱의 경로를 제공하도록 선택한 경우 앱의 이름과 경로를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="aebbc-113">If you choose to provide the path to the app, enter a name for the app and the path to the app.</span></span> <span data-ttu-id="aebbc-114">경로에서 변수를 사용합니다(예: "c:\" 대신 "%systemdrive%" 사용).</span><span class="sxs-lookup"><span data-stu-id="aebbc-114">Use variables in the path - for example, "%systemdrive%" instead of "c:\".</span></span>

> [!NOTE]
> <span data-ttu-id="aebbc-115">**시작** 메뉴에서 *앱을 추가하려는 경우 템플릿 이미지에서* **시작** *메뉴에 해당 앱을 추가*해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aebbc-115">If you want to add your app from the **Start** menu, you need to have *added that app to the **Start** menu on your template image.*</span></span> <span data-ttu-id="aebbc-116">그렇지 않으면 **시작** 메뉴에 *있는* 내용만 RemoteApp에 표시되어 혼란스러울 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aebbc-116">Otherwise, RemoteApp will only see what *is* on the **Start** menu, and you will be confused.</span></span> 
> 
> <span data-ttu-id="aebbc-117">앱이 **시작** 메뉴에 있는지 확인하려면 %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs 폴더 안에 바로 가기 파일(**.lnk**)을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="aebbc-117">To make sure your app is in the **Start** menu, place a shortcut file - **.lnk** - inside the %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs folder.</span></span>
> 
> <span data-ttu-id="aebbc-118">템플릿을 만들 때 **시작** 메뉴에 앱 추가하는 것을 잊어버린 경우 앱에 경로를 추가하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aebbc-118">If you forgot to add the app to the **Start** menu when you created the template, choose to add the path to the app.</span></span> <span data-ttu-id="aebbc-119">(또는 템플릿 이미지를 다시 만듭니다. 하지만 작업이 훨씬 더 복잡 합니다.)</span><span class="sxs-lookup"><span data-stu-id="aebbc-119">(Or recreate your template image, but that's quite a bit more work.)</span></span>
> 
> 

