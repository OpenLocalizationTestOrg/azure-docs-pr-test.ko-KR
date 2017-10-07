---
title: "Azure에서 Linux 가상 컴퓨터에서 램프 aaaDeploy | Microsoft Docs"
description: "자습서-Azure에서 Linux VM에 대 한 설치 hello LAMP 스택"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: a3d0ecb3277f15bd0a2fdc0d85b738a760e68865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a>Azure VM에 LAMP 웹 서버 설치
이 문서 toodeploy는 Apache 웹 서버, MySQL 및 Azure의 Ubuntu VM에서 PHP (hello LAMP 스택) 방법을 안내 합니다. Hello NGINX 웹 서버를 선호 하는 경우 참조 hello [LEMP 스택](tutorial-lemp-stack.md) 자습서입니다. toosee hello 램프 서버 작업을 필요에 따라 설치 하 고 수 WordPress 사이트를 구성 합니다. 이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * Ubuntu VM (hello LAMP 스택 hello 'L') 만들기
> * 웹 트래픽에 대해 포트 80 열기
> * Apache, MySQL 및 PHP 설치
> * 설치 및 구성 확인
> * WordPress hello 램프 서버에 설치


Hello LAMP 스택, 프로덕션 환경에 대 한 권장 사항을 비롯 한 자세한 내용은 hello [Ubuntu 설명서](https://help.ubuntu.com/community/ApacheMySQLPHP)합니다.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a>Apache, MySQL 및 PHP 설치

명령 tooupdate Ubuntu 패키지 원본 hello를 실행 하 고 Apache, MySQL 및 PHP를 설치 합니다. Note hello hello 명령 끝에 hello 캐럿 (^).


```bash
sudo apt update && sudo apt install lamp-server^
```



모르는 증명된 tooinstall hello 패키지 및 기타 종속성입니다. 메시지가 표시 되 면 MySQL을 선택한 다음 [Enter] toocontinue 루트 암호를 설정 합니다. Hello 남아 있는 프롬프트를 따릅니다. 이 프로세스는 MySQL 가진 hello 최소 필요한 PHP 확장 필요한 toouse PHP를 설치합니다. 

![MySQL 루트 암호 페이지][1]

## <a name="verify-installation-and-configuration"></a>설치 및 구성 확인


### <a name="apache"></a>Apache

다음 명령을 hello로 Apache의 hello 버전을 확인 합니다.
```bash
apache2 -v
```

설치 되어 있으며 포트 80 apache tooyour VM을 열고, hello에서 이제 hello 웹 서버에 액세스할 수 인터넷 합니다. tooview hello Apache2 Ubuntu 기본 페이지에서 웹 브라우저를 열고 hello hello VM의 공용 IP 주소를 입력 합니다. Hello tooSSH toohello VM을 사용 하는 공용 IP 주소를 사용 합니다.

![Apache 기본 페이지][3]


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

Tootest 추가 하려는 경우 브라우저에서 빠른 PHP 정보 페이지 tooview를 만듭니다. 다음 명령을 hello hello PHP 정보 페이지를 만듭니다.

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

이제 만든 hello PHP 정보 페이지를 확인할 수 있습니다. 브라우저를 열고 너무 이동`http://yourPublicIPAddress/info.php`합니다. VM의 hello 공용 IP 주소를 대체 합니다. 이와 유사한 toothis 이미지 표시 됩니다.

![PHP 정보 페이지][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a>다음 단계

이 자습서에서는 Azure에서 램프 서버를 배포했습니다. 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * Ubuntu VM 만들기
> * 웹 트래픽에 대해 포트 80 열기
> * Apache, MySQL 및 PHP 설치
> * 설치 및 구성 확인
> * WordPress hello 램프 서버에 설치

다음 자습서 toolearn toohello 어떻게 발전 toosecure 웹 서버 SSL 인증서를 사용 합니다.

> [!div class="nextstepaction"]
> [SSL로 웹 서버 보안](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png