---
title: "aaaGet hello 클라우드에서 Azure MFA를 시작 | Microsoft Docs"
description: "Hello tooget hello 클라우드에서 Azure MFA를 시작 하는 방법을 설명 하는 Microsoft Azure Multi-factor authentication 페이지입니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 6b2e6549-1a26-4666-9c4a-cbe5d64c4e66
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/24/2017
ms.author: kgremban
ms.openlocfilehash: a4aaf44bf08d96f2baad155072fdd6e0e727ce8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-in-hello-cloud"></a><span data-ttu-id="f7204-103">Hello 클라우드에서 Azure Multi-factor Authentication 시작</span><span class="sxs-lookup"><span data-stu-id="f7204-103">Getting started with Azure Multi-Factor Authentication in hello cloud</span></span>
<span data-ttu-id="f7204-104">이 문서는 hello 클라우드에서 Azure Multi-factor Authentication을 사용 하 여 tooget을 시작 하는 방법을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7204-104">This article walks through how tooget started using Azure Multi-Factor Authentication in hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="f7204-105">hello 다음 문서에 정보를 제공 방법을 사용 하 여 tooenable 사용자 hello **Azure 클래식 포털**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7204-105">hello following documentation provides information on how tooenable users using hello **Azure Classic Portal**.</span></span> <span data-ttu-id="f7204-106">원하는 방법에 대 한 경우 O365 사용자에 대 한 Azure 다단계 인증을 tooset 참조 [Office 365에 대 한 다단계 인증을 설정 합니다.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span><span class="sxs-lookup"><span data-stu-id="f7204-106">If you are looking for information on how tooset up Azure Multi-Factor Authentication for O365 users, see [Set up multi-factor authentication for Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span></span>

![Hello 클라우드에서 MFA](./media/multi-factor-authentication-get-started-cloud/mfa_in_cloud.png)

## <a name="prerequisite"></a><span data-ttu-id="f7204-108">필수 요소</span><span class="sxs-lookup"><span data-stu-id="f7204-108">Prerequisite</span></span>
<span data-ttu-id="f7204-109">[Azure 구독에 등록](https://azure.microsoft.com/pricing/free-trial/) -하나에 대 한 toosign 접속 해야 Azure 구독이 아직 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="f7204-109">[Sign up for an Azure subscription](https://azure.microsoft.com/pricing/free-trial/) - If you do not already have an Azure subscription, you need toosign-up for one.</span></span> <span data-ttu-id="f7204-110">Azure MFA를 시작하고 사용하려면 평가판 구독을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7204-110">If you are just starting out and using Azure MFA you can use a trial subscription</span></span>

## <a name="enable-azure-multi-factor-authentication"></a><span data-ttu-id="f7204-111">Azure Multi-Factor Authentication 사용</span><span class="sxs-lookup"><span data-stu-id="f7204-111">Enable Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="f7204-112">Azure Multi-factor Authentication을 포함 하는 라이선스를 보유 하는 사용자가 toodo tooturn Azure MFA에 할 일은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f7204-112">As long as your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need toodo tooturn on Azure MFA.</span></span> <span data-ttu-id="f7204-113">개별 사용자 단위로 2단계 인증 요구를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7204-113">You can start requiring two-step verification on an individual user basis.</span></span> <span data-ttu-id="f7204-114">Azure MFA를 사용 하는 hello 라이선스는:</span><span class="sxs-lookup"><span data-stu-id="f7204-114">hello licenses that enable Azure MFA are:</span></span>
- <span data-ttu-id="f7204-115">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="f7204-115">Azure Multi-Factor Authentication</span></span>
- <span data-ttu-id="f7204-116">Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="f7204-116">Azure Active Directory Premium</span></span>
- <span data-ttu-id="f7204-117">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="f7204-117">Enterprise Mobility + Security</span></span>

<span data-ttu-id="f7204-118">다음 세 개의 라이선스 중 하나가 없거나 충분 한 라이선스 toocover 없는 경우 모든 사용자의 너무 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7204-118">If you don't have one of these three licenses, or you don't have enough licenses toocover all of your users, that's ok too.</span></span> <span data-ttu-id="f7204-119">하기만 하면 toodo 별도 단계 및 [Multi-factor Auth 공급자를 만듭니다](multi-factor-authentication-get-started-auth-provider.md) 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7204-119">You just have toodo an extra step and [Create a Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md) in your directory.</span></span>

## <a name="turn-on-two-step-verification-for-users"></a><span data-ttu-id="f7204-120">사용자에 대한 2단계 확인을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7204-120">Turn on two-step verification for users</span></span>

<span data-ttu-id="f7204-121">에 나열 된 hello 절차 중 하나를 사용 하 여 [어떻게 사용자 또는 그룹에 대 한 2 단계 인증 toorequire](multi-factor-authentication-get-started-user-states.md) toostart Azure MFA를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7204-121">Use one of hello procedures listed in [How toorequire two-step verification for a user or group](multi-factor-authentication-get-started-user-states.md) toostart using Azure MFA.</span></span> <span data-ttu-id="f7204-122">로그인을 위한 모든, tooenforce 2 단계 인증을 선택할 수 있습니다 또는 tooyou 중요 한 경우에 조건부 액세스 정책을 toorequire 2 단계 인증을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7204-122">You can choose tooenforce two-step verification for all sign-ins, or you can create conditional access policies toorequire two-step verification only when it matters tooyou.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7204-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f7204-123">Next Steps</span></span>
<span data-ttu-id="f7204-124">이제를 hello 클라우드에서 Azure Multi-factor Authentication을 설정한, 구성 및 배포 설정 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7204-124">Now that you have set up Azure Multi-Factor Authentication in hello cloud, you can configure and set up your deployment.</span></span> <span data-ttu-id="f7204-125">자세한 내용은 [Azure Multi-Factor Authentication 구성](multi-factor-authentication-whats-next.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7204-125">See [Configuring Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) for more details.</span></span>

