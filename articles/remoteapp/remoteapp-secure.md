---
title: "Azure RemoteApp의 앱 및 리소스 보호 | Microsoft Docs"
description: "Azure RemoteApp의 앱 및 리소스 잠금 방법에 대해 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7fbade87-a453-426d-bfa5-c72227ea83cd
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 1c052906788f0f4fe4ca9fd6d3af63336245174a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="secure-apps-and-resources-in-azure-remoteapp"></a><span data-ttu-id="6a410-103">Azure RemoteApp의 앱 및 리소스 보호</span><span class="sxs-lookup"><span data-stu-id="6a410-103">Secure apps and resources in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6a410-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6a410-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="6a410-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="6a410-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="6a410-106">Azure RemoteApp은 사용자에게 중앙에서 관리되는 Windows 앱에 대한 액세스를 제공하여, 사용자가 수행할 수 있는 내용 및 사용할 수 없는 내용을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a410-106">Azure RemoteApp provides users access to centrally-managed Windows apps, which lets you control what your users can and can't do.</span></span>  <span data-ttu-id="6a410-107">관리되지 않는 장치(예: 자신의 개인 Macbook)에서 사용자가 연결하고 사용자 액세스나 환경을 제어하려는 경우 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a410-107">This is particularly useful when the user is connecting from an unmanaged device (like their personal Macbook) and you want to control the user access or experience.</span></span>

<span data-ttu-id="6a410-108">예를 들어 사용자 인증을 위해 Active Directory를 사용하고 사용자가 앱에서 데이터를 복사하지 못하도록 하려는 경우, 사용자의 데이터 복사를 차단하도록 원격 데스크톱 그룹 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a410-108">For example, if you are using Active Directory for user authentication and you want to prevent your users from copying data out of an app, you can configure a Remote Desktop Group Policy to block users from copying data.</span></span>

<span data-ttu-id="6a410-109">다른 예는 컬렉션에서 특정 앱에 대한 인터넷 액세스를 차단하려는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="6a410-109">Another example is if you want to block internet access for a particular app in your collection.</span></span> <span data-ttu-id="6a410-110">컬렉션에 대한 이미지를 만들 때 액세스를 차단하는 Windows 방화벽 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a410-110">You can create a Windows Firewall rule that blocks the access when you create the image for your collection.</span></span>

## <a name="implementation-options"></a><span data-ttu-id="6a410-111">구현 옵션</span><span class="sxs-lookup"><span data-stu-id="6a410-111">Implementation options</span></span>
  <span data-ttu-id="6a410-112">중요한 구현 옵션으로, 필요에 따라 동시에 또는 개별적으로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a410-112">Here are the key implementation options, which can be used individually or in tandem as needed:</span></span>

