---
title: "Azure Active Directory에 사전 통합된 앱에 대 한 hello SAML 토큰에서 발급 된 aaaCustomizing 클레임 | Microsoft Docs"
description: "Toocustomize hello 클레임 발급 방식 hello에 Azure Active Directory에 사전 통합된 앱에 대 한 SAML 토큰에 알아봅니다"
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
ms.openlocfilehash: a376318929472403e799f02fdd3fbddc91d0a70c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-claims-issued-in-hello-saml-token-for-pre-integrated-apps-in-azure-active-directory"></a><span data-ttu-id="be964-103">Azure Active Directory에 사전 통합된 앱에 대 한 SAML 토큰 hello에 발급 클레임 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="be964-103">Customizing claims issued in hello SAML token for pre-integrated apps in Azure Active Directory</span></span>
<span data-ttu-id="be964-104">Azure Active Directory hello single sign-on 지원 360 보다를 포함 하 여 Azure AD 응용 프로그램 갤러리에서에서 수천 개의 미리 통합 된 응용 프로그램을 지 원하는 오늘 hello SAML 2.0 프로토콜을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="be964-104">Today Azure Active Directory supports thousands of pre-integrated applications in hello Azure AD Application Gallery, including over 360 that support single sign-on using hello SAML 2.0 protocol.</span></span> <span data-ttu-id="be964-105">사용자가 SAML을 사용 하 여 Azure AD 통해 tooan 응용 프로그램에 인증 하는 경우 Azure AD는 토큰 toohello 응용 프로그램을 (HTTP POST)를 통해 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="be964-105">When a user authenticates tooan application through Azure AD using SAML, Azure AD sends a token toohello application (via an HTTP POST).</span></span> <span data-ttu-id="be964-106">및 그런 다음 hello 응용 프로그램의 유효성을 검사 하 고 사용자 이름 및 암호에 대 한 메시지를 표시 하는 대신에 hello 토큰 toolog hello 사용자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="be964-106">And then, hello application validates and uses hello token toolog hello user in instead of prompting for a username and password.</span></span> <span data-ttu-id="be964-107">이 SAML 토큰 "클레임" 이라고 하는 hello 사용자에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="be964-107">These SAML tokens contain pieces of information about hello user known as "claims".</span></span>

