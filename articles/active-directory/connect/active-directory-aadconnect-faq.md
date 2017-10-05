---
title: 'Azure Active Directory Connect: FAQ - | Microsoft Docs'
description: "이 페이지에는 Azure AD Connect에 대해 자주 묻는 질문과 대답이 있습니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 4e47a087-ebcd-4b63-9574-0c31907a39a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: fd5988b2d4170166902bb5cc39603d4a0f83be59
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a><span data-ttu-id="9030f-103">Azure Active Directory Connect에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="9030f-103">Frequently asked questions for Azure Active Directory Connect</span></span>

## <a name="general-installation"></a><span data-ttu-id="9030f-104">일반 설치</span><span class="sxs-lookup"><span data-stu-id="9030f-104">General installation</span></span>
<span data-ttu-id="9030f-105">**Q: Azure AD 전역 관리자가 2FA를 사용하도록 설정한 경우 설치가 작동하나요?**</span><span class="sxs-lookup"><span data-stu-id="9030f-105">**Q: Will installation work if the Azure AD Global Admin has 2FA enabled?**</span></span>  
<span data-ttu-id="9030f-106">2016년 2월 빌드에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-106">With the builds from February 2016, this is supported.</span></span>

<span data-ttu-id="9030f-107">**Q: Azure AD Connect를 무인 설치하는 방법이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9030f-107">**Q: Is there a way to install Azure AD Connect unattended?**</span></span>  
<span data-ttu-id="9030f-108">설치 마법사를 사용하여 Azure AD Connect 설치만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-108">It is only supported to install Azure AD Connect using the installation wizard.</span></span> <span data-ttu-id="9030f-109">무인 및 자동 설치는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-109">An unattended and silent installation is not supported.</span></span>

<span data-ttu-id="9030f-110">**Q: 하나의 도메인에 연결할 수 없는 포리스트가 있습니다. Azure AD Connect를 설치하려면 어떻게 하나요?**</span><span class="sxs-lookup"><span data-stu-id="9030f-110">**Q: I have a forest where one domain cannot be contacted. How do I install Azure AD Connect?**</span></span>  
<span data-ttu-id="9030f-111">2016년 2월 빌드에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-111">With the builds from February 2016, this is supported.</span></span>

<span data-ttu-id="9030f-112">**Q: AD DS 상태 에이전트는 서버 코어에서 작동하나요?**</span><span class="sxs-lookup"><span data-stu-id="9030f-112">**Q: Does the AD DS health agent work on server core?**</span></span>  
<span data-ttu-id="9030f-113">예.</span><span class="sxs-lookup"><span data-stu-id="9030f-113">Yes.</span></span> <span data-ttu-id="9030f-114">에이전트를 설치한 후 다음 PowerShell cmdlet을 사용하여 등록 프로세스를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-114">After installing the agent, you can complete the registration process using the following PowerShell cmdlet:</span></span> 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a><span data-ttu-id="9030f-115">네트워크</span><span class="sxs-lookup"><span data-stu-id="9030f-115">Network</span></span>
<span data-ttu-id="9030f-116">**Q: 방화벽, 네트워크 장치 또는 네트워크에서 열려 있는 상태로 유지할 수 있는 최대 시간 연결을 제한하는 다른 요소가 있습니다. Azure AD Connect를 사용하는 경우 클라이언트 쪽 기간 내 클라이언트 쪽 시간 제한 임계값은 얼마나 길어야 합니까?**</span><span class="sxs-lookup"><span data-stu-id="9030f-116">**Q: I have a firewall, network device, or something else that limits the maximum time connections can stay open on my network. How long should my client side timeout threshold be when using Azure AD Connect?**</span></span>  
<span data-ttu-id="9030f-117">모든 네트워킹 소프트웨어, 물리적 장치 또는 열린 상태로 둘 수 있는 최대 시간 연결을 제한하는 다른 것은 Azure AD Connect 클라이언트를 설치한 서버와 Azure Active Directory 간의 연결에 대해 적어도 5분(300초)의 임계값을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-117">All networking software, physical devices, or anything else that limits the maximum time connections can remain open should use a threshold of at least 5 minutes (300 seconds) for connectivity between the server where the Azure AD Connect client is installed and Azure Active Directory.</span></span> <span data-ttu-id="9030f-118">이는 이전에 릴리스된 모든 Microsoft ID 동기화 도구에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-118">This also applies to all previously released Microsoft Identity synchronization tools.</span></span>

