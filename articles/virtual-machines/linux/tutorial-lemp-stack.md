---
title: "Azure에서 Linux 가상 컴퓨터에서 LEMP aaaDeploy | Microsoft Docs"
description: "자습서-Azure에서 Linux VM에 대 한 설치 hello LEMP 스택"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: d8f9d84c5e9c0df4e9e985c10fe10f63a2f88214
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a>Azure VM에 LEMP 웹 서버 설치
이 문서 toodeploy는 NGINX 웹 서버, MySQL 및 Azure의 Ubuntu VM에서 PHP (hello LEMP 스택) 방법을 안내 합니다. hello LEMP 스택은 널리 사용 되는 대체 toohello [LAMP 스택](tutorial-lamp-stack.md)는 Azure에서 설치할 수 있습니다. toosee hello LEMP 서버 작업을 필요에 따라 설치 하 고 수 WordPress 사이트를 구성 합니다. 이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * Ubuntu VM (hello 'L' hello LEMP 스택의) 만들기
> * 웹 트래픽에 대해 포트 80 열기
> * NGINX, MySQL 및 PHP 설치
> * 설치 및 구성 확인
> * WordPress hello LEMP 서버에 설치


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a>NGINX, MySQL 및 PHP 설치

Hello 명령 tooupdate Ubuntu 패키지 원본 실행 NGINX, MySQL 및 PHP를 설치 하십시오. 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

모르는 증명된 tooinstall hello 패키지 및 기타 종속성입니다. 메시지가 표시 되 면 MySQL을 선택한 다음 [Enter] toocontinue 루트 암호를 설정 합니다. Hello 남아 있는 프롬프트를 따릅니다. 이 프로세스는 MySQL 가진 hello 최소 필요한 PHP 확장 필요한 toouse PHP를 설치합니다. 

![MySQL 루트 암호 페이지][1]

## <a name="verify-installation-and-configuration"></a>설치 및 구성 확인


### <a name="nginx"></a>NGINX

다음 명령을 hello로 NGINX의 hello 버전을 확인 합니다.
```bash
nginx -v
```

NGINX 설치 되어 있으며 포트 80 엽니다 tooyour VM hello 웹 서버 hello에서 액세스할 수 있습니다, 인터넷 합니다. tooview hello NGINX 시작 페이지에서 웹 브라우저를 열고 hello hello VM의 공용 IP 주소를 입력 합니다. Hello tooSSH toohello VM을 사용 하는 공용 IP 주소를 사용 합니다.

![NGINX 기본 페이지][3]


### <a name="mysql"></a>MySQL

다음 명령을 hello로 MySQL의 hello 버전을 확인 (참고 hello 자본 `V` 매개 변수):

```bash
msql -V
```

Hello MySQL의 toohelp 보안 hello 설치 스크립트를 실행 하는 것이 좋습니다.

```bash
mysql_secure_installation
```

MySQL 루트 암호를 입력 하 고 사용자 환경에 대 한 hello 보안 설정을 구성 합니다.

Toocreate MySQL 데이터베이스 사용자를 추가 하거나 로그인 tooMySQL 구성 설정을 변경 합니다.

```bash
mysql -u root -p
```

을 완료 한 후를 입력 하 여 hello mysql 프롬프트를 종료 `\q`합니다.

### <a name="php"></a>PHP

다음 명령을 hello로 hello PHP 버전을 확인 합니다.

```bash
php -v
```

NGINX toouse hello PHP FastCGI 프로세스 관리자 (PHP FPM)를 구성 합니다. 다음 명령은 tooback hello 원래 NGINX 서버를 구성 파일을 차단 하 고 다음 hello 원하는 편집기에 원본 파일을 편집 하는 hello를 실행 합니다.

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

Hello 편집기에서의 hello 내용을 대체 `/etc/nginx/sites-available/default` hello 다음과 같이 합니다. 에 대 한 설명은 hello 설정의 hello 주석을 참조 하십시오. Hello에 대 한 VM의 공용 IP 주소 대체 *yourPublicIPAddress*, hello 남은 설정을 유지 합니다. Hello 파일을 저장 합니다.

```
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;
    # Homepage of website is index.php
    index index.php;

    server_name yourPublicIPAddress;

    location / {
        try_files $uri $uri/ =404;
    }

    # Include FastCGI configuration for NGINX
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.0-fpm.sock;
    }
}
```

구문 오류에 대 한 hello NGINX 구성을 확인 하십시오.

```bash
sudo nginx -t
```

Hello 구문이 올바른 경우 다음 명령을 hello로 NGINX 다시 시작 합니다.

```bash
sudo service nginx restart
```

Tootest 추가 하려는 경우 브라우저에서 빠른 PHP 정보 페이지 tooview를 만듭니다. 다음 명령을 hello hello PHP 정보 페이지를 만듭니다.

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



이제 만든 hello PHP 정보 페이지를 확인할 수 있습니다. 브라우저를 열고 너무 이동`http://yourPublicIPAddress/info.php`합니다. VM의 hello 공용 IP 주소를 대체 합니다. 이와 유사한 toothis 이미지 표시 됩니다.

![PHP 정보 페이지][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a>다음 단계

이 자습서에서는 Azure에서 LEMP 서버를 배포했습니다. 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * Ubuntu VM 만들기
> * 웹 트래픽에 대해 포트 80 열기
> * NGINX, MySQL 및 PHP 설치
> * 설치 및 구성 확인
> * Hello LEMP 스택에 WordPress 설치

다음 자습서 toolearn toohello 어떻게 발전 toosecure 웹 서버 SSL 인증서를 사용 합니다.

> [!div class="nextstepaction"]
> [SSL로 웹 서버 보안](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
