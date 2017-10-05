---
title: "Azure Active Directory의 사전 통합된 앱에 대한 SAML 토큰에서 발급된 클레임 사용자 지정 | Microsoft Docs"
description: "Azure Active Directory의 사전 통합된 앱에 대한 SAML 토큰에서 발급된 클레임을 사용자 지정하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f1daad62-ac8a-44cd-ac76-e97455e47803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.custom: aaddev
ms.openlocfilehash: 6d232759630fcc567788a8326b566b659f89d17a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="customizing-claims-issued-in-the-saml-token-for-pre-integrated-apps-in-azure-active-directory"></a><span data-ttu-id="b66ec-103">Azure Active Directory의 사전 통합된 앱에 대한 SAML 토큰에서 발급된 클레임 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="b66ec-103">Customizing claims issued in the SAML token for pre-integrated apps in Azure Active Directory</span></span>
<span data-ttu-id="b66ec-104">현재 Azure Active Directory에서는 SAML 2.0 프로토콜을 사용하여 Single Sign-On을 지원하는 360개 이상의 응용 프로그램을 포함하여 Azure AD 응용 프로그램 갤러리에서 사전 통합된 수천 개의 응용 프로그램을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-104">Today Azure Active Directory supports thousands of pre-integrated applications in the Azure AD Application Gallery, including over 360 that support single sign-on using the SAML 2.0 protocol.</span></span> <span data-ttu-id="b66ec-105">사용자가 SAML을 사용하여 Azure AD를 통해 응용 프로그램을 인증하면 Azure AD는 응용 프로그램에 토큰을 보냅니다(HTTP POST를 통해).</span><span class="sxs-lookup"><span data-stu-id="b66ec-105">When a user authenticates to an application through Azure AD using SAML, Azure AD sends a token to the application (via an HTTP POST).</span></span> <span data-ttu-id="b66ec-106">그런 다음 응용 프로그램이 토큰의 유효성을 검사하고 사용하여 사용자 이름과 암호를 묻는 대신 사용자를 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-106">And then, the application validates and uses the token to log the user in instead of prompting for a username and password.</span></span> <span data-ttu-id="b66ec-107">이러한 SAML 토큰에는 "클레임"이라고 알려진 사용자에 대한 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-107">These SAML tokens contain pieces of information about the user known as "claims".</span></span>

