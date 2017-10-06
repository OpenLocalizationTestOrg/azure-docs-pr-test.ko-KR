---
title: "Azure 알림 허브 및 Node.js를 사용 하 여 aaaSending 푸시 알림"
description: "Toouse 알림 허브 toosend Node.js 응용 프로그램에서 알림을 강제 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 151d224fa6dd07e4acdc3a4887c4e95ee03168c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a><span data-ttu-id="59466-104">Azure 알림 허브 및 Node.js를 사용하여 푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="59466-104">Sending push notifications with Azure Notification Hubs and Node.js</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a><span data-ttu-id="59466-105">개요</span><span class="sxs-lookup"><span data-stu-id="59466-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="59466-106">toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59466-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="59466-107">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59466-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="59466-108">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59466-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span></span>
> 
> 

<span data-ttu-id="59466-109">이 가이드는 Node.js 응용 프로그램에서 직접 toosend Azure 알림 허브의 hello 도움말을 사용 하 여 알림을 푸시 방법을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59466-109">This guide will show you how toosend push notifications with hello help of Azure Notification Hubs directly from a Node.js application.</span></span> 

<span data-ttu-id="59466-110">가이드에서 다루는 hello 시나리오 hello 다음 플랫폼에 푸시 알림을 tooapplications 보내는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="59466-110">hello scenarios covered include sending push notifications tooapplications on hello following platforms:</span></span>

* <span data-ttu-id="59466-111">Android</span><span class="sxs-lookup"><span data-stu-id="59466-111">Android</span></span>
* <span data-ttu-id="59466-112">iOS</span><span class="sxs-lookup"><span data-stu-id="59466-112">iOS</span></span>
* <span data-ttu-id="59466-113">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="59466-113">Windows Phone</span></span>
* <span data-ttu-id="59466-114">범용 Windows 플랫폼</span><span class="sxs-lookup"><span data-stu-id="59466-114">Universal Windows Platform</span></span> 

