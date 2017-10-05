---
title: "Teams에서 Azure AD 앱 프록시 앱 액세스 | Microsoft Docs"
description: "Azure AD 응용 프로그램 프록시를 사용하여 Microsoft Teams를 통해 온-프레미스 응용 프로그램에 액세스합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 24e22d7314de536714a825cd7035d2cec2112278
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a><span data-ttu-id="c736a-103">Microsoft Teams를 통해 온-프레미스 응용 프로그램에 액세스</span><span class="sxs-lookup"><span data-stu-id="c736a-103">Access your on-premises applications through Microsoft Teams</span></span>

<span data-ttu-id="c736a-104">Azure Active Directory 응용 프로그램 프록시는 장소에 관계없이 온-프레미스 응용 프로그램에 Single Sign-On을 제공하며, Microsoft Teams를 사용하면 한 곳에서 효율적으로 공동 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c736a-104">Azure Active Directory Application Proxy gives you single sign-on to on-premises applications no matter where you are, and Microsoft Teams streamlines your collaborative efforts in one place.</span></span> <span data-ttu-id="c736a-105">이 두 가지를 통합하면 사용자가 어떤 상황에서도 팀 동료와 협력하여 생산성을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c736a-105">Integrating the two together means that your users can be productive with their teammates in any situation.</span></span> 

<span data-ttu-id="c736a-106">사용자가 [탭을 사용](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US)하여 해당 Teams 채널에 클라우드 앱을 추가할 수 있으나 모두가 사용하는 SharePoint 사이트 또는 계획 도구가 온-프레미스에 호스트되면 어떻게 될까요?</span><span class="sxs-lookup"><span data-stu-id="c736a-106">Your users can add cloud apps to their Teams channels [using tabs](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), but what happens if that SharePoint site or planning tool they all use is hosted on-premises?</span></span> <span data-ttu-id="c736a-107">응용 프로그램 프록시는 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="c736a-107">Application Proxy is the solution.</span></span> <span data-ttu-id="c736a-108">원격으로 앱에 액세스하는 데 항상 사용하는 것과 동일한 외부 URL을 사용하여 응용 프로그램 프록시를 통해 게시된 앱을 해당 채널에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c736a-108">They can add apps published through Application Proxy to their channels using the same external URLs they always use to access their apps remotely.</span></span> <span data-ttu-id="c736a-109">응용 프로그램 프록시는 Azure Active Directory를 통해 인증하므로 동일한 Single Sign-On 환경이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c736a-109">And because Application Proxy authenticates through Azure Active Directory, the same single sign-on experience carries through.</span></span>


## <a name="install-the-application-proxy-connector-and-publish-your-app"></a><span data-ttu-id="c736a-110">응용 프로그램 프록시 커넥터 설치 및 앱 게시</span><span class="sxs-lookup"><span data-stu-id="c736a-110">Install the Application Proxy connector and publish your app</span></span>

<span data-ttu-id="c736a-111">아직 수행하지 않은 경우 [테넌트에 대해 응용 프로그램 프록시를 구성하고 커넥터를 설치](active-directory-application-proxy-enable.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c736a-111">If you haven't already, [configure Application Proxy for your tenant and install the connector](active-directory-application-proxy-enable.md).</span></span> <span data-ttu-id="c736a-112">그런 다음, 원격 액세스를 위해 [온-프레미스 응용 프로그램을 게시](application-proxy-publish-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c736a-112">Then, [publish your on-premises application](application-proxy-publish-azure-portal.md) for remote access.</span></span> <span data-ttu-id="c736a-113">앱을 게시하는 경우 외부 URL을 기록해 둡니다. 최종 사용자가 Teams에 앱을 추가하는 경우 이 정보가 필요하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="c736a-113">When you're publishing the app, make note of the external URL because your end users need that information when they add the app to Teams.</span></span>

<span data-ttu-id="c736a-114">이미 게시된 앱이 있으나 외부 URL을 기억하지 못하는 경우 [Azure Portal](https://portal.azure.com)에서 찾아보세요.</span><span class="sxs-lookup"><span data-stu-id="c736a-114">If you already have your apps published but don't remember their external URLs, look them up in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c736a-115">로그인한 다음, **Azure Active Directory** > **Enterprise 응용 프로그램** > **모든 응용 프로그램** > 앱 선택 > **응용 프로그램 프록시**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c736a-115">Sign in, then navigate to **Azure Active Directory** > **Enterprise applications** > **All applications** > select your app > **Application proxy**.</span></span>

## <a name="add-your-app-to-teams"></a><span data-ttu-id="c736a-116">Teams에 앱 추가</span><span class="sxs-lookup"><span data-stu-id="c736a-116">Add your app to Teams</span></span>

<span data-ttu-id="c736a-117">응용 프로그램 프록시를 통해 앱을 게시하면 사용자가 해당 Teams 채널에서 직접 탭으로 추가할 수 있음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c736a-117">Once you publish the app through Application Proxy, let your users know that they can add it as a tab directly in their Teams channels.</span></span> <span data-ttu-id="c736a-118">사용자가 다음 세 가지 단계를 수행하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c736a-118">Have them follow these three steps:</span></span>

1. <span data-ttu-id="c736a-119">이 앱을 추가하려는Teams 채널로 이동하여 탭을 추가할 **+**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c736a-119">Navigate to the Teams channel where you want to add this app and select **+** to add a tab.</span></span>

   ![탭 추가 선택](./media/application-proxy-teams/add-tab.png)

2. <span data-ttu-id="c736a-121">탭 옵션에서 **웹 사이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c736a-121">Select **Website** from the tab options.</span></span>

   ![웹 사이트 추가](./media/application-proxy-teams/website.png)

3. <span data-ttu-id="c736a-123">탭 이름을 지정하고 URL을 응용 프로그램 프록시 외부 URL로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c736a-123">Give the tab a name and set the URL to the Application Proxy external URL.</span></span> 

   ![탭 이름 및 URL 구성](./media/application-proxy-teams/tab-name-url.png)

<span data-ttu-id="c736a-125">팀의 한 멤버가 탭을 추가하면 채널의 모든 사용자에게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c736a-125">Once one member of a team adds the tab, it shows up for everyone in the channel.</span></span> <span data-ttu-id="c736a-126">앱에 대한 액세스 권한이 있는 모든 사용자에게는 Microsoft Teams에 사용하는 자격 증명으로 Single Sign-On 액세스가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c736a-126">Any users who have access to the app get single sign-on access with the credentials they use for Microsoft Teams.</span></span> <span data-ttu-id="c736a-127">앱에 대한 액세스 권한이 없는 사용자에게는 Teams에 탭이 표시되지만 온-프레미스 앱 및 Azure Portal 게시 버전 앱에 대한 권한이 부여될 때까지 액세스가 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="c736a-127">Any users who don't have access to the app will see the tab in Teams, but are blocked until you give them permissions to the on-premises app and the Azure portal published version of the app.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c736a-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c736a-128">Next steps</span></span>

- <span data-ttu-id="c736a-129">응용 프로그램 프록시를 통해 [온-프레미스 SharePoint 사이트를 게시](application-proxy-enable-remote-access-sharepoint.md)하는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="c736a-129">Learn how to [publish on-premises SharePoint sites](application-proxy-enable-remote-access-sharepoint.md) with Application Proxy.</span></span>
- <span data-ttu-id="c736a-130">앱에서 외부 URL에 대해 [사용자 지정 도메인](active-directory-application-proxy-custom-domains.md)을 사용하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c736a-130">Configure your apps to use [custom domains](active-directory-application-proxy-custom-domains.md) for their external URL.</span></span> 
