---
title: "Office 365 사용자 계정으로 Azure RemoteApp을 사용하는 방법 | Microsoft Docs"
description: "Office 365 사용자 계정으로 Azure RemoteApp을 사용하는 방법을 알아봅니다."
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
ms.openlocfilehash: 1bc8949c236afd03415f961cf7a657d4d3926b07
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-remoteapp-with-office-365-user-accounts"></a><span data-ttu-id="3dfca-103">Office 365 사용자 계정으로 Azure RemoteApp을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="3dfca-103">How to use Azure RemoteApp with Office 365 user accounts</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3dfca-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3dfca-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3dfca-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="3dfca-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3dfca-106">Office 365 구독이 있는 경우 Office 365 서비스에 액세스하는 데 사용되는 사용자 이름 및 암호를 저장하는 Azure Active Directory가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dfca-106">If you have an Office 365 subscription you have an Azure Active Directory that stores your user names and passwords used to access Office 365 services.</span></span> <span data-ttu-id="3dfca-107">예를 들어 사용자가 Office 365 ProPlus를 활성화하면 라이선스를 확인하기 위해 Azure AD에 대해 인증이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3dfca-107">For example, when your users activate Office 365 ProPlus they authenticate against Azure AD to check for licenses.</span></span> <span data-ttu-id="3dfca-108">대부분의 고객은 Azure RemoteApp과 동일한 디렉터리를 사용하기를 원합니다.</span><span class="sxs-lookup"><span data-stu-id="3dfca-108">Most customers would like to use the same directory with Azure RemoteApp.</span></span>

<span data-ttu-id="3dfca-109">Azure RemoteApp을 배포하는 경우 대부분 다른 Azure AD와 연결된 Azure 구독을 사용할 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="3dfca-109">If you are deploying Azure RemoteApp you are most likely using an Azure subscription that is associated with a different Azure AD.</span></span> <span data-ttu-id="3dfca-110">Office 365 디렉터리를 사용하려면 Azure 구독을 이 디렉터리로 이동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dfca-110">In order to use your Office 365 directory, you will need to move the Azure subscription into that directory.</span></span>

