---
title: "Azure RemoteApp과 함께 Office 사용 | Microsoft Docs"
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
ms.openlocfilehash: a776d877c764109f15c1025db2be3114eea2130a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-office-with-azure-remoteapp"></a><span data-ttu-id="65ba0-103">Azure RemoteApp과 함께 Office 사용</span><span class="sxs-lookup"><span data-stu-id="65ba0-103">Using Office with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="65ba0-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="65ba0-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="65ba0-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="65ba0-106">Azure RemoteApp에서 Office 응용 프로그램 호스팅을 위한 두 가지 옵션으로, Office 365 ProPlus 또는 Office 2013 Professional Plus 평가판이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-106">You have two choices for hosting Office applications in Azure RemoteApp: Office 365 ProPlus or Office 2013 Professional Plus Trial.</span></span>

<span data-ttu-id="65ba0-107">**이 문서는 향상된 새 문서로 곧 대체될 것입니다. [Azure RemoteApp에서 Office 365 구독을 사용하는 방법](remoteapp-officesubscription.md)을 확인하세요. Office 365 + Azure RemoteApp을 사용하는 데 필요한 모든 정보를 제공합니다.**</span><span class="sxs-lookup"><span data-stu-id="65ba0-107">**Hey, did you know we have a new, better article that will soon replace this? Check out [How to use your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md). It covers all the info you need for using Office 365 + Azure RemoteApp.**</span></span>

## <a name="office-365-proplus"></a><span data-ttu-id="65ba0-108">Office 365 ProPlus</span><span class="sxs-lookup"><span data-stu-id="65ba0-108">Office 365 ProPlus</span></span>
<span data-ttu-id="65ba0-109">Office 365 ProPlus 템플릿 이미지를 사용하여 RemoteApp 컬렉션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-109">You can create a RemoteApp collection using the Office 365 ProPlus template image.</span></span> <span data-ttu-id="65ba0-110">이 옵션을 사용하면 Office 365 서비스를 RemoteApp까지 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-110">This option allows you to extend your Office 365 service to RemoteApp.</span></span> <span data-ttu-id="65ba0-111">기존 구독 계획이 있어야 하며, 독립 실행형이나 Office 365 서비스 계획을 통해 사용자에게 Office 365 ProPlus 서비스에 대한 라이선스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-111">You must have an existing subscription plan and your users must be licensed for the Office 365 ProPlus service, either standalone or through the Office 365 service plans.</span></span>

