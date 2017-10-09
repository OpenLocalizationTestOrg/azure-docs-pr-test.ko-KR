---
title: "Azure에서 Linux VM에 MySQL aaaSet | Microsoft Docs"
description: "Azure에서 Linux 가상 컴퓨터 (Ubuntu 또는 RedHat 제품군 운영 체제)에서 tooinstall hello MySQL 스택 하는 방법에 대해 알아봅니다"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 153bae7c-897b-46b3-bd86-192a6efb94fa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: e47d0de7f0eb5bb873ad20e4bc35f1b5f8d33bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-mysql-on-azure"></a>어떻게 tooinstall Azure에서 MySQL
이 문서에서는 살펴보겠습니다 방법을 tooinstall 및 Linux를 실행 하는 Azure 가상 컴퓨터에 MySQL을 구성 합니다.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a>가상 컴퓨터에 MySQL 설치
> [!NOTE]
> 이 자습서에서 순서 toocomplete Linux를 실행 하는 Microsoft Azure 가상 컴퓨터를 이미 있어야 합니다. 참조 하십시오는 [Azure Linux VM 자습서](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate 사용 하 여 Linux VM을 설정 하 고 `mysqlnode` hello VM 이름으로 및 `azureuser` 계속 진행 하기 전에 사용자로 합니다.
> 
> 

이 경우 hello MySQL 포트와 3306 포트를 사용 합니다.  

Toohello putty를 통해 만든 Linux VM을 연결 합니다. 인 경우 hello Azure Linux VM을 사용 하 여 처음으로 toouse putty tooa Linux VM을 연결 하는 방법을 참조 [여기](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

리포지토리 패키지 tooinstall MySQL5.6이이 문서에서 예로 사용 합니다. 실제로, MySQL5.6의 성능은 MySQL5.5보다 많이 개선되었습니다.  자세한 내용은 [여기](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/)를 참조하세요.

### <a name="how-tooinstall-mysql56-on-ubuntu"></a>어떻게 tooinstall ubuntu MySQL5.6
여기서는 Azure에 Ubuntu가 있는 Linux VM을 사용합니다.

* 1 단계: MySQL 서버를 설치 하는 5.6 너무 전환`root` 사용자:
  
            #[azureuser@mysqlnode:~]sudo su -
  
    mysql-server 5.6 설치:
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    설치 하는 동안 대화 창 poping 나타납니다 tooask를 있습니다 tooset MySQL 루트 아래에 암호를 하 고 필요한 여기에서 설정 hello 암호입니다.
  
    ![이미지](./media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    입력된 hello 암호 다시 tooconfirm 합니다.

    ![이미지](./media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* 2단계: MySQL Server 로그인
  
    MySQL Server 설치가 완료되면 MySQL 서비스가 자동으로 시작됩니다. `root` 사용자로 MySQL Server에 로그인할 수 있습니다.
    아래 명령 입력 하 고 toologin 암호 hello를 사용 합니다.
  
             #[root@mysqlnode ~]# mysql -uroot -p
* MySQL 서비스를 실행 하는 hello를 관리 하는 3 단계:
  
    (a) MySQL 서비스의 상태를 가져옵니다.
  
             #[root@mysqlnode ~]# service mysql status
  
    (b) MySQL 서비스를 시작합니다.
  
             #[root@mysqlnode ~]# service mysql start
  
    (c) MySQL 서비스를 중지합니다.
  
             #[root@mysqlnode ~]# service mysql stop
  
    (d) hello MySQL 서비스를 다시 시작.
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-tooinstall-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a>Red Hat OS 제품군에서 MySQL tooinstall CentOS, Oracle Linux를 선택 하는 방법
여기에서는 CentOS 또는 Oracle Linux와 함께 Linux VM을 사용합니다.

* 1 단계: 추가 hello MySQL Yum 저장소 스위치 너무`root` 사용자:
  
            #[azureuser@mysqlnode:~]sudo su -
  
    다운로드 하 고 hello MySQL 릴리스 패키지를 설치 합니다.
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* 2 단계: hello MySQL5.6 패키지를 다운로드 하기 위한 파일 tooenable hello MySQL 리포지토리 아래에서 편집 합니다.
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    이 파일 toobelow의 각 값을 업데이트 합니다.
  
        \# *Enable toouse MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* 3단계: MySQL 리포지토리에서 MySQL 설치 MySQL 설치:
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    MySQL RPM 패키지 및 모든 관련 패키지가 설치됩니다.
* 4 단계: MySQL 서비스를 실행 하는 hello 관리
  
    (a) hello MySQL server hello 서비스 상태를 확인 합니다.
  
           #[root@mysqlnode ~]#service mysqld status
  
    (b) hello 기본 포트의 MySQL server 실행 되 고 있는지 확인 합니다.
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    (c) hello MySQL 서버를 시작 합니다.

           #[root@mysqlnode ~]#service mysqld start

    (d) hello MySQL 서버를 중지 합니다.

           #[root@mysqlnode ~]#service mysqld stop

    (e)를 설정 MySQL toostart hello 시스템 부팅 합니다.

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-tooinstall-mysql-on-suse-linux"></a>어떻게 tooinstall SUSE Linux에서 MySQL
여기에서는 OpenSUSE와 Linux VM을 사용합니다.

* 1단계: MySQL 서버 다운로드 및 설치
  
    너무 전환`root` 아래의 명령을 통해 사용자:  
  
           #sudo su -
  
    MySQL 패키지 다운로드 및 설치:
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* MySQL 서비스를 실행 하는 hello를 관리 하는 2 단계:
  
    (a) hello MySQL server hello 상태를 확인 합니다.
  
           #[root@mysqlnode ~]# rcmysql status
  
    (b) 확인 여부 hello MySQL server의 기본 포트를 hello:
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    (c) hello MySQL 서버를 시작 합니다.

           #[root@mysqlnode ~]# rcmysql start

    (d) hello MySQL 서버를 중지 합니다.

           #[root@mysqlnode ~]# rcmysql stop

    (e)를 설정 MySQL toostart hello 시스템 부팅 합니다.

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a>다음 단계
[여기](https://www.mysql.com/)에서 MySQL에 대한 사용법 및 정보를 확인합니다.

