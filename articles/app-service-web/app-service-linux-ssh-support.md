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
# <a name="ssh-support-for-azure-web-app-on-linux"></a>Linux의 Azure Web App에 대한 SSH 지원

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>개요

[SSH(보안 셸)](https://en.wikipedia.org/wiki/Secure_Shell)는 네트워크 서비스를 안전하게 사용하기 위한 암호화 네트워크 프로토콜입니다. 이 방법은 명령줄에서 원격으로 안전하게 컴퓨터에 로그인하고 원격으로 관리 명령을 실행하는 데 가장 일반적으로 사용됩니다.

Linux의 웹앱은 새 웹앱의 런타임 스택에 사용되는 각 기본 제공 Docker 이미지를 통해 앱 컨테이너에 SSH 지원을 제공합니다. 

![런타임 스택](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

또한 SSH 서버를 이미지의 일부로 포함하고 이 항목에 설명된 대로 구성하여 사용자 지정 Docker 이미지에서 SSH를 사용할 수도 있습니다.



## <a name="making-a-client-connection"></a>클라이언트 연결 만들기

SSH 클라이언트 연결을 만들려면 주 사이트를 시작해야 합니다. 

다음과 같은 형식을 사용하여 웹앱에 대한 SCM(소스 제어 관리) 끝점을 브라우저에 붙여 넣습니다.

        https://<your sitename>.scm.azurewebsites.net/webssh/host

아직 인증을 받지 못한 경우 연결하기 위해서는 Azure 구독에서 인증을 받아야 합니다.

![SSH 연결](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a>사용자 지정 Docker 이미지를 사용한 SSH 지원

사용자 지정 Docker 이미지로 Azure Portal에서 컨테이너 및 클라이언트 간 SSH 통신을 지원하려면 Docker 이미지에 대해 다음 단계를 수행합니다. 

이러한 단계는 Azure App Service 리포지토리에 예제로 표시됩니다([여기](https://github.com/Azure-App-Service/node/blob/master/6.9.3/) 참조).

1. 이미지에 대한 Dockerfile의 [`RUN` 명령](https://docs.docker.com/engine/reference/builder/#run)에 `openssh-server` 설치를 포함하고 루트 계정에 대한 암호를 `"Docker!"`로 설정합니다. 

    > [!NOTE] 
    > 이 구성을 사용하면 컨테이너에 대한 외부 연결이 허용되지 않습니다. SSH는 게시 자격 증명을 사용하여 인증되는 Kudu/SCM 사이트를 통해서만 액세스할 수 있습니다.

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. [`COPY` 명령](https://docs.docker.com/engine/reference/builder/#copy)을 Dockerfile에 추가하여 [sshd_config](http://man.openbsd.org/sshd_config) 파일을 */etc/ssh/* 디렉터리에 복사합니다. 구성 파일은 Azure-App-Service GitHub 리포지토리([여기](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config) 참조)의 sshd_config 파일을 기준으로 해야 합니다.

    > [!NOTE] 
    > *sshd_config* 파일에 다음이 포함되어야 하며 이러한 항목이 없으면 연결이 실패합니다. 
    > * `Ciphers`에는 다음 중 하나 이상이 포함되어야 합니다. `aes128-cbc,3des-cbc,aes256-cbc`
    > * `MACs`에는 다음 중 하나 이상이 포함되어야 합니다. `hmac-sha1,hmac-sha1-96`

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. Dockerfile에 대한 [`EXPOSE` 명령](https://docs.docker.com/engine/reference/builder/#expose)에 포트 2222를 포함합니다. 루트 암호를 알고 있더라도 인터넷에서 포트 2222에 액세스할 수 없습니다. 개인 가상 네트워크의 브리지 네트워크 내에 있는 컨테이너에서만 액세스할 수 있는 내부 전용 포트입니다.

    ```docker
    EXPOSE 2222 80
    ```

4. ssh 서비스를 시작합니다. [여기](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh)에 제공되는 예제는 */bin* 디렉터리의 셸 스크립트를 사용합니다.

    ```bash
    #!/bin/bash
    service ssh start
    ```

    Dockerfile은 [`CMD` 명령](https://docs.docker.com/engine/reference/builder/#cmd)을 사용하여 스크립트를 실행합니다.

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a>다음 단계
Linux의 웹앱에 대한 자세한 내용은 다음 링크를 참조하세요. [당사 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview)에 질문 및 문제를 게시할 수 있습니다.

* [Linux에서 Azure Web App에 대한 사용자 지정 Docker 이미지를 사용하는 방법](app-service-linux-using-custom-docker-image.md)
* [Linux의 Azure Web App에서 Node.js용 PM2 구성 사용](app-service-linux-using-nodejs-pm2.md)
* [Linux의 Azure Web App에서 .NET Core 사용](app-service-linux-using-dotnetcore.md)
* [Linux의 Azure Web App에서 Ruby 사용](app-service-linux-ruby-get-started.md)
* [Linux의 Azure App Service Web App에 대한 FAQ](app-service-linux-faq.md)

