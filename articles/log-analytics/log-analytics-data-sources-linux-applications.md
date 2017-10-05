---
title: "OMS Log Analytics에서 Linux 응용 프로그램 성능 수집 | Microsoft Docs"
description: "이 문서에서는 MySQL 및 Apache HTTP 서버에 대한 성능 카운터를 수집하도록 Linux용 OMS 에이전트를 구성하는 세부 정보를 제공합니다."
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
ms.openlocfilehash: 04ea6f728e59ec8b47e54fe45e1adc6cbbfb85ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="collect-performance-counters-for-linux-applications-in-log-analytics"></a><span data-ttu-id="8fc22-103">Log Analytics에서 Linux 응용 프로그램에 대한 성능 카운터 수집</span><span class="sxs-lookup"><span data-stu-id="8fc22-103">Collect performance counters for Linux applications in Log Analytics</span></span> 
<span data-ttu-id="8fc22-104">이 문서에서는 특정 응용 프로그램에 대한 성능 카운터를 수집하도록 [Linux용 OMS 에이전트](https://github.com/Microsoft/OMS-Agent-for-Linux)를 구성하는 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-104">This article provides details for configuring the [OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) to collect performance counters for specific applications.</span></span>  <span data-ttu-id="8fc22-105">이 문서에 포함된 응용 프로그램은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-105">The applications included in this article are:</span></span>  

- [<span data-ttu-id="8fc22-106">MySQL</span><span class="sxs-lookup"><span data-stu-id="8fc22-106">MySQL</span></span>](#MySQL)
- [<span data-ttu-id="8fc22-107">Apache HTTP 서버</span><span class="sxs-lookup"><span data-stu-id="8fc22-107">Apache HTTP Server</span></span>](#apache-http-server)

## <a name="mysql"></a><span data-ttu-id="8fc22-108">MySQL</span><span class="sxs-lookup"><span data-stu-id="8fc22-108">MySQL</span></span>
<span data-ttu-id="8fc22-109">OMS 에이전트가 설치된 경우 컴퓨터에서 MySQL 서버나 MariaDB 서버가 감지되면, MySQL 서버용 성능 모니터링 공급자가 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-109">If MySQL Server or MariaDB Server is detected on the computer when the OMS agent is installed, a performance monitoring provider for MySQL Server will be automatically installed.</span></span> <span data-ttu-id="8fc22-110">이 공급자는 성능 통계를 공개하기 위해 로컬 MySQL/MariaDB 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-110">This provider connects to the local MySQL/MariaDB server to expose performance statistics.</span></span> <span data-ttu-id="8fc22-111">공급자가 MySQL 서버에 액세스할 수 있도록 MySQL 사용자 자격 증명을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-111">MySQL user credentials must be configured so that the provider can access the MySQL Server.</span></span>

### <a name="configure-mysql-credentials"></a><span data-ttu-id="8fc22-112">MySQL 자격 증명 구성</span><span class="sxs-lookup"><span data-stu-id="8fc22-112">Configure MySQL credentials</span></span>
<span data-ttu-id="8fc22-113">MySQL OMI 공급자가 MySQL 인스턴스의 성능 및 상태 정보를 쿼리하려면, 미리 정의된 MySQL 사용자와 설치되어 있는 MySQL 클라이언트 라이브러리가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-113">The MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order to query the performance and health information from the MySQL instance.</span></span>  <span data-ttu-id="8fc22-114">이러한 자격 증명은 Linux 에이전트에 저장된 인증 파일에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-114">These credentials are stored in an authentication file that's stored on the Linux agent.</span></span>  <span data-ttu-id="8fc22-115">인증 파일은 MySQL 인스턴스가 수신 대기할 바인딩 주소와 포트를 결정하고 메트릭 수집에 사용할 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-115">The authentication file specifies what bind-address and port the MySQL instance is listening on and what credentials to use to gather metrics.</span></span>  

<span data-ttu-id="8fc22-116">Linux용 OMS 에이전트를 설치하는 동안 MySQL OMI 공급자는 MySQL my.cnf 구성 파일(기본 위치)에서 바인딩 주소와 포트를 검색하고, MySQL OMI 인증 파일을 부분적으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-116">During installation of the OMS Agent for Linux the MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set the MySQL OMI authentication file.</span></span>

<span data-ttu-id="8fc22-117">MySQL 인증 파일은 `/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth`에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-117">The MySQL authentication file is stored at `/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth`.</span></span>


### <a name="authentication-file-format"></a><span data-ttu-id="8fc22-118">인증 파일 형식</span><span class="sxs-lookup"><span data-stu-id="8fc22-118">Authentication file format</span></span>
<span data-ttu-id="8fc22-119">다음은 MySQL OMI 인증 파일의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-119">Following is the format for the MySQL OMI authentication file</span></span>

    [Port]=[Bind-Address], [username], [Base64 encoded Password]
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    AutoUpdate=[true|false]

<span data-ttu-id="8fc22-120">인증 파일의 항목은 다음 테이블에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-120">The entries in the authentication file are described in the following table.</span></span>

| <span data-ttu-id="8fc22-121">속성</span><span class="sxs-lookup"><span data-stu-id="8fc22-121">Property</span></span> | <span data-ttu-id="8fc22-122">설명</span><span class="sxs-lookup"><span data-stu-id="8fc22-122">Description</span></span> |
|:--|:--|
| <span data-ttu-id="8fc22-123">포트</span><span class="sxs-lookup"><span data-stu-id="8fc22-123">Port</span></span> | <span data-ttu-id="8fc22-124">MySQL 인스턴스가 수신 대기 중인 현재 포트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-124">Represents the current port the MySQL instance is listening on.</span></span> <span data-ttu-id="8fc22-125">포트 0은 뒤에 나오는 속성이 기본 인스턴스에 사용된다는 것을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-125">Port 0 specifies that the properties following are used for default instance.</span></span> |
| <span data-ttu-id="8fc22-126">바인딩 주소</span><span class="sxs-lookup"><span data-stu-id="8fc22-126">Bind-Address</span></span>| <span data-ttu-id="8fc22-127">현재 MySQL 바인딩-주소입니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-127">Current MySQL bind-address.</span></span> |
| <span data-ttu-id="8fc22-128">username</span><span class="sxs-lookup"><span data-stu-id="8fc22-128">username</span></span>| <span data-ttu-id="8fc22-129">MySQL 서버 인스턴스를 모니터링하는 데 사용되는 MySQL 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-129">MySQL user used to use to monitor the MySQL server instance.</span></span> |
| <span data-ttu-id="8fc22-130">Base64로 인코딩된 암호</span><span class="sxs-lookup"><span data-stu-id="8fc22-130">Base64 encoded Password</span></span>| <span data-ttu-id="8fc22-131">Base64로 인코딩된 MySQL 모니터링 사용자의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-131">Password of the MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="8fc22-132">AutoUpdate</span><span class="sxs-lookup"><span data-stu-id="8fc22-132">AutoUpdate</span></span>| <span data-ttu-id="8fc22-133">MySQL OMI 공급자가 업그레이드되면 my.cnf 파일에서 변경 내용을 검색하고 MySQL OMI 인증 파일을 덮어쓸지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-133">Specifies whether to rescan for changes in the my.cnf file and overwrite the MySQL OMI Authentication file when the MySQL OMI Provider is upgraded.</span></span> |

### <a name="default-instance"></a><span data-ttu-id="8fc22-134">기본 인스턴스</span><span class="sxs-lookup"><span data-stu-id="8fc22-134">Default instance</span></span>
<span data-ttu-id="8fc22-135">MySQL OMI 인증 파일은 하나의 Linux 호스트에서 여러 MySQL 인스턴스를 쉽게 관리할 수 있도록 기본 인스턴스 및 포트 번호를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-135">The MySQL OMI authentication file can define a default instance and port number to make managing multiple MySQL instances on one Linux host easier.</span></span>  <span data-ttu-id="8fc22-136">기본 인스턴스는 포트 0으로 인스턴스에 의해 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-136">The default instance is denoted by an instance with port 0.</span></span> <span data-ttu-id="8fc22-137">모든 추가 인스턴스는 서로 다른 값을 지정하지 않는 한 기본 인스턴스의 설정 속성을 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-137">All additional instances will inherit properties set from the default instance unless they specify different values.</span></span> <span data-ttu-id="8fc22-138">예를 들어, '3308' 포드에서 수신 대기 중인 MySQL 인스턴스가 추가되면, 3308 포트에서 수신 대기 중인 인스턴스를 시도하고 모니터링하기 위해, 기본 인스턴스의 바인딩 주소, 사용자 이름, Base64로 인코딩된 암호가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-138">For example, if MySQL instance listening on port ‘3308’ is added, the default instance’s bind-address, username, and Base64 encoded password will be used to try and monitor the instance listening on 3308.</span></span> <span data-ttu-id="8fc22-139">3308의 인스턴스가 다른 주소로 바인딩되고 동일한 MySQL 사용자 이름과 암호 쌍이 사용되면, 바인딩 주소만 필요하고 다른 속성은 상속됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-139">If the instance on 3308 is bound to another address and uses the same MySQL username and password pair only the bind-address is needed, and the other properties will be inherited.</span></span>

<span data-ttu-id="8fc22-140">다음 테이블에는 예제 인스턴스 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-140">The following table has example instance settings</span></span> 

| <span data-ttu-id="8fc22-141">설명</span><span class="sxs-lookup"><span data-stu-id="8fc22-141">Description</span></span> | <span data-ttu-id="8fc22-142">파일</span><span class="sxs-lookup"><span data-stu-id="8fc22-142">File</span></span> |
|:--|:--|
| <span data-ttu-id="8fc22-143">기본 인스턴스 및 포트 3308의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-143">Default instance and instance with port 3308.</span></span> | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=, ,`<br>`AutoUpdate=true` |
| <span data-ttu-id="8fc22-144">기본 인스턴스 및 포트 3308의 인스턴스, 다른 사용자 이름 및 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-144">Default instance and instance with port 3308 and different user name and password.</span></span> | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=127.0.1.1, myuser2,cGluaGVhZA==`<br>`AutoUpdate=true` |


### <a name="mysql-omi-authentication-file-program"></a><span data-ttu-id="8fc22-145">MySQL OMI 인증 파일 프로그램</span><span class="sxs-lookup"><span data-stu-id="8fc22-145">MySQL OMI Authentication File Program</span></span>
<span data-ttu-id="8fc22-146">MySQL OMI 공급자의 설치에 포함된 것은 MySQL OMI 인증 파일 편집에 사용할 수 있는 MySQL OMI 인증 파일 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-146">Included with the installation of the MySQL OMI provider is a MySQL OMI authentication file program which can be used to edit the MySQL OMI Authentication file.</span></span> <span data-ttu-id="8fc22-147">다음 위치에서 인증 파일 프로그램을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-147">The authentication file program can be found at the following location.</span></span>

    /opt/microsoft/mysql-cimprov/bin/mycimprovauth

> [!NOTE]
> <span data-ttu-id="8fc22-148">자격 증명 파일은 omsagent 계정이 읽을 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-148">The credentials file must be readable by the omsagent account.</span></span> <span data-ttu-id="8fc22-149">omsgent로 mycimprovauth 명령을 실행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-149">Running the mycimprovauth command as omsgent is recommended.</span></span>

<span data-ttu-id="8fc22-150">다음 테이블에서 mycimprovauth 사용에 대한 구문의 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-150">The following table provides details on the syntax for using mycimprovauth.</span></span>

| <span data-ttu-id="8fc22-151">작업</span><span class="sxs-lookup"><span data-stu-id="8fc22-151">Operation</span></span> | <span data-ttu-id="8fc22-152">예제</span><span class="sxs-lookup"><span data-stu-id="8fc22-152">Example</span></span> | <span data-ttu-id="8fc22-153">설명</span><span class="sxs-lookup"><span data-stu-id="8fc22-153">Description</span></span>
|:--|:--|:--|
| <span data-ttu-id="8fc22-154">autoupdate *false\\</span><span class="sxs-lookup"><span data-stu-id="8fc22-154">autoupdate *false\\</span></span>|<span data-ttu-id="8fc22-155">true*</span><span class="sxs-lookup"><span data-stu-id="8fc22-155">true*</span></span> | <span data-ttu-id="8fc22-156">mycimprovauth autoupdate false</span><span class="sxs-lookup"><span data-stu-id="8fc22-156">mycimprovauth autoupdate false</span></span> | <span data-ttu-id="8fc22-157">다시 시작 또는 업데이트 시 인증 파일이 자동으로 업데이트될지 여부를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-157">Sets whether or not the authentication file will be automatically updated on restart or update.</span></span> |
| <span data-ttu-id="8fc22-158">default *bind-address username password*</span><span class="sxs-lookup"><span data-stu-id="8fc22-158">default *bind-address username password*</span></span> | <span data-ttu-id="8fc22-159">mycimprovauth default 127.0.0.1 root pwd</span><span class="sxs-lookup"><span data-stu-id="8fc22-159">mycimprovauth default 127.0.0.1 root pwd</span></span> | <span data-ttu-id="8fc22-160">MySQL OMI 인증 파일에서 기본 인스턴스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-160">Sets the default instance in the MySQL OMI authentication file.</span></span><br><span data-ttu-id="8fc22-161">암호 필드는 일반 텍스트로 입력되어야 하며 MySQL OMI 인증 파일의 암호는 Base 64로 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-161">The password field should be entered in plain text - the password in the MySQL OMI authentication file will be Base 64 encoded.</span></span> |
| <span data-ttu-id="8fc22-162">delete *default\\</span><span class="sxs-lookup"><span data-stu-id="8fc22-162">delete *default\\</span></span>|<span data-ttu-id="8fc22-163">port_num*</span><span class="sxs-lookup"><span data-stu-id="8fc22-163">port_num*</span></span> | <span data-ttu-id="8fc22-164">mycimprovauth 3308</span><span class="sxs-lookup"><span data-stu-id="8fc22-164">mycimprovauth 3308</span></span> | <span data-ttu-id="8fc22-165">기본값 또는 포트 번호로 지정된 인스턴스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-165">Deletes the specified instance by either default or by port number.</span></span> |
| <span data-ttu-id="8fc22-166">help</span><span class="sxs-lookup"><span data-stu-id="8fc22-166">help</span></span> | <span data-ttu-id="8fc22-167">mycimprov help</span><span class="sxs-lookup"><span data-stu-id="8fc22-167">mycimprov help</span></span> | <span data-ttu-id="8fc22-168">사용할 명령 목록을 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-168">Prints out a list of commands to use.</span></span> |
| <span data-ttu-id="8fc22-169">print</span><span class="sxs-lookup"><span data-stu-id="8fc22-169">print</span></span> | <span data-ttu-id="8fc22-170">mycimprov print</span><span class="sxs-lookup"><span data-stu-id="8fc22-170">mycimprov print</span></span> | <span data-ttu-id="8fc22-171">읽기 쉬운 MySQL OMI 인증 파일을 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-171">Prints out an easy to read MySQL OMI authentication file.</span></span> |
| <span data-ttu-id="8fc22-172">update port_num *bind-address username password*</span><span class="sxs-lookup"><span data-stu-id="8fc22-172">update port_num *bind-address username password*</span></span> | <span data-ttu-id="8fc22-173">mycimprov update 3307 127.0.0.1 root pwd</span><span class="sxs-lookup"><span data-stu-id="8fc22-173">mycimprov update 3307 127.0.0.1 root pwd</span></span> | <span data-ttu-id="8fc22-174">지정된 인스턴스를 업데이트하거나 존재하지 않는 경우 인스턴스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-174">Updates the specified instance or adds the instance if it does not exist.</span></span> |

<span data-ttu-id="8fc22-175">다음 예제 명령은 localhost에서 MySQL 서버의 기본 사용자 계정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-175">The following example commands define a default user account for the MySQL server on localhost.</span></span>  <span data-ttu-id="8fc22-176">암호 필드는 일반 텍스트로 입력되어야 하며 MySQL OMI 인증 파일의 암호는 Base 64로 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-176">The password field should be entered in plain text - the password in the MySQL OMI authentication file will be Base 64 encoded</span></span>

    sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>'
    sudo /opt/omi/bin/service_control restart

### <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="8fc22-177">MySQL 성능 카운터에 필요한 데이터베이스 권한</span><span class="sxs-lookup"><span data-stu-id="8fc22-177">Database Permissions Required for MySQL Performance Counters</span></span>
<span data-ttu-id="8fc22-178">MySQL 사용자는 MySQL 서버 성능 데이터를 수집하기 위해 다음 쿼리에 대한 액세스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-178">The MySQL User requires access to the following queries to collect MySQL Server performance data.</span></span> 

    SHOW GLOBAL STATUS;
    SHOW GLOBAL VARIABLES:


<span data-ttu-id="8fc22-179">또한 MySQL 사용자는 다음 기본 테이블에 대한 SELECT 액세스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-179">The MySQL user also requires SELECT access to the following default tables.</span></span>

- <span data-ttu-id="8fc22-180">information_schema</span><span class="sxs-lookup"><span data-stu-id="8fc22-180">information_schema</span></span>
- <span data-ttu-id="8fc22-181">mysql.</span><span class="sxs-lookup"><span data-stu-id="8fc22-181">mysql.</span></span> 

<span data-ttu-id="8fc22-182">이러한 권한은 다음과 같은 권한 부여 명령을 실행하여 부여될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-182">These privileges can be granted by running the following grant commands.</span></span>

    GRANT SELECT ON information_schema.* TO ‘monuser’@’localhost’;
    GRANT SELECT ON mysql.* TO ‘monuser’@’localhost’;


> [!NOTE]
> <span data-ttu-id="8fc22-183">MySQL 모니터링 사용자에게 권한을 부여하려면, 권한을 부여하는 사용자에게 'GRANT option' 권한은 물론 부여되는 권한에 대한 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-183">To grant permissions to a MySQL monitoring user the granting user must have the ‘GRANT option’ privilege as well as the privilege being granted.</span></span>

### <a name="define-performance-counters"></a><span data-ttu-id="8fc22-184">성능 카운터 정의</span><span class="sxs-lookup"><span data-stu-id="8fc22-184">Define performance counters</span></span>

<span data-ttu-id="8fc22-185">Log Analytics에 데이터를 보내도록 Linux용 OMS 에이전트를 구성한 후 수집할 성능 카운터를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-185">Once you configure the OMS Agent for Linux to send data to Log Analytics, you must configure the performance counters to collect.</span></span>  <span data-ttu-id="8fc22-186">다음 테이블의 카운터와 함께 [Log Analytics의 Windows 및 Linux 성능 데이터 원본](log-analytics-data-sources-windows-events.md)의 절차를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-186">Use the procedure in [Windows and Linux performance data sources in Log Analytics](log-analytics-data-sources-windows-events.md) with the counters in the following table.</span></span>

| <span data-ttu-id="8fc22-187">개체 이름</span><span class="sxs-lookup"><span data-stu-id="8fc22-187">Object Name</span></span> | <span data-ttu-id="8fc22-188">카운터 이름</span><span class="sxs-lookup"><span data-stu-id="8fc22-188">Counter Name</span></span> |
|:--|:--|
| <span data-ttu-id="8fc22-189">MySQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="8fc22-189">MySQL Database</span></span> | <span data-ttu-id="8fc22-190">디스크 공간(바이트)</span><span class="sxs-lookup"><span data-stu-id="8fc22-190">Disk Space in Bytes</span></span> |
| <span data-ttu-id="8fc22-191">MySQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="8fc22-191">MySQL Database</span></span> | <span data-ttu-id="8fc22-192">테이블</span><span class="sxs-lookup"><span data-stu-id="8fc22-192">Tables</span></span> |
| <span data-ttu-id="8fc22-193">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="8fc22-193">MySQL Server</span></span> | <span data-ttu-id="8fc22-194">중단된 연결 Pct</span><span class="sxs-lookup"><span data-stu-id="8fc22-194">Aborted Connection Pct</span></span> |
| <span data-ttu-id="8fc22-195">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="8fc22-195">MySQL Server</span></span> | <span data-ttu-id="8fc22-196">연결 사용 Pct</span><span class="sxs-lookup"><span data-stu-id="8fc22-196">Connection Use Pct</span></span> |
| <span data-ttu-id="8fc22-197">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="8fc22-197">MySQL Server</span></span> | <span data-ttu-id="8fc22-198">디스크 공간 사용(바이트)</span><span class="sxs-lookup"><span data-stu-id="8fc22-198">Disk Space Use in Bytes</span></span> |
| <span data-ttu-id="8fc22-199">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="8fc22-199">MySQL Server</span></span> | <span data-ttu-id="8fc22-200">전체 테이블 검색 Pct</span><span class="sxs-lookup"><span data-stu-id="8fc22-200">Full Table Scan Pct</span></span> |
| <span data-ttu-id="8fc22-201">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="8fc22-201">MySQL Server</span></span> | <span data-ttu-id="8fc22-202">InnoDB 버퍼 풀 적중 Pct</span><span class="sxs-lookup"><span data-stu-id="8fc22-202">InnoDB Buffer Pool Hit Pct</span></span> |
| <span data-ttu-id="8fc22-203">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="8fc22-203">MySQL Server</span></span> | <span data-ttu-id="8fc22-204">InnoDB 버퍼 풀 사용 Pct</span><span class="sxs-lookup"><span data-stu-id="8fc22-204">InnoDB Buffer Pool Use Pct</span></span> |
| <span data-ttu-id="8fc22-205">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="8fc22-205">MySQL Server</span></span> | <span data-ttu-id="8fc22-206">InnoDB 버퍼 풀 사용 Pct</span><span class="sxs-lookup"><span data-stu-id="8fc22-206">InnoDB Buffer Pool Use Pct</span></span> |
| <span data-ttu-id="8fc22-207">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="8fc22-207">MySQL Server</span></span> | <span data-ttu-id="8fc22-208">키 캐시 적중 Pct</span><span class="sxs-lookup"><span data-stu-id="8fc22-208">Key Cache Hit Pct</span></span> |
| <span data-ttu-id="8fc22-209">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="8fc22-209">MySQL Server</span></span> | <span data-ttu-id="8fc22-210">키 캐시 사용 Pct</span><span class="sxs-lookup"><span data-stu-id="8fc22-210">Key Cache Use Pct</span></span> |
| <span data-ttu-id="8fc22-211">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="8fc22-211">MySQL Server</span></span> | <span data-ttu-id="8fc22-212">키 캐시 쓰기 Pct</span><span class="sxs-lookup"><span data-stu-id="8fc22-212">Key Cache Write Pct</span></span> |
| <span data-ttu-id="8fc22-213">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="8fc22-213">MySQL Server</span></span> | <span data-ttu-id="8fc22-214">쿼리 캐시 적중 Pct</span><span class="sxs-lookup"><span data-stu-id="8fc22-214">Query Cache Hit Pct</span></span> |
| <span data-ttu-id="8fc22-215">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="8fc22-215">MySQL Server</span></span> | <span data-ttu-id="8fc22-216">쿼리 캐시 잘라내기 Pct</span><span class="sxs-lookup"><span data-stu-id="8fc22-216">Query Cache Prunes Pct</span></span> |
| <span data-ttu-id="8fc22-217">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="8fc22-217">MySQL Server</span></span> | <span data-ttu-id="8fc22-218">쿼리 캐시 사용 Pct</span><span class="sxs-lookup"><span data-stu-id="8fc22-218">Query Cache Use Pct</span></span> |
| <span data-ttu-id="8fc22-219">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="8fc22-219">MySQL Server</span></span> | <span data-ttu-id="8fc22-220">테이블 캐시 적중 Pct</span><span class="sxs-lookup"><span data-stu-id="8fc22-220">Table Cache Hit Pct</span></span> |
| <span data-ttu-id="8fc22-221">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="8fc22-221">MySQL Server</span></span> | <span data-ttu-id="8fc22-222">테이블 캐시 사용 Pct</span><span class="sxs-lookup"><span data-stu-id="8fc22-222">Table Cache Use Pct</span></span> |
| <span data-ttu-id="8fc22-223">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="8fc22-223">MySQL Server</span></span> | <span data-ttu-id="8fc22-224">테이블 잠금 경합 Pct</span><span class="sxs-lookup"><span data-stu-id="8fc22-224">Table Lock Contention Pct</span></span> |

## <a name="apache-http-server"></a><span data-ttu-id="8fc22-225">Apache HTTP 서버</span><span class="sxs-lookup"><span data-stu-id="8fc22-225">Apache HTTP Server</span></span> 
<span data-ttu-id="8fc22-226">omsagent 번들이 설치된 경우 컴퓨터에서 Apache HTTP 서버가 감지되면, Apache HTTP 서버용 성능 모니터링 공급자가 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-226">If Apache HTTP Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server will be automatically installed.</span></span> <span data-ttu-id="8fc22-227">이 공급자는 성능 데이터에 액세스하기 위해 Apache HTTP 서버에 로드되어야 하는 Apache 모듈에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-227">This provider relies on an Apache module that must be loaded into the Apache HTTP Server in order to access performance data.</span></span> <span data-ttu-id="8fc22-228">모듈은 다음 명령을 사용하여 로드될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-228">The module can be loaded with the following command:</span></span>
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="8fc22-229">Apache 모니터링 모듈을 언로드하려면, 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-229">To unload the Apache monitoring module, run the following command:</span></span>
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```

### <a name="define-performance-counters"></a><span data-ttu-id="8fc22-230">성능 카운터 정의</span><span class="sxs-lookup"><span data-stu-id="8fc22-230">Define performance counters</span></span>

<span data-ttu-id="8fc22-231">Log Analytics에 데이터를 보내도록 Linux용 OMS 에이전트를 구성한 후 수집할 성능 카운터를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-231">Once you configure the OMS Agent for Linux to send data to Log Analytics, you must configure the performance counters to collect.</span></span>  <span data-ttu-id="8fc22-232">다음 테이블의 카운터와 함께 [Log Analytics의 Windows 및 Linux 성능 데이터 원본](log-analytics-data-sources-windows-events.md)의 절차를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-232">Use the procedure in [Windows and Linux performance data sources in Log Analytics](log-analytics-data-sources-windows-events.md) with the counters in the following table.</span></span>

| <span data-ttu-id="8fc22-233">개체 이름</span><span class="sxs-lookup"><span data-stu-id="8fc22-233">Object Name</span></span> | <span data-ttu-id="8fc22-234">카운터 이름</span><span class="sxs-lookup"><span data-stu-id="8fc22-234">Counter Name</span></span> |
|:--|:--|
| <span data-ttu-id="8fc22-235">Apache HTTP 서버</span><span class="sxs-lookup"><span data-stu-id="8fc22-235">Apache HTTP Server</span></span> | <span data-ttu-id="8fc22-236">근무 중인 작업자</span><span class="sxs-lookup"><span data-stu-id="8fc22-236">Busy Workers</span></span> |
| <span data-ttu-id="8fc22-237">Apache HTTP 서버</span><span class="sxs-lookup"><span data-stu-id="8fc22-237">Apache HTTP Server</span></span> | <span data-ttu-id="8fc22-238">유휴 작업자</span><span class="sxs-lookup"><span data-stu-id="8fc22-238">Idle Workers</span></span> |
| <span data-ttu-id="8fc22-239">Apache HTTP 서버</span><span class="sxs-lookup"><span data-stu-id="8fc22-239">Apache HTTP Server</span></span> | <span data-ttu-id="8fc22-240">Pct 근무 중인 작업자</span><span class="sxs-lookup"><span data-stu-id="8fc22-240">Pct Busy Workers</span></span> |
| <span data-ttu-id="8fc22-241">Apache HTTP 서버</span><span class="sxs-lookup"><span data-stu-id="8fc22-241">Apache HTTP Server</span></span> | <span data-ttu-id="8fc22-242">총 Pct CPU</span><span class="sxs-lookup"><span data-stu-id="8fc22-242">Total Pct CPU</span></span> |
| <span data-ttu-id="8fc22-243">Apache 가상 호스트</span><span class="sxs-lookup"><span data-stu-id="8fc22-243">Apache Virtual Host</span></span> | <span data-ttu-id="8fc22-244">분당 오류 - 클라이언트</span><span class="sxs-lookup"><span data-stu-id="8fc22-244">Errors per Minute - Client</span></span> |
| <span data-ttu-id="8fc22-245">Apache 가상 호스트</span><span class="sxs-lookup"><span data-stu-id="8fc22-245">Apache Virtual Host</span></span> | <span data-ttu-id="8fc22-246">분당 오류 - 서버</span><span class="sxs-lookup"><span data-stu-id="8fc22-246">Errors per Minute - Server</span></span> |
| <span data-ttu-id="8fc22-247">Apache 가상 호스트</span><span class="sxs-lookup"><span data-stu-id="8fc22-247">Apache Virtual Host</span></span> | <span data-ttu-id="8fc22-248">요청당 KB</span><span class="sxs-lookup"><span data-stu-id="8fc22-248">KB per Request</span></span> |
| <span data-ttu-id="8fc22-249">Apache 가상 호스트</span><span class="sxs-lookup"><span data-stu-id="8fc22-249">Apache Virtual Host</span></span> | <span data-ttu-id="8fc22-250">초당 요청 KB</span><span class="sxs-lookup"><span data-stu-id="8fc22-250">Requests KB per Second</span></span> |
| <span data-ttu-id="8fc22-251">Apache 가상 호스트</span><span class="sxs-lookup"><span data-stu-id="8fc22-251">Apache Virtual Host</span></span> | <span data-ttu-id="8fc22-252">초당 요청</span><span class="sxs-lookup"><span data-stu-id="8fc22-252">Requests per Second</span></span> |



## <a name="next-steps"></a><span data-ttu-id="8fc22-253">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8fc22-253">Next steps</span></span>
* <span data-ttu-id="8fc22-254">Linux 에이전트에서 [성능 카운터를 수집합니다](log-analytics-data-sources-performance-counters.md).</span><span class="sxs-lookup"><span data-stu-id="8fc22-254">[Collect performance counters](log-analytics-data-sources-performance-counters.md) from Linux agents.</span></span>
* <span data-ttu-id="8fc22-255">데이터 원본 및 솔루션에서 수집한 데이터를 분석하기 위해 [로그 검색](log-analytics-log-searches.md) 에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8fc22-255">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 