<span data-ttu-id="9030f-119">**Q: SLD(단일 레이블 도메인)가 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="9030f-119">**Q: Are SLDs (Single Label Domains) supported?**</span></span>  
<span data-ttu-id="9030f-120">아니요 Azure AD Connect는 SLD를 사용하는 온-프레미스 포리스트/도메인을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-120">No, Azure AD Connect does not support on-premises forests/domains using SLDs.</span></span>

<span data-ttu-id="9030f-121">**Q: "마침표"를 포함하는 NetBios 이름이 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="9030f-121">**Q: Are "dotted" NetBios named supported?**</span></span>  
<span data-ttu-id="9030f-122">아니요, Azure AD Connect는 NetBios 이름에 마침표 "."를 포함하는 온-프레미스 포리스트/도메인을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-122">No, Azure AD Connect does not support on-premises forests/domains where the NetBios name contains a period "." in the name.</span></span>

## <a name="federation"></a><span data-ttu-id="9030f-123">페더레이션</span><span class="sxs-lookup"><span data-stu-id="9030f-123">Federation</span></span>
<span data-ttu-id="9030f-124">**Q: 내 Office 365 인증서를 갱신하라는 메일을 받는 경우 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="9030f-124">**Q: What do I do if I receive an email that asking me to renew my Office 365 certificate**</span></span>  
<span data-ttu-id="9030f-125">인증서를 갱신하는 방법은 [인증서 갱신](active-directory-aadconnect-o365-certs.md) 항목에 설명된 참고 자료를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="9030f-125">Use the guidance that is outlined in the [renew certificates](active-directory-aadconnect-o365-certs.md) topic on how to renew the certificate.</span></span>

<span data-ttu-id="9030f-126">**Q: O365 신뢰 당사자에 대해 "신뢰 당사자 자동 업데이트"를 설정했습니다. 토큰 서명 인증서가 자동으로 롤오버될 때 어떤 조치를 취해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="9030f-126">**Q: I have "Automatically update relying party" set for O365 relying party. Do I have to take any action when my token signing certificate automatically rolls over?**</span></span>  
<span data-ttu-id="9030f-127">[인증서 갱신](active-directory-aadconnect-o365-certs.md)문서에 설명된 참고 자료를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="9030f-127">Use the guidance that is outlined in the article [renew certificates](active-directory-aadconnect-o365-certs.md).</span></span>

## <a name="environment"></a><span data-ttu-id="9030f-128">Environment</span><span class="sxs-lookup"><span data-stu-id="9030f-128">Environment</span></span>
<span data-ttu-id="9030f-129">**Q: Azure AD Connect를 설치한 후에 서버 이름을 변경하는 것이 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="9030f-129">**Q: Is it supported to rename the server after Azure AD Connect has been installed?**</span></span>  
<span data-ttu-id="9030f-130">아니요.</span><span class="sxs-lookup"><span data-stu-id="9030f-130">No.</span></span> <span data-ttu-id="9030f-131">서버 이름을 변경하면 동기화 엔진이 SQL 데이터베이스에 연결할 수 없게 되고 서비스를 시작할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-131">Changing the server name will cause the sync engine to not be able to connect to the SQL database and the service will not be able to start.</span></span>

## <a name="identity-data"></a><span data-ttu-id="9030f-132">ID 데이터</span><span class="sxs-lookup"><span data-stu-id="9030f-132">Identity data</span></span>
<span data-ttu-id="9030f-133">**Q: Azure AD의 UPN(userPrincipalName) 특성이 온-프레미스 UPN가 일치하지 않습니다. 왜 그런가요?**</span><span class="sxs-lookup"><span data-stu-id="9030f-133">**Q: The UPN (userPrincipalName) attribute in Azure AD does not match the on-prem UPN - why?**</span></span>  
<span data-ttu-id="9030f-134">아래 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9030f-134">See these articles:</span></span>

