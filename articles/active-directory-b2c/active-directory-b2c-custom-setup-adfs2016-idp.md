---
title: "Azure Active Directory B2C: 사용자 지정 정책을 사용하여 SAML ID 공급자로 ADFS 추가"
description: "SAML 프로토콜 및 사용자 지정 정책을 사용하여 ADFS 2016을 설정하는 방법 문서"
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: ef0495460b5652dd6052a49ab9c722381e93458b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a><span data-ttu-id="662bf-103">Azure Active Directory B2C: 사용자 지정 정책을 사용하여 SAML ID 공급자로 ADFS 추가</span><span class="sxs-lookup"><span data-stu-id="662bf-103">Azure Active Directory B2C: Add ADFS as a SAML identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="662bf-104">이 문서에서는 [사용자 지정 정책](active-directory-b2c-overview-custom.md)을 사용하여 ADFS 계정의 사용자가 로그인할 수 있도록 하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-104">This article shows you how to enable sign-in for users from ADFS account through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="662bf-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="662bf-105">Prerequisites</span></span>

<span data-ttu-id="662bf-106">[사용자 지정 정책 시작](active-directory-b2c-get-started-custom.md) 문서의 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="662bf-107">이러한 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-107">These steps include:</span></span>

1.  <span data-ttu-id="662bf-108">ADFS 신뢰 당사자 트러스트 만들기</span><span class="sxs-lookup"><span data-stu-id="662bf-108">Creating an ADFS Relying Party Trust.</span></span>
2.  <span data-ttu-id="662bf-109">Azure AD B2C에 ADFS 신뢰 당사자 트러스트 인증서 추가</span><span class="sxs-lookup"><span data-stu-id="662bf-109">Adding the ADFS Relying Party Trust certificate to Azure AD B2C.</span></span>
3.  <span data-ttu-id="662bf-110">정책에 클레임 공급자 추가</span><span class="sxs-lookup"><span data-stu-id="662bf-110">Adding claims provider to a policy.</span></span>
4.  <span data-ttu-id="662bf-111">사용자 경험에 ADFS 계정 클레임 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="662bf-111">Registering the ADFS account claims provider to a user journey.</span></span>
5.  <span data-ttu-id="662bf-112">Azure AD B2C 테넌트에 정책 업로드 및 테스트</span><span class="sxs-lookup"><span data-stu-id="662bf-112">Uploading the policy to an Azure AD B2C tenant and test it.</span></span>

## <a name="to-create-a-claims-aware-relying-party-trust"></a><span data-ttu-id="662bf-113">클레임 인식 신뢰 당사자 트러스트를 만들려면</span><span class="sxs-lookup"><span data-stu-id="662bf-113">To create a claims-aware Relying Party Trust</span></span>

<span data-ttu-id="662bf-114">Azure AD(Azure Active Directory) B2C에서 ADFS를 ID 공급자로 사용하려면 먼저 ADFS 신뢰 당사자 트러스트를 만들고 올바른 매개 변수를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-114">To use ADFS as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an ADFS Relying Party Trust and supply it with the right parameters.</span></span>

<span data-ttu-id="662bf-115">AD FS 관리 스냅인을 사용하여 새 신뢰 당사자 트러스트를 추가하고 설정을 수동으로 구성하려면 페더레이션 서버에서 다음 절차를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-115">To add a new relying party trust by using the AD FS Management snap-in and manually configure the settings, perform the following procedure on a federation server.</span></span>

