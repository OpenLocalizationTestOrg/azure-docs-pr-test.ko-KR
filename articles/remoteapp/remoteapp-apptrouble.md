---
title: "Azure RemoteApp 문제 해결 - 응용 프로그램 시작 및 연결 실패 | Microsoft 문서"
description: "Azure RemoteApp의 응용 프로그램 시작 및 연결 문제에 대한 해결 방법을 알아봅니다."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e5cf7171-d1c2-4053-a38b-5af7821305e1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: fc9d538991adce7fc13e9654b9a7c6d113d03fde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-remoteapp---application-launch-and-connection-failures"></a><span data-ttu-id="67381-103">Azure RemoteApp 문제 해결 - 응용 프로그램 시작 및 연결 실패</span><span class="sxs-lookup"><span data-stu-id="67381-103">Troubleshoot Azure RemoteApp - Application launch and connection failures</span></span>
> [!IMPORTANT]
> <span data-ttu-id="67381-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="67381-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="67381-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="67381-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="67381-106">Azure RemoteApp에 호스트되는 응용 프로그램은 몇 가지 이유로 시작에 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67381-106">Applications hosted in Azure RemoteApp can fail to launch for a few different reasons.</span></span> <span data-ttu-id="67381-107">이 문서에서는 다양한 이유와 사용자가 응용 프로그램을 시작하려고 할 때 나타날 수 있는 오류 메시지에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="67381-107">This article describes various reasons and error messages users might receive when trying to launch applications.</span></span> <span data-ttu-id="67381-108">또한 연결 실패에 대해서도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="67381-108">It also talks about connection failures.</span></span> <span data-ttu-id="67381-109">그러나 Azure RemoteApp 클라이언트에 로그인할 때 발생하는 문제에 대해서는 이 문서에서 설명하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67381-109">(But this article does not describe issues when signing into the Azure RemoteApp client.)</span></span>  

<span data-ttu-id="67381-110">앱 시작 및 연결 실패로 인한 일반 오류 메시지에 대한 정보를 읽어 보세요.</span><span class="sxs-lookup"><span data-stu-id="67381-110">Read on for information about common error messages due to app launch and connection failures.</span></span>

## <a name="were-getting-you-set-up-try-again-in-10-minutes"></a><span data-ttu-id="67381-111">설정 중입니다... 10분 후에 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="67381-111">We're getting you set up... Try again in 10 minutes.</span></span>
<span data-ttu-id="67381-112">이 오류는 Azure RemoteApp이 사용자의 용량 요구에 맞게 확장되고 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="67381-112">This error means Azure RemoteApp is scaling up to meet the capacity need of your users.</span></span> <span data-ttu-id="67381-113">백그라운드에서는 더 많은 Azure RemoteApp VM 인스턴스가 사용자의 용량 요구 사항을 처리하기 위해 만들어지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67381-113">In the background more Azure RemoteApp VM instances are being created to handle the capacity needs of your users.</span></span> <span data-ttu-id="67381-114">일반적으로 5분 정도 걸리지만 최대 10분까지 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67381-114">Typically this takes around five minutes but can take up to 10 minutes.</span></span> <span data-ttu-id="67381-115">경우에 따라 신속하게 진행되지 않아 즉시 리소스가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67381-115">Sometimes, this doesn't happen fast enough and resources are needed immediately.</span></span> <span data-ttu-id="67381-116">예를 들어 오전 9시에 많은 사용자가 동시에 Azure RemoteAppn에서 앱을 사용해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67381-116">For example a 9 AM scenario where many users need to use your app in Azure RemoteAppn at the same time.</span></span> <span data-ttu-id="67381-117">이 경우 백 엔드에서 **용량 모드** 를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67381-117">If this happens to you we can enable **capacity mode** on the back end.</span></span> <span data-ttu-id="67381-118">이렇게 하려면 Azure 지원 티켓을 여세요.</span><span class="sxs-lookup"><span data-stu-id="67381-118">To do this open an Azure Support ticket.</span></span> <span data-ttu-id="67381-119">요청에는 반드시 구독 ID를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67381-119">Be certain to include your subscription ID in the request.</span></span>  

![설정 중입니다.](./media/remoteapp-apptrouble/ra-apptrouble1.png)

