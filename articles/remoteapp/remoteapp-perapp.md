---
title: "aaaPublish 응용 프로그램 tooindividual 사용자에 게는 Azure RemoteApp 컬렉션 (미리 보기) | Microsoft Docs"
description: "Azure RemoteApp에서 그룹에 따라 대신 앱 tooindividual 사용자를 게시할 수는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 87b435552ddbfc2c6d03aeb01d95a44985e71f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-tooindividual-users-in-an-azure-remoteapp-collection-preview"></a><span data-ttu-id="db71b-103">Azure RemoteApp 컬렉션 (미리 보기)에 tooindividual 사용자가 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="db71b-103">Publish applications tooindividual users in an Azure RemoteApp collection (Preview)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="db71b-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="db71b-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="db71b-106">이 문서에서는 설명 어떻게 toopublish 응용 프로그램 tooindividual 사용자는 Azure RemoteApp 컬렉션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-106">This article explains how toopublish applications tooindividual users in an Azure RemoteApp collection.</span></span> <span data-ttu-id="db71b-107">이것이 Azure RemoteApp에서, 현재 비공개 미리 보기 및 사용 가능한 유일한 tooselect 조기 채택자 평가 목적에서 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-107">This is new functionality in Azure RemoteApp, currently in private preview and available only tooselect early adopters for evaluation purposes.</span></span>

<span data-ttu-id="db71b-108">Azure RemoteApp만 한 가지 방법은 응용 프로그램 게시를 사용 하는 원래: 관리자에 게 게시할 앱 hello 이미지에서 표시 tooall 사용자 hello 컬렉션에 예상 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-108">Originally Azure RemoteApp enabled only one way of publishing applications: hello administrator would publish apps from hello image and they would be visible tooall users in hello collection.</span></span>

<span data-ttu-id="db71b-109">일반적인 시나리오는 tooinclude 단일에서 많은 응용 프로그램 이미지 및 순서 tooreduce 관리 비용이 증가 한 컬렉션을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-109">A common scenario is tooinclude many applications in a single image and deploy one collection in order tooreduce management costs.</span></span> <span data-ttu-id="db71b-110">종종 일부 응용 프로그램 관련 tooall 사용자-관리자 toopublish 앱 tooindividual 사용자 피드 해당 응용 프로그램에서 불필요 한 응용 프로그램 볼 하지 않는 방법을 합니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-110">Oftentimes not all applications are relevant tooall users – administrators would prefer toopublish apps tooindividual users so they don’t see unnecessary applications in their application feed.</span></span>

<span data-ttu-id="db71b-111">이제 Azure RemoteApp에서 현재 제한된 미리 보기 기능으로 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-111">This is now possible in Azure RemoteApp – currently as a limited preview feature.</span></span> <span data-ttu-id="db71b-112">다음은 hello 새로운 기능에 대 한 간단한 요약이입니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-112">Here is a brief summary of hello new functionality:</span></span>

1. <span data-ttu-id="db71b-113">컬렉션은 두 가지 모드 중 하나로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-113">A collection can be set into one of two modes:</span></span>
   
   * <span data-ttu-id="db71b-114">hello 원래 컬렉션 모드에서는 컬렉션의 모든 사용자가 볼 수 있는 모든 게시 된 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-114">hello original collection mode, where all users in a collection can see all published applications.</span></span> <span data-ttu-id="db71b-115">이 hello 기본 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-115">This is hello default mode.</span></span>
   * <span data-ttu-id="db71b-116">hello 새 응용 프로그램 모드를 toothem 명시적으로 할당 된 응용 프로그램에 사용자만 볼</span><span class="sxs-lookup"><span data-stu-id="db71b-116">hello new application mode, where users only see applications that have been explicitly assigned toothem</span></span>
2. <span data-ttu-id="db71b-117">Hello 순간에 hello 적용 모드에만 사용할 수 있으며 Azure RemoteApp PowerShell cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-117">At hello moment hello application mode can only be enabled using Azure RemoteApp PowerShell cmdlets.</span></span>
   
   * <span data-ttu-id="db71b-118">때 hello 컬렉션에 사용자 할당 tooapplication 모드 설정 hello Azure 포털을 통해 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-118">When set tooapplication mode, user assignment in hello collection cannot be managed through hello Azure portal.</span></span> <span data-ttu-id="db71b-119">사용자 할당은 toobe PowerShell cmdlet을 통해 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-119">User assignment has toobe managed through PowerShell cmdlets.</span></span>