* [<span data-ttu-id="9030f-135">Office 365, Azure 또는 Intune의 사용자 이름이 온-프레미스 UPN 또는 대체 로그인 ID와 일치하지 않습니다(영문).</span><span class="sxs-lookup"><span data-stu-id="9030f-135">User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID</span></span>](https://support.microsoft.com/en-us/kb/2523192)
* [<span data-ttu-id="9030f-136">다른 페더레이션된 도메인을 사용하기 위해 사용자 계정의 UPN을 변경한 후에 Azure Active Directory 동기화 도구에서 변경 사항이 동기화되지 않습니다(영문).</span><span class="sxs-lookup"><span data-stu-id="9030f-136">Changes aren't synced by the Azure Active Directory Sync tool after you change the UPN of a user account to use a different federated domain</span></span>](https://support.microsoft.com/en-us/kb/2669550)

<span data-ttu-id="9030f-137">[Azure AD Connect 동기화 서비스 기능](active-directory-aadconnectsyncservice-features.md)에 설명된 대로 동기화 엔진이 userPrincipalName을 업그레이드할 수 있도록 Azure AD를 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-137">You can also configure Azure AD to allow the sync engine to update the userPrincipalName as described in [Azure AD Connect sync service features](active-directory-aadconnectsyncservice-features.md).</span></span>

<span data-ttu-id="9030f-138">**Q:기존 Azure AD Group/Contact 개체와 온-프레미스 AD Group/Contact 개체의 소프트 매칭이 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="9030f-138">**Q: Is it supported to soft match on-premises AD Group/Contact objects with existing Azure AD Group/Contact objects?**</span></span>  
<span data-ttu-id="9030f-139">아니요. 현재는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-139">No, this is currently not supported.</span></span>

<span data-ttu-id="9030f-140">**Q: 기존 Azure AD Group/Contact 개체의 ImmutableId 특성을 온-프레미스 AD Group/Contact 개체에 하드 매칭하도록 수동 설정하는 것이 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="9030f-140">**Q: Is it supported to manually set ImmutableId attribute on existing Azure AD Group/Contact objects to hard match it to on-premises AD Group/Contact objects?**</span></span>  
<span data-ttu-id="9030f-141">아니요. 현재는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-141">No, this is currently not supported.</span></span>



## <a name="custom-configuration"></a><span data-ttu-id="9030f-142">사용자 지정 구성</span><span class="sxs-lookup"><span data-stu-id="9030f-142">Custom configuration</span></span>
<span data-ttu-id="9030f-143">**Q: Azure AD Connect에 대한 PowerShell cmdlet 설명서는 어디에 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9030f-143">**Q: Where are the PowerShell cmdlets for Azure AD Connect documented?**</span></span>  
<span data-ttu-id="9030f-144">이 사이트에 설명되어 있는 cmdlet을 제외하고, Azure AD Connect에 나오는 다른 PowerShell cmdlet은 고객 사용이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-144">With the exception of the cmdlets documented on this site, other PowerShell cmdlets found in Azure AD Connect are not supported for customer use.</span></span>

<span data-ttu-id="9030f-145">**Q: *Synchronization Service Manager*의 "서버 내보내기/서버 가져오기"를 사용하여 서버 간에 구성을 이동할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9030f-145">**Q: Can I use "Server export/server import" found in *Synchronization Service Manager* to move configuration between servers?**</span></span>  
<span data-ttu-id="9030f-146">아니요.</span><span class="sxs-lookup"><span data-stu-id="9030f-146">No.</span></span> <span data-ttu-id="9030f-147">이 옵션은 모든 구성 설정을 가져오는 것이 아니므로 사용하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-147">This option will not retrieve all configuration settings and should not be used.</span></span> <span data-ttu-id="9030f-148">그 대신 마법사를 사용하여 두 번째 서버에 기본 구성을 만들고 동기화 규칙 편집기를 사용하여 PowerShell 스크립트를 생성하여 서버 간에 사용자 지정 규칙을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-148">You should instead use the wizard to create the base configuration on the second server and use the sync rule editor to generate PowerShell scripts to move any custom rule between servers.</span></span> <span data-ttu-id="9030f-149">[스윙 마이그레이션](active-directory-aadconnect-upgrade-previous-version.md#swing-migration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9030f-149">See [Swing migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span>

<span data-ttu-id="9030f-150">**Q: autocomplete 특성이 "false"인 암호 입력 요소를 포함하고 있으니 Azure 로그인 페이지에 대한 암호를 캐시하면 이 문제를 방지할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9030f-150">**Q: Can passwords be cached for the Azure sign-in page and can this be prevented since it contains a password input element with the autocomplete = "false" attribute?**</span></span></br>
<span data-ttu-id="9030f-151">현재는 autocomplete 태그를 포함하여 암호 입력 필드의 HTML 특성을 수정하는 기능이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-151">We currently do not support modifying the HTML attributes of the Password input field, including the autocomplete tag.</span></span> <span data-ttu-id="9030f-152">현재 암호 필드에 특성을 추가할 수 있도록 사용자 지정 Javascript를 허용하는 기능을 개발하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-152">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span></span> <span data-ttu-id="9030f-153">이 기능은 2017년 하반기에 제공될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-153">This should be available later part of 2017.</span></span>

<span data-ttu-id="9030f-154">**Q: Azure 로그인 페이지에서 이전에 성공적으로 로그인한 사용자의 사용자 이름이 표시됩니다.  이 동작을 끌 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9030f-154">**Q: On the Azure sign-in page, usernames for users who have previously signed in successfully are shown.  Can this behavior be turned off?**</span></span></br>
<span data-ttu-id="9030f-155">현재는 로그인 페이지의 HTML 특성을 수정하는 기능이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-155">We currently do not support modifying the HTML attributes of the sign-in page.</span></span> <span data-ttu-id="9030f-156">현재 암호 필드에 특성을 추가할 수 있도록 사용자 지정 Javascript를 허용하는 기능을 개발하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-156">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span></span> <span data-ttu-id="9030f-157">이 기능은 2017년 하반기에 제공될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-157">This should be available later part of 2017.</span></span>

<span data-ttu-id="9030f-158">**Q: 동시 세션을 방지하는 방법이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9030f-158">**Q: Is there a way to prevent concurrent sessions?**</span></span></br>
<span data-ttu-id="9030f-159">아니요.</span><span class="sxs-lookup"><span data-stu-id="9030f-159">No.</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="9030f-160">문제 해결</span><span class="sxs-lookup"><span data-stu-id="9030f-160">Troubleshooting</span></span>
<span data-ttu-id="9030f-161">**Q: Azure AD Connect에 대한 도움을 받으려면 어떻게 합니까?**</span><span class="sxs-lookup"><span data-stu-id="9030f-161">**Q: How can I get help with Azure AD Connect?**</span></span>

[<span data-ttu-id="9030f-162">Microsoft KB(기술 자료) 검색</span><span class="sxs-lookup"><span data-stu-id="9030f-162">Search the Microsoft Knowledge Base (KB)</span></span>](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* <span data-ttu-id="9030f-163">Microsoft KB(기술 자료)에서 Azure AD Connect 지원에 대한 일반적인 고장 수리 문제에 대한 기술 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="9030f-163">Search the Microsoft Knowledge Base (KB) for technical solutions to common break-fix issues about Support for Azure AD Connect.</span></span>

[<span data-ttu-id="9030f-164">Microsoft Azure Active Directory 포럼</span><span class="sxs-lookup"><span data-stu-id="9030f-164">Microsoft Azure Active Directory Forums</span></span>](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* <span data-ttu-id="9030f-165">커뮤니티에서 기술 질문 및 대답을 검색하고 찾아보거나 [여기](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required)를 클릭하여 직접 질문을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-165">You can search and browse for technical questions and answers from the community or ask your own question by clicking [here](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span></span>

[<span data-ttu-id="9030f-166">Azure AD Connect 고객 지원</span><span class="sxs-lookup"><span data-stu-id="9030f-166">Azure AD Connect customer support</span></span>](https://manage.windowsazure.com/?getsupport=true)

* <span data-ttu-id="9030f-167">Azure Portal을 통해 지원을 받으려면 이 링크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9030f-167">Use this link to get support through the Azure portal.</span></span>