<span data-ttu-id="b66ec-108">ID에서 "클레임"은 해당 사용자에 대해 발급하는 토큰 내에서 ID 공급자가 사용자에 대해 나타내는 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-108">In identity-speak, a “claim” is information that an identity provider states about a user inside the token they issue for that user.</span></span> <span data-ttu-id="b66ec-109">[SAML 토큰 ](http://en.wikipedia.org/wiki/SAML_2.0)에서 이러한 데이터는 일반적으로 SAML 특성 문에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-109">In [SAML token](http://en.wikipedia.org/wiki/SAML_2.0), this data is typically contained in the SAML Attribute Statement.</span></span> <span data-ttu-id="b66ec-110">사용자 고유의 ID는 대개 이름 식별자라고도 하는 SAML Subject에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-110">The user’s unique ID is typically represented in the SAML Subject also called as Name Identifier.</span></span>

<span data-ttu-id="b66ec-111">기본적으로 Azure Active Directory는 Azure AD에 사용자의 사용자 이름(또는 사용자 계정 이름) 값과 함께 NameIdentifier 클레임이 포함된 SAML 토큰을 응용 프로그램에 발급합니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-111">By default, Azure Active Directory issues a SAML token to your application that contains a NameIdentifier claim, with a value of the user’s username (AKA user principal name) in Azure AD.</span></span> <span data-ttu-id="b66ec-112">이 값이 사용자를 고유하게 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-112">this value can uniquely identify the user.</span></span> <span data-ttu-id="b66ec-113">또한 SAML 토큰에는 사용자의 메일 주소, 이름 및 성을 포함하는 추가 클레임이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-113">The SAML token also contains additional claims containing the user’s email address, first name, and last name.</span></span>

<span data-ttu-id="b66ec-114">SAML 토큰이 응용 프로그램에 발급한 클레임을 보거나 편집하려면 Azure Portal에서 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-114">To view or edit the claims issued in the SAML token to the application, open the application in Azure portal.</span></span> <span data-ttu-id="b66ec-115">그런 다음 응용 프로그램의 **사용자 특성** 섹션에서 **기타 모든 사용자 특성 보기 및 편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-115">Then select the **View and edit all other user attributes** checkbox in the **User Attributes** section of the application.</span></span>

![사용자 특성 섹션][1]

<span data-ttu-id="b66ec-117">SAML 토큰에 발급된 클레임을 편집해야 할만한 두 가지 이유는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-117">There are two possible reasons why you might need to edit the claims issued in the SAML token:</span></span>
* <span data-ttu-id="b66ec-118">응용 프로그램이 다른 클레임 URI 또는 클레임 값 집합을 요구하도록 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-118">The application has been written to require a different set of claim URIs or claim values.</span></span>
* <span data-ttu-id="b66ec-119">Azure Active Directory에 저장된 사용자 이름(또는 사용자 계정 이름) 이외의 NameIdentifier 클레임을 요구하는 방식으로 응용 프로그램이 배포되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-119">The application has been deployed in a way that requires the NameIdentifier claim to be something other than the username (AKA user principal name) stored in Azure Active Directory.</span></span>

<span data-ttu-id="b66ec-120">원하는 기본 클레임 값을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-120">You can edit any of the default claim values.</span></span> <span data-ttu-id="b66ec-121">SAML 토큰 특성 테이블에서 클레임 행을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-121">Select the claim row in the SAML token attributes table.</span></span> <span data-ttu-id="b66ec-122">그러면 **특성 편집** 섹션이 열리고 클레임 이름, 값 및 클레임과 연결된 네임스페이스를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-122">This opens the **Edit Attribute** section and then you can edit claim name, value, and namespace associated with the claim.</span></span>

![사용자 특성 편집][2]

<span data-ttu-id="b66ec-124">**...** 아이콘을 클릭하면 열리는 상황에 맞는 메뉴를 사용하여 클레임(NameIdentifier 제외)을 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-124">You can also remove claims (other than NameIdentifier) using the context menu, which opens by clicking on the **...** icon.</span></span>  <span data-ttu-id="b66ec-125">**특성 추가** 단추를 사용하여 새 클레임을 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-125">You can also add new claims using the **Add attribute** button.</span></span>

![사용자 특성 편집][3]

## <a name="editing-the-nameidentifier-claim"></a><span data-ttu-id="b66ec-127">NameIdentifier 클레임 편집</span><span class="sxs-lookup"><span data-stu-id="b66ec-127">Editing the NameIdentifier claim</span></span>
<span data-ttu-id="b66ec-128">응용 프로그램이 다른 사용자 이름을 사용하여 배포된 경우 문제를 해결하려면 **사용자 특성** 섹션에서 **사용자 ID** 드롭다운을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-128">To solve the problem where the application has been deployed using a different username, click on the **User Identifier** drop down in the **User Attributes** section.</span></span> <span data-ttu-id="b66ec-129">이 작업을 수행하면 몇 가지 옵션이 있는 대화 상자가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-129">This action provides a dialog with several different options:</span></span>

![사용자 특성 편집][4]

<span data-ttu-id="b66ec-131">드롭다운에서 **user.mail**을 선택하여 NameIdentifier 클레임을 디렉터리에서 사용자의 이메일 주소가 되도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-131">In the drop-down, select **user.mail** to set the NameIdentifier claim to be the user’s email address in the directory.</span></span> <span data-ttu-id="b66ec-132">또는 **user.onpremisessamaccountname**을 선택하여 온-프레미스 Azure AD에서 동기화된 사용자의 SAM 계정 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-132">Or, select **user.onpremisessamaccountname** to set to the user’s SAM Account Name that has been synced from on-premises Azure AD.</span></span>

<span data-ttu-id="b66ec-133">특수한 **ExtractMailPrefix()** 함수를 사용하여 이메일 주소, SAM 계정 이름 또는 사용자 계정 이름에서 도메인 접미사를 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-133">You can also use the special **ExtractMailPrefix()** function to remove the domain suffix from either the email address, SAM Account Name, or the user principal name.</span></span> <span data-ttu-id="b66ec-134">그러면 전달되는 사용자 이름의 첫 부분만 추출됩니다(예: joe_smith@contoso.com 대신 "joe_smith").</span><span class="sxs-lookup"><span data-stu-id="b66ec-134">This extracts only the first part of the user name being passed through (for example, "joe_smith" instead of joe_smith@contoso.com).</span></span>

![사용자 특성 편집][5]

<span data-ttu-id="b66ec-136">이제 확인된 도메인에 사용자 ID 값을 결합하는 **join()** 함수가 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-136">We have now also added the **join()** function to join the verified domain with the user identifier value.</span></span> <span data-ttu-id="b66ec-137">**사용자 ID**에서 join() 함수를 선택하면 첫 번째로 이메일 주소 또는 사용자 계정 이름과 같은 사용자 ID를 선택한 다음 두 번째 드롭다운에서 확인된 도메인을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-137">when you select the join() function in the **User Identifier** First select the user identifier as like email address or user principal name and then in the second drop-down select your verified domain.</span></span> <span data-ttu-id="b66ec-138">확인된 도메인과 이메일 주소를 선택하면 Azure AD가 joe_smith@contoso.com에서 첫 번째 값 joe_smith를 추출해서 contoso.onmicrosoft.com에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-138">If you select the email address with the verified domain, then Azure AD extracts the username from the first value joe_smith from joe_smith@contoso.com and appends it with contoso.onmicrosoft.com.</span></span> <span data-ttu-id="b66ec-139">다음 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b66ec-139">See the following example:</span></span>

![사용자 특성 편집][6]

## <a name="adding-claims"></a><span data-ttu-id="b66ec-141">클레임 추가</span><span class="sxs-lookup"><span data-stu-id="b66ec-141">Adding claims</span></span>
<span data-ttu-id="b66ec-142">클레임을 추가할 때 특성 이름(SAML 사양에 따라 URI 패턴을 엄격히 따를 필요는 없음)을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-142">When adding a claim, you can specify the attribute name (which doesn’t strictly need to follow a URI pattern as per the SAML spec).</span></span> <span data-ttu-id="b66ec-143">디렉터리에 저장된 사용자 특성 중 원하는 것으로 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-143">Set the value to any user attribute that is stored in the directory.</span></span>

![사용자 특성 추가][7]

<span data-ttu-id="b66ec-145">예를 들어 조직에서 사용자가 속한 부서를 클레임(에: 영업)으로 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-145">For example, you need to send the department that the user belongs to in their organization as a claim (such as, Sales).</span></span> <span data-ttu-id="b66ec-146">응용 프로그램에 필요한 클레임 값을 입력한 다음 **user.department**를 값으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-146">Enter the claim name as expected by the application, and then select **user.department** as the value.</span></span>

> [!NOTE]
> <span data-ttu-id="b66ec-147">지정된 사용자에 대해 선택한 특성에 대한 값이 저장되어 있지 않으면 해당 클레임이 토큰에서 발급되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-147">If for a given user there is no value stored for a selected attribute, then that claim is not being issued in the token.</span></span>

> [!TIP]
> <span data-ttu-id="b66ec-148">**user.onpremisesecurityidentifier** 및 **user.onpremisesamaccountname**은 [Azure AD Connect 도구](../active-directory-aadconnect.md)를 사용하여 온-프레미스 Active Directory에서 사용자 데이터를 동기화할 때만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-148">The **user.onpremisesecurityidentifier** and **user.onpremisesamaccountname** are only supported when synchronizing user data from on-premises Active Directory using the [Azure AD Connect tool](../active-directory-aadconnect.md).</span></span>

## <a name="restricted-claims"></a><span data-ttu-id="b66ec-149">제한된 클레임</span><span class="sxs-lookup"><span data-stu-id="b66ec-149">Restricted claims</span></span>

<span data-ttu-id="b66ec-150">SAML에는 몇 가지 제한된 클레임이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-150">There are some restricted claims in SAML.</span></span> <span data-ttu-id="b66ec-151">이러한 클레임을 추가하면 Azure AD는 이러한 클레임을 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-151">If you add these claims, then Azure AD will not send these claims.</span></span> <span data-ttu-id="b66ec-152">다음은 SAML 제한된 클레임 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="b66ec-152">Following are the SAML restricted claim set:</span></span>

    | <span data-ttu-id="b66ec-153">클레임 형식(URI)</span><span class="sxs-lookup"><span data-stu-id="b66ec-153">Claim type (URI)</span></span> |
    | ------------------- |
    | <span data-ttu-id="b66ec-154">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span><span class="sxs-lookup"><span data-stu-id="b66ec-154">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span></span> |
    | <span data-ttu-id="b66ec-155">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span><span class="sxs-lookup"><span data-stu-id="b66ec-155">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span></span> |
    | <span data-ttu-id="b66ec-156">http://schemas.microsoft.com/identity/claims/accesstoken</span><span class="sxs-lookup"><span data-stu-id="b66ec-156">http://schemas.microsoft.com/identity/claims/accesstoken</span></span> |
    | <span data-ttu-id="b66ec-157">http://schemas.microsoft.com/identity/claims/openid2_id</span><span class="sxs-lookup"><span data-stu-id="b66ec-157">http://schemas.microsoft.com/identity/claims/openid2_id</span></span> |
    | <span data-ttu-id="b66ec-158">http://schemas.microsoft.com/identity/claims/identityprovider</span><span class="sxs-lookup"><span data-stu-id="b66ec-158">http://schemas.microsoft.com/identity/claims/identityprovider</span></span> |
    | <span data-ttu-id="b66ec-159">http://schemas.microsoft.com/identity/claims/objectidentifier</span><span class="sxs-lookup"><span data-stu-id="b66ec-159">http://schemas.microsoft.com/identity/claims/objectidentifier</span></span> |
    | <span data-ttu-id="b66ec-160">http://schemas.microsoft.com/identity/claims/puid</span><span class="sxs-lookup"><span data-stu-id="b66ec-160">http://schemas.microsoft.com/identity/claims/puid</span></span> |
    | <span data-ttu-id="b66ec-161">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1]</span><span class="sxs-lookup"><span data-stu-id="b66ec-161">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1]</span></span> |
    | <span data-ttu-id="b66ec-162">http://schemas.microsoft.com/identity/claims/tenantid</span><span class="sxs-lookup"><span data-stu-id="b66ec-162">http://schemas.microsoft.com/identity/claims/tenantid</span></span> |
    | <span data-ttu-id="b66ec-163">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span><span class="sxs-lookup"><span data-stu-id="b66ec-163">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span></span> |
    | <span data-ttu-id="b66ec-164">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span><span class="sxs-lookup"><span data-stu-id="b66ec-164">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span></span> |
    | <span data-ttu-id="b66ec-165">http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider</span><span class="sxs-lookup"><span data-stu-id="b66ec-165">http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider</span></span> |
    | <span data-ttu-id="b66ec-166">http://schemas.microsoft.com/ws/2008/06/identity/claims/groups</span><span class="sxs-lookup"><span data-stu-id="b66ec-166">http://schemas.microsoft.com/ws/2008/06/identity/claims/groups</span></span> |
    | <span data-ttu-id="b66ec-167">http://schemas.microsoft.com/claims/groups.link</span><span class="sxs-lookup"><span data-stu-id="b66ec-167">http://schemas.microsoft.com/claims/groups.link</span></span> |
    | <span data-ttu-id="b66ec-168">http://schemas.microsoft.com/ws/2008/06/identity/claims/role</span><span class="sxs-lookup"><span data-stu-id="b66ec-168">http://schemas.microsoft.com/ws/2008/06/identity/claims/role</span></span> |
    | <span data-ttu-id="b66ec-169">http://schemas.microsoft.com/ws/2008/06/identity/claims/wids</span><span class="sxs-lookup"><span data-stu-id="b66ec-169">http://schemas.microsoft.com/ws/2008/06/identity/claims/wids</span></span> |
    | <span data-ttu-id="b66ec-170">http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant</span><span class="sxs-lookup"><span data-stu-id="b66ec-170">http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant</span></span> |
    | <span data-ttu-id="b66ec-171">http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown</span><span class="sxs-lookup"><span data-stu-id="b66ec-171">http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown</span></span> |
    | <span data-ttu-id="b66ec-172">http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged</span><span class="sxs-lookup"><span data-stu-id="b66ec-172">http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged</span></span> |
    | <span data-ttu-id="b66ec-173">http://schemas.microsoft.com/2014/03/psso</span><span class="sxs-lookup"><span data-stu-id="b66ec-173">http://schemas.microsoft.com/2014/03/psso</span></span> |
    | <span data-ttu-id="b66ec-174">http://schemas.microsoft.com/claims/authnmethodsreferences</span><span class="sxs-lookup"><span data-stu-id="b66ec-174">http://schemas.microsoft.com/claims/authnmethodsreferences</span></span> |
    | <span data-ttu-id="b66ec-175">http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor</span><span class="sxs-lookup"><span data-stu-id="b66ec-175">http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor</span></span> |
    | <span data-ttu-id="b66ec-176">http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername</span><span class="sxs-lookup"><span data-stu-id="b66ec-176">http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername</span></span> |
    | <span data-ttu-id="b66ec-177">http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey</span><span class="sxs-lookup"><span data-stu-id="b66ec-177">http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey</span></span> |
    | <span data-ttu-id="b66ec-178">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname</span><span class="sxs-lookup"><span data-stu-id="b66ec-178">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname</span></span> |
    | <span data-ttu-id="b66ec-179">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid</span><span class="sxs-lookup"><span data-stu-id="b66ec-179">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid</span></span> |
    | <span data-ttu-id="b66ec-180">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid</span><span class="sxs-lookup"><span data-stu-id="b66ec-180">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid</span></span> |
    | <span data-ttu-id="b66ec-181">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision</span><span class="sxs-lookup"><span data-stu-id="b66ec-181">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision</span></span> |
    | <span data-ttu-id="b66ec-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication</span><span class="sxs-lookup"><span data-stu-id="b66ec-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication</span></span> |
    | <span data-ttu-id="b66ec-183">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid</span><span class="sxs-lookup"><span data-stu-id="b66ec-183">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid</span></span> |
    | <span data-ttu-id="b66ec-184">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid</span><span class="sxs-lookup"><span data-stu-id="b66ec-184">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid</span></span> |
    | <span data-ttu-id="b66ec-185">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid</span><span class="sxs-lookup"><span data-stu-id="b66ec-185">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid</span></span> |
    | <span data-ttu-id="b66ec-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid</span><span class="sxs-lookup"><span data-stu-id="b66ec-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid</span></span> |
    | <span data-ttu-id="b66ec-187">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup</span><span class="sxs-lookup"><span data-stu-id="b66ec-187">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup</span></span> |
    | <span data-ttu-id="b66ec-188">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim</span><span class="sxs-lookup"><span data-stu-id="b66ec-188">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim</span></span> |
    | <span data-ttu-id="b66ec-189">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup</span><span class="sxs-lookup"><span data-stu-id="b66ec-189">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup</span></span> |
    | <span data-ttu-id="b66ec-190">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion</span><span class="sxs-lookup"><span data-stu-id="b66ec-190">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion</span></span> |
    | <span data-ttu-id="b66ec-191">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority</span><span class="sxs-lookup"><span data-stu-id="b66ec-191">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority</span></span> |
    | <span data-ttu-id="b66ec-192">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim</span><span class="sxs-lookup"><span data-stu-id="b66ec-192">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim</span></span> |
    | <span data-ttu-id="b66ec-193">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname</span><span class="sxs-lookup"><span data-stu-id="b66ec-193">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname</span></span> |
    | <span data-ttu-id="b66ec-194">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn</span><span class="sxs-lookup"><span data-stu-id="b66ec-194">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn</span></span> |
    | <span data-ttu-id="b66ec-195">http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid</span><span class="sxs-lookup"><span data-stu-id="b66ec-195">http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid</span></span> |
    | <span data-ttu-id="b66ec-196">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn</span><span class="sxs-lookup"><span data-stu-id="b66ec-196">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn</span></span> |
    | <span data-ttu-id="b66ec-197">http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent</span><span class="sxs-lookup"><span data-stu-id="b66ec-197">http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent</span></span> |
    | <span data-ttu-id="b66ec-198">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier</span><span class="sxs-lookup"><span data-stu-id="b66ec-198">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier</span></span> |
    | <span data-ttu-id="b66ec-199">http://schemas.microsoft.com/identity/claims/scope</span><span class="sxs-lookup"><span data-stu-id="b66ec-199">http://schemas.microsoft.com/identity/claims/scope</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b66ec-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b66ec-200">Next steps</span></span>
* [<span data-ttu-id="b66ec-201">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="b66ec-201">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="b66ec-202">Azure Active Directory 응용 프로그램 갤러리에 있지 않은 응용 프로그램에 Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="b66ec-202">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="b66ec-203">SAML 기반 Single Sign-On 문제 해결</span><span class="sxs-lookup"><span data-stu-id="b66ec-203">Troubleshooting SAML-Based Single Sign-On</span></span>](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saml-claims-customization/user-attribute-section.png
[2]: ./media/active-directory-saml-claims-customization/edit-claim-name-value.png
[3]: ./media/active-directory-saml-claims-customization/delete-claim.png
[4]: ./media/active-directory-saml-claims-customization/user-identifier.png
[5]: ./media/active-directory-saml-claims-customization/extractemailprefix-function.png
[6]: ./media/active-directory-saml-claims-customization/join-function.png
[7]: ./media/active-directory-saml-claims-customization/add-attribute.png