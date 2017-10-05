---
title: "문제 해결: 'Active Directory' 항목이 없거나 사용할 수 없는 | Microsoft Docs"
description: "Azure 관리 포털에 Active Directory 메뉴 항목이 표시되지 않을 경우 수행할 작업입니다."
services: active-directory
documentationcenter: na
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 3383020d-6397-43ea-b7aa-c6a9d6a1e3df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.openlocfilehash: be3a797c4a405fd2f6636e67f4c961dd6d143486
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a><span data-ttu-id="96d64-103">문제 해결: 'Active Directory' 항목이 없거나 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="96d64-103">Troubleshooting: 'Active Directory' item is missing or not available</span></span>
<span data-ttu-id="96d64-104">Azure Active Directory 기능 및 서비스 사용에 대한 지침은 대부분 "Azure 관리 포털로 이동한 다음 **Active Directory**를 클릭합니다."로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="96d64-104">Many of the instructions for using Azure Active Directory features and services begin with "Go to the Azure Management Portal and click **Active Directory**."</span></span> <span data-ttu-id="96d64-105">하지만 Active Directory 확장 또는 메뉴 항목이 표시되지 않거나 **사용할 수 없음**으로 표시되는 경우 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="96d64-105">But what do you do if the Active Directory extension or menu item does not appear or if it is marked **Not Available**?</span></span> <span data-ttu-id="96d64-106">이 항목은 도움을 주기 위해 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="96d64-106">This topic is designed to help.</span></span> <span data-ttu-id="96d64-107">**Active Directory** 가 표시되지 않거나 사용할 수 없는 조건 및 계속 진행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="96d64-107">It describes the conditions under which **Active Directory** does not appear or is unavailable and explains how to proceed.</span></span>

## <a name="active-directory-is-missing"></a><span data-ttu-id="96d64-108">Active Directory가 없음</span><span class="sxs-lookup"><span data-stu-id="96d64-108">Active Directory is missing</span></span>
<span data-ttu-id="96d64-109">일반적으로 **Active Directory** 항목은 왼쪽 탐색 메뉴에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="96d64-109">Typically, an **Active Directory** item appears in the left navigation menu.</span></span> <span data-ttu-id="96d64-110">Azure Active Directory 절차의 지침에서는 이 항목이 표시된다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="96d64-110">The instructions in Azure Active Directory procedures assume that this item is in your view.</span></span>

![스크린샷: Azure의 Active Directory](./media/active-directory-troubleshooting/typical-view.png)

<span data-ttu-id="96d64-112">다음 조건 중 하나라도 true이면 Active Directory 항목이 왼쪽 탐색 메뉴에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="96d64-112">The Active Directory item appears in the left navigation menu when any of the following conditions is true.</span></span> <span data-ttu-id="96d64-113">그렇지 않으면 항목이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96d64-113">Otherwise, the item does not appear.</span></span>

* <span data-ttu-id="96d64-114">현재 사용자가 Microsoft 계정(이전의 Windows Live ID)을 사용하여 로그온했습니다.</span><span class="sxs-lookup"><span data-stu-id="96d64-114">The current user signed on with a Microsoft account (formerly known as a Windows Live ID).</span></span>
  
    <span data-ttu-id="96d64-115">또는</span><span class="sxs-lookup"><span data-stu-id="96d64-115">OR</span></span>
* <span data-ttu-id="96d64-116">Azure 테넌트에 디렉터리가 있고 현재 계정이 디렉터리 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="96d64-116">The Azure tenant has a directory and the current account is a directory administrator.</span></span>
  
    <span data-ttu-id="96d64-117">또는</span><span class="sxs-lookup"><span data-stu-id="96d64-117">OR</span></span>
* <span data-ttu-id="96d64-118">Azure 테넌트에 ACS(Azure AD 액세스 제어) 네임스페이스가 하나 이상 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96d64-118">The Azure tenant has at least one Azure AD Access Control (ACS) namespace.</span></span> <span data-ttu-id="96d64-119">자세한 내용은 [액세스 제어 네임스페이스](https://msdn.microsoft.com/library/azure/gg185908.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="96d64-119">For more information, see [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span></span>
  
    <span data-ttu-id="96d64-120">또는</span><span class="sxs-lookup"><span data-stu-id="96d64-120">OR</span></span>
* <span data-ttu-id="96d64-121">Azure 테넌트에 Azure Multi-Factor Authentication 공급자가 하나 이상 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96d64-121">The Azure tenant has at least one Azure Multi-Factor Authentication provider.</span></span> <span data-ttu-id="96d64-122">자세한 내용은 [Azure Multi-Factor Authentication 공급자 관리](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="96d64-122">For more information, see [Administering Azure Multi-Factor Authentication Providers](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>

<span data-ttu-id="96d64-123">액세스 제어 네임스페이스 또는 Multi-Factor Authentication 공급자를 만들려면 **+새로 만들기** > **App Services** > **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96d64-123">To create an Access Control namespace or a Multi-Factor Authentication provider, click **+New** > **App Services** > **Active Directory**.</span></span>

<span data-ttu-id="96d64-124">디렉터리에 대한 관리자 권한을 얻으려면 관리자가 계정에 관리자 역할을 할당하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="96d64-124">To get administrative rights to a directory, have an administrator assign an administrator role to your account.</span></span> <span data-ttu-id="96d64-125">자세한 내용은 [관리자 역할 할당](active-directory-assign-admin-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="96d64-125">For details, see [Assigning administrator roles](active-directory-assign-admin-roles.md).</span></span>

## <a name="active-directory-is-not-available"></a><span data-ttu-id="96d64-126">Active Directory를 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="96d64-126">Active Directory is not available</span></span>
<span data-ttu-id="96d64-127">**+새로 만들기** > **App Services**를 클릭하면 **Active Directory** 항목이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="96d64-127">When you click **+New** > **App Services**, an **Active Directory** item appears.</span></span> <span data-ttu-id="96d64-128">특히, Active Directory 항목은 현재 사용자가 디렉터리, 액세스 제어 또는 Multi-Factor Authentication 공급자와 같은 Active Directory 기능을 모두 사용할 수 있을 때 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="96d64-128">Specifically, the Active Directory item appears when any of the Active Directory features, such as Directory, Access Control, or Multi-Factor Auth Provider, are available to the current user.</span></span>

<span data-ttu-id="96d64-129">그러나 페이지가 로드되는 동안에는 항목이 흐리게 표시되며 **사용할 수 없음**으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="96d64-129">However, while the page is loading, the item is dimmed and is marked **Not Available**.</span></span> <span data-ttu-id="96d64-130">이는 임시 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="96d64-130">This is a temporary state.</span></span> <span data-ttu-id="96d64-131">몇 초간 기다리면 항목을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96d64-131">If you wait a few seconds, the item becomes available.</span></span> <span data-ttu-id="96d64-132">지연이 길어질 경우 웹 페이지를 새로 고치면 문제가 해결되는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="96d64-132">If the delay is prolonged, refreshing the web page often resolves the problem.</span></span>

![스크린샷: Active Directory를 사용할 수 없음](./media/active-directory-troubleshooting/not-available.png)

