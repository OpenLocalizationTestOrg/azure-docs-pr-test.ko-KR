---
title: "Azure 응용 프로그램에서 온-프레미스 Active Directory와 aaaAuthenticate | Microsoft Docs"
description: "Hello에 온-프레미스 Active Directory와 Azure 앱 서비스 tooauthenticate 기간 업무 앱에 대 한 다른 옵션에 대 한 자세한 내용은"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: dde6b7e6-bf6a-4fa5-8390-3a18155d21bd
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: 65bf25aaa0447fbbea7c754db55842d57e70757e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-on-premises-active-directory-in-your-azure-app"></a><span data-ttu-id="0cc2c-103">Azure 앱에서 온-프레미스 Active Directory를 사용하여 인증</span><span class="sxs-lookup"><span data-stu-id="0cc2c-103">Authenticate with on-premises Active Directory in your Azure app</span></span>
<span data-ttu-id="0cc2c-104">이 문서에서는 어떻게 tooauthenticate와 온-프레미스 AD (Active Directory)에서 [Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-104">This article shows you how tooauthenticate with on-premises Active Directory (AD) in [Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> <span data-ttu-id="0cc2c-105">Azure 앱 hello 클라우드에서 호스트 되는 않는 방법으로 tooauthenticate 온-프레미스 AD 사용자가 안전 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-105">An Azure app is hosted in hello cloud, but there are ways tooauthenticate on-premises AD users securely.</span></span> 

## <a name="authenticate-through-azure-active-directory"></a><span data-ttu-id="0cc2c-106">Azure Active Directory를 통해 인증</span><span class="sxs-lookup"><span data-stu-id="0cc2c-106">Authenticate through Azure Active Directory</span></span>
<span data-ttu-id="0cc2c-107">Azure Active Directory 테넌트는 온-프레미스 AD를 사용하여 디렉터리 동기화될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-107">An Azure Active Directory tenant can be directory-synced with an on-premises AD.</span></span> <span data-ttu-id="0cc2c-108">이 방법을 AD 사용자가 앱에서 액세스할 수를 사용 하면 인터넷 hello 및 온-프레미스 자격 증명을 사용 하 여 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-108">This approach enables AD users to access your App from hello internet and authenticate using their on-premises credentials.</span></span> <span data-ttu-id="0cc2c-109">또한 Azure App Service는 [이 메서드에 대한 턴키 솔루션](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-109">Furthermore, Azure App Service provides a [turn-key solution for this method](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span> <span data-ttu-id="0cc2c-110">단추를 몇 번 클릭하여 Azure 앱에 디렉터리 동기화된 테넌트를 사용하여 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-110">With a few clicks of a button, you can enable authentication with a directory-synced tenant for your Azure app.</span></span> <span data-ttu-id="0cc2c-111">이 방법에는 다음 장점 hello:</span><span class="sxs-lookup"><span data-stu-id="0cc2c-111">This approach has hello following advantages:</span></span>

* <span data-ttu-id="0cc2c-112">앱에서 인증 코드가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-112">Does not require any authentication code in your app.</span></span> <span data-ttu-id="0cc2c-113">앱 서비스 do 인증을 hello 및에 응용 프로그램에서 기능을 제공 하 여 시간을 보낼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-113">Let App Service do hello authentication for you and spend your time on providing functionality in your app.</span></span>
* <span data-ttu-id="0cc2c-114">[Azure AD Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx) toodirectory 데이터 Azure 응용 프로그램에서 액세스 하는 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-114">[Azure AD Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx) enables access toodirectory data from your Azure app.</span></span>
* <span data-ttu-id="0cc2c-115">SSO를 너무 제공[Azure Active Directory에서 지 원하는 모든 응용 프로그램](/marketplace/active-directory/), Office 365, Dynamics CRM Online, Microsoft Intune 및 수천 개의 타사 클라우드 응용 프로그램을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-115">Provides SSO too[all applications supported by Azure Active Directory](/marketplace/active-directory/), including Office 365, Dynamics CRM Online, Microsoft Intune, and thousands of non-Microsoft cloud applications.</span></span> 
* <span data-ttu-id="0cc2c-116">Azure Active Directory는 역할 기반 액세스 제어를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-116">Azure Active Directory supports role-based access control.</span></span> <span data-ttu-id="0cc2c-117">최소한의 변경 tooyour 코드로 hello [Authorize(Roles="X")] 패턴을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-117">You can use hello [Authorize(Roles="X")] pattern with minimal changes tooyour code.</span></span>

<span data-ttu-id="0cc2c-118">확인 하려면 Azure Active Directory를 사용 하 여 인증 하는 기간 업무 Azure 앱 toowrite 어떻게 toosee [Azure Active Directory 인증 사용 Azure 기간 업무 앱을 만듭니다](web-sites-dotnet-lob-application-azure-ad.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-118">toosee how toowrite a line-of-business Azure app that authenticates with Azure Active Directory, see [Create a line-of-business Azure app with Azure Active Directory authentication](web-sites-dotnet-lob-application-azure-ad.md).</span></span>

## <a name="authenticate-through-an-on-premises-sts"></a><span data-ttu-id="0cc2c-119">온-프레미스 STS를 통해 인증</span><span class="sxs-lookup"><span data-stu-id="0cc2c-119">Authenticate through an on-premises STS</span></span>
<span data-ttu-id="0cc2c-120">온-프레미스 보안 토큰 서비스 (STS) 같은 Active Directory Federation Services (AD FS)를 사용 하도록 설정한 경우에 Azure 응용 프로그램에 대 한 toofederate 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-120">If you have an on-premises secure token service (STS) like Active Directory Federation Services (AD FS), you can use that toofederate authentication for your Azure app.</span></span> <span data-ttu-id="0cc2c-121">이 방법은 회사 정책에서 AD 데이터를 Azure에 저장하지 않도록 금지하는 경우에 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-121">This approach is best when company policy prohibits AD data from being stored in Azure.</span></span> <span data-ttu-id="0cc2c-122">그러나 note hello 다음:</span><span class="sxs-lookup"><span data-stu-id="0cc2c-122">However, note hello following:</span></span>

* <span data-ttu-id="0cc2c-123">STS 토폴로지를 온-프레미스에 배포해야 하므로 비용 및 관리 오버헤드가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-123">STS topology must be deployed on-premises, with cost and management overhead.</span></span>
* <span data-ttu-id="0cc2c-124">AD FS 관리자만 구성할 수 [신뢰 당사자 트러스트 및 클레임 규칙](http://technet.microsoft.com/library/dd807108.aspx)는 hello 개발자 옵션을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-124">Only AD FS administrators can configure [relying party trusts and claim rules](http://technet.microsoft.com/library/dd807108.aspx), which may limit hello developer's options.</span></span> <span data-ttu-id="0cc2c-125">Hello에 다른 손 가능한 toomanage 이며 사용자 지정 [클레임](http://technet.microsoft.com/library/ee913571.aspx) 응용 프로그램별 별로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-125">On hello other hand, it is possible toomanage and customize [claims](http://technet.microsoft.com/library/ee913571.aspx) on a per-application basis.</span></span>
* <span data-ttu-id="0cc2c-126">Tooon 온-프레미스 액세스 AD 데이터 hello 회사 방화벽을 통해 별도 솔루션이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-126">Access tooon-premises AD data requires a separate solution through hello corporate firewall.</span></span>

<span data-ttu-id="0cc2c-127">toowrite는 온-프레미스 STS를 사용 하 여 인증 하는 기간 업무 Azure 앱을 확인 하려면 어떻게 해야 toosee [AD FS 인증에 Azure 기간 업무 앱을 만듭니다](web-sites-dotnet-lob-application-adfs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-127">toosee how toowrite a line-of-business Azure app that authenticates with an on-premises STS, see [Create a line-of-business Azure app with AD FS authentication](web-sites-dotnet-lob-application-adfs.md).</span></span>

