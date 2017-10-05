---
title: "로그인 및 액세스 패널 페이지에 회사 브랜딩 추가"
description: "회사 브랜딩을 Azure 로그인 페이지 및 액세스 패널 페이지에 추가하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f74621b4-4ef0-4899-8c0e-0c20347a8c31
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/23/2017
ms.author: curtand
ms.openlocfilehash: c558bd5f2b7fae91483cc2c6724c40442bb65045
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-company-branding-to-your-sign-in-and-access-panel-pages"></a><span data-ttu-id="d4ddb-103">로그인 및 액세스 패널 페이지에 회사 브랜딩 추가</span><span class="sxs-lookup"><span data-stu-id="d4ddb-103">Add company branding to your sign-in and Access Panel pages</span></span>
<span data-ttu-id="d4ddb-104">혼동을 피하기 위해 대부분의 회사는 관리하는 모든 웹 사이트 및 서비스에 일관된 모양과 느낌을 적용하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="d4ddb-105">Azure Active Directory는 회사 로고 및 사용자 지정 색 구성표를 포함하도록 다음의 웹 페이지의 외관을 사용자 지정하는 방식으로 이 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-105">Azure Active Directory provides this capability by allowing you to customize the appearance of the following web pages with your company logo and custom color schemes:</span></span>

* <span data-ttu-id="d4ddb-106">**로그인 페이지** - 이 페이지는 Office 365 또는 Azure AD를 ID 공급자로 사용하는 기타 웹 기반 응용 프로그램에 로그인할 경우에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-106">**Sign-in page** - This is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="d4ddb-107">홈 영역 검색하는 동안 또는 자격 증명을 입력하는 경우 이 페이지와 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-107">You interact with this page either during a Home Realm Discovery or to enter your credentials.</span></span> <span data-ttu-id="d4ddb-108">홈 영역 검색을 사용하면 시스템에서 해당 온-프레미스 STS(예: AD FS)에 페더레이션된 사용자를 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-108">The Home Realm Discovery allows the system to redirect federated users to their on-premises STS (such as AD FS).</span></span>
* <span data-ttu-id="d4ddb-109">**액세스 패널 페이지** - 액세스 패널은 Azure AD 관리자가 사용자에게 액세스 권한을 부여한 클라우드 기반 응용 프로그램을 보고 시작할 수 있도록 하는 웹 기반 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-109">**Access Panel page** - The Access Panel is a web-based portal that allows you to view and launch the cloud-based applications your Azure AD administrator has granted you access to.</span></span> <span data-ttu-id="d4ddb-110">액세스 패널에 액세스하려면 다음 URL을 사용합니다. [https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="d4ddb-110">To access the Access Panel, use the following URL: [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>

<span data-ttu-id="d4ddb-111">이 항목에서는 로그인 페이지와 액세스 패널 페이지를 사용자 지정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-111">This topic explains how you can customize the sign-in page and the access panel page.</span></span>

