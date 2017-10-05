---
title: "Azure 알림 허브 및 Node.js를 사용하여 푸시 알림 보내기"
description: "알림 허브를 사용하여 Node.js 응용 프로그램에 푸시 알림을 보내는 방법에 대해 알아봅니다."
keywords: "푸시 알림, 푸시 알림, node.js 푸시, ios 푸시"
services: notification-hubs
documentationcenter: nodejs
author: ysxu
manager: erikre
editor: 
ms.assetid: ded4749c-6c39-4ff8-b2cf-1927b3e92f93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 10/25/2016
ms.author: yuaxu
ms.openlocfilehash: dc4987b16b2e930641c6c90eff8b65c1bf8d573c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a><span data-ttu-id="f365a-104">Azure 알림 허브 및 Node.js를 사용하여 푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="f365a-104">Sending push notifications with Azure Notification Hubs and Node.js</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a><span data-ttu-id="f365a-105">개요</span><span class="sxs-lookup"><span data-stu-id="f365a-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f365a-106">이 자습서를 완료하려면 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="f365a-107">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f365a-108">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f365a-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span></span>
> 
> 

<span data-ttu-id="f365a-109">이 가이드에서는 Node.js 응용 프로그램에서 직접 Azure 알림 허브의 도움말을 사용하여 푸시 알림을 보내는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-109">This guide will show you how to send push notifications with the help of Azure Notification Hubs directly from a Node.js application.</span></span> 

<span data-ttu-id="f365a-110">시나리오는 다음 플랫폼에서 응용 프로그램에 푸시 알림을 보내기를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-110">The scenarios covered include sending push notifications to applications on the following platforms:</span></span>

* <span data-ttu-id="f365a-111">Android</span><span class="sxs-lookup"><span data-stu-id="f365a-111">Android</span></span>
* <span data-ttu-id="f365a-112">iOS</span><span class="sxs-lookup"><span data-stu-id="f365a-112">iOS</span></span>
* <span data-ttu-id="f365a-113">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="f365a-113">Windows Phone</span></span>
* <span data-ttu-id="f365a-114">범용 Windows 플랫폼</span><span class="sxs-lookup"><span data-stu-id="f365a-114">Universal Windows Platform</span></span> 