<span data-ttu-id="be964-108">id 관점, "클레임"은 해당 사용자에 대해 발급 하는 hello 토큰 내에서 사용자에 대 한 id 공급자를 나타내는 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="be964-108">In identity-speak, a “claim” is information that an identity provider states about a user inside hello token they issue for that user.</span></span> <span data-ttu-id="be964-109">[SAML 토큰](http://en.wikipedia.org/wiki/SAML_2.0),이 데이터는 일반적으로 SAML 특성 설명을 hello에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be964-109">In [SAML token](http://en.wikipedia.org/wiki/SAML_2.0), this data is typically contained in hello SAML Attribute Statement.</span></span> <span data-ttu-id="be964-110">hello 사용자의 고유 ID는 일반적으로 표현 SAML 주체 이름을 식별자로 라고도 하는 hello에.</span><span class="sxs-lookup"><span data-stu-id="be964-110">hello user’s unique ID is typically represented in hello SAML Subject also called as Name Identifier.</span></span>

<span data-ttu-id="be964-111">기본적으로 Azure Active Directory는 NameIdentifier 클레임 값이 Azure AD에서 hello 사용자의 사용자 이름 (즉, 사용자 계정 이름)을 포함 하는 SAML 토큰 tooyour 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="be964-111">By default, Azure Active Directory issues a SAML token tooyour application that contains a NameIdentifier claim, with a value of hello user’s username (AKA user principal name) in Azure AD.</span></span> <span data-ttu-id="be964-112">이 값 hello 사용자를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be964-112">this value can uniquely identify hello user.</span></span> <span data-ttu-id="be964-113">또한 hello SAML 토큰 hello 사용자의 전자 메일 주소, 이름 및 성을 포함 하는 추가 클레임을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="be964-113">hello SAML token also contains additional claims containing hello user’s email address, first name, and last name.</span></span>

<span data-ttu-id="be964-114">tooview 또는 편집 hello 클레임 SAML 토큰 toohello 응용 프로그램을 Azure 포털에서 열기 hello 응용 프로그램 hello에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be964-114">tooview or edit hello claims issued in hello SAML token toohello application, open hello application in Azure portal.</span></span> <span data-ttu-id="be964-115">Hello 선택 **보기 및 다른 모든 사용자 특성을 편집** hello 확인란을 선택 **사용자 특성** hello 응용 프로그램의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="be964-115">Then select hello **View and edit all other user attributes** checkbox in hello **User Attributes** section of hello application.</span></span>

![사용자 특성 섹션][1]

<span data-ttu-id="be964-117">두 가지 가능한 원인은 hello SAML 토큰에서 발급 된 tooedit hello 클레임 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be964-117">There are two possible reasons why you might need tooedit hello claims issued in hello SAML token:</span></span>
* <span data-ttu-id="be964-118">hello 응용 프로그램을 다른 클레임 Uri의 설정 또는 클레임 값 toorequire를 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="be964-118">hello application has been written toorequire a different set of claim URIs or claim values.</span></span>
* <span data-ttu-id="be964-119">hello 응용 프로그램 hello NameIdentifier 클레임 toobe 이외의 hello 사용자 이름 (즉, 사용자 계정 이름) Azure Active Directory에 저장 해야 하는 방식으로 배포 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="be964-119">hello application has been deployed in a way that requires hello NameIdentifier claim toobe something other than hello username (AKA user principal name) stored in Azure Active Directory.</span></span>

<span data-ttu-id="be964-120">Hello 기본 클레임 값을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be964-120">You can edit any of hello default claim values.</span></span> <span data-ttu-id="be964-121">Hello SAML 토큰 특성 테이블의 hello 클레임 행을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="be964-121">Select hello claim row in hello SAML token attributes table.</span></span> <span data-ttu-id="be964-122">Hello 열립니다 **특성 편집** 클레임 이름, 값 및 hello 클레임과 연결 된 네임 스페이스 섹션 및 다음 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be964-122">This opens hello **Edit Attribute** section and then you can edit claim name, value, and namespace associated with hello claim.</span></span>

![사용자 특성 편집][2]

<span data-ttu-id="be964-124">Hello를 클릭 하 여 열 수 있는 hello 상황에 맞는 메뉴를 사용 하 여 (제외 NameIdentifier) 클레임을 제거할 수도 있습니다 **...**  아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="be964-124">You can also remove claims (other than NameIdentifier) using hello context menu, which opens by clicking on hello **...** icon.</span></span>  <span data-ttu-id="be964-125">Hello를 사용 하 여 새 클레임을 추가할 수도 있습니다 **특성 추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="be964-125">You can also add new claims using hello **Add attribute** button.</span></span>

![사용자 특성 편집][3]

## <a name="editing-hello-nameidentifier-claim"></a><span data-ttu-id="be964-127">Hello NameIdentifier 클레임 편집</span><span class="sxs-lookup"><span data-stu-id="be964-127">Editing hello NameIdentifier claim</span></span>
<span data-ttu-id="be964-128">hello toosolve hello 문제 hello 응용 프로그램을 배포한 다른 사용자 이름을 사용 하 여 클릭 **사용자 식별자** hello에서 드롭 다운 **사용자 특성** 섹션.</span><span class="sxs-lookup"><span data-stu-id="be964-128">toosolve hello problem where hello application has been deployed using a different username, click on hello **User Identifier** drop down in hello **User Attributes** section.</span></span> <span data-ttu-id="be964-129">이 작업을 수행하면 몇 가지 옵션이 있는 대화 상자가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="be964-129">This action provides a dialog with several different options:</span></span>

![사용자 특성 편집][4]

<span data-ttu-id="be964-131">Hello 드롭다운 목록에서에서 선택 **user.mail** tooset hello NameIdentifier 클레임 hello 디렉터리에 toobe hello 사용자의 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="be964-131">In hello drop-down, select **user.mail** tooset hello NameIdentifier claim toobe hello user’s email address in hello directory.</span></span> <span data-ttu-id="be964-132">선택 또는 **user.onpremisessamaccountname** tooset toohello 사용자 SAM 계정 이름에서 동기화 된 온-프레미스 Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be964-132">Or, select **user.onpremisessamaccountname** tooset toohello user’s SAM Account Name that has been synced from on-premises Azure AD.</span></span>

<span data-ttu-id="be964-133">특별 한 hello를 사용할 수도 있습니다 **ExtractMailPrefix()** hello 전자 메일 주소, SAM 계정 이름 또는 hello 사용자 계정 이름에서 함수 tooremove hello 도메인 접미사입니다.</span><span class="sxs-lookup"><span data-stu-id="be964-133">You can also use hello special **ExtractMailPrefix()** function tooremove hello domain suffix from either hello email address, SAM Account Name, or hello user principal name.</span></span> <span data-ttu-id="be964-134">통해 전달 되는 hello hello 사용자의 첫 번째 부분 이름을 추출 (예를 들어 "joe_smith" 대신 joe_smith@contoso.com).</span><span class="sxs-lookup"><span data-stu-id="be964-134">This extracts only hello first part of hello user name being passed through (for example, "joe_smith" instead of joe_smith@contoso.com).</span></span>

![사용자 특성 편집][5]

<span data-ttu-id="be964-136">Hello 또한 추가 이제 **join ()** 함수 toojoin hello hello 사용자 식별자 값을 사용 하 여 도메인을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="be964-136">We have now also added hello **join()** function toojoin hello verified domain with hello user identifier value.</span></span> <span data-ttu-id="be964-137">hello에 hello join () 함수를 선택 하면 **사용자 식별자** 첫 번째 select와 같은 전자 메일 주소 또는 사용자 계정 이름으로 사용자의 id를 hello 및 hello 두 번째 드롭다운 목록에서 확인 된 도메인을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="be964-137">when you select hello join() function in hello **User Identifier** First select hello user identifier as like email address or user principal name and then in hello second drop-down select your verified domain.</span></span> <span data-ttu-id="be964-138">Hello 확인 된 도메인과 hello 전자 메일 주소를 선택한 다음 Azure AD에서 첫 번째 값 joe_smith hello에서에서 hello username 추출 joe_smith@contoso.com contoso.onmicrosoft.com에 추가 합니다. 다음 예제는 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="be964-138">If you select hello email address with hello verified domain, then Azure AD extracts hello username from hello first value joe_smith from joe_smith@contoso.com and appends it with contoso.onmicrosoft.com. See hello following example:</span></span>

![사용자 특성 편집][6]

## <a name="adding-claims"></a><span data-ttu-id="be964-140">클레임 추가</span><span class="sxs-lookup"><span data-stu-id="be964-140">Adding claims</span></span>
<span data-ttu-id="be964-141">클레임을 추가할 때는 hello 특성 이름 (toofollow hello SAML 사양에 따라 URI 패턴을 필요 하지 않은 엄격 하 게)를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be964-141">When adding a claim, you can specify hello attribute name (which doesn’t strictly need toofollow a URI pattern as per hello SAML spec).</span></span> <span data-ttu-id="be964-142">Hello 디렉터리에 저장 된 hello 값 tooany 사용자 특성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="be964-142">Set hello value tooany user attribute that is stored in hello directory.</span></span>

![사용자 특성 추가][7]

<span data-ttu-id="be964-144">예를 들어 toosend 해야 사용자 hello hello 부서 속한 tooin 조직 (예: 판매)을 클레임으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="be964-144">For example, you need toosend hello department that hello user belongs tooin their organization as a claim (such as, Sales).</span></span> <span data-ttu-id="be964-145">Hello 응용 프로그램에서 예상 대로 hello 클레임 이름을 입력 한 다음 선택 **user.department** hello 값으로.</span><span class="sxs-lookup"><span data-stu-id="be964-145">Enter hello claim name as expected by hello application, and then select **user.department** as hello value.</span></span>

> [!NOTE]
> <span data-ttu-id="be964-146">지정된 된 사용자에 대 한 선택한 특성에 대해 저장 된 값이 없는, hello 토큰에서 해당 클레임이 발급 되 고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be964-146">If for a given user there is no value stored for a selected attribute, then that claim is not being issued in hello token.</span></span>

> [!TIP]
> <span data-ttu-id="be964-147">hello **user.onpremisesecurityidentifier** 및 **user.onpremisesamaccountname** 때 사용자 데이터를 동기화 온-프레미스 Active Directory hello를 사용 하 여만 지원 됩니다 [Azure AD Connect 도구](../active-directory-aadconnect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="be964-147">hello **user.onpremisesecurityidentifier** and **user.onpremisesamaccountname** are only supported when synchronizing user data from on-premises Active Directory using hello [Azure AD Connect tool](../active-directory-aadconnect.md).</span></span>

## <a name="restricted-claims"></a><span data-ttu-id="be964-148">제한된 클레임</span><span class="sxs-lookup"><span data-stu-id="be964-148">Restricted claims</span></span>

<span data-ttu-id="be964-149">SAML에는 몇 가지 제한된 클레임이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be964-149">There are some restricted claims in SAML.</span></span> <span data-ttu-id="be964-150">이러한 클레임을 추가하면 Azure AD는 이러한 클레임을 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="be964-150">If you add these claims, then Azure AD will not send these claims.</span></span> <span data-ttu-id="be964-151">다음은 hello SAML 클레임 집합을 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="be964-151">Following are hello SAML restricted claim set:</span></span>

    | <span data-ttu-id="be964-152">클레임 형식(URI)</span><span class="sxs-lookup"><span data-stu-id="be964-152">Claim type (URI)</span></span> |
    | ------------------- |
    | <span data-ttu-id="be964-153">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span><span class="sxs-lookup"><span data-stu-id="be964-153">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span></span> |
    | <span data-ttu-id="be964-154">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span><span class="sxs-lookup"><span data-stu-id="be964-154">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span></span> |
    | <span data-ttu-id="be964-155">http://schemas.microsoft.com/identity/claims/accesstoken</span><span class="sxs-lookup"><span data-stu-id="be964-155">http://schemas.microsoft.com/identity/claims/accesstoken</span></span> |
    | <span data-ttu-id="be964-156">http://schemas.microsoft.com/identity/claims/openid2_id</span><span class="sxs-lookup"><span data-stu-id="be964-156">http://schemas.microsoft.com/identity/claims/openid2_id</span></span> |
    | <span data-ttu-id="be964-157">http://schemas.microsoft.com/identity/claims/identityprovider</span><span class="sxs-lookup"><span data-stu-id="be964-157">http://schemas.microsoft.com/identity/claims/identityprovider</span></span> |
    | <span data-ttu-id="be964-158">http://schemas.microsoft.com/identity/claims/objectidentifier</span><span class="sxs-lookup"><span data-stu-id="be964-158">http://schemas.microsoft.com/identity/claims/objectidentifier</span></span> |
    | <span data-ttu-id="be964-159">http://schemas.microsoft.com/identity/claims/puid</span><span class="sxs-lookup"><span data-stu-id="be964-159">http://schemas.microsoft.com/identity/claims/puid</span></span> |
    | <span data-ttu-id="be964-160">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1]</span><span class="sxs-lookup"><span data-stu-id="be964-160">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1]</span></span> |
    | <span data-ttu-id="be964-161">http://schemas.microsoft.com/identity/claims/tenantid</span><span class="sxs-lookup"><span data-stu-id="be964-161">http://schemas.microsoft.com/identity/claims/tenantid</span></span> |
    | <span data-ttu-id="be964-162">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span><span class="sxs-lookup"><span data-stu-id="be964-162">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span></span> |
    | <span data-ttu-id="be964-163">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span><span class="sxs-lookup"><span data-stu-id="be964-163">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span></span> |
    | <span data-ttu-id="be964-164">http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider</span><span class="sxs-lookup"><span data-stu-id="be964-164">http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider</span></span> |
    | <span data-ttu-id="be964-165">http://schemas.microsoft.com/ws/2008/06/identity/claims/groups</span><span class="sxs-lookup"><span data-stu-id="be964-165">http://schemas.microsoft.com/ws/2008/06/identity/claims/groups</span></span> |
    | <span data-ttu-id="be964-166">http://schemas.microsoft.com/claims/groups.link</span><span class="sxs-lookup"><span data-stu-id="be964-166">http://schemas.microsoft.com/claims/groups.link</span></span> |
    | <span data-ttu-id="be964-167">http://schemas.microsoft.com/ws/2008/06/identity/claims/role</span><span class="sxs-lookup"><span data-stu-id="be964-167">http://schemas.microsoft.com/ws/2008/06/identity/claims/role</span></span> |
    | <span data-ttu-id="be964-168">http://schemas.microsoft.com/ws/2008/06/identity/claims/wids</span><span class="sxs-lookup"><span data-stu-id="be964-168">http://schemas.microsoft.com/ws/2008/06/identity/claims/wids</span></span> |
    | <span data-ttu-id="be964-169">http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant</span><span class="sxs-lookup"><span data-stu-id="be964-169">http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant</span></span> |
    | <span data-ttu-id="be964-170">http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown</span><span class="sxs-lookup"><span data-stu-id="be964-170">http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown</span></span> |
    | <span data-ttu-id="be964-171">http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged</span><span class="sxs-lookup"><span data-stu-id="be964-171">http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged</span></span> |
    | <span data-ttu-id="be964-172">http://schemas.microsoft.com/2014/03/psso</span><span class="sxs-lookup"><span data-stu-id="be964-172">http://schemas.microsoft.com/2014/03/psso</span></span> |
    | <span data-ttu-id="be964-173">http://schemas.microsoft.com/claims/authnmethodsreferences</span><span class="sxs-lookup"><span data-stu-id="be964-173">http://schemas.microsoft.com/claims/authnmethodsreferences</span></span> |
    | <span data-ttu-id="be964-174">http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor</span><span class="sxs-lookup"><span data-stu-id="be964-174">http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor</span></span> |
    | <span data-ttu-id="be964-175">http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername</span><span class="sxs-lookup"><span data-stu-id="be964-175">http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername</span></span> |
    | <span data-ttu-id="be964-176">http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey</span><span class="sxs-lookup"><span data-stu-id="be964-176">http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey</span></span> |
    | <span data-ttu-id="be964-177">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname</span><span class="sxs-lookup"><span data-stu-id="be964-177">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname</span></span> |
    | <span data-ttu-id="be964-178">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid</span><span class="sxs-lookup"><span data-stu-id="be964-178">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid</span></span> |
    | <span data-ttu-id="be964-179">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid</span><span class="sxs-lookup"><span data-stu-id="be964-179">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid</span></span> |
    | <span data-ttu-id="be964-180">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision</span><span class="sxs-lookup"><span data-stu-id="be964-180">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision</span></span> |
    | <span data-ttu-id="be964-181">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication</span><span class="sxs-lookup"><span data-stu-id="be964-181">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication</span></span> |
    | <span data-ttu-id="be964-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid</span><span class="sxs-lookup"><span data-stu-id="be964-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid</span></span> |
    | <span data-ttu-id="be964-183">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid</span><span class="sxs-lookup"><span data-stu-id="be964-183">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid</span></span> |
    | <span data-ttu-id="be964-184">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid</span><span class="sxs-lookup"><span data-stu-id="be964-184">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid</span></span> |
    | <span data-ttu-id="be964-185">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid</span><span class="sxs-lookup"><span data-stu-id="be964-185">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid</span></span> |
    | <span data-ttu-id="be964-186">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup</span><span class="sxs-lookup"><span data-stu-id="be964-186">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup</span></span> |
    | <span data-ttu-id="be964-187">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim</span><span class="sxs-lookup"><span data-stu-id="be964-187">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim</span></span> |
    | <span data-ttu-id="be964-188">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup</span><span class="sxs-lookup"><span data-stu-id="be964-188">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup</span></span> |
    | <span data-ttu-id="be964-189">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion</span><span class="sxs-lookup"><span data-stu-id="be964-189">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion</span></span> |
    | <span data-ttu-id="be964-190">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority</span><span class="sxs-lookup"><span data-stu-id="be964-190">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority</span></span> |
    | <span data-ttu-id="be964-191">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim</span><span class="sxs-lookup"><span data-stu-id="be964-191">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim</span></span> |
    | <span data-ttu-id="be964-192">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname</span><span class="sxs-lookup"><span data-stu-id="be964-192">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname</span></span> |
    | <span data-ttu-id="be964-193">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn</span><span class="sxs-lookup"><span data-stu-id="be964-193">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn</span></span> |
    | <span data-ttu-id="be964-194">http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid</span><span class="sxs-lookup"><span data-stu-id="be964-194">http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid</span></span> |
    | <span data-ttu-id="be964-195">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn</span><span class="sxs-lookup"><span data-stu-id="be964-195">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn</span></span> |
    | <span data-ttu-id="be964-196">http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent</span><span class="sxs-lookup"><span data-stu-id="be964-196">http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent</span></span> |
    | <span data-ttu-id="be964-197">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier</span><span class="sxs-lookup"><span data-stu-id="be964-197">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier</span></span> |
    | <span data-ttu-id="be964-198">http://schemas.microsoft.com/identity/claims/scope</span><span class="sxs-lookup"><span data-stu-id="be964-198">http://schemas.microsoft.com/identity/claims/scope</span></span> |

## <a name="next-steps"></a><span data-ttu-id="be964-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="be964-199">Next steps</span></span>
* [<span data-ttu-id="be964-200">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="be964-200">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="be964-201">Single sign on tooapplications hello Azure Active Directory 응용 프로그램 갤러리에 없는 구성</span><span class="sxs-lookup"><span data-stu-id="be964-201">Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="be964-202">SAML 기반 Single Sign-On 문제 해결</span><span class="sxs-lookup"><span data-stu-id="be964-202">Troubleshooting SAML-Based Single Sign-On</span></span>](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saml-claims-customization/user-attribute-section.png
[2]: ./media/active-directory-saml-claims-customization/edit-claim-name-value.png
[3]: ./media/active-directory-saml-claims-customization/delete-claim.png
[4]: ./media/active-directory-saml-claims-customization/user-identifier.png
[5]: ./media/active-directory-saml-claims-customization/extractemailprefix-function.png
[6]: ./media/active-directory-saml-claims-customization/join-function.png
[7]: ./media/active-directory-saml-claims-customization/add-attribute.png