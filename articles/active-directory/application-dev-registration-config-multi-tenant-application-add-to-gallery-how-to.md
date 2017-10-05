---
title: "Azure AD 응용 프로그램 갤러리에 다중 테넌트 응용 프로그램을 추가하는 방법 | Microsoft Docs"
description: "Azure AD 응용 프로그램 갤러리에서 사용자 지정 개발 다중 테넌트 응용 프로그램을 나열하는 방법을 설명합니다."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 208f0d40bd7a8e8f35f16e1fcb09c305d833dbb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-add-a-multi-tenant-application-to-the-azure-ad-application-gallery"></a><span data-ttu-id="37789-103">Azure AD 응용 프로그램 갤러리에 다중 테넌트 응용 프로그램을 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="37789-103">How to add a multi-tenant application to the Azure AD application gallery</span></span>

## <a name="what-is-the-azure-ad-application-gallery"></a><span data-ttu-id="37789-104">Azure AD 응용 프로그램 갤러리란?</span><span class="sxs-lookup"><span data-stu-id="37789-104">What is the Azure AD Application Gallery?</span></span>

<span data-ttu-id="37789-105">Azure AD 응용 프로그램 갤러리는 수백만 명의 Azure Active Directory 고객에게 응용 프로그램을 제공하여 Marketplace에서 응용 프로그램의 영향과 범위를 넓히는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="37789-105">The Azure AD Application Gallery is a great way to get your application in front of all the millions of Azure Active Directory customers to broaden the impact and reach of your application in the marketplace.</span></span> <span data-ttu-id="37789-106">아래 단계에서는 Azure AD 응용 프로그램 갤러리에 응용 프로그램을 나열하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="37789-106">The below steps explain how you can list your application in the Azure AD Application Gallery.</span></span>

## <a name="if-your-application-supports-saml-or-openidconnect"></a><span data-ttu-id="37789-107">응용 프로그램이 SAML 또는 OpenIDConnect를 지원하는 경우</span><span class="sxs-lookup"><span data-stu-id="37789-107">If your application supports SAML or OpenIDConnect</span></span>
<span data-ttu-id="37789-108">Azure AD 응용 프로그램 갤러리에 나열하려는 다중 테넌트 응용 프로그램이 있는 경우 먼저 응용 프로그램이 다음 Single Sign-On 기술 중 하나를 지원하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37789-108">If you have a multi-tenant application you'd like to list in the Azure AD Application Gallery, you must first make sure that your application supports one of the following single sign-on technologies:</span></span>

1. <span data-ttu-id="37789-109">**OpenID Connect** - 인증을 위한 OpenID Connect 및 구성을 위한 Azure AD 동의 API를 사용하는 Azure AD과 통합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="37789-109">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and the Azure AD consent API for configuration.</span></span> <span data-ttu-id="37789-110">통합을 시작하고 응용 프로그램이 SAML을 지원하지 않으면 이것이 권장 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="37789-110">If you are just starting an integration and your application does not support SAML, then this is the recommend mode.</span></span>
2. <span data-ttu-id="37789-111">**SAML** – 응용 프로그램에는 이미 SAML 프로토콜을 사용하여 타사 ID 공급자를 구성할 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37789-111">**SAML** – Your application already has the ability to configure third-party identity providers using the SAML protocol.</span></span>

<span data-ttu-id="37789-112">응용 프로그램에서 이러한 Single Sign-On 모드 중 하나를 지원하고 Azure AD 응용 프로그램 갤러리에 다중 테넌트 응용 프로그램을 나열하려는 경우 아래 문서의 단계를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37789-112">If your application supports one of these single sign-on modes and you'd like to list your multi-tenant application in the Azure AD Application Gallery, you can follow the steps in the document below.</span></span> <span data-ttu-id="37789-113">빠르게 시작하려면 **waadpartners@microsoft.com**으로 메일을 보내세요.</span><span class="sxs-lookup"><span data-stu-id="37789-113">To get started quickly send an email to **waadpartners@microsoft.com**.</span></span>

## <a name="if-your-application-does-not-support-saml-or-openidconnect"></a><span data-ttu-id="37789-114">응용 프로그램이 SAML 또는 OpenIDConnect를 지원하지 않는 경우</span><span class="sxs-lookup"><span data-stu-id="37789-114">If your application does not support SAML or OpenIDConnect</span></span>
<span data-ttu-id="37789-115">응용 프로그램이 이러한 모드 중 하나를 지원하지 않더라도 암호 Single Sign-On 기술을 사용하여 갤러리에 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37789-115">Even if your application does not support one of these modes, we can still integrate it into our gallery using our Password Single Sign-on technology.</span></span> <span data-ttu-id="37789-116">이 옵션을 살펴보려면 **waadpartners@microsoft.com**으로 메일을 보내세요.</span><span class="sxs-lookup"><span data-stu-id="37789-116">If you'd like to explore this option, you can send an email to **waadpartners@microsoft.com**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37789-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="37789-117">Next steps</span></span>
[<span data-ttu-id="37789-118">Azure Active Directory 응용 프로그램 갤러리에 응용 프로그램을 나열하는 방법</span><span class="sxs-lookup"><span data-stu-id="37789-118">How to list your application in the Azure Active Directory application gallery</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)
