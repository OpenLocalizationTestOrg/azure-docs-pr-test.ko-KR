---
title: "aaaEnable Microsoft 비즈니스용 Windows Hello 조직의 | Microsoft Docs"
description: "조직에 배포 지침 tooenable Microsoft Passport 합니다."
services: active-directory
documentationcenter: 
keywords: "Microsoft Passport 구성, 비즈니스용 Microsoft Windows Hello 배포"
author: MarkusVi
manager: femila
tags: azure-classic-portal
ms.assetid: 7dbbe3c6-1cd7-429c-a9b2-115fcbc02416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: 6041f5916f606752bc55844b1b2d0a423b913cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-microsoft-windows-hello-for-business-in-your-organization"></a><span data-ttu-id="278d6-104">조직에서 비즈니스용 Microsoft Windows Hello 사용</span><span class="sxs-lookup"><span data-stu-id="278d6-104">Enable Microsoft Windows Hello for Business in your organization</span></span>
<span data-ttu-id="278d6-105">후 [Azure Active Directory와 Windows 10 도메인에 가입 된 장치에 연결](active-directory-azureadjoin-devices-group-policy.md), 조직에서 비즈니스에 대 한 Microsoft Windows Hello tooenable 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-105">After [connecting Windows 10 domain-joined devices with Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), do hello following tooenable Microsoft Windows Hello for Business in your organization:</span></span>

1. <span data-ttu-id="278d6-106">System Center Configuration Manager 배포</span><span class="sxs-lookup"><span data-stu-id="278d6-106">Deploy System Center Configuration Manager</span></span>  
2. <span data-ttu-id="278d6-107">정책 설정 구성</span><span class="sxs-lookup"><span data-stu-id="278d6-107">Configure policy settings</span></span>
3. <span data-ttu-id="278d6-108">Hello 인증서 프로필 구성</span><span class="sxs-lookup"><span data-stu-id="278d6-108">Configure hello certificate profile</span></span>  

## <a name="deploy-system-center-configuration-manager"></a><span data-ttu-id="278d6-109">System Center Configuration Manager 배포</span><span class="sxs-lookup"><span data-stu-id="278d6-109">Deploy System Center Configuration Manager</span></span>
<span data-ttu-id="278d6-110">비즈니스 키에 대 한 Windows Hello를 기반으로 toodeploy 사용자 인증서를 다음 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-110">toodeploy user certificates based on Windows Hello for Business keys, you need hello following:</span></span>

