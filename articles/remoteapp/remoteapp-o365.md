---
title: "Azure RemoteApp과 함께 Office aaaUsing | Microsoft Docs"
description: "Office 및 Azure RemoteApp 연동 방법에 대해 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: f1773baf-8aa1-423c-a2f9-e4679e0463d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d065c1a0a2191c9e2e405264a835cecf791d6ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-office-with-azure-remoteapp"></a><span data-ttu-id="91b74-103">Azure RemoteApp과 함께 Office 사용</span><span class="sxs-lookup"><span data-stu-id="91b74-103">Using Office with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="91b74-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="91b74-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="91b74-106">Azure RemoteApp에서 Office 응용 프로그램 호스팅을 위한 두 가지 옵션으로, Office 365 ProPlus 또는 Office 2013 Professional Plus 평가판이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-106">You have two choices for hosting Office applications in Azure RemoteApp: Office 365 ProPlus or Office 2013 Professional Plus Trial.</span></span>

<span data-ttu-id="91b74-107">**이 문서는 향상된 새 문서로 곧 대체될 것입니다. 체크 아웃 [어떻게 toouse Azure RemoteApp과 함께 Office 365 구독](remoteapp-officesubscription.md)합니다. Office 365 + Azure RemoteApp을 사용 하기 위해 필요한 모든 hello 정보를 처리 합니다.**</span><span class="sxs-lookup"><span data-stu-id="91b74-107">**Hey, did you know we have a new, better article that will soon replace this? Check out [How toouse your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md). It covers all hello info you need for using Office 365 + Azure RemoteApp.**</span></span>

## <a name="office-365-proplus"></a><span data-ttu-id="91b74-108">Office 365 ProPlus</span><span class="sxs-lookup"><span data-stu-id="91b74-108">Office 365 ProPlus</span></span>
<span data-ttu-id="91b74-109">템플릿 이미지를 Office 365 ProPlus hello를 사용 하 여 RemoteApp 컬렉션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-109">You can create a RemoteApp collection using hello Office 365 ProPlus template image.</span></span> <span data-ttu-id="91b74-110">이 옵션 tooextend을 사용 하면 Office 365 서비스 tooRemoteApp 합니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-110">This option allows you tooextend your Office 365 service tooRemoteApp.</span></span> <span data-ttu-id="91b74-111">기존 구독 계획에 있어야 하 고 Office 365 ProPlus 서비스를 독립 실행형 hello에 대 한 또는 hello Office 365 서비스 계획을 통해 사용자가 허가 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-111">You must have an existing subscription plan and your users must be licensed for hello Office 365 ProPlus service, either standalone or through hello Office 365 service plans.</span></span>

