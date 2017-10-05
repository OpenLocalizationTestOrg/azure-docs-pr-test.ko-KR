---
title: "Linux VM에서 PostgreSQL 설정 | Microsoft Docs"
description: "Azure Linux 가상 컴퓨터에 PostgreSQL을 설치하고 구성하는 방법을 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 1a747363-0cc5-4ba3-9be7-084dfeb04651
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: 0bccdc1cfdbda06b57da8cd662373ef137768672
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-configure-postgresql-on-azure"></a><span data-ttu-id="7fb9d-103">Azure에서 PostgreSQL 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="7fb9d-103">Install and configure PostgreSQL on Azure</span></span>
<span data-ttu-id="7fb9d-104">PostgreSQL은 Oracle 및 DB2와 유사한 고급 오픈 소스 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-104">PostgreSQL is an advanced open-source database similar to Oracle and DB2.</span></span> <span data-ttu-id="7fb9d-105">전체 ACID 규정 준수, 신뢰할 수 있는 트랜잭션 처리 및 다중 버전 동시성 제어와 같은 엔터프라이즈 기능이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-105">It includes enterprise-ready features such as full ACID compliance, reliable transactional processing, and multi-version concurrency control.</span></span> <span data-ttu-id="7fb9d-106">또한 ANSI SQL 및 SQL/MED(Oracle, MySQL, MongoDB 등에 대한 외부 데이터 래퍼 포함)와 같은 표준을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-106">It also supports standards such as ANSI SQL and SQL/MED (including foreign data wrappers for Oracle, MySQL, MongoDB, and many others).</span></span> <span data-ttu-id="7fb9d-107">12개 이상의 프로시저 언어, GIN 및 GiST 인덱스, 공간 데이터 지원 및 JSON에 대한 여러 NoSQL 같은 기능 또는 키 값 기반 응용 프로그램에 대한 지원을 통해 확장성을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-107">It is highly extensible with support for over 12 procedural languages, GIN and GiST indexes, spatial data support, and multiple NoSQL-like features for JSON or key-value-based applications.</span></span>

<span data-ttu-id="7fb9d-108">이 문서에서는 Linux를 실행하는 Azure 가상 컴퓨터에서 PostgreSQL을 설치 및 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-108">In this article, you will learn how to install and configure PostgreSQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a><span data-ttu-id="7fb9d-109">PostgreSQL 설치</span><span class="sxs-lookup"><span data-stu-id="7fb9d-109">Install PostgreSQL</span></span>
> [!NOTE]
> <span data-ttu-id="7fb9d-110">이 자습서를 완료하려면 Linux를 실행하는 Azure 가상 컴퓨터가 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-110">You must already have an Azure virtual machine running Linux in order to complete this tutorial.</span></span> <span data-ttu-id="7fb9d-111">계속하기 전에 Linux VM을 생성하고 설정하려면 [Azure Linux VM 자습서](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-111">To create and set up a Linux VM before proceeding, see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

<span data-ttu-id="7fb9d-112">이 경우 PostgreSQL 포트로 포트 1999를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-112">In this case, use port 1999 as the PostgreSQL port.</span></span>  

<span data-ttu-id="7fb9d-113">PuTTY를 통해 생성한 Linux VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-113">Connect to the Linux VM you created via PuTTY.</span></span> <span data-ttu-id="7fb9d-114">Azure Linux VM을 처음 사용하는 경우 [Azure에서 Linux와 함께 SSH를 사용하는 방법](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하여 Linux VM에 연결하기 위해 PuTTY를 사용하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-114">If this is the first time you're using an Azure Linux VM, see [How to Use SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to learn how to use PuTTY to connect to a Linux VM.</span></span>

1. <span data-ttu-id="7fb9d-115">다음 명령을 실행하여 루트(관리자)로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-115">Run the following command to switch to the root (admin):</span></span>
   
        # sudo su -