3. <span data-ttu-id="db71b-120">사용자는 데이터만 볼 hello 응용 프로그램은 toothem 직접 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-120">Users will only see hello applications published directly toothem.</span></span> <span data-ttu-id="db71b-121">그러나 수 가능한 사용자 toolaunch hello 운영 체제에 직접 액세스 하 여 hello 이미지에서 사용할 수 있는 다른 응용 프로그램을 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-121">However, it may still be possible for a user toolaunch hello other applications available on hello image by accessing them directly in hello operating system.</span></span>
   
   * <span data-ttu-id="db71b-122">이 기능은 응용 프로그램의 보안 잠금 기능을 제공 하지 않습니다. 피드 hello 응용 프로그램의 표시 여부를 제한 하기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-122">This feature does not provide a secure lockdown of applications; it only limits visibility in hello application feed.</span></span>
   * <span data-ttu-id="db71b-123">응용 프로그램에서 tooisolate 사용자가 필요한 경우 toouse 분리 된 컬렉션에 대 한 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-123">If you need tooisolate users from applications, you will need toouse separate collections for that.</span></span>

## <a name="how-tooget-azure-remoteapp-powershell-cmdlets"></a><span data-ttu-id="db71b-124">어떻게 tooget Azure RemoteApp PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="db71b-124">How tooget Azure RemoteApp PowerShell cmdlets</span></span>
<span data-ttu-id="db71b-125">tootry hello 새 미리 보기 기능 toouse Azure PowerShell cmdlet을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-125">tootry hello new preview functionality, you will need toouse Azure PowerShell cmdlets.</span></span> <span data-ttu-id="db71b-126">현재 하지 가능한 toouse hello Azure 관리 포털 tooenable hello 새 응용 프로그램 게시 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-126">It is currently not possible toouse hello Azure Management portal tooenable hello new application publishing mode.</span></span>

<span data-ttu-id="db71b-127">첫째, 있어야 hello [Azure PowerShell 모듈](/powershell/azure/overview) 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-127">First, make sure you have hello [Azure PowerShell module](/powershell/azure/overview) installed.</span></span>

<span data-ttu-id="db71b-128">그런 다음 관리자 모드와 실행된 hello cmdlet을 다음의 hello PowerShell 콘솔을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-128">Then launch hello PowerShell console in administrator mode and run hello following cmdlet:</span></span>

        Add-AzureAccount

<span data-ttu-id="db71b-129">Azure 사용자 이름 및 암호를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-129">It will prompt you for your Azure user name and password.</span></span> <span data-ttu-id="db71b-130">로그인 한 후 Azure 구독에 대 한 Azure RemoteApp cmdlet 수 toorun 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-130">Once signed in, you will be able toorun Azure RemoteApp cmdlets against your Azure subscriptions.</span></span>

## <a name="how-toocheck-which-mode-a-collection-is-in"></a><span data-ttu-id="db71b-131">어떻게 toocheck 모드는 컬렉션은</span><span class="sxs-lookup"><span data-stu-id="db71b-131">How toocheck which mode a collection is in</span></span>
<span data-ttu-id="db71b-132">Hello 다음 cmdlet을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-132">Run hello following cmdlet:</span></span>

        Get-AzureRemoteAppCollection <collectionName>

![Hello 컬렉션 모드를 확인 합니다.](./media/remoteapp-perapp/araacllelvel.png)

<span data-ttu-id="db71b-134">hello AclLevel 속성 hello 다음 값을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-134">hello AclLevel property can have hello following values:</span></span>

* <span data-ttu-id="db71b-135">컬렉션: hello 원래 게시 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-135">Collection: hello original publishing mode.</span></span> <span data-ttu-id="db71b-136">모든 사용자는 게시된 앱을 모두 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-136">All users see all published apps.</span></span>
* <span data-ttu-id="db71b-137">응용 프로그램: hello 새 게시 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-137">Application: hello new publishing mode.</span></span> <span data-ttu-id="db71b-138">사용자는 hello 앱만 게시 toothem 직접 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-138">Users see only hello apps published directly toothem.</span></span>

