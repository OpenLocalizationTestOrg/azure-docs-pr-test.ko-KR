---
title: "설정에서 Azure AD으로 Windows 10 장치 설정| Microsoft Docs"
description: "사용자가 설정 메뉴를 통해 Azure AD에 조인시킬 수 있는 방법에 대해 설명합니다."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 5a3963f16b471ad1ca8681b22a1a027935400465
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a><span data-ttu-id="6af15-103">설정에서 Azure AD으로 Windows 10 장치 설정</span><span class="sxs-lookup"><span data-stu-id="6af15-103">Set up a Windows 10 device with Azure AD from Settings</span></span>
<span data-ttu-id="6af15-104">Windows 7 또는 Windows 8을 이미 사용 중이고 컴퓨터 또는 장치를 Windows 10으로 업그레이드한 경우 설정 메뉴에서 Azure Active Directory(Azure AD)에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6af15-104">If you are already using Windows 7 or Windows 8, and your computer or device has been upgraded to Windows 10, you can join to Azure Active Directory (Azure AD) through the Settings menu.</span></span>

## <a name="to-join-to-azure-ad-from-the-settings-menu"></a><span data-ttu-id="6af15-105">설정 메뉴에서 Azure AD에 연결하려면</span><span class="sxs-lookup"><span data-stu-id="6af15-105">To join to Azure AD from the Settings menu</span></span>
1. <span data-ttu-id="6af15-106">**시작** 메뉴에서 **설정** 참을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6af15-106">From the **Start** menu, click the **Settings** charm.</span></span>
2. <span data-ttu-id="6af15-107">**설정**에서 **시스템**->**정보**->**Azure AD 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6af15-107">From **Settings**, select     **System**->**About**->**Join Azure AD**.</span></span>
   
   <span data-ttu-id="6af15-108"><center>
   ![설정 메뉴에서 Azure AD 연결](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span><span class="sxs-lookup"><span data-stu-id="6af15-108"><center>
![Join Azure AD from the Settings menu](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span></span>
3. <span data-ttu-id="6af15-109">Azure AD 조인 메시지 창에서 **계속** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6af15-109">Click **Continue** in the Azure AD Join message window.</span></span>
   
   <span data-ttu-id="6af15-110"><center>
   ![Azure AD 연결 메시지 창](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span><span class="sxs-lookup"><span data-stu-id="6af15-110"><center>
![Join Azure AD message window](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span></span>
4. <span data-ttu-id="6af15-111">로그인 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6af15-111">Provide your sign-in credentials.</span></span> <span data-ttu-id="6af15-112">이 로그인 환경은 완전한 인증에 필요한 모든 단계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6af15-112">This sign-in experience will include all the steps that are required to complete authentication.</span></span> <span data-ttu-id="6af15-113">페더레이션된 테넌트의 일부인 경우 관리자가 조직이 호스팅하는 페더레이션 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6af15-113">If you are part of a federated tenant, your administrator will provide you with the federation experience that's hosted by your organization.</span></span>
   <span data-ttu-id="6af15-114"><center>
   ![로그인 자격 증명 제공](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span><span class="sxs-lookup"><span data-stu-id="6af15-114"><center>
![Provide sign-in credentials](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span></span>
5. <span data-ttu-id="6af15-115">조직에서 Azure AD를 연결하기 위해 다중요소 인증을 구성한 경우 계속 진행하기 전에 두 번째 요소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6af15-115">If your organization has configured Azure Multi-Factor Authentication for joining to Azure AD, provide the second factor before proceeding.</span></span>
6. <span data-ttu-id="6af15-116">**이 장치가 관리되도록 허용** 화면에서 **동의**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6af15-116">Click **Accept** on the **Allow this device to be managed** screen.</span></span>
7. <span data-ttu-id="6af15-117">"이제 장치가 Azure AD의 조직에 조인되었습니다"라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6af15-117">You should see the message "Your device is now joined to your organization in Azure AD".</span></span>

## <a name="additional-information"></a><span data-ttu-id="6af15-118">추가 정보</span><span class="sxs-lookup"><span data-stu-id="6af15-118">Additional information</span></span>
* [<span data-ttu-id="6af15-119">Azure AD 조인에 대한 사용 시나리오에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="6af15-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="6af15-120">Windows 10 환경용 Azure AD에 도메인 가입된 장치 연결</span><span class="sxs-lookup"><span data-stu-id="6af15-120">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="6af15-121">Azure AD 조인 설정</span><span class="sxs-lookup"><span data-stu-id="6af15-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)
* [<span data-ttu-id="6af15-122">Microsoft Passport를 통해 암호 없이 ID 인증</span><span class="sxs-lookup"><span data-stu-id="6af15-122">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)

