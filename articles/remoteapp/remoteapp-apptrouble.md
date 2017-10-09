---
title: "RemoteApp 문제 해결-aaaAzure 응용 프로그램 실행 및 연결 오류 | Microsoft Docs"
description: "시작 주소와 연결 하는 Azure RemoteApp에서 tooapplications tootroubleshoot 발급 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: e51d480c9d3fa1f2076f95b63c7a8cd2f6956a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-remoteapp---application-launch-and-connection-failures"></a><span data-ttu-id="53bc8-103">Azure RemoteApp 문제 해결 - 응용 프로그램 시작 및 연결 실패</span><span class="sxs-lookup"><span data-stu-id="53bc8-103">Troubleshoot Azure RemoteApp - Application launch and connection failures</span></span>
> [!IMPORTANT]
> <span data-ttu-id="53bc8-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="53bc8-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="53bc8-106">Azure RemoteApp에서 호스팅되는 응용 프로그램은 몇 가지 다른 이유로 toolaunch를 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-106">Applications hosted in Azure RemoteApp can fail toolaunch for a few different reasons.</span></span> <span data-ttu-id="53bc8-107">이 문서에서는 다양 한 이유를 설명 하 고 오류 메시지 사용자 때 표시 될 수 toolaunch 응용 프로그램을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-107">This article describes various reasons and error messages users might receive when trying toolaunch applications.</span></span> <span data-ttu-id="53bc8-108">또한 연결 실패에 대해서도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-108">It also talks about connection failures.</span></span> <span data-ttu-id="53bc8-109">그러나 Azure RemoteApp 클라이언트 hello에 로그인 할 경우이 문서의 문제를 설명 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-109">(But this article does not describe issues when signing into hello Azure RemoteApp client.)</span></span>  

<span data-ttu-id="53bc8-110">Tooapp 시작 및 연결 오류 때문에 일반 오류 메시지에 대 한 내용은 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-110">Read on for information about common error messages due tooapp launch and connection failures.</span></span>

## <a name="were-getting-you-set-up-try-again-in-10-minutes"></a><span data-ttu-id="53bc8-111">설정 중입니다... 10분 후에 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="53bc8-111">We're getting you set up... Try again in 10 minutes.</span></span>
<span data-ttu-id="53bc8-112">이 오류는 Azure RemoteApp의 사용자 toomeet hello 용량 필요 확장은 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-112">This error means Azure RemoteApp is scaling up toomeet hello capacity need of your users.</span></span> <span data-ttu-id="53bc8-113">Hello 백그라운드에서 더 많은 Azure RemoteApp VM 인스턴스 사용자의 toohandle hello 용량 요구 만들고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-113">In hello background more Azure RemoteApp VM instances are being created toohandle hello capacity needs of your users.</span></span> <span data-ttu-id="53bc8-114">일반적으로이 분 정도 걸리지만 too10 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-114">Typically this takes around five minutes but can take up too10 minutes.</span></span> <span data-ttu-id="53bc8-115">경우에 따라 신속하게 진행되지 않아 즉시 리소스가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-115">Sometimes, this doesn't happen fast enough and resources are needed immediately.</span></span> <span data-ttu-id="53bc8-116">예를 들어 많은 필요한 toouse 이러한 앱에서 Azure RemoteAppn hello에서 오전 9 시 시나리오 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-116">For example a 9 AM scenario where many users need toouse your app in Azure RemoteAppn at hello same time.</span></span> <span data-ttu-id="53bc8-117">설정 가능 tooyou 이런 경우가 발생 하는 경우 **용량 모드** hello에 백 엔드 합니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-117">If this happens tooyou we can enable **capacity mode** on hello back end.</span></span> <span data-ttu-id="53bc8-118">이 열려 있는 한 Azure 지원 티켓 toodo 합니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-118">toodo this open an Azure Support ticket.</span></span> <span data-ttu-id="53bc8-119">특정 tooinclude hello 요청에서 구독 ID 수입니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-119">Be certain tooinclude your subscription ID in hello request.</span></span>  

![설정 중입니다.](./media/remoteapp-apptrouble/ra-apptrouble1.png)