<span data-ttu-id="662bf-116">로컬 컴퓨터에서 **관리자**또는 동등한 멤버 자격은 최소한 이 절차를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-116">Membership in **Administrators**, or equivalent, on the local computer is the minimum required to complete this procedure.</span></span> <span data-ttu-id="662bf-117">[로컬 및 도메인 기본 그룹](http://go.microsoft.com/fwlink/?LinkId=83477)에서 적절한 계정 및 그룹 멤버 자격을 사용하는 방법에 대한 세부 정보를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-117">Review details about using the appropriate accounts and group memberships at [Local and Domain Default Groups](http://go.microsoft.com/fwlink/?LinkId=83477)</span></span>

1.  <span data-ttu-id="662bf-118">서버 관리자에서 **도구**를 클릭하고 **ADFS 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-118">In Server Manager, click **Tools**, and then select **ADFS Management**.</span></span>

2.  <span data-ttu-id="662bf-119">**신뢰 당사자 트러스트 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-119">Click on **Add Relying Party Trust**.</span></span>
    <span data-ttu-id="662bf-120">![신뢰 당사자 트러스트 추가](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span><span class="sxs-lookup"><span data-stu-id="662bf-120">![Add Relying Party Trust](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span></span>

3.  <span data-ttu-id="662bf-121">**시작** 페이지에서 **클레임 인식**을 클릭하고 **시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-121">On the **Welcome** page, choose **Claims aware** and click **Start**.</span></span>
    <span data-ttu-id="662bf-122">![시작 페이지에서 클레임 인식 선택](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span><span class="sxs-lookup"><span data-stu-id="662bf-122">![On the Welcome page, choose Claims aware](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span></span>
4.  <span data-ttu-id="662bf-123">**데이터 원본 선택** 페이지에서 **신뢰 당사자에 대한 데이터를 수동으로 입력**을 클릭하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-123">On the **Select Data Source** page, click **Enter data about the relying party manually**, and then click **Next**.</span></span>
    <span data-ttu-id="662bf-124">![신뢰 당사자에 대한 데이터 입력](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span><span class="sxs-lookup"><span data-stu-id="662bf-124">![Enter data about the relying party](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span></span>

5.  <span data-ttu-id="662bf-125">**표시 이름 지정** 페이지에서 **표시 이름**에 이름을 입력하고 **메모** 아래에서 이 신뢰 당사자 트러스트에 대한 설명을 입력한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-125">On the **Specify Display Name** page, type a name in **Display name**, under **Notes** type a description for this relying party trust, and then click **Next**.</span></span>
    <span data-ttu-id="662bf-126">![표시 이름 및 메모 지정](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span><span class="sxs-lookup"><span data-stu-id="662bf-126">![Specify Display Name and notes](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span></span>
6.  <span data-ttu-id="662bf-127">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-127">Optional.</span></span> <span data-ttu-id="662bf-128">선택적 토큰 암호화 인증서가 있는 경우 **인증서 구성** 페이지에서 **찾아보기**를 클릭하여 인증서 파일을 찾은 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-128">If you have an optional token encryption certificate, then on the **Configure Certificate** page, click **Browse** to locate your certificate file, and then click **Next**.</span></span>
    <span data-ttu-id="662bf-129">![인증서 구성](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span><span class="sxs-lookup"><span data-stu-id="662bf-129">![Configure Certificate](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span></span>
7.  <span data-ttu-id="662bf-130">**URL 구성** 페이지에서 **SAML 2.0 WebSSO 프로토콜에 대한 지원 설정** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-130">On the **Configure URL** page, select the **Enable support for the SAML 2.0 WebSSO protocol** check box.</span></span> <span data-ttu-id="662bf-131">**신뢰 당사자 SAML 2.0 SSO 서비스 URL** 아래에서 이 신뢰 당사자 트러스트에 대한 SAML(Security Assertion Markup Language) 서비스 끝점 URL을 입력한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-131">Under **Relying party SAML 2.0 SSO service URL**, type the Security Assertion Markup Language (SAML) service endpoint URL for this relying party trust, and then click **Next**.</span></span>  <span data-ttu-id="662bf-132">**신뢰 당사자 SAML 2.0 SSO 서비스 URL**에 `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-132">For the **Relying party SAML 2.0 SSO service URL**, paste the `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span></span> <span data-ttu-id="662bf-133">{테넌트}를 테넌트의 이름(예: contosob2c.onmicrosoft.com)으로 바꾸고 {정책}을 확장 정책 이름(예: B2C_1A_TrustFrameworkExtensions)으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-133">Replace {tenant} with your tenant's name (for example, contosob2c.onmicrosoft.com), and replace the {policy} with your extensions policy name (for example, B2C_1A_TrustFrameworkExtensions).</span></span>
    > [!IMPORTANT]
    ><span data-ttu-id="662bf-134">정책 이름은 signup_or_signin 정책에서 상속됩니다. 이 경우에는 `B2C_1A_TrustFrameworkExtensions`입니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-134">The policy name  is the one that signup_or_signin policy inherits from, in this case it is: `B2C_1A_TrustFrameworkExtensions`.</span></span>
    ><span data-ttu-id="662bf-135">예를 들어 URL은 https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-135">For example the URL could be:   https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span></span>

    ![신뢰 당사자 SAML 2.0 SSO 서비스 URL](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. <span data-ttu-id="662bf-137">**식별자 구성** 페이지에서 이전 단계와 동일한 URL을 지정하고 **추가**를 클릭하여 목록에 추가하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-137">On the **Configure Identifiers** page, specify the same URL as the previous step, click **Add** to add them to the list, and then click **Next**.</span></span>
    <span data-ttu-id="662bf-138">![신뢰 당사자 트러스트 식별자](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span><span class="sxs-lookup"><span data-stu-id="662bf-138">![Relying party trust identifiers](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span></span>
9.  <span data-ttu-id="662bf-139">**액세스 제어 정책 선택**에서 정책을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-139">On the **Choose Access Control Policy** select a policy and click **Next**.</span></span>
    <span data-ttu-id="662bf-140">![액세스 제어 정책 선택](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span><span class="sxs-lookup"><span data-stu-id="662bf-140">![Choose Access Control Policy](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span></span>
10.  <span data-ttu-id="662bf-141">**트러스트 추가 준비 완료** 페이지에서 설정을 검토하고 **다음**을 클릭하여 신뢰 당사자 트러스트 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-141">On the **Ready to Add Trust** page, review the settings, and then click **Next** to save your relying party trust information.</span></span>
    <span data-ttu-id="662bf-142">![신뢰 당사자 트러스트 정보 저장](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span><span class="sxs-lookup"><span data-stu-id="662bf-142">![Save your relying party trust information](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span></span>
11.  <span data-ttu-id="662bf-143">**마침** 페이지에서 **닫기**를 클릭하면 이 작업이 **클레임 규칙 편집** 대화 상자를 자동으로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-143">On the **Finish** page, click **Close**, this action automatically displays the **Edit Claim Rules** dialog box.</span></span>
    <span data-ttu-id="662bf-144">![클레임 규칙 편집](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span><span class="sxs-lookup"><span data-stu-id="662bf-144">![Edit Claim Rules](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span></span>
12. <span data-ttu-id="662bf-145">**규칙 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-145">Click **Add Rule**.</span></span>  
      <span data-ttu-id="662bf-146">![새 규칙 추가](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span><span class="sxs-lookup"><span data-stu-id="662bf-146">![Add new rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span></span>
13.  <span data-ttu-id="662bf-147">**클레임 규칙 템플릿**에서 **LDAP 특성을 클레임으로 전송**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-147">In **Claim rule template**, select **Send LDAP attributes as claims**.</span></span>
    <span data-ttu-id="662bf-148">![LDAP 특성을 클레임 템플릿 규칙으로 전송 선택](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span><span class="sxs-lookup"><span data-stu-id="662bf-148">![Select Send LDAP attributes as claims template rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span></span>
14.  <span data-ttu-id="662bf-149">**클레임 규칙 이름**을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-149">Provide **Claim rule name**.</span></span> <span data-ttu-id="662bf-150">**특성 저장소**에서 **Active Directory 선택**을 선택합니다. 다음과 같은 클레임을 추가한 후 **마침** 및 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-150">For the **Attribute store** select **Select Active Directory** Add the following claims, then click **Finish** and **OK**.</span></span>
    <span data-ttu-id="662bf-151">![규칙 속성 설정](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span><span class="sxs-lookup"><span data-stu-id="662bf-151">![Set rule properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span></span>
15.  <span data-ttu-id="662bf-152">서버 관리자에서 **신뢰 당사자 트러스트**를 선택하고 만든 신뢰 당사자 트러스트를 선택하고 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-152">In Server Manager, select **Relying Party Trusts** then select the relying party trust you created and click **Properties**.</span></span>
    <span data-ttu-id="662bf-153">![신뢰 당사자 편집 속성](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span><span class="sxs-lookup"><span data-stu-id="662bf-153">![Relying party edit properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span></span>
16.  <span data-ttu-id="662bf-154">신뢰 당사자 트러스트(B2C 데모) 속성 창에서 **서명** 탭을 클릭하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-154">One the relying party trust (B2C Demo) properties window click **Signature** tab and click **Add**.</span></span>  
    <span data-ttu-id="662bf-155">![서명 설정](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span><span class="sxs-lookup"><span data-stu-id="662bf-155">![Set signature](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span></span>
17.  <span data-ttu-id="662bf-156">서명 인증서를 추가합니다(개인 키 없는 .cert 파일).</span><span class="sxs-lookup"><span data-stu-id="662bf-156">Add your signature certificate (.cert file, without private key).</span></span>  
    ![서명 인증서 추가](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  <span data-ttu-id="662bf-158">신뢰 당사자 트러스트(B2C 데모) 속성 창에서 **고급** 탭을 클릭하고 **보안 해시 알고리즘**을 **SHA-1**로 설정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-158">On the relying party trust (B2C Demo) properties window click **Advanced** tab and change the **Secure hash algorithm** to **SHA-1**, Click **Ok**.</span></span>  
    <span data-ttu-id="662bf-159">![보안 해시 알고리즘을 SHA-1로 설정](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span><span class="sxs-lookup"><span data-stu-id="662bf-159">![Set secure hash algorithm to SHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span></span>

## <a name="add-the-adfs-account-application-key-to-azure-ad-b2c"></a><span data-ttu-id="662bf-160">Azure AD B2C에 ADFS 계정 응용 프로그램 키 추가</span><span class="sxs-lookup"><span data-stu-id="662bf-160">Add the ADFS account application key to Azure AD B2C</span></span>
<span data-ttu-id="662bf-161">ADFS 계정으로 페더레이션하려면 응용 프로그램 대신 Azure AD B2C를 신뢰하기 위해 ADFS 계정에 대한 클라이언트 암호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-161">Federation with ADFS accounts requires a client secret for ADFS account to trust Azure AD B2C on behalf of the application.</span></span> <span data-ttu-id="662bf-162">Azure AD B2C 테넌트에 ADFS 인증서를 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-162">You need to store your ADFS certificate in your Azure AD B2C tenant.</span></span> 

1.  <span data-ttu-id="662bf-163">Azure AD B2C 테넌트로 이동하고 **B2C 설정** > **ID 경험 프레임워크**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-163">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="662bf-164">**정책 키**를 선택하여 테넌트에 사용 가능한 키를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-164">Select **Policy Keys** to view the keys available in your tenant.</span></span>
3.  <span data-ttu-id="662bf-165">**+추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-165">Click **+Add**.</span></span>
4.  <span data-ttu-id="662bf-166">**옵션**에는 **업로드**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-166">For **Options**, use **Upload**.</span></span>
5.  <span data-ttu-id="662bf-167">**이름**에는 `ADFSSamlCert`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-167">For **Name**, use `ADFSSamlCert`.</span></span>  
    <span data-ttu-id="662bf-168">`B2C_1A_` 접두사가 자동으로 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-168">The prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="662bf-169">파일 업로드에서 **개인 키가 있는 인증서 .pfx 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-169">In the File upload,** select your certificate .pfx file with private key.</span></span> <span data-ttu-id="662bf-170">참고: 이 인증서(개인 키 포함)는 ADFS 신뢰 당사자에 발급되고 사용되는 것과 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-170">Note: this certificate (with the private key) should be the same one that issued and used for the ADFS relying party.</span></span>
<span data-ttu-id="662bf-171">![정책 키 업로드](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span><span class="sxs-lookup"><span data-stu-id="662bf-171">![Upload policy key](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span></span>
7.  <span data-ttu-id="662bf-172">**만들기**</span><span class="sxs-lookup"><span data-stu-id="662bf-172">Click **Create**</span></span>
8.  <span data-ttu-id="662bf-173">`B2C_1A_ADFSSamlCert` 키를 만들었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-173">Confirm that you've created the key `B2C_1A_ADFSSamlCert`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="662bf-174">확장 정책에서 클레임 공급자 추가</span><span class="sxs-lookup"><span data-stu-id="662bf-174">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="662bf-175">사용자가 ADFS 계정을 사용하여 로그인하도록 하려면 ADFS 계정을 클레임 공급자로 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-175">If you want users to sign in by using ADFS account, you need to define ADFS account as a claims provider.</span></span> <span data-ttu-id="662bf-176">즉, Azure AD B2C가 통신하는 끝점을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-176">In other words, you need to specify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="662bf-177">끝점은 Azure AD B2C에서 사용하는 일련의 클레임을 제공하여 특정 사용자가 인증했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-177">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span>

<span data-ttu-id="662bf-178">확장 정책 파일에서 `<ClaimsProvider>` 노드를 추가하여 ADFS를 클레임 공급자로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-178">Define ADFS as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1. <span data-ttu-id="662bf-179">작업 디렉터리에서 확장 정책 파일(TrustFrameworkExtensions.xml)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-179">Open the extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="662bf-180">XML 편집기가 필요하면 간단한 플랫폼 간 편집기인 [Visual Studio Code를 사용해 보세요](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="662bf-180">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2. <span data-ttu-id="662bf-181">`<ClaimsProviders>` 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-181">Find the `<ClaimsProviders>` section</span></span>
3. <span data-ttu-id="662bf-182">`ClaimsProviders` 요소 아래에서 다음 XML 코드 조각을 추가하고 `identityProvider`를 DNS(도메인을 나타내는 임의 값)로 바꾸고 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-182">Add the following XML snippet under the `ClaimsProviders` element and replace `identityProvider` with your DNS (Arbitrary value that indicates your domain), and save the file.</span></span> 

```xml
<ClaimsProvider>
    <Domain>contoso.com</Domain>
    <DisplayName>Contoso ADFS</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Contoso-SAML2">
        <DisplayName>Contoso ADFS</DisplayName>
        <Description>Login with your Contoso account</Description>
        <Protocol Name="SAML2"/>
        <Metadata>
        <Item Key="RequestsSigned">false</Item>
        <Item Key="WantsEncryptedAssertions">false</Item>
        <Item Key="PartnerEntity">https://{your_ADFS_domain}/federationmetadata/2007-06/federationmetadata.xml</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userPrincipalName" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="contoso.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication"/>
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-the-adfs-account-claims-provider-to-sign-up-or-sign-in-user-journey"></a><span data-ttu-id="662bf-183">등록 또는 로그인 사용자 경험에 ADFS 계정 클레임 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="662bf-183">Register the ADFS account claims provider to Sign up or Sign in user journey</span></span>
<span data-ttu-id="662bf-184">이 시점에서 ID 공급자가 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-184">At this point, the identity provider has been set up.</span></span>  <span data-ttu-id="662bf-185">그러나 등록/로그인 화면에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-185">However, it is not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="662bf-186">이제 `SignUpOrSignIn` 사용자 경험에 ADFS 계정 ID 공급자를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-186">Now you need to add the ADFS account identity provider to your user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="662bf-187">사용할 수 있도록 하려면 기존 템플릿 사용자 경험의 복제본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-187">To make it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="662bf-188">그런 다음 ADFS ID 공급자를 포함하도록 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-188">Then, we modify it so it includes the ADFS identity provider:</span></span>
    >[!NOTE]
    >If you previously copied the `<UserJourneys>` element from base file of your policy to the extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  <span data-ttu-id="662bf-189">정책의 기본 파일(예: TrustFrameworkBase.xml)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-189">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="662bf-190">`<UserJourneys>` 요소를 찾고 `<UserJourneys>` 노드의 전체 콘텐츠를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-190">Find the `<UserJourneys>` element and copy the entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="662bf-191">확장 파일(예: TrustFrameworkExtensions.xml)을 열고 `<UserJourneys>` 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-191">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="662bf-192">요소가 존재하지 않는 경우 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-192">If the element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="662bf-193">복사한 `<UserJournesy>` 노드의 전체 콘텐츠를 `<UserJourneys>` 요소의 자식으로 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-193">Paste the entire content of `<UserJournesy>` node that you copied as a child of the `<UserJourneys>` element.</span></span>

### <a name="display-the-button"></a><span data-ttu-id="662bf-194">단추 표시</span><span class="sxs-lookup"><span data-stu-id="662bf-194">Display the button</span></span>
<span data-ttu-id="662bf-195">`<ClaimsProviderSelections>` 요소는 클레임 공급자 선택 옵션 목록과 해당 순서를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-195">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span></span>  <span data-ttu-id="662bf-196">`<ClaimsProviderSelection>` 요소는 등록/로그인 페이지에서 ID 공급자 단추를 사용하는 것과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-196">`<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="662bf-197">ADFS 계정에 `<ClaimsProviderSelection>` 요소를 추가하면 사용자가 페이지를 열 때 새 단추가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-197">If you add a `<ClaimsProviderSelection>` element for  ADFS account, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="662bf-198">이 요소를 추가하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-198">To add this element:</span></span>

1.  <span data-ttu-id="662bf-199">복사한 사용자 경험에서 `Id="SignUpOrSignIn"`이 포함된 `<UserJourney>` 노드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-199">Find the `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in the user journey that you copied.</span></span>
2.  <span data-ttu-id="662bf-200">`Order="1"`이 포함된 `<OrchestrationStep>` 노드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-200">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="662bf-201">`<ClaimsProviderSelections>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-201">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-the-button-to-an-action"></a><span data-ttu-id="662bf-202">작업에 단추 연결</span><span class="sxs-lookup"><span data-stu-id="662bf-202">Link the button to an action</span></span>

<span data-ttu-id="662bf-203">이제 단추가 준비되었으므로 동작에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-203">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="662bf-204">이 경우에 작업을 통해 Azure AD B2C에서 ADFS 계정과 통신하여 토큰을 수신할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-204">The action, in this case, is for Azure AD B2C to communicate with ADFS account to receive a token.</span></span> <span data-ttu-id="662bf-205">ADFS 계정 클레임 공급자의 기술 프로필을 연결하여 동작에 단추를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-205">Link the button to an action by linking the technical profile for your ADFS account claims provider:</span></span>

1.  <span data-ttu-id="662bf-206">`<UserJourney>` 노드에 `Order="2"`가 포함된 `<OrchestrationStep>`을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-206">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="662bf-207">`<ClaimsExchanges>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-207">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * <span data-ttu-id="662bf-208">`Id`에 이전 섹션의 `TargetClaimsExchangeId`와 동일한 값이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-208">Ensure the `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section.</span></span>
> * <span data-ttu-id="662bf-209">`TechnicalProfileReferenceId`를 이전에 만든 기술 프로필로(Contoso-SAML2)로 설정하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-209">Ensure `TechnicalProfileReferenceId` is set to the technical profile you created earlier (Contoso-SAML2).</span></span>

## <a name="upload-the-policy-to-your-tenant"></a><span data-ttu-id="662bf-210">테넌트에 정책 업로드</span><span class="sxs-lookup"><span data-stu-id="662bf-210">Upload the policy to your tenant</span></span>
1.  <span data-ttu-id="662bf-211">[Azure Portal](https://portal.azure.com)에서 [Azure AD B2C 테넌트의 컨텍스트](active-directory-b2c-navigate-to-b2c-context.md)로 전환하고 **Azure AD B2C** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-211">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="662bf-212">**ID 경험 프레임워크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-212">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="662bf-213">**모든 정책** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-213">Open the **All Policies** blade.</span></span>
4.  <span data-ttu-id="662bf-214">**정책 업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-214">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="662bf-215">**정책이 있는 경우 덮어쓰기** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-215">Check **Overwrite the policy if it exists** box.</span></span>
6.  <span data-ttu-id="662bf-216">TrustFrameworkExtensions.xml을 **업로드**하고 유효성 검사가 실패하지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-216">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="662bf-217">지금 실행을 사용하여 사용자 지정 정책 테스트</span><span class="sxs-lookup"><span data-stu-id="662bf-217">Test the custom policy by using Run Now</span></span>
1.  <span data-ttu-id="662bf-218">**Azure AD B2C 설정**을 열고 **ID 경험 프레임워크**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-218">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="662bf-219">업로드한 RP(신뢰 당사자) 사용자 지정 정책인 **B2C_1A_signup_signin**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-219">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="662bf-220">**지금 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-220">Select **Run now**.</span></span>
3.  <span data-ttu-id="662bf-221">ADFS 계정을 사용하여 로그인할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-221">You should be able to sign in using ADFS account.</span></span>

## <a name="optional-register-the-adfs-account-claims-provider-to-profile-edit-user-journey"></a><span data-ttu-id="662bf-222">[선택 사항]프로필 편집 사용자 경험에 ADFS 계정 클레임 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="662bf-222">[Optional] Register the ADFS account claims provider to Profile-Edit user journey</span></span>
<span data-ttu-id="662bf-223">`ProfileEdit` 사용자 경험에 ADFS 계정 ID 공급자를 추가하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-223">You may want to add the ADFS account identity provider also to your user `ProfileEdit` user journey.</span></span> <span data-ttu-id="662bf-224">사용할 수 있도록 하려면 마지막 두 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-224">To make it available, we repeat the last two steps:</span></span>

### <a name="display-the-button"></a><span data-ttu-id="662bf-225">단추 표시</span><span class="sxs-lookup"><span data-stu-id="662bf-225">Display the button</span></span>
1.  <span data-ttu-id="662bf-226">정책의 확장 파일(예: TrustFrameworkExtensions.xml)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-226">Open the extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="662bf-227">복사한 사용자 경험에서 `Id="ProfileEdit"`이 포함된 `<UserJourney>` 노드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-227">Find the `<UserJourney>` node that includes `Id="ProfileEdit"` in the user journey that you copied.</span></span>
3.  <span data-ttu-id="662bf-228">`Order="1"`이 포함된 `<OrchestrationStep>` 노드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-228">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="662bf-229">`<ClaimsProviderSelections>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-229">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="662bf-230">작업에 단추 연결</span><span class="sxs-lookup"><span data-stu-id="662bf-230">Link the button to an action</span></span>
1.  <span data-ttu-id="662bf-231">`<UserJourney>` 노드에 `Order="2"`가 포함된 `<OrchestrationStep>`을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-231">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="662bf-232">`<ClaimsExchanges>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-232">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-the-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="662bf-233">지금 실행을 사용하여 사용자 지정 프로필-편집 정책 테스트</span><span class="sxs-lookup"><span data-stu-id="662bf-233">Test the custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="662bf-234">**Azure AD B2C 설정**을 열고 **ID 경험 프레임워크**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-234">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="662bf-235">업로드한 RP(신뢰 당사자) 사용자 지정 정책인 **B2C_1A_ProfileEdit**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-235">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="662bf-236">**지금 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-236">Select **Run now**.</span></span>
3.  <span data-ttu-id="662bf-237">ADFS 계정을 사용하여 로그인할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-237">You should be able to sign in using ADFS account.</span></span>

## <a name="download-the-complete-policy-files"></a><span data-ttu-id="662bf-238">완성 정책 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="662bf-238">Download the complete policy files</span></span>
<span data-ttu-id="662bf-239">선택 사항: 사용자 지정 정책을 사용하여 시작을 완료한 후에 고유한 사용자 지정 정책 사용하여 시나리오를 빌드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="662bf-239">Optional: We recommend you build your scenario using your own Custom policy files after completing the Getting Started with Custom Policies walk through.</span></span> [<span data-ttu-id="662bf-240">참조 전용 정책 샘플 파일</span><span class="sxs-lookup"><span data-stu-id="662bf-240">Policy sample files for reference only</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