* <span data-ttu-id="278d6-111">**System Center Configuration Manager 현재 분기** -1606 이상 더 좋은 tooinstall 버전이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-111">**System Center Configuration Manager Current Branch** - You need tooinstall version 1606 or better.</span></span> <span data-ttu-id="278d6-112">자세한 내용은 참조 hello [System Center Configuration Manager에 대 한 설명서](https://technet.microsoft.com/library/mt346023.aspx) 및 [System Center Configuration Manager 팀 블로그](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-112">For more information, see hello [Documentation for System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) and [System Center Configuration Manager Team Blog](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).</span></span>
* <span data-ttu-id="278d6-113">**공개 키 인프라 (PKI)** -tooenable Microsoft Windows Hello 사용자 인증서를 사용 하 여 비즈니스에 대 한 위치에서 PKI를 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-113">**Public key infrastructure (PKI)** - tooenable Microsoft Windows Hello for Business by using user certificates, you must have a PKI in place.</span></span> <span data-ttu-id="278d6-114">하나를 갖고 있지 않거나 toouse 원하는 경우 Windows Server 2016이 설치 되어 10551 (또는 그 이상)를 작성 하는 새 도메인 컨트롤러를 배포할 수 사용자 인증서에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-114">If you don’t have one, or you don’t want toouse it for user certificates, you can deploy a new domain controller that has Windows Server 2016 build 10551 (or better) installed.</span></span> <span data-ttu-id="278d6-115">다음과 같이 hello 너무[기존 도메인에서 복제 도메인 컨트롤러를 설치](https://technet.microsoft.com/library/jj574134.aspx) 또는 너무[새 환경을 만드는 경우 새 Active Directory 포리스트를 설치](https://technet.microsoft.com/library/jj574166)합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-115">Follow hello steps too[install a replica domain controller in an existing domain](https://technet.microsoft.com/library/jj574134.aspx) or too[install a new Active Directory forest, if you're creating a new environment](https://technet.microsoft.com/library/jj574166).</span></span> <span data-ttu-id="278d6-116">(Iso hello에 다운로드할 수 있는 [Signiant 미디어 교환이](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)</span><span class="sxs-lookup"><span data-stu-id="278d6-116">(hello ISOs are available for download on [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)</span></span>

## <a name="configure-policy-settings"></a><span data-ttu-id="278d6-117">정책 설정 구성</span><span class="sxs-lookup"><span data-stu-id="278d6-117">Configure policy settings</span></span>
<span data-ttu-id="278d6-118">Microsoft Windows Hello tooconfigure hello 비즈니스 정책 설정에 대 한 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-118">tooconfigure hello Microsoft Windows Hello for Business policy settings, you have two options:</span></span>

* <span data-ttu-id="278d6-119">Active Directory에서 그룹 정책</span><span class="sxs-lookup"><span data-stu-id="278d6-119">Group Policy in Active Directory</span></span> 
* <span data-ttu-id="278d6-120">System Center Configuration Manager hello</span><span class="sxs-lookup"><span data-stu-id="278d6-120">hello System Center Configuration Manager</span></span> 

<span data-ttu-id="278d6-121">사용 하 여 그룹 정책 Active Directory에는 비즈니스 정책 설정에 대 한 Microsoft Windows Hello 메서드 tooconfigure 권장 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-121">Using Group Policy in Active Directory is hello recommended method tooconfigure Microsoft Windows Hello for Business policy settings.</span></span> 

<span data-ttu-id="278d6-122">System Center Configuration Manager를 사용 하는 것이 인증서를 사용할 때 그 toodeploy hello 기본 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-122">Using System Center Configuration Manager is hello preferred method when you also use it toodeploy certificates.</span></span> <span data-ttu-id="278d6-123">이 시나리오의 경우</span><span class="sxs-lookup"><span data-stu-id="278d6-123">This scenario:</span></span>

* <span data-ttu-id="278d6-124">호환 hello 최신 배포 시나리오</span><span class="sxs-lookup"><span data-stu-id="278d6-124">Ensures compatibility with hello newer deployment scenarios</span></span>
* <span data-ttu-id="278d6-125">Windows 10 버전 1607 이상 hello 클라이언트 쪽에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-125">Requires on hello client side Windows 10 Version 1607 or better.</span></span>

### <a name="configure-microsoft-windows-hello-for-business-via-group-policy-in-active-directory"></a><span data-ttu-id="278d6-126">Active Directory에서 그룹 정책을 통해 비즈니스용 Microsoft Windows Hello 구성</span><span class="sxs-lookup"><span data-stu-id="278d6-126">Configure Microsoft Windows Hello for Business via group policy in Active Directory</span></span>
<span data-ttu-id="278d6-127">**단계**:</span><span class="sxs-lookup"><span data-stu-id="278d6-127">**Steps**:</span></span>

1. <span data-ttu-id="278d6-128">서버 관리자를 열고 너무 이동**도구** > **그룹 정책 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-128">Open Server Manager, and navigate too**Tools** > **Group Policy Management**.</span></span>
2. <span data-ttu-id="278d6-129">그룹 정책 관리에서 해당 하는 Azure AD Join tooenable 원하는 toohello 도메인은 toohello 도메인 노드를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-129">From Group Policy Management, navigate toohello domain node that corresponds toohello domain in which you want tooenable Azure AD Join.</span></span>
3. <span data-ttu-id="278d6-130">**그룹 정책 개체**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-130">Right-click **Group Policy Objects**, and select **New**.</span></span> <span data-ttu-id="278d6-131">예를 들어 그룹 정책 개체에 이름을 지정하고 비즈니스용 Windows Hello를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-131">Give your Group Policy Object a name, for example, Enable Windows Hello for Business.</span></span> <span data-ttu-id="278d6-132">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-132">Click **OK**.</span></span>
4. <span data-ttu-id="278d6-133">새 그룹 정책 개체를 마우스 오른쪽 단추로 클릭하고 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-133">Right-click your new Group Policy Object, and then select **Edit**.</span></span>
5. <span data-ttu-id="278d6-134">너무 이동**컴퓨터 구성** > **정책** > **관리 템플릿** > **Windows 구성 요소** > **비즈니스용 Windows Hello**합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-134">Navigate too**Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Windows Hello for Business**.</span></span>
6. <span data-ttu-id="278d6-135">**비즈니스용 Windows Hello 사용**을 마우스 오른쪽 단추로 클릭한 다음 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-135">Right-click **Enable Windows Hello for Business**, and then select **Edit**.</span></span>
7. <span data-ttu-id="278d6-136">선택 hello **Enabled** 옵션 단추를 선택한 다음 클릭 **적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-136">Select hello **Enabled** option button, and then click **Apply**.</span></span> <span data-ttu-id="278d6-137">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-137">Click **OK**.</span></span>
8. <span data-ttu-id="278d6-138">이제 hello 그룹 정책 개체 tooa 선택한 위치에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-138">You can now link hello Group Policy Object tooa location of your choice.</span></span> <span data-ttu-id="278d6-139">tooenable이이 정책은 모든 링크 hello 그룹 정책 toohello 도메인은 조직에서 hello 도메인에 가입 된 Windows 10 장치에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-139">tooenable this policy for all of hello domain-joined Windows 10 devices in your organization, link hello Group Policy toohello domain.</span></span> <span data-ttu-id="278d6-140">예:</span><span class="sxs-lookup"><span data-stu-id="278d6-140">For example:</span></span>
   * <span data-ttu-id="278d6-141">Windows 10 도메인에 가입된 컴퓨터가 배치될 Active Directory의 특정 OU(조직 구성 단위)입니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-141">A specific organizational unit (OU) in Active Directory where Windows 10 domain-joined computers will be located</span></span>
   * <span data-ttu-id="278d6-142">Azure AD에 자동 등록될 Windows 10 도메인에 가입된 컴퓨터를 포함하는 특정 보안 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-142">A specific security group that contains Windows 10 domain-joined computers that will be automatically registered with Azure AD</span></span>

### <a name="configure-windows-hello-for-business-using-system-center-configuration-manager"></a><span data-ttu-id="278d6-143">System Center Configuration Manager를 사용하여 비즈니스용 Windows Hello 구성</span><span class="sxs-lookup"><span data-stu-id="278d6-143">Configure Windows Hello for Business using System Center Configuration Manager</span></span>
<span data-ttu-id="278d6-144">**단계**:</span><span class="sxs-lookup"><span data-stu-id="278d6-144">**Steps**:</span></span>

1. <span data-ttu-id="278d6-145">열기 hello **System Center Configuration Manager**를 이동한 후 너무**자산 및 호환성 > 규정 준수 설정 > 회사 리소스 액세스 > 비즈니스 프로필에 대 한 Windows Hello**합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-145">Open hello **System Center Configuration Manager**, and then navigate too**Assets & Compliance > Compliance Settings > Company Resource Access > Windows Hello for Business Profiles**.</span></span>
   
    ![비즈니스용 Windows Hello 구성](./media/active-directory-azureadjoin-passport-deployment/01.png)
2. <span data-ttu-id="278d6-147">도구 모음의 hello hello 위쪽에 클릭 **프로필 비즈니스용 Windows Hello 만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-147">In hello toolbar on hello top, click **Create Windows Hello for business Profile**.</span></span>
   
    ![비즈니스용 Windows Hello 구성](./media/active-directory-azureadjoin-passport-deployment/02.png)
3. <span data-ttu-id="278d6-149">Hello에 **일반** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-149">On hello **General** dialog, perform hello following steps:</span></span>
   
    ![비즈니스용 Windows Hello 구성](./media/active-directory-azureadjoin-passport-deployment/03.png)
   
    <span data-ttu-id="278d6-151">a.</span><span class="sxs-lookup"><span data-stu-id="278d6-151">a.</span></span> <span data-ttu-id="278d6-152">Hello에 **이름** 텍스트 상자, 예를 들어 프로필에 대 한 이름 입력 **내 WHfB 프로필**합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-152">In hello **Name** textbox, type a name for your profile, for example, **My WHfB Profile**.</span></span>
   
    <span data-ttu-id="278d6-153">b.</span><span class="sxs-lookup"><span data-stu-id="278d6-153">b.</span></span> <span data-ttu-id="278d6-154">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-154">Click **Next**.</span></span>
4. <span data-ttu-id="278d6-155">Hello에 **지원 되는 플랫폼** 대화 상자에서 비즈니스 프로필에 대 한이 Windows Hello로 프로 비전 됩니다을 클릭 한 다음 선택 hello 플랫폼 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-155">On hello **Supported Platforms** dialog, select hello platforms that will be provisioned with this Windows Hello for business profile, and then click **Next**.</span></span>
   
    ![비즈니스용 Windows Hello 구성](./media/active-directory-azureadjoin-passport-deployment/04.png)
5. <span data-ttu-id="278d6-157">Hello에 **설정을** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-157">On hello **Settings** dialog, perform hello following steps:</span></span>
   
    ![비즈니스용 Windows Hello 구성](./media/active-directory-azureadjoin-passport-deployment/05.png)
   
    <span data-ttu-id="278d6-159">a.</span><span class="sxs-lookup"><span data-stu-id="278d6-159">a.</span></span> <span data-ttu-id="278d6-160">**비즈니스용 Windows Hello 구성**에서 **사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-160">As **Configure Windows Hello for Business**, select **Enabled**.</span></span>
   
    <span data-ttu-id="278d6-161">b.</span><span class="sxs-lookup"><span data-stu-id="278d6-161">b.</span></span> <span data-ttu-id="278d6-162">**TPM(신뢰할 수 있는 플랫폼 모듈) 사용**에서 **필수**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-162">As **Use a Trusted Platform Module (TPM)**, select **Required**.</span></span> 
   
    <span data-ttu-id="278d6-163">c.</span><span class="sxs-lookup"><span data-stu-id="278d6-163">c.</span></span> <span data-ttu-id="278d6-164">**인증 방법**에서 **인증서 기반**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-164">As **Authentication method**, select **Certificate-based**.</span></span>
   
    <span data-ttu-id="278d6-165">d.</span><span class="sxs-lookup"><span data-stu-id="278d6-165">d.</span></span> <span data-ttu-id="278d6-166">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-166">Click **Next**.</span></span>
6. <span data-ttu-id="278d6-167">Hello에 **요약** 대화 상자를 클릭 하 여 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-167">On hello **Summary** dialog, click **Next**.</span></span>
7. <span data-ttu-id="278d6-168">Hello에 **완료** 대화 상자를 클릭 하 여 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-168">On hello **Completion** dialog, click **Close**.</span></span>
8. <span data-ttu-id="278d6-169">도구 모음의 hello hello 위쪽에 클릭 **배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-169">In hello toolbar on hello top, click **Deploy**.</span></span>
   
    ![비즈니스용 Windows Hello 구성](./media/active-directory-azureadjoin-passport-deployment/06.png)

## <a name="configure-hello-certificate-profile"></a><span data-ttu-id="278d6-171">Hello 인증서 프로필 구성</span><span class="sxs-lookup"><span data-stu-id="278d6-171">Configure hello certificate profile</span></span>
<span data-ttu-id="278d6-172">인증서 기반 인증을 온-프레미스 인증을 위해 사용 하는 경우 tooconfigure 필요 하 고 인증서 프로필을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-172">If you are using certificate-based authentication for on-premises authentication, you need tooconfigure and deploy a certificate profile.</span></span> <span data-ttu-id="278d6-173">이 작업을 위해서는 tooset NDES 서버 및 hello System Center Configuration Manager에서에서 인증서 등록 지점 사이트 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-173">This task requires you tooset up an NDES server and Certificate Registration Point site role in hello System Center Configuration Manager.</span></span> <span data-ttu-id="278d6-174">자세한 내용은 참조 hello [Prerequisites for Certificate Profiles in Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-174">For more details, see hello [Prerequisites for Certificate Profiles in Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).</span></span>

1. <span data-ttu-id="278d6-175">열기 hello **System Center Configuration Manager**를 이동한 후 너무**자산 및 호환성 > 규정 준수 설정 > 회사 리소스 액세스 > 인증서 프로필**합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-175">Open hello **System Center Configuration Manager**, and then navigate too**Assets & Compliance > Compliance Settings > Company Resource Access > Certificate Profiles**.</span></span>
2. <span data-ttu-id="278d6-176">스마트 카드 로그인 EKU(확장 키 사용)가 있는 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-176">Select a template that has Smart Card sign-in extended key usage (EKU).</span></span>

<span data-ttu-id="278d6-177">Hello에 **SCEP 등록** 페이지 toochoose hello 인증서 프로필의 필요한 **설치, 그렇지 않으면 작업 실패에 대 한 tooPassport** hello로 **키 저장소 공급자**합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-177">On hello **SCEP Enrollment** page of hello certificate profile, you need toochoose **Install tooPassport for Work otherwise fail** as hello **Key Storage Provider**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="278d6-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="278d6-178">Next steps</span></span>
* [<span data-ttu-id="278d6-179">Hello 엔터프라이즈용 Windows 10: 작업에 대 한 방법으로 toouse 장치</span><span class="sxs-lookup"><span data-stu-id="278d6-179">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="278d6-180">Azure Active Directory Join을 통해 기능 10 tooWindows 장치 클라우드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="278d6-180">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="278d6-181">Microsoft Passport를 통해 암호 없이 ID 인증</span><span class="sxs-lookup"><span data-stu-id="278d6-181">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="278d6-182">Azure AD 조인에 대한 사용 시나리오에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="278d6-182">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="278d6-183">Windows 10 환경용에 대 한 AD 도메인에 가입 된 장치 tooAzure 연결</span><span class="sxs-lookup"><span data-stu-id="278d6-183">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="278d6-184">Azure AD 조인 설정</span><span class="sxs-lookup"><span data-stu-id="278d6-184">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