## <a name="could-not-auto-reconnect-to-your-applications-please-re-launch-your-application"></a><span data-ttu-id="67381-121">응용 프로그램에 자동으로 다시 연결할 수 없습니다. 응용 프로그램을 다시 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="67381-121">Could not auto-reconnect to your applications, please re-launch your application</span></span>
<span data-ttu-id="67381-122">이 오류 메시지는 Azure RemoteApp 사용 중 4시간 이상 절전 모드 상태였던 PC의 절전 상태를 해제하고, Azure RemoteApp 클라이언트에서 자동으로 다시 연결을 시도하고, 시간 제한이 초과될 때 자주 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="67381-122">This error message is often seen if you were using Azure RemoteApp and then put your PC to sleep longer than 4 hours and then woke your PC up and the Azure RemoteApp client attempt to auto reconnect and timeout was exceeded.</span></span>  <span data-ttu-id="67381-123">사용자에게 응용 프로그램으로 다시 돌아와서 Azure RemoteApp 클라이언트에서 열도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="67381-123">Instruct users to navigate back to the application and attempt to open it from the Azure RemoteApp client.</span></span>

![응용 프로그램에 자동으로 다시 연결할 수 없습니다.](./media/remoteapp-apptrouble/ra-apptrouble2.png) 

## <a name="problems-with-the-temp-profile"></a><span data-ttu-id="67381-125">임시 프로필 문제</span><span class="sxs-lookup"><span data-stu-id="67381-125">Problems with the temp profile</span></span>
<span data-ttu-id="67381-126">이 오류는 사용자 프로필(사용자 프로필 디스크)을 탑재하지 못하여 사용자가 임시 프로필을 받을 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="67381-126">This error occurs when your user profile (User Profile Disk) failed to mount and the user received a temporary profile.</span></span>  <span data-ttu-id="67381-127">관리자는 Azure Portal에서 컬렉션으로 이동한 다음 **세션** 탭으로 이동하고 사용자를 **로그오프**해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67381-127">Administrators should navigate to the collection in the Azure portal and then go to the **Sessions** tab and attempt to **Log Off** the user.</span></span> <span data-ttu-id="67381-128">이렇게 하면 사용자 세션이 완전히 로그오프되어 사용자가 앱을 다시 실행할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67381-128">This will force a full log off of the user session - then have the user attempt to launch an app again.</span></span> <span data-ttu-id="67381-129">실패한 경우 Azure 지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="67381-129">If that fails contact Azure support.</span></span>

## <a name="azure-remoteapp-has-stopped-working"></a><span data-ttu-id="67381-130">Azure RemoteApp의 작동이 중지되었습니다.</span><span class="sxs-lookup"><span data-stu-id="67381-130">Azure RemoteApp has stopped working</span></span>
<span data-ttu-id="67381-131">이 오류 메시지는 Azure RemoteApp 클라이언트에 문제가 있어 다시 시작해야 함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="67381-131">This error message means the Azure RemoteApp client is having an issue and needs to be restarted.</span></span> <span data-ttu-id="67381-132">사용자에게 닫도록 지시합니다. **프로그램 닫기**를 선택한 다음 Azure RemoteApp 클라이언트를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="67381-132">Instruct users to close: select **Close program** and then launch the Azure RemoteApp client again.</span></span>  <span data-ttu-id="67381-133">문제가 계속 발생하면 Azure 지원 티켓을 여세요.</span><span class="sxs-lookup"><span data-stu-id="67381-133">If the issue continues open and Azure Support ticket.</span></span>

![Azure RemoteApp의 작동이 중지되었습니다.](./media/remoteapp-apptrouble/ra-apptrouble3.png)  

## <a name="an-error-occurred-while-remote-desktop-connection-was-accessing-this-resource-retry-the-connection-or-contact-your-system-administrator"></a><span data-ttu-id="67381-135">원격 데스크톱 연결이 이 리소스에 액세스하는 동안 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="67381-135">An error occurred while Remote Desktop Connection was accessing this resource.</span></span> <span data-ttu-id="67381-136">연결을 다시 시도하거나 시스템 관리자에게 문의하십시오.</span><span class="sxs-lookup"><span data-stu-id="67381-136">Retry the connection or contact your system administrator</span></span>
<span data-ttu-id="67381-137">일반 오류 메시지입니다. 조사할 수 있도록 Azure 지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="67381-137">This is a generic error message - contact Azure support so we can investigate.</span></span> 

![일반 Azure RemoteApp 메시지](./media/remoteapp-apptrouble/ra-apptrouble4.png) 

