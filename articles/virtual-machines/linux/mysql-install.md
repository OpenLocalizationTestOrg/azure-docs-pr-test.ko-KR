---
title: "Azure의 Linux VM에서 MySQL 설정 | Microsoft Docs"
description: "Azure Linux 가상 컴퓨터(Ubuntu 또는 RedHat 제품군 OS)에 MySQL 스택을 설치하는 방법을 알아봅니다."
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
ms.openlocfilehash: 0ee70bda954cf0a193d43b5b47702e7b2c37844d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-mysql-on-azure"></a><span data-ttu-id="c22d0-103">Azure에 MySQL을 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="c22d0-103">How to install MySQL on Azure</span></span>
<span data-ttu-id="c22d0-104">이 문서에서는 Linux를 실행하는 Azure 가상 컴퓨터에서 MySQL을 설치 및 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c22d0-104">In this article, you will learn how to install and configure MySQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a><span data-ttu-id="c22d0-105">가상 컴퓨터에 MySQL 설치</span><span class="sxs-lookup"><span data-stu-id="c22d0-105">Install MySQL on your virtual machine</span></span>
> [!NOTE]
> <span data-ttu-id="c22d0-106">이 자습서를 완료하려면 Linux를 실행하는 Microsoft Azure 가상 컴퓨터가 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c22d0-106">You must already have a Microsoft Azure virtual machine running Linux in order to complete this tutorial.</span></span> <span data-ttu-id="c22d0-107">계속하기 전에 VM 이름으로 `mysqlnode`를 사용하고 사용자로 `azureuser`를 사용하여 Linux VM을 만들고 설정하려면 [Azure Linux VM 자습서](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c22d0-107">Please see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to create and set up a Linux VM with `mysqlnode` as the VM name and `azureuser` as user before proceeding.</span></span>
> 
> 

<span data-ttu-id="c22d0-108">이 경우 3306 포트를 MySQL 포트로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c22d0-108">In this case, use 3306 port as the MySQL port.</span></span>  