<span data-ttu-id="3dfca-111">Office 365 클라이언트 응용 프로그램을 배포하는 방법에 대한 자세한 내용은 [Azure RemoteApp으로 Office 365 구독을 사용하는 방법](remoteapp-officesubscription.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3dfca-111">For info on how to deploy Office 365 client applications, see [How to use your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md).</span></span>

## <a name="phase-1-register-your-free-office-365-azure-active-directory-subscription"></a><span data-ttu-id="3dfca-112">단계 1: 무료 Office 365 Azure Active Directory 구독 등록</span><span class="sxs-lookup"><span data-stu-id="3dfca-112">Phase 1: Register your free Office 365 Azure Active Directory subscription</span></span>
<span data-ttu-id="3dfca-113">Azure 클래식 포털을 사용하는 경우 [무료 Azure Active Directory 구독 등록](https://technet.microsoft.com/library/dn832618.aspx)의 단계에 따라 Azure 관리 포털을 통해 Azure AD에 대한 관리 액세스 권한을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="3dfca-113">If you are using the Azure classic portal, use the steps in [Register your free Azure Active Directory subscription](https://technet.microsoft.com/library/dn832618.aspx) to get administrative access to your Azure AD via the Azure Management Portal.</span></span> <span data-ttu-id="3dfca-114">이 프로세스를 완료하면 Azure 포털에 로그인하여 사용자의 디렉터리가 있는 것을 확인할 수 있습니다. 이 시점에서는 Azure RemoteApp과 함께 사용하는 전체 Azure 구독이 다른 디렉터리에 있으므로 다른 항목은 보이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3dfca-114">As the result of this process you should be able to log into the Azure portal and see your directory there – at this point you won’t see much more since the full Azure subscription you are using with Azure RemoteApp is in a different directory.</span></span>

<span data-ttu-id="3dfca-115">이 단계에서 만든 관리자 계정의 이름과 암호는 2단계에서 필요하므로 기억해 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dfca-115">Remember the name and password of the administrator account you created in this step – they will be needed in Phase 2.</span></span>

<span data-ttu-id="3dfca-116">Azure 포털을 사용하는 경우 [Office 365 포털을 사용하여 무료 Azure Active Directory를 등록 및 활성화하는 방법](http://azureblogger.com/2016/01/how-to-register-and-activate-a-free-azure-active-directory-using-office-365-portal/)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="3dfca-116">If you are using the Azure portal, check out [How to register and activate a free Azure Active Directory using Office 365 portal](http://azureblogger.com/2016/01/how-to-register-and-activate-a-free-azure-active-directory-using-office-365-portal/).</span></span>

## <a name="phase-2-change-the-azure-ad-associated-with-your-azure-subscription"></a><span data-ttu-id="3dfca-117">단계 2: Azure 구독과 연결된 Azure AD를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3dfca-117">Phase 2: Change the Azure AD associated with your Azure subscription.</span></span>
<span data-ttu-id="3dfca-118">Azure 구독의 현지 디렉터리를 1단계에서 작업한 Office 365 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3dfca-118">We are going to change your Azure subscription from its current directory into the Office 365 directory we worked with in Phase 1.</span></span>

<span data-ttu-id="3dfca-119">[Azure RemoteApp에서 Azure Active Directory 테넌트 변경](remoteapp-changetenant.md)에 설명된 지침을 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3dfca-119">Follow the instructions described in [Change the Azure Active Directory tenant in Azure RemoteApp](remoteapp-changetenant.md).</span></span> <span data-ttu-id="3dfca-120">다음 단계에 특히 주의합니다.</span><span class="sxs-lookup"><span data-stu-id="3dfca-120">Pay particular attention to the following steps:</span></span>

* <span data-ttu-id="3dfca-121">1단계: 이 구독에서 ARA(Azure RemoteApp)를 배포한 경우 계속 진행하기 전에 먼저 ARA 컬렉션에서 모든 Azure AD 사용자 계정을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dfca-121">Step #1: If you have deployed Azure RemoteApp (ARA) in this subscription, make sure you remove all Azure AD user accounts from any ARA collections first, before trying anything else.</span></span> <span data-ttu-id="3dfca-122">또는 기존 컬렉션을 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dfca-122">Alternatively, you can consider deleting any existing collections.</span></span>
* <span data-ttu-id="3dfca-123">2단계: 이 단계가 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="3dfca-123">Step #2: This is a critical step.</span></span> <span data-ttu-id="3dfca-124">구독에서 Microsoft 계정(예: @outlook.com을 서비스 관리자로 사용해야 합니다. 구독에 연결된 기존 Azure AD에서는 사용자 계정을 사용할 수 없기 때문입니다. 이 계정을 사용하는 경우 다른 Azure AD로 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3dfca-124">You need to use a Microsoft account (e.g. @outlook.com) as a Service Administrator on the subscription; this is because we cannot have any user accounts from the existing Azure AD attached to the subscription – if we do, we won’t be able to move it to a different Azure AD.</span></span>
* <span data-ttu-id="3dfca-125">4단계: 기존 디렉터리를 추가할 때 해당 디렉터리에 대한 관리자 계정으로 로그인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3dfca-125">Step #4: When adding an existing directory, the system will ask you to sign in with the administrator account for that directory.</span></span> <span data-ttu-id="3dfca-126">단계 1의 관리자 계정을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dfca-126">Make sure to use the administrator account from Phase 1.</span></span>
* <span data-ttu-id="3dfca-127">5단계: 구독의 부모 디렉터리를 Office 365 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3dfca-127">Step #5: Change the parent directory of the subscription to your Office 365 directory.</span></span> <span data-ttu-id="3dfca-128">그러면 설정 -> 구독 아래에 Office 365 디렉터리가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="3dfca-128">The end result should be that under Settings -> Subscriptions your subscription lists the Office 365 directory.</span></span> 
  <span data-ttu-id="3dfca-129">![구독의 부모 디렉터리 변경](./media/remoteapp-o365user/settings.png)</span><span class="sxs-lookup"><span data-stu-id="3dfca-129">![Change the parent directory of the subscription](./media/remoteapp-o365user/settings.png)</span></span>

<span data-ttu-id="3dfca-130">이제 Azure RemoteApp 구독이 Office 365 Azure AD와 연결되었습니다. Azure RemoteApp에서 기존 Office 365 사용자 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dfca-130">At this point your Azure RemoteApp subscription is associated with your Office 365 Azure AD; you can use the existing Office 365 user accounts with Azure RemoteApp!</span></span>

