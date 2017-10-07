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
# <a name="ssh-support-for-azure-web-app-on-linux"></a>Linux의 Azure Web App에 대한 SSH 지원

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>개요

[SSH(보안 셸)](https://en.wikipedia.org/wiki/Secure_Shell)는 네트워크 서비스를 안전하게 사용하기 위한 암호화 네트워크 프로토콜입니다. 가장 일반적으로 사용된 toolog 시스템에 원격으로 안전 하 게 명령줄에서 사용 되며 원격으로 관리 명령을 실행 합니다.

웹 응용 프로그램에 액세스 Linux 각각 hello 새 웹 응용 프로그램의 런타임 스택을 hello에 사용 되는 기본 제공 Docker 이미지와 hello 응용 프로그램 컨테이너에 대 한 SSH 지원을 제공 합니다. 

![런타임 스택](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

Hello 이미지의 일부로 hello SSH 서버를 포함 하 고이 항목에 설명 된 대로 구성 하 여 사용자 지정 Docker 이미지와 SSH를 사용할 수 있습니다.



## <a name="making-a-client-connection"></a>클라이언트 연결 만들기

SSH 클라이언트 연결을 주 사이트 hello toomake 시작 되어야 합니다. 

웹 앱에 대 한 소스 제어 관리 (SCM) 끝점을 hello 양식 다음 hello를 사용 하 여 브라우저에 붙여 넣습니다.

        https://<your sitename>.scm.azurewebsites.net/webssh/host

인증 이미 되지 않은 경우 사용자가 필요한 tooauthenticate Azure 구독 tooconnect입니다.

![SSH 연결](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a>사용자 지정 Docker 이미지를 사용한 SSH 지원

사용자 지정 Docker 이미지 toosupport SSH 간의 통신을 위해 hello 컨테이너와 hello 클라이언트 hello Azure 포털에에서 Docker 이미지에 대 한 단계를 수행 하는 hello를 수행 하십시오. 

예를 들어 Azure 앱 서비스 저장소 hello에 표시 되는 이러한 단계는 [여기](https://github.com/Azure-App-Service/node/blob/master/6.9.3/)합니다.

1. Hello 포함 `openssh-server` 에서 설치 [ `RUN` 명령](https://docs.docker.com/engine/reference/builder/#run) Dockerfile 이미지에 대 한 hello와 hello 루트 계정에 대 한 hello 암호를 너무 설정`"Docker!"`합니다. 

    > [!NOTE] 
    > 이 구성은 toohello 컨테이너는 외부 연결을 허용 하지 않습니다. SSH를 사용 하 여 인증 되는 SCM 사이트 hello 게시 자격 증명 / Kudu hello를 통해 액세스할 수 있습니다.

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. 추가 [ `COPY` 명령](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy는 [sshd_config](http://man.openbsd.org/sshd_config) toohello 파일 */등/ssh/* 디렉터리입니다. 구성 파일 hello Azure 앱 서비스 GitHub 리포지토리에 쿼리하여 sshd_config 파일에 따라 [여기](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config)합니다.

    > [!NOTE] 
    > hello *sshd_config* 파일 hello 다음이 있어야 합니다. 또는 hello 연결이 실패 합니다. 
    > * `Ciphers`hello 다음 중 하나 이상 포함 해야 합니다: `aes128-cbc,3des-cbc,aes256-cbc`합니다.
    > * `MACs`hello 다음 중 하나 이상 포함 해야 합니다: `hmac-sha1,hmac-sha1-96`합니다.

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. Hello에 포트 2222 포함 [ `EXPOSE` 명령](https://docs.docker.com/engine/reference/builder/#expose) hello Dockerfile에 대 한 합니다. 포트 2222 hello에서 액세스할 수 없는 hello 루트 암호를 알고 있지만 인터넷 합니다. 개인 가상 네트워크의 hello 브리지 네트워크 내의 컨테이너에 의해서만 액세스할 수 있는 내부 전용 포트 이며

    ```docker
    EXPOSE 2222 80
    ```

4. Toostart hello ssh 서비스 있는지 확인 합니다. hello 예제 [여기](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) 에 셸 스크립트를 사용 하 여 */b i n* 디렉터리입니다.

    ```bash
    #!/bin/bash
    service ssh start
    ```

    Dockerfile hello hello를 사용 하 여 [ `CMD` 명령](https://docs.docker.com/engine/reference/builder/#cmd) toorun hello 스크립트입니다.

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a>다음 단계
Linux에서 웹 앱에 대 한 자세한 정보에 대 한 링크를 따라 hello를 참조 하십시오. [당사 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview)에 질문 및 문제를 게시할 수 있습니다.

* [Linux에서 Azure 웹 앱에 대 한 사용자 지정 Docker toouse 이미지 방법](app-service-linux-using-custom-docker-image.md)
* [Linux의 Azure Web App에서 Node.js용 PM2 구성 사용](app-service-linux-using-nodejs-pm2.md)
* [Linux의 Azure Web App에서 .NET Core 사용](app-service-linux-using-dotnetcore.md)
* [Linux의 Azure Web App에서 Ruby 사용](app-service-linux-ruby-get-started.md)
* [Linux의 Azure App Service Web App에 대한 FAQ](app-service-linux-faq.md)

