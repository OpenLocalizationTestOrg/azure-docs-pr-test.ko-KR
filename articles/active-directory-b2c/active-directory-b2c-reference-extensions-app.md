---
title: "확장 앱 - Azure AD B2C | Microsoft Docs"
description: "Hello b2c 확장 앱을 복원"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f0392e32-0771-473c-a799-81438ca2bcff
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/17/2017
ms.author: parja
ms.openlocfilehash: b36410c18314bd893dc669b49814fdcd77fae054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-extensions-app"></a><span data-ttu-id="0bf9b-103">Azure AD B2C: 확장 앱</span><span class="sxs-lookup"><span data-stu-id="0bf9b-103">Azure AD B2C: Extensions app</span></span>

<span data-ttu-id="0bf9b-104">Azure AD B2C 디렉터리를 만든 경우 앱 호출할 `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` hello 새 디렉터리 안에 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-104">When an Azure AD B2C directory is created, an app called `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` is automatically created inside hello new directory.</span></span> <span data-ttu-id="0bf9b-105">이 응용 프로그램, 참조 tooas hello **b2c 확장 앱**에서 볼 수 *앱 등록*합니다.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-105">This app, referred tooas hello **b2c-extensions-app**, is visible in *App registrations*.</span></span> <span data-ttu-id="0bf9b-106">사용자 및 사용자 지정 특성에 대 한 Azure AD B2C 서비스 toostore 정보 hello에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-106">It is used by hello Azure AD B2C service toostore information about users and custom attributes.</span></span> <span data-ttu-id="0bf9b-107">Hello 앱을 삭제 하는 경우 Azure AD B2C 제대로 작동 하지 않 및 프로덕션 환경에 영향을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-107">If hello app is deleted, Azure AD B2C will not function correctly and your production environment will be affected.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0bf9b-108">Tooimmediately delete 테 넌 트 계획 하지 않는 한 hello b2c 확장 앱을 삭제 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-108">Do not delete hello b2c-extensions-app unless you are planning tooimmediately delete your tenant.</span></span> <span data-ttu-id="0bf9b-109">30 일에 대 한 hello 앱 삭제 된 상태인 경우 사용자 정보를 영구적으로 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-109">If hello app remains deleted for more than 30 days, user information will be permanently lost.</span></span>

## <a name="verifying-that-hello-extensions-app-is-present"></a><span data-ttu-id="0bf9b-110">Hello 확장 앱 있는지 확인 하는 중</span><span class="sxs-lookup"><span data-stu-id="0bf9b-110">Verifying that hello extensions app is present</span></span>

<span data-ttu-id="0bf9b-111">b2c 확장 앱 hello tooverify이 있음:</span><span class="sxs-lookup"><span data-stu-id="0bf9b-111">tooverify that hello b2c-extensions-app is present:</span></span>

1. <span data-ttu-id="0bf9b-112">Azure AD B2C 테 넌 트 내에서 클릭 **더 많은 서비스** hello 왼쪽 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-112">Inside your Azure AD B2C tenant, click on **More services** in hello left-hand navigation menu.</span></span>
1. <span data-ttu-id="0bf9b-113">**앱 등록**을 검색하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-113">Search for and open **App registrations**.</span></span>
1. <span data-ttu-id="0bf9b-114">**b2c-extensions-app**으로 시작하는 앱을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-114">Look for an app that begins with **b2c-extensions-app**</span></span>

## <a name="recover-hello-extensions-app"></a><span data-ttu-id="0bf9b-115">Hello 확장 응용 프로그램을 복구 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-115">Recover hello extensions app</span></span>

<span data-ttu-id="0bf9b-116">30 일 toorecover hello b2c-확장-app를 실수로 삭제 한 경우 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-116">If you accidentally deleted hello b2c-extensions-app, you have 30 days toorecover it.</span></span> <span data-ttu-id="0bf9b-117">Hello Graph API를 사용 하 여 hello 응용 프로그램을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-117">You can restore hello app using hello Graph API:</span></span>

1. <span data-ttu-id="0bf9b-118">너무 찾아보기[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-118">Browse too[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span></span>
1. <span data-ttu-id="0bf9b-119">Toorestore 삭제 hello 응용 프로그램에 대 한 원하는 hello Azure AD B2C 디렉터리에 대 한 전역 관리자 toohello 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-119">Log in toohello site as a global administrator for hello Azure AD B2C directory that you want toorestore hello deleted app for.</span></span>
1. <span data-ttu-id="0bf9b-120">Hello URL에 대해 HTTP GET 발급 `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` api 버전 1.6 = 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-120">Issue an HTTP GET against hello URL `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` with api-version=1.6.</span></span> <span data-ttu-id="0bf9b-121">있는지 tooreplace 확인 `{tenantName}` 을 테 넌 트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-121">Make sure tooreplace `{tenantName}` with your tenant name.</span></span> <span data-ttu-id="0bf9b-122">이 작업에는 지난 30 일간 hello 내에서 삭제 하는 hello 응용 프로그램의 모든 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-122">This operation will list all of hello applications that have been deleted within hello past 30 days.</span></span>
1. <span data-ttu-id="0bf9b-123">Hello 응용 프로그램에서 hello 이름 ' b2c 확장 app' 및 복사로 시작 하는 hello 목록에서 찾을 해당 `objectid` 속성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-123">Find hello application in hello list where hello name begins with 'b2c-extension-app’ and copy its `objectid` property value.</span></span>
1. <span data-ttu-id="0bf9b-124">Hello URL에 대해 HTTP POST 발급 `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`합니다.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-124">Issue an HTTP POST against hello URL `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span></span> <span data-ttu-id="0bf9b-125">Hello 대체 `{OBJECTID}` hello로 hello URL의 일부 `objectid` hello 이전 단계에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-125">Replace hello `{OBJECTID}` portion of hello URL with hello `objectid` from hello previous step.</span></span> 

<span data-ttu-id="0bf9b-126">이제 있어야 너무[앱이 복원 hello](#verifying-that-the-extensions-app-is-present) hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-126">You should now be able too[see hello restored app](#verifying-that-the-extensions-app-is-present) in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="0bf9b-127">응용 프로그램 삭제 되어 hello 내에서 지난 30 일 경우에 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-127">An application can only be restored if it has been deleted within hello last 30 days.</span></span> <span data-ttu-id="0bf9b-128">30일이 지난 경우 데이터는 영구적으로 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-128">If it has been more than 30 days, data will be permanently lost.</span></span> <span data-ttu-id="0bf9b-129">추가 지원이 필요한 경우 지원 티켓을 파일로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0bf9b-129">For more assistance, file a support ticket.</span></span>
