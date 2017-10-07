---
title: "설정에서 Azure AD 사용 하 여 Windows 10 장치 aaaSet | Microsoft Docs"
description: "사용자가 hello 설정 메뉴를 통해 AD tooAzure를 조인할 수는 방법에 대해 설명 합니다."
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
ms.openlocfilehash: d6485228338db571cc01f913c99fbba49e0bb74a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a><span data-ttu-id="167b8-103">설정에서 Azure AD으로 Windows 10 장치 설정</span><span class="sxs-lookup"><span data-stu-id="167b8-103">Set up a Windows 10 device with Azure AD from Settings</span></span>
<span data-ttu-id="167b8-104">이미 실행 중인 Windows 7 또는 Windows 8 및 컴퓨터 또는 장치를 사용 하 여 업그레이드 된 tooWindows 10 되었습니다 면 hello 설정 메뉴를 통해 Active Directory (Azure AD) tooAzure 조인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="167b8-104">If you are already using Windows 7 or Windows 8, and your computer or device has been upgraded tooWindows 10, you can join tooAzure Active Directory (Azure AD) through hello Settings menu.</span></span>

## <a name="toojoin-tooazure-ad-from-hello-settings-menu"></a><span data-ttu-id="167b8-105">hello 설정 메뉴에서 toojoin tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="167b8-105">toojoin tooAzure AD from hello Settings menu</span></span>
1. <span data-ttu-id="167b8-106">Hello에서 **시작** 메뉴 hello 클릭 **설정을** 참입니다.</span><span class="sxs-lookup"><span data-stu-id="167b8-106">From hello **Start** menu, click hello **Settings** charm.</span></span>
2. <span data-ttu-id="167b8-107">**설정**에서 **시스템**->**정보**->**Azure AD 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="167b8-107">From **Settings**, select     **System**->**About**->**Join Azure AD**.</span></span>
   
   <span data-ttu-id="167b8-108"><center>
   ![Hello 설정 메뉴에서 Azure AD 조인](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center></span><span class="sxs-lookup"><span data-stu-id="167b8-108"><center>
![Join Azure AD from hello Settings menu](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span></span>
3. <span data-ttu-id="167b8-109">클릭 **계속** hello Azure AD Join 메시지 창에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="167b8-109">Click **Continue** in hello Azure AD Join message window.</span></span>
   
   <span data-ttu-id="167b8-110"><center>
   ![Azure AD 연결 메시지 창](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span><span class="sxs-lookup"><span data-stu-id="167b8-110"><center>
![Join Azure AD message window](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span></span>
4. <span data-ttu-id="167b8-111">로그인 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="167b8-111">Provide your sign-in credentials.</span></span> <span data-ttu-id="167b8-112">이 로그인 환경을 필요한 toocomplete 인증을 모든 hello 단계가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="167b8-112">This sign-in experience will include all hello steps that are required toocomplete authentication.</span></span> <span data-ttu-id="167b8-113">페더레이션된 테 넌 트의 일부인 경우 관리자가 조직에서 호스팅하는 hello 페더레이션 experience와 함께 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b8-113">If you are part of a federated tenant, your administrator will provide you with hello federation experience that's hosted by your organization.</span></span>
   <span data-ttu-id="167b8-114"><center>
   ![로그인 자격 증명 제공](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span><span class="sxs-lookup"><span data-stu-id="167b8-114"><center>
![Provide sign-in credentials](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span></span>
5. <span data-ttu-id="167b8-115">조직에서 Azure Multi-factor Authentication tooAzure AD에 추가 하기 위해 구성한, 계속 진행 하기 전에 hello 두 번째 요소를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b8-115">If your organization has configured Azure Multi-Factor Authentication for joining tooAzure AD, provide hello second factor before proceeding.</span></span>
6. <span data-ttu-id="167b8-116">클릭 **Accept** hello에 **관리 되는이 장치 toobe 허용** 화면입니다.</span><span class="sxs-lookup"><span data-stu-id="167b8-116">Click **Accept** on hello **Allow this device toobe managed** screen.</span></span>
7. <span data-ttu-id="167b8-117">"장치는 Azure AD에서 조인 된 tooyour 조직이 이제" hello 메시지를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b8-117">You should see hello message "Your device is now joined tooyour organization in Azure AD".</span></span>

## <a name="additional-information"></a><span data-ttu-id="167b8-118">추가 정보</span><span class="sxs-lookup"><span data-stu-id="167b8-118">Additional information</span></span>
* [<span data-ttu-id="167b8-119">Azure AD 조인에 대한 사용 시나리오에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="167b8-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="167b8-120">Windows 10 환경용에 대 한 AD 도메인에 가입 된 장치 tooAzure 연결</span><span class="sxs-lookup"><span data-stu-id="167b8-120">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="167b8-121">Azure AD 조인 설정</span><span class="sxs-lookup"><span data-stu-id="167b8-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)
* [<span data-ttu-id="167b8-122">Microsoft Passport를 통해 암호 없이 ID 인증</span><span class="sxs-lookup"><span data-stu-id="167b8-122">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)

