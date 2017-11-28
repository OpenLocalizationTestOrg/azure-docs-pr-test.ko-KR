---
title: "Linux에서 Azure 웹 앱에 대 한 사용자 지정 Docker 이미지 aaaHow toouse | Microsoft Docs"
description: "어떻게 Linux에서 Azure 웹 앱에 대 한 사용자 지정 Docker toouse 이미지입니다."
keywords: "azure app service, 웹앱, linux, docker, 컨테이너"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: b97bd4e6-dff0-4976-ac20-d5c109a559a8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 8853095d0e1067cfea4297bbd23b622fe4a0d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a><span data-ttu-id="5cb8f-104">Linux에서 Azure Web App에 대한 사용자 지정 Docker 이미지 사용</span><span class="sxs-lookup"><span data-stu-id="5cb8f-104">Using a custom Docker image for Azure Web App on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="5cb8f-105">App Service는 PHP 7.0 및 Node.js 4.5와 같은 특정 버전에 대한 지원을 통해 Linux에 미리 정의된 응용 프로그램 스택을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-105">App Service provides pre-defined application stacks on Linux with support for specific versions, such as PHP 7.0 and Node.js 4.5.</span></span> <span data-ttu-id="5cb8f-106">Linux에서 응용 프로그램 서비스 Docker 컨테이너를 사용 하 여 toohost 이러한 미리 작성 된 응용 프로그램 스택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-106">App Service on Linux uses Docker containers toohost these pre-built application stacks.</span></span> <span data-ttu-id="5cb8f-107">또한 사용자 지정 Docker 이미지 toodeploy Azure에 이미 정의 되어 있지는 웹 응용 프로그램 tooan 응용 프로그램 스택을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-107">You can also use a custom Docker image toodeploy your web app tooan application stack that is not already defined in Azure.</span></span> <span data-ttu-id="5cb8f-108">사용자 지정 Docker 이미지는 공용 또는 개인 Docker 리포지토리에 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-108">Custom Docker images can be hosted on either a public or private Docker repository.</span></span>


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a><span data-ttu-id="5cb8f-109">방법: 웹앱에 대한 사용자 지정 Docker 이미지 설정</span><span class="sxs-lookup"><span data-stu-id="5cb8f-109">How to: set a custom Docker image for a web app</span></span>
<span data-ttu-id="5cb8f-110">새 모두에 대 한 사용자 지정 Docker 이미지 hello 및 기존 웹 앱을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-110">You can set hello custom Docker image for both new and existing webs apps.</span></span> <span data-ttu-id="5cb8f-111">Hello에 Linux에서 웹 응용 프로그램을 만드는 하는 경우 [Azure 포털](https://portal.azure.com/#create/Microsoft.AppSvcLinux), 클릭 **구성 컨테이너** tooset Docker 이미지를 사용자 지정:</span><span class="sxs-lookup"><span data-stu-id="5cb8f-111">When you create a web app on Linux in hello [Azure portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), click **Configure container** tooset a custom Docker image:</span></span>

