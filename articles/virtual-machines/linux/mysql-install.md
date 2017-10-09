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
# <a name="how-tooinstall-mysql-on-azure"></a><span data-ttu-id="a0df4-103">어떻게 tooinstall Azure에서 MySQL</span><span class="sxs-lookup"><span data-stu-id="a0df4-103">How tooinstall MySQL on Azure</span></span>
<span data-ttu-id="a0df4-104">이 문서에서는 살펴보겠습니다 방법을 tooinstall 및 Linux를 실행 하는 Azure 가상 컴퓨터에 MySQL을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-104">In this article, you will learn how tooinstall and configure MySQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a><span data-ttu-id="a0df4-105">가상 컴퓨터에 MySQL 설치</span><span class="sxs-lookup"><span data-stu-id="a0df4-105">Install MySQL on your virtual machine</span></span>
> [!NOTE]
> <span data-ttu-id="a0df4-106">이 자습서에서 순서 toocomplete Linux를 실행 하는 Microsoft Azure 가상 컴퓨터를 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-106">You must already have a Microsoft Azure virtual machine running Linux in order toocomplete this tutorial.</span></span> <span data-ttu-id="a0df4-107">참조 하십시오는 [Azure Linux VM 자습서](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate 사용 하 여 Linux VM을 설정 하 고 `mysqlnode` hello VM 이름으로 및 `azureuser` 계속 진행 하기 전에 사용자로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-107">Please see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate and set up a Linux VM with `mysqlnode` as hello VM name and `azureuser` as user before proceeding.</span></span>
> 
> 

<span data-ttu-id="a0df4-108">이 경우 hello MySQL 포트와 3306 포트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-108">In this case, use 3306 port as hello MySQL port.</span></span>  