2. <span data-ttu-id="7fb9d-116">일부 배포의 경우 PostgreSQL을 설치하기 전에 설치해야 하는 종속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-116">Some distributions have dependencies that you must install before installing PostgreSQL.</span></span> <span data-ttu-id="7fb9d-117">이 목록에서 배포를 확인하고 적절한 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-117">Check for your distro in this list and run the appropriate command:</span></span>
   
   * <span data-ttu-id="7fb9d-118">Red Hat 기반 Linux:</span><span class="sxs-lookup"><span data-stu-id="7fb9d-118">Red Hat base Linux:</span></span>
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="7fb9d-119">Debian 기반 Linux:</span><span class="sxs-lookup"><span data-stu-id="7fb9d-119">Debian base Linux:</span></span>
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="7fb9d-120">SUSE Linux:</span><span class="sxs-lookup"><span data-stu-id="7fb9d-120">SUSE Linux:</span></span>
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. <span data-ttu-id="7fb9d-121">루트 디렉터리에 PostgreSQL를 다운로드한 다음 패키지의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-121">Download PostgreSQL into the root directory, and then unzip the package:</span></span>
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    <span data-ttu-id="7fb9d-122">위 내용은 한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-122">The above is an example.</span></span> <span data-ttu-id="7fb9d-123">[/pub/source/의 인덱스](https://ftp.postgresql.org/pub/source/)에서 더 자세한 다운로드 주소를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-123">You can find the more detailed download address in the [Index of /pub/source/](https://ftp.postgresql.org/pub/source/).</span></span>
4. <span data-ttu-id="7fb9d-124">빌드를 시작하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-124">To start the build, run these commands:</span></span>
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. <span data-ttu-id="7fb9d-125">설명서(HTML 및 man 페이지) 및 추가 모듈(contrib)을 비롯하여 빌드할 수 있는 모든 항목을 빌드하려는 경우에는 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-125">If  you want to build everything that can be built, including the documentation (HTML and man pages) and additional modules (contrib), run the following command instead:</span></span>
   
        # gmake install-world
   
    <span data-ttu-id="7fb9d-126">다음과 같은 확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-126">You should receive the following confirmation message:</span></span>
   
        PostgreSQL, contrib, and documentation successfully made. Ready to install.

## <a name="configure-postgresql"></a><span data-ttu-id="7fb9d-127">PostgreSQL 구성</span><span class="sxs-lookup"><span data-stu-id="7fb9d-127">Configure PostgreSQL</span></span>
1. <span data-ttu-id="7fb9d-128">(선택 사항) 바로 가기 링크를 만들어 버전 번호를 포함하지 않도록 PostgreSQL 참조를 짧게 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-128">(Optional) Create a symbolic link to shorten the PostgreSQL reference to not include the version number:</span></span>
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. <span data-ttu-id="7fb9d-129">데이터베이스에 대한 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-129">Create a directory for the database:</span></span>
   
        # mkdir -p /opt/pgsql_data
3. <span data-ttu-id="7fb9d-130">루트가 아닌 사용자를 만들고 해당 사용자의 프로필을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-130">Create a non-root user and modify that user’s profile.</span></span> <span data-ttu-id="7fb9d-131">그런 다음 이 새 사용자(이 예제에서는 *postgres* 임)로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-131">Then, switch to this new user (called *postgres* in our example):</span></span>
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > <span data-ttu-id="7fb9d-132">보안상의 이유로, PostgreSQL은 루트가 아닌 사용자를 사용하여 데이터베이스를 초기화, 시작 또는 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-132">For security reasons, PostgreSQL uses a non-root user to initialize, start, or shut down the database.</span></span>
   > 
   > 
4. <span data-ttu-id="7fb9d-133">아래 명령을 입력하여 *bash_profile* 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-133">Edit the *bash_profile* file by entering the commands below.</span></span> <span data-ttu-id="7fb9d-134">*bash_profile* 파일 끝에 다음 줄이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-134">These lines will be added to the end of the *bash_profile* file:</span></span>
   
        cat >> ~/.bash_profile <<EOF
        export PGPORT=1999
        export PGDATA=/opt/pgsql_data
        export LANG=en_US.utf8
        export PGHOME=/opt/pgsql
        export PATH=\$PATH:\$PGHOME/bin
        export MANPATH=\$MANPATH:\$PGHOME/share/man
        export DATA=`date +"%Y%m%d%H%M"`
        export PGUSER=postgres
        alias rm='rm -i'
        alias ll='ls -lh'
        EOF
5. <span data-ttu-id="7fb9d-135">*bash_profile* 파일을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-135">Execute the *bash_profile* file:</span></span>
   
        $ source .bash_profile
6. <span data-ttu-id="7fb9d-136">다음 명령을 사용하여 설치의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-136">Validate your installation by using the following command:</span></span>
   
        $ which psql
   
    <span data-ttu-id="7fb9d-137">설치에 성공하면 다음과 같은 응답이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-137">If your installation is successful, you will see the following response:</span></span>
   
        /opt/pgsql/bin/psql
7. <span data-ttu-id="7fb9d-138">또한 PostgreSQL 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-138">You can also check the PostgreSQL version:</span></span>
   
        $ psql -V
8. <span data-ttu-id="7fb9d-139">데이터베이스를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-139">Initialize the database:</span></span>
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    <span data-ttu-id="7fb9d-140">다음과 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-140">You should receive the following output:</span></span>

![이미지](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a><span data-ttu-id="7fb9d-142">PostgreSQL 설정</span><span class="sxs-lookup"><span data-stu-id="7fb9d-142">Set up PostgreSQL</span></span>
<!--    [postgres@ test ~]$ exit -->

<span data-ttu-id="7fb9d-143">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-143">Run the following commands:</span></span>

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

<span data-ttu-id="7fb9d-144">/Etc/init.d/postgresql 파일에서 두 변수를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-144">Modify two variables in the /etc/init.d/postgresql file.</span></span> <span data-ttu-id="7fb9d-145">접두사가 PostgreSQL의 설치 경로인 **/opt/pgsql**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-145">The prefix is set to the installation path of PostgreSQL: **/opt/pgsql**.</span></span> <span data-ttu-id="7fb9d-146">PGDATA가 PostgreSQL의 데이터 저장소 경로인 **/opt/pgsql_data**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-146">PGDATA is set to the data storage path of PostgreSQL: **/opt/pgsql_data**.</span></span>

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![이미지](./media/postgresql-install/no2.png)

<span data-ttu-id="7fb9d-148">파일을 변경하여 실행 가능하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-148">Change the file to make it executable:</span></span>

    # chmod +x /etc/init.d/postgresql

<span data-ttu-id="7fb9d-149">PostgreSQL을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-149">Start PostgreSQL:</span></span>

    # /etc/init.d/postgresql start

<span data-ttu-id="7fb9d-150">PostgreSQL의 끝점이 켜져 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-150">Check if the endpoint of PostgreSQL is on:</span></span>

    # netstat -tunlp|grep 1999

<span data-ttu-id="7fb9d-151">다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-151">You should see the following output:</span></span>

![이미지](./media/postgresql-install/no3.png)

## <a name="connect-to-the-postgres-database"></a><span data-ttu-id="7fb9d-153">Postgres 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="7fb9d-153">Connect to the Postgres database</span></span>
<span data-ttu-id="7fb9d-154">다시 한 번 postgres 사용자로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-154">Switch to the postgres user once again:</span></span>

    # su - postgres

<span data-ttu-id="7fb9d-155">Postgres 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-155">Create a Postgres database:</span></span>

    $ createdb events

<span data-ttu-id="7fb9d-156">방금 만든 이벤트 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-156">Connect to the events database that you just created:</span></span>

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a><span data-ttu-id="7fb9d-157">Postgres 테이블 만들기 및 삭제</span><span class="sxs-lookup"><span data-stu-id="7fb9d-157">Create and delete a Postgres table</span></span>
<span data-ttu-id="7fb9d-158">데이터베이스에 연결했으므로 해당 데이터베이스에 테이블을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-158">Now that you have connected to the database, you can create tables in it.</span></span>

<span data-ttu-id="7fb9d-159">예를 들어 다음 명령을 사용하여 새로운 예제 Postgres 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-159">For example, create a new example Postgres table by using the following command:</span></span>

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

<span data-ttu-id="7fb9d-160">이제 다음 열 이름 및 제한 사항을 사용하는 4열 테이블을 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-160">You have now set up a four-column table with the following column names and restrictions:</span></span>

1. <span data-ttu-id="7fb9d-161">"name" 열은 20자 이하가 되도록 VARCHAR 명령에 의해 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-161">The “name” column has been limited by the VARCHAR command to be under 20 characters long.</span></span>
2. <span data-ttu-id="7fb9d-162">"food" 열은 각자 가져오는 음식 항목을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-162">The “food” column indicates the food item that each person will bring.</span></span> <span data-ttu-id="7fb9d-163">VARCHAR이 이 텍스트를 30자 이하로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-163">VARCHAR limits this text to be under 30 characters.</span></span>
3. <span data-ttu-id="7fb9d-164">"confirmed" 열은 초대받은 사람이 집들이에 RSVP를 설정했는지 여부를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-164">The “confirmed” column records whether the person has RSVP’d to the potluck.</span></span> <span data-ttu-id="7fb9d-165">허용되는 값은 "Y"와 "N"입니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-165">The acceptable values are "Y" and "N".</span></span>
4. <span data-ttu-id="7fb9d-166">"date" 열에는 이벤트에 대해 등록한 날짜가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-166">The “date” column shows when they signed up for the event.</span></span> <span data-ttu-id="7fb9d-167">Postgres에서는 날짜가 yyyy-mm-dd로 작성되도록 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-167">Postgres requires that dates be written as yyyy-mm-dd.</span></span>

<span data-ttu-id="7fb9d-168">테이블이 생성된 경우 다음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-168">You should see the following if your table has been successfully created:</span></span>

![이미지](./media/postgresql-install/no4.png)

<span data-ttu-id="7fb9d-170">다음 명령을 사용하여 테이블 구조를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-170">You can also check the table structure by using the following command:</span></span>

![이미지](./media/postgresql-install/no5.png)

### <a name="add-data-to-a-table"></a><span data-ttu-id="7fb9d-172">테이블에 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="7fb9d-172">Add data to a table</span></span>
<span data-ttu-id="7fb9d-173">먼저, 행에 정보를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-173">First, insert information into a row:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

<span data-ttu-id="7fb9d-174">다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-174">You should see this output:</span></span>

![이미지](./media/postgresql-install/no6.png)

<span data-ttu-id="7fb9d-176">테이블에 몇 명의 더 많은 사람을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-176">You can add a couple more people to the table as well.</span></span> <span data-ttu-id="7fb9d-177">다음은 몇 가지 옵션입니다. 또는 직접 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-177">Here are some options, or you can create your own:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a><span data-ttu-id="7fb9d-178">테이블 표시</span><span class="sxs-lookup"><span data-stu-id="7fb9d-178">Show tables</span></span>
<span data-ttu-id="7fb9d-179">테이블을 표시하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-179">Use the following command to show a table:</span></span>

    select * from potluck;

<span data-ttu-id="7fb9d-180">출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-180">The output is:</span></span>

![이미지](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a><span data-ttu-id="7fb9d-182">테이블의 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="7fb9d-182">Delete data in a table</span></span>
<span data-ttu-id="7fb9d-183">테이블의 데이터를 삭제하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-183">Use the following command to delete data in a table:</span></span>

    delete from potluck where name=’John’;

<span data-ttu-id="7fb9d-184">"John" 행에 있는 모든 정보를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-184">This deletes all the information in the "John" row.</span></span> <span data-ttu-id="7fb9d-185">출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-185">The output is:</span></span>

![이미지](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a><span data-ttu-id="7fb9d-187">테이블의 데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="7fb9d-187">Update data in a table</span></span>
<span data-ttu-id="7fb9d-188">테이블의 데이터를 업데이트하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-188">Use the following command to update data in a table.</span></span> <span data-ttu-id="7fb9d-189">이 경우에는 Sandy가 참석하겠다고 확인했으므로 회신을 "N"에서 "Y"로 RSVP를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-189">For this one, Sandy has confirmed that she is attending, so we will change her RSVP from "N" to "Y":</span></span>

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a><span data-ttu-id="7fb9d-190">PostgreSQL에 대한 자세한 정보 얻기</span><span class="sxs-lookup"><span data-stu-id="7fb9d-190">Get more information about PostgreSQL</span></span>
<span data-ttu-id="7fb9d-191">Azure Linux VM에서 PostgreSQL의 설치를 완료하면 Azure에서 사용하여 즐길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-191">Now that you have completed the installation of PostgreSQL in an Azure Linux VM, you can enjoy using it in Azure.</span></span> <span data-ttu-id="7fb9d-192">PostgreSQL에 대해 자세히 알아보려면 [PostgreSQL 웹 사이트](http://www.postgresql.org/)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="7fb9d-192">To learn more about PostgreSQL, visit the [PostgreSQL website](http://www.postgresql.org/).</span></span>

