---
title: "Azure Active Directory에서 SAML 기반 Single Sign-On을 응용 프로그램에 디버그하는 방법 | Microsoft Docs"
description: "Azure Active Directory에서 SAML 기반 Single Sign-On을 응용 프로그램에 디버그하는 방법을 알아봅니다. "
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: edbe492b-1050-4fca-a48a-d1fa97d47815
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.custom: aaddev
ms.reviewer: dastrock
ms.openlocfilehash: 31447d597296bac57481dc2acb4a95ee3a104161
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-debug-saml-based-single-sign-on-to-applications-in-azure-active-directory"></a><span data-ttu-id="e0ca9-103">Azure Active Directory에서 SAML 기반 Single Sign-On을 응용 프로그램에 디버그하는 방법</span><span class="sxs-lookup"><span data-stu-id="e0ca9-103">How to debug SAML-based single sign-on to applications in Azure Active Directory</span></span>
<span data-ttu-id="e0ca9-104">SAML 기반 응용 프로그램 통합을 디버그할 때 종종 [Fiddler](http://www.telerik.com/fiddler) 와 같은 도구를 사용하여 SAML 요청, SAML 응답 및 응용 프로그램에 발급된 실제 SAML 토큰을 확인하는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ca9-104">When debugging a SAML-based application integration, it is often helpful to use a tool like [Fiddler](http://www.telerik.com/fiddler) to see the SAML request, the SAML response, and the actual SAML token that is issued to the application.</span></span> <span data-ttu-id="e0ca9-105">SAML 토큰을 검사하면 모든 필수 특성, SAML 주체의 사용자 이름 및 발급자 URI가 예상대로 제공되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ca9-105">By examining the SAML token, you can ensure that all of the required attributes, the username in the SAML subject, and the issuer URI are coming through as expected.</span></span>

![][1]

<span data-ttu-id="e0ca9-106">SAML 토큰이 포함된 Azure AD의 응답은 일반적으로 https://login.windows.net에서 HTTP 302가 리디렉션되고 응용 프로그램의 구성된 **회신 URL**로 전송된 후에 발생하는 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="e0ca9-106">The response from Azure AD that contains the SAML token is typically the one that occurs after an HTTP 302 redirect from https://login.windows.net, and is sent to the configured **Reply URL** of the application.</span></span> 

<span data-ttu-id="e0ca9-107">이 줄을 선택한 다음 오른쪽 패널에서 **Inspectors > WebForms** 탭을 선택하여 SAML 토큰을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ca9-107">You can view the SAML token by selecting this line and then selecting the **Inspectors > WebForms** tab in the right panel.</span></span> <span data-ttu-id="e0ca9-108">여기에서 **SAMLResponse** 값을 마우스 오른쪽 단추로 클릭하고 **Send to TextWizard**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ca9-108">From there, right-click the **SAMLResponse** value and select **Send to TextWizard**.</span></span> <span data-ttu-id="e0ca9-109">그런 다음 **Transform** 메뉴에서 **From Base64**를 선택하여 토큰을 디코딩하고 해당 콘텐츠를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ca9-109">Then select **From Base64** from the **Transform** menu to decode the token and see its contents.</span></span>

<span data-ttu-id="e0ca9-110">**참고**: 이 HTTP 요청의 콘텐츠를 보려는 경우 Fiddler에서 수행해야 하는 HTTPS 트래픽의 암호 해독을 구성하라는 메시지를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ca9-110">**Note**: To see the contents of this HTTP request, Fiddler may prompt you to configure decryption of HTTPS traffic, which you will need to do.</span></span>

## <a name="related-articles"></a><span data-ttu-id="e0ca9-111">관련 문서</span><span class="sxs-lookup"><span data-stu-id="e0ca9-111">Related Articles</span></span>
* [<span data-ttu-id="e0ca9-112">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="e0ca9-112">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="e0ca9-113">Azure Active Directory 응용 프로그램 갤러리에 있지 않은 응용 프로그램에 Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="e0ca9-113">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="e0ca9-114">사전 통합된 앱에 대해 SAML 토큰에서 발급된 클레임을 사용자 지정하는 방법</span><span class="sxs-lookup"><span data-stu-id="e0ca9-114">How to Customize Claims Issued in the SAML Token for Pre-Integrated Apps</span></span>](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png