## <a name="could-not-auto-reconnect-tooyour-applications-please-re-launch-your-application"></a><span data-ttu-id="53bc8-121">자동으로 다시 연결 하지 못했습니다 tooyour 응용 프로그램을 실행 하세요. 다시 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="53bc8-121">Could not auto-reconnect tooyour applications, please re-launch your application</span></span>
<span data-ttu-id="53bc8-122">Azure RemoteApp을 사용 하 던 하 고 다음 4 시간을 초과 하 여 PC toosleep를 입력 하 고 다음 절전 PC 모드에서 해제 하 고 hello Azure RemoteApp 클라이언트 시도 tooauto 다시 연결 하 고 제한 시간이 초과 되었습니다에 자주이 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-122">This error message is often seen if you were using Azure RemoteApp and then put your PC toosleep longer than 4 hours and then woke your PC up and hello Azure RemoteApp client attempt tooauto reconnect and timeout was exceeded.</span></span>  <span data-ttu-id="53bc8-123">사용자가 toonavigate 백 toohello 응용 프로그램에 지시 하 고 tooopen 시도 hello Azure RemoteApp 클라이언트에서.</span><span class="sxs-lookup"><span data-stu-id="53bc8-123">Instruct users toonavigate back toohello application and attempt tooopen it from hello Azure RemoteApp client.</span></span>

![자동으로 다시 연결 하지 못했습니다 tooyour 응용 프로그램](./media/remoteapp-apptrouble/ra-apptrouble2.png) 

## <a name="problems-with-hello-temp-profile"></a><span data-ttu-id="53bc8-125">임시 프로필 hello에 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-125">Problems with hello temp profile</span></span>
<span data-ttu-id="53bc8-126">이 오류는 사용자 프로필 (사용자 프로필 디스크) toomount를 실패 하 고 hello 사용자 임시 프로필을 받을 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-126">This error occurs when your user profile (User Profile Disk) failed toomount and hello user received a temporary profile.</span></span>  <span data-ttu-id="53bc8-127">관리자는 hello Azure 포털에서에서 toohello 컬렉션을 이동 하 고 이동 하 여 toohello **세션** 탭 및 너무 시도**로그 오프** hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-127">Administrators should navigate toohello collection in hello Azure portal and then go toohello **Sessions** tab and attempt too**Log Off** hello user.</span></span> <span data-ttu-id="53bc8-128">Hello 사용자 세션-오프 전체 로그를 강제로 후 다시 hello 사용자 시도 toolaunch 앱이 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-128">This will force a full log off of hello user session - then have hello user attempt toolaunch an app again.</span></span> <span data-ttu-id="53bc8-129">실패한 경우 Azure 지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="53bc8-129">If that fails contact Azure support.</span></span>

## <a name="azure-remoteapp-has-stopped-working"></a><span data-ttu-id="53bc8-130">Azure RemoteApp의 작동이 중지되었습니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-130">Azure RemoteApp has stopped working</span></span>
<span data-ttu-id="53bc8-131">이 오류 메시지는 hello Azure RemoteApp 클라이언트는 문제가 발생 하 고 toobe 다시 시작을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-131">This error message means hello Azure RemoteApp client is having an issue and needs toobe restarted.</span></span> <span data-ttu-id="53bc8-132">사용자가 tooclose 지시: 선택 **프로그램 닫기** 다음 hello Azure RemoteApp 클라이언트를 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-132">Instruct users tooclose: select **Close program** and then launch hello Azure RemoteApp client again.</span></span>  <span data-ttu-id="53bc8-133">Hello 문제가 열기 및 Azure 지원 티켓을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-133">If hello issue continues open and Azure Support ticket.</span></span>

![Azure RemoteApp의 작동이 중지되었습니다.](./media/remoteapp-apptrouble/ra-apptrouble3.png)  

## <a name="an-error-occurred-while-remote-desktop-connection-was-accessing-this-resource-retry-hello-connection-or-contact-your-system-administrator"></a><span data-ttu-id="53bc8-135">원격 데스크톱 연결이 이 리소스에 액세스하는 동안 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="53bc8-135">An error occurred while Remote Desktop Connection was accessing this resource.</span></span> <span data-ttu-id="53bc8-136">Hello 연결을 다시 시도 하거나 시스템 관리자에 게 문의</span><span class="sxs-lookup"><span data-stu-id="53bc8-136">Retry hello connection or contact your system administrator</span></span>
<span data-ttu-id="53bc8-137">일반 오류 메시지입니다. 조사할 수 있도록 Azure 지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="53bc8-137">This is a generic error message - contact Azure support so we can investigate.</span></span> 

![일반 Azure RemoteApp 메시지](./media/remoteapp-apptrouble/ra-apptrouble4.png) 

