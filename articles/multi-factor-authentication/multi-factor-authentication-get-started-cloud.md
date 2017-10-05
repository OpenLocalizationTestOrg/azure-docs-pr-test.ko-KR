---
title: "클라우드에서 Azure MFA 시작 | Microsoft Docs"
description: "클라우드에서 Azure MFA 시작 방법을 설명하는 Microsoft Azure Multi-Factor Authentication 페이지입니다."
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
ms.openlocfilehash: 19f3228b874fc4e37bf83388dae4341428226482
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-in-the-cloud"></a><span data-ttu-id="bbbd9-103">클라우드에서 Azure Multi-Factor Authentication 시작</span><span class="sxs-lookup"><span data-stu-id="bbbd9-103">Getting started with Azure Multi-Factor Authentication in the cloud</span></span>
<span data-ttu-id="bbbd9-104">이 문서에서는 클라우드에서 Azure Multi-Factor Authentication을 사용하기 시작하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bbbd9-104">This article walks through how to get started using Azure Multi-Factor Authentication in the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="bbbd9-105">다음 문서는 **Azure 클래식 포털**사용자에 대해 사용하도록 설정하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bbbd9-105">The following documentation provides information on how to enable users using the **Azure Classic Portal**.</span></span> <span data-ttu-id="bbbd9-106">O365 사용자를 위해 Azure Multi-Factor Authentication을 설정하는 방법을 찾는 경우 [Office 365용 Multi-Factor Authentication 설정](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bbbd9-106">If you are looking for information on how to set up Azure Multi-Factor Authentication for O365 users, see [Set up multi-factor authentication for Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span></span>

![클라우드의 MFA](./media/multi-factor-authentication-get-started-cloud/mfa_in_cloud.png)

## <a name="prerequisite"></a><span data-ttu-id="bbbd9-108">필수 요소</span><span class="sxs-lookup"><span data-stu-id="bbbd9-108">Prerequisite</span></span>
<span data-ttu-id="bbbd9-109">[Azure 구독 등록](https://azure.microsoft.com/pricing/free-trial/) - 아직 Azure 구독이 없는 경우 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbbd9-109">[Sign up for an Azure subscription](https://azure.microsoft.com/pricing/free-trial/) - If you do not already have an Azure subscription, you need to sign-up for one.</span></span> <span data-ttu-id="bbbd9-110">Azure MFA를 시작하고 사용하려면 평가판 구독을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbbd9-110">If you are just starting out and using Azure MFA you can use a trial subscription</span></span>

## <a name="enable-azure-multi-factor-authentication"></a><span data-ttu-id="bbbd9-111">Azure Multi-Factor Authentication 사용</span><span class="sxs-lookup"><span data-stu-id="bbbd9-111">Enable Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="bbbd9-112">사용자가 Azure Multi-Factor Authentication을 포함하는 라이선스를 가지고 있는 한 Azure MFA를 설정하도록 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bbbd9-112">As long as your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need to do to turn on Azure MFA.</span></span> <span data-ttu-id="bbbd9-113">개별 사용자 단위로 2단계 인증 요구를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbbd9-113">You can start requiring two-step verification on an individual user basis.</span></span> <span data-ttu-id="bbbd9-114">Azure MFA를 활성화하는 라이선스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bbbd9-114">The licenses that enable Azure MFA are:</span></span>
- <span data-ttu-id="bbbd9-115">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="bbbd9-115">Azure Multi-Factor Authentication</span></span>
- <span data-ttu-id="bbbd9-116">Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="bbbd9-116">Azure Active Directory Premium</span></span>
- <span data-ttu-id="bbbd9-117">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="bbbd9-117">Enterprise Mobility + Security</span></span>

<span data-ttu-id="bbbd9-118">이러한 세 가지 라이선스 중 하나가 없거나 모든 사용자를 포함할 충분한 라이선스가 없는 경우에도 괜찮습니다.</span><span class="sxs-lookup"><span data-stu-id="bbbd9-118">If you don't have one of these three licenses, or you don't have enough licenses to cover all of your users, that's ok too.</span></span> <span data-ttu-id="bbbd9-119">별도 단계를 수행하고 디렉터리에 [Multi-Factor Auth 공급자를 만들](multi-factor-authentication-get-started-auth-provider.md)어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbbd9-119">You just have to do an extra step and [Create a Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md) in your directory.</span></span>

## <a name="turn-on-two-step-verification-for-users"></a><span data-ttu-id="bbbd9-120">사용자에 대한 2단계 확인을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bbbd9-120">Turn on two-step verification for users</span></span>

<span data-ttu-id="bbbd9-121">[사용자 또는 그룹에 대해 2단계 인증을 요구하는 방법](multi-factor-authentication-get-started-user-states.md)에 나열된 절차 중 하나를 사용하여 Azure MFA를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bbbd9-121">Use one of the procedures listed in [How to require two-step verification for a user or group](multi-factor-authentication-get-started-user-states.md) to start using Azure MFA.</span></span> <span data-ttu-id="bbbd9-122">모든 로그인에 대해 2단계 인증을 적용하거나 문제가 될 때만 2단계 인증을 요구하는 조건부 액세스 정책을 만들도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbbd9-122">You can choose to enforce two-step verification for all sign-ins, or you can create conditional access policies to require two-step verification only when it matters to you.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbbd9-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bbbd9-123">Next Steps</span></span>
<span data-ttu-id="bbbd9-124">클라우드에서 Azure Multi-Factor Authentication을 설정했으므로 배포를 구성 및 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbbd9-124">Now that you have set up Azure Multi-Factor Authentication in the cloud, you can configure and set up your deployment.</span></span> <span data-ttu-id="bbbd9-125">자세한 내용은 [Azure Multi-Factor Authentication 구성](multi-factor-authentication-whats-next.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bbbd9-125">See [Configuring Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) for more details.</span></span>