<span data-ttu-id="59466-115">알림 허브에 대 한 자세한 내용은 참조 hello [다음 단계](#next) 섹션.</span><span class="sxs-lookup"><span data-stu-id="59466-115">For more information on notification hubs, see hello [Next Steps](#next) section.</span></span>

## <a name="what-are-notification-hubs"></a><span data-ttu-id="59466-116">알림 허브 정의</span><span class="sxs-lookup"><span data-stu-id="59466-116">What are Notification Hubs?</span></span>
<span data-ttu-id="59466-117">Azure 알림 허브 푸시 알림을 toomobile 장치 보내기 위한 사용 하기 쉬운, 다중 플랫폼, 확장 가능한 인프라를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="59466-117">Azure Notification Hubs provide an easy-to-use, multi-platform, scalable infrastructure for sending push notifications toomobile devices.</span></span> <span data-ttu-id="59466-118">에 대 한 내용은 hello 서비스 인프라를 hello 참조 [Azure 알림 허브](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) 페이지.</span><span class="sxs-lookup"><span data-stu-id="59466-118">For details on hello service infrastructure, see hello [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) page.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="59466-119">Node.js 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="59466-119">Create a Node.js Application</span></span>
<span data-ttu-id="59466-120">이 자습서의 첫 번째 단계 hello 새 빈 Node.js 응용 프로그램을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="59466-120">hello first step in this tutorial is creating a new blank Node.js application.</span></span> <span data-ttu-id="59466-121">Node.js 응용 프로그램을 만드는 방법에 지침은 [만들기 Node.js 응용 프로그램 tooAzure 웹 사이트를 배포 하 고][nodejswebsite], [Node.js 클라우드 서비스] [ Node.js Cloud Service] Windows PowerShell을 사용 하 여 또는 [WebMatrix로 웹 사이트]합니다.</span><span class="sxs-lookup"><span data-stu-id="59466-121">For instructions on creating a Node.js application, see [Create and deploy a Node.js application tooAzure Web Site][nodejswebsite], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or [Web Site with WebMatrix].</span></span>

## <a name="configure-your-application-toouse-notification-hubs"></a><span data-ttu-id="59466-122">응용 프로그램 tooUse 알림 허브를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="59466-122">Configure Your Application tooUse Notification Hubs</span></span>
<span data-ttu-id="59466-123">Azure 알림 허브 toouse 해야 toodownload 및 사용 하 여 hello Node.js [azure 패키지](https://www.npmjs.com/package/azure), 기본 제공 hello 푸시 알림 REST 서비스와 통신 하는 도우미 라이브러리 집합을 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="59466-123">toouse Azure Notification Hubs, you need toodownload and use hello Node.js [azure package](https://www.npmjs.com/package/azure), which includes a built-in set of helper libraries that communicate with hello push notification REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="59466-124">노드 패키지 관리자 (NPM) tooobtain hello 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="59466-124">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="59466-125">와 같은 명령줄 인터페이스를 사용 하 여 **PowerShell** (Windows) **터미널** (Mac) 또는 **를 이용한 적** (Linux) 빈 응용 프로그램을 만들 위치 toohello 폴더 이동 .</span><span class="sxs-lookup"><span data-stu-id="59466-125">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Linux) and navigate toohello folder where you created your blank application.</span></span>
2. <span data-ttu-id="59466-126">형식 **npm 설치 azure sb** hello 명령 창에서.</span><span class="sxs-lookup"><span data-stu-id="59466-126">Type **npm install azure-sb** in hello command window.</span></span>
3. <span data-ttu-id="59466-127">Hello를 수동으로 실행할 수 있습니다 **ls** 또는 **dir** 명령 tooverify 하는 **노드\_모듈** 폴더를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="59466-127">You can manually run hello **ls** or **dir** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="59466-128">해당 폴더 내의 hello 찾습니다 **azure** tooaccess 필요한 hello 라이브러리를 포함 하는 패키지 hello 알림 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="59466-128">Inside that folder, find hello **azure** package, which contains hello libraries you need tooaccess hello Notification Hub.</span></span>

> [!NOTE]
> <span data-ttu-id="59466-129">Hello 공식에 NPM을 설치 하는 방법에 대 한 자세히 알아볼 수 있습니다 [NPM 블로그](http://blog.npmjs.org/post/85484771375/how-to-install-npm)합니다.</span><span class="sxs-lookup"><span data-stu-id="59466-129">You can learn more about installing NPM on hello official [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span></span> 
> 
> 

### <a name="import-hello-module"></a><span data-ttu-id="59466-130">Hello 모듈 가져오기</span><span class="sxs-lookup"><span data-stu-id="59466-130">Import hello module</span></span>
<span data-ttu-id="59466-131">텍스트 편집기를 사용 하 여 추가 hello toohello 맨 뒤 hello **server.js** hello 응용 프로그램의 파일:</span><span class="sxs-lookup"><span data-stu-id="59466-131">Using a text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a><span data-ttu-id="59466-132">Azure 알림 허브 연결 설정</span><span class="sxs-lookup"><span data-stu-id="59466-132">Setup an Azure Notification Hub connection</span></span>
<span data-ttu-id="59466-133">hello **NotificationHubService** 개체는 알림 허브를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59466-133">hello **NotificationHubService** object lets you work with notification hubs.</span></span> <span data-ttu-id="59466-134">hello 다음 코드에서는 **NotificationHubService** 라는 hello nofication 허브에 대 한 개체 **hubname**합니다.</span><span class="sxs-lookup"><span data-stu-id="59466-134">hello following code creates a **NotificationHubService** object for hello nofication hub named **hubname**.</span></span> <span data-ttu-id="59466-135">Hello의 hello 위쪽 추가 **server.js** 후 hello 문 tooimport hello azure 모듈 파일:</span><span class="sxs-lookup"><span data-stu-id="59466-135">Add it near hello top of hello **server.js** file, after hello statement tooimport hello azure module:</span></span>

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

<span data-ttu-id="59466-136">연결 hello **connectionstring** hello에서 값을 얻을 수 [Azure 포털] hello 다음 단계를 수행 하 여:</span><span class="sxs-lookup"><span data-stu-id="59466-136">hello connection **connectionstring** value can be obtained from hello [Azure Portal] by performing hello following steps:</span></span>

1. <span data-ttu-id="59466-137">Hello 왼쪽된 탐색 창에서 클릭 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="59466-137">In hello left navigation pane, click **Browse**.</span></span>
2. <span data-ttu-id="59466-138">선택 **알림 허브**, 및 toouse hello 샘플에 대 한 원하는 찾기 hello 허브 합니다.</span><span class="sxs-lookup"><span data-stu-id="59466-138">Select **Notification Hubs**, and then find hello hub you wish toouse for hello sample.</span></span> <span data-ttu-id="59466-139">Toohello 참조할 수 있습니다 [Windows 스토어를 시작 하기 자습서](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) 새 알림 허브를 만드는 데 도움이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="59466-139">You can refer toohello [Windows Store Getting Started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) if you need help creating a new Notification Hub.</span></span>
3. <span data-ttu-id="59466-140">**설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59466-140">Select **Settings**.</span></span>
4. <span data-ttu-id="59466-141">**액세스 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59466-141">Click on **Access Policies**.</span></span> <span data-ttu-id="59466-142">공유 및 전체 액세스 연결 문자열이 모두 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="59466-142">You will see both shared and full access connection strings.</span></span>

![Azure 포털 - 알림 허브](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> <span data-ttu-id="59466-144">Hello를 사용 하 여 hello 연결 문자열을 검색할 수 있습니다 **Get AzureSbNamespace** 에서 제공 하는 cmdlet [Azure PowerShell](/powershell/azureps-cmdlets-docs) 또는 hello **azure sb 네임 스페이스 표시** 명령을 hello [Azure CLI (명령줄 인터페이스 Azure)](../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="59466-144">You can also retrieve hello connection string using hello **Get-AzureSbNamespace** cmdlet provided by [Azure PowerShell](/powershell/azureps-cmdlets-docs) or hello **azure sb namespace show** command with hello [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md).</span></span>
> 
> 

## <a name="general-architecture"></a><span data-ttu-id="59466-145">일반 아키텍처</span><span class="sxs-lookup"><span data-stu-id="59466-145">General architecture</span></span>
<span data-ttu-id="59466-146">hello **NotificationHubService** 개체 hello 푸시 알림 toospecific 장치 및 응용 프로그램을 보내기 위한 개체 인스턴스를 다음을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="59466-146">hello **NotificationHubService** object exposes hello following object instances for sending push notifications toospecific devices and applications:</span></span>

* <span data-ttu-id="59466-147">**Android** -hello를 사용 하 여 **GcmService** 개체에서 제공 되는 **notificationHubService.gcm**</span><span class="sxs-lookup"><span data-stu-id="59466-147">**Android** - use hello **GcmService** object, which is available at **notificationHubService.gcm**</span></span>
* <span data-ttu-id="59466-148">**iOS** -hello를 사용 하 여 **ApnsService** 개체에 액세스할 수 있는 **notificationHubService.apns**</span><span class="sxs-lookup"><span data-stu-id="59466-148">**iOS** - use hello **ApnsService** object, which is accessible at **notificationHubService.apns**</span></span>
* <span data-ttu-id="59466-149">**Windows Phone** -hello를 사용 하 여 **MpnsService** 개체에서 제공 되는 **notificationHubService.mpns**</span><span class="sxs-lookup"><span data-stu-id="59466-149">**Windows Phone** - use hello **MpnsService** object, which is available at **notificationHubService.mpns**</span></span>
* <span data-ttu-id="59466-150">**유니버설 Windows 플랫폼** -hello를 사용 하 여 **WnsService** 개체에서 제공 되는 **notificationHubService.wns**</span><span class="sxs-lookup"><span data-stu-id="59466-150">**Universal Windows Platform** - use hello **WnsService** object, which is available at **notificationHubService.wns**</span></span>

### <a name="how-to-send-push-notifications-tooandroid-applications"></a><span data-ttu-id="59466-151">방법: tooAndroid 응용 프로그램 알림을 푸시 보내기</span><span class="sxs-lookup"><span data-stu-id="59466-151">How to: Send push notifications tooAndroid applications</span></span>
<span data-ttu-id="59466-152">hello **GcmService** 개체를 제공는 **보낼** 메서드를 사용 하는 toosend 푸시 알림을 tooAndroid 응용 프로그램 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59466-152">hello **GcmService** object provides a **send** method that can be used toosend push notifications tooAndroid applications.</span></span> <span data-ttu-id="59466-153">hello **보낼** 메서드 매개 변수 뒤 hello 허용:</span><span class="sxs-lookup"><span data-stu-id="59466-153">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="59466-154">**태그** -hello 태그 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="59466-154">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="59466-155">없는 태그를 사용 하는 경우 tooall 클라이언트 hello 알림이 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59466-155">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="59466-156">**페이로드** -hello 메시지의 JSON 또는 원시 문자열 페이로드입니다.</span><span class="sxs-lookup"><span data-stu-id="59466-156">**Payload** - hello message's JSON or raw string payload.</span></span>
* <span data-ttu-id="59466-157">**콜백** -hello 콜백 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="59466-157">**Callback** - hello callback function.</span></span>

<span data-ttu-id="59466-158">Hello 페이로드 형식에 대 한 자세한 내용은 참조 hello **페이로드** hello 섹션 [GCM 서버 구현](http://developer.android.com/google/gcm/server.html#payload) 문서.</span><span class="sxs-lookup"><span data-stu-id="59466-158">For more information on hello payload format, see hello **Payload** section of hello [Implementing GCM Server](http://developer.android.com/google/gcm/server.html#payload) document.</span></span>

<span data-ttu-id="59466-159">hello 다음 코드에서는 사용 hello **GcmService** hello에 의해 노출 되는 인스턴스 **NotificationHubService** toosend 푸시 알림 tooall 클라이언트를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="59466-159">hello following code uses hello **GcmService** instance exposed by hello **NotificationHubService** toosend a push notification tooall registered clients.</span></span>

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

### <a name="how-to-send-push-notifications-tooios-applications"></a><span data-ttu-id="59466-160">방법: tooiOS 응용 프로그램 알림을 푸시 보내기</span><span class="sxs-lookup"><span data-stu-id="59466-160">How to: Send push notifications tooiOS applications</span></span>
<span data-ttu-id="59466-161">동일 위에서 설명한 Android 응용 프로그램에서와 마찬가지로 hello **ApnsService** 개체를 제공는 **보낼** 메서드를 사용 하는 toosend 푸시 알림을 tooiOS 응용 프로그램 수입니다.</span><span class="sxs-lookup"><span data-stu-id="59466-161">Same as with Android applications described above, hello **ApnsService** object provides a **send** method that can be used toosend push notifications tooiOS applications.</span></span> <span data-ttu-id="59466-162">hello **보낼** 메서드 매개 변수 뒤 hello 허용:</span><span class="sxs-lookup"><span data-stu-id="59466-162">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="59466-163">**태그** -hello 태그 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="59466-163">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="59466-164">없는 태그를 사용 하는 경우 tooall 클라이언트 hello 알림이 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59466-164">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="59466-165">**페이로드** -hello 메시지의 JSON 또는 문자열 페이로드입니다.</span><span class="sxs-lookup"><span data-stu-id="59466-165">**Payload** - hello message's JSON or string payload.</span></span>
* <span data-ttu-id="59466-166">**콜백** -hello 콜백 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="59466-166">**Callback** - hello callback function.</span></span>

<span data-ttu-id="59466-167">자세한 내용은 hello 페이로드 형식에 대 한 참조 hello **알림 페이로드** hello 섹션 [로컬 및 푸시 알림 프로그래밍 가이드](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) 문서.</span><span class="sxs-lookup"><span data-stu-id="59466-167">For more information hello payload format, see hello **Notification Payload** section of hello [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.</span></span>

<span data-ttu-id="59466-168">hello 다음 코드에서는 사용 hello **ApnsService** hello에 의해 노출 되는 인스턴스 **NotificationHubService** toosend 경고 메시지 tooall 클라이언트:</span><span class="sxs-lookup"><span data-stu-id="59466-168">hello following code uses hello **ApnsService** instance exposed by hello **NotificationHubService** toosend an alert message tooall clients:</span></span>

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-toowindows-phone-applications"></a><span data-ttu-id="59466-169">방법: 보내기 푸시 알림을 tooWindows 전화 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="59466-169">How to: Send push notifications tooWindows Phone applications</span></span>
<span data-ttu-id="59466-170">hello **MpnsService** 개체를 제공는 **보낼** 메서드를 사용 하는 toosend 푸시 알림을 tooWindows 전화 응용 프로그램 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59466-170">hello **MpnsService** object provides a **send** method that can be used toosend push notifications tooWindows Phone applications.</span></span> <span data-ttu-id="59466-171">hello **보낼** 메서드 매개 변수 뒤 hello 허용:</span><span class="sxs-lookup"><span data-stu-id="59466-171">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="59466-172">**태그** -hello 태그 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="59466-172">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="59466-173">없는 태그를 사용 하는 경우 tooall 클라이언트 hello 알림이 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59466-173">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="59466-174">**페이로드** -hello 메시지의 XML 페이로드입니다.</span><span class="sxs-lookup"><span data-stu-id="59466-174">**Payload** - hello message's XML payload.</span></span>
* <span data-ttu-id="59466-175">**TargetName** - `toast` - 알림 메시지인 경우.</span><span class="sxs-lookup"><span data-stu-id="59466-175">**TargetName** - `toast` for toast notifications.</span></span> <span data-ttu-id="59466-176">`token` - 타일 알림 메시지인 경우.</span><span class="sxs-lookup"><span data-stu-id="59466-176">`token` for tile notifications.</span></span>
* <span data-ttu-id="59466-177">**알림 클래스** -hello hello 알림의 우선 순위입니다.</span><span class="sxs-lookup"><span data-stu-id="59466-177">**NotificationClass** - hello priority of hello notification.</span></span> <span data-ttu-id="59466-178">Hello 참조 **HTTP 헤더 요소** hello 섹션 [푸시 알림 서버에서](http://msdn.microsoft.com/library/hh221551.aspx) 유효한 값에 대 한 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="59466-178">See hello **HTTP Header Elements** section of hello [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) document for valid values.</span></span>
* <span data-ttu-id="59466-179">**Options** - 선택적 요청 헤더</span><span class="sxs-lookup"><span data-stu-id="59466-179">**Options** - optional request headers.</span></span>
* <span data-ttu-id="59466-180">**콜백** -hello 콜백 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="59466-180">**Callback** - hello callback function.</span></span>

<span data-ttu-id="59466-181">유효한 목록은 **TargetName**, **알림 클래스** hello를 확인해 보세요 헤더 옵션 및 [서버에서 대 한 푸시 알림](http://msdn.microsoft.com/library/hh221551.aspx) 페이지.</span><span class="sxs-lookup"><span data-stu-id="59466-181">For a list of valid **TargetName**, **NotificationClass** and header options, check out hello [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) page.</span></span>

<span data-ttu-id="59466-182">다음 샘플 코드는 hello hello를 사용 하 여 **MpnsService** hello에 의해 노출 되는 인스턴스 **NotificationHubService** toosend 푸시 알림:</span><span class="sxs-lookup"><span data-stu-id="59466-182">hello following sample code uses hello **MpnsService** instance exposed by hello **NotificationHubService** toosend a toast push notification:</span></span>

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-toouniversal-windows-platform-uwp-applications"></a><span data-ttu-id="59466-183">방법: 보내기 푸시 알림을 tooUniversal Windows 플랫폼 (UWP) 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="59466-183">How to: Send push notifications tooUniversal Windows Platform (UWP) applications</span></span>
<span data-ttu-id="59466-184">hello **WnsService** 개체를 제공는 **보낼** 메서드를 사용 하는 toosend 푸시 알림을 tooUniversal Windows 플랫폼 응용 프로그램 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59466-184">hello **WnsService** object provides a **send** method that can be used toosend push notifications tooUniversal Windows Platform applications.</span></span>  <span data-ttu-id="59466-185">hello **보낼** 메서드 매개 변수 뒤 hello 허용:</span><span class="sxs-lookup"><span data-stu-id="59466-185">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="59466-186">**태그** -hello 태그 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="59466-186">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="59466-187">없는 태그를 사용 하는 경우 등록 된 tooall 클라이언트 hello 알림이 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59466-187">If no tag is provided, hello notification will be sent tooall registered clients.</span></span>
* <span data-ttu-id="59466-188">**페이로드** -hello XML 메시지 페이로드입니다.</span><span class="sxs-lookup"><span data-stu-id="59466-188">**Payload** - hello XML message payload.</span></span>
* <span data-ttu-id="59466-189">**형식** -hello 알림 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="59466-189">**Type** - hello notification type.</span></span>
* <span data-ttu-id="59466-190">**Options** - 선택적 요청 헤더</span><span class="sxs-lookup"><span data-stu-id="59466-190">**Options** - optional request headers.</span></span>
* <span data-ttu-id="59466-191">**콜백** -hello 콜백 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="59466-191">**Callback** - hello callback function.</span></span>

<span data-ttu-id="59466-192">유효한 유형 및 요청 헤더 목록은 [푸시 알림 서비스 요청 및 응답 헤더](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59466-192">For a list of valid types and request headers, see [Push notification service request and response headers](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span></span>

<span data-ttu-id="59466-193">hello 다음 코드에서는 사용 hello **WnsService** hello에 의해 노출 되는 인스턴스 **NotificationHubService** toosend 알림 푸시 알림 tooa UWP 앱:</span><span class="sxs-lookup"><span data-stu-id="59466-193">hello following code uses hello **WnsService** instance exposed by hello **NotificationHubService** toosend a toast push notification tooa UWP app:</span></span>

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a><span data-ttu-id="59466-194">다음 단계</span><span class="sxs-lookup"><span data-stu-id="59466-194">Next Steps</span></span>
<span data-ttu-id="59466-195">위의 hello 샘플 조각 있습니다 tooeasily 빌드 서비스 인프라 toodeliver 푸시 알림을 tooa 광범위 한 장치를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="59466-195">hello sample snippets above allow you tooeasily build service infrastructure toodeliver push notifications tooa wide variety of devices.</span></span> <span data-ttu-id="59466-196">Node.js와 함께 알림 허브를 사용 하 여 hello 기본 사항 학습 한, 했으므로 이러한 기능을 추가로 확장 하는 방법에 대 한 자세한 이러한 링크 toolearn을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="59466-196">Now that you've learned hello basics of using Notification Hubs with node.js, follow these links toolearn more about how you can extend these capabilities further.</span></span>

* <span data-ttu-id="59466-197">참조에 대 한 MSDN 참조 hello [Azure 알림 허브](https://msdn.microsoft.com/library/azure/jj927170.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="59466-197">See hello MSDN Reference for [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span></span>
* <span data-ttu-id="59466-198">Hello 방문 [노드 용 Azure SDK] 더 많은 샘플 및 구현 세부 사항에 대 한 GitHub의 리포지토리 합니다.</span><span class="sxs-lookup"><span data-stu-id="59466-198">Visit hello [Azure SDK for Node] repository on GitHub for more samples and implementation details.</span></span>

[노드 용 Azure SDK]: https://github.com/WindowsAzure/azure-sdk-for-node
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain hello Default Management Credentials for hello Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application tooUse Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages tooa Topic]: #How_to_Send_Messages_to_a_Topic
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
[WebMatrix로 웹 사이트]: /develop/nodejs/tutorials/web-site-with-webmatrix/
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
[Azure 포털]: https://portal.azure.com
