---
title: "aaaConnect tooSQL C 및 c + +를 사용 하 여 데이터베이스 | Microsoft Docs"
description: "사용 하 여 hello 샘플의 코드에서이 빠른 시작 toobuild c + +와 최신 응용 프로그램 및 hello 클라우드에서 Azure SQL 데이터베이스와 함께 강력한 관계형 데이터베이스에서 지원 합니다."
services: sql-database
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: 
ms.assetid: 07d9e0b1-3234-4f17-a252-a7559160a9db
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 03/06/2017
ms.author: edmacauley
ms.openlocfilehash: 9b581424c91bfdd93deb6914212629519a011d8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-database-using-c-and-c"></a><span data-ttu-id="a720a-103">TooSQL 연결 C 및 c + +를 사용 하 여 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="a720a-103">Connect tooSQL Database using C and C++</span></span>
<span data-ttu-id="a720a-104">이 게시물은 tooconnect tooAzure SQL DB를 시도 하는 C 및 c + + 개발자를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-104">This post is aimed at C and C++ developers trying tooconnect tooAzure SQL DB.</span></span> <span data-ttu-id="a720a-105">나뉘어집니다 구간으로 분할 toohello 섹션 가장 관심을 캡처하는 이동할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-105">It is broken down into sections so you can jump toohello section that best captures your interest.</span></span> 

## <a name="prerequisites-for-hello-cc-tutorial"></a><span data-ttu-id="a720a-106">C/c + + 자습서 hello에 대 한 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="a720a-106">Prerequisites for hello C/C++ tutorial</span></span>
<span data-ttu-id="a720a-107">다음 항목 hello 지정 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-107">Make sure you have hello following items:</span></span>

