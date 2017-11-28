---
title: "Office 365 사용자 계정으로 Azure RemoteApp aaaHow toouse | Microsoft Docs"
description: "자세한 내용은 방법 내 Office 365 사용자 계정으로 Azure RemoteApp toouse"
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: aba70fd3-60b0-4b44-9321-1ab18760ccd5
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d2dbed2a6838adf9bb0f7508eb7dcecb0a74a62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-remoteapp-with-office-365-user-accounts"></a><span data-ttu-id="36385-103">어떻게 Office 365 사용자 계정으로 Azure RemoteApp toouse</span><span class="sxs-lookup"><span data-stu-id="36385-103">How toouse Azure RemoteApp with Office 365 user accounts</span></span>
> [!IMPORTANT]
> <span data-ttu-id="36385-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="36385-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="36385-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="36385-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="36385-106">사용자 이름을 저장 하는 Azure Active Directory가 Office 365 구독이 있는 경우 암호 tooaccess Office 365 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="36385-106">If you have an Office 365 subscription you have an Azure Active Directory that stores your user names and passwords used tooaccess Office 365 services.</span></span> <span data-ttu-id="36385-107">예를 들어 사용자가 활성화 Office 365 ProPlus 라이선스에 대 한 Azure AD toocheck에 대해 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="36385-107">For example, when your users activate Office 365 ProPlus they authenticate against Azure AD toocheck for licenses.</span></span> <span data-ttu-id="36385-108">대부분의 고객은 toouse 같은 hello 동일한 Azure RemoteApp과 함께 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="36385-108">Most customers would like toouse hello same directory with Azure RemoteApp.</span></span>

<span data-ttu-id="36385-109">Azure RemoteApp을 배포하는 경우 대부분 다른 Azure AD와 연결된 Azure 구독을 사용할 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="36385-109">If you are deploying Azure RemoteApp you are most likely using an Azure subscription that is associated with a different Azure AD.</span></span> <span data-ttu-id="36385-110">Office 365 디렉터리 toouse 순서, toomove hello 해당 디렉터리에 Azure 구독이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="36385-110">In order toouse your Office 365 directory, you will need toomove hello Azure subscription into that directory.</span></span>

