---
title: "Azure RemoteApp 컬렉션의 개별 사용자에게 응용 프로그램 게시(미리 보기) | Microsoft Docs"
description: "Azure RemoteApp에서 그룹 대신 개별 사용자에게 앱을 게시할 수 있는 방법에 대해 알아봅니다."
services: remoteapp-preview
documentationcenter: 
author: piotrci
manager: mbaldwin
editor: 
ms.assetid: 1fd0539d-fa65-4ea5-a98e-0be0cf580690
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: piotrci
ms.openlocfilehash: c94ffffdec3e46ed08d941ee58dcf17b432e1dad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="publish-applications-to-individual-users-in-an-azure-remoteapp-collection-preview"></a><span data-ttu-id="648c5-103">Azure RemoteApp 컬렉션의 개별 사용자에게 응용 프로그램 게시(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="648c5-103">Publish applications to individual users in an Azure RemoteApp collection (Preview)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="648c5-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="648c5-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="648c5-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="648c5-106">이 문서에서는 Azure RemoteApp 컬렉션의 개별 사용자에게 응용 프로그램을 게시하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-106">This article explains how to publish applications to individual users in an Azure RemoteApp collection.</span></span> <span data-ttu-id="648c5-107">Azure RemoteApp의 새로운 기능은 현재 비공개 미리 보기 상태이며 평가 목적으로 선택된 초기 채택자만이 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-107">This is new functionality in Azure RemoteApp, currently in private preview and available only to select early adopters for evaluation purposes.</span></span>

<span data-ttu-id="648c5-108">원래 Azure RemoteApp을 사용하면 응용 프로그램을 게시하는 한 가지 방법만이 가능합니다. 관리자는 이미지에서 앱을 게시하며 컬렉션의 모든 사용자에게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-108">Originally Azure RemoteApp enabled only one way of publishing applications: the administrator would publish apps from the image and they would be visible to all users in the collection.</span></span>

<span data-ttu-id="648c5-109">일반적인 시나리오는 단일 이미지에 많은 응용 프로그램을 포함하고 관리 비용을 줄이기 위해 하나의 컬렉션을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-109">A common scenario is to include many applications in a single image and deploy one collection in order to reduce management costs.</span></span> <span data-ttu-id="648c5-110">종종 일부 응용 프로그램은 일부 사용자와 관련이 없습니다. 관리자는 개별 사용자가 응용 프로그램 피드에서 불필요한 응용 프로그램을 확인하지 못하도록 개별 사용자에게 앱을 게시하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-110">Oftentimes not all applications are relevant to all users – administrators would prefer to publish apps to individual users so they don’t see unnecessary applications in their application feed.</span></span>

<span data-ttu-id="648c5-111">이제 Azure RemoteApp에서 현재 제한된 미리 보기 기능으로 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-111">This is now possible in Azure RemoteApp – currently as a limited preview feature.</span></span> <span data-ttu-id="648c5-112">다음은 새로운 기능의 간략한 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-112">Here is a brief summary of the new functionality:</span></span>

1. <span data-ttu-id="648c5-113">컬렉션은 두 가지 모드 중 하나로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-113">A collection can be set into one of two modes:</span></span>
   
   * <span data-ttu-id="648c5-114">원래 컬렉션 모드에서는 컬렉션의 모든 사용자가 게시된 응용 프로그램을 모두 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-114">the original collection mode, where all users in a collection can see all published applications.</span></span> <span data-ttu-id="648c5-115">이것이 기본 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-115">This is the default mode.</span></span>
   * <span data-ttu-id="648c5-116">새로운 응용 프로그램 모드에서는 사용자가 명시적으로 할당된 응용 프로그램만을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-116">the new application mode, where users only see applications that have been explicitly assigned to them</span></span>
2. <span data-ttu-id="648c5-117">현재 응용 프로그램 모드는 Azure RemoteApp PowerShell cmdlet을 사용하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-117">At the moment the application mode can only be enabled using Azure RemoteApp PowerShell cmdlets.</span></span>
   
   * <span data-ttu-id="648c5-118">응용 프로그램 모드로 설정하면 컬렉션의 사용자 할당은 Azure 포털을 통해 관리될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-118">When set to application mode, user assignment in the collection cannot be managed through the Azure portal.</span></span> <span data-ttu-id="648c5-119">사용자 할당은 PowerShell cmdlet을 통해 관리될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-119">User assignment has to be managed through PowerShell cmdlets.</span></span>
3. <span data-ttu-id="648c5-120">사용자는 자신에게 직접 게시된 응용 프로그램만을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-120">Users will only see the applications published directly to them.</span></span> <span data-ttu-id="648c5-121">그러나 사용자가 운영 체제에 직접 액세스하여 이미지에서 사용할 수 있는 다른 응용 프로그램을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-121">However, it may still be possible for a user to launch the other applications available on the image by accessing them directly in the operating system.</span></span>
   
   * <span data-ttu-id="648c5-122">이 기능은 응용 프로그램의 보안 잠금 기능을 제공하지 않으며 응용 프로그램 피드에서 표시 유형을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-122">This feature does not provide a secure lockdown of applications; it only limits visibility in the application feed.</span></span>
   * <span data-ttu-id="648c5-123">응용 프로그램에서 사용자를 격리해야 하는 경우 이에 대한 별도 컬렉션을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-123">If you need to isolate users from applications, you will need to use separate collections for that.</span></span>

## <a name="how-to-get-azure-remoteapp-powershell-cmdlets"></a><span data-ttu-id="648c5-124">Azure RemoteApp PowerShell cmdlet을 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="648c5-124">How to get Azure RemoteApp PowerShell cmdlets</span></span>
<span data-ttu-id="648c5-125">새 미리 보기 기능을 실행하려면 Azure PowerShell cmdlet을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-125">To try the new preview functionality, you will need to use Azure PowerShell cmdlets.</span></span> <span data-ttu-id="648c5-126">현재 Azure 관리 포털을 사용하여 새 응용 프로그램 게시 모드를 사용하도록 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-126">It is currently not possible to use the Azure Management portal to enable the new application publishing mode.</span></span>

<span data-ttu-id="648c5-127">우선 [Azure PowerShell 모듈](/powershell/azure/overview) 을 설치했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-127">First, make sure you have the [Azure PowerShell module](/powershell/azure/overview) installed.</span></span>

<span data-ttu-id="648c5-128">그런 다음 관리자 모드에서 PowerShell 콘솔을 시작하고 다음 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-128">Then launch the PowerShell console in administrator mode and run the following cmdlet:</span></span>

        Add-AzureAccount

<span data-ttu-id="648c5-129">Azure 사용자 이름 및 암호를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-129">It will prompt you for your Azure user name and password.</span></span> <span data-ttu-id="648c5-130">로그인하면 Azure 구독에 대해 Azure RemoteApp cmdlet을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-130">Once signed in, you will be able to run Azure RemoteApp cmdlets against your Azure subscriptions.</span></span>

## <a name="how-to-check-which-mode-a-collection-is-in"></a><span data-ttu-id="648c5-131">컬렉션이 있는 모드를 확인하는 방법</span><span class="sxs-lookup"><span data-stu-id="648c5-131">How to check which mode a collection is in</span></span>
<span data-ttu-id="648c5-132">다음 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-132">Run the following cmdlet:</span></span>

        Get-AzureRemoteAppCollection <collectionName>

![컬렉션 모드를 확인합니다.](./media/remoteapp-perapp/araacllelvel.png)

<span data-ttu-id="648c5-134">AclLevel 속성은 다음 값을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-134">The AclLevel property can have the following values:</span></span>

* <span data-ttu-id="648c5-135">컬렉션: 원래 게시 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-135">Collection: the original publishing mode.</span></span> <span data-ttu-id="648c5-136">모든 사용자는 게시된 앱을 모두 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-136">All users see all published apps.</span></span>
* <span data-ttu-id="648c5-137">응용 프로그램: 새 게시 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-137">Application: the new publishing mode.</span></span> <span data-ttu-id="648c5-138">사용자는 자신에게 직접 게시된 앱만 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-138">Users see only the apps published directly to them.</span></span>

## <a name="how-to-switch-to-application-publishing-mode"></a><span data-ttu-id="648c5-139">응용 프로그램 게시 모드로 전환하는 방법</span><span class="sxs-lookup"><span data-stu-id="648c5-139">How to switch to application publishing mode</span></span>
<span data-ttu-id="648c5-140">다음 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-140">Run the following cmdlet:</span></span>

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

<span data-ttu-id="648c5-141">응용 프로그램 게시 상태를 그대로 유지합니다. 처음에 모든 사용자는 원래 게시된 앱을 모두 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-141">Application publishing state will be preserved: initially all users will see all of the original published apps.</span></span>

## <a name="how-to-list-users-who-can-see-a-specific-application"></a><span data-ttu-id="648c5-142">특정 응용 프로그램을 볼 수 있는 사용자를 나열하는 방법</span><span class="sxs-lookup"><span data-stu-id="648c5-142">How to list users who can see a specific application</span></span>
<span data-ttu-id="648c5-143">다음 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-143">Run the following cmdlet:</span></span>

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

<span data-ttu-id="648c5-144">응용 프로그램을 볼 수 있는 모든 사용자를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-144">This lists all users who can see the application.</span></span>

<span data-ttu-id="648c5-145">참고: Get-AzureRemoteAppProgram -CollectionName <collectionName>을 실행하여 응용 프로그램 별칭(위의 구문에서 "앱 별칭"이라고 함)을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-145">Note: You can see the application aliases (called "app alias" in the syntax above) by running Get-AzureRemoteAppProgram -CollectionName <collectionName>.</span></span>

## <a name="how-to-assign-an-application-to-a-user"></a><span data-ttu-id="648c5-146">사용자에게 응용 프로그램을 할당하는 방법</span><span class="sxs-lookup"><span data-stu-id="648c5-146">How to assign an application to a user</span></span>
<span data-ttu-id="648c5-147">다음 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-147">Run the following cmdlet:</span></span>

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

<span data-ttu-id="648c5-148">이제 사용자가 Azure RemoteApp 클라이언트에서 응용 프로그램을 보고 여기에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-148">The user will now see the application in the Azure RemoteApp client and will be able to connect to it.</span></span>

## <a name="how-to-remove-an-application-from-a-user"></a><span data-ttu-id="648c5-149">사용자의 응용 프로그램을 제거하는 방법</span><span class="sxs-lookup"><span data-stu-id="648c5-149">How to remove an application from a user</span></span>
<span data-ttu-id="648c5-150">다음 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-150">Run the following cmdlet:</span></span>

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a><span data-ttu-id="648c5-151">사용자 의견 제공</span><span class="sxs-lookup"><span data-stu-id="648c5-151">Providing feedback</span></span>
<span data-ttu-id="648c5-152">이 미리 보기 기능에 대한 제안과 의견에 감사합니다.</span><span class="sxs-lookup"><span data-stu-id="648c5-152">We appreciate your feedback and suggestions regarding this preview feature.</span></span> <span data-ttu-id="648c5-153">[설문 조사](http://www.instant.ly/s/FDdrb) 를 입력하여 의견을 알려주세요.</span><span class="sxs-lookup"><span data-stu-id="648c5-153">Please fill out the [survey](http://www.instant.ly/s/FDdrb) to let us know what you think.</span></span>

## <a name="havent-had-a-chance-to-try-the-preview-feature"></a><span data-ttu-id="648c5-154">미리 보기 기능을 시도해 본 적이 있나요?</span><span class="sxs-lookup"><span data-stu-id="648c5-154">Haven't had a chance to try the preview feature?</span></span>
<span data-ttu-id="648c5-155">미리 보기에 아직 참여하지 않은 경우 이 [설문 조사](http://www.instant.ly/s/AY83p) 를 사용하여 액세스를 요청하세요.</span><span class="sxs-lookup"><span data-stu-id="648c5-155">If you have not participated in the preview yet, please use this [survey](http://www.instant.ly/s/AY83p) to request access.</span></span>