* <span data-ttu-id="a720a-108">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="a720a-108">An active Azure account.</span></span> <span data-ttu-id="a720a-109">아직 구독하지 않은 경우 [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-109">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a720a-110">[Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a720a-110">[Visual Studio](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="a720a-111">C + + 언어 구성 요소 toobuild hello를 설치 하 고이 샘플을 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-111">You must install hello C++ language components toobuild and run this sample.</span></span>
* <span data-ttu-id="a720a-112">[Visual Studio Linux 개발](https://visualstudiogallery.msdn.microsoft.com/725025cf-7067-45c2-8d01-1e0fd359ae6e).</span><span class="sxs-lookup"><span data-stu-id="a720a-112">[Visual Studio Linux Development](https://visualstudiogallery.msdn.microsoft.com/725025cf-7067-45c2-8d01-1e0fd359ae6e).</span></span> <span data-ttu-id="a720a-113">Linux에서 개발 하는 경우에 hello Visual Studio Linux 확장도 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-113">If you are developing on Linux, you must also install hello Visual Studio Linux extension.</span></span> 

## <span data-ttu-id="a720a-114"><a id="AzureSQL"></a>가상 컴퓨터에서 Azure SQL Database 및 SQL Server</span><span class="sxs-lookup"><span data-stu-id="a720a-114"><a id="AzureSQL"></a>Azure SQL Database and SQL Server on virtual machines</span></span>
<span data-ttu-id="a720a-115">Azure SQL Microsoft SQL Server에서 작성 되 고 높은 가용성, 성능, 좋 및 확장 가능한 서비스 디자인 된 tooprovide 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-115">Azure SQL is built on Microsoft SQL Server and is designed tooprovide a high-availability, performant, and scalable service.</span></span> <span data-ttu-id="a720a-116">독점적인 온-프레미스에서 실행 중인 데이터베이스를 통해 많은 이점을 toousing SQL Azure 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-116">There are many benefits toousing SQL Azure over your proprietary database running on premises.</span></span> <span data-ttu-id="a720a-117">SQL Azure와 함께 하지 않는 tooinstall, 설정, 유지 관리 했거나 데이터베이스 있지만 hello 콘텐츠 및 데이터베이스의 hello 구조를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-117">With SQL Azure you don’t have tooinstall, set up, maintain, or manage your database but only hello content and hello structure of your database.</span></span> <span data-ttu-id="a720a-118">내결함성과 중복성처럼 데이터 베이스에 대해 일반적으로 걱정하는 것이 모두 기본 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-118">Typical things that we worry about with databases like fault tolerance and redundancy are all built in.</span></span> 

<span data-ttu-id="a720a-119">Azure에는 현재 Azure SQL server 작업 부하를 호스팅하기 위한 두 가지 옵션, 즉 서비스로서 데이터베이스인 Azure SQL Database와 가상 컴퓨터(VM)의 SQL server가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-119">Azure currently has two options for hosting SQL server workloads: Azure SQL database, database as a service and SQL server on Virtual Machines (VM).</span></span> <span data-ttu-id="a720a-120">우리는 가져올 수 없습니다 이러한 두 hello 차이점에 대 한 정보를 확인할 Azure SQL 데이터베이스는 새로운 클라우드 기반 응용 프로그램 tootake 이점이 hello 비용 절감 효과 위한 최선의 방법은 클라우드 서비스 성능 최적화를 제공 된다는 점이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-120">We will not get into detail about hello differences between these two except that Azure SQL database is your best bet for new cloud-based applications tootake advantage of hello cost savings and performance optimization that cloud services provide.</span></span> <span data-ttu-id="a720a-121">마이그레이션 또는 온-프레미스 응용 프로그램 toohello 클라우드 확장 하려는 경우 Azure 가상 컴퓨터에 SQL server 더 적합 작동 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-121">If you are considering migrating or extending your on-premises applications toohello cloud, SQL server on Azure virtual machine might work out better for you.</span></span> <span data-ttu-id="a720a-122">tookeep 가지 간단한이이 문서에서는 Azure SQL 데이터베이스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-122">tookeep things simple for this article, let's create an Azure SQL database.</span></span> 

## <span data-ttu-id="a720a-123"><a id="ODBC"></a>데이터 액세스 기술: ODBC 및 OLE DB</span><span class="sxs-lookup"><span data-stu-id="a720a-123"><a id="ODBC"></a>Data access technologies: ODBC and OLE DB</span></span>
<span data-ttu-id="a720a-124">SQL DB 연결 tooAzure 마찬가지 이며 현재 두 가지 tooconnect toodatabases: ODBC (Open Database connectivity) 및 OLE DB (개체 연결과 데이터베이스).</span><span class="sxs-lookup"><span data-stu-id="a720a-124">Connecting tooAzure SQL DB is no different and currently there are two ways tooconnect toodatabases: ODBC (Open Database connectivity) and OLE DB (Object Linking and Embedding database).</span></span> <span data-ttu-id="a720a-125">최근 몇 년간 Microsoft는 [기본 관계형 데이터 액세스에 대해 ODBC](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)에 맞추어 왔습니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-125">In recent years, Microsoft has aligned with [ODBC for native relational data access](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/).</span></span> <span data-ttu-id="a720a-126">ODBC은 비교적 간단하고 OLE DB보다 훨씬 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-126">ODBC is relatively simple, and also much faster than OLE DB.</span></span> <span data-ttu-id="a720a-127">유일한 주의할 여기 hello ODBC는 이전 C 스타일 API를 사용 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-127">hello only caveat here is that ODBC does use an old C-style API.</span></span> 

## <span data-ttu-id="a720a-128"><a id="Create"></a>1단계: Azure SQL Database 만들기</span><span class="sxs-lookup"><span data-stu-id="a720a-128"><a id="Create"></a>Step 1:  Creating your Azure SQL Database</span></span>
<span data-ttu-id="a720a-129">Hello 참조 [시작 하기 페이지](sql-database-get-started-portal.md) toolearn 어떻게 toocreate 예제 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="a720a-129">See hello [getting started page](sql-database-get-started-portal.md) toolearn how toocreate a sample database.</span></span>  <span data-ttu-id="a720a-130">또는 설치 하려면이 방법을 [짧은 2 분 비디오](https://azure.microsoft.com/documentation/videos/azure-sql-database-create-dbs-in-seconds/) 사용 하 여 Azure SQL 데이터베이스 toocreate hello Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-130">Alternatively, you can follow this [short two-minute video](https://azure.microsoft.com/documentation/videos/azure-sql-database-create-dbs-in-seconds/) toocreate an Azure SQL database using hello Azure portal.</span></span>

## <span data-ttu-id="a720a-131"><a id="ConnectionString"></a>2단계: 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="a720a-131"><a id="ConnectionString"></a>Step 2:  Get connection string</span></span>
<span data-ttu-id="a720a-132">Azure SQL 데이터베이스 프로 비전 한 후 다음 단계 toodetermine 연결 정보는 hello 아웃 toocarry 필요 하 고 방화벽 액세스에 대 한 클라이언트 IP 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-132">After your Azure SQL database has been provisioned, you need toocarry out hello following steps toodetermine connection information and add your client IP for firewall access.</span></span> 

<span data-ttu-id="a720a-133">[Azure 포털](https://portal.azure.com/), tooyour Azure SQL 데이터베이스 ODBC 연결 문자열 hello를 사용 하 여 이동 **데이터베이스 연결 문자열 표시** 데이터베이스에 대 한 hello 개요 섹션의 일부분으로 나열:</span><span class="sxs-lookup"><span data-stu-id="a720a-133">In [Azure portal](https://portal.azure.com/), go tooyour Azure SQL database ODBC connection string by using hello **Show database connection strings** listed as a part of hello overview section for your database:</span></span> 

![ODBCConnectionString](./media/sql-database-develop-cplusplus-simple/azureportal.png)

![ODBCConnectionStringProps](./media/sql-database-develop-cplusplus-simple/dbconnection.png)

<span data-ttu-id="a720a-136">Hello의 hello 내용을 복사 **ODBC (포함 Node.js) [SQL 인증]** 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-136">Copy hello contents of hello **ODBC (Includes Node.js) [SQL authentication]** string.</span></span> <span data-ttu-id="a720a-137">이 문자열을 사용 하 여 우리는 c + + ODBC 명령줄 인터프리터에서 이후 tooconnect 합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-137">We use this string later tooconnect from our C++ ODBC command-line interpreter.</span></span> <span data-ttu-id="a720a-138">이 문자열 hello 드라이버, 서버 및 다른 데이터베이스 연결 매개 변수 등의 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-138">This string provides details such as hello driver, server, and other database connection parameters.</span></span> 

## <span data-ttu-id="a720a-139"><a id="Firewall"></a>3 단계: 추가 IP toohello 방화벽</span><span class="sxs-lookup"><span data-stu-id="a720a-139"><a id="Firewall"></a>Step 3:  Add your IP toohello firewall</span></span>
<span data-ttu-id="a720a-140">Toohello 방화벽 섹션 데이터베이스 서버에 이동 하 고 추가 프로그램 [다음이 단계를 사용 하 여 클라이언트 IP toohello 방화벽](sql-database-configure-firewall-settings.md) toomake 있는지 성공적으로 연결을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-140">Go toohello firewall section for your Database server and add your [client IP toohello firewall using these steps](sql-database-configure-firewall-settings.md) toomake sure we can establish a successful connection:</span></span> 

![AddyourIPWindow](./media/sql-database-develop-cplusplus-simple/ip.png)

<span data-ttu-id="a720a-142">이 시점에서 Azure SQL DB 구성 및 준비 tooconnect c + + 코드는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-142">At this point, you have configured your Azure SQL DB and are ready tooconnect from your C++ code.</span></span> 

## <span data-ttu-id="a720a-143"><a id="Windows"></a>4단계: Windows C/C++ 응용 프로그램에서 연결</span><span class="sxs-lookup"><span data-stu-id="a720a-143"><a id="Windows"></a>Step 4: Connecting from a Windows C/C++ application</span></span>
<span data-ttu-id="a720a-144">Tooyour를 쉽게 연결할 수 있습니다 [이 샘플을 사용 하 여 Windows에서 ODBC를 사용 하 여 Azure SQL DB](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29) 을 Visual Studio와 함께 빌드하 합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-144">You can easily connect tooyour [Azure SQL DB using ODBC on Windows using this sample](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29) that builds with Visual Studio.</span></span> <span data-ttu-id="a720a-145">hello 샘플 사용된 tooconnect tooour Azure SQL DB 수 있는 ODBC 명령줄 인터프리터를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-145">hello sample implements an ODBC command-line interpreter that can be used tooconnect tooour Azure SQL DB.</span></span> <span data-ttu-id="a720a-146">이 샘플에서는 명령줄 인수로 데이터베이스 원본 이름 (DSN) 파일 파일 또는 hello Azure 포털에서에서 앞에서 복사한 우리는 hello verbose 연결 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-146">This sample takes either a Database source name file (DSN) file as a command-line argument or hello verbose connection string that we copied earlier from hello Azure portal.</span></span> <span data-ttu-id="a720a-147">이 프로젝트에 대 한 hello 속성 페이지를 열고이 하 다음과 같이 명령 인수로 hello 연결 문자열을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-147">Bring up hello property page for this project and paste hello connection string as a command argument as shown here:</span></span> 

![DSN Propsfile](./media/sql-database-develop-cplusplus-simple/props.png)

<span data-ttu-id="a720a-149">해당 데이터베이스 연결 문자열의 일부로 데이터베이스에 대 한 hello 올바른 인증 세부 정보를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-149">Make sure you provide hello right authentication details for your database as a part of that database connection string.</span></span> 

<span data-ttu-id="a720a-150">Hello 응용 프로그램 toobuild 시작 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-150">Launch hello application toobuild it.</span></span> <span data-ttu-id="a720a-151">창 성공적인 연결 유효성 검사를 수행 하는 hello를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-151">You should see hello following window validating a successful connection.</span></span> <span data-ttu-id="a720a-152">와 같은 몇 가지 기본 SQL 명령의 실행할 수 **테이블을 만들** toovalidate 데이터베이스 연결:</span><span class="sxs-lookup"><span data-stu-id="a720a-152">You can even run some basic SQL commands like **create table** toovalidate your database connectivity:</span></span>

![SQL 명령](./media/sql-database-develop-cplusplus-simple/sqlcommands.png)

<span data-ttu-id="a720a-154">또는 명령 인수에 제공 되는 경우 시작 된 hello 마법사를 사용 하는 DSN 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-154">Alternatively, you could create a DSN file using hello wizard that is launched when no command arguments are provided.</span></span> <span data-ttu-id="a720a-155">이 옵션을 함께 시도하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-155">We recommend that you try this option as well.</span></span> <span data-ttu-id="a720a-156">자동화 및 인증 설정 보호를 위해 DSN 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-156">You can use this DSN file for automation and protecting your authentication settings:</span></span> 

![파일 DSN 만들기](./media/sql-database-develop-cplusplus-simple/datasource.png)

<span data-ttu-id="a720a-158">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-158">Congratulations!</span></span> <span data-ttu-id="a720a-159">SQL tooAzure를 성공적으로 연결 되어 이제 c + + 및 ODBC를 사용 하 여 Windows에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-159">You have now successfully connected tooAzure SQL using C++ and ODBC on Windows.</span></span> <span data-ttu-id="a720a-160">계속 읽어보세요 수 toodo hello Linux 플랫폼에 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-160">You can continue reading toodo hello same for Linux platform as well.</span></span> 

## <span data-ttu-id="a720a-161"><a id="Linux"></a>5 단계: Linux C/C++ 응용 프로그램에서 연결</span><span class="sxs-lookup"><span data-stu-id="a720a-161"><a id="Linux"></a>Step 5: Connecting from a Linux C/C++ application</span></span>
<span data-ttu-id="a720a-162">경우에 대비 hello 뉴스 듣지 아직 Visual Studio를 사용 하면 있습니다 toodevelop c + + Linux 응용 프로그램의 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-162">In case you haven’t heard hello news yet, Visual Studio now allows you toodevelop C++ Linux application as well.</span></span> <span data-ttu-id="a720a-163">이 새 시나리오 hello에서 참고할 수 [Linux 개발용 Visual c + +](https://blogs.msdn.microsoft.com/vcblog/2016/03/30/visual-c-for-linux-development/) 블로그.</span><span class="sxs-lookup"><span data-stu-id="a720a-163">You can read about this new scenario in hello [Visual C++ for Linux Development](https://blogs.msdn.microsoft.com/vcblog/2016/03/30/visual-c-for-linux-development/) blog.</span></span> <span data-ttu-id="a720a-164">Linux 용 toobuild, Linux 배포판 실행 되 고 있는 원격 컴퓨터가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-164">toobuild for Linux, you need a remote machine where your Linux distro is running.</span></span> <span data-ttu-id="a720a-165">원격 컴퓨터가 없다면 [Linux Azure 가상 컴퓨터](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용하여 신속하게 하나를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-165">If you don’t have one available, you can set one up quickly using [Linux Azure Virtual machines](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="a720a-166">이 자습서에서는 Ubuntu 16.04 Linux 배포판이 설치되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-166">For this tutorial, let us assume that you have an Ubuntu 16.04 Linux distribution set up.</span></span> <span data-ttu-id="a720a-167">여기에 나오는 hello 단계 tooUbuntu 15.10, Red Hat 6 및 Red Hat 7에도 적용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-167">hello steps here should also apply tooUbuntu 15.10, Red Hat 6, and Red Hat 7.</span></span> 

<span data-ttu-id="a720a-168">hello 다음 설치 단계를 수행 하면 배포판에 대 한 SQL 및 ODBC에 대 한 필요한 hello 라이브러리:</span><span class="sxs-lookup"><span data-stu-id="a720a-168">hello following steps install hello libraries needed for SQL and ODBC for your distro:</span></span>

    sudo su
    sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/mssql-ubuntu-test/ xenial main" > /etc/apt/sources.list.d/mssqlpreview.list'
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    apt-get update
    apt-get install msodbcsql
    apt-get install unixodbc-dev-utf16 #this step is optional but recommended*

<span data-ttu-id="a720a-169">Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-169">Launch Visual Studio.</span></span> <span data-ttu-id="a720a-170">도구-> 옵션에는 플랫폼 간-> 연결 관리자-> 연결 tooyour Linux 상자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-170">Under Tools -> Options -> Cross Platform -> Connection Manager, add a connection tooyour Linux box:</span></span> 

![도구 옵션](./media/sql-database-develop-cplusplus-simple/tools.png)

<span data-ttu-id="a720a-172">SSH 통해 연결이 설정된 후에 빈 프로젝트(Linux) 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-172">After connection over SSH is established, create an Empty project (Linux) template:</span></span> 

![새 프로젝트 템플릿](./media/sql-database-develop-cplusplus-simple/template.png)

<span data-ttu-id="a720a-174">그런 다음 [새 C 소스 파일을 추가하고 다음 내용으로 교체](https://github.com/Microsoft/VCSamples/blob/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29/odbcconnector/odbcconnector.c)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-174">You can then add a [new C source file and replace it with this content](https://github.com/Microsoft/VCSamples/blob/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29/odbcconnector/odbcconnector.c).</span></span> <span data-ttu-id="a720a-175">ODBC Api SQLAllocHandle hello, SQLSetConnectAttr, 및 SQLDriverConnect를 사용 하 여 있습니다 수 tooinitialize와 tooyour 데이터베이스 연결을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-175">Using hello ODBC APIs SQLAllocHandle, SQLSetConnectAttr, and SQLDriverConnect, you should be able tooinitialize and establish a connection tooyour database.</span></span> <span data-ttu-id="a720a-176">마찬가지로 hello Windows ODBC 샘플 해야 hello Azure 포털에서에서 이전에 복사한 데이터베이스 연결 문자열 매개 변수에서 tooreplace hello SQLDriverConnect 호출 hello 세부 정보.</span><span class="sxs-lookup"><span data-stu-id="a720a-176">Like with hello Windows ODBC sample, you need tooreplace hello SQLDriverConnect call with hello details from your database connection string parameters copied from hello Azure portal previously.</span></span> 

     retcode = SQLDriverConnect(
        hdbc, NULL, "Driver=ODBC Driver 13 for SQL"
                    "Server;Server=<yourserver>;Uid=<yourusername>;Pwd=<"
                    "yourpassword>;database=<yourdatabase>",
        SQL_NTS, outstr, sizeof(outstr), &outstrlen, SQL_DRIVER_NOPROMPT);

<span data-ttu-id="a720a-177">컴파일 전에 tooadd 마지막 일 toodo hello **odbc** 라이브러리 종속성으로:</span><span class="sxs-lookup"><span data-stu-id="a720a-177">hello last thing toodo before compiling is tooadd **odbc** as a library dependency:</span></span> 

![입력된 라이브러리로 ODBC 추가](./media/sql-database-develop-cplusplus-simple/lib.png)

<span data-ttu-id="a720a-179">toolaunch 응용 프로그램에서 hello hello Linux 콘솔 (를) 실행 **디버그** 메뉴:</span><span class="sxs-lookup"><span data-stu-id="a720a-179">toolaunch your application, bring up hello Linux Console from hello **Debug** menu:</span></span> 

![Linux 콘솔](./media/sql-database-develop-cplusplus-simple/linuxconsole.png)

<span data-ttu-id="a720a-181">연결에 성공 하면 이제 표시 되어야 hello hello Linux 콘솔에에서 인쇄는 현재 데이터베이스 이름:</span><span class="sxs-lookup"><span data-stu-id="a720a-181">If your connection was successful, you should now see hello current database name printed in hello Linux Console:</span></span> 

![Linux 콘솔 창 출력](./media/sql-database-develop-cplusplus-simple/linuxconsolewindow.png)

<span data-ttu-id="a720a-183">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-183">Congratulations!</span></span> <span data-ttu-id="a720a-184">Hello 자습서를 성공적으로 마쳤습니다 및 Azure SQL DB tooyour c + +에서 Windows 및 Linux 플랫폼에 연결할 이제 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-184">You have successfully completed hello tutorial and can now connect tooyour Azure SQL DB from C++ on Windows and Linux platforms.</span></span>

## <span data-ttu-id="a720a-185"><a id="GetSolution"></a>Hello 완료 C/c + + 자습서 솔루션 가져오기</span><span class="sxs-lookup"><span data-stu-id="a720a-185"><a id="GetSolution"></a>Get hello complete C/C++ tutorial solution</span></span>
<span data-ttu-id="a720a-186">Github에서이 문서에서 모든 hello 샘플을 포함 하는 hello GetStarted 솔루션을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a720a-186">You can find hello GetStarted solution that contains all hello samples in this article at github:</span></span>

* <span data-ttu-id="a720a-187">[Windows c + + ODBC 샘플](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29), hello Windows c + + ODBC 샘플 tooconnect tooAzure SQL 다운로드</span><span class="sxs-lookup"><span data-stu-id="a720a-187">[ODBC C++ Windows sample](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29), Download hello Windows C++ ODBC Sample tooconnect tooAzure SQL</span></span>
* <span data-ttu-id="a720a-188">[C + + Linux ODBC 샘플](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29), hello Linux c + + ODBC 샘플 tooconnect tooAzure SQL 다운로드</span><span class="sxs-lookup"><span data-stu-id="a720a-188">[ODBC C++ Linux sample](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29), Download hello Linux C++ ODBC Sample tooconnect tooAzure SQL</span></span>

## <a name="next-steps"></a><span data-ttu-id="a720a-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a720a-189">Next steps</span></span>
* <span data-ttu-id="a720a-190">검토 hello [SQL 데이터베이스 개발 개요](sql-database-develop-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a720a-190">Review hello [SQL Database Development Overview](sql-database-develop-overview.md)</span></span>
* <span data-ttu-id="a720a-191">Hello에 대 한 자세한 내용은 [ODBC API 참조](https://docs.microsoft.com/sql/odbc/reference/syntax/odbc-api-reference/)</span><span class="sxs-lookup"><span data-stu-id="a720a-191">More information on hello [ODBC API Reference](https://docs.microsoft.com/sql/odbc/reference/syntax/odbc-api-reference/)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a720a-192">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a720a-192">Additional resources</span></span>
* [<span data-ttu-id="a720a-193">Azure SQL 데이터베이스를 사용한 다중 테넌트 SaaS 응용 프로그램 디자인 패턴</span><span class="sxs-lookup"><span data-stu-id="a720a-193">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* <span data-ttu-id="a720a-194">모든 hello 탐색 [SQL 데이터베이스의 기능](https://azure.microsoft.com/services/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="a720a-194">Explore all hello [capabilities of SQL Database](https://azure.microsoft.com/services/sql-database/)</span></span>

