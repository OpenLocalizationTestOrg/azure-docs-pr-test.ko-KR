---
title: "문제 해결: 'Active Directory' 항목이 없거나 사용할 수 없는 | Microsoft Docs"
description: "Active Directory 메뉴 항목이 hello Azure 관리 포털에에서 나타나지 않는 경우 어떤 toodo 합니다."
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
ms.openlocfilehash: d7355a4e39141f0b09272dc5615c309b23c8c70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a><span data-ttu-id="14e0c-103">문제 해결: 'Active Directory' 항목이 없거나 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="14e0c-103">Troubleshooting: 'Active Directory' item is missing or not available</span></span>
<span data-ttu-id="14e0c-104">로 시작 하는 다양 한 Azure Active Directory 기능 및 서비스를 사용 하 여 hello 지침은 "toohello Azure 관리 포털을 이동 하 고 클릭 **Active Directory**."</span><span class="sxs-lookup"><span data-stu-id="14e0c-104">Many of hello instructions for using Azure Active Directory features and services begin with "Go toohello Azure Management Portal and click **Active Directory**."</span></span> <span data-ttu-id="14e0c-105">???????????? Hello Active Directory 확장 프로그램이 나 메뉴 항목이 표시 되지 않으면 또는 표시 되는 경우 하지만 **사용할 수 없는**?</span><span class="sxs-lookup"><span data-stu-id="14e0c-105">But what do you do if hello Active Directory extension or menu item does not appear or if it is marked **Not Available**?</span></span> <span data-ttu-id="14e0c-106">이 항목은 설계 된 toohelp입니다.</span><span class="sxs-lookup"><span data-stu-id="14e0c-106">This topic is designed toohelp.</span></span> <span data-ttu-id="14e0c-107">Hello 기준을 설명 **Active Directory** 나타나지 않으면 또는 사용할 수 없게 되며 설명 어떻게 tooproceed 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e0c-107">It describes hello conditions under which **Active Directory** does not appear or is unavailable and explains how tooproceed.</span></span>

## <a name="active-directory-is-missing"></a><span data-ttu-id="14e0c-108">Active Directory가 없음</span><span class="sxs-lookup"><span data-stu-id="14e0c-108">Active Directory is missing</span></span>
<span data-ttu-id="14e0c-109">일반적으로 **Active Directory** hello 왼쪽된 탐색 메뉴에 항목이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14e0c-109">Typically, an **Active Directory** item appears in hello left navigation menu.</span></span> <span data-ttu-id="14e0c-110">Azure Active Directory 절차의 지침에 hello이이 항목이 보기에 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e0c-110">hello instructions in Azure Active Directory procedures assume that this item is in your view.</span></span>

![스크린샷: Azure의 Active Directory](./media/active-directory-troubleshooting/typical-view.png)

<span data-ttu-id="14e0c-112">hello 다음 조건 중 하나에 hello Active Directory 항목이 hello 왼쪽된 탐색 메뉴에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="14e0c-112">hello Active Directory item appears in hello left navigation menu when any of hello following conditions is true.</span></span> <span data-ttu-id="14e0c-113">그렇지 않으면 hello 항목이 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="14e0c-113">Otherwise, hello item does not appear.</span></span>

* <span data-ttu-id="14e0c-114">hello 현재 사용자 (이전의 Windows Live ID)는 Microsoft 계정으로 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e0c-114">hello current user signed on with a Microsoft account (formerly known as a Windows Live ID).</span></span>
  
    <span data-ttu-id="14e0c-115">또는</span><span class="sxs-lookup"><span data-stu-id="14e0c-115">OR</span></span>
* <span data-ttu-id="14e0c-116">hello Azure 테 넌 트에 디렉터리가 및 hello 현재 계정이 디렉터리 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="14e0c-116">hello Azure tenant has a directory and hello current account is a directory administrator.</span></span>
  
    <span data-ttu-id="14e0c-117">또는</span><span class="sxs-lookup"><span data-stu-id="14e0c-117">OR</span></span>