<span data-ttu-id="c22d0-109">putty를 통해 생성한 Linux VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c22d0-109">Connect to the Linux VM you created via putty.</span></span> <span data-ttu-id="c22d0-110">처음으로 Azure Linux VM을 사용하는 경우 putty를 사용하여 Linux VM에 연결하는 방법은 [여기](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c22d0-110">If this is the first time you use Azure Linux VM, see how to use putty connect to a Linux VM [here](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="c22d0-111">이 문서의 예로는 MySQL5.6을 설치하는 리포지토리 패키지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c22d0-111">We will use repository package to install MySQL5.6 as an example in this article.</span></span> <span data-ttu-id="c22d0-112">실제로, MySQL5.6의 성능은 MySQL5.5보다 많이 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c22d0-112">Actually, MySQL5.6 has more improvement in performance than MySQL5.5.</span></span>  <span data-ttu-id="c22d0-113">자세한 내용은 [여기](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c22d0-113">More information [here](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).</span></span>

### <a name="how-to-install-mysql56-on-ubuntu"></a><span data-ttu-id="c22d0-114">Ubuntu에 MySQL5.6을 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="c22d0-114">How to install MySQL5.6 on Ubuntu</span></span>
<span data-ttu-id="c22d0-115">여기서는 Azure에 Ubuntu가 있는 Linux VM을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c22d0-115">We will use Linux VM with Ubuntu from Azure here.</span></span>

* <span data-ttu-id="c22d0-116">1단계: MySQL Server 5.6 설치 `root` 사용자로 전환:</span><span class="sxs-lookup"><span data-stu-id="c22d0-116">Step 1: Install MySQL Server 5.6   Switch to `root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="c22d0-117">mysql-server 5.6 설치:</span><span class="sxs-lookup"><span data-stu-id="c22d0-117">Install mysql-server 5.6:</span></span>
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    <span data-ttu-id="c22d0-118">설치하는 동안 아래에서 MySQL 루트 암호를 설정하라는 내용의 팝업 대화 창이 표시되면 여기에서 암호를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c22d0-118">During installation, you will see a dialog window poping up to ask you to set MySQL root password below, and you need set the password here.</span></span>
  
    ![이미지](./media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    <span data-ttu-id="c22d0-120">암호를 다시 입력하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c22d0-120">Input the password again to confirm.</span></span>

    ![이미지](./media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* <span data-ttu-id="c22d0-122">2단계: MySQL Server 로그인</span><span class="sxs-lookup"><span data-stu-id="c22d0-122">Step 2: Login MySQL Server</span></span>
  
    <span data-ttu-id="c22d0-123">MySQL Server 설치가 완료되면 MySQL 서비스가 자동으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="c22d0-123">When MySQL server installation finished, MySQL service will be started automatically.</span></span> <span data-ttu-id="c22d0-124">`root` 사용자로 MySQL Server에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c22d0-124">You can login MySQL Server with `root` user.</span></span>
    <span data-ttu-id="c22d0-125">아래와 같은 명령을 사용하여 로그인하고 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c22d0-125">Use the below command to login and input password.</span></span>
  
             #[root@mysqlnode ~]# mysql -uroot -p
* <span data-ttu-id="c22d0-126">3단계: 실행 중인 MySQL 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="c22d0-126">Step 3: Manage the running MySQL service</span></span>
  
    <span data-ttu-id="c22d0-127">(a) MySQL 서비스의 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c22d0-127">(a) Get status of MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql status
  
    <span data-ttu-id="c22d0-128">(b) MySQL 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c22d0-128">(b) Start MySQL Service</span></span>
  
             #[root@mysqlnode ~]# service mysql start
  
    <span data-ttu-id="c22d0-129">(c) MySQL 서비스를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="c22d0-129">(c) Stop MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql stop
  
    <span data-ttu-id="c22d0-130">(d) MySQL 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c22d0-130">(d) Restart the MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-to-install-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a><span data-ttu-id="c22d0-131">CentOS, Oracle Linux와 같은 Red Hat OS 제품군에서 MySQL을 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="c22d0-131">How to install MySQL on Red Hat OS family like CentOS, Oracle Linux</span></span>
<span data-ttu-id="c22d0-132">여기에서는 CentOS 또는 Oracle Linux와 함께 Linux VM을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c22d0-132">We will use Linux VM with CentOS or Oracle Linux here.</span></span>

* <span data-ttu-id="c22d0-133">1단계: MySQL Yum 리포지토리 추가 `root` 사용자로 전환:</span><span class="sxs-lookup"><span data-stu-id="c22d0-133">Step 1: Add the MySQL Yum repository   Switch to `root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="c22d0-134">MySQL 릴리스 패키지 다운로드 및 설치:</span><span class="sxs-lookup"><span data-stu-id="c22d0-134">Download and install the MySQL release package:</span></span>
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* <span data-ttu-id="c22d0-135">2단계: 아래 파일을 편집하여 MySQL5.6 패키지 다운로드에 MySQL을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c22d0-135">Step 2: Edit below file to enable the MySQL repository for downloading the MySQL5.6 package.</span></span>
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    <span data-ttu-id="c22d0-136">이 파일의 각 값을 아래와 같이 업데이트:</span><span class="sxs-lookup"><span data-stu-id="c22d0-136">Update each value of this file to below:</span></span>
  
        \# *Enable to use MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* <span data-ttu-id="c22d0-137">3단계: MySQL 리포지토리에서 MySQL 설치 MySQL 설치:</span><span class="sxs-lookup"><span data-stu-id="c22d0-137">Step 3: Install MySQL from MySQL repository   Install MySQL:</span></span>
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    <span data-ttu-id="c22d0-138">MySQL RPM 패키지 및 모든 관련 패키지가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="c22d0-138">MySQL RPM package and all related packages will be installed.</span></span>
* <span data-ttu-id="c22d0-139">4단계: 실행 중인 MySQL 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="c22d0-139">Step 4: Manage the running MySQL service</span></span>
  
    <span data-ttu-id="c22d0-140">(a) MySQL 서버의 서비스 상태 확인:</span><span class="sxs-lookup"><span data-stu-id="c22d0-140">(a) Check the service status of the MySQL server:</span></span>
  
           #[root@mysqlnode ~]#service mysqld status
  
    <span data-ttu-id="c22d0-141">(b) MySQL 서버의 기본 포트가 실행 중인지 확인:</span><span class="sxs-lookup"><span data-stu-id="c22d0-141">(b) Check whether the default port of  MySQL server is running:</span></span>
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    <span data-ttu-id="c22d0-142">(c) MySQL 서버 시작:</span><span class="sxs-lookup"><span data-stu-id="c22d0-142">(c) Start the MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld start

    <span data-ttu-id="c22d0-143">(d) MySQL 서버 중지:</span><span class="sxs-lookup"><span data-stu-id="c22d0-143">(d) Stop the MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld stop

    <span data-ttu-id="c22d0-144">(e) 시스템을 부팅할 때 MySQL을 시작하도록 설정:</span><span class="sxs-lookup"><span data-stu-id="c22d0-144">(e) Set MySQL to start when the system boot-up:</span></span>

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-to-install-mysql-on-suse-linux"></a><span data-ttu-id="c22d0-145">SUSE Linux에 MySQL을 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="c22d0-145">How to install MySQL on SUSE Linux</span></span>
<span data-ttu-id="c22d0-146">여기에서는 OpenSUSE와 Linux VM을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c22d0-146">We will use Linux VM with OpenSUSE here.</span></span>

* <span data-ttu-id="c22d0-147">1단계: MySQL 서버 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="c22d0-147">Step 1: Download and install MySQL Server</span></span>
  
    <span data-ttu-id="c22d0-148">아래 명령을 통해 `root` 사용자로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="c22d0-148">Switch to `root` user through below command:</span></span>  
  
           #sudo su -
  
    <span data-ttu-id="c22d0-149">MySQL 패키지 다운로드 및 설치:</span><span class="sxs-lookup"><span data-stu-id="c22d0-149">Download and install MySQL package:</span></span>
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* <span data-ttu-id="c22d0-150">2단계: 실행 중인 MySQL 서비스 관리:</span><span class="sxs-lookup"><span data-stu-id="c22d0-150">Step 2: Manage the running MySQL service</span></span>
  
    <span data-ttu-id="c22d0-151">(a) MySQL Server 상태 확인:</span><span class="sxs-lookup"><span data-stu-id="c22d0-151">(a) Check the status of the MySQL server:</span></span>
  
           #[root@mysqlnode ~]# rcmysql status
  
    <span data-ttu-id="c22d0-152">(b) MySQL Server의 기본 포트 상태 확인:</span><span class="sxs-lookup"><span data-stu-id="c22d0-152">(b) Check whether the default port of the MySQL server:</span></span>
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    <span data-ttu-id="c22d0-153">(c) MySQL 서버 시작:</span><span class="sxs-lookup"><span data-stu-id="c22d0-153">(c) Start the MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql start

    <span data-ttu-id="c22d0-154">(d) MySQL 서버 중지:</span><span class="sxs-lookup"><span data-stu-id="c22d0-154">(d) Stop the MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql stop

    <span data-ttu-id="c22d0-155">(e) 시스템을 부팅할 때 MySQL을 시작하도록 설정:</span><span class="sxs-lookup"><span data-stu-id="c22d0-155">(e) Set MySQL to start when the system boot-up:</span></span>

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a><span data-ttu-id="c22d0-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c22d0-156">Next Step</span></span>
<span data-ttu-id="c22d0-157">[여기](https://www.mysql.com/)에서 MySQL에 대한 사용법 및 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c22d0-157">Find more usage and information regarding MySQL [Here](https://www.mysql.com/).</span></span>

