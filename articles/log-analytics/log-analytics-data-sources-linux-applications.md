---
title: "OMS 로그 분석의 Linux 응용 프로그램 성능 aaaCollect | Microsoft Docs"
description: "이 문서 Apache HTTP Server 및 MySQL에 대 한 Linux toocollect 성능 카운터에 대 한 hello OMS 에이전트를 구성 하는 세부 정보를 제공 합니다."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 51105c6add5c7941a004570a76a4d94c02fc8a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-performance-counters-for-linux-applications-in-log-analytics"></a><span data-ttu-id="b240a-103">Log Analytics에서 Linux 응용 프로그램에 대한 성능 카운터 수집</span><span class="sxs-lookup"><span data-stu-id="b240a-103">Collect performance counters for Linux applications in Log Analytics</span></span> 
<span data-ttu-id="b240a-104">이 문서에서는 hello 구성에 대 한 세부 정보를 제공 [Linux 용 OMS 에이전트](https://github.com/Microsoft/OMS-Agent-for-Linux) 특정 응용 프로그램에 대 한 toocollect 성능 카운터입니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-104">This article provides details for configuring hello [OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) toocollect performance counters for specific applications.</span></span>  <span data-ttu-id="b240a-105">이 문서에 포함 하는 hello 응용 프로그램은:</span><span class="sxs-lookup"><span data-stu-id="b240a-105">hello applications included in this article are:</span></span>  

- [<span data-ttu-id="b240a-106">MySQL</span><span class="sxs-lookup"><span data-stu-id="b240a-106">MySQL</span></span>](#MySQL)
- [<span data-ttu-id="b240a-107">Apache HTTP 서버</span><span class="sxs-lookup"><span data-stu-id="b240a-107">Apache HTTP Server</span></span>](#apache-http-server)

## <a name="mysql"></a><span data-ttu-id="b240a-108">MySQL</span><span class="sxs-lookup"><span data-stu-id="b240a-108">MySQL</span></span>
<span data-ttu-id="b240a-109">Hello OMS 에이전트를 설치할 때 hello 컴퓨터에서 MySQL Server 또는 MariaDB 서버가 검색 되 면 한 성능 모니터링 공급자 MySQL Server에 대 한 자동으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-109">If MySQL Server or MariaDB Server is detected on hello computer when hello OMS agent is installed, a performance monitoring provider for MySQL Server will be automatically installed.</span></span> <span data-ttu-id="b240a-110">이 공급자는 toohello 로컬 MySQL/MariaDB 서버 tooexpose 성능 통계를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-110">This provider connects toohello local MySQL/MariaDB server tooexpose performance statistics.</span></span> <span data-ttu-id="b240a-111">MySQL 사용자 자격 증명 hello 공급자 액세스할 수 있도록 MySQL 서버 hello 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-111">MySQL user credentials must be configured so that hello provider can access hello MySQL Server.</span></span>

### <a name="configure-mysql-credentials"></a><span data-ttu-id="b240a-112">MySQL 자격 증명 구성</span><span class="sxs-lookup"><span data-stu-id="b240a-112">Configure MySQL credentials</span></span>
<span data-ttu-id="b240a-113">hello MySQL OMI 공급자는 미리 구성 된 MySQL 사용자가 수행 해야 하 고 MySQL 클라이언트 라이브러리가 순서 tooquery hello 성능 및 상태 정보 hello MySQL 인스턴스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-113">hello MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order tooquery hello performance and health information from hello MySQL instance.</span></span>  <span data-ttu-id="b240a-114">이러한 자격 증명 hello Linux 에이전트에 저장 되는 인증 파일에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-114">These credentials are stored in an authentication file that's stored on hello Linux agent.</span></span>  <span data-ttu-id="b240a-115">hello 인증 파일에 바인딩 주소 지정 하 고 포트 hello MySQL 인스턴스가 수신 중인 toouse toogather 메트릭을 자격 증명.</span><span class="sxs-lookup"><span data-stu-id="b240a-115">hello authentication file specifies what bind-address and port hello MySQL instance is listening on and what credentials toouse toogather metrics.</span></span>  

<span data-ttu-id="b240a-116">MySQL OMI Linux hello에 대 한 hello OMS 에이전트를 설치 하는 동안 공급자가 바인딩 주소 및 포트와 집합 hello MySQL OMI 인증 파일을 부분적으로 한 MySQL my.cnf 구성 파일 (기본 위치)을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-116">During installation of hello OMS Agent for Linux hello MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set hello MySQL OMI authentication file.</span></span>

<span data-ttu-id="b240a-117">hello MySQL 인증 파일에 저장 된 `/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth`합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-117">hello MySQL authentication file is stored at `/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth`.</span></span>


### <a name="authentication-file-format"></a><span data-ttu-id="b240a-118">인증 파일 형식</span><span class="sxs-lookup"><span data-stu-id="b240a-118">Authentication file format</span></span>
<span data-ttu-id="b240a-119">다음은 hello MySQL OMI 인증 파일에 대 한 hello 형식</span><span class="sxs-lookup"><span data-stu-id="b240a-119">Following is hello format for hello MySQL OMI authentication file</span></span>

    [Port]=[Bind-Address], [username], [Base64 encoded Password]
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    AutoUpdate=[true|false]

<span data-ttu-id="b240a-120">다음 표에 hello hello 인증 파일의 hello 항목을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-120">hello entries in hello authentication file are described in hello following table.</span></span>

| <span data-ttu-id="b240a-121">속성</span><span class="sxs-lookup"><span data-stu-id="b240a-121">Property</span></span> | <span data-ttu-id="b240a-122">설명</span><span class="sxs-lookup"><span data-stu-id="b240a-122">Description</span></span> |
|:--|:--|
| <span data-ttu-id="b240a-123">포트</span><span class="sxs-lookup"><span data-stu-id="b240a-123">Port</span></span> | <span data-ttu-id="b240a-124">Hello 현재 포트 hello를 MySQL 인스턴스가 수신 중인를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-124">Represents hello current port hello MySQL instance is listening on.</span></span> <span data-ttu-id="b240a-125">포트 0 다음 hello 속성이 기본 인스턴스에 대해 사용 되도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-125">Port 0 specifies that hello properties following are used for default instance.</span></span> |
| <span data-ttu-id="b240a-126">바인딩 주소</span><span class="sxs-lookup"><span data-stu-id="b240a-126">Bind-Address</span></span>| <span data-ttu-id="b240a-127">현재 MySQL 바인딩-주소입니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-127">Current MySQL bind-address.</span></span> |
| <span data-ttu-id="b240a-128">username</span><span class="sxs-lookup"><span data-stu-id="b240a-128">username</span></span>| <span data-ttu-id="b240a-129">MySQL 사용자 toouse toomonitor hello MySQL server 인스턴스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-129">MySQL user used toouse toomonitor hello MySQL server instance.</span></span> |
| <span data-ttu-id="b240a-130">Base64로 인코딩된 암호</span><span class="sxs-lookup"><span data-stu-id="b240a-130">Base64 encoded Password</span></span>| <span data-ttu-id="b240a-131">Base 64로 인코드된 hello MySQL 모니터링 사용자의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-131">Password of hello MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="b240a-132">AutoUpdate</span><span class="sxs-lookup"><span data-stu-id="b240a-132">AutoUpdate</span></span>| <span data-ttu-id="b240a-133">에 대 한 toorescan hello my.cnf 파일에서 변경 되는지 여부를 지정 하 고 hello MySQL OMI 공급자가 업그레이드 hello MySQL OMI 인증 파일을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-133">Specifies whether toorescan for changes in hello my.cnf file and overwrite hello MySQL OMI Authentication file when hello MySQL OMI Provider is upgraded.</span></span> |

### <a name="default-instance"></a><span data-ttu-id="b240a-134">기본 인스턴스</span><span class="sxs-lookup"><span data-stu-id="b240a-134">Default instance</span></span>
<span data-ttu-id="b240a-135">기본 인스턴스 및 보다 쉽게 한 Linux 호스트에서 여러 MySQL 인스턴스를 관리 하는 포트 번호 toomake hello MySQL OMI 인증 파일 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-135">hello MySQL OMI authentication file can define a default instance and port number toomake managing multiple MySQL instances on one Linux host easier.</span></span>  <span data-ttu-id="b240a-136">hello 기본 인스턴스가 포트 0 인스턴스에 의해 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-136">hello default instance is denoted by an instance with port 0.</span></span> <span data-ttu-id="b240a-137">모든 추가 인스턴스는 서로 다른 값을 지정 하지 않은 경우 hello 기본 인스턴스에서 설정 하는 속성을 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-137">All additional instances will inherit properties set from hello default instance unless they specify different values.</span></span> <span data-ttu-id="b240a-138">예를 들어 포트 '3308'에서 수신 대기 중인 MySQL 인스턴스가 추가 되 면 hello 기본 인스턴스의 바인딩 주소, username 및 password Base64 인코딩 tootry 사용된 되며 3308에서 수신 대기 하는 hello 인스턴스를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-138">For example, if MySQL instance listening on port ‘3308’ is added, hello default instance’s bind-address, username, and Base64 encoded password will be used tootry and monitor hello instance listening on 3308.</span></span> <span data-ttu-id="b240a-139">사용 하 여 3308 hello 인스턴스가 바인딩된 tooanother 주소인 경우 hello 동일한 MySQL 사용자 이름 및 암호 쌍만 hello 바인딩 주소의 필요 정도와 hello 다른 속성은 상속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-139">If hello instance on 3308 is bound tooanother address and uses hello same MySQL username and password pair only hello bind-address is needed, and hello other properties will be inherited.</span></span>

<span data-ttu-id="b240a-140">다음 표에 hello에 인스턴스 설정 예</span><span class="sxs-lookup"><span data-stu-id="b240a-140">hello following table has example instance settings</span></span> 

| <span data-ttu-id="b240a-141">설명</span><span class="sxs-lookup"><span data-stu-id="b240a-141">Description</span></span> | <span data-ttu-id="b240a-142">파일</span><span class="sxs-lookup"><span data-stu-id="b240a-142">File</span></span> |
|:--|:--|
| <span data-ttu-id="b240a-143">기본 인스턴스 및 포트 3308의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-143">Default instance and instance with port 3308.</span></span> | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=, ,`<br>`AutoUpdate=true` |
| <span data-ttu-id="b240a-144">기본 인스턴스 및 포트 3308의 인스턴스, 다른 사용자 이름 및 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-144">Default instance and instance with port 3308 and different user name and password.</span></span> | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=127.0.1.1, myuser2,cGluaGVhZA==`<br>`AutoUpdate=true` |


### <a name="mysql-omi-authentication-file-program"></a><span data-ttu-id="b240a-145">MySQL OMI 인증 파일 프로그램</span><span class="sxs-lookup"><span data-stu-id="b240a-145">MySQL OMI Authentication File Program</span></span>
<span data-ttu-id="b240a-146">에 포함 되어 hello 설치 hello MySQL OMI 공급자 MySQL OMI 인증 파일 프로그램 사용된 tooedit hello MySQL OMI 인증 파일 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-146">Included with hello installation of hello MySQL OMI provider is a MySQL OMI authentication file program which can be used tooedit hello MySQL OMI Authentication file.</span></span> <span data-ttu-id="b240a-147">hello 인증 파일 프로그램 hello 수정할 수 있는 위치에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-147">hello authentication file program can be found at hello following location.</span></span>

    /opt/microsoft/mysql-cimprov/bin/mycimprovauth

> [!NOTE]
> <span data-ttu-id="b240a-148">hello 자격 증명 파일 hello omsagent 계정이 읽을 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-148">hello credentials file must be readable by hello omsagent account.</span></span> <span data-ttu-id="b240a-149">로 hello mycimprovauth 명령을 실행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-149">Running hello mycimprovauth command as omsgent is recommended.</span></span>

<span data-ttu-id="b240a-150">hello 다음 표에서 자세히 설명 hello 구문 mycimprovauth 사용에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-150">hello following table provides details on hello syntax for using mycimprovauth.</span></span>

| <span data-ttu-id="b240a-151">작업</span><span class="sxs-lookup"><span data-stu-id="b240a-151">Operation</span></span> | <span data-ttu-id="b240a-152">예제</span><span class="sxs-lookup"><span data-stu-id="b240a-152">Example</span></span> | <span data-ttu-id="b240a-153">설명</span><span class="sxs-lookup"><span data-stu-id="b240a-153">Description</span></span>
|:--|:--|:--|
| <span data-ttu-id="b240a-154">autoupdate *false\\</span><span class="sxs-lookup"><span data-stu-id="b240a-154">autoupdate *false\\</span></span>|<span data-ttu-id="b240a-155">true*</span><span class="sxs-lookup"><span data-stu-id="b240a-155">true*</span></span> | <span data-ttu-id="b240a-156">mycimprovauth autoupdate false</span><span class="sxs-lookup"><span data-stu-id="b240a-156">mycimprovauth autoupdate false</span></span> | <span data-ttu-id="b240a-157">여부 hello 인증 파일은 자동으로 업데이트 하는 집합에 다시 시작 하거나 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-157">Sets whether or not hello authentication file will be automatically updated on restart or update.</span></span> |
| <span data-ttu-id="b240a-158">default *bind-address username password*</span><span class="sxs-lookup"><span data-stu-id="b240a-158">default *bind-address username password*</span></span> | <span data-ttu-id="b240a-159">mycimprovauth default 127.0.0.1 root pwd</span><span class="sxs-lookup"><span data-stu-id="b240a-159">mycimprovauth default 127.0.0.1 root pwd</span></span> | <span data-ttu-id="b240a-160">집합 hello hello MySQL OMI 인증 파일의에서 기본 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="b240a-160">Sets hello default instance in hello MySQL OMI authentication file.</span></span><br><span data-ttu-id="b240a-161">일반 텍스트에 hello 암호 필드를 입력할 수-hello MySQL OMI 인증 파일에에서 hello 암호 Base 64로 인코딩된 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-161">hello password field should be entered in plain text - hello password in hello MySQL OMI authentication file will be Base 64 encoded.</span></span> |
| <span data-ttu-id="b240a-162">delete *default\\</span><span class="sxs-lookup"><span data-stu-id="b240a-162">delete *default\\</span></span>|<span data-ttu-id="b240a-163">port_num*</span><span class="sxs-lookup"><span data-stu-id="b240a-163">port_num*</span></span> | <span data-ttu-id="b240a-164">mycimprovauth 3308</span><span class="sxs-lookup"><span data-stu-id="b240a-164">mycimprovauth 3308</span></span> | <span data-ttu-id="b240a-165">중 하나가 기본적으로 또는 포트 번호로 hello 지정 된 인스턴스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-165">Deletes hello specified instance by either default or by port number.</span></span> |
| <span data-ttu-id="b240a-166">help</span><span class="sxs-lookup"><span data-stu-id="b240a-166">help</span></span> | <span data-ttu-id="b240a-167">mycimprov help</span><span class="sxs-lookup"><span data-stu-id="b240a-167">mycimprov help</span></span> | <span data-ttu-id="b240a-168">명령 toouse 목록 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-168">Prints out a list of commands toouse.</span></span> |
| <span data-ttu-id="b240a-169">print</span><span class="sxs-lookup"><span data-stu-id="b240a-169">print</span></span> | <span data-ttu-id="b240a-170">mycimprov print</span><span class="sxs-lookup"><span data-stu-id="b240a-170">mycimprov print</span></span> | <span data-ttu-id="b240a-171">MySQL OMI 인증 파일 프로그램 쉽게 tooread 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-171">Prints out an easy tooread MySQL OMI authentication file.</span></span> |
| <span data-ttu-id="b240a-172">update port_num *bind-address username password*</span><span class="sxs-lookup"><span data-stu-id="b240a-172">update port_num *bind-address username password*</span></span> | <span data-ttu-id="b240a-173">mycimprov update 3307 127.0.0.1 root pwd</span><span class="sxs-lookup"><span data-stu-id="b240a-173">mycimprov update 3307 127.0.0.1 root pwd</span></span> | <span data-ttu-id="b240a-174">Hello 지정 된 인스턴스를 업데이트 하거나 존재 하지 않는 경우 hello 인스턴스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-174">Updates hello specified instance or adds hello instance if it does not exist.</span></span> |

<span data-ttu-id="b240a-175">hello 다음 예제 명령은 hello MySQL server에 대 한 기본 사용자 계정을 localhost에 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-175">hello following example commands define a default user account for hello MySQL server on localhost.</span></span>  <span data-ttu-id="b240a-176">일반 텍스트에 hello 암호 필드를 입력할 수-hello MySQL OMI 인증 파일에에서 hello 암호 Base 64로 인코딩된 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-176">hello password field should be entered in plain text - hello password in hello MySQL OMI authentication file will be Base 64 encoded</span></span>

    sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>'
    sudo /opt/omi/bin/service_control restart

### <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="b240a-177">MySQL 성능 카운터에 필요한 데이터베이스 권한</span><span class="sxs-lookup"><span data-stu-id="b240a-177">Database Permissions Required for MySQL Performance Counters</span></span>
<span data-ttu-id="b240a-178">MySQL 사용자 hello 쿼리 toocollect MySQL Server 성능 데이터를 다음 액세스 toohello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-178">hello MySQL User requires access toohello following queries toocollect MySQL Server performance data.</span></span> 

    SHOW GLOBAL STATUS;
    SHOW GLOBAL VARIABLES:


<span data-ttu-id="b240a-179">hello MySQL 사용자에 대 한 SELECT 권한도 toohello 다음 기본 표 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-179">hello MySQL user also requires SELECT access toohello following default tables.</span></span>

- <span data-ttu-id="b240a-180">information_schema</span><span class="sxs-lookup"><span data-stu-id="b240a-180">information_schema</span></span>
- <span data-ttu-id="b240a-181">mysql.</span><span class="sxs-lookup"><span data-stu-id="b240a-181">mysql.</span></span> 

<span data-ttu-id="b240a-182">Hello 다음 grant 명령을 실행 하 여 이러한 권한은 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-182">These privileges can be granted by running hello following grant commands.</span></span>

    GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
    GRANT SELECT ON mysql.* too‘monuser’@’localhost’;


> [!NOTE]
> <span data-ttu-id="b240a-183">toogrant 권한 tooa 부여할 hello 권한 뿐만 아니라 ' GRANT option ' hello MySQL 모니터링 사용자 권한을 부여 하는 사용자 hello 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-183">toogrant permissions tooa MySQL monitoring user hello granting user must have hello ‘GRANT option’ privilege as well as hello privilege being granted.</span></span>

### <a name="define-performance-counters"></a><span data-ttu-id="b240a-184">성능 카운터 정의</span><span class="sxs-lookup"><span data-stu-id="b240a-184">Define performance counters</span></span>

<span data-ttu-id="b240a-185">Linux toosend 데이터 tooLog 분석에 대 한 hello OMS 에이전트를 구성 하 고 나면 hello 성능 카운터 toocollect를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-185">Once you configure hello OMS Agent for Linux toosend data tooLog Analytics, you must configure hello performance counters toocollect.</span></span>  <span data-ttu-id="b240a-186">hello 절차를 사용 하 여 [로그 분석에서 Windows 및 Linux 성능 데이터 원본](log-analytics-data-sources-windows-events.md) 다음 표에 hello에 hello 카운터와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-186">Use hello procedure in [Windows and Linux performance data sources in Log Analytics](log-analytics-data-sources-windows-events.md) with hello counters in hello following table.</span></span>

| <span data-ttu-id="b240a-187">개체 이름</span><span class="sxs-lookup"><span data-stu-id="b240a-187">Object Name</span></span> | <span data-ttu-id="b240a-188">카운터 이름</span><span class="sxs-lookup"><span data-stu-id="b240a-188">Counter Name</span></span> |
|:--|:--|
| <span data-ttu-id="b240a-189">MySQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="b240a-189">MySQL Database</span></span> | <span data-ttu-id="b240a-190">디스크 공간(바이트)</span><span class="sxs-lookup"><span data-stu-id="b240a-190">Disk Space in Bytes</span></span> |
| <span data-ttu-id="b240a-191">MySQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="b240a-191">MySQL Database</span></span> | <span data-ttu-id="b240a-192">테이블</span><span class="sxs-lookup"><span data-stu-id="b240a-192">Tables</span></span> |
| <span data-ttu-id="b240a-193">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="b240a-193">MySQL Server</span></span> | <span data-ttu-id="b240a-194">중단된 연결 Pct</span><span class="sxs-lookup"><span data-stu-id="b240a-194">Aborted Connection Pct</span></span> |
| <span data-ttu-id="b240a-195">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="b240a-195">MySQL Server</span></span> | <span data-ttu-id="b240a-196">연결 사용 Pct</span><span class="sxs-lookup"><span data-stu-id="b240a-196">Connection Use Pct</span></span> |
| <span data-ttu-id="b240a-197">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="b240a-197">MySQL Server</span></span> | <span data-ttu-id="b240a-198">디스크 공간 사용(바이트)</span><span class="sxs-lookup"><span data-stu-id="b240a-198">Disk Space Use in Bytes</span></span> |
| <span data-ttu-id="b240a-199">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="b240a-199">MySQL Server</span></span> | <span data-ttu-id="b240a-200">전체 테이블 검색 Pct</span><span class="sxs-lookup"><span data-stu-id="b240a-200">Full Table Scan Pct</span></span> |
| <span data-ttu-id="b240a-201">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="b240a-201">MySQL Server</span></span> | <span data-ttu-id="b240a-202">InnoDB 버퍼 풀 적중 Pct</span><span class="sxs-lookup"><span data-stu-id="b240a-202">InnoDB Buffer Pool Hit Pct</span></span> |
| <span data-ttu-id="b240a-203">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="b240a-203">MySQL Server</span></span> | <span data-ttu-id="b240a-204">InnoDB 버퍼 풀 사용 Pct</span><span class="sxs-lookup"><span data-stu-id="b240a-204">InnoDB Buffer Pool Use Pct</span></span> |
| <span data-ttu-id="b240a-205">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="b240a-205">MySQL Server</span></span> | <span data-ttu-id="b240a-206">InnoDB 버퍼 풀 사용 Pct</span><span class="sxs-lookup"><span data-stu-id="b240a-206">InnoDB Buffer Pool Use Pct</span></span> |
| <span data-ttu-id="b240a-207">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="b240a-207">MySQL Server</span></span> | <span data-ttu-id="b240a-208">키 캐시 적중 Pct</span><span class="sxs-lookup"><span data-stu-id="b240a-208">Key Cache Hit Pct</span></span> |
| <span data-ttu-id="b240a-209">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="b240a-209">MySQL Server</span></span> | <span data-ttu-id="b240a-210">키 캐시 사용 Pct</span><span class="sxs-lookup"><span data-stu-id="b240a-210">Key Cache Use Pct</span></span> |
| <span data-ttu-id="b240a-211">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="b240a-211">MySQL Server</span></span> | <span data-ttu-id="b240a-212">키 캐시 쓰기 Pct</span><span class="sxs-lookup"><span data-stu-id="b240a-212">Key Cache Write Pct</span></span> |
| <span data-ttu-id="b240a-213">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="b240a-213">MySQL Server</span></span> | <span data-ttu-id="b240a-214">쿼리 캐시 적중 Pct</span><span class="sxs-lookup"><span data-stu-id="b240a-214">Query Cache Hit Pct</span></span> |
| <span data-ttu-id="b240a-215">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="b240a-215">MySQL Server</span></span> | <span data-ttu-id="b240a-216">쿼리 캐시 잘라내기 Pct</span><span class="sxs-lookup"><span data-stu-id="b240a-216">Query Cache Prunes Pct</span></span> |
| <span data-ttu-id="b240a-217">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="b240a-217">MySQL Server</span></span> | <span data-ttu-id="b240a-218">쿼리 캐시 사용 Pct</span><span class="sxs-lookup"><span data-stu-id="b240a-218">Query Cache Use Pct</span></span> |
| <span data-ttu-id="b240a-219">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="b240a-219">MySQL Server</span></span> | <span data-ttu-id="b240a-220">테이블 캐시 적중 Pct</span><span class="sxs-lookup"><span data-stu-id="b240a-220">Table Cache Hit Pct</span></span> |
| <span data-ttu-id="b240a-221">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="b240a-221">MySQL Server</span></span> | <span data-ttu-id="b240a-222">테이블 캐시 사용 Pct</span><span class="sxs-lookup"><span data-stu-id="b240a-222">Table Cache Use Pct</span></span> |
| <span data-ttu-id="b240a-223">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="b240a-223">MySQL Server</span></span> | <span data-ttu-id="b240a-224">테이블 잠금 경합 Pct</span><span class="sxs-lookup"><span data-stu-id="b240a-224">Table Lock Contention Pct</span></span> |

## <a name="apache-http-server"></a><span data-ttu-id="b240a-225">Apache HTTP 서버</span><span class="sxs-lookup"><span data-stu-id="b240a-225">Apache HTTP Server</span></span> 
<span data-ttu-id="b240a-226">Apache HTTP Server hello omsagent 번들을 설치할 때 hello 컴퓨터에서 검색 되 면 한 성능 모니터링 공급자 Apache HTTP Server에 대 한 자동으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-226">If Apache HTTP Server is detected on hello computer when hello omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server will be automatically installed.</span></span> <span data-ttu-id="b240a-227">이 공급자는 순서 tooaccess 성능 데이터에 hello Apache HTTP Server에 로드 해야 하는 Apache 모듈을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-227">This provider relies on an Apache module that must be loaded into hello Apache HTTP Server in order tooaccess performance data.</span></span> <span data-ttu-id="b240a-228">다음 명령을 hello로 hello 모듈을 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-228">hello module can be loaded with hello following command:</span></span>
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="b240a-229">toounload hello Apache 모니터링 모듈을 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-229">toounload hello Apache monitoring module, run hello following command:</span></span>
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```

### <a name="define-performance-counters"></a><span data-ttu-id="b240a-230">성능 카운터 정의</span><span class="sxs-lookup"><span data-stu-id="b240a-230">Define performance counters</span></span>

<span data-ttu-id="b240a-231">Linux toosend 데이터 tooLog 분석에 대 한 hello OMS 에이전트를 구성 하 고 나면 hello 성능 카운터 toocollect를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-231">Once you configure hello OMS Agent for Linux toosend data tooLog Analytics, you must configure hello performance counters toocollect.</span></span>  <span data-ttu-id="b240a-232">hello 절차를 사용 하 여 [로그 분석에서 Windows 및 Linux 성능 데이터 원본](log-analytics-data-sources-windows-events.md) 다음 표에 hello에 hello 카운터와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-232">Use hello procedure in [Windows and Linux performance data sources in Log Analytics](log-analytics-data-sources-windows-events.md) with hello counters in hello following table.</span></span>

| <span data-ttu-id="b240a-233">개체 이름</span><span class="sxs-lookup"><span data-stu-id="b240a-233">Object Name</span></span> | <span data-ttu-id="b240a-234">카운터 이름</span><span class="sxs-lookup"><span data-stu-id="b240a-234">Counter Name</span></span> |
|:--|:--|
| <span data-ttu-id="b240a-235">Apache HTTP 서버</span><span class="sxs-lookup"><span data-stu-id="b240a-235">Apache HTTP Server</span></span> | <span data-ttu-id="b240a-236">근무 중인 작업자</span><span class="sxs-lookup"><span data-stu-id="b240a-236">Busy Workers</span></span> |
| <span data-ttu-id="b240a-237">Apache HTTP 서버</span><span class="sxs-lookup"><span data-stu-id="b240a-237">Apache HTTP Server</span></span> | <span data-ttu-id="b240a-238">유휴 작업자</span><span class="sxs-lookup"><span data-stu-id="b240a-238">Idle Workers</span></span> |
| <span data-ttu-id="b240a-239">Apache HTTP 서버</span><span class="sxs-lookup"><span data-stu-id="b240a-239">Apache HTTP Server</span></span> | <span data-ttu-id="b240a-240">Pct 근무 중인 작업자</span><span class="sxs-lookup"><span data-stu-id="b240a-240">Pct Busy Workers</span></span> |
| <span data-ttu-id="b240a-241">Apache HTTP 서버</span><span class="sxs-lookup"><span data-stu-id="b240a-241">Apache HTTP Server</span></span> | <span data-ttu-id="b240a-242">총 Pct CPU</span><span class="sxs-lookup"><span data-stu-id="b240a-242">Total Pct CPU</span></span> |
| <span data-ttu-id="b240a-243">Apache 가상 호스트</span><span class="sxs-lookup"><span data-stu-id="b240a-243">Apache Virtual Host</span></span> | <span data-ttu-id="b240a-244">분당 오류 - 클라이언트</span><span class="sxs-lookup"><span data-stu-id="b240a-244">Errors per Minute - Client</span></span> |
| <span data-ttu-id="b240a-245">Apache 가상 호스트</span><span class="sxs-lookup"><span data-stu-id="b240a-245">Apache Virtual Host</span></span> | <span data-ttu-id="b240a-246">분당 오류 - 서버</span><span class="sxs-lookup"><span data-stu-id="b240a-246">Errors per Minute - Server</span></span> |
| <span data-ttu-id="b240a-247">Apache 가상 호스트</span><span class="sxs-lookup"><span data-stu-id="b240a-247">Apache Virtual Host</span></span> | <span data-ttu-id="b240a-248">요청당 KB</span><span class="sxs-lookup"><span data-stu-id="b240a-248">KB per Request</span></span> |
| <span data-ttu-id="b240a-249">Apache 가상 호스트</span><span class="sxs-lookup"><span data-stu-id="b240a-249">Apache Virtual Host</span></span> | <span data-ttu-id="b240a-250">초당 요청 KB</span><span class="sxs-lookup"><span data-stu-id="b240a-250">Requests KB per Second</span></span> |
| <span data-ttu-id="b240a-251">Apache 가상 호스트</span><span class="sxs-lookup"><span data-stu-id="b240a-251">Apache Virtual Host</span></span> | <span data-ttu-id="b240a-252">초당 요청</span><span class="sxs-lookup"><span data-stu-id="b240a-252">Requests per Second</span></span> |



## <a name="next-steps"></a><span data-ttu-id="b240a-253">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b240a-253">Next steps</span></span>
* <span data-ttu-id="b240a-254">Linux 에이전트에서 [성능 카운터를 수집합니다](log-analytics-data-sources-performance-counters.md).</span><span class="sxs-lookup"><span data-stu-id="b240a-254">[Collect performance counters](log-analytics-data-sources-performance-counters.md) from Linux agents.</span></span>
* <span data-ttu-id="b240a-255">에 대 한 자세한 내용은 [검색 로그](log-analytics-log-searches.md) tooanalyze hello 데이터가 데이터 원본 및 솔루션에서 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="b240a-255">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
