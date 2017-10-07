---
title: "개인 장치 tooyour 조직 aaaJoin | Microsoft Docs"
description: "사용자가 자신의 개인 Windows 10 장치 tootheir 회사 네트워크를 등록할 수는 방법에 대해 설명 하 고 BYOD 시나리오에 대 한 배포 단계를 제공 합니다."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 9f3d38f5-1cfd-43d4-97da-4fed1255a1ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 979e2461dd9ad0438aa402a0a3223cc84c4c625c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-personal-device-tooyour-organization"></a><span data-ttu-id="63dff-103">개인 장치 tooyour 조직 참가</span><span class="sxs-lookup"><span data-stu-id="63dff-103">Join a personal device tooyour organization</span></span>
## <a name="toojoin-a-windows-10-device-tooyour-organization"></a><span data-ttu-id="63dff-104">toojoin Windows 10 장치 tooyour 조직</span><span class="sxs-lookup"><span data-stu-id="63dff-104">toojoin a Windows 10 device tooyour organization</span></span>
1. <span data-ttu-id="63dff-105">Hello에서 **시작** 메뉴 선택 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="63dff-105">From hello **Start** menu, select **Settings**.</span></span>
2. <span data-ttu-id="63dff-106">**계정**을 선택한 다음 **계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63dff-106">Select **Accounts**, and then click **Your account**.</span></span>
3. <span data-ttu-id="63dff-107">**회사 또는 학교 계정 추가**를 클릭한 다음 조직 계정을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="63dff-107">Click **Add Work or School account**, and then type in your organizational account.</span></span>
4. <span data-ttu-id="63dff-108">Hello 로그인 페이지에서 조직에 대 한 사용자 이름 및 암호를 입력 한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="63dff-108">On hello sign-in page for your organization, enter your user name and password, and then click **OK**.</span></span>
5. <span data-ttu-id="63dff-109">다중요소 인증 시도라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="63dff-109">You will be prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="63dff-110">(이 문제는 IT 관리자가 구성할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="63dff-110">(This challenge is configurable by an IT administrator.)</span></span>
6. <span data-ttu-id="63dff-111">Azure Active Directory (Azure AD) hello 장치 모바일 장치 관리 등록 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="63dff-111">Azure Active Directory (Azure AD) checks whether hello device requires mobile device management enrollment.</span></span>
7. <span data-ttu-id="63dff-112">Windows Azure AD에서 hello 조직의 디렉터리에서 hello 장치를 등록 하 고 해당 하는 경우 모바일 장치 관리에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="63dff-112">Windows registers hello device in hello organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
8. <span data-ttu-id="63dff-113">관리 되는 사용자 인 경우 Windows hello 자동 로그인 통해 toohello 데스크톱을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="63dff-113">If you are a managed user, Windows takes you toohello desktop through hello automatic sign-in.</span></span>
9. <span data-ttu-id="63dff-114">페더레이션된 사용자 인 경우 됩니다 화면 tooenter tooa Windows 로그인 자격 증명을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="63dff-114">If you are a federated user, you will be taken tooa Windows sign-in screen tooenter your credentials.</span></span>

## <a name="additional-information"></a><span data-ttu-id="63dff-115">추가 정보</span><span class="sxs-lookup"><span data-stu-id="63dff-115">Additional information</span></span>
* [<span data-ttu-id="63dff-116">Hello 엔터프라이즈용 Windows 10: 작업에 대 한 방법으로 toouse 장치</span><span class="sxs-lookup"><span data-stu-id="63dff-116">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="63dff-117">Azure Active Directory Join을 통해 기능 10 tooWindows 장치 클라우드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="63dff-117">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="63dff-118">Microsoft Passport를 통해 암호 없이 ID 인증</span><span class="sxs-lookup"><span data-stu-id="63dff-118">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="63dff-119">Azure AD 조인에 대한 사용 시나리오에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="63dff-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="63dff-120">Windows 10 환경용에 대 한 AD 도메인에 가입 된 장치 tooAzure 연결</span><span class="sxs-lookup"><span data-stu-id="63dff-120">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="63dff-121">Azure AD 조인 설정</span><span class="sxs-lookup"><span data-stu-id="63dff-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

