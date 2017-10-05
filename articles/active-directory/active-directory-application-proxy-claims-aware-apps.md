---
title: "클레임 인식 앱 - Azure AD 앱 프록시 | Microsoft Docs"
description: "사용자의 안전한 원격 액세스를 위해 ADFS 클레임을 허용하는 온-프레미스 ASP.NET 응용 프로그램을 게시하는 방법입니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 5784222608b01509fc4ff84b1a8792cbcfea89e6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a><span data-ttu-id="e2656-103">응용 프로그램 프록시에서 클레임 인식 앱으로 작업</span><span class="sxs-lookup"><span data-stu-id="e2656-103">Working with claims-aware apps in Application Proxy</span></span>
<span data-ttu-id="e2656-104">[클레임 인식 앱](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx)은 STS(보안 토큰 서비스)에 대한 리디렉션을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e2656-104">[Claims-aware apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) perform a redirection to the Security Token Service (STS).</span></span> <span data-ttu-id="e2656-105">STS는 토큰의 교환으로 사용자의 자격 증명을 요청한 다음 응용 프로그램에 사용자를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="e2656-105">The STS requests credentials from the user in exchange for a token and then redirects the user to the application.</span></span> <span data-ttu-id="e2656-106">응용 프로그램 프록시를 이러한 리디렉션과 함께 작동하도록 하는 몇 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2656-106">There are a few ways to enable Application Proxy to work with these redirects.</span></span> <span data-ttu-id="e2656-107">이 문서를 사용하여 클레임 인식 앱에 대한 배포를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e2656-107">Use this article to configure your deployment for claims-aware apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e2656-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e2656-108">Prerequisites</span></span>
<span data-ttu-id="e2656-109">클레임 인식 앱이 리디렉션되는 STS가 온-프레미스 네트워크 외부에서 사용 가능한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e2656-109">Make sure that the STS that the claims-aware app redirects to is available outside of your on-premises network.</span></span> <span data-ttu-id="e2656-110">프록시를 통해 노출하거나 외부 연결을 허용하여 STS를 사용할 수 있도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2656-110">You can make the STS available by exposing it through a proxy or by allowing outside connections.</span></span> 

## <a name="publish-your-application"></a><span data-ttu-id="e2656-111">응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="e2656-111">Publish your application</span></span>

1. <span data-ttu-id="e2656-112">[응용 프로그램 프록시로 응용 프로그램 게시](application-proxy-publish-azure-portal.md)에 설명된 지침에 따라 응용 프로그램을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="e2656-112">Publish your application according to the instructions described in [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>
2. <span data-ttu-id="e2656-113">포털에서 응용 프로그램 페이지로 이동하고 **Single Sign-On**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2656-113">Navigate to the application page in the portal and select **Single sign-on**.</span></span>
3. <span data-ttu-id="e2656-114">**Azure Active Directory**를 **사전 인증 방법**으로 선택했다면 **Azure AD Single Sign-On 비활성화**를 **내부 인증 방법**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2656-114">If you chose **Azure Active Directory** as your **Preauthentication Method**, select **Azure AD single sign-on disabled** as your **Internal Authentication Method**.</span></span> <span data-ttu-id="e2656-115">**사전 인증 방법**으로 **통과**를 선택하면 아무 것도 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e2656-115">If you chose **Passthrough** as your **Preauthentication Method**, you don't need to change anything.</span></span>

## <a name="configure-adfs"></a><span data-ttu-id="e2656-116">ADFS 구성</span><span class="sxs-lookup"><span data-stu-id="e2656-116">Configure ADFS</span></span>

<span data-ttu-id="e2656-117">두 가지 방법 중 하나에서 클레임 인식 앱에 대한 ADFS를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2656-117">You can configure ADFS for claims-aware apps in one of two ways.</span></span> <span data-ttu-id="e2656-118">첫 번째는 사용자 지정 도메인을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e2656-118">The first is by using custom domains.</span></span> <span data-ttu-id="e2656-119">두 번째는 WS-Federation을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e2656-119">The second is with WS-Federation.</span></span> 

### <a name="option-1-custom-domains"></a><span data-ttu-id="e2656-120">옵션 1: 사용자 지정 도메인</span><span class="sxs-lookup"><span data-stu-id="e2656-120">Option 1: Custom domains</span></span>

<span data-ttu-id="e2656-121">응용 프로그램에 대한 모든 내부 URL이 FQDN(정규화된 도메인 이름)인 경우 응용 프로그램에 대한 [사용자 지정 도메인](active-directory-application-proxy-custom-domains.md)을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2656-121">If all the internal URLs for your applications are fully qualified domain names (FQDNs), then you can configure [custom domains](active-directory-application-proxy-custom-domains.md) for your applications.</span></span> <span data-ttu-id="e2656-122">사용자 지정 도메인을 사용하여 내부 URL과 동일한 외부 URL을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e2656-122">Use the custom domains to create external URLs that are the same as the internal URLs.</span></span> <span data-ttu-id="e2656-123">외부 URL이 내부 URL과 일치하는 경우 사용자가 온-프레미스 또는 원격인지 관계 없이 STS 리디렉션이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="e2656-123">When your external URLs match your internal URLs, then the STS redirections work whether your users are on-premises or remote.</span></span> 

### <a name="option-2-ws-federation"></a><span data-ttu-id="e2656-124">옵션 2: WS-Federation</span><span class="sxs-lookup"><span data-stu-id="e2656-124">Option 2: WS-Federation</span></span>

1. <span data-ttu-id="e2656-125">ADFS 관리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2656-125">Open ADFS Management.</span></span>
2. <span data-ttu-id="e2656-126">**신뢰 당사자 트러스트**로 이동하여 응용 프로그램 프록시로 게시하려는 앱을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2656-126">Go to **Relying Party Trusts**, right-click on the app you are publishing with Application Proxy, and choose **Properties**.</span></span>  

   ![신뢰 당사자 트러스트 앱 이름을 마우스 오른쪽 단추로 클릭 - 스크린샷](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. <span data-ttu-id="e2656-128">**끝점** 탭에 있는 **끝점 유형** 아래에서 **WS-Federation**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2656-128">On the **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.</span></span>
4. <span data-ttu-id="e2656-129">**신뢰할 수 있는 URL** 아래에 **외부 URL** 아래에 있는 응용 프로그램 프록시에 입력한 URL을 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e2656-129">Under **Trusted URL**, enter the URL you entered in the Application Proxy under **External URL** and click **OK**.</span></span>  

   ![끝점 추가 - 신뢰할 수 있는 URL 값 설정 - 스크린샷](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a><span data-ttu-id="e2656-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e2656-131">Next steps</span></span>
* <span data-ttu-id="e2656-132">클레임 인식이 아닌 응용 프로그램에 대한 [Single Sign-On 사용](application-proxy-sso-overview.md)</span><span class="sxs-lookup"><span data-stu-id="e2656-132">[Enable single-sign on](application-proxy-sso-overview.md) for applications that aren't claims-aware</span></span>
* [<span data-ttu-id="e2656-133">네이티브 클라이언트 앱을 사용하여 프록시 응용 프로그램과 상호 작용</span><span class="sxs-lookup"><span data-stu-id="e2656-133">Enable native client apps to interact with proxy applications</span></span>](active-directory-application-proxy-native-client.md)