<span data-ttu-id="36385-111">방법에 대 한 정보 toodeploy Office 365 클라이언트 응용 프로그램 참조 [어떻게 toouse Azure RemoteApp과 함께 Office 365 구독](remoteapp-officesubscription.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="36385-111">For info on how toodeploy Office 365 client applications, see [How toouse your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md).</span></span>

## <a name="phase-1-register-your-free-office-365-azure-active-directory-subscription"></a><span data-ttu-id="36385-112">단계 1: 무료 Office 365 Azure Active Directory 구독 등록</span><span class="sxs-lookup"><span data-stu-id="36385-112">Phase 1: Register your free Office 365 Azure Active Directory subscription</span></span>
<span data-ttu-id="36385-113">Hello Azure 클래식 포털을 사용 하는 경우의 hello 단계를 사용 하 여 [무료 Azure Active Directory 구독을 등록](https://technet.microsoft.com/library/dn832618.aspx) hello Azure 관리 포털을 통해 tooget 관리 액세스 tooyour Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36385-113">If you are using hello Azure classic portal, use hello steps in [Register your free Azure Active Directory subscription](https://technet.microsoft.com/library/dn832618.aspx) tooget administrative access tooyour Azure AD via hello Azure Management Portal.</span></span> <span data-ttu-id="36385-114">이 프로세스의 hello 결과로 hello Azure 포털에 수 toolog 수 해야 하며 디렉터리가 보이지 있습니다-이 시점에서 표시 되지 않습니다 훨씬 더 hello Azure RemoteApp과 함께 사용 하는 전체 Azure 구독에에서 있으므로 다른 디렉터리 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="36385-114">As hello result of this process you should be able toolog into hello Azure portal and see your directory there – at this point you won’t see much more since hello full Azure subscription you are using with Azure RemoteApp is in a different directory.</span></span>

<span data-ttu-id="36385-115">Hello 이름 및이 단계에서 만든 hello 관리자 계정의 암호를 기억 – 2 단계에서에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="36385-115">Remember hello name and password of hello administrator account you created in this step – they will be needed in Phase 2.</span></span>

<span data-ttu-id="36385-116">Hello Azure 포털을 사용 하는 경우 체크 아웃 [어떻게 tooregister Office 365 포털을 사용 하 여 무료 Azure Active Directory를 활성화 하 고](http://azureblogger.com/2016/01/how-to-register-and-activate-a-free-azure-active-directory-using-office-365-portal/)합니다.</span><span class="sxs-lookup"><span data-stu-id="36385-116">If you are using hello Azure portal, check out [How tooregister and activate a free Azure Active Directory using Office 365 portal](http://azureblogger.com/2016/01/how-to-register-and-activate-a-free-azure-active-directory-using-office-365-portal/).</span></span>

## <a name="phase-2-change-hello-azure-ad-associated-with-your-azure-subscription"></a><span data-ttu-id="36385-117">2 단계: Azure 구독과 연결 된 변경 hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36385-117">Phase 2: Change hello Azure AD associated with your Azure subscription.</span></span>
<span data-ttu-id="36385-118">하겠습니다 toochange Azure 구독에서 현재 디렉터리에서 1 단계에서에서 들과 협력 hello Office 365 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36385-118">We are going toochange your Azure subscription from its current directory into hello Office 365 directory we worked with in Phase 1.</span></span>

<span data-ttu-id="36385-119">에 설명 된 hello 지침에 따라 [변경 hello Azure Active Directory 테 넌 트 Azure RemoteApp에서](remoteapp-changetenant.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="36385-119">Follow hello instructions described in [Change hello Azure Active Directory tenant in Azure RemoteApp](remoteapp-changetenant.md).</span></span> <span data-ttu-id="36385-120">다음 단계는 특히 주의 toohello 비용을 지불 합니다.</span><span class="sxs-lookup"><span data-stu-id="36385-120">Pay particular attention toohello following steps:</span></span>

* <span data-ttu-id="36385-121">1단계: 이 구독에서 ARA(Azure RemoteApp)를 배포한 경우 계속 진행하기 전에 먼저 ARA 컬렉션에서 모든 Azure AD 사용자 계정을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36385-121">Step #1: If you have deployed Azure RemoteApp (ARA) in this subscription, make sure you remove all Azure AD user accounts from any ARA collections first, before trying anything else.</span></span> <span data-ttu-id="36385-122">또는 기존 컬렉션을 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36385-122">Alternatively, you can consider deleting any existing collections.</span></span>
* <span data-ttu-id="36385-123">2단계: 이 단계가 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="36385-123">Step #2: This is a critical step.</span></span> <span data-ttu-id="36385-124">Microsoft 계정 toouse 필요 (예: @outlook.com) hello 구독;에서 서비스 관리자로 때문에 이것이 이전 없는 경우 연결 된 Azure AD toohello 구독 – 기존 hello에서 모든 사용자 계정을 수 toomove 수 없습니다 것 tooa 다른 Azure Ad입니다.</span><span class="sxs-lookup"><span data-stu-id="36385-124">You need toouse a Microsoft account (e.g. @outlook.com) as a Service Administrator on hello subscription; this is because we cannot have any user accounts from hello existing Azure AD attached toohello subscription – if we do, we won’t be able toomove it tooa different Azure AD.</span></span>
* <span data-ttu-id="36385-125">#4 단계: 기존 디렉터리를 추가할 때 hello 시스템이 묻습니다 toosign hello 관리자 계정 사용 하 여 해당 디렉터리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="36385-125">Step #4: When adding an existing directory, hello system will ask you toosign in with hello administrator account for that directory.</span></span> <span data-ttu-id="36385-126">1 단계에서에서 toouse hello 관리자 계정이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="36385-126">Make sure toouse hello administrator account from Phase 1.</span></span>
* <span data-ttu-id="36385-127">5 단계: hello 구독 tooyour Office 365 디렉터리의 hello 부모 디렉터리를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="36385-127">Step #5: Change hello parent directory of hello subscription tooyour Office 365 directory.</span></span> <span data-ttu-id="36385-128">hello 최종 결과 설정에서-> 구독 구독 hello Office 365 디렉터리를 나열 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36385-128">hello end result should be that under Settings -> Subscriptions your subscription lists hello Office 365 directory.</span></span> 
  <span data-ttu-id="36385-129">![Hello 구독의 hello 부모 디렉터리를 변경 합니다.](./media/remoteapp-o365user/settings.png)</span><span class="sxs-lookup"><span data-stu-id="36385-129">![Change hello parent directory of hello subscription](./media/remoteapp-o365user/settings.png)</span></span>

<span data-ttu-id="36385-130">이 시점에서 Azure RemoteApp 구독에 Office 365; Azure AD와 연결 된 Azure RemoteApp과 함께 hello 기존 Office 365 사용자 계정을 사용할 수 있습니다!</span><span class="sxs-lookup"><span data-stu-id="36385-130">At this point your Azure RemoteApp subscription is associated with your Office 365 Azure AD; you can use hello existing Office 365 user accounts with Azure RemoteApp!</span></span>

