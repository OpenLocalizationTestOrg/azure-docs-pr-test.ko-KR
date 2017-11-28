---
title: "Azure Active Directory B2C: 사용자 지정 정책을 사용하여 SAML ID 공급자로 ADFS 추가"
description: "SAML 프로토콜 및 사용자 지정 정책을 사용 하 여 ADFS 2016 설정에 대 한 방법 tooarticle"
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
ms.openlocfilehash: 30fb7700e7834e3d91fab1fc1b169b761584b204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a><span data-ttu-id="174eb-103">Azure Active Directory B2C: 사용자 지정 정책을 사용하여 SAML ID 공급자로 ADFS 추가</span><span class="sxs-lookup"><span data-stu-id="174eb-103">Azure Active Directory B2C: Add ADFS as a SAML identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="174eb-104">이 문서에서는 어떻게 tooenable 로그인 hello 사용 하 여 ADFS 계정에서 사용자에 대 한 [사용자 지정 정책을](active-directory-b2c-overview-custom.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-104">This article shows you how tooenable sign-in for users from ADFS account through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="174eb-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="174eb-105">Prerequisites</span></span>

<span data-ttu-id="174eb-106">Hello에서 단계를 완료 하는 hello [사용자 지정 정책을 사용 하 여 시작](active-directory-b2c-get-started-custom.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="174eb-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="174eb-107">이러한 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-107">These steps include:</span></span>

1.  <span data-ttu-id="174eb-108">ADFS 신뢰 당사자 트러스트 만들기</span><span class="sxs-lookup"><span data-stu-id="174eb-108">Creating an ADFS Relying Party Trust.</span></span>
2.  <span data-ttu-id="174eb-109">Hello ad FS 신뢰 당사자 트러스트 인증서 tooAzure AD B2C를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-109">Adding hello ADFS Relying Party Trust certificate tooAzure AD B2C.</span></span>
3.  <span data-ttu-id="174eb-110">클레임 공급자 tooa 정책을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-110">Adding claims provider tooa policy.</span></span>
4.  <span data-ttu-id="174eb-111">등록 hello ADFS 계정 공급자 tooa 사용자 여행을 클레임입니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-111">Registering hello ADFS account claims provider tooa user journey.</span></span>
5.  <span data-ttu-id="174eb-112">업로드 hello 정책 tooan Azure AD B2C 테 넌 트을 테스트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-112">Uploading hello policy tooan Azure AD B2C tenant and test it.</span></span>

## <a name="toocreate-a-claims-aware-relying-party-trust"></a><span data-ttu-id="174eb-113">toocreate 클레임 인식 신뢰 당사자 트러스트</span><span class="sxs-lookup"><span data-stu-id="174eb-113">toocreate a claims-aware Relying Party Trust</span></span>

<span data-ttu-id="174eb-114">ADFS toouse (Azure AD) Azure Active Directory B2C에는 id 공급자는 ad FS 신뢰 당사자 트러스트 toocreate 필요 하 고이 hello 오른쪽 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-114">toouse ADFS as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate an ADFS Relying Party Trust and supply it with hello right parameters.</span></span>

<span data-ttu-id="174eb-115">tooadd hello AD FS 관리 스냅인을 사용 하 여 신뢰 하 고 hello 설정을 수동으로 구성 하는 새 신뢰 당사자 페더레이션 서버에서 절차를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-115">tooadd a new relying party trust by using hello AD FS Management snap-in and manually configure hello settings, perform hello following procedure on a federation server.</span></span>

<span data-ttu-id="174eb-116">멤버 자격이 **관리자**, 또는 이와 동등한 hello 로컬 컴퓨터에 최소 필수 toocomplete hello이이 절차입니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-116">Membership in **Administrators**, or equivalent, on hello local computer is hello minimum required toocomplete this procedure.</span></span> <span data-ttu-id="174eb-117">Hello 적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](http://go.microsoft.com/fwlink/?LinkId=83477)</span><span class="sxs-lookup"><span data-stu-id="174eb-117">Review details about using hello appropriate accounts and group memberships at [Local and Domain Default Groups](http://go.microsoft.com/fwlink/?LinkId=83477)</span></span>

1.  <span data-ttu-id="174eb-118">서버 관리자에서 **도구**를 클릭하고 **ADFS 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-118">In Server Manager, click **Tools**, and then select **ADFS Management**.</span></span>

2.  <span data-ttu-id="174eb-119">**신뢰 당사자 트러스트 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-119">Click on **Add Relying Party Trust**.</span></span>
    <span data-ttu-id="174eb-120">![신뢰 당사자 트러스트 추가](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span><span class="sxs-lookup"><span data-stu-id="174eb-120">![Add Relying Party Trust](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span></span>

3.  <span data-ttu-id="174eb-121">Hello에 **시작** 페이지에서 선택 **클레임 인식** 클릭 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-121">On hello **Welcome** page, choose **Claims aware** and click **Start**.</span></span>
    <span data-ttu-id="174eb-122">![Hello 시작 페이지에서 클레임 인식 선택](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span><span class="sxs-lookup"><span data-stu-id="174eb-122">![On hello Welcome page, choose Claims aware](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span></span>
4.  <span data-ttu-id="174eb-123">Hello에 **데이터 원본 선택** 페이지 **hello 신뢰 당사자에 대 한 데이터를 직접 입력**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-123">On hello **Select Data Source** page, click **Enter data about hello relying party manually**, and then click **Next**.</span></span>
    <span data-ttu-id="174eb-124">![Hello 신뢰 당사자 트러스트 데이터 입력](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span><span class="sxs-lookup"><span data-stu-id="174eb-124">![Enter data about hello relying party](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span></span>

5.  <span data-ttu-id="174eb-125">Hello에 **표시 이름 지정** 페이지에 이름을 입력 합니다 **표시 이름**아래 **메모** 이 신뢰 당사자 트러스트에 대 한 설명을 입력 한 다음 클릭 **다음** .</span><span class="sxs-lookup"><span data-stu-id="174eb-125">On hello **Specify Display Name** page, type a name in **Display name**, under **Notes** type a description for this relying party trust, and then click **Next**.</span></span>
    <span data-ttu-id="174eb-126">![표시 이름 및 메모 지정](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span><span class="sxs-lookup"><span data-stu-id="174eb-126">![Specify Display Name and notes](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span></span>
6.  <span data-ttu-id="174eb-127">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-127">Optional.</span></span> <span data-ttu-id="174eb-128">있는지 선택적 토큰 암호화 인증서를 다음 hello에 **인증서 구성** 페이지 **찾아보기** toolocate 인증서 파일을 클릭 한 다음 **다음** .</span><span class="sxs-lookup"><span data-stu-id="174eb-128">If you have an optional token encryption certificate, then on hello **Configure Certificate** page, click **Browse** toolocate your certificate file, and then click **Next**.</span></span>
    <span data-ttu-id="174eb-129">![인증서 구성](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span><span class="sxs-lookup"><span data-stu-id="174eb-129">![Configure Certificate](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span></span>
7.  <span data-ttu-id="174eb-130">Hello에 **URL 구성** 페이지, 선택 hello **hello SAML 2.0 WebSSO 프로토콜에 대 한 지원을 사용 하도록 설정** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-130">On hello **Configure URL** page, select hello **Enable support for hello SAML 2.0 WebSSO protocol** check box.</span></span> <span data-ttu-id="174eb-131">아래 **신뢰 당사자 SAML 2.0 SSO 서비스 URL**이 신뢰 당사자 트러스트에 대 한 hello SAML Security Assertion Markup Language () 서비스 끝점 URL을 입력 한 다음, **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-131">Under **Relying party SAML 2.0 SSO service URL**, type hello Security Assertion Markup Language (SAML) service endpoint URL for this relying party trust, and then click **Next**.</span></span>  <span data-ttu-id="174eb-132">Hello에 대 한 **신뢰 당사자 SAML 2.0 SSO 서비스 URL**, hello 붙여 `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-132">For hello **Relying party SAML 2.0 SSO service URL**, paste hello `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span></span> <span data-ttu-id="174eb-133">테 넌 트의 이름 (예를 들어 contosob2c.onmicrosoft.com)으로 {tenant}를 대체 하 고 확장명 정책 이름 (예를 들어 B2C_1A_TrustFrameworkExtensions)으로 hello {정책}를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-133">Replace {tenant} with your tenant's name (for example, contosob2c.onmicrosoft.com), and replace hello {policy} with your extensions policy name (for example, B2C_1A_TrustFrameworkExtensions).</span></span>
    > [!IMPORTANT]
    ><span data-ttu-id="174eb-134">hello 정책 이름은 signup_or_signin 정책에서 상속한,이 경우 하나 hello: `B2C_1A_TrustFrameworkExtensions`합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-134">hello policy name  is hello one that signup_or_signin policy inherits from, in this case it is: `B2C_1A_TrustFrameworkExtensions`.</span></span>
    ><span data-ttu-id="174eb-135">예를 들어 hello URL 일 수 없습니다: https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-135">For example hello URL could be:   https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span></span>

    ![신뢰 당사자 SAML 2.0 SSO 서비스 URL](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. <span data-ttu-id="174eb-137">Hello에 **식별자 구성** 페이지에서 지정 하는 hello hello 이전 단계와 동일한 URL을 클릭 **추가** tooadd 해당 toohello 목록으로 이동한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-137">On hello **Configure Identifiers** page, specify hello same URL as hello previous step, click **Add** tooadd them toohello list, and then click **Next**.</span></span>
    <span data-ttu-id="174eb-138">![신뢰 당사자 트러스트 식별자](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span><span class="sxs-lookup"><span data-stu-id="174eb-138">![Relying party trust identifiers](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span></span>
9.  <span data-ttu-id="174eb-139">Hello에 **액세스 제어 정책 선택** 정책을 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-139">On hello **Choose Access Control Policy** select a policy and click **Next**.</span></span>
    <span data-ttu-id="174eb-140">![액세스 제어 정책 선택](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span><span class="sxs-lookup"><span data-stu-id="174eb-140">![Choose Access Control Policy](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span></span>
10.  <span data-ttu-id="174eb-141">Hello에 **tooAdd 신뢰 준비** 페이지 hello 설정을 검토 한 다음 클릭 **다음** toosave 신뢰 당사자 트러스트 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-141">On hello **Ready tooAdd Trust** page, review hello settings, and then click **Next** toosave your relying party trust information.</span></span>
    <span data-ttu-id="174eb-142">![신뢰 당사자 트러스트 정보 저장](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span><span class="sxs-lookup"><span data-stu-id="174eb-142">![Save your relying party trust information](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span></span>
11.  <span data-ttu-id="174eb-143">Hello에 **마침** 페이지를 클릭 **닫기**,이 작업은 자동으로 hello 표시 **클레임 규칙 편집** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="174eb-143">On hello **Finish** page, click **Close**, this action automatically displays hello **Edit Claim Rules** dialog box.</span></span>
    <span data-ttu-id="174eb-144">![클레임 규칙 편집](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span><span class="sxs-lookup"><span data-stu-id="174eb-144">![Edit Claim Rules](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span></span>
12. <span data-ttu-id="174eb-145">**규칙 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-145">Click **Add Rule**.</span></span>  
      <span data-ttu-id="174eb-146">![새 규칙 추가](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span><span class="sxs-lookup"><span data-stu-id="174eb-146">![Add new rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span></span>
13.  <span data-ttu-id="174eb-147">**클레임 규칙 템플릿**에서 **LDAP 특성을 클레임으로 전송**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-147">In **Claim rule template**, select **Send LDAP attributes as claims**.</span></span>
    <span data-ttu-id="174eb-148">![LDAP 특성을 클레임 템플릿 규칙으로 전송 선택](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span><span class="sxs-lookup"><span data-stu-id="174eb-148">![Select Send LDAP attributes as claims template rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span></span>
14.  <span data-ttu-id="174eb-149">**클레임 규칙 이름**을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-149">Provide **Claim rule name**.</span></span> <span data-ttu-id="174eb-150">Hello에 대 한 **특성 저장소** 선택 **Active Directory 선택** hello 다음 클레임을 추가한 후 클릭 **마침** 및 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-150">For hello **Attribute store** select **Select Active Directory** Add hello following claims, then click **Finish** and **OK**.</span></span>
    <span data-ttu-id="174eb-151">![규칙 속성 설정](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span><span class="sxs-lookup"><span data-stu-id="174eb-151">![Set rule properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span></span>
15.  <span data-ttu-id="174eb-152">서버 관리자에서 선택 **신뢰 당사자 트러스트** 만든 hello 신뢰 당사자 트러스트를 선택 하 고 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-152">In Server Manager, select **Relying Party Trusts** then select hello relying party trust you created and click **Properties**.</span></span>
    <span data-ttu-id="174eb-153">![신뢰 당사자 편집 속성](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span><span class="sxs-lookup"><span data-stu-id="174eb-153">![Relying party edit properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span></span>
16.  <span data-ttu-id="174eb-154">신뢰 당사자 트러스트 (B2C 데모) 속성 창을 클릭 hello 하나 **서명** 탭을 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-154">One hello relying party trust (B2C Demo) properties window click **Signature** tab and click **Add**.</span></span>  
    <span data-ttu-id="174eb-155">![서명 설정](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span><span class="sxs-lookup"><span data-stu-id="174eb-155">![Set signature](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span></span>
17.  <span data-ttu-id="174eb-156">서명 인증서를 추가합니다(개인 키 없는 .cert 파일).</span><span class="sxs-lookup"><span data-stu-id="174eb-156">Add your signature certificate (.cert file, without private key).</span></span>  
    ![서명 인증서 추가](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  <span data-ttu-id="174eb-158">Hello 신뢰 당사자 트러스트 (B2C 데모) 속성 창에서 클릭 **고급** 탭 하 고 hello 변경 **보안 해시 알고리즘** 너무**s h A-1**, 클릭 **확인**.</span><span class="sxs-lookup"><span data-stu-id="174eb-158">On hello relying party trust (B2C Demo) properties window click **Advanced** tab and change hello **Secure hash algorithm** too**SHA-1**, Click **Ok**.</span></span>  
    <span data-ttu-id="174eb-159">![보안 해시 알고리즘 tooSHA-1을 설정 합니다.](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span><span class="sxs-lookup"><span data-stu-id="174eb-159">![Set secure hash algorithm tooSHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span></span>

## <a name="add-hello-adfs-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="174eb-160">Hello ADFS 계정 응용 프로그램 키 tooAzure AD B2C 추가</span><span class="sxs-lookup"><span data-stu-id="174eb-160">Add hello ADFS account application key tooAzure AD B2C</span></span>
<span data-ttu-id="174eb-161">ADFS 계정으로 페더레이션 hello 응용 프로그램을 대신 하 여 ADFS 계정 tootrust Azure AD B2C에 대 한 클라이언트 암호에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-161">Federation with ADFS accounts requires a client secret for ADFS account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="174eb-162">Toostore ADFS 인증서에에서 필요한 Azure AD B2C 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-162">You need toostore your ADFS certificate in your Azure AD B2C tenant.</span></span> 

1.  <span data-ttu-id="174eb-163">Tooyour Azure AD B2C 테 넌 트를 이동 하 고 선택 **B2C 설정** > **Id 경험 프레임 워크**</span><span class="sxs-lookup"><span data-stu-id="174eb-163">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="174eb-164">선택 **정책 키** 테 넌 트에 사용할 수 있는 tooview hello 키입니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-164">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="174eb-165">**+추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-165">Click **+Add**.</span></span>
4.  <span data-ttu-id="174eb-166">**옵션**에는 **업로드**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-166">For **Options**, use **Upload**.</span></span>
5.  <span data-ttu-id="174eb-167">**이름**에는 `ADFSSamlCert`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-167">For **Name**, use `ADFSSamlCert`.</span></span>  
    <span data-ttu-id="174eb-168">hello 접두사 `B2C_1A_` 자동으로 추가 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-168">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="174eb-169">Hello 파일 업로드에서 * * 개인 키가 있는 인증서.pfx 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-169">In hello File upload,** select your certificate .pfx file with private key.</span></span> <span data-ttu-id="174eb-170">참고:이 인증서 (개인 키 포함 hello) hello 발급 한 hello ad FS 신뢰 당사자에 대해 사용 된 동일한 것 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-170">Note: this certificate (with hello private key) should be hello same one that issued and used for hello ADFS relying party.</span></span>
<span data-ttu-id="174eb-171">![정책 키 업로드](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span><span class="sxs-lookup"><span data-stu-id="174eb-171">![Upload policy key](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span></span>
7.  <span data-ttu-id="174eb-172">**만들기**</span><span class="sxs-lookup"><span data-stu-id="174eb-172">Click **Create**</span></span>
8.  <span data-ttu-id="174eb-173">Hello 키를 만든 확인 `B2C_1A_ADFSSamlCert`합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-173">Confirm that you've created hello key `B2C_1A_ADFSSamlCert`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="174eb-174">확장 정책에서 클레임 공급자 추가</span><span class="sxs-lookup"><span data-stu-id="174eb-174">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="174eb-175">ADFS 계정을 사용 하 여 사용자가 toosign에서 원하는 클레임 공급자로 toodefine ADFS 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-175">If you want users toosign in by using ADFS account, you need toodefine ADFS account as a claims provider.</span></span> <span data-ttu-id="174eb-176">즉, Azure AD B2C와 통신 하는 끝점 toospecify를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-176">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="174eb-177">hello 끝점은 특정 사용자가 인증 하는 Azure AD B2C tooverify에서 사용 되는 클레임 집합을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-177">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="174eb-178">확장 정책 파일에서 `<ClaimsProvider>` 노드를 추가하여 ADFS를 클레임 공급자로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-178">Define ADFS as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1. <span data-ttu-id="174eb-179">작업 디렉터리부터 hello 확장명 정책 파일 (TrustFrameworkExtensions.xml)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-179">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="174eb-180">XML 편집기가 필요하면 간단한 플랫폼 간 편집기인 [Visual Studio Code를 사용해 보세요](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="174eb-180">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2. <span data-ttu-id="174eb-181">Hello `<ClaimsProviders>` 섹션</span><span class="sxs-lookup"><span data-stu-id="174eb-181">Find hello `<ClaimsProviders>` section</span></span>
3. <span data-ttu-id="174eb-182">Hello hello 아래 XML 조각 다음 추가 `ClaimsProviders` 요소 및 바꾸기 `identityProvider` (임의 값 도메인을 나타내는), dns 및 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-182">Add hello following XML snippet under hello `ClaimsProviders` element and replace `identityProvider` with your DNS (Arbitrary value that indicates your domain), and save hello file.</span></span> 

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

## <a name="register-hello-adfs-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="174eb-183">Hello ADFS 계정 클레임 공급자 tooSign를 등록 하거나 사용자의 여행 로그인</span><span class="sxs-lookup"><span data-stu-id="174eb-183">Register hello ADFS account claims provider tooSign up or Sign in user journey</span></span>
<span data-ttu-id="174eb-184">이 시점에서 hello id 공급자 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-184">At this point, hello identity provider has been set up.</span></span>  <span data-ttu-id="174eb-185">그러나, hello 로그-up/로그인 화면 중에서 가능 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-185">However, it is not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="174eb-186">이제 tooadd hello ADFS 계정 id 공급자 tooyour 사용자 필요한 `SignUpOrSignIn` 사용자 여행 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-186">Now you need tooadd hello ADFS account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="174eb-187">toomake 기존 템플릿 사용자 여행 중복 만듭니다 사용할 수 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-187">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="174eb-188">다음, 우리 수정 hello ADFS id 공급자를 포함 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-188">Then, we modify it so it includes hello ADFS identity provider:</span></span>
    >[!NOTE]
    >If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  <span data-ttu-id="174eb-189">Hello 정책 (예를 들어 TrustFrameworkBase.xml)의 기본 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-189">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="174eb-190">Hello `<UserJourneys>` 의 요소와 복사 hello 전체 내용을 `<UserJourneys>` 노드.</span><span class="sxs-lookup"><span data-stu-id="174eb-190">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="174eb-191">Hello 확장 파일 (예를 들어 TrustFrameworkExtensions.xml)를 열고 hello `<UserJourneys>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-191">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="174eb-192">존재 하지 않으면 hello 요소 하나를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-192">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="174eb-193">전체 내용을 hello `<UserJournesy>` hello의 자식으로 복사한 노드 `<UserJourneys>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-193">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="174eb-194">디스플레이 hello 단추</span><span class="sxs-lookup"><span data-stu-id="174eb-194">Display hello button</span></span>
<span data-ttu-id="174eb-195">hello `<ClaimsProviderSelections>` 요소 hello 클레임 공급자 선택 옵션 목록 및 해당 순서를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-195">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="174eb-196">`<ClaimsProviderSelection>`요소는 로그-up/로그인 페이지에 유사한 tooan identity provider 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-196">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="174eb-197">추가 하는 경우는 `<ClaimsProviderSelection>` ADFS 계정에 대 한 요소, 사용자 hello 페이지에 처음 삽입 새 단추 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-197">If you add a `<ClaimsProviderSelection>` element for  ADFS account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="174eb-198">tooadd이이 요소:</span><span class="sxs-lookup"><span data-stu-id="174eb-198">tooadd this element:</span></span>

1.  <span data-ttu-id="174eb-199">Hello `<UserJourney>` 포함 된 노드 `Id="SignUpOrSignIn"` 복사한 hello 사용자 여정에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-199">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="174eb-200">Hello 찾을 `<OrchestrationStep>` 포함 된 노드`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="174eb-200">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="174eb-201">`<ClaimsProviderSelections>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-201">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="174eb-202">링크 hello 단추 tooan 동작</span><span class="sxs-lookup"><span data-stu-id="174eb-202">Link hello button tooan action</span></span>

<span data-ttu-id="174eb-203">Toolink 필요한 위치에 있는 단추를가지고 그 tooan 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-203">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="174eb-204">hello 동작이 경우 ADFS 계정 tooreceive와 Azure AD B2C toocommunicate에 대 한 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-204">hello action, in this case, is for Azure AD B2C toocommunicate with ADFS account tooreceive a token.</span></span> <span data-ttu-id="174eb-205">ADFS 계정 클레임 공급자에 대 한 hello 기술 프로필을 연결 하 여 hello 단추 tooan 동작을 연결할:</span><span class="sxs-lookup"><span data-stu-id="174eb-205">Link hello button tooan action by linking hello technical profile for your ADFS account claims provider:</span></span>

1.  <span data-ttu-id="174eb-206">Hello `<OrchestrationStep>` 포함 된 `Order="2"` hello에 `<UserJourney>` 노드.</span><span class="sxs-lookup"><span data-stu-id="174eb-206">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="174eb-207">`<ClaimsExchanges>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-207">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * <span data-ttu-id="174eb-208">Hello 확인 `Id` 의과 같은 값인 hello에 `TargetClaimsExchangeId` hello 섹션 앞에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-208">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section.</span></span>
> * <span data-ttu-id="174eb-209">확인 `TechnicalProfileReferenceId` 이전 (Contoso SAML2)를 만든 toohello 기술 프로필 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-209">Ensure `TechnicalProfileReferenceId` is set toohello technical profile you created earlier (Contoso-SAML2).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="174eb-210">Hello 정책 tooyour 테 넌 트에 업로드</span><span class="sxs-lookup"><span data-stu-id="174eb-210">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="174eb-211">Hello에 [Azure 포털](https://portal.azure.com), hello를 전환 [Azure AD B2C 테 넌 트의 상황에 맞는](active-directory-b2c-navigate-to-b2c-context.md), 및 열기 hello **Azure AD B2C** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-211">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="174eb-212">**ID 경험 프레임워크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-212">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="174eb-213">열기 hello **모든 정책** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-213">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="174eb-214">**정책 업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-214">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="174eb-215">확인 **있으면 hello 정책 덮어쓰기** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-215">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="174eb-216">**업로드** TrustFrameworkExtensions.xml hello 유효성 검사가 발생 하지 않도록 하 고</span><span class="sxs-lookup"><span data-stu-id="174eb-216">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="174eb-217">지금 실행에 사용 하 여 hello 사용자 지정 정책 테스트</span><span class="sxs-lookup"><span data-stu-id="174eb-217">Test hello custom policy by using Run Now</span></span>
1.  <span data-ttu-id="174eb-218">열기 **Azure AD B2C 설정** 너무 이동**Id 경험 프레임 워크**합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-218">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="174eb-219">열기 **B2C_1A_signup_signin**를 업로드 하는 신뢰 당사자 (RP) 사용자 지정 정책 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-219">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="174eb-220">**지금 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-220">Select **Run now**.</span></span>
3.  <span data-ttu-id="174eb-221">ADFS 계정을 사용 하 여 수 toosign 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-221">You should be able toosign in using ADFS account.</span></span>

## <a name="optional-register-hello-adfs-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="174eb-222">[선택 사항] Hello ADFS 계정 클레임 공급자의 tooProfile 편집 사용자 여행 등록</span><span class="sxs-lookup"><span data-stu-id="174eb-222">[Optional] Register hello ADFS account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="174eb-223">좋습니다 tooadd hello ADFS 계정 id 공급자도 tooyour 사용자 `ProfileEdit` 사용자 여행 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-223">You may want tooadd hello ADFS account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="174eb-224">toomake 마지막 두 단계 hello 반복 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-224">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="174eb-225">디스플레이 hello 단추</span><span class="sxs-lookup"><span data-stu-id="174eb-225">Display hello button</span></span>
1.  <span data-ttu-id="174eb-226">정책 (예를 들어 TrustFrameworkExtensions.xml) hello 확장 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-226">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="174eb-227">Hello `<UserJourney>` 포함 된 노드 `Id="ProfileEdit"` 복사한 hello 사용자 여정에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-227">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="174eb-228">Hello 찾을 `<OrchestrationStep>` 포함 된 노드`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="174eb-228">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="174eb-229">`<ClaimsProviderSelections>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-229">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="174eb-230">링크 hello 단추 tooan 동작</span><span class="sxs-lookup"><span data-stu-id="174eb-230">Link hello button tooan action</span></span>
1.  <span data-ttu-id="174eb-231">Hello `<OrchestrationStep>` 포함 된 `Order="2"` hello에 `<UserJourney>` 노드.</span><span class="sxs-lookup"><span data-stu-id="174eb-231">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="174eb-232">`<ClaimsExchanges>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-232">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="174eb-233">지금 실행에 사용 하 여 hello 사용자 지정 프로필 편집 정책 테스트</span><span class="sxs-lookup"><span data-stu-id="174eb-233">Test hello custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="174eb-234">열기 **Azure AD B2C 설정** 너무 이동**Id 경험 프레임 워크**합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-234">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="174eb-235">열기 **B2C_1A_ProfileEdit**를 업로드 하는 신뢰 당사자 (RP) 사용자 지정 정책 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-235">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="174eb-236">**지금 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-236">Select **Run now**.</span></span>
3.  <span data-ttu-id="174eb-237">ADFS 계정을 사용 하 여 수 toosign 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-237">You should be able toosign in using ADFS account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="174eb-238">Hello 완성 된 정책 파일을 다운로드</span><span class="sxs-lookup"><span data-stu-id="174eb-238">Download hello complete policy files</span></span>
<span data-ttu-id="174eb-239">선택 사항: 권장 hello 사용자 지정 정책을 사용 하 여 시작 안내를 완료 한 후 사용자 고유의 사용자 지정 정책 파일을 사용 하 여 시나리오를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="174eb-239">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through.</span></span> [<span data-ttu-id="174eb-240">참조 전용 정책 샘플 파일</span><span class="sxs-lookup"><span data-stu-id="174eb-240">Policy sample files for reference only</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
