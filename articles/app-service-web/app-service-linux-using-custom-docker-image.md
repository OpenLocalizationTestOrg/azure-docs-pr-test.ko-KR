---
title: "Linux에서 Azure Web App에 대한 사용자 지정 Docker 이미지를 사용하는 방법 | Microsoft Docs"
description: "Linux에서 Azure Web App에 대한 사용자 지정 Docker 이미지를 사용하는 방법"
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
ms.openlocfilehash: 1458217a31c4781b28877c030a665f5b22819e13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a><span data-ttu-id="ec9e1-104">Linux에서 Azure Web App에 대한 사용자 지정 Docker 이미지 사용</span><span class="sxs-lookup"><span data-stu-id="ec9e1-104">Using a custom Docker image for Azure Web App on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="ec9e1-105">App Service는 PHP 7.0 및 Node.js 4.5와 같은 특정 버전에 대한 지원을 통해 Linux에 미리 정의된 응용 프로그램 스택을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-105">App Service provides pre-defined application stacks on Linux with support for specific versions, such as PHP 7.0 and Node.js 4.5.</span></span> <span data-ttu-id="ec9e1-106">Linux의 App Service는 Docker 컨테이너를 사용하여 이러한 미리 작성된 응용 프로그램 스택을 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-106">App Service on Linux uses Docker containers to host these pre-built application stacks.</span></span> <span data-ttu-id="ec9e1-107">또한 사용자 지정 Docker 이미지를 사용하여 Azure에 아직 정의되지 않은 응용 프로그램 스택에 웹앱을 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-107">You can also use a custom Docker image to deploy your web app to an application stack that is not already defined in Azure.</span></span> <span data-ttu-id="ec9e1-108">사용자 지정 Docker 이미지는 공용 또는 개인 Docker 리포지토리에 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-108">Custom Docker images can be hosted on either a public or private Docker repository.</span></span>


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a><span data-ttu-id="ec9e1-109">방법: 웹앱에 대한 사용자 지정 Docker 이미지 설정</span><span class="sxs-lookup"><span data-stu-id="ec9e1-109">How to: set a custom Docker image for a web app</span></span>
<span data-ttu-id="ec9e1-110">신규 및 기존 웹앱에 대해 사용자 지정 Docker 이미지를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-110">You can set the custom Docker image for both new and existing webs apps.</span></span> <span data-ttu-id="ec9e1-111">[Azure Portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux)에서 Linux의 웹앱을 만들 경우 **컨테이너 구성**을 클릭하여 사용자 지정 Docker 이미지를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-111">When you create a web app on Linux in the [Azure portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), click **Configure container** to set a custom Docker image:</span></span>