<span data-ttu-id="a0df4-109">Toohello putty를 통해 만든 Linux VM을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-109">Connect toohello Linux VM you created via putty.</span></span> <span data-ttu-id="a0df4-110">인 경우 hello Azure Linux VM을 사용 하 여 처음으로 toouse putty tooa Linux VM을 연결 하는 방법을 참조 [여기](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-110">If this is hello first time you use Azure Linux VM, see how toouse putty connect tooa Linux VM [here](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="a0df4-111">리포지토리 패키지 tooinstall MySQL5.6이이 문서에서 예로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-111">We will use repository package tooinstall MySQL5.6 as an example in this article.</span></span> <span data-ttu-id="a0df4-112">실제로, MySQL5.6의 성능은 MySQL5.5보다 많이 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-112">Actually, MySQL5.6 has more improvement in performance than MySQL5.5.</span></span>  <span data-ttu-id="a0df4-113">자세한 내용은 [여기](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0df4-113">More information [here](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).</span></span>

### <a name="how-tooinstall-mysql56-on-ubuntu"></a><span data-ttu-id="a0df4-114">어떻게 tooinstall ubuntu MySQL5.6</span><span class="sxs-lookup"><span data-stu-id="a0df4-114">How tooinstall MySQL5.6 on Ubuntu</span></span>
<span data-ttu-id="a0df4-115">여기서는 Azure에 Ubuntu가 있는 Linux VM을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-115">We will use Linux VM with Ubuntu from Azure here.</span></span>

* <span data-ttu-id="a0df4-116">1 단계: MySQL 서버를 설치 하는 5.6 너무 전환`root` 사용자:</span><span class="sxs-lookup"><span data-stu-id="a0df4-116">Step 1: Install MySQL Server 5.6   Switch too`root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="a0df4-117">mysql-server 5.6 설치:</span><span class="sxs-lookup"><span data-stu-id="a0df4-117">Install mysql-server 5.6:</span></span>
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    <span data-ttu-id="a0df4-118">설치 하는 동안 대화 창 poping 나타납니다 tooask를 있습니다 tooset MySQL 루트 아래에 암호를 하 고 필요한 여기에서 설정 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-118">During installation, you will see a dialog window poping up tooask you tooset MySQL root password below, and you need set hello password here.</span></span>
  
    ![이미지](./media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    <span data-ttu-id="a0df4-120">입력된 hello 암호 다시 tooconfirm 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-120">Input hello password again tooconfirm.</span></span>

    ![이미지](./media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* <span data-ttu-id="a0df4-122">2단계: MySQL Server 로그인</span><span class="sxs-lookup"><span data-stu-id="a0df4-122">Step 2: Login MySQL Server</span></span>
  
    <span data-ttu-id="a0df4-123">MySQL Server 설치가 완료되면 MySQL 서비스가 자동으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-123">When MySQL server installation finished, MySQL service will be started automatically.</span></span> <span data-ttu-id="a0df4-124">`root` 사용자로 MySQL Server에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-124">You can login MySQL Server with `root` user.</span></span>
    <span data-ttu-id="a0df4-125">아래 명령 입력 하 고 toologin 암호 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-125">Use hello below command toologin and input password.</span></span>
  
             #[root@mysqlnode ~]# mysql -uroot -p
* <span data-ttu-id="a0df4-126">MySQL 서비스를 실행 하는 hello를 관리 하는 3 단계:</span><span class="sxs-lookup"><span data-stu-id="a0df4-126">Step 3: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="a0df4-127">(a) MySQL 서비스의 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-127">(a) Get status of MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql status
  
    <span data-ttu-id="a0df4-128">(b) MySQL 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-128">(b) Start MySQL Service</span></span>
  
             #[root@mysqlnode ~]# service mysql start
  
    <span data-ttu-id="a0df4-129">(c) MySQL 서비스를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-129">(c) Stop MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql stop
  
    <span data-ttu-id="a0df4-130">(d) hello MySQL 서비스를 다시 시작.</span><span class="sxs-lookup"><span data-stu-id="a0df4-130">(d) Restart hello MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-tooinstall-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a><span data-ttu-id="a0df4-131">Red Hat OS 제품군에서 MySQL tooinstall CentOS, Oracle Linux를 선택 하는 방법</span><span class="sxs-lookup"><span data-stu-id="a0df4-131">How tooinstall MySQL on Red Hat OS family like CentOS, Oracle Linux</span></span>
<span data-ttu-id="a0df4-132">여기에서는 CentOS 또는 Oracle Linux와 함께 Linux VM을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-132">We will use Linux VM with CentOS or Oracle Linux here.</span></span>

* <span data-ttu-id="a0df4-133">1 단계: 추가 hello MySQL Yum 저장소 스위치 너무`root` 사용자:</span><span class="sxs-lookup"><span data-stu-id="a0df4-133">Step 1: Add hello MySQL Yum repository   Switch too`root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="a0df4-134">다운로드 하 고 hello MySQL 릴리스 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-134">Download and install hello MySQL release package:</span></span>
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* <span data-ttu-id="a0df4-135">2 단계: hello MySQL5.6 패키지를 다운로드 하기 위한 파일 tooenable hello MySQL 리포지토리 아래에서 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-135">Step 2: Edit below file tooenable hello MySQL repository for downloading hello MySQL5.6 package.</span></span>
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    <span data-ttu-id="a0df4-136">이 파일 toobelow의 각 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-136">Update each value of this file toobelow:</span></span>
  
        \# *Enable toouse MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* <span data-ttu-id="a0df4-137">3단계: MySQL 리포지토리에서 MySQL 설치 MySQL 설치:</span><span class="sxs-lookup"><span data-stu-id="a0df4-137">Step 3: Install MySQL from MySQL repository   Install MySQL:</span></span>
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    <span data-ttu-id="a0df4-138">MySQL RPM 패키지 및 모든 관련 패키지가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-138">MySQL RPM package and all related packages will be installed.</span></span>
* <span data-ttu-id="a0df4-139">4 단계: MySQL 서비스를 실행 하는 hello 관리</span><span class="sxs-lookup"><span data-stu-id="a0df4-139">Step 4: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="a0df4-140">(a) hello MySQL server hello 서비스 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-140">(a) Check hello service status of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]#service mysqld status
  
    <span data-ttu-id="a0df4-141">(b) hello 기본 포트의 MySQL server 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-141">(b) Check whether hello default port of  MySQL server is running:</span></span>
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    <span data-ttu-id="a0df4-142">(c) hello MySQL 서버를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-142">(c) Start hello MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld start

    <span data-ttu-id="a0df4-143">(d) hello MySQL 서버를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-143">(d) Stop hello MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld stop

    <span data-ttu-id="a0df4-144">(e)를 설정 MySQL toostart hello 시스템 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-144">(e) Set MySQL toostart when hello system boot-up:</span></span>

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-tooinstall-mysql-on-suse-linux"></a><span data-ttu-id="a0df4-145">어떻게 tooinstall SUSE Linux에서 MySQL</span><span class="sxs-lookup"><span data-stu-id="a0df4-145">How tooinstall MySQL on SUSE Linux</span></span>
<span data-ttu-id="a0df4-146">여기에서는 OpenSUSE와 Linux VM을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-146">We will use Linux VM with OpenSUSE here.</span></span>

* <span data-ttu-id="a0df4-147">1단계: MySQL 서버 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="a0df4-147">Step 1: Download and install MySQL Server</span></span>
  
    <span data-ttu-id="a0df4-148">너무 전환`root` 아래의 명령을 통해 사용자:</span><span class="sxs-lookup"><span data-stu-id="a0df4-148">Switch too`root` user through below command:</span></span>  
  
           #sudo su -
  
    <span data-ttu-id="a0df4-149">MySQL 패키지 다운로드 및 설치:</span><span class="sxs-lookup"><span data-stu-id="a0df4-149">Download and install MySQL package:</span></span>
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* <span data-ttu-id="a0df4-150">MySQL 서비스를 실행 하는 hello를 관리 하는 2 단계:</span><span class="sxs-lookup"><span data-stu-id="a0df4-150">Step 2: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="a0df4-151">(a) hello MySQL server hello 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-151">(a) Check hello status of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]# rcmysql status
  
    <span data-ttu-id="a0df4-152">(b) 확인 여부 hello MySQL server의 기본 포트를 hello:</span><span class="sxs-lookup"><span data-stu-id="a0df4-152">(b) Check whether hello default port of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    <span data-ttu-id="a0df4-153">(c) hello MySQL 서버를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-153">(c) Start hello MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql start

    <span data-ttu-id="a0df4-154">(d) hello MySQL 서버를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-154">(d) Stop hello MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql stop

    <span data-ttu-id="a0df4-155">(e)를 설정 MySQL toostart hello 시스템 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-155">(e) Set MySQL toostart when hello system boot-up:</span></span>

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a><span data-ttu-id="a0df4-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a0df4-156">Next Step</span></span>
<span data-ttu-id="a0df4-157">[여기](https://www.mysql.com/)에서 MySQL에 대한 사용법 및 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0df4-157">Find more usage and information regarding MySQL [Here](https://www.mysql.com/).</span></span>

