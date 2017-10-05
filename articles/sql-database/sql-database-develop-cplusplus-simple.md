---
title: "C 및 C++를 사용하여 SQL Database에 연결 | Microsoft Docs"
description: "이 빠른 시작에 포함된 샘플 코드를 사용하여 C++으로 최신 응용 프로그램을 개발하고 Azure SQL Database로 클라우드에서 강력한 관계형 데이터베이스를 통해 지원할 수 있습니다."
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
ms.openlocfilehash: ee7398304b7ba864eff17eb6e7d7c3777f4a9fe6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-sql-database-using-c-and-c"></a><span data-ttu-id="a00a5-103">C 및 C++를 사용하여 SQL Database에 연결</span><span class="sxs-lookup"><span data-stu-id="a00a5-103">Connect to SQL Database using C and C++</span></span>
<span data-ttu-id="a00a5-104">이 게시물의 목적은 Azure SQL DB에 연결하려고 시도하는 C 및 C++ 개발자를 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-104">This post is aimed at C and C++ developers trying to connect to Azure SQL DB.</span></span> <span data-ttu-id="a00a5-105">가장 관심 있는 부분을 캡처하는 섹션으로 이동할 수 있도록 섹션이 세분화됩니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-105">It is broken down into sections so you can jump to the section that best captures your interest.</span></span> 

## <a name="prerequisites-for-the-cc-tutorial"></a><span data-ttu-id="a00a5-106">C/C++ 자습서의 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="a00a5-106">Prerequisites for the C/C++ tutorial</span></span>
<span data-ttu-id="a00a5-107">다음 항목이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-107">Make sure you have the following items:</span></span>