![Linux의 새 웹앱에 대한 사용자 지정 Docker 이미지][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a><span data-ttu-id="5cb8f-113">방법: Docker 허브에서 사용자 지정 Docker 이미지 사용</span><span class="sxs-lookup"><span data-stu-id="5cb8f-113">How to: use a custom Docker image from Docker Hub</span></span> ##
<span data-ttu-id="5cb8f-114">사용자 지정 Docker 이미지를 Docker 허브에서 toouse:</span><span class="sxs-lookup"><span data-stu-id="5cb8f-114">toouse a custom Docker image from Docker Hub:</span></span>

1. <span data-ttu-id="5cb8f-115">Hello에 [Azure 포털](https://portal.azure.com)에서 다음 linux에서 웹 앱을 찾을 **설정** 클릭 **Docker 컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-115">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="5cb8f-116">선택 **Docker 허브** hello로 **이미지 원본**를 클릭 한 다음 **공용** 또는 **개인** 및 형식 hello **이미지 및 선택적 태그 이름을**와 같은 `node:4.5`합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-116">Select **Docker Hub** as hello **Image source**, then click either **Public** or **Private** and type hello **Image and optional tag name**, such as `node:4.5`.</span></span> <span data-ttu-id="5cb8f-117">hello **시작 명령** 는 설정에 따라 자동으로 hello Docker 이미지 파일에 정의 된 되지만 직접 명령을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-117">hello **Startup command** is set automatically based on what is defined in hello Docker image file, but you can set your own commands.</span></span>  

    ![Docker 허브 공용 리포지토리 이미지 구성][2]

    <span data-ttu-id="5cb8f-119">Tooenter hello Docker 허브 자격 증명으로도 필요한 개인 저장소에서 이미지 이면 (**로그인 사용자 이름과** 및 **암호**) hello 개인 Docker 허브 저장소에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-119">When your image is from a private repository, you also need tooenter hello Docker Hub credentials as (**Login username** and **Password**) for hello private Docker Hub repository.</span></span>

    ![Docker 허브 개인 리포지토리 이미지 구성][3]

3. <span data-ttu-id="5cb8f-121">클릭 하 여 hello 컨테이너를 구성 하 고 나면 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-121">After you have configured hello container, click **Save**.</span></span>

## <a name="how-toouse-a-docker-image-from-a-private-image-registry"></a><span data-ttu-id="5cb8f-122">개인 이미지 레지스트리에서 toouse는 Docker 이미지 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5cb8f-122">How toouse a Docker image from a private image registry</span></span> ##
<span data-ttu-id="5cb8f-123">toouse 개인 이미지 레지스트리에서 Docker 이미지를 사용자 지정:</span><span class="sxs-lookup"><span data-stu-id="5cb8f-123">toouse a custom Docker image from a private image registry:</span></span>

1. <span data-ttu-id="5cb8f-124">Hello에 [Azure 포털](https://portal.azure.com)에서 다음 linux에서 웹 앱을 찾을 **설정** 클릭 **Docker 컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-124">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="5cb8f-125">클릭 **개인 레지스트리** hello로 **이미지 원본**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-125">Click **Private registry** as hello **Image source**.</span></span> <span data-ttu-id="5cb8f-126">Hello 입력 **이미지와 선택적 태그 이름을**, **서버 URL** hello 자격 증명과 함께 hello 개인 레지스트리 (**로그인 사용자 이름** 및 **암호** ).</span><span class="sxs-lookup"><span data-stu-id="5cb8f-126">Enter hello **Image and optional tag name**, **Server URL** for hello private registry, along with hello credentials (**Login username** and **Password**).</span></span> <span data-ttu-id="5cb8f-127">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-127">Click **Save**.</span></span>

    ![개인 레지스트리에서 Docker 이미지 구성][4]


## <a name="how-to-set-hello-port-used-by-your-docker-image"></a><span data-ttu-id="5cb8f-129">방법: Docker 이미지에서 사용 하는 hello 포트 설정</span><span class="sxs-lookup"><span data-stu-id="5cb8f-129">How to: set hello port used by your Docker image</span></span> ##

<span data-ttu-id="5cb8f-130">웹 앱에 대 한 사용자 지정 Docker 이미지를 사용 하는 경우에 hello을 사용할 수 있습니다 `WEBSITES_PORT` 생성 toohello 컨테이너 추가 Dockerfile의 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-130">When you use a custom Docker image for your web app, you can use hello `WEBSITES_PORT` environment variable in your Dockerfile, which gets added toohello generated container.</span></span> <span data-ttu-id="5cb8f-131">다음 예제는 Ruby 응용 프로그램에 대 한 docker 파일의 hello를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-131">Consider hello following example of a docker file for a Ruby application:</span></span>

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

<span data-ttu-id="5cb8f-132">Hello 명령의 마지막 줄에서 런타임 시 hello WEBSITES_PORT이 환경 변수에 전달 되 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-132">On last line of hello command, you can see that hello WEBSITES_PORT environment variable is passed at runtime.</span></span> <span data-ttu-id="5cb8f-133">명령은 대/소문자를 구분해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-133">Remember that casing matters in commands.</span></span>

<span data-ttu-id="5cb8f-134">이전에 hello를 사용 하 여 플랫폼 `PORT` 응용 프로그램 설정, म 계획 toodeprecate hello 사용 하 여가이 앱을 설정 하 고 있으며 toousing 이동 `WEBSITES_PORT` 단독으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-134">Previously hello platform was using `PORT` app setting, we are planning toodeprecate hello use this app setting and move toousing `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="5cb8f-135">다른 사용자에 의해 작성 된 기존 Docker 이미지를 사용 하는 경우에 hello 응용 프로그램에 대 한 toospecify 포트 80 이외의 포트를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-135">When you use an existing Docker image built by someone else, you may need toospecify a port other than port 80 for hello application.</span></span> <span data-ttu-id="5cb8f-136">tooconfigure hello 포트, 명명 된 설정 하는 응용 프로그램 추가 `WEBSITES_PORT` 아래와 같이 hello 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-136">tooconfigure hello port, add an application setting named `WEBSITES_PORT` with hello value as shown below:</span></span>

![사용자 지정 Docker 이미지에 대한 PORT 앱 설정 구성][6]

## <a name="how-to-set-hello-startup-time-for-your-docker-image"></a><span data-ttu-id="5cb8f-138">방법: hello 시작 시간을 Docker 이미지를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-138">How to: set hello startup time for your Docker image</span></span> ##

<span data-ttu-id="5cb8f-139">기본적으로 컨테이너 230 초 전에 시작 되지 않으면 hello 플랫폼 다시 시작 됩니다 컨테이너.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-139">By default, if your container does not start before 230 seconds, hello platform will restart your container.</span></span> <span data-ttu-id="5cb8f-140">사용자 지정 Docker 이미지 230 초 이상에서 시작 되 면 hello를 사용할 수 있습니다 `WEBSITES_CONTAINER_START_TIME_LIMIT` 설정, 앱이이 설정에 대 한 hello 값은 초 단위, 다시 시작 하기 전에 실행 중인 컨테이너 hello 플랫폼 유지를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-140">If your custom Docker image starts in more than 230 seconds, you can use hello `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting, hello value for this setting is in seconds, this will allow hello platform keep your container running before restarting it.</span></span> <span data-ttu-id="5cb8f-141">hello 기본값이 230 초 및 hello 최대 허용 값은 600 초입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-141">hello default value is 230 seconds, and hello max allowed value is 600 seconds.</span></span>

## <a name="how-to-unmount-hello-platform-provided-storage"></a><span data-ttu-id="5cb8f-142">방법: hello 플랫폼 제공 된 저장소를 탑재 해제</span><span class="sxs-lookup"><span data-stu-id="5cb8f-142">How to: unmount hello platform provided storage</span></span> ##

<span data-ttu-id="5cb8f-143">Hello 플랫폼에서 영구 저장소 공유 toohello 기본적으로 탑재 `\home\` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-143">By default, hello platform will mount a persistent storage share toohello `\home\` directory.</span></span> <span data-ttu-id="5cb8f-144">컨테이너 이미지를 영구 공유가 필요 없는 경우 hello 설정 하 여 해당 저장소를 탑재 비활성화할 수 있습니다 `WEBSITES_ENABLE_APP_SERVICE_STORAGE` 앱 설정 너무`false`합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-144">If your container image does not need a persistent share, you can disable mounting that storage by setting hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting too`false`.</span></span> <span data-ttu-id="5cb8f-145">계속 액세스 toothat 저장소 hello scm 사이트에서 및가 toohello hello 플랫폼에서 생성 한 로그 파일 (설정 된 경우) 모든 Docker 로그 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-145">You will still have access toothat storage from hello scm site, and all Docker logs (if enabled) will be written toohello log files generated by hello platform.</span></span>

## <a name="how-to-switch-back-toousing-a-built-in-image"></a><span data-ttu-id="5cb8f-146">방법: 기본 제공 이미지 toousing 다시 전환</span><span class="sxs-lookup"><span data-stu-id="5cb8f-146">How to: Switch back toousing a built-in image</span></span> ##

<span data-ttu-id="5cb8f-147">사용자 지정 이미지 toousing 기본 제공 이미지를 사용 하 여 tooswitch:</span><span class="sxs-lookup"><span data-stu-id="5cb8f-147">tooswitch from using a custom image toousing a built-in image:</span></span>

1. <span data-ttu-id="5cb8f-148">Hello에 [Azure 포털](https://portal.azure.com)에서 다음 linux에서 웹 앱을 찾을 **설정** 클릭 **앱 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-148">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **App Service**.</span></span>

2. <span data-ttu-id="5cb8f-149">선택 하면 **런타임 스택을** toouse hello 기본 제공 이미지에 대 한 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-149">Select your **Runtime Stack** toouse for hello built-in image, then click **Save**.</span></span> 

![기본 제공 Docker 이미지 구성][5]


## <a name="troubleshooting"></a><span data-ttu-id="5cb8f-151">문제 해결</span><span class="sxs-lookup"><span data-stu-id="5cb8f-151">Troubleshooting</span></span> ##

<span data-ttu-id="5cb8f-152">응용 프로그램에 사용자 지정 Docker 이미지와 toostart 실패 하면 hello Docker hello 로그 파일 디렉터리에 로그를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-152">When your application fails toostart with your custom Docker image, check hello Docker logs in hello LogFiles directory.</span></span> <span data-ttu-id="5cb8f-153">SCM 사이트 또는 FTP를 통해 이 디렉터리에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-153">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="5cb8f-154">toolog hello `stdout` 및 `stderr` tooenable 사용자 컨테이너에서 필요한 **Docker 컨테이너 로깅** 아래 **진단 로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-154">toolog hello `stdout` and `stderr` from your container, you need tooenable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![로깅 사용][8]

![Kudu tooview Docker 로그를 사용 하 여][7]

<span data-ttu-id="5cb8f-157">hello SCM 사이트에 액세스할 수 있습니다 **고급 도구** hello에 **개발 도구** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-157">You can access hello SCM site from **Advanced Tools** in hello **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5cb8f-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5cb8f-158">Next Steps</span></span> ##

<span data-ttu-id="5cb8f-159">Hello Linux에서 웹 앱과 함께 시작 하는 링크 tooget 뒤를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-159">Follow hello following links tooget started with Web App on Linux.</span></span>   

* [<span data-ttu-id="5cb8f-160">소개 tooAzure Linux에서 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="5cb8f-160">Introduction tooAzure Web App on Linux</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="5cb8f-161">Linux의 Azure Web App에서 Node.js용 PM2 구성 사용</span><span class="sxs-lookup"><span data-stu-id="5cb8f-161">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](./app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="5cb8f-162">Linux의 Azure App Service Web App에 대한 FAQ</span><span class="sxs-lookup"><span data-stu-id="5cb8f-162">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<span data-ttu-id="5cb8f-163">[당사 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview)에 질문 및 문제를 게시하세요.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-163">Post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