## <a name="how-tooswitch-tooapplication-publishing-mode"></a><span data-ttu-id="db71b-139">어떻게 tooswitch tooapplication 게시 모드</span><span class="sxs-lookup"><span data-stu-id="db71b-139">How tooswitch tooapplication publishing mode</span></span>
<span data-ttu-id="db71b-140">Hello 다음 cmdlet을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-140">Run hello following cmdlet:</span></span>

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

<span data-ttu-id="db71b-141">응용 프로그램 게시 상태를 유지 됩니다: 처음에 모든 사용자는 hello 원래 게시 된 앱을 모두 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-141">Application publishing state will be preserved: initially all users will see all of hello original published apps.</span></span>

## <a name="how-toolist-users-who-can-see-a-specific-application"></a><span data-ttu-id="db71b-142">어떻게 toolist 사용자가 특정 응용 프로그램을 볼 수 있는 사용자</span><span class="sxs-lookup"><span data-stu-id="db71b-142">How toolist users who can see a specific application</span></span>
<span data-ttu-id="db71b-143">Hello 다음 cmdlet을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-143">Run hello following cmdlet:</span></span>

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

<span data-ttu-id="db71b-144">Hello 응용 프로그램을 볼 수 있는 모든 사용자를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-144">This lists all users who can see hello application.</span></span>

<span data-ttu-id="db71b-145">참고: Get AzureRemoteAppProgram CollectionName를 실행 하 여 hello 응용 프로그램 별칭 (위의 hello 구문에서 "응용 프로그램 별칭" 라고 함)를 볼 수 <collectionName>합니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-145">Note: You can see hello application aliases (called "app alias" in hello syntax above) by running Get-AzureRemoteAppProgram -CollectionName <collectionName>.</span></span>

## <a name="how-tooassign-an-application-tooa-user"></a><span data-ttu-id="db71b-146">어떻게 tooassign 응용 프로그램 tooa 사용자</span><span class="sxs-lookup"><span data-stu-id="db71b-146">How tooassign an application tooa user</span></span>
<span data-ttu-id="db71b-147">Hello 다음 cmdlet을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-147">Run hello following cmdlet:</span></span>

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

<span data-ttu-id="db71b-148">hello 사용자는 이제 hello Azure RemoteApp 클라이언트에서 hello 응용 프로그램에 표시 하 고 수 tooconnect tooit 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-148">hello user will now see hello application in hello Azure RemoteApp client and will be able tooconnect tooit.</span></span>

## <a name="how-tooremove-an-application-from-a-user"></a><span data-ttu-id="db71b-149">어떻게 tooremove 사용자 로부터 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="db71b-149">How tooremove an application from a user</span></span>
<span data-ttu-id="db71b-150">Hello 다음 cmdlet을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-150">Run hello following cmdlet:</span></span>

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a><span data-ttu-id="db71b-151">사용자 의견 제공</span><span class="sxs-lookup"><span data-stu-id="db71b-151">Providing feedback</span></span>
<span data-ttu-id="db71b-152">이 미리 보기 기능에 대한 제안과 의견에 감사합니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-152">We appreciate your feedback and suggestions regarding this preview feature.</span></span> <span data-ttu-id="db71b-153">Hello 정보를 입력 하세요 [설문 조사](http://www.instant.ly/s/FDdrb) toolet 어떻게 생각 알려주세요.</span><span class="sxs-lookup"><span data-stu-id="db71b-153">Please fill out hello [survey](http://www.instant.ly/s/FDdrb) toolet us know what you think.</span></span>

## <a name="havent-had-a-chance-tootry-hello-preview-feature"></a><span data-ttu-id="db71b-154">기회 tootry hello 미리 보기 기능이 없 었?</span><span class="sxs-lookup"><span data-stu-id="db71b-154">Haven't had a chance tootry hello preview feature?</span></span>
<span data-ttu-id="db71b-155">경우 있습니다 하지 참여 hello 미리 보기에 아직를 사용 하 여이 [설문 조사](http://www.instant.ly/s/AY83p) toorequest 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="db71b-155">If you have not participated in hello preview yet, please use this [survey](http://www.instant.ly/s/AY83p) toorequest access.</span></span>