* <span data-ttu-id="a00a5-108">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="a00a5-108">An active Azure account.</span></span> <span data-ttu-id="a00a5-109">아직 구독하지 않은 경우 [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-109">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a00a5-110">[Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a00a5-110">[Visual Studio](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="a00a5-111">이 샘플을 빌드하고 실행하려면 C++ 언어 구성 요소를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-111">You must install the C++ language components to build and run this sample.</span></span>
* <span data-ttu-id="a00a5-112">[Visual Studio Linux 개발](https://visualstudiogallery.msdn.microsoft.com/725025cf-7067-45c2-8d01-1e0fd359ae6e).</span><span class="sxs-lookup"><span data-stu-id="a00a5-112">[Visual Studio Linux Development](https://visualstudiogallery.msdn.microsoft.com/725025cf-7067-45c2-8d01-1e0fd359ae6e).</span></span> <span data-ttu-id="a00a5-113">Linux에서 개발하는 경우에 Visual Studio Linux 확장도 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-113">If you are developing on Linux, you must also install the Visual Studio Linux extension.</span></span> 

## <span data-ttu-id="a00a5-114"><a id="AzureSQL"></a>가상 컴퓨터에서 Azure SQL Database 및 SQL Server</span><span class="sxs-lookup"><span data-stu-id="a00a5-114"><a id="AzureSQL"></a>Azure SQL Database and SQL Server on virtual machines</span></span>
<span data-ttu-id="a00a5-115">Azure SQL은 Microsoft SQL Server에서 빌드되고 가용성이 높고 성능과 확장성이 뛰어난 서비스를 제공하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-115">Azure SQL is built on Microsoft SQL Server and is designed to provide a high-availability, performant, and scalable service.</span></span> <span data-ttu-id="a00a5-116">온-프레미스에서 실행되는 전용 데이터베이스를 통해 SQL Azure를 사용하는 많은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-116">There are many benefits to using SQL Azure over your proprietary database running on premises.</span></span> <span data-ttu-id="a00a5-117">SQL Azure에서는 데이터베이스를 설치, 설정, 유지 또는 관리할 필요가 없이 데이터베이스의 콘텐츠와 구조만 관리하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-117">With SQL Azure you don’t have to install, set up, maintain, or manage your database but only the content and the structure of your database.</span></span> <span data-ttu-id="a00a5-118">내결함성과 중복성처럼 데이터 베이스에 대해 일반적으로 걱정하는 것이 모두 기본 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-118">Typical things that we worry about with databases like fault tolerance and redundancy are all built in.</span></span> 

<span data-ttu-id="a00a5-119">Azure에는 현재 Azure SQL server 작업 부하를 호스팅하기 위한 두 가지 옵션, 즉 서비스로서 데이터베이스인 Azure SQL Database와 가상 컴퓨터(VM)의 SQL server가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-119">Azure currently has two options for hosting SQL server workloads: Azure SQL database, database as a service and SQL server on Virtual Machines (VM).</span></span> <span data-ttu-id="a00a5-120">Azure SQL Database가 새로운 클라우드 기반 응용 프로그램을 위해 클라우드 서비스가 제공하는 비용 절감과 성능 최적화를 활용하는 최선의 방법이라는 점을 제외하고 이 두 옵션간에 차이점을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-120">We will not get into detail about the differences between these two except that Azure SQL database is your best bet for new cloud-based applications to take advantage of the cost savings and performance optimization that cloud services provide.</span></span> <span data-ttu-id="a00a5-121">클라우드로 온-프레미스 응용 프로그램을 마이그레이션 또는 확장하려는 경우 Azure 가상 컴퓨터에서 SQL server가 더 적합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-121">If you are considering migrating or extending your on-premises applications to the cloud, SQL server on Azure virtual machine might work out better for you.</span></span> <span data-ttu-id="a00a5-122">이 문서에서 작업을 더 간단하게 유지하기 위해, Azure SQL Database를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-122">To keep things simple for this article, let's create an Azure SQL database.</span></span> 

## <span data-ttu-id="a00a5-123"><a id="ODBC"></a>데이터 액세스 기술: ODBC 및 OLE DB</span><span class="sxs-lookup"><span data-stu-id="a00a5-123"><a id="ODBC"></a>Data access technologies: ODBC and OLE DB</span></span>
<span data-ttu-id="a00a5-124">Azure SQL DB에 연결하는 것은 다르지 않고 데이터베이스에 연결하는 방법에는 ODBC(Open Database connectivity) 및 OLE DB(개체 연결 및 포함 데이터베이스)의 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-124">Connecting to Azure SQL DB is no different and currently there are two ways to connect to databases: ODBC (Open Database connectivity) and OLE DB (Object Linking and Embedding database).</span></span> <span data-ttu-id="a00a5-125">최근 몇 년간 Microsoft는 [기본 관계형 데이터 액세스에 대해 ODBC](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)에 맞추어 왔습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-125">In recent years, Microsoft has aligned with [ODBC for native relational data access](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/).</span></span> <span data-ttu-id="a00a5-126">ODBC은 비교적 간단하고 OLE DB보다 훨씬 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-126">ODBC is relatively simple, and also much faster than OLE DB.</span></span> <span data-ttu-id="a00a5-127">한 가지 주의할 점은 ODBC는 이전 C 스타일 API를 사용한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-127">The only caveat here is that ODBC does use an old C-style API.</span></span> 

## <span data-ttu-id="a00a5-128"><a id="Create"></a>1단계: Azure SQL Database 만들기</span><span class="sxs-lookup"><span data-stu-id="a00a5-128"><a id="Create"></a>Step 1:  Creating your Azure SQL Database</span></span>
<span data-ttu-id="a00a5-129">샘플 데이터베이스를 만드는 방법을 알아보려면 [시작 페이지](sql-database-get-started-portal.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a00a5-129">See the [getting started page](sql-database-get-started-portal.md) to learn how to create a sample database.</span></span>  <span data-ttu-id="a00a5-130">또는 [짧은 2분 비디오](https://azure.microsoft.com/documentation/videos/azure-sql-database-create-dbs-in-seconds/)를 보고 Azure Portal을 사용하여 Azure SQL Database를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-130">Alternatively, you can follow this [short two-minute video](https://azure.microsoft.com/documentation/videos/azure-sql-database-create-dbs-in-seconds/) to create an Azure SQL database using the Azure portal.</span></span>

## <span data-ttu-id="a00a5-131"><a id="ConnectionString"></a>2단계: 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="a00a5-131"><a id="ConnectionString"></a>Step 2:  Get connection string</span></span>
<span data-ttu-id="a00a5-132">Azure SQL Database를 프로비전한 후 연결 정보를 확인하고 방화벽 액세스에 대한 클라이언트 IP를 추가하려면 다음 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-132">After your Azure SQL database has been provisioned, you need to carry out the following steps to determine connection information and add your client IP for firewall access.</span></span> 

<span data-ttu-id="a00a5-133">[Azure Portal](https://portal.azure.com/)에서, 데이터베이스에 대한 개요 섹션의 일부로 나열된 **데이터베이스 연결 문자열 표시**를 사용하여 Azure SQL Database ODBC 연결 문자열로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-133">In [Azure portal](https://portal.azure.com/), go to your Azure SQL database ODBC connection string by using the **Show database connection strings** listed as a part of the overview section for your database:</span></span> 

![ODBCConnectionString](./media/sql-database-develop-cplusplus-simple/azureportal.png)

![ODBCConnectionStringProps](./media/sql-database-develop-cplusplus-simple/dbconnection.png)

<span data-ttu-id="a00a5-136">**ODBC(Node.js 포함) [SQL 인증]** 문자열의 내용을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-136">Copy the contents of the **ODBC (Includes Node.js) [SQL authentication]** string.</span></span> <span data-ttu-id="a00a5-137">이 문자열은 C++ ODBC 명령줄 인터프리터에서 연결하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-137">We use this string later to connect from our C++ ODBC command-line interpreter.</span></span> <span data-ttu-id="a00a5-138">이 문자열은 드라이버, 서버 및 다른 데이터베이스 연결 매개 변수 등의 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-138">This string provides details such as the driver, server, and other database connection parameters.</span></span> 

## <span data-ttu-id="a00a5-139"><a id="Firewall"></a>3단계: 방화벽에 IP 추가</span><span class="sxs-lookup"><span data-stu-id="a00a5-139"><a id="Firewall"></a>Step 3:  Add your IP to the firewall</span></span>
<span data-ttu-id="a00a5-140">Database 서버에 대한 방화벽 섹션으로 이동하고 [이 단계를 사용하여 방화벽에 클라이언트 IP](sql-database-configure-firewall-settings.md)를 추가하여 다음과 같이 성공적인 연결을 설정하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-140">Go to the firewall section for your Database server and add your [client IP to the firewall using these steps](sql-database-configure-firewall-settings.md) to make sure we can establish a successful connection:</span></span> 

![AddyourIPWindow](./media/sql-database-develop-cplusplus-simple/ip.png)

<span data-ttu-id="a00a5-142">이 시점에서 Azure SQL DB를 구성하고 C++ 코드에서 연결할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-142">At this point, you have configured your Azure SQL DB and are ready to connect from your C++ code.</span></span> 

## <span data-ttu-id="a00a5-143"><a id="Windows"></a>4단계: Windows C/C++ 응용 프로그램에서 연결</span><span class="sxs-lookup"><span data-stu-id="a00a5-143"><a id="Windows"></a>Step 4: Connecting from a Windows C/C++ application</span></span>
<span data-ttu-id="a00a5-144">Visual Studio에서 빌드한 [이 샘플을 사용하여 Windows에서 ODBC를 사용하여 Azure SQL DB](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29)에 쉽게 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-144">You can easily connect to your [Azure SQL DB using ODBC on Windows using this sample](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29) that builds with Visual Studio.</span></span> <span data-ttu-id="a00a5-145">샘플에서는 Azure SQL DB에 연결하는 데 사용할 수 있는 ODBC 명령줄 인터프리터를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-145">The sample implements an ODBC command-line interpreter that can be used to connect to our Azure SQL DB.</span></span> <span data-ttu-id="a00a5-146">이 샘플에는 명령줄 인수로서 데이터베이스 원본 이름(DSN) 파일 또는 Azure Portal에서 이전에 복사한 세부 정보 표시 연결 문자열을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-146">This sample takes either a Database source name file (DSN) file as a command-line argument or the verbose connection string that we copied earlier from the Azure portal.</span></span> <span data-ttu-id="a00a5-147">이 프로젝트에 대한 속성 페이지를 표시하고 다음과 같이 명령 인수로서 연결 문자열을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-147">Bring up the property page for this project and paste the connection string as a command argument as shown here:</span></span> 

![DSN Propsfile](./media/sql-database-develop-cplusplus-simple/props.png)

<span data-ttu-id="a00a5-149">해당 데이터베이스 연결 문자열의 일부로 데이터베이스에 대한 올바른 인증 세부 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-149">Make sure you provide the right authentication details for your database as a part of that database connection string.</span></span> 

<span data-ttu-id="a00a5-150">빌드하려면 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-150">Launch the application to build it.</span></span> <span data-ttu-id="a00a5-151">성공적인 연결의 유효성을 검사하는 창이 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-151">You should see the following window validating a successful connection.</span></span> <span data-ttu-id="a00a5-152">데이터베이스 연결의 유효성을 검사하려면 **테이블 만들기**와 같은 몇 가지 기본 SQL 명령을 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-152">You can even run some basic SQL commands like **create table** to validate your database connectivity:</span></span>

![SQL 명령](./media/sql-database-develop-cplusplus-simple/sqlcommands.png)

<span data-ttu-id="a00a5-154">또는 명령 인수가 제공되지 않는 경우 시작되는 마법사를 사용 하여 DSN 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-154">Alternatively, you could create a DSN file using the wizard that is launched when no command arguments are provided.</span></span> <span data-ttu-id="a00a5-155">이 옵션을 함께 시도하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-155">We recommend that you try this option as well.</span></span> <span data-ttu-id="a00a5-156">자동화 및 인증 설정 보호를 위해 DSN 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-156">You can use this DSN file for automation and protecting your authentication settings:</span></span> 

![파일 DSN 만들기](./media/sql-database-develop-cplusplus-simple/datasource.png)

<span data-ttu-id="a00a5-158">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-158">Congratulations!</span></span> <span data-ttu-id="a00a5-159">이제 Windows에서 C++ 및 ODBC를 사용하여 Azure SQL에 성공적으로 연결했습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-159">You have now successfully connected to Azure SQL using C++ and ODBC on Windows.</span></span> <span data-ttu-id="a00a5-160">Linux 플랫폼에도 동일한 작업을 수행하는 읽기를 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-160">You can continue reading to do the same for Linux platform as well.</span></span> 

## <span data-ttu-id="a00a5-161"><a id="Linux"></a>5 단계: Linux C/C++ 응용 프로그램에서 연결</span><span class="sxs-lookup"><span data-stu-id="a00a5-161"><a id="Linux"></a>Step 5: Connecting from a Linux C/C++ application</span></span>
<span data-ttu-id="a00a5-162">아직 새 소식을 듣지 못했다면 Visual Studio에서 이제 C++ Linux 응용 프로그램도 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-162">In case you haven’t heard the news yet, Visual Studio now allows you to develop C++ Linux application as well.</span></span> <span data-ttu-id="a00a5-163">[Linux 개발용 Visual C++](https://blogs.msdn.microsoft.com/vcblog/2016/03/30/visual-c-for-linux-development/) 블로그에서 이 새 시나리오에 대해 참고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-163">You can read about this new scenario in the [Visual C++ for Linux Development](https://blogs.msdn.microsoft.com/vcblog/2016/03/30/visual-c-for-linux-development/) blog.</span></span> <span data-ttu-id="a00a5-164">Linux용으로 빌드하려면 Linux distro가 실행되고 있는 원격 컴퓨터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-164">To build for Linux, you need a remote machine where your Linux distro is running.</span></span> <span data-ttu-id="a00a5-165">원격 컴퓨터가 없다면 [Linux Azure 가상 컴퓨터](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용하여 신속하게 하나를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-165">If you don’t have one available, you can set one up quickly using [Linux Azure Virtual machines](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="a00a5-166">이 자습서에서는 Ubuntu 16.04 Linux 배포판이 설치되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-166">For this tutorial, let us assume that you have an Ubuntu 16.04 Linux distribution set up.</span></span> <span data-ttu-id="a00a5-167">여기 나온 단계는 Ubuntu 15.10, Red Hat 6 및 Red Hat 7에도 적용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-167">The steps here should also apply to Ubuntu 15.10, Red Hat 6, and Red Hat 7.</span></span> 

<span data-ttu-id="a00a5-168">다음 단계에서는 배포에 대한 SQL 및 ODBC에 필요한 라이브러리를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-168">The following steps install the libraries needed for SQL and ODBC for your distro:</span></span>

    sudo su
    sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/mssql-ubuntu-test/ xenial main" > /etc/apt/sources.list.d/mssqlpreview.list'
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    apt-get update
    apt-get install msodbcsql
    apt-get install unixodbc-dev-utf16 #this step is optional but recommended*

<span data-ttu-id="a00a5-169">Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-169">Launch Visual Studio.</span></span> <span data-ttu-id="a00a5-170">[도구] -> [옵션] -> [플랫폼 간] -> [연결 관리자]에서 Linux 상자에 연결을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-170">Under Tools -> Options -> Cross Platform -> Connection Manager, add a connection to your Linux box:</span></span> 

![도구 옵션](./media/sql-database-develop-cplusplus-simple/tools.png)

<span data-ttu-id="a00a5-172">SSH 통해 연결이 설정된 후에 빈 프로젝트(Linux) 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-172">After connection over SSH is established, create an Empty project (Linux) template:</span></span> 

![새 프로젝트 템플릿](./media/sql-database-develop-cplusplus-simple/template.png)

<span data-ttu-id="a00a5-174">그런 다음 [새 C 소스 파일을 추가하고 다음 내용으로 교체](https://github.com/Microsoft/VCSamples/blob/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29/odbcconnector/odbcconnector.c)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-174">You can then add a [new C source file and replace it with this content](https://github.com/Microsoft/VCSamples/blob/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29/odbcconnector/odbcconnector.c).</span></span> <span data-ttu-id="a00a5-175">ODBC Api SQLAllocHandle, SQLSetConnectAttr 및 SQLDriverConnect를 사용하여 초기화하고 데이터베이스에 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-175">Using the ODBC APIs SQLAllocHandle, SQLSetConnectAttr, and SQLDriverConnect, you should be able to initialize and establish a connection to your database.</span></span> <span data-ttu-id="a00a5-176">Windows ODBC 샘플과 마찬가지로 SQLDriverConnect 호출을 Azure Portal에서 이전에 복사한 데이터베이스 연결 문자열 매개 변수의 세부 정보로 교체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-176">Like with the Windows ODBC sample, you need to replace the SQLDriverConnect call with the details from your database connection string parameters copied from the Azure portal previously.</span></span> 

     retcode = SQLDriverConnect(
        hdbc, NULL, "Driver=ODBC Driver 13 for SQL"
                    "Server;Server=<yourserver>;Uid=<yourusername>;Pwd=<"
                    "yourpassword>;database=<yourdatabase>",
        SQL_NTS, outstr, sizeof(outstr), &outstrlen, SQL_DRIVER_NOPROMPT);

<span data-ttu-id="a00a5-177">컴파일하기 전에 마지막으로 라이브러리 종속성으로 **odbc**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-177">The last thing to do before compiling is to add **odbc** as a library dependency:</span></span> 

![입력된 라이브러리로 ODBC 추가](./media/sql-database-develop-cplusplus-simple/lib.png)

<span data-ttu-id="a00a5-179">응용 프로그램을 시작하려면 **디버그** 메뉴에서 Linux 콘솔을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-179">To launch your application, bring up the Linux Console from the **Debug** menu:</span></span> 

![Linux 콘솔](./media/sql-database-develop-cplusplus-simple/linuxconsole.png)

<span data-ttu-id="a00a5-181">연결에 성공하면 이제 Linux 콘솔에 인쇄된 현재 데이터베이스 이름이 보입니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-181">If your connection was successful, you should now see the current database name printed in the Linux Console:</span></span> 

![Linux 콘솔 창 출력](./media/sql-database-develop-cplusplus-simple/linuxconsolewindow.png)

<span data-ttu-id="a00a5-183">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-183">Congratulations!</span></span> <span data-ttu-id="a00a5-184">이 자습서를 성공적으로 완료했습니다. 이제 Windows 및 Linux 플랫폼의 C++에서 Azure SQL DB에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-184">You have successfully completed the tutorial and can now connect to your Azure SQL DB from C++ on Windows and Linux platforms.</span></span>

## <span data-ttu-id="a00a5-185"><a id="GetSolution"></a> 전체 C++ 자습서 솔루션 가져오기</span><span class="sxs-lookup"><span data-stu-id="a00a5-185"><a id="GetSolution"></a>Get the complete C/C++ tutorial solution</span></span>
<span data-ttu-id="a00a5-186">github에서 이 문서의 모든 샘플을 포함하는 GetStarted 솔루션을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a00a5-186">You can find the GetStarted solution that contains all the samples in this article at github:</span></span>

* <span data-ttu-id="a00a5-187">[ODBC C++ Windows 샘플](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29), Azure SQL에 연결하려면 Windows C++ ODBC 샘플 다운로드</span><span class="sxs-lookup"><span data-stu-id="a00a5-187">[ODBC C++ Windows sample](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29), Download the Windows C++ ODBC Sample to connect to Azure SQL</span></span>
* <span data-ttu-id="a00a5-188">[ODBC C++ Windows 샘플](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29), Azure SQL에 연결하려면 Linux C++ ODBC 샘플 다운로드</span><span class="sxs-lookup"><span data-stu-id="a00a5-188">[ODBC C++ Linux sample](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29), Download the Linux C++ ODBC Sample to connect to Azure SQL</span></span>

## <a name="next-steps"></a><span data-ttu-id="a00a5-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a00a5-189">Next steps</span></span>
* <span data-ttu-id="a00a5-190">[SQL 데이터베이스 개발 개요](sql-database-develop-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a00a5-190">Review the [SQL Database Development Overview](sql-database-develop-overview.md)</span></span>
* <span data-ttu-id="a00a5-191">[ODBC API 참조](https://docs.microsoft.com/sql/odbc/reference/syntax/odbc-api-reference/)에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="a00a5-191">More information on the [ODBC API Reference](https://docs.microsoft.com/sql/odbc/reference/syntax/odbc-api-reference/)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a00a5-192">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a00a5-192">Additional resources</span></span>
* [<span data-ttu-id="a00a5-193">Azure SQL 데이터베이스를 사용한 다중 테넌트 SaaS 응용 프로그램 디자인 패턴</span><span class="sxs-lookup"><span data-stu-id="a00a5-193">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* <span data-ttu-id="a00a5-194">모든 [SQL 데이터베이스의 기능](https://azure.microsoft.com/services/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="a00a5-194">Explore all the [capabilities of SQL Database](https://azure.microsoft.com/services/sql-database/)</span></span>

