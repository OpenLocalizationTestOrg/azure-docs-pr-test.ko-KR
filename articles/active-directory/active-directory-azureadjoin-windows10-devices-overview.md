---
title: "엔터프라이즈를 위한 Windows 10: 작업에 장치를 사용하는 방법 | Microsoft Docs"
description: "기업용 Windows 10 장치 배포 및 Windows 클라우드용 Azure Active Directory와 통합하는 방법에 대한 개요 장치를 프로비전하고 Azure 포털을 통해 기업에서 사용할 수 있는 다양한 방법을 비교합니다."
keywords: "windows 클라우드, Azure Active Directory에서 Windows, Azure에서 Windows 10 장치, Azure Windows 장치"
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2cb9ab6a-55b6-4658-b7f2-6e05ae015e1b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 804156048a7596f9937098e6fe762f424526473c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-10-for-the-enterprise-ways-to-use-devices-for-work"></a><span data-ttu-id="40070-105">엔터프라이즈를 위한 Windows 10: 작업에 장치를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="40070-105">Windows 10 for the enterprise: Ways to use devices for work</span></span>
<span data-ttu-id="40070-106">Windows 10은 Azure Active Directory를 활용할 수 있는 기능을 제공합니다(Azure AD).</span><span class="sxs-lookup"><span data-stu-id="40070-106">Windows 10 gives you the ability to leverage Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="40070-107">Windows 10 장치를 Azure AD에 연결할 수 있어 사용자는 비즈니스 앱 및 리소스에 대한 액세스 권한을 얻기 위해 Azure AD 계정을 사용하거나 Azure ID를 추가하여 Windows에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40070-107">You can connect Windows 10 devices to Azure AD so that users can sign in to Windows by using Azure AD accounts or by adding their Azure IDs to gain access to business apps and resources.</span></span>

![Azure Active Directory 및 Windows Cloud](./media/active-directory-azureadjoin/windows10-overview.png)

## <a name="integrating-windows-10-devices-with-azure-active-directory--a-content-map"></a><span data-ttu-id="40070-109">Windows 10 장치와 Azure Active Directory 통합 - 콘텐츠 맵</span><span class="sxs-lookup"><span data-stu-id="40070-109">Integrating Windows 10 devices with Azure Active Directory--a content map</span></span>
<span data-ttu-id="40070-110">다음 항목에서는 조직에서 Windows 10 장치를 활용하는 다양한 기능에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="40070-110">The following topics provide insights into different capabilities of Windows 10 devices in your organization.</span></span>

|  | <span data-ttu-id="40070-111">토픽</span><span class="sxs-lookup"><span data-stu-id="40070-111">Topics</span></span> |
| --- | --- |
| <span data-ttu-id="40070-112">시작</span><span class="sxs-lookup"><span data-stu-id="40070-112">Getting started</span></span> |[<span data-ttu-id="40070-113">작업 공간에서 Windows 10 장치 사용</span><span class="sxs-lookup"><span data-stu-id="40070-113">Using Windows 10 devices in your workplace</span></span>](active-directory-azureadjoin-windows10-devices.md) <br> <br> [<span data-ttu-id="40070-114">Azure Active Directory 조인을 통해 클라우드 기능을 Windows 10 장치로 확장</span><span class="sxs-lookup"><span data-stu-id="40070-114">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-overview.md) <br> <br> [<span data-ttu-id="40070-115">Microsoft Passport를 통해 암호 없이 ID 인증</span><span class="sxs-lookup"><span data-stu-id="40070-115">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md) |
| <span data-ttu-id="40070-116">배포</span><span class="sxs-lookup"><span data-stu-id="40070-116">Deployment</span></span> |[<span data-ttu-id="40070-117">Azure AD 연결에 대한 사용 시나리오와 배포 고려 사항</span><span class="sxs-lookup"><span data-stu-id="40070-117">Usage scenarios and deployment considerations for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md) <br><br> [<span data-ttu-id="40070-118">Windows 10 환경용 Azure AD에 도메인 가입된 장치 연결</span><span class="sxs-lookup"><span data-stu-id="40070-118">Connecting domain-joined devices to Azure AD, for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)<br><br>[<span data-ttu-id="40070-119">조직에서 Microsoft Passport for Work 사용</span><span class="sxs-lookup"><span data-stu-id="40070-119">Enabling Microsoft Passport for work in the organization</span></span>](active-directory-azureadjoin-passport-deployment.md)<br><br> [<span data-ttu-id="40070-120">Windows 10용 엔터프라이즈 상태 로밍 사용</span><span class="sxs-lookup"><span data-stu-id="40070-120">Enabling Enterprise State Roaming for Windows 10</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)<br><br> |
| <span data-ttu-id="40070-121">사용자 작업</span><span class="sxs-lookup"><span data-stu-id="40070-121">User tasks</span></span> |[<span data-ttu-id="40070-122">설치하는 동안 Azure AD로 새 Windows 10 장치 설정</span><span class="sxs-lookup"><span data-stu-id="40070-122">Setting up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md) <br><br> [<span data-ttu-id="40070-123">설정 메뉴에서 Azure AD로 Windows 10 장치 설정</span><span class="sxs-lookup"><span data-stu-id="40070-123">Setting up a Windows 10 device with Azure AD from the settings menu</span></span>](active-directory-azureadjoin-user-upgrade.md) <br><br> [<span data-ttu-id="40070-124">개인 Windows 10 장치를 조직에 조인</span><span class="sxs-lookup"><span data-stu-id="40070-124">Joining a personal Windows 10 device to your organization</span></span>](active-directory-azureadjoin-personal-device.md) |

