---
title: "조직에서 비즈니스용 Microsoft Windows Hello 사용 | Microsoft Docs"
description: "조직에서 Microsoft Passport를 사용하도록 설정하는 배포 지침입니다."
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
ms.openlocfilehash: 58943e1e29755c983e55c675dd4fe7b75ac47b34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-microsoft-windows-hello-for-business-in-your-organization"></a><span data-ttu-id="6a046-104">조직에서 비즈니스용 Microsoft Windows Hello 사용</span><span class="sxs-lookup"><span data-stu-id="6a046-104">Enable Microsoft Windows Hello for Business in your organization</span></span>
<span data-ttu-id="6a046-105">[Windows 10 도메인에 가입된 장치와 Azure Active Directory를 연결한](active-directory-azureadjoin-devices-group-policy.md) 후에 조직에서 비즈니스용 Microsoft Windows Hello를 사용하도록 설정하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-105">After [connecting Windows 10 domain-joined devices with Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), do the following to enable Microsoft Windows Hello for Business in your organization:</span></span>

1. <span data-ttu-id="6a046-106">System Center Configuration Manager 배포</span><span class="sxs-lookup"><span data-stu-id="6a046-106">Deploy System Center Configuration Manager</span></span>  
2. <span data-ttu-id="6a046-107">정책 설정 구성</span><span class="sxs-lookup"><span data-stu-id="6a046-107">Configure policy settings</span></span>
3. <span data-ttu-id="6a046-108">인증서 프로필 구성</span><span class="sxs-lookup"><span data-stu-id="6a046-108">Configure the certificate profile</span></span>  

## <a name="deploy-system-center-configuration-manager"></a><span data-ttu-id="6a046-109">System Center Configuration Manager 배포</span><span class="sxs-lookup"><span data-stu-id="6a046-109">Deploy System Center Configuration Manager</span></span>
<span data-ttu-id="6a046-110">비즈니스용 Windows Hello 키에 따라 사용자 인증서를 배포하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-110">To deploy user certificates based on Windows Hello for Business keys, you need the following:</span></span>