<span data-ttu-id="f365a-115">알림 허브에 대한 자세한 내용은 [다음 단계](#next) 섹션을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="f365a-115">For more information on notification hubs, see the [Next Steps](#next) section.</span></span>

## <a name="what-are-notification-hubs"></a><span data-ttu-id="f365a-116">알림 허브 정의</span><span class="sxs-lookup"><span data-stu-id="f365a-116">What are Notification Hubs?</span></span>
<span data-ttu-id="f365a-117">Azure 알림 허브는 모바일 장치에 푸시 알림을 보내는 사용하기 쉽고 확장성 있는 다중 플랫폼 인프라를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-117">Azure Notification Hubs provide an easy-to-use, multi-platform, scalable infrastructure for sending push notifications to mobile devices.</span></span> <span data-ttu-id="f365a-118">서비스 인프라에 대한 세부 정보는 [Azure 알림 허브](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f365a-118">For details on the service infrastructure, see the [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) page.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="f365a-119">Node.js 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="f365a-119">Create a Node.js Application</span></span>
<span data-ttu-id="f365a-120">이 자습서의 첫 번째 단계는 새로운 빈 Node.js 응용 프로그램을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-120">The first step in this tutorial is creating a new blank Node.js application.</span></span> <span data-ttu-id="f365a-121">Node.js 응용 프로그램을 만드는 방법에 대한 지침은 [Node.js 응용 프로그램을 만들어 Azure 웹 사이트에 배포][nodejswebsite], Windows PowerShell을 사용한 [Node.js 클라우드 서비스][Node.js Cloud Service] 또는 [WebMatrix를 사용하는 웹 사이트]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f365a-121">For instructions on creating a Node.js application, see [Create and deploy a Node.js application to Azure Web Site][nodejswebsite], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or [Web Site with WebMatrix].</span></span>

## <a name="configure-your-application-to-use-notification-hubs"></a><span data-ttu-id="f365a-122">알림 허브를 사용하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="f365a-122">Configure Your Application to Use Notification Hubs</span></span>
<span data-ttu-id="f365a-123">Azure 알림 허브를 사용하려면 푸시 알림 REST 라이브러리와 통신하는 일련의 기본 제공 도우미 라이브러리가 포함되어 있는 Node.js [Azure 패키지](https://www.npmjs.com/package/azure)를 다운로드하여 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-123">To use Azure Notification Hubs, you need to download and use the Node.js [azure package](https://www.npmjs.com/package/azure), which includes a built-in set of helper libraries that communicate with the push notification REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="f365a-124">NPM(Node Package Manager)을 사용하여 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="f365a-124">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="f365a-125">**PowerShell**(Windows), **Terminal**(Mac), **Bash**(Linux) 등과 같은 명령줄 인터페이스를 사용하여 빈 응용 프로그램을 만든 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-125">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Linux) and navigate to the folder where you created your blank application.</span></span>
2. <span data-ttu-id="f365a-126">명령 창에 **npm install azure-sb** 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-126">Type **npm install azure-sb** in the command window.</span></span>
3. <span data-ttu-id="f365a-127">**ls** 또는 **dir** 명령을 수동으로 실행하여 **node\_modules** 폴더가 만들어졌는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-127">You can manually run the **ls** or **dir** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="f365a-128">이 폴더에서 알림 허브에 액세스하는 데 필요한 라이브러리가 들어 있는 **Azure** 패키지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-128">Inside that folder, find the **azure** package, which contains the libraries you need to access the Notification Hub.</span></span>

> [!NOTE]
> <span data-ttu-id="f365a-129">자세한 내용은 공식 [NPM 블로그](http://blog.npmjs.org/post/85484771375/how-to-install-npm)에서 NPM 설치에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-129">You can learn more about installing NPM on the official [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span></span> 
> 
> 

### <a name="import-the-module"></a><span data-ttu-id="f365a-130">모듈 가져오기</span><span class="sxs-lookup"><span data-stu-id="f365a-130">Import the module</span></span>
<span data-ttu-id="f365a-131">텍스트 편집기를 사용하여 다음을 응용 프로그램의 **server.js** 파일 맨 위에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-131">Using a text editor, add the following to the top of the **server.js** file of the application:</span></span>

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a><span data-ttu-id="f365a-132">Azure 알림 허브 연결 설정</span><span class="sxs-lookup"><span data-stu-id="f365a-132">Setup an Azure Notification Hub connection</span></span>
<span data-ttu-id="f365a-133">**NotificationHubService** 개체를 사용하면 허브 알림으로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-133">The **NotificationHubService** object lets you work with notification hubs.</span></span> <span data-ttu-id="f365a-134">다음 코드는 **hubname** 알림 허브에 대한 **NotificationHubService** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-134">The following code creates a **NotificationHubService** object for the nofication hub named **hubname**.</span></span> <span data-ttu-id="f365a-135">이 코드를 **server.js** 파일의 위쪽, Azure 모듈을 가져오기 위한 문 뒤에 추가하십시오.</span><span class="sxs-lookup"><span data-stu-id="f365a-135">Add it near the top of the **server.js** file, after the statement to import the azure module:</span></span>

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

<span data-ttu-id="f365a-136">다음 단계를 수행하여 **Azure 포털** 에서 [connectionstring] 연결 값을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-136">The connection **connectionstring** value can be obtained from the [Azure Portal] by performing the following steps:</span></span>

1. <span data-ttu-id="f365a-137">왼쪽 탐색 창에서 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-137">In the left navigation pane, click **Browse**.</span></span>
2. <span data-ttu-id="f365a-138">**알림 허브**를 선택한 다음 샘플로 사용하려는 허브를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-138">Select **Notification Hubs**, and then find the hub you wish to use for the sample.</span></span> <span data-ttu-id="f365a-139">새 알림 허브를 만드는 데 도움이 필요한 경우 [Windows 스토어 시작 자습서](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) 를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-139">You can refer to the [Windows Store Getting Started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) if you need help creating a new Notification Hub.</span></span>
3. <span data-ttu-id="f365a-140">**설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-140">Select **Settings**.</span></span>
4. <span data-ttu-id="f365a-141">**액세스 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-141">Click on **Access Policies**.</span></span> <span data-ttu-id="f365a-142">공유 및 전체 액세스 연결 문자열이 모두 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-142">You will see both shared and full access connection strings.</span></span>

![Azure 포털 - 알림 허브](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> <span data-ttu-id="f365a-144">[Azure PowerShell](/powershell/azureps-cmdlets-docs)에서 제공하는 **Get-AzureSbNamespace** cmdlet 또는 [Azure CLI(Azure 명령줄 인터페이스)](../cli-install-nodejs.md)로 **azure sb namespace show** 명령을 사용하여 연결 문자열을 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-144">You can also retrieve the connection string using the **Get-AzureSbNamespace** cmdlet provided by [Azure PowerShell](/powershell/azureps-cmdlets-docs) or the **azure sb namespace show** command with the [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md).</span></span>
> 
> 

## <a name="general-architecture"></a><span data-ttu-id="f365a-145">일반 아키텍처</span><span class="sxs-lookup"><span data-stu-id="f365a-145">General architecture</span></span>
<span data-ttu-id="f365a-146">**NotificationHubService** 개체는 특정 장치 및 응용 프로그램에 푸시 알림을 보내는 다음 개체 인스턴스를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-146">The **NotificationHubService** object exposes the following object instances for sending push notifications to specific devices and applications:</span></span>

* <span data-ttu-id="f365a-147">**Android** - **notificationHubService.gcm**에서 제공되는 **GcmService** 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-147">**Android** - use the **GcmService** object, which is available at **notificationHubService.gcm**</span></span>
* <span data-ttu-id="f365a-148">**iOS** - **notificationHubService.apns**에서 액세스할 수 있는 **ApnsService** 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-148">**iOS** - use the **ApnsService** object, which is accessible at **notificationHubService.apns**</span></span>
* <span data-ttu-id="f365a-149">**Windows Phone** - **notificationHubService.mpns**에서 제공되는 **MpnsService** 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-149">**Windows Phone** - use the **MpnsService** object, which is available at **notificationHubService.mpns**</span></span>
* <span data-ttu-id="f365a-150">**유니버설 Windows 플랫폼** - **notificationHubService.wns**에서 제공되는 **WnsService** 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-150">**Universal Windows Platform** - use the **WnsService** object, which is available at **notificationHubService.wns**</span></span>

### <a name="how-to-send-push-notifications-to-android-applications"></a><span data-ttu-id="f365a-151">방법: Android 응용 프로그램에 푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="f365a-151">How to: Send push notifications to Android applications</span></span>
<span data-ttu-id="f365a-152">**GcmService** 개체는 Android 응용 프로그램에 푸시 알림을 보내는 데 사용할 수 있는 **보내기** 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-152">The **GcmService** object provides a **send** method that can be used to send push notifications to Android applications.</span></span> <span data-ttu-id="f365a-153">**send** 메서드는 다음 매개 변수를 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-153">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="f365a-154">**Tags** - 태그 식별자.</span><span class="sxs-lookup"><span data-stu-id="f365a-154">**Tags** - the tag identifier.</span></span> <span data-ttu-id="f365a-155">태그를 제공하지 않은 경우 모든 클라이언트에게 알림이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-155">If no tag is provided, the notification will be sent to all clients.</span></span>
* <span data-ttu-id="f365a-156">**Payload** - 메시지의 JSON 또는 원시 문자열 페이로드</span><span class="sxs-lookup"><span data-stu-id="f365a-156">**Payload** - the message's JSON or raw string payload.</span></span>
* <span data-ttu-id="f365a-157">**Callback** - 콜백 함수.</span><span class="sxs-lookup"><span data-stu-id="f365a-157">**Callback** - the callback function.</span></span>

<span data-ttu-id="f365a-158">페이로드 형식에 대한 자세한 내용은 **GCM 서버 구현** 문서의 [페이로드](http://developer.android.com/google/gcm/server.html#payload) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f365a-158">For more information on the payload format, see the **Payload** section of the [Implementing GCM Server](http://developer.android.com/google/gcm/server.html#payload) document.</span></span>

<span data-ttu-id="f365a-159">다음 코드는 **NotificationHubService**에 의해 노출되는 **GcmService** 인스턴스를 사용하여 모든 등록된 클라이언트에 푸시 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-159">The following code uses the **GcmService** instance exposed by the **NotificationHubService** to send a push notification to all registered clients.</span></span>

    var payload = {
      data: {
        message: 'Hello!'
      }
    };
    notificationHubService.gcm.send(null, payload, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-ios-applications"></a><span data-ttu-id="f365a-160">방법: iOS 응용 프로그램에 푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="f365a-160">How to: Send push notifications to iOS applications</span></span>
<span data-ttu-id="f365a-161">위에서 설명한 Android 응용 프로그램과 동일하게 **ApnsService** 개체는 iOS 응용 프로그램에 알림을 보내는 데 사용할 수 있는 **보내기** 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-161">Same as with Android applications described above, the **ApnsService** object provides a **send** method that can be used to send push notifications to iOS applications.</span></span> <span data-ttu-id="f365a-162">**send** 메서드는 다음 매개 변수를 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-162">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="f365a-163">**Tags** - 태그 식별자.</span><span class="sxs-lookup"><span data-stu-id="f365a-163">**Tags** - the tag identifier.</span></span> <span data-ttu-id="f365a-164">태그를 제공하지 않은 경우 모든 클라이언트에게 알림이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-164">If no tag is provided, the notification will be sent to all clients.</span></span>
* <span data-ttu-id="f365a-165">**Payload** - 메시지의 JSON 또는 문자열 페이로드</span><span class="sxs-lookup"><span data-stu-id="f365a-165">**Payload** - the message's JSON or string payload.</span></span>
* <span data-ttu-id="f365a-166">**Callback** - 콜백 함수.</span><span class="sxs-lookup"><span data-stu-id="f365a-166">**Callback** - the callback function.</span></span>

<span data-ttu-id="f365a-167">페이로드 형식에 대한 자세한 내용은 **로컬 및 푸시 알림 프로그래밍 가이드** 문서의 [알림 페이로드](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f365a-167">For more information the payload format, see The **Notification Payload** section of the [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.</span></span>

<span data-ttu-id="f365a-168">다음 코드는 **NotificationHubService**에 의해 표시되는 **ApnsService** 인스턴스를 사용하여 모든 클라이언트에 경고 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-168">The following code uses the **ApnsService** instance exposed by the **NotificationHubService** to send an alert message to all clients:</span></span>

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-windows-phone-applications"></a><span data-ttu-id="f365a-169">방법: Windows Phone 응용 프로그램에 푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="f365a-169">How to: Send push notifications to Windows Phone applications</span></span>
<span data-ttu-id="f365a-170">**MpnsService** 개체는 Windows Phone 응용 프로그램에 푸시 알림을 보내는 데 사용할 수 있는 **보내기** 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-170">The **MpnsService** object provides a **send** method that can be used to send push notifications to Windows Phone applications.</span></span> <span data-ttu-id="f365a-171">**send** 메서드는 다음 매개 변수를 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-171">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="f365a-172">**Tags** - 태그 식별자.</span><span class="sxs-lookup"><span data-stu-id="f365a-172">**Tags** - the tag identifier.</span></span> <span data-ttu-id="f365a-173">태그를 제공하지 않은 경우 모든 클라이언트에게 알림이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-173">If no tag is provided, the notification will be sent to all clients.</span></span>
* <span data-ttu-id="f365a-174">**Payload** - 메시지의 XML 페이로드</span><span class="sxs-lookup"><span data-stu-id="f365a-174">**Payload** - the message's XML payload.</span></span>
* <span data-ttu-id="f365a-175">**TargetName** - `toast` - 알림 메시지인 경우.</span><span class="sxs-lookup"><span data-stu-id="f365a-175">**TargetName** - `toast` for toast notifications.</span></span> <span data-ttu-id="f365a-176">`token` - 타일 알림 메시지인 경우.</span><span class="sxs-lookup"><span data-stu-id="f365a-176">`token` for tile notifications.</span></span>
* <span data-ttu-id="f365a-177">**NotificationClass** - 알림 우선 순위.</span><span class="sxs-lookup"><span data-stu-id="f365a-177">**NotificationClass** - The priority of the notification.</span></span> <span data-ttu-id="f365a-178">유효한 값은 **서버에서 푸시 알림** 문서의 [HTTP 헤더 요소](http://msdn.microsoft.com/library/hh221551.aspx) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f365a-178">See the **HTTP Header Elements** section of the [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) document for valid values.</span></span>
* <span data-ttu-id="f365a-179">**Options** - 선택적 요청 헤더</span><span class="sxs-lookup"><span data-stu-id="f365a-179">**Options** - optional request headers.</span></span>
* <span data-ttu-id="f365a-180">**Callback** - 콜백 함수.</span><span class="sxs-lookup"><span data-stu-id="f365a-180">**Callback** - the callback function.</span></span>

<span data-ttu-id="f365a-181">유효한 **TargetName**, **NotificationClass** 및 헤더 옵션 목록은 [서버의 푸시 알림](http://msdn.microsoft.com/library/hh221551.aspx) 페이지를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f365a-181">For a list of valid **TargetName**, **NotificationClass** and header options, check out the [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) page.</span></span>

<span data-ttu-id="f365a-182">다음 샘플 코드는 **NotificationHubService**에 의해 노출되는 **MpnsService** 인스턴스를 사용하여 알림 푸시 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-182">The following sample code uses the **MpnsService** instance exposed by the **NotificationHubService** to send a toast push notification:</span></span>

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-universal-windows-platform-uwp-applications"></a><span data-ttu-id="f365a-183">방법: UWP(범용 Windows 플랫폼) 응용 프로그램에 푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="f365a-183">How to: Send push notifications to Universal Windows Platform (UWP) applications</span></span>
<span data-ttu-id="f365a-184">**WnsService** 개체는 유니버설 Windows 플랫폼 응용 프로그램에 푸시 알림을 보내는 데 사용할 수 있는 **send** 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-184">The **WnsService** object provides a **send** method that can be used to send push notifications to Universal Windows Platform applications.</span></span>  <span data-ttu-id="f365a-185">**send** 메서드는 다음 매개 변수를 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-185">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="f365a-186">**Tags** - 태그 식별자.</span><span class="sxs-lookup"><span data-stu-id="f365a-186">**Tags** - the tag identifier.</span></span> <span data-ttu-id="f365a-187">태그를 제공하지 않은 경우 모든 등록된 클라이언트에게 알림이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-187">If no tag is provided, the notification will be sent to all registered clients.</span></span>
* <span data-ttu-id="f365a-188">**Payload** - XML 메시지 페이로드</span><span class="sxs-lookup"><span data-stu-id="f365a-188">**Payload** - the XML message payload.</span></span>
* <span data-ttu-id="f365a-189">**Type** - 알림 유형</span><span class="sxs-lookup"><span data-stu-id="f365a-189">**Type** - the notification type.</span></span>
* <span data-ttu-id="f365a-190">**Options** - 선택적 요청 헤더</span><span class="sxs-lookup"><span data-stu-id="f365a-190">**Options** - optional request headers.</span></span>
* <span data-ttu-id="f365a-191">**Callback** - 콜백 함수.</span><span class="sxs-lookup"><span data-stu-id="f365a-191">**Callback** - the callback function.</span></span>

<span data-ttu-id="f365a-192">유효한 유형 및 요청 헤더 목록은 [푸시 알림 서비스 요청 및 응답 헤더](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f365a-192">For a list of valid types and request headers, see [Push notification service request and response headers](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span></span>

<span data-ttu-id="f365a-193">다음 코드는 **NotificationHubService**에 의해 노출되는 **WnsService** 인스턴스를 사용하여 UWP 앱에 알림 푸시 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-193">The following code uses the **WnsService** instance exposed by the **NotificationHubService** to send a toast push notification to a UWP app:</span></span>

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a><span data-ttu-id="f365a-194">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f365a-194">Next Steps</span></span>
<span data-ttu-id="f365a-195">위의 샘플 코드 조각을 사용하면 다양한 장치에 푸시 알림을 전달하는 서비스 인프라를 쉽게 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-195">The sample snippets above allow you to easily build service infrastructure to deliver push notifications to a wide variety of devices.</span></span> <span data-ttu-id="f365a-196">이제 node.js가 있는 알림 허브를 사용하는 기본 사항을 배웠으므로 다음 링크를 따라서 이러한 기능을 더욱 확장할 수 있는 방법에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-196">Now that you've learned the basics of using Notification Hubs with node.js, follow these links to learn more about how you can extend these capabilities further.</span></span>

* <span data-ttu-id="f365a-197">[Azure 알림 허브](https://msdn.microsoft.com/library/azure/jj927170.aspx)는 MSDN 참조를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f365a-197">See the MSDN Reference for [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span></span>
* <span data-ttu-id="f365a-198">추가 샘플 및 구현 세부 정보는 GitHub에서 [Node용 Azure SDK] 리포지토리를 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="f365a-198">Visit the [Azure SDK for Node] repository on GitHub for more samples and implementation details.</span></span>

<span data-ttu-id="f365a-199">[Node용 Azure SDK]: https://github.com/WindowsAzure/azure-sdk-for-node</span><span class="sxs-lookup"><span data-stu-id="f365a-199">[Azure SDK for Node]: https://github.com/WindowsAzure/azure-sdk-for-node</span></span>
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain the Default Management Credentials for the Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application to Use Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages to a Topic]: #How_to_Send_Messages_to_a_Topic
[How to: Receive Messages from a Subscription]: #How_to_Receive_Messages_from_a_Subscription
[How to: Handle Application Crashes and Unreadable Messages]: #How_to_Handle_Application_Crashes_and_Unreadable_Messages
[How to: Delete Topics and Subscriptions]: #How_to_Delete_Topics_and_Subscriptions
[1]: #Next_Steps
[Topic Concepts]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-topics-01.png
[Azure Classic Portal]: http://manage.windowsazure.com
[image]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-03.png
[2]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-04.png
[3]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-05.png
[4]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-06.png
[5]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-07.png
[SqlFilter.SqlExpression]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx
[Azure Service Bus Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/jj927170.aspx
[SqlFilter]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.aspx
<span data-ttu-id="f365a-200">[WebMatrix를 사용하는 웹 사이트]: /develop/nodejs/tutorials/web-site-with-webmatrix/</span><span class="sxs-lookup"><span data-stu-id="f365a-200">[Web Site with WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/</span></span>
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
<span data-ttu-id="f365a-201">[connectionstring]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="f365a-201">[Azure Portal]: https://portal.azure.com</span></span>