![Linux의 새 웹앱에 대한 사용자 지정 Docker 이미지][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a><span data-ttu-id="ec9e1-113">방법: Docker 허브에서 사용자 지정 Docker 이미지 사용</span><span class="sxs-lookup"><span data-stu-id="ec9e1-113">How to: use a custom Docker image from Docker Hub</span></span> ##
<span data-ttu-id="ec9e1-114">Docker 허브에서 사용자 지정 Docker 이미지를 사용하려면</span><span class="sxs-lookup"><span data-stu-id="ec9e1-114">To use a custom Docker image from Docker Hub:</span></span>

1. <span data-ttu-id="ec9e1-115">[Azure Portal](https://portal.azure.com)에서 Linux의 웹앱을 찾은 후 **설정**에서 **Docker 컨테이너**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-115">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="ec9e1-116">**Docker 허브**를 **이미지 소스**로 선택하고 **공용** 또는 **개인**을 클릭하고 **이미지 및 선택적 태그 이름**(예: `node:4.5`)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-116">Select **Docker Hub** as the **Image source**, then click either **Public** or **Private** and type the **Image and optional tag name**, such as `node:4.5`.</span></span> <span data-ttu-id="ec9e1-117">**시작 명령**은 자동으로 Docker 이미지 파일에 정의된 내용을 기준으로 하지만 명령을 직접 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-117">The **Startup command** is set automatically based on what is defined in the Docker image file, but you can set your own commands.</span></span>  

    ![Docker 허브 공용 리포지토리 이미지 구성][2]

    <span data-ttu-id="ec9e1-119">이미지가 개인 리포지토리에 있는 것이면 개인 Docker 허브 리포지토리에 대해 Docker 허브 자격 증명(**로그인 사용자 이름** 및 **암호**)도 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-119">When your image is from a private repository, you also need to enter the Docker Hub credentials as (**Login username** and **Password**) for the private Docker Hub repository.</span></span>

    ![Docker 허브 개인 리포지토리 이미지 구성][3]

3. <span data-ttu-id="ec9e1-121">컨테이너를 구성한 후 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-121">After you have configured the container, click **Save**.</span></span>

## <a name="how-to-use-a-docker-image-from-a-private-image-registry"></a><span data-ttu-id="ec9e1-122">개인 이미지 레지스트리의 Docker 이미지를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="ec9e1-122">How to use a Docker image from a private image registry</span></span> ##
<span data-ttu-id="ec9e1-123">개인 이미지 레지스트리의 사용자 지정 Docker 이미지를 사용하려면</span><span class="sxs-lookup"><span data-stu-id="ec9e1-123">To use a custom Docker image from a private image registry:</span></span>

1. <span data-ttu-id="ec9e1-124">[Azure Portal](https://portal.azure.com)에서 Linux의 웹앱을 찾은 후 **설정**에서 **Docker 컨테이너**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-124">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="ec9e1-125">**이미지 소스**로 **개인 레지스트리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-125">Click **Private registry** as the **Image source**.</span></span> <span data-ttu-id="ec9e1-126">개인 레지스트리에 대한 **이미지 및 선택적 태그 이름**, **서버 URL**을 입력하고 자격 증명(**로그인 사용자 이름** 및 **암호**)를 함께 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-126">Enter the **Image and optional tag name**, **Server URL** for the private registry, along with the credentials (**Login username** and **Password**).</span></span> <span data-ttu-id="ec9e1-127">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-127">Click **Save**.</span></span>

    ![개인 레지스트리에서 Docker 이미지 구성][4]


## <a name="how-to-set-the-port-used-by-your-docker-image"></a><span data-ttu-id="ec9e1-129">방법: Docker 이미지에 사용되는 포트 설정</span><span class="sxs-lookup"><span data-stu-id="ec9e1-129">How to: set the port used by your Docker image</span></span> ##

<span data-ttu-id="ec9e1-130">웹앱에 대한 사용자 지정 Docker 이미지를 사용하는 경우 생성된 컨테이너에 추가된 `WEBSITES_PORT` 환경 변수를 Dockerfile에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-130">When you use a custom Docker image for your web app, you can use the `WEBSITES_PORT` environment variable in your Dockerfile, which gets added to the generated container.</span></span> <span data-ttu-id="ec9e1-131">다음의 Ruby 응용 프로그램용 docker 파일 예제를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-131">Consider the following example of a docker file for a Ruby application:</span></span>

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

<span data-ttu-id="ec9e1-132">명령의 마지막 줄에서 런타임에 WEBSITES_PORT 환경 변수가 전달된다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-132">On last line of the command, you can see that the WEBSITES_PORT environment variable is passed at runtime.</span></span> <span data-ttu-id="ec9e1-133">명령은 대/소문자를 구분해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-133">Remember that casing matters in commands.</span></span>

<span data-ttu-id="ec9e1-134">이전에 플랫폼은 `PORT` 앱 설정을 사용했으며 이 앱 설정 사용을 사용되지 않도록 하고 `WEBSITES_PORT`를 단독으로 사용하도록 이동할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-134">Previously the platform was using `PORT` app setting, we are planning to deprecate the use this app setting and move to using `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="ec9e1-135">다른 사용자가 작성한 기존 Docker 이미지를 사용하면 응용 프로그램에 대해 포트 80 이외의 포트를 지정해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-135">When you use an existing Docker image built by someone else, you may need to specify a port other than port 80 for the application.</span></span> <span data-ttu-id="ec9e1-136">포트를 구성하려면 아래와 같이 값과 함께 `WEBSITES_PORT`라는 응용 프로그램 설정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-136">To configure the port, add an application setting named `WEBSITES_PORT` with the value as shown below:</span></span>

![사용자 지정 Docker 이미지에 대한 PORT 앱 설정 구성][6]

## <a name="how-to-set-the-startup-time-for-your-docker-image"></a><span data-ttu-id="ec9e1-138">방법: Docker 이미지의 시작 시간 설정</span><span class="sxs-lookup"><span data-stu-id="ec9e1-138">How to: set the startup time for your Docker image</span></span> ##

<span data-ttu-id="ec9e1-139">기본적으로 컨테이너가 230초 전에 시작되지 않으면 플랫폼이 컨테이너를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-139">By default, if your container does not start before 230 seconds, the platform will restart your container.</span></span> <span data-ttu-id="ec9e1-140">사용자 지정 Docker 이미지가 230초 이후에 시작하는 경우 `WEBSITES_CONTAINER_START_TIME_LIMIT` 앱 설정을 사용할 수 있습니다. 이 설정에 대한 값은 초 단위이고 다시 시작하기 전에 실행 중인 컨테이너 플랫폼을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-140">If your custom Docker image starts in more than 230 seconds, you can use the `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting, the value for this setting is in seconds, this will allow the platform keep your container running before restarting it.</span></span> <span data-ttu-id="ec9e1-141">기본값은 230초이고 허용되는 최대 값은 600초입니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-141">The default value is 230 seconds, and the max allowed value is 600 seconds.</span></span>

## <a name="how-to-unmount-the-platform-provided-storage"></a><span data-ttu-id="ec9e1-142">방법: 플랫폼 제공 저장소 탑재 해제</span><span class="sxs-lookup"><span data-stu-id="ec9e1-142">How to: unmount the platform provided storage</span></span> ##

<span data-ttu-id="ec9e1-143">플랫폼은 영구 저장소 공유를 `\home\` 디렉터리에 기본적으로 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-143">By default, the platform will mount a persistent storage share to the `\home\` directory.</span></span> <span data-ttu-id="ec9e1-144">컨테이너 이미지에 영구 공유가 필요하지 않은 경우 `WEBSITES_ENABLE_APP_SERVICE_STORAGE` 앱 설정을 `false`로 설정하여 해당 저장소의 탑재를 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-144">If your container image does not need a persistent share, you can disable mounting that storage by setting the `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting to `false`.</span></span> <span data-ttu-id="ec9e1-145">SCM 사이트에서 해당 저장소에 액세스할 수 있으며 모든 Docker 로그(설정된 경우)를 플랫폼에 의해 생성된 로그 파일에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-145">You will still have access to that storage from the scm site, and all Docker logs (if enabled) will be written to the log files generated by the platform.</span></span>

## <a name="how-to-switch-back-to-using-a-built-in-image"></a><span data-ttu-id="ec9e1-146">방법: 기본 제공 이미지 사용 방식으로 다시 전환</span><span class="sxs-lookup"><span data-stu-id="ec9e1-146">How to: Switch back to using a built-in image</span></span> ##

<span data-ttu-id="ec9e1-147">사용자 지정 이미지를 사용하는 방식에서 기본 제공 이미지를 사용하는 방식으로 전환하려면</span><span class="sxs-lookup"><span data-stu-id="ec9e1-147">To switch from using a custom image to using a built-in image:</span></span>

1. <span data-ttu-id="ec9e1-148">[Azure Portal](https://portal.azure.com)에서 Linux의 웹앱을 찾은 후 **설정**에서 **App Service**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-148">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **App Service**.</span></span>

2. <span data-ttu-id="ec9e1-149">기본 제공 이미지에 사용한 **런타임 스택**을 선택하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-149">Select your **Runtime Stack** to use for the built-in image, then click **Save**.</span></span> 

![기본 제공 Docker 이미지 구성][5]


## <a name="troubleshooting"></a><span data-ttu-id="ec9e1-151">문제 해결</span><span class="sxs-lookup"><span data-stu-id="ec9e1-151">Troubleshooting</span></span> ##

<span data-ttu-id="ec9e1-152">응용 프로그램이 사용자 지정 Docker 이미지로 시작하지 못할 경우 LogFiles 디렉터리에서 Docker 로그를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-152">When your application fails to start with your custom Docker image, check the Docker logs in the LogFiles directory.</span></span> <span data-ttu-id="ec9e1-153">SCM 사이트 또는 FTP를 통해 이 디렉터리에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-153">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="ec9e1-154">컨테이너에서 `stdout` 및 `stderr`을 로그하려면 **진단 로그** 아래에서 **Docker 컨테이너 로깅**을 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-154">To log the `stdout` and `stderr` from your container, you need to enable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![로깅 사용][8]

![Kudu를 사용하여 Docker 로그 보기][7]

<span data-ttu-id="ec9e1-157">**고급 도구**의 **개발 도구** 메뉴에서 SCM 사이트에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-157">You can access the SCM site from **Advanced Tools** in the **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec9e1-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ec9e1-158">Next Steps</span></span> ##

<span data-ttu-id="ec9e1-159">Linux에서 웹앱을 시작하려면 다음 링크를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-159">Follow the following links to get started with Web App on Linux.</span></span>   

* [<span data-ttu-id="ec9e1-160">Linux의 Azure Web App 소개</span><span class="sxs-lookup"><span data-stu-id="ec9e1-160">Introduction to Azure Web App on Linux</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="ec9e1-161">Linux의 Azure Web App에서 Node.js용 PM2 구성 사용</span><span class="sxs-lookup"><span data-stu-id="ec9e1-161">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](./app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="ec9e1-162">Linux의 Azure App Service Web App에 대한 FAQ</span><span class="sxs-lookup"><span data-stu-id="ec9e1-162">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<span data-ttu-id="ec9e1-163">[당사 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview)에 질문 및 문제를 게시하세요.</span><span class="sxs-lookup"><span data-stu-id="ec9e1-163">Post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