* <span data-ttu-id="14e0c-118">hello Azure 테 넌 트에 하나 이상의 Azure AD 액세스 제어 (ACS) 네임 스페이스를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14e0c-118">hello Azure tenant has at least one Azure AD Access Control (ACS) namespace.</span></span> <span data-ttu-id="14e0c-119">자세한 내용은 [액세스 제어 네임스페이스](https://msdn.microsoft.com/library/azure/gg185908.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14e0c-119">For more information, see [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span></span>
  
    <span data-ttu-id="14e0c-120">또는</span><span class="sxs-lookup"><span data-stu-id="14e0c-120">OR</span></span>
* <span data-ttu-id="14e0c-121">hello Azure 테 넌 트에 Azure Multi-factor Authentication 공급자를 하나 이상 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14e0c-121">hello Azure tenant has at least one Azure Multi-Factor Authentication provider.</span></span> <span data-ttu-id="14e0c-122">자세한 내용은 [Azure Multi-Factor Authentication 공급자 관리](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14e0c-122">For more information, see [Administering Azure Multi-Factor Authentication Providers](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>

<span data-ttu-id="14e0c-123">toocreate는 액세스 제어 네임 스페이스 또는 Multi-factor Authentication 공급자를 클릭 **+ 새로 만들기** > **응용 프로그램 서비스** > **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="14e0c-123">toocreate an Access Control namespace or a Multi-Factor Authentication provider, click **+New** > **App Services** > **Active Directory**.</span></span>

<span data-ttu-id="14e0c-124">tooget 관리 권한을 tooa 디렉터리는 관리자가 관리자 역할 tooyour 계정을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e0c-124">tooget administrative rights tooa directory, have an administrator assign an administrator role tooyour account.</span></span> <span data-ttu-id="14e0c-125">자세한 내용은 [관리자 역할 할당](active-directory-assign-admin-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14e0c-125">For details, see [Assigning administrator roles](active-directory-assign-admin-roles.md).</span></span>

## <a name="active-directory-is-not-available"></a><span data-ttu-id="14e0c-126">Active Directory를 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="14e0c-126">Active Directory is not available</span></span>
<span data-ttu-id="14e0c-127">**+새로 만들기** > **App Services**를 클릭하면 **Active Directory** 항목이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="14e0c-127">When you click **+New** > **App Services**, an **Active Directory** item appears.</span></span> <span data-ttu-id="14e0c-128">특히 hello Active Directory 항목에는 사용할 수 있는 toohello 현재 사용자 디렉터리, 액세스 제어, Multi-factor Auth 공급자 등의 hello Active Directory 기능을 모두 있을 때 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="14e0c-128">Specifically, hello Active Directory item appears when any of hello Active Directory features, such as Directory, Access Control, or Multi-Factor Auth Provider, are available toohello current user.</span></span>

<span data-ttu-id="14e0c-129">그러나 hello 페이지 로드 하는 동안 hello 항목 흐리게 표시 되 고 표시 된 **사용할 수 없는**합니다.</span><span class="sxs-lookup"><span data-stu-id="14e0c-129">However, while hello page is loading, hello item is dimmed and is marked **Not Available**.</span></span> <span data-ttu-id="14e0c-130">이는 임시 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="14e0c-130">This is a temporary state.</span></span> <span data-ttu-id="14e0c-131">몇 초 정도 기다린 hello 항목 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14e0c-131">If you wait a few seconds, hello item becomes available.</span></span> <span data-ttu-id="14e0c-132">Hello 지연이 길어질 경우 새로 고침 hello 웹 페이지는 종종 hello 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e0c-132">If hello delay is prolonged, refreshing hello web page often resolves hello problem.</span></span>

![스크린샷: Active Directory를 사용할 수 없음](./media/active-directory-troubleshooting/not-available.png)

