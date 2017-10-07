---
title: "Linux에서 Azure 앱 서비스 웹 앱에 대 한 aaaSSH 지원 | Microsoft Docs"
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
ms.openlocfilehash: e00be6d4631e8936a2a8bc106da1fc06237a4b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="ssh-support-for-azure-web-app-on-linux"></a><span data-ttu-id="074b9-104">Linux의 Azure Web App에 대한 SSH 지원</span><span class="sxs-lookup"><span data-stu-id="074b9-104">SSH support for Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="074b9-105">개요</span><span class="sxs-lookup"><span data-stu-id="074b9-105">Overview</span></span>

<span data-ttu-id="074b9-106">[SSH(보안 셸)](https://en.wikipedia.org/wiki/Secure_Shell)는 네트워크 서비스를 안전하게 사용하기 위한 암호화 네트워크 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="074b9-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) is a cryptographic network protocol for using network services securely.</span></span> <span data-ttu-id="074b9-107">가장 일반적으로 사용된 toolog 시스템에 원격으로 안전 하 게 명령줄에서 사용 되며 원격으로 관리 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="074b9-107">It is most commonly used toolog into a system remotely securely from a command-line and execute administrative commands remotely.</span></span>

<span data-ttu-id="074b9-108">웹 응용 프로그램에 액세스 Linux 각각 hello 새 웹 응용 프로그램의 런타임 스택을 hello에 사용 되는 기본 제공 Docker 이미지와 hello 응용 프로그램 컨테이너에 대 한 SSH 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="074b9-108">Web App on Linux provides SSH support into hello app container with each of hello built-in Docker images used for hello Runtime Stack of new web apps.</span></span> 

![런타임 스택](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

<span data-ttu-id="074b9-110">Hello 이미지의 일부로 hello SSH 서버를 포함 하 고이 항목에 설명 된 대로 구성 하 여 사용자 지정 Docker 이미지와 SSH를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="074b9-110">You can also use SSH with your custom Docker images by including hello SSH server as part of hello image and configuring it as described in this topic.</span></span>



## <a name="making-a-client-connection"></a><span data-ttu-id="074b9-111">클라이언트 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="074b9-111">Making a client connection</span></span>

<span data-ttu-id="074b9-112">SSH 클라이언트 연결을 주 사이트 hello toomake 시작 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="074b9-112">toomake an SSH client connection, hello main site must be started.</span></span> 

<span data-ttu-id="074b9-113">웹 앱에 대 한 소스 제어 관리 (SCM) 끝점을 hello 양식 다음 hello를 사용 하 여 브라우저에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="074b9-113">Paste hello Source Control Management (SCM) endpoint for your web app into your browser using hello following form:</span></span>

        https://<your sitename>.scm.azurewebsites.net/webssh/host

<span data-ttu-id="074b9-114">인증 이미 되지 않은 경우 사용자가 필요한 tooauthenticate Azure 구독 tooconnect입니다.</span><span class="sxs-lookup"><span data-stu-id="074b9-114">If you are not already authenticated, you are required tooauthenticate with your Azure subscription tooconnect.</span></span>

![SSH 연결](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a><span data-ttu-id="074b9-116">사용자 지정 Docker 이미지를 사용한 SSH 지원</span><span class="sxs-lookup"><span data-stu-id="074b9-116">SSH support with custom Docker images</span></span>

<span data-ttu-id="074b9-117">사용자 지정 Docker 이미지 toosupport SSH 간의 통신을 위해 hello 컨테이너와 hello 클라이언트 hello Azure 포털에에서 Docker 이미지에 대 한 단계를 수행 하는 hello를 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="074b9-117">In order for a custom Docker image toosupport SSH communication between hello container and hello client in hello Azure portal, perform hello following steps for your Docker image.</span></span> 

<span data-ttu-id="074b9-118">예를 들어 Azure 앱 서비스 저장소 hello에 표시 되는 이러한 단계는 [여기](https://github.com/Azure-App-Service/node/blob/master/6.9.3/)합니다.</span><span class="sxs-lookup"><span data-stu-id="074b9-118">These steps are are shown in hello Azure App Service repository as an example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span></span>

1. <span data-ttu-id="074b9-119">Hello 포함 `openssh-server` 에서 설치 [ `RUN` 명령](https://docs.docker.com/engine/reference/builder/#run) Dockerfile 이미지에 대 한 hello와 hello 루트 계정에 대 한 hello 암호를 너무 설정`"Docker!"`합니다.</span><span class="sxs-lookup"><span data-stu-id="074b9-119">Include hello `openssh-server` installation in [`RUN` instruction](https://docs.docker.com/engine/reference/builder/#run) in hello Dockerfile for your image and set hello password for hello root account too`"Docker!"`.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="074b9-120">이 구성은 toohello 컨테이너는 외부 연결을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="074b9-120">This configuration does not allow external connections toohello container.</span></span> <span data-ttu-id="074b9-121">SSH를 사용 하 여 인증 되는 SCM 사이트 hello 게시 자격 증명 / Kudu hello를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="074b9-121">SSH can only be accessed via hello Kudu / SCM Site, which is authenticated using hello publishing credentials.</span></span>

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. <span data-ttu-id="074b9-122">추가 [ `COPY` 명령](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy는 [sshd_config](http://man.openbsd.org/sshd_config) toohello 파일 */등/ssh/* 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="074b9-122">Add a [`COPY` instruction](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy a [sshd_config](http://man.openbsd.org/sshd_config) file toohello */etc/ssh/* directory.</span></span> <span data-ttu-id="074b9-123">구성 파일 hello Azure 앱 서비스 GitHub 리포지토리에 쿼리하여 sshd_config 파일에 따라 [여기](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config)합니다.</span><span class="sxs-lookup"><span data-stu-id="074b9-123">Your configuration file should be based on our sshd_config file in hello Azure-App-Service GitHub repository [here](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span></span>

    > [!NOTE] 
    > <span data-ttu-id="074b9-124">hello *sshd_config* 파일 hello 다음이 있어야 합니다. 또는 hello 연결이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="074b9-124">hello *sshd_config* file must include hello following or hello connection fails:</span></span> 
    > * <span data-ttu-id="074b9-125">`Ciphers`hello 다음 중 하나 이상 포함 해야 합니다: `aes128-cbc,3des-cbc,aes256-cbc`합니다.</span><span class="sxs-lookup"><span data-stu-id="074b9-125">`Ciphers` must include at least one of hello following: `aes128-cbc,3des-cbc,aes256-cbc`.</span></span>
    > * <span data-ttu-id="074b9-126">`MACs`hello 다음 중 하나 이상 포함 해야 합니다: `hmac-sha1,hmac-sha1-96`합니다.</span><span class="sxs-lookup"><span data-stu-id="074b9-126">`MACs` must include at least one of hello following: `hmac-sha1,hmac-sha1-96`.</span></span>

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. <span data-ttu-id="074b9-127">Hello에 포트 2222 포함 [ `EXPOSE` 명령](https://docs.docker.com/engine/reference/builder/#expose) hello Dockerfile에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="074b9-127">Include port 2222 in hello [`EXPOSE` instruction](https://docs.docker.com/engine/reference/builder/#expose) for hello Dockerfile.</span></span> <span data-ttu-id="074b9-128">포트 2222 hello에서 액세스할 수 없는 hello 루트 암호를 알고 있지만 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="074b9-128">Although hello root password is known, port 2222 cannot be accessed from hello internet.</span></span> <span data-ttu-id="074b9-129">개인 가상 네트워크의 hello 브리지 네트워크 내의 컨테이너에 의해서만 액세스할 수 있는 내부 전용 포트 이며</span><span class="sxs-lookup"><span data-stu-id="074b9-129">It is an internal only port accessible only by containers within hello bridge network of a private virtual network.</span></span>

    ```docker
    EXPOSE 2222 80
    ```

4. <span data-ttu-id="074b9-130">Toostart hello ssh 서비스 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="074b9-130">Make sure toostart hello ssh service.</span></span> <span data-ttu-id="074b9-131">hello 예제 [여기](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) 에 셸 스크립트를 사용 하 여 */b i n* 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="074b9-131">hello example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) uses a shell script in */bin* directory.</span></span>

    ```bash
    #!/bin/bash
    service ssh start
    ```

    <span data-ttu-id="074b9-132">Dockerfile hello hello를 사용 하 여 [ `CMD` 명령](https://docs.docker.com/engine/reference/builder/#cmd) toorun hello 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="074b9-132">hello Dockerfile uses hello [`CMD` instruction](https://docs.docker.com/engine/reference/builder/#cmd) toorun hello script.</span></span>

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a><span data-ttu-id="074b9-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="074b9-133">Next steps</span></span>
<span data-ttu-id="074b9-134">Linux에서 웹 앱에 대 한 자세한 정보에 대 한 링크를 따라 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="074b9-134">See hello following links for more information regarding Web App on Linux.</span></span> <span data-ttu-id="074b9-135">[당사 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview)에 질문 및 문제를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="074b9-135">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="074b9-136">Linux에서 Azure 웹 앱에 대 한 사용자 지정 Docker toouse 이미지 방법</span><span class="sxs-lookup"><span data-stu-id="074b9-136">How toouse a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="074b9-137">Linux의 Azure Web App에서 Node.js용 PM2 구성 사용</span><span class="sxs-lookup"><span data-stu-id="074b9-137">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="074b9-138">Linux의 Azure Web App에서 .NET Core 사용</span><span class="sxs-lookup"><span data-stu-id="074b9-138">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="074b9-139">Linux의 Azure Web App에서 Ruby 사용</span><span class="sxs-lookup"><span data-stu-id="074b9-139">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="074b9-140">Linux의 Azure App Service Web App에 대한 FAQ</span><span class="sxs-lookup"><span data-stu-id="074b9-140">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