> [!NOTE]
> * <span data-ttu-id="d4ddb-112">회사 브랜딩은 Azure Active Directory의 Premium 또는 Basic Edition으로 업그레이드하거나 Office 365 사용자인 경우에만 사용할 수 있는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-112">Company branding is a feature that is available only if you upgraded to the Premium or Basic edition of Azure Active Directory, or are an Office 365 user.</span></span> <span data-ttu-id="d4ddb-113">자세한 내용은 [Azure Active Directory 버전](active-directory-editions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-113">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>
> * <span data-ttu-id="d4ddb-114">Azure Active Directory Premium 및 Basic 버전은 Azure Active Directory 전 세계 인스턴스를 사용하여 중국의 고객에게 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-114">Azure Active Directory Premium and Basic editions are available for customers in China using the worldwide instance of Azure Active Directory.</span></span> <span data-ttu-id="d4ddb-115">Azure Active Directory Premium 및 Basic 버전은 현재 중국 21Vianet이 운영하는 Microsoft Azure에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-115">Azure Active Directory Premium and Basic editions are not currently supported in the Microsoft Azure service operated by 21Vianet in China.</span></span> <span data-ttu-id="d4ddb-116">자세한 내용은 [Azure Active Directory 포럼](https://feedback.azure.com/forums/169401-azure-active-directory/)을 통해 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-116">For more information, contact us at the [Azure Active Directory Forum](https://feedback.azure.com/forums/169401-azure-active-directory/).</span></span>
>
>

## <a name="customizing-the-sign-in-page"></a><span data-ttu-id="d4ddb-117">로그인 페이지 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="d4ddb-117">Customizing the sign-in page</span></span>
<span data-ttu-id="d4ddb-118">일반적으로 조직이 구독하는 클라우드 앱 및 서비스에 대해 브라우저 기반 액세스가 필요한 경우 로그인 페이지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-118">Typically, if you need browser-based access to your cloud apps and services that your organization subscribes to, you use the sign-in page.</span></span>

<span data-ttu-id="d4ddb-119">로그인 페이지에 변경 내용을 적용할 경우 변경 내용을 표시하려면 최대 1시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-119">If you have applied changes to your sign-in page, it can take up to an hour for the changes to appear.</span></span>

<span data-ttu-id="d4ddb-120">https://outlook.com/**contoso**.com 또는 https://mail.**contoso**.com과 같은 테넌트 특정 URL로 서비스를 이용할 경우 브랜드가 지정된 로그인 페이지만이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-120">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span></span>

<span data-ttu-id="d4ddb-121">비테넌트 특정 URL (예: https://mail.office365.com ) 을 사용하여 서비스에 방문하는 경우 브랜드가 지정되지 않은 로그인 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-121">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span></span> <span data-ttu-id="d4ddb-122">이 경우에 사용자 ID를 입력하거나 사용자 타일을 선택하면 브랜딩이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-122">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="d4ddb-123">도메인 이름은 브랜딩을 구성한 Azure 클래식 포털의 **Active Directory** > **디렉터리** > **도메인** 섹션에 “활성”으로 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-123">Your domain name must appear as “Active” in the **Active Directory** > **Directory** > **Domains** section of the Azure classic portal where you have configured branding.</span></span>
> * <span data-ttu-id="d4ddb-124">로그인 페이지 브랜딩은 Microsoft의 소비자 로그인 페이지에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-124">Sign-in page branding doesn’t carry over to the consumer sign in page of Microsoft.</span></span> <span data-ttu-id="d4ddb-125">개인 Microsoft 계정으로 로그인한 사용자는 Azure AD에서 렌더링하는 브랜드가 지정된 사용자 타일 목록을 볼 수 있지만 조직의 브랜딩이 Microsoft 계정 로그인 페이지에 적용되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-125">If you sign in with a personal Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but the branding of your organization does not apply to the Microsoft account sign-in page.</span></span>
>
>

<span data-ttu-id="d4ddb-126">이 페이지에 회사 브랜드, 색 및 기타 사용자지정 가능한 요소를 표시하려면 다음 이미지를 참조하여 두 환경의 차이를 이해하세요.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-126">If you want to show your company brand, colors and other customizable elements on this page, see the following images to understand the difference between the two experiences.</span></span>

<span data-ttu-id="d4ddb-127">다음 스크린샷은 사용자 지정을 하기 **전에** 데스크톱 컴퓨터에서 Office 365 로그인 페이지에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-127">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **before** a customization:</span></span>

![사용자 지정하기 전 Office 365 로그인 페이지][1]

<span data-ttu-id="d4ddb-129">다음 스크린샷은 사용자 지정 **후** 데스크톱 컴퓨터 Office 365 로그인 페이지의 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-129">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **after** a customization:</span></span>

![사용자 지정한 후 Office 365 로그인 페이지][2]

<span data-ttu-id="d4ddb-131">다음 스크린샷은 사용자 지정 **전** 모바일 장치 Office 365 로그인 페이지의 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-131">The following screenshot shows an example of the Office 365 sign-in page on a mobile device **before** a customization:</span></span>

![사용자 지정하기 전 Office 365 로그인 페이지][3]

<span data-ttu-id="d4ddb-133">다음 스크린샷은 사용자 지정 **후** 모바일 장치 Office 365 로그인 페이지의 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-133">The following screenshot shows an example of the Office 365 sign-in page on a mobile device **after** a customization:</span></span>

![사용자 지정한 후 Office 365 로그인 페이지][4]

<span data-ttu-id="d4ddb-135">브라우저 창의 크기를 조정할 때 앞에 표시된 그림처럼 흔히 큰 그림은 다양한 화면의 가로 세로 비율에 맞게 잘립니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-135">When you resize a browser window, the large Illustration, like the one shown previously, is often cropped to accommodate different screen aspect ratios.</span></span> <span data-ttu-id="d4ddb-136">따라서 그림에서 주요 시각적 요소가 항상 왼쪽 위 모서리(오른쪽에서 왼쪽으로 쓰는 언어의 경우 오른쪽 위)에 나타나도록 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-136">With this in mind, you should try to keep the key visual elements in the illustration so that they always appear in the top-left corner (top-right for right-to-left languages).</span></span> <span data-ttu-id="d4ddb-137">일반적으로 크기 조정은 오른쪽 아래 모서리에서 발생하여 위쪽/왼쪽으로 이동하거나 아래쪽에서 위쪽으로 이동하기 때문에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-137">This is important because resizing typically occurs from the bottom-right corner going towards the top / left or from the bottom towards the top.</span></span>

<span data-ttu-id="d4ddb-138">다음 그림은 브라우저 크기가 왼쪽에 맞게 조정될 때 그림이 어떻게 잘리는지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-138">The following picture shows how the illustration is cropped when the browser is resized to the left:</span></span>

![][6]

<span data-ttu-id="d4ddb-139">다음은 브라우저가 위쪽으로 크기 조정된 후에 표시되는 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-139">Here is how it appears after the browser is resized toward the top:</span></span>

![][7]

## <a name="what-elements-on-the-page-can-i-customize"></a><span data-ttu-id="d4ddb-140">페이지에서 어떤 요소를 사용자 지정할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="d4ddb-140">What elements on the page can I customize?</span></span>
<span data-ttu-id="d4ddb-141">로그인 페이지에서는 다음과 같은 요소를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-141">You can customize the following elements on the sign-in page:</span></span>

![][5]

| <span data-ttu-id="d4ddb-142">페이지 요소</span><span class="sxs-lookup"><span data-stu-id="d4ddb-142">Page element</span></span> | <span data-ttu-id="d4ddb-143">페이지에서의 위치</span><span class="sxs-lookup"><span data-stu-id="d4ddb-143">Location on the page</span></span> |
|:--- | --- |
| <span data-ttu-id="d4ddb-144">배너 로고</span><span class="sxs-lookup"><span data-stu-id="d4ddb-144">Banner Logo</span></span> |<span data-ttu-id="d4ddb-145">페이지 오른쪽 상단에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-145">Shown at the top-right of the page.</span></span> <span data-ttu-id="d4ddb-146">로그인하는 대상 사이트(예:</span><span class="sxs-lookup"><span data-stu-id="d4ddb-146">Replaces the logo the destination site you are signing in to displays (For example.</span></span> <span data-ttu-id="d4ddb-147">Office 365 또는 Azure)에 일반적으로 표시되는 로고를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-147">Office 365 or Azure).</span></span> |
| <span data-ttu-id="d4ddb-148">큰 그림/배경색</span><span class="sxs-lookup"><span data-stu-id="d4ddb-148">Large Illustration / Background Color</span></span> |<span data-ttu-id="d4ddb-149">페이지 왼쪽에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-149">Shown at the left of the page.</span></span> <span data-ttu-id="d4ddb-150">로그인하는 대상 사이트에 표시할 이미지를 교체합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-150">Replaces the image the destination site you are signing in to displays.</span></span> <span data-ttu-id="d4ddb-151">낮은 대역폭 연결이나 좁은 화면에서는 배경색이 큰 그림 대신 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-151">The Background Color may be shown in place of the Large Illustration on low bandwidth connections, or on narrow screens.</span></span> |
| <span data-ttu-id="d4ddb-152">로그인 유지</span><span class="sxs-lookup"><span data-stu-id="d4ddb-152">Keep me signed-in</span></span> |<span data-ttu-id="d4ddb-153">암호 텍스트 상자 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-153">Shown under the Password textbox.</span></span> |
| <span data-ttu-id="d4ddb-154">로그인 페이지 텍스트</span><span class="sxs-lookup"><span data-stu-id="d4ddb-154">Sign-in Page Text</span></span> |<span data-ttu-id="d4ddb-155">회사 또는 학교 계정으로 로그인하기 전에 유용한 정보를 전달해야 하는 경우 페이지 바닥글 위에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-155">Shown above the page footer when you need to convey helpful information before a sign-in with a work or school account.</span></span> <span data-ttu-id="d4ddb-156">예를 들어 지원 센터 전화 번호나 법적 고지 사항을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-156">For example, you may want to include the phone number to your help desk, or a legal statement.</span></span> |

> [!NOTE]
> <span data-ttu-id="d4ddb-157">모든 요소는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-157">All elements are optional.</span></span> <span data-ttu-id="d4ddb-158">예를 들어 배너 로고는 지정하고 큰 그림은 지정하지 않으면 로그인 페이지에는 대상 사이트에 대한 로고와 그림(예: Office 365 캘리포니아 고속도로 이미지)이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-158">For example, if you specify a Banner Logo but no Large Illustration, the sign-in page shows your logo and the illustration for the destination site (that is, the Office 365 California highway image).</span></span>
>
>

<span data-ttu-id="d4ddb-159">로그인 페이지의 **로그인 유지** 확인란은 사용자가 브라우저를 닫았다가 다시 열 때 로그인 상태를 유지할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-159">On your sign-in page, the **Keep me signed in** checkbox allows a user to remain signed in when they close and re-open their browser.</span></span> <span data-ttu-id="d4ddb-160">세션 수명에는 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-160">It does not effect session lifetime.</span></span> <span data-ttu-id="d4ddb-161">이 확인란을 Azure Active Directory 로그인 페이지에서 숨길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-161">You can hide the checkbox on the Azure Active Directory sign-in page.</span></span>

<span data-ttu-id="d4ddb-162">확인란 표시 여부는 **KMSI 숨기기** 설정에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-162">Whether the checkbox is displayed depends on the setting of **Hide KMSI**.</span></span>

![][9]

<span data-ttu-id="d4ddb-163">확인란을 숨기려면 이 설정을 **숨겨짐**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-163">To hide the checkbox, configure this setting to **Hidden**.</span></span>

> [!NOTE]
> <span data-ttu-id="d4ddb-164">SharePoint Online과 Office 2010의 일부 기능은 이 확인란을 선택할 수 있는 사용자에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-164">Some features of SharePoint Online and Office 2010 depend on users being able to check this box.</span></span> <span data-ttu-id="d4ddb-165">이 설정을 숨겨짐으로 구성하면 사용자에게 로그인을 요청하는 예상치 못한 메시지가 추가로 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-165">If you configure this setting to hidden, your users may see additional and unexpected prompts to sign-in.</span></span>
>
>

<span data-ttu-id="d4ddb-166">이 페이지의 모든 요소를 지역화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-166">You can also localize all elements on this page.</span></span> <span data-ttu-id="d4ddb-167">"기본" 사용자 지정 요소 집합을 구성한 후 다른 로캘로 추가 버전을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-167">Once you’ve configured a “default” set of customization elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="d4ddb-168">다양한 요소를 적절히 조합하여 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-168">You can also mix and match various elements.</span></span> <span data-ttu-id="d4ddb-169">예를 들어 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-169">For example, you can:</span></span>

* <span data-ttu-id="d4ddb-170">모든 문화권에 적용되는 "기본" 큰 그림을 만든 다음 영어와 프랑스어에 대한 특정 버전을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-170">Create a “default” Large Illustration that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="d4ddb-171">다른 모든 언어에 대해 기본 그림이 표시되는 반면 이 두 언어 중 하나로 브라우저를 설정하면 특정 이미지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-171">When you set your browsers to one of these two languages, the specific image appears, while the default illustration appears for all other languages.</span></span>
* <span data-ttu-id="d4ddb-172">조직에 따라 다른 로고를 구성합니다(예: 일본어 또는 히브리어 버전).</span><span class="sxs-lookup"><span data-stu-id="d4ddb-172">Configure different logos for your organization (e.g. Japanese or Hebrew versions).</span></span>

## <a name="access-panel-page-customization"></a><span data-ttu-id="d4ddb-173">액세스 패널 페이지 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="d4ddb-173">Access panel page customization</span></span>
<span data-ttu-id="d4ddb-174">액세스 패널 페이지는 기본적으로 관리자가 액세스 권한을 부여한 클라우드 앱에 빠른 액세스가 가능한 포털 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-174">The Access Panel page is essentially a portal page for quick access to the cloud apps you have been granted access to by your administrator.</span></span> <span data-ttu-id="d4ddb-175">이 페이지에서 앱을 클릭 가능한 응용 프로그램 타일로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-175">On this page, your apps appear as clickable application tiles.</span></span>

<span data-ttu-id="d4ddb-176">다음 스크린샷에서 사용자 지정 후 액세스 패널 페이지의 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-176">The following screenshot shows an example of an access panel page after customization.</span></span>

![][8]

## <a name="configure-your-directory-with-company-branding"></a><span data-ttu-id="d4ddb-177">회사 브랜딩으로 디렉터리 구성</span><span class="sxs-lookup"><span data-stu-id="d4ddb-177">Configure your directory with company branding</span></span>
<span data-ttu-id="d4ddb-178">Azure 클래식 포털에서 디렉터리당 하나의 기본 사용자 지정 가능 요소 집합을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-178">You can configure one default set of customizable elements per directory in the Azure classic portal.</span></span> <span data-ttu-id="d4ddb-179">기본값을 저장한 후 관리자는 다양한 언어/로캘로 각 요소의 지역화된 버전을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-179">After the defaults have been saved, an administrator can add localized versions of each element, for different languages / locales.</span></span> <span data-ttu-id="d4ddb-180">모든 사용자 지정 가능한 요소는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-180">All customizable elements are optional.</span></span>

<span data-ttu-id="d4ddb-181">예를 들어 기본 배너 로고는 구성하고 큰 그림은 구성하지 않을 경우 로그인 페이지에서 오른쪽 위 모서리에 로고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-181">For example, if you configure a default Banner Logo but no Large Illustration, the sign-in page displays your logo in the upper-right corner.</span></span> <span data-ttu-id="d4ddb-182">하지만 사이트의 기본 그림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-182">However the default illustration of the site is displayed.</span></span>

<span data-ttu-id="d4ddb-183">다음과 같은 구성을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-183">Imagine the following configuration:</span></span>

* <span data-ttu-id="d4ddb-184">영어로 표시된 기본 배너 로고 및 로그인 페이지 텍스트</span><span class="sxs-lookup"><span data-stu-id="d4ddb-184">A default Banner Logo and Sign-In Page Text in English</span></span>
* <span data-ttu-id="d4ddb-185">독일어에 대한 로그인 페이지 텍스트</span><span class="sxs-lookup"><span data-stu-id="d4ddb-185">A language-specific sign in Page Text for German</span></span>

<span data-ttu-id="d4ddb-186">언어 기본 설정이 독일어인 경우 독일어 텍스트를 제외한 기본 배너 로고를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-186">If your language preference is German, you get the default Banner Logo but the German text.</span></span>

<span data-ttu-id="d4ddb-187">기술적으로 Azure AD에서 지원하는 다양한 각 언어 집합을 구성할 수 있지만 유지 관리 및 성능상의 이유로 변형 수를 낮게 유지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-187">While you could technically configure a different set for each language supported by Azure AD, we recommend that you keep the number of variations low, for maintenance and performance reasons.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4ddb-188">Yammer는 사용자가 로그인할 때까지 Azure AD 브랜드 로그인 페이지를 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-188">Yammer does not show the Azure AD branded sign-in page until after the user signs in.</span></span> <span data-ttu-id="d4ddb-189">사용자에게 일반 Office 365 로그인 페이지가 먼저 표시된 후 브랜드 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-189">The user sees the generic Office 365 sign-in page first, and then the branded page after that.</span></span>   
 
 
<span data-ttu-id="d4ddb-190">**디렉터리에 회사 브랜딩을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d4ddb-190">**To add company branding to your directory, perform the following steps:**</span></span>

1. <span data-ttu-id="d4ddb-191">사용자 지정하려는 디렉터리의 관리자로 [Azure 클래식 포털](https://manage.windowsazure.com) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-191">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an administrator of the directory you want to customize.</span></span>
2. <span data-ttu-id="d4ddb-192">사용자 지정하려는 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-192">Select the directory you want to customize.</span></span>
3. <span data-ttu-id="d4ddb-193">위쪽 도구 모음에서 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-193">In the toolbar on the top, click **Configure**.</span></span>
4. <span data-ttu-id="d4ddb-194">**브랜딩 사용자 지정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-194">Click **Customize Branding**.</span></span>
5. <span data-ttu-id="d4ddb-195">사용자 지정할 요소를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-195">Modify the elements you want to customize.</span></span> <span data-ttu-id="d4ddb-196">모든 필드는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-196">All fields are optional.</span></span>
6. <span data-ttu-id="d4ddb-197">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-197">Click **Save**.</span></span>

<span data-ttu-id="d4ddb-198">로그인 페이지 브랜딩의 새로운 변경 내용을 보려면 최대 1시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-198">It can take up to an hour for new change you made to the sign-in page branding to appear.</span></span>

<span data-ttu-id="d4ddb-199">**언어별 회사 브랜딩을 추가하려면 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d4ddb-199">**To add language-specific company branding, perform the following steps:**</span></span>

1. <span data-ttu-id="d4ddb-200">사용자 지정하려는 디렉터리의 관리자로 [Azure 클래식 포털](https://manage.windowsazure.com) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-200">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an administrator of the directory you want to customize.</span></span>
2. <span data-ttu-id="d4ddb-201">사용자 지정하려는 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-201">Select the directory you want to customize.</span></span>
<span data-ttu-id="d4ddb-202">fs3.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-202">fs3.</span></span> <span data-ttu-id="d4ddb-203">위쪽 도구 모음에서 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-203">In the toolbar on the top, click **Configure**.</span></span>
4. <span data-ttu-id="d4ddb-204">**브랜딩 사용자 지정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-204">Click **Customize Branding**.</span></span>
5. <span data-ttu-id="d4ddb-205">**특정 언어에 대한 브랜딩 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-205">Click **Add branding for a specific language**.</span></span>
6. <span data-ttu-id="d4ddb-206">로고를 사용자 지정할 언어를 선택한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-206">Select the language you want to customize the logo for, and then click **Next**.</span></span>
7. <span data-ttu-id="d4ddb-207">언어별 재정의를 구성하려는 요소만 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-207">Edit only the elements for which you want to configure language-specific overrides.</span></span> <span data-ttu-id="d4ddb-208">모든 필드는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-208">All fields are optional.</span></span> <span data-ttu-id="d4ddb-209">필드를 비워 두면 사용자 지정 기본값이 대신 표시되거나, 사용자 지정 기본값이 구성되지 않은 경우에는 Microsoft 기본값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-209">If a field is left blank, then the custom default value is displayed instead (or the Microsoft default if a custom default is not configured).</span></span>
8. <span data-ttu-id="d4ddb-210">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-210">Click **Save**.</span></span>

<span data-ttu-id="d4ddb-211">**디렉터리에서 회사 브랜딩을 제거하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d4ddb-211">**To remove company branding from your directory, perform the following steps:**</span></span>

1. <span data-ttu-id="d4ddb-212">사용자 지정하려는 디렉터리의 관리자로 [Azure 클래식 포털](https://manage.windowsazure.com) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-212">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an administrator of the directory you want to customize.</span></span>
2. <span data-ttu-id="d4ddb-213">사용자 지정하려는 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-213">Select the directory you want to customize.</span></span>
3. <span data-ttu-id="d4ddb-214">위쪽 도구 모음에서 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-214">In the toolbar on the top, click **Configure**.</span></span>
4. <span data-ttu-id="d4ddb-215">**브랜딩 사용자 지정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-215">Click **Customize Branding**.</span></span>
5. <span data-ttu-id="d4ddb-216">브랜딩 사용자 지정 페이지에서 **기존 브랜딩 설정 편집** 을 선택하고 다음 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-216">On the Customize Branding page, select **Edit Existing Branding Settings** and then go to the next page.</span></span>
6. <span data-ttu-id="d4ddb-217">제거하려는 요소에 따라 다음 중 하나 이상을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-217">Depending on which elements you want to remove, do one or more of the following:</span></span>

    <span data-ttu-id="d4ddb-218">a.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-218">a.</span></span> <span data-ttu-id="d4ddb-219">**배너 로고** 아래에서 **업로드된 로고 제거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-219">Under **Banner Logo**, select **Remove uploaded logo**.</span></span>

    <span data-ttu-id="d4ddb-220">b.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-220">b.</span></span> <span data-ttu-id="d4ddb-221">**타일 로고** 아래에서 **업로드된 로고 제거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-221">Under **Tile Logo**, select **Remove uploaded logo**.</span></span>

    <span data-ttu-id="d4ddb-222">c.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-222">c.</span></span> <span data-ttu-id="d4ddb-223">모든 텍스트 상자에서 텍스트를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-223">Remove the text from all textboxes.</span></span>

    <span data-ttu-id="d4ddb-224">d.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-224">d.</span></span> <span data-ttu-id="d4ddb-225">**Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-225">Click **Next**.</span></span>

    <span data-ttu-id="d4ddb-226">e.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-226">e.</span></span> <span data-ttu-id="d4ddb-227">모든 텍스트 상자에서 텍스트를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-227">Remove the text from all textboxes.</span></span>
7. <span data-ttu-id="d4ddb-228">**저장** 을 클릭하여 요소를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-228">Click **Save** to remove the elements.</span></span>
8. <span data-ttu-id="d4ddb-229">필요한 경우 **브랜딩 사용자 지정** 을 다시 클릭하여 제거해야 하는 모든 언어별 브랜딩에 대해 이러한 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-229">If necessary, click **Customize Branding** again and repeat these steps for all language-specific branding that needs to be removed.</span></span>
    <span data-ttu-id="d4ddb-230">**브랜딩 사용자 지정**을 클릭하고 구성된 기존 설정이 없는 **기본 브랜딩 사용자 지정** 양식이 표시되면 모든 브랜딩 설정이 제거된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-230">All branding settings have been removed when you click **Customize Branding** and see the **Customize Default Branding** form with no existing settings configured.</span></span>

## <a name="testing-and-examples"></a><span data-ttu-id="d4ddb-231">테스트 및 예제</span><span class="sxs-lookup"><span data-stu-id="d4ddb-231">Testing and examples</span></span>
<span data-ttu-id="d4ddb-232">프로덕션 환경을 변경하기 전에 테스트 테넌트를 시험하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-232">We recommend that you experiment with a test tenant before making changes in your production environment.</span></span>

<span data-ttu-id="d4ddb-233">**브랜딩이 적용되었는지 확인하려면**</span><span class="sxs-lookup"><span data-stu-id="d4ddb-233">**To verify whether your branding has been applied:**</span></span>

1. <span data-ttu-id="d4ddb-234">InPrivate 또는 Incognito 브라우저 세션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-234">Open an InPrivate or Incognito browser session.</span></span>
2. <span data-ttu-id="d4ddb-235">https://outlook.com/contoso.com로 이동하여 contoso.com을 사용자 지정된 도메인으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-235">Visit https://outlook.com/contoso.com, replacing contoso.com with the domain you’ve customized.</span></span>

<span data-ttu-id="d4ddb-236">또한 contoso.onmicrosoft.com과 같이 표시되는 도메인으로도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-236">This also works with domains that look like contoso.onmicrosoft.com.</span></span>

<span data-ttu-id="d4ddb-237">효과적인 사용자 지정 집합을 만드는 데 도움을 주기 위해 다음과 같은 두 가상 로그인 페이지를 사용자 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-237">To help you create effective customization sets, we have customized the following two fictitious sign-in pages:</span></span>

* [<span data-ttu-id="d4ddb-238">http://aka.ms/aaddemo001</span><span class="sxs-lookup"><span data-stu-id="d4ddb-238">http://aka.ms/aaddemo001</span></span>](http://aka.ms/aaddemo001)
* [<span data-ttu-id="d4ddb-239">http://aka.ms/aaddemo002</span><span class="sxs-lookup"><span data-stu-id="d4ddb-239">http://aka.ms/aaddemo002</span></span>](http://aka.ms/aaddemo002)

<span data-ttu-id="d4ddb-240">언어별 설정을 테스트하려면 웹 브라우저의 기본 언어 설정을 사용자 지정에서 설정한 언어로 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-240">To test the language-specific settings, you need to modify the default language preferences in your web browser to a language you have set in your customization.</span></span> <span data-ttu-id="d4ddb-241">Internet Explorer에서는 **인터넷 옵션** 메뉴에서 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-241">In Internet Explorer, you configure this in the **Internet Options** menu.</span></span>

## <a name="customizable-elements"></a><span data-ttu-id="d4ddb-242">사용자 지정 가능한 요소</span><span class="sxs-lookup"><span data-stu-id="d4ddb-242">Customizable elements</span></span>
<span data-ttu-id="d4ddb-243">Azure AD의 일부 사용자 지정 가능한 요소에는 여러 가지 사용 사례가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-243">Some customizable elements in Azure AD have multiple use cases.</span></span> <span data-ttu-id="d4ddb-244">디렉터리당 한 번 회사 로고를 구성할 수 있고 로그인 및 액세스 패널 페이지 모두에서 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-244">You can configure company logos once per directory and is used on both, the sign-in and Access Panel pages.</span></span> <span data-ttu-id="d4ddb-245">일부 사용자 지정 가능한 요소는 로그인 페이지에만 특정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-245">Some customizable elements are specific only to the sign-in page.</span></span> <span data-ttu-id="d4ddb-246">다음 표에서는 여러 가지 사용자 지정 가능한 요소에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-246">The following table provides details for the different customizable elements.</span></span>

| <span data-ttu-id="d4ddb-247">이름</span><span class="sxs-lookup"><span data-stu-id="d4ddb-247">Name</span></span> | <span data-ttu-id="d4ddb-248">설명</span><span class="sxs-lookup"><span data-stu-id="d4ddb-248">Description</span></span> | <span data-ttu-id="d4ddb-249">제약 조건</span><span class="sxs-lookup"><span data-stu-id="d4ddb-249">Constraints</span></span> | <span data-ttu-id="d4ddb-250">추천</span><span class="sxs-lookup"><span data-stu-id="d4ddb-250">Recommendations</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d4ddb-251">배너 로고</span><span class="sxs-lookup"><span data-stu-id="d4ddb-251">Banner Logo</span></span> |<span data-ttu-id="d4ddb-252">배너 로고는 로그인 페이지와 액세스 패널에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-252">The Banner Logo is displayed on the sign-in page and the Access panel.</span></span> |<p><span data-ttu-id="d4ddb-253">JPG 또는 PNG</span><span class="sxs-lookup"><span data-stu-id="d4ddb-253">JPG or PNG</span></span></p><p><span data-ttu-id="d4ddb-254">60x280픽셀</span><span class="sxs-lookup"><span data-stu-id="d4ddb-254">60x280 pixels</span></span></p><p><span data-ttu-id="d4ddb-255">10KB</span><span class="sxs-lookup"><span data-stu-id="d4ddb-255">10 KB</span></span></p> |<p><span data-ttu-id="d4ddb-256">조직의 전체 로고 사용(픽토그램과 로고 형식 포함)</span><span class="sxs-lookup"><span data-stu-id="d4ddb-256">Use your organization’s full logo (including pictogram and logotype)</span></span></p><p><span data-ttu-id="d4ddb-257">모바일 장치에서 스크롤 막대가 표시되지 않도록 높이를 30픽셀 미만으로 유지하세요.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-257">Keep it under 30 pixels high to avoid introducing scrollbars on mobile devices</span></span></p><p><span data-ttu-id="d4ddb-258">4KB 미만으로 유지하세요.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-258">Keep it under 4 KB</span></span></p><p><span data-ttu-id="d4ddb-259">투명 PNG 사용(로그인 페이지가 항상 흰색 배경은 아님)</span><span class="sxs-lookup"><span data-stu-id="d4ddb-259">Use a transparent PNG (don’t assume that the sign-in page always has a white background)</span></span></p> |
| <span data-ttu-id="d4ddb-260">타일 로고</span><span class="sxs-lookup"><span data-stu-id="d4ddb-260">Tile Logo</span></span> |<span data-ttu-id="d4ddb-261">(현재 로그인 페이지에서 사용되지 않음) 나중에 이 텍스트는 환경의 여러 위치에서 일반 "회사 또는 학교 계정" 픽토그램을 대체하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-261">(currently not used in the sign-in page) In the future, this text may be used to replace the generic “work or school account” pictogram in different places of the experience.</span></span> |<p><span data-ttu-id="d4ddb-262">JPG 또는 PNG</span><span class="sxs-lookup"><span data-stu-id="d4ddb-262">JPG or PNG</span></span></p><p><span data-ttu-id="d4ddb-263">120x120픽셀</span><span class="sxs-lookup"><span data-stu-id="d4ddb-263">120x120 pixels</span></span></p><p><span data-ttu-id="d4ddb-264">10KB</span><span class="sxs-lookup"><span data-stu-id="d4ddb-264">10 KB</span></span></p> |<p><span data-ttu-id="d4ddb-265">이 이미지는 50%로 크기 조정할 수 있으므로 간단하게(작은 텍스트 없음) 유지하세요.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-265">Keep it simple (no small text), as this image may be resized to 50%</span></span> |
| </p> | | | |
| <span data-ttu-id="d4ddb-266">로그인 페이지 사용자 이름 레이블</span><span class="sxs-lookup"><span data-stu-id="d4ddb-266">Sign-in Page User Name Label</span></span> |<span data-ttu-id="d4ddb-267">(현재 로그인 페이지에서 사용되지 않음) 나중에 이 텍스트는 환경의 여러 위치에서 일반 “회사 또는 학교 계정” 문자열을 대체하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-267">(currently not used in the sign-in page) In the future, this text may be used to replace the generic “work or school account” string in different places of the experience.</span></span> <span data-ttu-id="d4ddb-268">"Contoso 계정" 또는 "Contoso ID"와 같은 항목으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-268">You can set it to something like “Contoso account” or “Contoso ID.”</span></span> |<p><span data-ttu-id="d4ddb-269">유니코드 텍스트, 최대 50자</span><span class="sxs-lookup"><span data-stu-id="d4ddb-269">Unicode text, up to 50 characters</span></span></p><p><span data-ttu-id="d4ddb-270">일반 텍스트 전용(링크 또는 HTML 태그 없음)</span><span class="sxs-lookup"><span data-stu-id="d4ddb-270">Plain text only (no links or HTML tags)</span></span></p> |<p><span data-ttu-id="d4ddb-271">짧고 간단하게 만드세요.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-271">Keep it short and simple</span></span></p><p><span data-ttu-id="d4ddb-272">제공된 회사 또는 학교 계정을 일반적으로 참조하는 방법을 사용자에게 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-272">Ask your users how they usually refer to the work or school account you provide them with.</span></span></p> |
| <span data-ttu-id="d4ddb-273">로그인 페이지 텍스트</span><span class="sxs-lookup"><span data-stu-id="d4ddb-273">Sign-in Page Text</span></span> |<span data-ttu-id="d4ddb-274">이 “상용구” 텍스트는 로그인 페이지 양식 아래에 표시되며 추가 지침 또는 도움말 및 지원을 받을 수 있는 위치를 전달하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-274">This “boilerplate” text appears below the sign-in page form and can be used to communicate additional instructions, or where to get help and support.</span></span> |<p><span data-ttu-id="d4ddb-275">유니코드 텍스트, 최대 256자</span><span class="sxs-lookup"><span data-stu-id="d4ddb-275">Unicode text, up to 256 characters</span></span></p><p><span data-ttu-id="d4ddb-276">일반 텍스트 전용(링크 또는 HTML 태그 없음)</span><span class="sxs-lookup"><span data-stu-id="d4ddb-276">Plain text only (no links or HTML tags)</span></span></p> |<span data-ttu-id="d4ddb-277">250자 미만(약 텍스트 3 줄)으로 유지하세요.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-277">Keep it under 250 characters (approximately 3 lines of text)</span></span> |
| <span data-ttu-id="d4ddb-278">로그인 페이지 그림</span><span class="sxs-lookup"><span data-stu-id="d4ddb-278">Sign-in Page Illustration</span></span> |<span data-ttu-id="d4ddb-279">그림은 로그인 페이지에서 로그인 페이지 양식 왼쪽에 표시되는 큰 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-279">The illustration is a large image that is displayed on the sign-in page to the left of the sign-in page form.</span></span> |<p><span data-ttu-id="d4ddb-280">JPG 또는 PNG</span><span class="sxs-lookup"><span data-stu-id="d4ddb-280">JPG or PNG</span></span></p><p><span data-ttu-id="d4ddb-281">1420x1200</span><span class="sxs-lookup"><span data-stu-id="d4ddb-281">1420x1200</span></span></p><p><span data-ttu-id="d4ddb-282">500KB</span><span class="sxs-lookup"><span data-stu-id="d4ddb-282">500 KB</span></span></p> |<p><span data-ttu-id="d4ddb-283">1420x1200픽셀</span><span class="sxs-lookup"><span data-stu-id="d4ddb-283">1420x1200 pixels</span></span></p><p><span data-ttu-id="d4ddb-284">중요: 최대한 작게(200KB 미만이 이상적임) 유지하세요.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-284">Important: Keep it as small as possible, ideally under 200 KB.</span></span> <span data-ttu-id="d4ddb-285">이 이미지가 너무 크면 이미지가 캐시되지 않을 경우 로그인 페이지의 성능에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-285">If this image is too large, the performance of the Sign-in page is impacted when the image isn’t cached</span></span></p><p><span data-ttu-id="d4ddb-286">이 이미지는 다양한 화면 비율에 맞게 잘리는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-286">This image is often cropped, to accommodate different screen ratios.</span></span> <span data-ttu-id="d4ddb-287">크기 조정은 브라우저 창이 축소될 때 아래쪽/오른쪽 모서리에서 위쪽/왼쪽으로 이동하며 발생하므로 기본 시각적 요소를 왼쪽 위 모서리(RTL 언어의 경우 오른쪽 위)에 유지하세요.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-287">Keep the primary visual elements in the top left corner (top right for RTL languages), because resizing occurs from the bottom/right corner, going towards the top / left, as the browser window shrinks.</span></span></p> |
| <span data-ttu-id="d4ddb-288">로그인 페이지 배경색</span><span class="sxs-lookup"><span data-stu-id="d4ddb-288">Sign-in Page Background Color</span></span> |<span data-ttu-id="d4ddb-289">로그인 페이지 배경색은 로그인 페이지 양식의 왼쪽 영역에서 사용되며,</span><span class="sxs-lookup"><span data-stu-id="d4ddb-289">The sign-in page background color is used in the area to the left of the sign-in page form.</span></span> |<span data-ttu-id="d4ddb-290">16진수 형식(예: #FFFFFF)의 RGB 색이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-290">Must be an RGB color in hexadecimal form (example: #FFFFFF)</span></span> |<p><span data-ttu-id="d4ddb-291">낮은 대역폭 연결에서는 배경색이 큰 그림 대신 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-291">The background color may be shown in place of the large Illustration on low-bandwidth connections</span></span></p><p><span data-ttu-id="d4ddb-292">배너 로고의 기본 색을 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d4ddb-292">We suggest picking the primary color of the Banner Logo</span></span></p> |

## <a name="next-steps"></a><span data-ttu-id="d4ddb-293">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d4ddb-293">Next steps</span></span>
* [<span data-ttu-id="d4ddb-294">Azure Active Directory Premium 시작</span><span class="sxs-lookup"><span data-stu-id="d4ddb-294">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="d4ddb-295">액세스 및 사용 보고서 보기</span><span class="sxs-lookup"><span data-stu-id="d4ddb-295">View your access and usage reports</span></span>](active-directory-view-access-usage-reports.md)

<!--Image references-->
[1]: ./media/active-directory-add-company-branding/SignInPage_beforecustomization.png
[2]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization.png
[3]: ./media/active-directory-add-company-branding/SignInPage_mobile_beforecustomization.png
[4]: ./media/active-directory-add-company-branding/SignInPage_mobile_aftercustomization.png
[5]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_elements.png
[6]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_croppedleft.png
[7]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_croppedtop.png
[8]: ./media/active-directory-add-company-branding/APBranding.png
[9]: ./media/active-directory-add-company-branding/hidekmsi.png
