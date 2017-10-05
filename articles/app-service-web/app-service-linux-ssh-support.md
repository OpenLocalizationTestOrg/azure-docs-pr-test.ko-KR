---
title: "Linux의 Azure App Service Web App에 대한 SSH 지원 | Microsoft Docs"
description: "Linux의 Azure Web App에서 SSH를 사용하는 경우에 대해 자세히 알아봅니다."
keywords: "azure app service, 웹앱, linux, oss"
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 66f9988f-8ffa-414a-9137-3a9b15a5573c
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: wesmc
ms.openlocfilehash: feee7a5c91d213a6b0bfdaf264a4da4d9e79cbe7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="ssh-support-for-azure-web-app-on-linux"></a><span data-ttu-id="f4670-104">Linux의 Azure Web App에 대한 SSH 지원</span><span class="sxs-lookup"><span data-stu-id="f4670-104">SSH support for Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="f4670-105">개요</span><span class="sxs-lookup"><span data-stu-id="f4670-105">Overview</span></span>

<span data-ttu-id="f4670-106">[SSH(보안 셸)](https://en.wikipedia.org/wiki/Secure_Shell)는 네트워크 서비스를 안전하게 사용하기 위한 암호화 네트워크 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="f4670-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) is a cryptographic network protocol for using network services securely.</span></span> <span data-ttu-id="f4670-107">이 방법은 명령줄에서 원격으로 안전하게 컴퓨터에 로그인하고 원격으로 관리 명령을 실행하는 데 가장 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4670-107">It is most commonly used to log into a system remotely securely from a command-line and execute administrative commands remotely.</span></span>

<span data-ttu-id="f4670-108">Linux의 웹앱은 새 웹앱의 런타임 스택에 사용되는 각 기본 제공 Docker 이미지를 통해 앱 컨테이너에 SSH 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f4670-108">Web App on Linux provides SSH support into the app container with each of the built-in Docker images used for the Runtime Stack of new web apps.</span></span> 

![런타임 스택](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

<span data-ttu-id="f4670-110">또한 SSH 서버를 이미지의 일부로 포함하고 이 항목에 설명된 대로 구성하여 사용자 지정 Docker 이미지에서 SSH를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4670-110">You can also use SSH with your custom Docker images by including the SSH server as part of the image and configuring it as described in this topic.</span></span>



## <a name="making-a-client-connection"></a><span data-ttu-id="f4670-111">클라이언트 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="f4670-111">Making a client connection</span></span>

<span data-ttu-id="f4670-112">SSH 클라이언트 연결을 만들려면 주 사이트를 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4670-112">To make an SSH client connection, the main site must be started.</span></span> 

<span data-ttu-id="f4670-113">다음과 같은 형식을 사용하여 웹앱에 대한 SCM(소스 제어 관리) 끝점을 브라우저에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f4670-113">Paste the Source Control Management (SCM) endpoint for your web app into your browser using the following form:</span></span>

        https://<your sitename>.scm.azurewebsites.net/webssh/host

<span data-ttu-id="f4670-114">아직 인증을 받지 못한 경우 연결하기 위해서는 Azure 구독에서 인증을 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4670-114">If you are not already authenticated, you are required to authenticate with your Azure subscription to connect.</span></span>

![SSH 연결](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a><span data-ttu-id="f4670-116">사용자 지정 Docker 이미지를 사용한 SSH 지원</span><span class="sxs-lookup"><span data-stu-id="f4670-116">SSH support with custom Docker images</span></span>

<span data-ttu-id="f4670-117">사용자 지정 Docker 이미지로 Azure Portal에서 컨테이너 및 클라이언트 간 SSH 통신을 지원하려면 Docker 이미지에 대해 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f4670-117">In order for a custom Docker image to support SSH communication between the container and the client in the Azure portal, perform the following steps for your Docker image.</span></span> 

<span data-ttu-id="f4670-118">이러한 단계는 Azure App Service 리포지토리에 예제로 표시됩니다([여기](https://github.com/Azure-App-Service/node/blob/master/6.9.3/) 참조).</span><span class="sxs-lookup"><span data-stu-id="f4670-118">These steps are are shown in the Azure App Service repository as an example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span></span>

1. <span data-ttu-id="f4670-119">이미지에 대한 Dockerfile의 [`RUN` 명령](https://docs.docker.com/engine/reference/builder/#run)에 `openssh-server` 설치를 포함하고 루트 계정에 대한 암호를 `"Docker!"`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f4670-119">Include the `openssh-server` installation in [`RUN` instruction](https://docs.docker.com/engine/reference/builder/#run) in the Dockerfile for your image and set the password for the root account to `"Docker!"`.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="f4670-120">이 구성을 사용하면 컨테이너에 대한 외부 연결이 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4670-120">This configuration does not allow external connections to the container.</span></span> <span data-ttu-id="f4670-121">SSH는 게시 자격 증명을 사용하여 인증되는 Kudu/SCM 사이트를 통해서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4670-121">SSH can only be accessed via the Kudu / SCM Site, which is authenticated using the publishing credentials.</span></span>

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. <span data-ttu-id="f4670-122">[`COPY` 명령](https://docs.docker.com/engine/reference/builder/#copy)을 Dockerfile에 추가하여 [sshd_config](http://man.openbsd.org/sshd_config) 파일을 */etc/ssh/* 디렉터리에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f4670-122">Add a [`COPY` instruction](https://docs.docker.com/engine/reference/builder/#copy) to the Dockerfile to copy a [sshd_config](http://man.openbsd.org/sshd_config) file to the */etc/ssh/* directory.</span></span> <span data-ttu-id="f4670-123">구성 파일은 Azure-App-Service GitHub 리포지토리([여기](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config) 참조)의 sshd_config 파일을 기준으로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4670-123">Your configuration file should be based on our sshd_config file in the Azure-App-Service GitHub repository [here](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f4670-124">*sshd_config* 파일에 다음이 포함되어야 하며 이러한 항목이 없으면 연결이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="f4670-124">The *sshd_config* file must include the following or the connection fails:</span></span> 
    > * <span data-ttu-id="f4670-125">`Ciphers`에는 다음 중 하나 이상이 포함되어야 합니다. `aes128-cbc,3des-cbc,aes256-cbc`</span><span class="sxs-lookup"><span data-stu-id="f4670-125">`Ciphers` must include at least one of the following: `aes128-cbc,3des-cbc,aes256-cbc`.</span></span>
    > * <span data-ttu-id="f4670-126">`MACs`에는 다음 중 하나 이상이 포함되어야 합니다. `hmac-sha1,hmac-sha1-96`</span><span class="sxs-lookup"><span data-stu-id="f4670-126">`MACs` must include at least one of the following: `hmac-sha1,hmac-sha1-96`.</span></span>

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. <span data-ttu-id="f4670-127">Dockerfile에 대한 [`EXPOSE` 명령](https://docs.docker.com/engine/reference/builder/#expose)에 포트 2222를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f4670-127">Include port 2222 in the [`EXPOSE` instruction](https://docs.docker.com/engine/reference/builder/#expose) for the Dockerfile.</span></span> <span data-ttu-id="f4670-128">루트 암호를 알고 있더라도 인터넷에서 포트 2222에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f4670-128">Although the root password is known, port 2222 cannot be accessed from the internet.</span></span> <span data-ttu-id="f4670-129">개인 가상 네트워크의 브리지 네트워크 내에 있는 컨테이너에서만 액세스할 수 있는 내부 전용 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="f4670-129">It is an internal only port accessible only by containers within the bridge network of a private virtual network.</span></span>

    ```docker
    EXPOSE 2222 80
    ```

4. <span data-ttu-id="f4670-130">ssh 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f4670-130">Make sure to start the ssh service.</span></span> <span data-ttu-id="f4670-131">[여기](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh)에 제공되는 예제는 */bin* 디렉터리의 셸 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4670-131">The example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) uses a shell script in */bin* directory.</span></span>

    ```bash
    #!/bin/bash
    service ssh start
    ```

    <span data-ttu-id="f4670-132">Dockerfile은 [`CMD` 명령](https://docs.docker.com/engine/reference/builder/#cmd)을 사용하여 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f4670-132">The Dockerfile uses the [`CMD` instruction](https://docs.docker.com/engine/reference/builder/#cmd) to run the script.</span></span>

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a><span data-ttu-id="f4670-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f4670-133">Next steps</span></span>
<span data-ttu-id="f4670-134">Linux의 웹앱에 대한 자세한 내용은 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4670-134">See the following links for more information regarding Web App on Linux.</span></span> <span data-ttu-id="f4670-135">[당사 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview)에 질문 및 문제를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4670-135">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="f4670-136">Linux에서 Azure Web App에 대한 사용자 지정 Docker 이미지를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="f4670-136">How to use a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="f4670-137">Linux의 Azure Web App에서 Node.js용 PM2 구성 사용</span><span class="sxs-lookup"><span data-stu-id="f4670-137">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="f4670-138">Linux의 Azure Web App에서 .NET Core 사용</span><span class="sxs-lookup"><span data-stu-id="f4670-138">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="f4670-139">Linux의 Azure Web App에서 Ruby 사용</span><span class="sxs-lookup"><span data-stu-id="f4670-139">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="f4670-140">Linux의 Azure App Service Web App에 대한 FAQ</span><span class="sxs-lookup"><span data-stu-id="f4670-140">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

