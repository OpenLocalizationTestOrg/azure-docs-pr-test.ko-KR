---
title: "개인 장치를 조직에 조인| Microsoft Docs"
description: "사용자가 자신의 개인 Windows 10 장치를 회사 네트워크에 등록하는 방법에 대해 설명하며 BYOD 시나리오에 대한 배포 단계를 제공합니다."
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
ms.openlocfilehash: 9418365ea18b065551448742b21c8b17a1749fc8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-personal-device-to-your-organization"></a><span data-ttu-id="ce620-103">개인 장치를 조직에 조인</span><span class="sxs-lookup"><span data-stu-id="ce620-103">Join a personal device to your organization</span></span>
## <a name="to-join-a-windows-10-device-to-your-organization"></a><span data-ttu-id="ce620-104">Windows 10 장치를 조직에 조인하려면</span><span class="sxs-lookup"><span data-stu-id="ce620-104">To join a Windows 10 device to your organization</span></span>
1. <span data-ttu-id="ce620-105">**시작** 메뉴에서 **설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ce620-105">From the **Start** menu, select **Settings**.</span></span>
2. <span data-ttu-id="ce620-106">**계정**을 선택한 다음 **계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce620-106">Select **Accounts**, and then click **Your account**.</span></span>
3. <span data-ttu-id="ce620-107">**회사 또는 학교 계정 추가**를 클릭한 다음 조직 계정을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ce620-107">Click **Add Work or School account**, and then type in your organizational account.</span></span>
4. <span data-ttu-id="ce620-108">조직에 대한 로그인 페이지에서 사용자 이름 및 암호를 입력한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce620-108">On the sign-in page for your organization, enter your user name and password, and then click **OK**.</span></span>
5. <span data-ttu-id="ce620-109">다중요소 인증 시도라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce620-109">You will be prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="ce620-110">(이 문제는 IT 관리자가 구성할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="ce620-110">(This challenge is configurable by an IT administrator.)</span></span>
6. <span data-ttu-id="ce620-111">Azure Active Directory(Azure AD)에서 장치를 모바일 장치 관리에 등록해야 하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ce620-111">Azure Active Directory (Azure AD) checks whether the device requires mobile device management enrollment.</span></span>
7. <span data-ttu-id="ce620-112">Windows에서 조직의 디렉터리에 있는 장치를 Azure AD에 등록하고 해당하는 경우 모바일 장치 관리에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="ce620-112">Windows registers the device in the organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
8. <span data-ttu-id="ce620-113">관리되는 사용자인 경우 Windows에 자동 로그인되어 바탕 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce620-113">If you are a managed user, Windows takes you to the desktop through the automatic sign-in.</span></span>
9. <span data-ttu-id="ce620-114">페더레이션 사용자의 경우, Windows 로그인 화면으로 이동하고 자격 증명을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce620-114">If you are a federated user, you will be taken to a Windows sign-in screen to enter your credentials.</span></span>

## <a name="additional-information"></a><span data-ttu-id="ce620-115">추가 정보</span><span class="sxs-lookup"><span data-stu-id="ce620-115">Additional information</span></span>
* [<span data-ttu-id="ce620-116">엔터프라이즈를 위한 Windows 10: 작업에 장치를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="ce620-116">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="ce620-117">Azure Active Directory 조인을 통해 클라우드 기능을 Windows 10 장치로 확장</span><span class="sxs-lookup"><span data-stu-id="ce620-117">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="ce620-118">Microsoft Passport를 통해 암호 없이 ID 인증</span><span class="sxs-lookup"><span data-stu-id="ce620-118">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="ce620-119">Azure AD 조인에 대한 사용 시나리오에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="ce620-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="ce620-120">Windows 10 환경용 Azure AD에 도메인 가입된 장치 연결</span><span class="sxs-lookup"><span data-stu-id="ce620-120">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="ce620-121">Azure AD 조인 설정</span><span class="sxs-lookup"><span data-stu-id="ce620-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