1. <span data-ttu-id="6a410-113">RemoteApp 컬렉션이 도메인에 가입되어 있으면 [여기](../azure-subscription-service-limits.md)에 설명된 유휴 상태 및 연결 끊기 시간 제한 정책을 제외하고는 모든 [그룹 정책](https://technet.microsoft.com/library/cc725828.aspx)을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a410-113">If your RemoteApp collection is domain joined you can enforce any [Group Policy](https://technet.microsoft.com/library/cc725828.aspx) (with the exception of the Idle and Disconnect timeout policies described [here](../azure-subscription-service-limits.md)).</span></span>
2. <span data-ttu-id="6a410-114">그룹 정책에 대한 대안으로(컬렉션이 도메인에 가입되지 않거나 AD에 적절한 권한이 없는 경우), [로컬 정책](https://technet.microsoft.com/library/cc775702.aspx) 을 템플릿 이미지로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a410-114">As an alternative to Group Policy (if your collection is not domain joined or you don't have the right privileges in AD), you can configure [Local Polices](https://technet.microsoft.com/library/cc775702.aspx) into your template image.</span></span>  <span data-ttu-id="6a410-115">충돌이 발생하는 경우 해당 그룹 정책이 로컬 정책보다 우선합니다.</span><span class="sxs-lookup"><span data-stu-id="6a410-115">Note that group polices trump local policies when there is a conflict.</span></span>
3. <span data-ttu-id="6a410-116">일부 OS/앱 설정은 정책을 통해 구성할 수 없지만 템플릿 이미지를 구성하는 동안에 [RegEdit 도구](remoteapp-hybridtrouble.md)를 사용하여 레지스트리 키를 통해 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a410-116">Some OS/app settings are not configurable via policy, but can be via registry key using the [RegEdit tool](remoteapp-hybridtrouble.md) while configuring your template image.</span></span>
4. <span data-ttu-id="6a410-117">[Windows 방화벽](http://windows.microsoft.com/en-US/windows-8/Windows-Firewall-from-start-to-finish) 을 사용하여 앱이 실행 중인 컴퓨터에서/로 네트워크 액세스를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a410-117">You can use [Windows Firewall](http://windows.microsoft.com/en-US/windows-8/Windows-Firewall-from-start-to-finish) to control network access to and from the machine where the app is running.</span></span> <span data-ttu-id="6a410-118">URL 및 여기에 정의된 포트를 차단하지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a410-118">Just make sure you don't block the URLs and ports defined here.</span></span>
5. <span data-ttu-id="6a410-119">[AppLocker](https://technet.microsoft.com/library/hh831440.aspx) 를 사용하여 사용자가 실행할 수 있는 응용 프로그램 및 파일을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a410-119">You can use [AppLocker](https://technet.microsoft.com/library/hh831440.aspx) to control which applications and files users can run.</span></span> <span data-ttu-id="6a410-120">예를 들어, 전문 사용자는 게시되지 않았지만 AppLocker이 차단할 수 있는 컬렉션을 만드는데 사용되는 이미지에서 사용할 수 있는 응용 프로그램을 실행하는 방법을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a410-120">For example, savvy users can figure out how to run applications that you did not publish but that are available in the image you used to create the collection - AppLocker can block this.</span></span>

## <a name="detailed-information"></a><span data-ttu-id="6a410-121">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="6a410-121">Detailed information</span></span>
* <span data-ttu-id="6a410-122">가장 유용할 것 같은 다음 RDS 정책은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6a410-122">The following RDS policies are likely to be most useful:</span></span>
  * [<span data-ttu-id="6a410-123">장치 및 리소스 리디렉션</span><span class="sxs-lookup"><span data-stu-id="6a410-123">Device and Resource Redirection</span></span>](https://technet.microsoft.com/library/ee791794.aspx)
  * [<span data-ttu-id="6a410-124">프린터 리디렉션</span><span class="sxs-lookup"><span data-stu-id="6a410-124">Printer Redirection</span></span>](https://technet.microsoft.com/library/ee791784.aspx)
  * <span data-ttu-id="6a410-125">[프로필](https://technet.microsoft.com/library/ee791865.aspx).</span><span class="sxs-lookup"><span data-stu-id="6a410-125">[Profiles](https://technet.microsoft.com/library/ee791865.aspx).</span></span>
* <span data-ttu-id="6a410-126">RemoteApp PowerShell 모듈을 통한 리디렉션 구성([여기](remoteapp-redirection.md) 참조)은 정책을 적용할 클라이언트 컴퓨터에 따라 다르므로 보안이 주된 목표라면 템플릿 이미지 로컬 정책이나 그룹 정책을 통해 정책을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a410-126">Note that configuring redirections via the RemoteApp PowerShell module (as seen [here](remoteapp-redirection.md)) relies on the client machine to enforce the policy, so if security is the primary objective you'll want to enforce the policy via the template image local policy or via group policy.</span></span>
* <span data-ttu-id="6a410-127">[Windows Server 2012 R2 정책](https://technet.microsoft.com/library/hh831791.aspx)</span><span class="sxs-lookup"><span data-stu-id="6a410-127">[Windows Server 2012 R2 policies](https://technet.microsoft.com/library/hh831791.aspx).</span></span>
* <span data-ttu-id="6a410-128">[Office 2013 정책](https://technet.microsoft.com/library/cc178969.aspx)([Office 도구 모음을 사용자 지정하는 방법](https://technet.microsoft.com/library/cc179143.aspx) 포함)</span><span class="sxs-lookup"><span data-stu-id="6a410-128">[Office 2013 polices](https://technet.microsoft.com/library/cc178969.aspx) (including [how to customize the Office toolbar](https://technet.microsoft.com/library/cc179143.aspx)).</span></span>

