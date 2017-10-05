---
title: "Azure AD Connect: 미리 보기의 기능 | Microsoft Docs"
description: "이 항목에서는 Azure AD Connect에서 미리 보기 상태인 기능을 더 자세하게 설명합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: cbf8f729d0ebfb271bb0d8702ac043442b42c262
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="more-details-about-features-in-preview"></a><span data-ttu-id="cff2c-103">미리 보기 기능에 대한 자세한 내용</span><span class="sxs-lookup"><span data-stu-id="cff2c-103">More details about features in preview</span></span>
<span data-ttu-id="cff2c-104">이 항목에서는 현재 미리 보기 상태인 기능을 사용하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cff2c-104">This topic describes how to use features currently in preview.</span></span>

## <a name="group-writeback"></a><span data-ttu-id="cff2c-105">그룹 쓰기 저장</span><span class="sxs-lookup"><span data-stu-id="cff2c-105">Group writeback</span></span>
<span data-ttu-id="cff2c-106">선택적 기능의 그룹 쓰기 저장에 대한 옵션을 사용하면 Exchange가 설치된 포리스트로 **Office 365 그룹** 을 쓰기 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff2c-106">The option for group writeback in optional features allows you to writeback **Office 365 Groups** to a forest with Exchange installed.</span></span> <span data-ttu-id="cff2c-107">항상 클라우드에서 마스터되는 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="cff2c-107">This is a group that is always mastered in the cloud.</span></span> <span data-ttu-id="cff2c-108">Exchange 온-프레미스가 있는 경우 이러한 그룹을 온-프레미스에 쓰기 저장하여 온-프레미스 Exchange 사서함이 있는 사용자가 이 그룹에서 메일을 보내고 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff2c-108">If you have Exchange on-premises, then you can write back these groups to on-premises so users with an on-premises Exchange mailbox can send and receive emails from these groups.</span></span>

<span data-ttu-id="cff2c-109">Office 365 그룹에 대한 자세한 내용 및 사용 방법은 [여기](http://aka.ms/O365g)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff2c-109">More information about Office 365 Groups and how to use them can be found [here](http://aka.ms/O365g).</span></span>

<span data-ttu-id="cff2c-110">Office 365 그룹은 온-프레미스 AD DS에서 배포 그룹으로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff2c-110">An Office 365 group is represented as a distribution group in on-premises AD DS.</span></span> <span data-ttu-id="cff2c-111">이 새 그룹 유형을 인식하려면 온-프레미스 Exchange 서버는 Exchange 2013 누적 업데이트 8(2015년 3월에 릴리스됨) 또는 Exchange 2016이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff2c-111">Your on-premises Exchange server must be on Exchange 2013 cumulative update 8 (released in March 2015) or Exchange 2016 to recognize this new group type.</span></span>

<span data-ttu-id="cff2c-112">**미리 보기 중 참고**</span><span class="sxs-lookup"><span data-stu-id="cff2c-112">**Notes during the preview**</span></span>

* <span data-ttu-id="cff2c-113">미리 보기에서 현재 주소록 특성이 채워지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cff2c-113">The address book attribute is currently not populated in the preview.</span></span> <span data-ttu-id="cff2c-114">이 특성이 없으면 그룹이 GAL에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cff2c-114">Without this attribute, the group is not visible in the GAL.</span></span> <span data-ttu-id="cff2c-115">이 특성을 채우는 가장 쉬운 방법은 Exchange PowerShell cmdlet `update-recipient`를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cff2c-115">The easiest way to populate this attribute is to use the Exchange PowerShell cmdlet `update-recipient`.</span></span>
* <span data-ttu-id="cff2c-116">Exchange 스키마가 있는 포리스트만 그룹에 대한 유효한 대상이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff2c-116">Only forests with the Exchange schema are valid targets for groups.</span></span> <span data-ttu-id="cff2c-117">검색된 Exchange가 없는 경우, 그룹 쓰기 저장을 사용하도록 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cff2c-117">If no Exchange was detected, then group writeback is not possible to enable.</span></span>
* <span data-ttu-id="cff2c-118">현재 단일 포리스트 Exchange 조직 배포만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cff2c-118">Only single-forest Exchange organization deployments are currently supported.</span></span> <span data-ttu-id="cff2c-119">둘 이상의 Exchange 조직 온-프레미스가 있는 경우 이러한 그룹을 다른 포리스트에 표시하려면 온-프레미스 GALSync 솔루션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cff2c-119">If you have more than one Exchange organization on-premises, then you need an on-premises GALSync solution for these groups to appear in your other forests.</span></span>
* <span data-ttu-id="cff2c-120">그룹 쓰기 저장 기능은 보안 그룹 또는 배포 그룹을 처리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cff2c-120">The Group writeback feature does not handle security groups or distribution groups.</span></span>

> [!NOTE]
> <span data-ttu-id="cff2c-121">Azure AD Premium에 대한 구독은 그룹 쓰기 저장에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cff2c-121">A subscription to Azure AD Premium is required for group writeback.</span></span>
> 
>

## <a name="user-writeback"></a><span data-ttu-id="cff2c-122">사용자 쓰기 저장</span><span class="sxs-lookup"><span data-stu-id="cff2c-122">User writeback</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cff2c-123">사용자 쓰기 저장 미리 보기 기능은 Azure AD Connect 2015년 8월 업데이트에서 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cff2c-123">The user writeback preview feature was removed in the August 2015 update to Azure AD Connect.</span></span> <span data-ttu-id="cff2c-124">이 기능을 사용하도록 설정한 경우 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff2c-124">If you have enabled it, then you should disable this feature.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="cff2c-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cff2c-125">Next steps</span></span>
<span data-ttu-id="cff2c-126">[Azure AD Connect의 사용자 지정 설치](active-directory-aadconnect-get-started-custom.md)를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="cff2c-126">Continue your [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span></span>

<span data-ttu-id="cff2c-127">[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cff2c-127">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