* <span data-ttu-id="6a046-111">**System Center Configuration Manager 현재 분기** - 1606 이상 버전을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-111">**System Center Configuration Manager Current Branch** - You need to install version 1606 or better.</span></span> <span data-ttu-id="6a046-112">자세한 내용은 [System Center Configuration Manager용 문서](https://technet.microsoft.com/library/mt346023.aspx) 및 [System Center Configuration Manager 팀 블로그](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a046-112">For more information, see the [Documentation for System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) and [System Center Configuration Manager Team Blog](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).</span></span>
* <span data-ttu-id="6a046-113">**PKI(공개 키 인프라)** - 사용자 인증서를 사용하여 비즈니스용 Microsoft Windows Hello를 사용하려면 PKI가 제 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-113">**Public key infrastructure (PKI)** - To enable Microsoft Windows Hello for Business by using user certificates, you must have a PKI in place.</span></span> <span data-ttu-id="6a046-114">PKI 인프라가 없거나 사용자 인증에 대해 사용하지 않으려는 경우 Windows Server 2016 빌드 10551(또는 그 이상)이 설치된 새 도메인 컨트롤러를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-114">If you don’t have one, or you don’t want to use it for user certificates, you can deploy a new domain controller that has Windows Server 2016 build 10551 (or better) installed.</span></span> <span data-ttu-id="6a046-115">단계를 따라 [기존 도메인에 복제본 도메인 컨트롤러를 설치](https://technet.microsoft.com/library/jj574134.aspx)하거나 [새 환경을 만드는 경우 새 Active Directory 포리스트를 설치](https://technet.microsoft.com/library/jj574166)합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-115">Follow the steps to [install a replica domain controller in an existing domain](https://technet.microsoft.com/library/jj574134.aspx) or to [install a new Active Directory forest, if you're creating a new environment](https://technet.microsoft.com/library/jj574166).</span></span> <span data-ttu-id="6a046-116">(ISO는 [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true)에서 다운로드할 수 있음)</span><span class="sxs-lookup"><span data-stu-id="6a046-116">(The ISOs are available for download on [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)</span></span>

## <a name="configure-policy-settings"></a><span data-ttu-id="6a046-117">정책 설정 구성</span><span class="sxs-lookup"><span data-stu-id="6a046-117">Configure policy settings</span></span>
<span data-ttu-id="6a046-118">비즈니스용 Microsoft Windows Hello 정책 설정을 구성하려면 다음 두 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-118">To configure the Microsoft Windows Hello for Business policy settings, you have two options:</span></span>

* <span data-ttu-id="6a046-119">Active Directory에서 그룹 정책</span><span class="sxs-lookup"><span data-stu-id="6a046-119">Group Policy in Active Directory</span></span> 
* <span data-ttu-id="6a046-120">System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="6a046-120">The System Center Configuration Manager</span></span> 

<span data-ttu-id="6a046-121">Active Directory에서 그룹 정책 사용은 비즈니스용 Microsoft Windows Hello 정책 설정을 구성하는 바람직한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-121">Using Group Policy in Active Directory is the recommended method to configure Microsoft Windows Hello for Business policy settings.</span></span> 

<span data-ttu-id="6a046-122">System Center Configuration Manager 사용은 인증서를 배포하기 위해 이를 사용하는 경우 선호되는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-122">Using System Center Configuration Manager is the preferred method when you also use it to deploy certificates.</span></span> <span data-ttu-id="6a046-123">이 시나리오의 경우</span><span class="sxs-lookup"><span data-stu-id="6a046-123">This scenario:</span></span>

* <span data-ttu-id="6a046-124">새로운 배포 시나리오와의 호환성을 보장하고</span><span class="sxs-lookup"><span data-stu-id="6a046-124">Ensures compatibility with the newer deployment scenarios</span></span>
* <span data-ttu-id="6a046-125">클라이언트 쪽 Windows 10 버전 1607 또는 그 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-125">Requires on the client side Windows 10 Version 1607 or better.</span></span>

### <a name="configure-microsoft-windows-hello-for-business-via-group-policy-in-active-directory"></a><span data-ttu-id="6a046-126">Active Directory에서 그룹 정책을 통해 비즈니스용 Microsoft Windows Hello 구성</span><span class="sxs-lookup"><span data-stu-id="6a046-126">Configure Microsoft Windows Hello for Business via group policy in Active Directory</span></span>
<span data-ttu-id="6a046-127">**단계**:</span><span class="sxs-lookup"><span data-stu-id="6a046-127">**Steps**:</span></span>

1. <span data-ttu-id="6a046-128">서버 관리자를 열고 **도구** > **그룹 정책 관리**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-128">Open Server Manager, and navigate to **Tools** > **Group Policy Management**.</span></span>
2. <span data-ttu-id="6a046-129">그룹 정책 관리에서 Azure AD 연결을 사용하도록 설정하려는 도메인에 해당하는 도메인 노드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-129">From Group Policy Management, navigate to the domain node that corresponds to the domain in which you want to enable Azure AD Join.</span></span>
3. <span data-ttu-id="6a046-130">**그룹 정책 개체**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-130">Right-click **Group Policy Objects**, and select **New**.</span></span> <span data-ttu-id="6a046-131">예를 들어 그룹 정책 개체에 이름을 지정하고 비즈니스용 Windows Hello를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-131">Give your Group Policy Object a name, for example, Enable Windows Hello for Business.</span></span> <span data-ttu-id="6a046-132">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-132">Click **OK**.</span></span>
4. <span data-ttu-id="6a046-133">새 그룹 정책 개체를 마우스 오른쪽 단추로 클릭하고 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-133">Right-click your new Group Policy Object, and then select **Edit**.</span></span>
5. <span data-ttu-id="6a046-134">**컴퓨터 구성** > **정책** > **관리 템플릿** > **Windows 구성 요소** > **비즈니스용 Windows Hello**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-134">Navigate to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Windows Hello for Business**.</span></span>
6. <span data-ttu-id="6a046-135">**비즈니스용 Windows Hello 사용**을 마우스 오른쪽 단추로 클릭한 다음 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-135">Right-click **Enable Windows Hello for Business**, and then select **Edit**.</span></span>
7. <span data-ttu-id="6a046-136">**사용** 옵션 단추를 선택하고 **적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-136">Select the **Enabled** option button, and then click **Apply**.</span></span> <span data-ttu-id="6a046-137">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-137">Click **OK**.</span></span>
8. <span data-ttu-id="6a046-138">이제 그룹 정책 개체를 선택한 위치에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-138">You can now link the Group Policy Object to a location of your choice.</span></span> <span data-ttu-id="6a046-139">조직의 모든 Windows 10 도메인에 가입된 장치에 대해 이 정책을 사용하도록 설정하려면 그룹 정책을 도메인에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-139">To enable this policy for all of the domain-joined Windows 10 devices in your organization, link the Group Policy to the domain.</span></span> <span data-ttu-id="6a046-140">예:</span><span class="sxs-lookup"><span data-stu-id="6a046-140">For example:</span></span>
   * <span data-ttu-id="6a046-141">Windows 10 도메인에 가입된 컴퓨터가 배치될 Active Directory의 특정 OU(조직 구성 단위)입니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-141">A specific organizational unit (OU) in Active Directory where Windows 10 domain-joined computers will be located</span></span>
   * <span data-ttu-id="6a046-142">Azure AD에 자동 등록될 Windows 10 도메인에 가입된 컴퓨터를 포함하는 특정 보안 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-142">A specific security group that contains Windows 10 domain-joined computers that will be automatically registered with Azure AD</span></span>

### <a name="configure-windows-hello-for-business-using-system-center-configuration-manager"></a><span data-ttu-id="6a046-143">System Center Configuration Manager를 사용하여 비즈니스용 Windows Hello 구성</span><span class="sxs-lookup"><span data-stu-id="6a046-143">Configure Windows Hello for Business using System Center Configuration Manager</span></span>
<span data-ttu-id="6a046-144">**단계**:</span><span class="sxs-lookup"><span data-stu-id="6a046-144">**Steps**:</span></span>

1. <span data-ttu-id="6a046-145">**System Center Configuration Manager**를 열고 **자산 및 규정 준수 > 규정 준수 설정 > 회사 리소스 액세스 > 비즈니스용 Windows Hello 프로필**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-145">Open the **System Center Configuration Manager**, and then navigate to **Assets & Compliance > Compliance Settings > Company Resource Access > Windows Hello for Business Profiles**.</span></span>
   
    ![비즈니스용 Windows Hello 구성](./media/active-directory-azureadjoin-passport-deployment/01.png)
2. <span data-ttu-id="6a046-147">상단 도구 모음에서 **비즈니스용 Windows Hello 프로필**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-147">In the toolbar on the top, click **Create Windows Hello for business Profile**.</span></span>
   
    ![비즈니스용 Windows Hello 구성](./media/active-directory-azureadjoin-passport-deployment/02.png)
3. <span data-ttu-id="6a046-149">**일반** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-149">On the **General** dialog, perform the following steps:</span></span>
   
    ![비즈니스용 Windows Hello 구성](./media/active-directory-azureadjoin-passport-deployment/03.png)
   
    <span data-ttu-id="6a046-151">a.</span><span class="sxs-lookup"><span data-stu-id="6a046-151">a.</span></span> <span data-ttu-id="6a046-152">**이름** 텍스트 상자에 프로필의 이름을 입력합니다(예: **내 WHfB 프로필**).</span><span class="sxs-lookup"><span data-stu-id="6a046-152">In the **Name** textbox, type a name for your profile, for example, **My WHfB Profile**.</span></span>
   
    <span data-ttu-id="6a046-153">b.</span><span class="sxs-lookup"><span data-stu-id="6a046-153">b.</span></span> <span data-ttu-id="6a046-154">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-154">Click **Next**.</span></span>
4. <span data-ttu-id="6a046-155">**지원되는 플랫폼** 대화 상자에서 이 비즈니스용 Windows Hello 프로필로 프로비전된 플랫폼을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-155">On the **Supported Platforms** dialog, select the platforms that will be provisioned with this Windows Hello for business profile, and then click **Next**.</span></span>
   
    ![비즈니스용 Windows Hello 구성](./media/active-directory-azureadjoin-passport-deployment/04.png)
5. <span data-ttu-id="6a046-157">**설정** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-157">On the **Settings** dialog, perform the following steps:</span></span>
   
    ![비즈니스용 Windows Hello 구성](./media/active-directory-azureadjoin-passport-deployment/05.png)
   
    <span data-ttu-id="6a046-159">a.</span><span class="sxs-lookup"><span data-stu-id="6a046-159">a.</span></span> <span data-ttu-id="6a046-160">**비즈니스용 Windows Hello 구성**에서 **사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-160">As **Configure Windows Hello for Business**, select **Enabled**.</span></span>
   
    <span data-ttu-id="6a046-161">b.</span><span class="sxs-lookup"><span data-stu-id="6a046-161">b.</span></span> <span data-ttu-id="6a046-162">**TPM(신뢰할 수 있는 플랫폼 모듈) 사용**에서 **필수**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-162">As **Use a Trusted Platform Module (TPM)**, select **Required**.</span></span> 
   
    <span data-ttu-id="6a046-163">c.</span><span class="sxs-lookup"><span data-stu-id="6a046-163">c.</span></span> <span data-ttu-id="6a046-164">**인증 방법**에서 **인증서 기반**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-164">As **Authentication method**, select **Certificate-based**.</span></span>
   
    <span data-ttu-id="6a046-165">d.</span><span class="sxs-lookup"><span data-stu-id="6a046-165">d.</span></span> <span data-ttu-id="6a046-166">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-166">Click **Next**.</span></span>
6. <span data-ttu-id="6a046-167">**요약** 대화 상자에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-167">On the **Summary** dialog, click **Next**.</span></span>
7. <span data-ttu-id="6a046-168">**완료** 대화 상자에서 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-168">On the **Completion** dialog, click **Close**.</span></span>
8. <span data-ttu-id="6a046-169">위쪽의 도구 모음에서 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-169">In the toolbar on the top, click **Deploy**.</span></span>
   
    ![비즈니스용 Windows Hello 구성](./media/active-directory-azureadjoin-passport-deployment/06.png)

## <a name="configure-the-certificate-profile"></a><span data-ttu-id="6a046-171">인증서 프로필 구성</span><span class="sxs-lookup"><span data-stu-id="6a046-171">Configure the certificate profile</span></span>
<span data-ttu-id="6a046-172">온-프레미스 인증을 위해 인증서 기반 인증을 사용하는 경우 인증서 프로필을 구성하고 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-172">If you are using certificate-based authentication for on-premises authentication, you need to configure and deploy a certificate profile.</span></span> <span data-ttu-id="6a046-173">이 태스크에서는 System Center Configuration Manager에서 NDES 서버 및 인증서 등록 지점 사이트 역할을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-173">This task requires you to set up an NDES server and Certificate Registration Point site role in the System Center Configuration Manager.</span></span> <span data-ttu-id="6a046-174">자세한 내용은 [Configuration Manager에서 인증서 프로필에 대한 필수 구성 요소](https://technet.microsoft.com/library/dn261205.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a046-174">For more details, see the [Prerequisites for Certificate Profiles in Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).</span></span>

1. <span data-ttu-id="6a046-175">**System Center Configuration Manager**를 열고 **자산 및 규정 준수 > 규정 준수 설정 > 회사 리소스 액세스 > 인증서 프로필**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-175">Open the **System Center Configuration Manager**, and then navigate to **Assets & Compliance > Compliance Settings > Company Resource Access > Certificate Profiles**.</span></span>
2. <span data-ttu-id="6a046-176">스마트 카드 로그인 EKU(확장 키 사용)가 있는 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-176">Select a template that has Smart Card sign-in extended key usage (EKU).</span></span>

<span data-ttu-id="6a046-177">인증서 프로필의 **SCEP 등록** 페이지에서 **Passport for Work에 설치하지 않으면 실패**를 **키 저장소 공급자**로 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a046-177">On the **SCEP Enrollment** page of the certificate profile, you need to choose **Install to Passport for Work otherwise fail** as the **Key Storage Provider**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a046-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6a046-178">Next steps</span></span>
* [<span data-ttu-id="6a046-179">엔터프라이즈를 위한 Windows 10: 작업에 장치를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="6a046-179">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="6a046-180">Azure Active Directory 조인을 통해 클라우드 기능을 Windows 10 장치로 확장</span><span class="sxs-lookup"><span data-stu-id="6a046-180">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="6a046-181">Microsoft Passport를 통해 암호 없이 ID 인증</span><span class="sxs-lookup"><span data-stu-id="6a046-181">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="6a046-182">Azure AD 조인에 대한 사용 시나리오에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="6a046-182">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="6a046-183">Windows 10 환경용 Azure AD에 도메인 가입된 장치 연결</span><span class="sxs-lookup"><span data-stu-id="6a046-183">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="6a046-184">Azure AD 조인 설정</span><span class="sxs-lookup"><span data-stu-id="6a046-184">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