<span data-ttu-id="91b74-112">RemoteApp은 Office 365 공유 컴퓨터 정품 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-112">RemoteApp supports Office 365 Shared Computer Activation.</span></span> <span data-ttu-id="91b74-113">공유 컴퓨터 정품 인증을 사용 하도록 설정 하 고 hello를 사용 하 여 [Office 배포 도구](http://www.microsoft.com/download/details.aspx?id=36778) 설치의 경우 Office 365 ProPlus 설치 활성화 되지 않고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-113">When you enable Shared Computer Activation, and use hello [Office Deployment tool](http://www.microsoft.com/download/details.aspx?id=36778) for installation, Office 365 ProPlus installs without being activated.</span></span> <span data-ttu-id="91b74-114">Office 365를 포함 하는 컬렉션에 사용자가 로그인 할 때 Office 365 ProPlus에 대 한 hello 사용자가 제공 하는 경우 Office toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-114">When a user signs into a collection that contains Office 365, Office checks toosee if hello user has been provisioned for Office 365 ProPlus.</span></span> <span data-ttu-id="91b74-115">활성화 되 면, Office 일시적으로 Office 365 ProPlus-이 활성화 될 때까지 해당 사용자가 로그 아웃 hello 서비스 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-115">If so, Office temporarily activates Office 365 ProPlus - this activation persists until that users signs out of hello service.</span></span>

<span data-ttu-id="91b74-116">toouse Office 365 공유 컴퓨터 인증을 해야 toocreate는 [사용자 지정 템플릿을](remoteapp-create-custom-image.md) 및 Office 365 ProPlus 설치, 다음과 같은 [이러한 방향은](https://technet.microsoft.com/library/dn782858.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-116">toouse Office 365 Shared Computer Activation, you need toocreate a [custom template](remoteapp-create-custom-image.md) and install Office 365 ProPlus there, following [these directions](https://technet.microsoft.com/library/dn782858.aspx).</span></span>

<span data-ttu-id="91b74-117">Hello에 사용자의 Office 365 라이선스를 관리할 수 있습니다 [Office 365 관리 포털](https://portal.office365.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-117">You can manage your users’ Office 365 licenses at hello [Office 365 Admin Portal](https://portal.office365.com/).</span></span> <span data-ttu-id="91b74-118">[Office 365 서비스 계획](http://technet.microsoft.com/library/office-365-plan-options.aspx)에 대한 자세한 내용을 읽어 보세요.</span><span class="sxs-lookup"><span data-stu-id="91b74-118">Read more information about [Office 365 service plans](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span></span>  

## <a name="office-2013-professional-plus-trial"></a><span data-ttu-id="91b74-119">Office 2013 Professional Plus 평가판</span><span class="sxs-lookup"><span data-stu-id="91b74-119">Office 2013 Professional Plus Trial</span></span>
<span data-ttu-id="91b74-120">RemoteApp의 30 일 평가판을 하는 동안 hello Office 2013 Professional 더하기 (평가판) 템플릿 이미지 toocreate RemoteApp 컬렉션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-120">During a 30-day trial of RemoteApp, you can use hello Office 2013 Professional Plus (trial) template image toocreate a RemoteApp collection.</span></span> <span data-ttu-id="91b74-121">사용자가 toothis 평가판 컬렉션 자신의 Azure Active Directory 작업 계정 또는 Microsoft 계정을 사용 하 여 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-121">You can assign users toothis trial collection using their Azure Active Directory work accounts or Microsoft accounts.</span></span> <span data-ttu-id="91b74-122">추가 구독은 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-122">No additional subscription is required.</span></span>

<span data-ttu-id="91b74-123">이 가장 좋습니다 tookick hello 타이어 이며 좋은 RemoteApp에 Office 파악할 하십시오.</span><span class="sxs-lookup"><span data-stu-id="91b74-123">This is a great option tookick hello tires and get a good feeling for Office in RemoteApp.</span></span> <span data-ttu-id="91b74-124">그러나 이 옵션은 평가 및 테스트 용도로만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-124">However, this option is intended for evaluation and testing only.</span></span> <span data-ttu-id="91b74-125">Hello Office 2013 Professional 더하기 (평가판) 템플릿 이미지를 사용 하 여 만든 연결 된 RemoteApp 컬렉션 모드 전환된 tooproduction 일 수 없습니다 및 hello hello 평가 기간이 끝나기 전에 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-125">RemoteApp collections created using hello Office 2013 Professional Plus (trial) template image cannot be transitioned tooproduction mode and will be disabled at hello end of hello trial period.</span></span>

## <a name="switching-from-trial-tooproduction"></a><span data-ttu-id="91b74-126">Tooproduction 평가판에서 전환</span><span class="sxs-lookup"><span data-stu-id="91b74-126">Switching from trial tooproduction</span></span>
<span data-ttu-id="91b74-127">30 일 무료 평가판을 시작할 때 hello hello 포털의 RemoteApp 섹션에서에서 메모 알려 기간 남은 hello 평가판에서 유료 계정 tootransition tooa 필요 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-127">When you start your 30-day free trial, a note in hello RemoteApp section of hello portal will tell you how long you have left in hello trial before you need tootransition tooa paid account.</span></span> <span data-ttu-id="91b74-128">Hello 링크를 사용 하 여이 정보에 사용자 계정 및 스위치 tooproduction 모드를 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-128">You can activate your account and switch tooproduction mode using hello link in this note.</span></span>

<span data-ttu-id="91b74-129">사용자 계정을 활성화 하면 계정에 연결 된 모든 hello RemoteApp 컬렉션이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-129">When you activate your account, this will affect all hello RemoteApp collections in your account.</span></span>

* <span data-ttu-id="91b74-130">Windows Server 2012 R2 hello 또는 hello Office 365 ProPlus 템플릿 이미지를 실행 중인 컬렉션 tooproduction를 원활 하 게 전환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-130">Collections that are running with hello Windows Server 2012 R2 or hello Office 365 ProPlus template images will transition tooproduction seamlessly.</span></span> <span data-ttu-id="91b74-131">진행 중인 세션을 비롯한 모든 사용자 데이터와 설정은 원래대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-131">All user data and settings, including ongoing sessions, remain intact.</span></span>
* <span data-ttu-id="91b74-132">업로드된 사용자 지정 템플릿 이미지가 있는 경우 이러한 이미지를 사용하는 컬렉션도 매끄럽게 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-132">If you have uploaded custom template images, collections using those images will also transition seamlessly.</span></span>
* <span data-ttu-id="91b74-133">hello Office 2013 Professional 더하기 (평가판) 템플릿 이미지만 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-133">hello Office 2013 Professional Plus (Trial) template image is intended for evaluation only.</span></span> <span data-ttu-id="91b74-134">이 템플릿 이미지와 실행 중인 컬렉션 전환된 tooproduction 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-134">Collections running with this template image cannot be transitioned tooproduction.</span></span> <span data-ttu-id="91b74-135">"사용 안 함" 상태로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-135">They will be put in "disabled" state.</span></span>

<span data-ttu-id="91b74-136">평가판의 만료 hello로 tooproduction 모드를 전환 되지 않으면 RemoteApp 컬렉션 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-136">If you do not transition tooproduction mode by hello expiration of your trial, your RemoteApp collections will be disabled.</span></span> <span data-ttu-id="91b74-137">걱정 하지 마십시오-설정 및 사용자 데이터 저장 되므로 다른 90 일 동안 데이터 손실 없이 사용자 서비스 및 스위치 tooproduction 모드를 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91b74-137">Don't worry - Your settings and users’ data are saved for another 90 days, so you can still activate your service and switch tooproduction mode without any data loss.</span></span>

