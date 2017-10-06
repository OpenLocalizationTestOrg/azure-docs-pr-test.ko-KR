---
title: "SAML 기반 single sign on tooapplications Azure Active Directory에서 aaaHow toodebug | Microsoft Docs"
description: "자세한 내용은 방법 toodebug SAML 기반 single sign on tooapplications Azure Active Directory에 "
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
ms.openlocfilehash: 846c7b3497c8842947c5b406f4362b9e06785b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-saml-based-single-sign-on-tooapplications-in-azure-active-directory"></a><span data-ttu-id="242d5-103">어떻게 toodebug SAML 기반 single sign on tooapplications Azure Active Directory에</span><span class="sxs-lookup"><span data-stu-id="242d5-103">How toodebug SAML-based single sign-on tooapplications in Azure Active Directory</span></span>
<span data-ttu-id="242d5-104">SAML 기반 응용 프로그램 통합을 디버깅할 때 종종 유용한 toouse 도구 이므로 같은 [Fiddler](http://www.telerik.com/fiddler) toosee hello SAML 요청, hello SAML 응답 및 toohello 응용 프로그램에 발급 된 hello 실제 SAML 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="242d5-104">When debugging a SAML-based application integration, it is often helpful toouse a tool like [Fiddler](http://www.telerik.com/fiddler) toosee hello SAML request, hello SAML response, and hello actual SAML token that is issued toohello application.</span></span> <span data-ttu-id="242d5-105">Hello SAML 토큰을 검사 하 여 hello의 모든 필수 특성 확인, hello hello SAML 주체에 대 한 사용자 이름 및 발급자 예상 대로 URI를 통해 들어오는 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="242d5-105">By examining hello SAML token, you can ensure that all of hello required attributes, hello username in hello SAML subject, and hello issuer URI are coming through as expected.</span></span>

![][1]

<span data-ttu-id="242d5-106">hello hello SAML 토큰을 포함 하는 Azure AD의 응답은 일반적으로 hello https://login.windows.net에서 HTTP 302 리디렉션 후 발생 하 고 보낸된 toohello 구성 **회신 URL** hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="242d5-106">hello response from Azure AD that contains hello SAML token is typically hello one that occurs after an HTTP 302 redirect from https://login.windows.net, and is sent toohello configured **Reply URL** of hello application.</span></span> 

<span data-ttu-id="242d5-107">이 줄을 선택 하 고 hello를 선택 하 여 hello SAML 토큰을 볼 수 있습니다 **검사자 > WebForms** hello 오른쪽 패널의 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="242d5-107">You can view hello SAML token by selecting this line and then selecting hello **Inspectors > WebForms** tab in hello right panel.</span></span> <span data-ttu-id="242d5-108">여기에서 마우스 오른쪽 단추로 클릭 hello **SAMLResponse** 값 및 선택 **tooTextWizard 보낼**합니다.</span><span class="sxs-lookup"><span data-stu-id="242d5-108">From there, right-click hello **SAMLResponse** value and select **Send tooTextWizard**.</span></span> <span data-ttu-id="242d5-109">다음 선택 **에서 Base64** hello에서 **변환** 메뉴 toodecode hello 토큰 및 해당 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="242d5-109">Then select **From Base64** from hello **Transform** menu toodecode hello token and see its contents.</span></span>

<span data-ttu-id="242d5-110">**참고**: toosee hello 내용의이 HTTP 요청, Fiddler 묻는 메시지를 tooconfigure 암호 해독 해야 HTTPS 트래픽의 toodo 합니다.</span><span class="sxs-lookup"><span data-stu-id="242d5-110">**Note**: toosee hello contents of this HTTP request, Fiddler may prompt you tooconfigure decryption of HTTPS traffic, which you will need toodo.</span></span>

## <a name="related-articles"></a><span data-ttu-id="242d5-111">관련 문서</span><span class="sxs-lookup"><span data-stu-id="242d5-111">Related Articles</span></span>
* [<span data-ttu-id="242d5-112">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="242d5-112">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="242d5-113">Single sign on tooapplications hello Azure Active Directory 응용 프로그램 갤러리에 없는 구성</span><span class="sxs-lookup"><span data-stu-id="242d5-113">Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="242d5-114">tooCustomize 클레임 발급 방식 hello Pre-Integrated 앱에 대 한 SAML 토큰</span><span class="sxs-lookup"><span data-stu-id="242d5-114">How tooCustomize Claims Issued in hello SAML Token for Pre-Integrated Apps</span></span>](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png