<span data-ttu-id="65ba0-112">RemoteApp은 Office 365 공유 컴퓨터 정품 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-112">RemoteApp supports Office 365 Shared Computer Activation.</span></span> <span data-ttu-id="65ba0-113">[공유 컴퓨터 정품 인증]을 활성화하고 설치를 위해 [Office 배포 도구](http://www.microsoft.com/download/details.aspx?id=36778)를 사용하면 Office 365 ProPlus가 정품 인증없이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-113">When you enable Shared Computer Activation, and use the [Office Deployment tool](http://www.microsoft.com/download/details.aspx?id=36778) for installation, Office 365 ProPlus installs without being activated.</span></span> <span data-ttu-id="65ba0-114">사용자가 Office 365를 포함하는 컬렉션에 로그인하면 Office는 해당 사용자가 Office 365 ProPlus에 프로비전되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-114">When a user signs into a collection that contains Office 365, Office checks to see if the user has been provisioned for Office 365 ProPlus.</span></span> <span data-ttu-id="65ba0-115">프로비전된 경우 Office는 Office 365 ProPlus를 임시로 활성화합니다. 이 활성화는 해당 사용자가 서비스를 로그아웃할 때까지 지속됩니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-115">If so, Office temporarily activates Office 365 ProPlus - this activation persists until that users signs out of the service.</span></span>

<span data-ttu-id="65ba0-116">[Office 365 공유 컴퓨터 정품 인증]을 사용하려면 [사용자 지정 템플릿](remoteapp-create-custom-image.md)을 만들고 [이 지침](https://technet.microsoft.com/library/dn782858.aspx)에 따라 Office 365 ProPlus를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-116">To use Office 365 Shared Computer Activation, you need to create a [custom template](remoteapp-create-custom-image.md) and install Office 365 ProPlus there, following [these directions](https://technet.microsoft.com/library/dn782858.aspx).</span></span>

<span data-ttu-id="65ba0-117">[Office 365 관리 포털](https://portal.office365.com/)에서 사용자의 Office 365 라이선스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-117">You can manage your users’ Office 365 licenses at the [Office 365 Admin Portal](https://portal.office365.com/).</span></span> <span data-ttu-id="65ba0-118">[Office 365 서비스 계획](http://technet.microsoft.com/library/office-365-plan-options.aspx)에 대한 자세한 내용을 읽어 보세요.</span><span class="sxs-lookup"><span data-stu-id="65ba0-118">Read more information about [Office 365 service plans](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span></span>  

## <a name="office-2013-professional-plus-trial"></a><span data-ttu-id="65ba0-119">Office 2013 Professional Plus 평가판</span><span class="sxs-lookup"><span data-stu-id="65ba0-119">Office 2013 Professional Plus Trial</span></span>
<span data-ttu-id="65ba0-120">RemoteApp의 30일 평가 기간 동안 Office 2013 Professional Plus(평가판) 템플릿 이미지를 사용하여 RemoteApp 컬렉션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-120">During a 30-day trial of RemoteApp, you can use the Office 2013 Professional Plus (trial) template image to create a RemoteApp collection.</span></span> <span data-ttu-id="65ba0-121">Azure Active Directory 작업 계정이나 Microsoft 계정을 사용하여 이 평가판 컬렉션에 사용자를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-121">You can assign users to this trial collection using their Azure Active Directory work accounts or Microsoft accounts.</span></span> <span data-ttu-id="65ba0-122">추가 구독은 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-122">No additional subscription is required.</span></span>

<span data-ttu-id="65ba0-123">이 옵션은 RemoteApp의 Office를 평가하고 파악하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-123">This is a great option to kick the tires and get a good feeling for Office in RemoteApp.</span></span> <span data-ttu-id="65ba0-124">그러나 이 옵션은 평가 및 테스트 용도로만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-124">However, this option is intended for evaluation and testing only.</span></span> <span data-ttu-id="65ba0-125">Office 2013 Professional Plus(평가판) 템플릿 이미지를 사용하여 만든 RemoteApp 컬렉션은 프로덕션 모드로 전환할 수 없으며 평가 기간이 끝나면 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-125">RemoteApp collections created using the Office 2013 Professional Plus (trial) template image cannot be transitioned to production mode and will be disabled at the end of the trial period.</span></span>

## <a name="switching-from-trial-to-production"></a><span data-ttu-id="65ba0-126">평가판에서 프로덕션으로 전환</span><span class="sxs-lookup"><span data-stu-id="65ba0-126">Switching from trial to production</span></span>
<span data-ttu-id="65ba0-127">30일 무료 평가판을 시작하면 유료 계정으로 전환해야 하기까지 남은 기간을 알리는 메모가 포털의 RemoteApp 섹션에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-127">When you start your 30-day free trial, a note in the RemoteApp section of the portal will tell you how long you have left in the trial before you need to transition to a paid account.</span></span> <span data-ttu-id="65ba0-128">이 메모의 링크를 사용하여 계정을 활성화하고 프로덕션 모드로 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-128">You can activate your account and switch to production mode using the link in this note.</span></span>

<span data-ttu-id="65ba0-129">계정을 활성화하면 계정의 모든 RemoteApp 컬렉션에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-129">When you activate your account, this will affect all the RemoteApp collections in your account.</span></span>

* <span data-ttu-id="65ba0-130">Windows Server 2012 R2 또는 Office 365 ProPlus 템플릿 이미지를 사용하여 실행되는 컬렉션이 프로덕션으로 매끄럽게 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-130">Collections that are running with the Windows Server 2012 R2 or the Office 365 ProPlus template images will transition to production seamlessly.</span></span> <span data-ttu-id="65ba0-131">진행 중인 세션을 비롯한 모든 사용자 데이터와 설정은 원래대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-131">All user data and settings, including ongoing sessions, remain intact.</span></span>
* <span data-ttu-id="65ba0-132">업로드된 사용자 지정 템플릿 이미지가 있는 경우 이러한 이미지를 사용하는 컬렉션도 매끄럽게 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-132">If you have uploaded custom template images, collections using those images will also transition seamlessly.</span></span>
* <span data-ttu-id="65ba0-133">Office 2013 Professional Plus(평가판) 템플릿 이미지는 평가 용도로만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-133">The Office 2013 Professional Plus (Trial) template image is intended for evaluation only.</span></span> <span data-ttu-id="65ba0-134">이 템플릿 이미지를 사용하여 실행되는 컬렉션은 프로덕션으로 전환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-134">Collections running with this template image cannot be transitioned to production.</span></span> <span data-ttu-id="65ba0-135">"사용 안 함" 상태로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-135">They will be put in "disabled" state.</span></span>

<span data-ttu-id="65ba0-136">평가판이 만료될 때까지 프로덕션 모드로 전환하지 않으면 RemoteApp 컬렉션을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-136">If you do not transition to production mode by the expiration of your trial, your RemoteApp collections will be disabled.</span></span> <span data-ttu-id="65ba0-137">걱정하지 마세요. 설정과 사용자 데이터는 90일 동안 저장되므로 데이터 손실 없이 서비스를 활성화하고 프로덕션 모드로 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ba0-137">Don't worry - Your settings and users’ data are saved for another 90 days, so you can still activate your service and switch to production mode without any data loss.</span></span>

