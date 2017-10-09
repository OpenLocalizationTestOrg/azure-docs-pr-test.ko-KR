---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: True
ROBOTS: NOINDEX
ms.openlocfilehash: 8b526144cd565f6750368e12970f008e66cc2023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toolog-analytics"></a><span data-ttu-id="97875-101">Linux 컴퓨터 tooLog 분석 연결</span><span class="sxs-lookup"><span data-stu-id="97875-101">Connect your Linux computers tooLog Analytics</span></span>
<span data-ttu-id="97875-102">Log Analytics를 사용하여 Linux 컴퓨터에서 생성되는 데이터를 수집하고 그에 따른 조치를 취할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-102">Using Log Analytics, you can collect and act on data generated from Linux computers.</span></span> <span data-ttu-id="97875-103">Linux tooOMS에서 수집 된 데이터를 추가 하면 toomanage Linux 시스템 및 컴퓨터의 위치에 상관 없이 Docker와 같은 컨테이너 솔루션-어디에서 나 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-103">Adding data collected from Linux tooOMS allows you toomanage Linux systems and container solutions like Docker, regardless of where your computers are located — virtually anywhere.</span></span> <span data-ttu-id="97875-104">데이터 원본 서비스 AWS (Amazon Web) 또는 Microsoft Azure 같은 클라우드 호스팅 서비스의 가상 컴퓨터 물리적 서버로 온-프레미스 데이터 센터에 있는 또는 책상 노트북에도 hello 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-104">Data sources might reside in your on-premises datacenter as physical servers, virtual computers in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure, or even hello laptop on your desk.</span></span> <span data-ttu-id="97875-105">뿐만 아니라 OMS는 Windows 컴퓨터에서도 유사하게 데이터를 수집하기 때문에 진정한 하이브리드 IT 환경을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-105">In addition, OMS also collects data from Windows computers similarly, so it supports a truly hybrid IT environment.</span></span>

<span data-ttu-id="97875-106">하나의 관리 포털을 통해 OMS의 Log Analytics에서 이 모든 소스의 데이터를 보고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-106">You can view and manage data from all of those sources with Log Analytics in OMS with a single management portal.</span></span> <span data-ttu-id="97875-107">Hello 필요성을 줄이고이 toomonitor 여러 시스템을 사용 하 여 사용 하면 쉽게 tooconsume 있으며 toowhatever 비즈니스 분석 솔루션이 나 시스템에 이미 있는 원하는 모든 데이터를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-107">This reduces hello need toomonitor it using many different systems, makes it easy tooconsume, and you can export any data you like toowhatever business analytics solution or system that you already have.</span></span>

<span data-ttu-id="97875-108">이 문서는 Linux 용 OMS 에이전트 hello를 사용 하 여 Linux 컴퓨터에 대 한 데이터 수집 및 관리 하는 데 도움이 되는 빠른 시작 가이드입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-108">This article is a quick start guide that will help you collect and manage data for your Linux computers using hello OMS Agent for Linux.</span></span> <span data-ttu-id="97875-109">프록시 서버 구성, CollectD 메트릭에 대한 정보, 사용자 지정 JSON 데이터 원본과 같은 자세한 기술 정보는 GitHub의 [Linux용 OMS 에이전트 개요](https://github.com/Microsoft/OMS-Agent-for-Linux)(영문) 및 [Linux용 OMS 에이전트 전체 설명서](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97875-109">For more technical details such as proxy server configuration, information about CollectD metrics, and custom JSON data sources, you’ll find that information at [OMS Agent for Linux overview](https://github.com/Microsoft/OMS-Agent-for-Linux) and [OMS Agent for Linux full documentation](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) on GitHub.</span></span>

<span data-ttu-id="97875-110">현재 Linux 컴퓨터에서 데이터 형식을 따르는 hello를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-110">Currently, you can collect hello following types of data from Linux computers:</span></span>

* <span data-ttu-id="97875-111">성능 메트릭</span><span class="sxs-lookup"><span data-stu-id="97875-111">Performance metrics</span></span>
* <span data-ttu-id="97875-112">Syslog 이벤트</span><span class="sxs-lookup"><span data-stu-id="97875-112">Syslog events</span></span>
* <span data-ttu-id="97875-113">Nagios 및 Zabbix의 경고</span><span class="sxs-lookup"><span data-stu-id="97875-113">Alerts from Nagios and Zabbix</span></span>
* <span data-ttu-id="97875-114">Docker 컨테이너 성능 메트릭, 인벤토리 및 로그</span><span class="sxs-lookup"><span data-stu-id="97875-114">Docker container performance metrics, inventory and logs</span></span>

## <a name="supported-linux-versions"></a><span data-ttu-id="97875-115">지원되는 Linux 버전</span><span class="sxs-lookup"><span data-stu-id="97875-115">Supported Linux versions</span></span>
<span data-ttu-id="97875-116">x86 및 x64 버전 모두 다양한 Linux 배포에 대해 공식적으로 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-116">Both x86 and x64 versions are officially supported on a variety of Linux distributions.</span></span> <span data-ttu-id="97875-117">그러나 Linux 용 OMS 에이전트 hello 나열 되지 않은 다른 배포 에서도 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-117">However, hello OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="97875-118">Amazon Linux 2012.09~2015.09</span><span class="sxs-lookup"><span data-stu-id="97875-118">Amazon Linux 2012.09 through 2015.09</span></span>
* <span data-ttu-id="97875-119">CentOS Linux 5, 6, 7</span><span class="sxs-lookup"><span data-stu-id="97875-119">CentOS Linux 5, 6, and 7</span></span>
* <span data-ttu-id="97875-120">Oracle Linux 5, 6, 7</span><span class="sxs-lookup"><span data-stu-id="97875-120">Oracle Linux 5, 6, and 7</span></span>
* <span data-ttu-id="97875-121">Red Hat Enterprise Linux Server 5, 6, 7</span><span class="sxs-lookup"><span data-stu-id="97875-121">Red Hat Enterprise Linux Server 5, 6 and 7</span></span>
* <span data-ttu-id="97875-122">Debian GNU/Linux 6, 7, 8</span><span class="sxs-lookup"><span data-stu-id="97875-122">Debian GNU/Linux 6, 7, and 8</span></span>
* <span data-ttu-id="97875-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span><span class="sxs-lookup"><span data-stu-id="97875-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span></span>
* <span data-ttu-id="97875-124">SUSE Linux Enterprise Server 11 및 12</span><span class="sxs-lookup"><span data-stu-id="97875-124">SUSE Linux Enterprise Server 11 and 12</span></span>

## <a name="oms-agent-for-linux"></a><span data-ttu-id="97875-125">Linux 용 OMS 에이전트</span><span class="sxs-lookup"><span data-stu-id="97875-125">OMS Agent for Linux</span></span>
<span data-ttu-id="97875-126">hello Linux 용 Operations Management Suite 에이전트는 여러 패키지로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-126">hello Operations Management Suite Agent for Linux comprises multiple packages.</span></span> <span data-ttu-id="97875-127">hello 릴리스 파일 hello 포함 되어 있는지와 함께 hello 셸 번들을 실행 하 여 사용할 수 있는 패키지를 다음 `--extract`합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-127">hello release file contains hello following packages, available by running hello shell bundle with `--extract`.</span></span>

| <span data-ttu-id="97875-128">**패키지**</span><span class="sxs-lookup"><span data-stu-id="97875-128">**Package**</span></span> | <span data-ttu-id="97875-129">**버전**</span><span class="sxs-lookup"><span data-stu-id="97875-129">**Version**</span></span> | <span data-ttu-id="97875-130">**설명**</span><span class="sxs-lookup"><span data-stu-id="97875-130">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="97875-131">omsagent</span><span class="sxs-lookup"><span data-stu-id="97875-131">omsagent</span></span> |<span data-ttu-id="97875-132">1.1.0</span><span class="sxs-lookup"><span data-stu-id="97875-132">1.1.0</span></span> |<span data-ttu-id="97875-133">hello Linux 용 Operations Management Suite 에이전트</span><span class="sxs-lookup"><span data-stu-id="97875-133">hello Operations Management Suite Agent for Linux</span></span> |
| <span data-ttu-id="97875-134">omsconfig</span><span class="sxs-lookup"><span data-stu-id="97875-134">omsconfig</span></span> |<span data-ttu-id="97875-135">1.1.1</span><span class="sxs-lookup"><span data-stu-id="97875-135">1.1.1</span></span> |<span data-ttu-id="97875-136">Hello OMS 에이전트에 대 한 구성 에이전트</span><span class="sxs-lookup"><span data-stu-id="97875-136">Configuration agent for hello OMS Agent</span></span> |
| <span data-ttu-id="97875-137">omi</span><span class="sxs-lookup"><span data-stu-id="97875-137">omi</span></span> |<span data-ttu-id="97875-138">1.0.8.3</span><span class="sxs-lookup"><span data-stu-id="97875-138">1.0.8.3</span></span> |<span data-ttu-id="97875-139">Open Management Infrastructure(OMI) -- 경량 CIM 서버</span><span class="sxs-lookup"><span data-stu-id="97875-139">Open Management Infrastructure (OMI) -- a lightweight CIM Server</span></span> |
| <span data-ttu-id="97875-140">scx</span><span class="sxs-lookup"><span data-stu-id="97875-140">scx</span></span> |<span data-ttu-id="97875-141">1.6.2</span><span class="sxs-lookup"><span data-stu-id="97875-141">1.6.2</span></span> |<span data-ttu-id="97875-142">운영 체제 성능 메트릭용 OMI CIM 공급자</span><span class="sxs-lookup"><span data-stu-id="97875-142">OMI CIM Providers for operating system performance metrics</span></span> |
| <span data-ttu-id="97875-143">apache-cimprov</span><span class="sxs-lookup"><span data-stu-id="97875-143">apache-cimprov</span></span> |<span data-ttu-id="97875-144">1.0.0</span><span class="sxs-lookup"><span data-stu-id="97875-144">1.0.0</span></span> |<span data-ttu-id="97875-145">OMI용 Apache HTTP 서버 성능 모니터링 공급자.</span><span class="sxs-lookup"><span data-stu-id="97875-145">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="97875-146">Apache HTTP 서버가 감지되는 경우에만 설치됨.</span><span class="sxs-lookup"><span data-stu-id="97875-146">Only installed if Apache HTTP Server is detected.</span></span> |
| <span data-ttu-id="97875-147">mysql-cimprov</span><span class="sxs-lookup"><span data-stu-id="97875-147">mysql-cimprov</span></span> |<span data-ttu-id="97875-148">1.0.0</span><span class="sxs-lookup"><span data-stu-id="97875-148">1.0.0</span></span> |<span data-ttu-id="97875-149">OMI용 MySQL 서버 성능 모니터링 공급자.</span><span class="sxs-lookup"><span data-stu-id="97875-149">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="97875-150">MySQL/MariaDB 서버가 감지되는 경우에만 설치됨.</span><span class="sxs-lookup"><span data-stu-id="97875-150">Only installed if MySQL/MariaDB server is detected.</span></span> |
| <span data-ttu-id="97875-151">docker-cimprov</span><span class="sxs-lookup"><span data-stu-id="97875-151">docker-cimprov</span></span> |<span data-ttu-id="97875-152">0.1.0</span><span class="sxs-lookup"><span data-stu-id="97875-152">0.1.0</span></span> |<span data-ttu-id="97875-153">OMI용 Docker 공급자.</span><span class="sxs-lookup"><span data-stu-id="97875-153">Docker provider for OMI.</span></span> <span data-ttu-id="97875-154">Docker가 감지되는 경우에만 설치됨.</span><span class="sxs-lookup"><span data-stu-id="97875-154">Only installed if Docker is detected.</span></span> |

### <a name="additional-installation-artifacts"></a><span data-ttu-id="97875-155">추가적인 설치 아티팩트</span><span class="sxs-lookup"><span data-stu-id="97875-155">Additional installation artifacts</span></span>
<span data-ttu-id="97875-156">Linux 패키지에 대 한 hello OMS 에이전트를 설치한 후 hello 다음과 같은 추가 시스템 차원 구성 변경 내용이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-156">After installing hello OMS agent for Linux packages, hello following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="97875-157">이러한 아티팩트는 omsagent 패키지 hello 때 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-157">These artifacts are removed when hello omsagent package is uninstalled.</span></span>

* <span data-ttu-id="97875-158">`omsagent` 라는 이름의 권한 없는 사용자가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-158">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="97875-159">이 hello 계정을 hello omsagent 디먼이 실행으로</span><span class="sxs-lookup"><span data-stu-id="97875-159">This is hello account hello omsagent daemon runs as</span></span>
* <span data-ttu-id="97875-160">Sudoers "include" 파일이 만들어집니다 /etc/sudoers.d/omsagent에 권한을 부여 omsagent toorestart hello syslog 및 omsagent 디먼을 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-160">A sudoers “include” file is created at /etc/sudoers.d/omsagent This authorizes omsagent toorestart hello syslog and omsagent daemons.</span></span> <span data-ttu-id="97875-161">Sudo "include" 지시문은 hello 설치 된 버전의 sudo에서 지원 되지 않는, 너무/등/sudoers 이러한 항목이 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-161">If sudo “include” directives are not supported in hello installed version of sudo, these entries will be written too/etc/sudoers.</span></span>
* <span data-ttu-id="97875-162">hello syslog 구성이 수정 된 tooforward 이벤트 toohello 에이전트의 하위 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-162">hello syslog configuration is modified tooforward a subset of events toohello agent.</span></span> <span data-ttu-id="97875-163">자세한 내용은 참조 hello **데이터 수집 구성** 아래 섹션</span><span class="sxs-lookup"><span data-stu-id="97875-163">For more information, see hello **Configuring Data Collection** section below</span></span>

### <a name="linux-data-collection-details"></a><span data-ttu-id="97875-164">Linux 데이터 수집 세부 정보</span><span class="sxs-lookup"><span data-stu-id="97875-164">Linux data collection details</span></span>
<span data-ttu-id="97875-165">hello 다음 표에서 데이터 수집 방법과 데이터가 수집 되는 방법에 대 한 기타 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-165">hello following table shows data collection methods and other details about how data is collected.</span></span>

| <span data-ttu-id="97875-166">원본</span><span class="sxs-lookup"><span data-stu-id="97875-166">source</span></span> | <span data-ttu-id="97875-167">직접 에이전트</span><span class="sxs-lookup"><span data-stu-id="97875-167">Direct Agent</span></span> | <span data-ttu-id="97875-168">SCOM 에이전트</span><span class="sxs-lookup"><span data-stu-id="97875-168">SCOM agent</span></span> | <span data-ttu-id="97875-169">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="97875-169">Azure Storage</span></span> | <span data-ttu-id="97875-170">SCOM 필요?</span><span class="sxs-lookup"><span data-stu-id="97875-170">SCOM required?</span></span> | <span data-ttu-id="97875-171">관리 그룹을 통해 전송되는 SCOM 에이전트 데이터</span><span class="sxs-lookup"><span data-stu-id="97875-171">SCOM agent data sent via management group</span></span> | <span data-ttu-id="97875-172">수집 빈도</span><span class="sxs-lookup"><span data-stu-id="97875-172">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="97875-173">Zabbix</span><span class="sxs-lookup"><span data-stu-id="97875-173">Zabbix</span></span> |![예](./media/log-analytics-linux-agents/oms-bullet-green.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="97875-179">1분</span><span class="sxs-lookup"><span data-stu-id="97875-179">1 minute</span></span> |
| <span data-ttu-id="97875-180">Nagios</span><span class="sxs-lookup"><span data-stu-id="97875-180">Nagios</span></span> |![예](./media/log-analytics-linux-agents/oms-bullet-green.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="97875-186">도착 시</span><span class="sxs-lookup"><span data-stu-id="97875-186">on arrival</span></span> |
| <span data-ttu-id="97875-187">syslog</span><span class="sxs-lookup"><span data-stu-id="97875-187">syslog</span></span> |![예](./media/log-analytics-linux-agents/oms-bullet-green.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="97875-193">Azure 저장소: 10분, 에이전트: 도착 시</span><span class="sxs-lookup"><span data-stu-id="97875-193">from Azure storage: 10 minutes; from agent: on arrival</span></span> |
| <span data-ttu-id="97875-194">Linux 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="97875-194">Linux performance counters</span></span> |![예](./media/log-analytics-linux-agents/oms-bullet-green.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="97875-200">예약된 대로, 최소 10초</span><span class="sxs-lookup"><span data-stu-id="97875-200">As scheduled, minimum of 10 seconds</span></span> |
| <span data-ttu-id="97875-201">변경 내용 추적</span><span class="sxs-lookup"><span data-stu-id="97875-201">change tracking</span></span> |![예](./media/log-analytics-linux-agents/oms-bullet-green.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="97875-207">매시간</span><span class="sxs-lookup"><span data-stu-id="97875-207">hourly</span></span> |

### <a name="package-requirements"></a><span data-ttu-id="97875-208">패키지 요구 사항</span><span class="sxs-lookup"><span data-stu-id="97875-208">Package Requirements</span></span>
| <span data-ttu-id="97875-209">**필수 패키지**</span><span class="sxs-lookup"><span data-stu-id="97875-209">**Required package**</span></span> | <span data-ttu-id="97875-210">**설명**</span><span class="sxs-lookup"><span data-stu-id="97875-210">**Description**</span></span> | <span data-ttu-id="97875-211">**최소 버전**</span><span class="sxs-lookup"><span data-stu-id="97875-211">**Minimum version**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="97875-212">Glibc</span><span class="sxs-lookup"><span data-stu-id="97875-212">Glibc</span></span> |<span data-ttu-id="97875-213">GNU C 라이브러리</span><span class="sxs-lookup"><span data-stu-id="97875-213">GNU C library</span></span> |<span data-ttu-id="97875-214">2.5-12</span><span class="sxs-lookup"><span data-stu-id="97875-214">2.5-12</span></span> |
| <span data-ttu-id="97875-215">Openssl</span><span class="sxs-lookup"><span data-stu-id="97875-215">Openssl</span></span> |<span data-ttu-id="97875-216">OpenSSL 라이브러리</span><span class="sxs-lookup"><span data-stu-id="97875-216">OpenSSL libraries</span></span> |<span data-ttu-id="97875-217">0.9.8e 또는 1.0</span><span class="sxs-lookup"><span data-stu-id="97875-217">0.9.8e or 1.0</span></span> |
| <span data-ttu-id="97875-218">Curl</span><span class="sxs-lookup"><span data-stu-id="97875-218">Curl</span></span> |<span data-ttu-id="97875-219">cURL 웹 클라이언트</span><span class="sxs-lookup"><span data-stu-id="97875-219">cURL web client</span></span> |<span data-ttu-id="97875-220">7.15.5</span><span class="sxs-lookup"><span data-stu-id="97875-220">7.15.5</span></span> |
| <span data-ttu-id="97875-221">Python-ctypes</span><span class="sxs-lookup"><span data-stu-id="97875-221">Python-ctypes</span></span> |<span data-ttu-id="97875-222">함수 라이브러리</span><span class="sxs-lookup"><span data-stu-id="97875-222">function libraries</span></span> |<span data-ttu-id="97875-223">해당 없음</span><span class="sxs-lookup"><span data-stu-id="97875-223">n/a</span></span> |
| <span data-ttu-id="97875-224">PAM</span><span class="sxs-lookup"><span data-stu-id="97875-224">PAM</span></span> |<span data-ttu-id="97875-225">플러그형 인증 모듈</span><span class="sxs-lookup"><span data-stu-id="97875-225">Pluggable authentication Modules</span></span> |<span data-ttu-id="97875-226">해당 없음</span><span class="sxs-lookup"><span data-stu-id="97875-226">n/a</span></span> |

> [!NOTE]
> <span data-ttu-id="97875-227">Rsyslog 또는 syslog-ng 중 하나는 필수 toocollect syslog 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-227">Either rsyslog or syslog-ng are required toocollect syslog messages.</span></span> <span data-ttu-id="97875-228">Red Hat Enterprise Linux, CentOS 및 Oracle Linux 버전 (sysklog)의 버전 5에 hello 기본 syslog 디먼은 syslog 이벤트 수집이 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-228">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="97875-229">이 버전의,이 배포에서 syslog 데이터 toocollect hello rsyslog 디먼을 설치 해야 하며 tooreplace sysklog를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-229">toocollect syslog data from this version of these distributions, hello rsyslog daemon should be installed and configured tooreplace sysklog.</span></span>
>
>

## <a name="quick-install"></a><span data-ttu-id="97875-230">빠른 설치</span><span class="sxs-lookup"><span data-stu-id="97875-230">Quick install</span></span>
<span data-ttu-id="97875-231">다음 명령을 toodownload hello omsagent hello 실행, hello 체크섬 다음 설치 및 등록 hello 에이전트의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-231">Run hello following commands toodownload hello omsagent, validate hello checksum, then  install and onboard hello agent.</span></span> <span data-ttu-id="97875-232">명령은 64비트용입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-232">Commands are for 64-bit.</span></span> <span data-ttu-id="97875-233">hello 작업 영역 ID와 기본 키에서에서 발견 되 hello OMS 포털에서 **설정** hello에 **연결 된 원본** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-233">hello Workspace ID and Primary Key are found in hello OMS portal under **Settings** on hello **Connected Sources** tab.</span></span>

![작업 영역 정보](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

<span data-ttu-id="97875-235">다양 한 다른 메서드 tooinstall 에이전트 hello을 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-235">There are a variety of other methods tooinstall hello agent and upgrade it.</span></span> <span data-ttu-id="97875-236">자세한 내용은 [단계 tooinstall hello Linux 용 OMS 에이전트](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux)합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-236">You can read more about them at [Steps tooinstall hello OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span></span>

<span data-ttu-id="97875-237">Hello를 볼 수도 있습니다 [Azure 동영상 연습](https://www.youtube.com/watch?v=mF1wtHPEzT0)합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-237">You can also view hello [Azure video walkthrough](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span></span>

## <a name="choose-your-linux-data-collection-method"></a><span data-ttu-id="97875-238">Linux 데이터 수집 방법 선택</span><span class="sxs-lookup"><span data-stu-id="97875-238">Choose your Linux data collection method</span></span>
<span data-ttu-id="97875-239">어떻게 hello toocollect toouse hello OMS 포털을 사용할 것인지에 따라 다릅니다. like 또는 Linux 클라이언트에서 직접 다양 한 구성 파일을 편집 하려는 경우에 데이터 유형을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-239">How you choose hello data types you'd like toocollect depends on whether you want toouse hello OMS portal or if you want edit various configuration files directly on your Linux clients.</span></span> <span data-ttu-id="97875-240">Toouse hello 포털을 선택 하면 hello 구성이 tooall Linux 클라이언트를 자동으로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-240">If you choose toouse hello portal, hello configuration is sent tooall of your Linux clients automatically.</span></span> <span data-ttu-id="97875-241">Linux 클라이언트 마다 다른 구성 해야 할 경우 tooedit 클라이언트 파일을 개별적으로 필요 하거나 PowerShell DSC, Chef 또는 puppet과 같은 대안을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-241">If you need different configurations for different Linux clients, you will need tooedit client files individually – or use an alternative like PowerShell DSC, Chef, or Puppet.</span></span>

<span data-ttu-id="97875-242">Hello syslog 이벤트를 지정할 수 있습니다 및 toocollect hello Linux 컴퓨터의 구성 파일을 사용 하 여 원하는 성능 카운터입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-242">You can specify hello syslog events and performance counters that you want toocollect using configuration files on hello Linux computers.</span></span> <span data-ttu-id="97875-243">*에이전트 구성 파일을 편집 하 여 tooconfigure 데이터 컬렉션을 선택한 경우 hello 중앙 집중식된 구성을 비활성화 해야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="97875-243">*If you chose tooconfigure data collection by editing agent configuration files, you should disable hello centralized configuration.*</span></span>  <span data-ttu-id="97875-244">Hello 에이전트의 구성 파일 뿐만 아니라 Linux 또는 개별 컴퓨터에 대 한 모든 OMS 에이전트에 대 한 toodisable 중앙 구성에서 데이터 수집 tooconfigure 아래 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-244">Instructions are provided below tooconfigure data collection in hello agent's configuration files as well as toodisable central configuration for all OMS Agents for Linux, or individual computers.</span></span>

### <a name="disable-oms-management-for-an-individual-linux-computer"></a><span data-ttu-id="97875-245">개별 Linux 컴퓨터에 대한 OMS 관리 비활성화</span><span class="sxs-lookup"><span data-stu-id="97875-245">Disable OMS management for an individual Linux computer</span></span>
<span data-ttu-id="97875-246">OMS_MetaConfigHelper.py 스크립트 hello 하 여 개별 Linux 컴퓨터에 대 한 구성 데이터에 대 한 중앙 집중식된 데이터 수집 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-246">Centralized data collection for configuration data is disabled for an individual Linux computer with hello OMS_MetaConfigHelper.py script.</span></span> <span data-ttu-id="97875-247">이것은 컴퓨터 하위 집합에 특별한 구성이 필요한 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-247">This can be useful if a subset of computers should have a specialized configuration.</span></span>

<span data-ttu-id="97875-248">toodisable 중앙 집중식된 구성:</span><span class="sxs-lookup"><span data-stu-id="97875-248">toodisable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

<span data-ttu-id="97875-249">중앙 집중식된 구성 toore 사용:</span><span class="sxs-lookup"><span data-stu-id="97875-249">toore-enable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a><span data-ttu-id="97875-250">Linux 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="97875-250">Linux performance counters</span></span>
<span data-ttu-id="97875-251">Linux 성능 카운터는 비슷한 tooWindows 성능 카운터를 둘 다 동일 하 게 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-251">Linux performance counters are similar tooWindows performance counters—both operate similarly.</span></span> <span data-ttu-id="97875-252">프로시저 tooadd 다음 hello를 사용 하 고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-252">You can use hello following procedures tooadd and configure them.</span></span> <span data-ttu-id="97875-253">TooOMS, 추가 된 후 데이터 30 초 마다에 수집 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-253">After they are added tooOMS, data is collected for them every 30 seconds.</span></span>

### <a name="tooadd-a-linux-performance-counter-in-oms"></a><span data-ttu-id="97875-254">tooadd OMS에서 Linux 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="97875-254">tooadd a Linux performance counter in OMS</span></span>
1. <span data-ttu-id="97875-255">hello OMS 포털을 사용 하 여 Linux 용 OMS 에이전트 tooconfigure Linux 성능 카운터를 추가할 수 있습니다 hello 설정 페이지에서 클릭 **데이터**합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-255">tooconfigure OMS Agents for Linux using hello OMS portal, you can add Linux performance counters on hello Settings page, click **Data**.</span></span>  
2. <span data-ttu-id="97875-256">Hello에 **설정** 페이지 **데이터** , 클릭 **Linux 성능 카운터** 이름과 다음 선택 또는 입력 hello tooadd hello 카운터의 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-256">On hello **Settings** page under **Data** , click **Linux performance counters** and then select or type hello name of hello counter you want tooadd.</span></span>  
    <span data-ttu-id="97875-257">![데이터](./media/log-analytics-linux-agents/oms-settings-data01.png)</span><span class="sxs-lookup"><span data-stu-id="97875-257">![data](./media/log-analytics-linux-agents/oms-settings-data01.png)</span></span>
3. <span data-ttu-id="97875-258">Hello 카운터의 전체 이름을 hello를 모르는 경우 이름의 일부를 입력을 시작할 수 있습니다 하 고 사용 가능한 카운터 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-258">If you don't know hello full name of hello counter, you can start typing a partial name and a list of available counters will appear.</span></span> <span data-ttu-id="97875-259">Tooadd 원하는 하 hello 목록에 hello 이름을 클릭 한 다음 hello 플러스 tooadd hello 아이콘을 클릭 하 hello 카운터를 찾을 때 카운터입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-259">When you find hello counter you want tooadd, click hello name in hello list and then click hello plus icon tooadd hello counter.</span></span>
4. <span data-ttu-id="97875-260">Hello 카운터를 추가한 후 색 막대로 강조 표시 하는 카운터의 hello 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="97875-260">After you add hello counter, it appears in hello list of counters highlighted with a colored bar.</span></span>
5. <span data-ttu-id="97875-261">기본적으로 hello **구성 toomy 컴퓨터 아래 적용** 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-261">By default, hello **Apply below configuration toomy machines** option is selected.</span></span> <span data-ttu-id="97875-262">구성 데이터를 보내는 toodisable 원한다 면 hello 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-262">If you want toodisable sending configuration data, clear hello selection.</span></span>
6. <span data-ttu-id="97875-263">클릭 하 여 hello hello 페이지 맨 아래에 성능 카운터 수정을 마쳤으면 **저장** toofinalize 변경 내용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-263">When you are done modifying performance counters, at hello bottom of hello page click **Save** toofinalize your changes.</span></span> <span data-ttu-id="97875-264">일반적으로 5 분 이내에 등록 된 OMS에 Linux 용 hello 구성 변경 내용 아 tooall hello OMS 에이전트로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-264">hello configuration changes that you've made are then sent tooall hello OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-performance-counters-in-oms"></a><span data-ttu-id="97875-265">OMS에서 Linux 성능 카운터 구성</span><span class="sxs-lookup"><span data-stu-id="97875-265">Configure Linux performance counters in OMS</span></span>
<span data-ttu-id="97875-266">Windows 성능 카운터의 경우, 각 성능 카운터에 대해 특정 인스턴스를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-266">For Windows performance counters, you can choose a specific instance for each performance counter.</span></span> <span data-ttu-id="97875-267">그러나 Linux 성능 카운터에 대 한 사용자가 선택한 카운터의 카운터 인스턴스가 hello 부모 카운터의 tooall 자식 카운터를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-267">However, for Linux performance counters, whatever instance of a counter that you choose applies tooall child counters of hello parent counter.</span></span> <span data-ttu-id="97875-268">hello 다음 표에서 hello 공용 인스턴스 사용 가능한 tooboth Linux 맟 Windows 성능 카운터입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-268">hello following table shows hello common instances available tooboth Linux and Windows performance counters.</span></span>

| <span data-ttu-id="97875-269">**인스턴스 이름**</span><span class="sxs-lookup"><span data-stu-id="97875-269">**Instance name**</span></span> | <span data-ttu-id="97875-270">**의미**</span><span class="sxs-lookup"><span data-stu-id="97875-270">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="97875-271">\_합계</span><span class="sxs-lookup"><span data-stu-id="97875-271">\_Total</span></span> |<span data-ttu-id="97875-272">모든 hello 인스턴스</span><span class="sxs-lookup"><span data-stu-id="97875-272">Total of all hello instances</span></span> |
| \* |<span data-ttu-id="97875-273">모든 인스턴스</span><span class="sxs-lookup"><span data-stu-id="97875-273">All instances</span></span> |
| <span data-ttu-id="97875-274">(/&#124;/var)</span><span class="sxs-lookup"><span data-stu-id="97875-274">(/&#124;/var)</span></span> |<span data-ttu-id="97875-275">/ 또는 /var로 명명된 인스턴트와 일치</span><span class="sxs-lookup"><span data-stu-id="97875-275">Matches instances named: / or /var</span></span> |

<span data-ttu-id="97875-276">마찬가지로, 부모 카운터에 대 한 사용자가 선택한 hello 샘플 간격 자식 카운터 tooall를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-276">Similarly, hello sample interval that you choose for a parent counter applies tooall its child counters.</span></span> <span data-ttu-id="97875-277">즉, 모든 hello 자식 카운터의 샘플 간격과 인스턴스가 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-277">In other words, all hello child counter sample intervals and instances are tied together.</span></span>

### <a name="add-and-configure-performance-metrics-with-linux"></a><span data-ttu-id="97875-278">Linux에서 성능 메트릭 추가 및 구성</span><span class="sxs-lookup"><span data-stu-id="97875-278">Add and configure performance metrics with Linux</span></span>
<span data-ttu-id="97875-279">성능 메트릭 toocollect/등/옵트인/microsoft/omsagent hello 구성에 의해 제어 됩니다/&lt;작업 영역 id&gt;/conf/omsagent.conf 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-279">Performance metrics toocollect are controlled by hello configuration in /etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf.</span></span> <span data-ttu-id="97875-280">참조 [사용 가능한 성능 메트릭](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) hello Linux 용 OMS 에이전트에 대 한 메트릭 및 사용 가능한 클래스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-280">See [Available performance metrics](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) for available classes and metrics for hello OMS Agent for Linux.</span></span>

<span data-ttu-id="97875-281">각 개체 또는 성능 메트릭 toocollect의 범주는 단일 hello 구성 파일에 정의 되어야 합니다 `<source>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-281">Each object, or category, of performance metrics toocollect should be defined in hello configuration file as a single `<source>` element.</span></span> <span data-ttu-id="97875-282">hello 구문 아래 hello 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="97875-282">hello syntax follows hello pattern below.</span></span>

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

<span data-ttu-id="97875-283">이 요소의 hello 구성 가능한 매개 변수는.</span><span class="sxs-lookup"><span data-stu-id="97875-283">hello configurable parameters of this element are:</span></span>

* <span data-ttu-id="97875-284">**개체\_이름**: hello 컬렉션에 대 한 hello 개체 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-284">**Object\_name**: hello object name for hello collection.</span></span>
* <span data-ttu-id="97875-285">**인스턴스\_regex**:는 *정규식* 어떤 인스턴스 toocollect를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-285">**Instance\_regex**: a *regular expression* defining which instances toocollect.</span></span> <span data-ttu-id="97875-286">값 hello: `.*` 모든 인스턴스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-286">hello value: `.*` specifies all instances.</span></span> <span data-ttu-id="97875-287">만 hello에 대 한 프로세서 메트릭 toocollect \_지정 총 인스턴스 `_Total`합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-287">toocollect processor metrics for only hello \_Total instance, you could specify `_Total`.</span></span> <span data-ttu-id="97875-288">에 대 한 toocollect 프로세스 메트릭만 crond 또는 sshd 인스턴스에 hello, 지정할 수 있습니다: `(crond|sshd)`합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-288">toocollect process metrics for only hello crond or sshd instances, you could specify: `(crond|sshd)`.</span></span>
* <span data-ttu-id="97875-289">**카운터\_이름\_regex**:는 *정규식* 어떤 (hello 개체)에 대 한 카운터 toocollect를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-289">**Counter\_name\_regex**: a *regular expression* defining which counters (for hello object) toocollect.</span></span> <span data-ttu-id="97875-290">toocollect hello 개체에 대 한 모든 카운터 지정: `.*`합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-290">toocollect all counters for hello object, specify: `.*`.</span></span> <span data-ttu-id="97875-291">hello 메모리 개체에 대 한만 스왑 공간 카운터만 toocollect, 다음을 지정할 수 있습니다.`.+Swap.+`</span><span class="sxs-lookup"><span data-stu-id="97875-291">toocollect only swap space counters for hello memory object, you could specify: `.+Swap.+`</span></span>
* <span data-ttu-id="97875-292">**간격:**: hello 주파수는 hello 개체의 카운터를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-292">**Interval:**: hello frequency at which hello object's counters are collected.</span></span>

<span data-ttu-id="97875-293">성능 메트릭에 대 한 hello 기본 구성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-293">hello default configuration for performance metrics is:</span></span>

```
<source>
  type oms_omi
  object_name "Physical Disk"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Logical Disk"
  instance_regex ".*
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Processor"
  instance_regex ".*
  counter_name_regex ".*"
  interval 30s
</source>

<source>
  type oms_omi
  object_name "Memory"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

### <a name="enable-mysql-performance-counters-using-linux-commands"></a><span data-ttu-id="97875-294">Linux 명령을 사용하여 MySQL 성능 카운터 활성화</span><span class="sxs-lookup"><span data-stu-id="97875-294">Enable MySQL performance counters using Linux commands</span></span>
<span data-ttu-id="97875-295">Hello omsagent 번들을 설치할 때 hello 컴퓨터에서 MySQL Server 또는 MariaDB 서버가 검색 되 면 한 성능 모니터링 MySQL Server에 대 한 공급자가 자동으로 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-295">If MySQL Server or MariaDB Server is detected on hello computer when hello omsagent bundle is installed, a performance monitoring provider for MySQL Server is automatically installed.</span></span> <span data-ttu-id="97875-296">이 공급자는 toohello 로컬 MySQL/MariaDB 서버 tooexpose 성능 통계를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-296">This provider connects toohello local MySQL/MariaDB server tooexpose performance statistics.</span></span> <span data-ttu-id="97875-297">Hello 공급자 액세스할 수 있도록 MySQL 서버 hello tooconfigure MySQL 사용자 자격 증명이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-297">You need tooconfigure MySQL user credentials so that hello provider can access hello MySQL Server.</span></span>

<span data-ttu-id="97875-298">toodefine 기본 사용자 계정 MySQL 서버 hello에 대 한 localhost를 사용 하 여 hello 다음 명령 예제에 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-298">toodefine a default user account for hello MySQL server on localhost, use hello following command example.</span></span>

> [!NOTE]
> <span data-ttu-id="97875-299">hello 자격 증명 파일 hello omsagent 계정이 읽을 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-299">hello credentials file must be readable by hello omsagent account.</span></span> <span data-ttu-id="97875-300">로 hello mycimprovauth 명령을 실행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-300">Running hello mycimprovauth command as omsgent is recommended.</span></span>
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


<span data-ttu-id="97875-301">또는 지정할 수 있습니다 hello hello 파일을 만들어 파일에서 MySQL 자격 증명 필요: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. Hello mysql-auth 파일을 통해 모니터링할 MySQL 자격 증명을 관리 하는 방법에 대 한 자세한 내용은 참조 [관리 MySQL 모니터링 자격 증명 hello 인증 파일에](#manage-mysql-monitoring-credentials-in-the-authentication-file)합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-301">Alternatively, you can specify hello required MySQL credentials in a file, by creating hello file: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. For more information about managing MySQL credentials for monitoring through hello mysql-auth file, see [Manage MySQL monitoring credentials in hello authentication file](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span></span>

<span data-ttu-id="97875-302">참조 [MySQL 성능 카운터에 필요한 데이터베이스 권한](#database-permissions-required-for-mysql-performance-counters) hello MySQL 사용자 toocollect MySQL Server 성능 데이터에 필요한 개체 사용 권한에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-302">See [Database permissions required for MySQL performance counters](#database-permissions-required-for-mysql-performance-counters) for details about object permissions required by hello MySQL user toocollect MySQL Server performance data.</span></span>

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a><span data-ttu-id="97875-303">Linux 명령을 사용하여 Apache HTTP 서버 성능 카운터 활성화</span><span class="sxs-lookup"><span data-stu-id="97875-303">Enable Apache HTTP Server performance counters using Linux commands</span></span>
<span data-ttu-id="97875-304">Apache HTTP Server hello omsagent 번들을 설치할 때 hello 컴퓨터에서 검색 되 면 한 성능 모니터링 공급자 Apache HTTP server가 자동으로 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-304">If Apache HTTP Server is detected on hello computer when hello omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server is automatically installed.</span></span> <span data-ttu-id="97875-305">이 공급자는 사용 하는 Apache "모듈" 순서 tooaccess 성능 데이터에 hello Apache HTTP Server에 로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-305">This provider relies on an Apache "module" that must be loaded into hello Apache HTTP Server in order tooaccess performance data.</span></span>

<span data-ttu-id="97875-306">다음 명령을 hello로 hello 모듈을 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-306">You can load hello module with hello following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="97875-307">toounload hello Apache 모니터링 모듈을 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-307">toounload hello Apache monitoring module, run hello following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="tooview-performance-data-with-log-analytics"></a><span data-ttu-id="97875-308">로그 분석을 사용 하 여 tooview 성능 데이터</span><span class="sxs-lookup"><span data-stu-id="97875-308">tooview performance data with Log Analytics</span></span>
1. <span data-ttu-id="97875-309">Hello Operations Management Suite 포털에서 hello 로그 검색 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-309">In hello Operations Management Suite portal, click hello Log Search tile.</span></span>
2. <span data-ttu-id="97875-310">Hello 검색 표시줄에 입력 `* (Type=Perf)` tooview 모든 성능 카운터입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-310">In hello search bar, type `* (Type=Perf)` tooview all performance counters.</span></span>

<span data-ttu-id="97875-311">OMS에 Windows 성능 카운터 데이터도 수집 하므로 범위를 좁혀야 hello tooLinux 관련 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-311">Because OMS also collects Windows performance counter data, you should scope-down hello search tooLinux-specific data.</span></span> <span data-ttu-id="97875-312">따라서 hello 다음 예제에서는 보여 Chorizo21 이라는 성능 데이터 특정 tooan 예제 Linux 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-312">So, hello following example would show performance data specific tooan example Linux server named Chorizo21.</span></span>

```
Type=Perf Computer=chorizo*
```

![검색 결과에 표시된 예제 서버](./media/log-analytics-linux-agents/oms-perfsearch01.png)

<span data-ttu-id="97875-314">Hello 결과에서 클릭할 수 있는 **메트릭** tooview hello 카운터에 대해 수집 된 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-314">In hello results, you can click **Metrics** tooview hello counters that data was collected for.</span></span> <span data-ttu-id="97875-315">각 카운터에 대한 실시간 데이터가 그래프로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-315">Real-time data is shown as graphs for each counter.</span></span>

![메트릭](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a><span data-ttu-id="97875-317">syslog</span><span class="sxs-lookup"><span data-stu-id="97875-317">Syslog</span></span>
<span data-ttu-id="97875-318">Syslog는 이벤트 로깅 프로토콜 비슷한 tooWindows 이벤트 로그-둘 다 동일 하 게 작동 OMS에 표시 될 때입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-318">Syslog is an event logging protocol similar tooWindows Event logs—both operate similarly when displayed in OMS.</span></span>

### <a name="tooadd-a-new-linux-syslog-facility-in-oms"></a><span data-ttu-id="97875-319">tooadd OMS에서 새로운 Linux syslog 기능</span><span class="sxs-lookup"><span data-stu-id="97875-319">tooadd a new Linux syslog facility in OMS</span></span>
1. <span data-ttu-id="97875-320">Hello에 **설정** 페이지의 **데이터** , 클릭 **Syslog** toohello 왼쪽 hello 더하기 아이콘의 이름을 입력 합니다 hello tooadd 원하는 hello syslog 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-320">On hello **Settings** page under **Data** , click **Syslog** and then toohello left of hello plus icon, type hello name of hello syslog facility that you want tooadd.</span></span>
    <span data-ttu-id="97875-321">![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span><span class="sxs-lookup"><span data-stu-id="97875-321">![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span></span>
2. <span data-ttu-id="97875-322">Hello 시설의 전체 이름을 hello를 모르는 경우 이름의 일부를 입력을 시작할 수 있습니다 및 사용 가능한 syslog 기능 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-322">If you don’t know hello full name of hello facility, you can start typing a partial name and a list of available syslog facilities will appear.</span></span> <span data-ttu-id="97875-323">Tooadd 원하는 하 hello 목록에서 hello 이름을 클릭 한 다음 hello 및 아이콘 tooadd hello를 클릭 하는 hello syslog 기능을 찾을 때 syslog 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-323">When you find hello syslog facility that you want tooadd, click hello name in hello list and then click hello plus icon tooadd hello syslog facility.</span></span>
3. <span data-ttu-id="97875-324">Hello 기능을 추가 하면 hello 목록에 나타나고 색된 막대로 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-324">After you add hello facility, it appears in hello list of highlighted with a colored bar.</span></span> <span data-ttu-id="97875-325">다음으로 hello 심각도 (syslog 기능 정보 범주)을 선택 toocollect 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-325">Next, choose hello severities (categories of syslog facility information) that you want toocollect.</span></span>
4. <span data-ttu-id="97875-326">Hello hello 페이지 맨 아래에 클릭 **저장** toofinalize 변경 내용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-326">At hello bottom of hello page click **Save** toofinalize your changes.</span></span> <span data-ttu-id="97875-327">일반적으로 5 분 이내에 등록 된 OMS에 Linux 용 hello 구성 변경 내용 아 tooall hello OMS 에이전트로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-327">hello configuration changes that you’ve made are then sent tooall hello OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-syslog-facilities-in-linux"></a><span data-ttu-id="97875-328">Linux에서 Linux syslog 기능 구성</span><span class="sxs-lookup"><span data-stu-id="97875-328">Configure Linux syslog facilities in Linux</span></span>
<span data-ttu-id="97875-329">Syslog 이벤트는 syslog 디먼 hello 전송 됩니다, 그리고 예를 들어 rsyslog 또는 syslog ng, tooa 로컬 포트 해당 hello 에이전트에서 수신 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-329">Syslog events are sent from hello syslog daemon, for example rsyslog or syslog-ng, tooa local port that hello agent is listening on.</span></span> <span data-ttu-id="97875-330">기본 포트는 25224입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-330">By default, port 25224.</span></span> <span data-ttu-id="97875-331">Hello 에이전트를 설치할 때 기본 syslog 구성이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-331">When hello agent is installed, a default syslog configuration is applied.</span></span> <span data-ttu-id="97875-332">위치는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-332">This is found at:</span></span>

<span data-ttu-id="97875-333">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span><span class="sxs-lookup"><span data-stu-id="97875-333">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span></span>

<span data-ttu-id="97875-334">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span><span class="sxs-lookup"><span data-stu-id="97875-334">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span></span>

<span data-ttu-id="97875-335">hello 기본 OMS 에이전트 syslog 구성은 심각도 경고 이상인 모든 기능의 syslog 이벤트를에서 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-335">hello default OMS agent syslog configuration uploads syslog events from all facilities with a severity of warning or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="97875-336">Hello syslog 구성을 편집 하는 경우 hello 변경 tootake 효과 대 한 hello syslog 디먼을 다시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-336">If you edit hello syslog configuration, you must restart hello syslog daemon for hello changes tootake effect.</span></span>
>
>

<span data-ttu-id="97875-337">hello 기본 syslog 구성은 hello OMS 에이전트에 대 한 Linux 용 OMS에 대 한 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-337">hello default syslog configuration for hello OMS Agent for Linux for OMS is:</span></span>

#### <a name="rsyslog"></a><span data-ttu-id="97875-338">Rsyslog</span><span class="sxs-lookup"><span data-stu-id="97875-338">Rsyslog</span></span>
```
kern.warning       @127.0.0.1:25224
user.warning       @127.0.0.1:25224
daemon.warning     @127.0.0.1:25224
auth.warning       @127.0.0.1:25224
syslog.warning     @127.0.0.1:25224
uucp.warning       @127.0.0.1:25224
authpriv.warning   @127.0.0.1:25224
ftp.warning        @127.0.0.1:25224
cron.warning       @127.0.0.1:25224
local0.warning     @127.0.0.1:25224
local1.warning     @127.0.0.1:25224
local2.warning     @127.0.0.1:25224
local3.warning     @127.0.0.1:25224
local4.warning     @127.0.0.1:25224
local5.warning     @127.0.0.1:25224
local6.warning     @127.0.0.1:25224
local7.warning     @127.0.0.1:25224
```

#### <a name="syslog-ng"></a><span data-ttu-id="97875-339">Syslog-ng</span><span class="sxs-lookup"><span data-stu-id="97875-339">Syslog-ng</span></span>
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="tooview-all-syslog-events-with-log-analytics"></a><span data-ttu-id="97875-340">tooview 로그 분석을 갖는 모든 Syslog 이벤트</span><span class="sxs-lookup"><span data-stu-id="97875-340">tooview all Syslog events with Log Analytics</span></span>
1. <span data-ttu-id="97875-341">Hello Operations Management Suite 포털에서 클릭 hello **로그 검색** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-341">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="97875-342">Hello에 **로그 관리** 미리 정의 된 syslog 검색을 선택한 다음 한 toorun 선택 그룹화 것입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-342">In hello **Log Management** grouping, choose a predefined syslog search and then select one toorun it.</span></span>

<span data-ttu-id="97875-343">이 예제는 모든 Syslog 이벤트를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="97875-343">This example shows all Syslog events.</span></span>

![로그 검색에 표시된 Syslog 이벤트](./media/log-analytics-linux-agents/oms-linux-syslog.png)

<span data-ttu-id="97875-345">이제 검색 결과를 세부적으로 들여다 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-345">Now you can drill into search results.</span></span>

## <a name="linux-alerts"></a><span data-ttu-id="97875-346">Linux 경고</span><span class="sxs-lookup"><span data-stu-id="97875-346">Linux alerts</span></span>
<span data-ttu-id="97875-347">Toomanage Nagios 또는 Zabbix를 사용 하 여 Linux 컴퓨터 다음 OMS는 이러한 도구에서 생성 된 hello 경고를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-347">If you use Nagios or Zabbix toomanage your Linux machines, then OMS can receive hello alerts generated from those tools.</span></span> <span data-ttu-id="97875-348">그러나 현재 없습니다 메서드 tooconfigure 들어오는 경고 데이터는 hello OMS 포털을 사용 하 여.</span><span class="sxs-lookup"><span data-stu-id="97875-348">However, there is currently no method tooconfigure incoming alert data using hello OMS portal.</span></span> <span data-ttu-id="97875-349">대신, tooedit는 config 파일 toostart 보내는 경고 tooOMS 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-349">Instead, you will need tooedit a config file toostart sending alerts tooOMS.</span></span>

### <a name="collect-alerts-from-nagios"></a><span data-ttu-id="97875-350">Nagios의 경고 수집</span><span class="sxs-lookup"><span data-stu-id="97875-350">Collect alerts from Nagios</span></span>
<span data-ttu-id="97875-351">Nagios 서버에서 경고 toocollect toomake hello 구성 변경 내용을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-351">toocollect alerts from a Nagios server, you need toomake hello following configuration changes.</span></span>

1. <span data-ttu-id="97875-352">Grant hello 사용자 **omsagent** 읽기 액세스 toohello Nagios 로그 파일 (예: /var/log/nagios/nagios.log).</span><span class="sxs-lookup"><span data-stu-id="97875-352">Grant hello user **omsagent** read access toohello Nagios log file (i.e. /var/log/nagios/nagios.log).</span></span> <span data-ttu-id="97875-353">Hello 그룹 hello nagios.log 파일을 소유 하는 것으로 가정 **nagios** , hello 사용자를 추가할 수 있습니다 **omsagent** toohello **nagios** 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-353">Assuming hello nagios.log file is owned by hello group **nagios** , you can add hello user **omsagent** toohello **nagios** group.</span></span>

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. <span data-ttu-id="97875-354">Hello omsagent.confconfiguration 파일 수정 (/ 등/옵트인/microsoft/omsagent/&lt;작업 영역 id&gt;/conf/omsagent.conf).</span><span class="sxs-lookup"><span data-stu-id="97875-354">Modify hello omsagent.confconfiguration file (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf).</span></span> <span data-ttu-id="97875-355">충족 했는지 확인 hello 다음 항목이 있고 주석으로 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-355">Ensure hello following entries are present and not commented out:</span></span>

    ```
    <source>
    type tail
    #Update path toopoint tooyour nagios.log
    path /var/log/nagios/nagios.log
    format none
    tag oms.nagios
    </source>

    <filter oms.nagios>
    type filter_nagios_log
    </filter>
    ```
3. <span data-ttu-id="97875-356">Hello omsagent 디먼을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-356">Restart hello omsagent daemon:</span></span>

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a><span data-ttu-id="97875-357">Zabbix의 경고 수집</span><span class="sxs-lookup"><span data-stu-id="97875-357">Collect alerts from Zabbix</span></span>
<span data-ttu-id="97875-358">Zabbix 서버에서 경고 toocollect 해야 toospecify 사용자와 암호를 제외 하 고 위의 nagios와 유사한 단계 toothose를 수행 합니다 *일반 텍스트*합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-358">toocollect alerts from a Zabbix server, you'll perform similar steps toothose for Nagios above, except you'll need toospecify a user and password in *clear text*.</span></span> <span data-ttu-id="97875-359">바람직하지는 않지만 곧 변경될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-359">This is not ideal, but will likely change soon.</span></span> <span data-ttu-id="97875-360">tooaddress이이 문제를 좋습니다 hello 사용자 만들고 권한 toomonitor만 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-360">tooaddress this issue, we recommend that you create hello user and grant it permission toomonitor only.</span></span>

<span data-ttu-id="97875-361">Hello omsagent.conf 구성 파일의 예제 섹션 (/ 등/옵트인/microsoft/omsagent/&lt;작업 영역 id&gt;/conf/omsagent.conf)에 대 한 Zabbix hello 다음:</span><span class="sxs-lookup"><span data-stu-id="97875-361">An example section of hello omsagent.conf configuration file  (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf) for Zabbix should resemble hello following:</span></span>

```
<source>
  type zabbix_alerts
  run_interval 1m
  tag oms.zabbix
  zabbix_url http://localhost/zabbix/api_jsonrpc.php
  zabbix_username Admin
  zabbix_password zabbix
</source>

```

### <a name="view-alerts-in-log-analytics-search"></a><span data-ttu-id="97875-362">Log Analytics 검색에서 경고 보기</span><span class="sxs-lookup"><span data-stu-id="97875-362">View alerts in Log Analytics search</span></span>
<span data-ttu-id="97875-363">프로그램 Linux 컴퓨터 toosend 경고 tooOMS를 구성한 후에 몇 가지 간단한 로그 검색 쿼리 tooview hello 알림을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-363">After you've configured your Linux computers toosend alerts tooOMS, you can use a few simple log search queries tooview hello alerts.</span></span> <span data-ttu-id="97875-364">hello 다음 검색 쿼리 예제에서는 반환 생성 된 모든 기록 된 hello 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-364">hello following search query example returns all hello recorded alerts that were generated.</span></span> <span data-ttu-id="97875-365">예를 들어 IT 인프라에서 일종의 문제가 발생 하는 경우 다음에 대 한 결과 hello 다음 예제 쿼리 hello 문제가 문제가 발생 한 위치를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-365">For example, if some sort of problem occurs in your IT infrastructure, then results for hello following example query might indicate where hello problem might originate.</span></span> <span data-ttu-id="97875-366">및 드릴 수 있습니다 쉽게 toohello 경고 소스 시스템 toohelp 좁은 하 여 조사 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-366">And, you can easily drill in toohello alerts by source system toohelp narrow your investigation.</span></span> <span data-ttu-id="97875-367">hello 혜택은 반드시 없을 정도로 toogo toovarious 관리 시스템의 hello 시작-있는 경고 tooOMS 보내기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-367">hello benefit is that you don't necessarily have toogo toovarious management systems from hello start—provided that your alerts are sent tooOMS, you can start there.</span></span>

```
Type=Alert
```

#### <a name="tooview-all-nagios-alerts-with-log-analytics"></a><span data-ttu-id="97875-368">tooview 로그 분석와 모든 Nagios 경고</span><span class="sxs-lookup"><span data-stu-id="97875-368">tooview all Nagios alerts with Log Analytics</span></span>
1. <span data-ttu-id="97875-369">Hello Operations Management Suite 포털에서 클릭 hello **로그 검색** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-369">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="97875-370">Hello 쿼리 표시줄에 다음 검색 쿼리 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-370">In hello query bar, type hello following search query</span></span>

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![로그 검색에 표시된 Nagios 경고](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

<span data-ttu-id="97875-372">Hello 검색 결과 본 후 있습니다 수 정보를 상세히 추가 같은 *AlertState*합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-372">After you see hello search results, you can drill into additional details such as *AlertState*.</span></span>

### <a name="tooview-all-zabbix-alerts-with-log-analytics"></a><span data-ttu-id="97875-373">tooview 로그 분석과 함께 모든 Zabbix 경고</span><span class="sxs-lookup"><span data-stu-id="97875-373">tooview all Zabbix alerts with Log Analytics</span></span>
1. <span data-ttu-id="97875-374">Hello Operations Management Suite 포털에서 클릭 hello **로그 검색** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-374">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="97875-375">Hello 쿼리 표시줄에 다음 검색 쿼리 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-375">In hello query bar, type hello following search query</span></span>

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![로그 검색에 표시된 Zabbix 경고](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

<span data-ttu-id="97875-377">Hello 검색 결과 본 후 있습니다 수 정보를 상세히 추가 같은 *AlertName*합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-377">After you see hello search results, you can drill into additional details such as *AlertName*.</span></span>

## <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="97875-378">System Center Operations Manager와의 호환성</span><span class="sxs-lookup"><span data-stu-id="97875-378">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="97875-379">Linux 용 OMS 에이전트 hello hello System Center Operations Manager 에이전트와 에이전트 이진 파일을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-379">hello OMS Agent for Linux shares agent binaries with hello System Center Operations Manager agent.</span></span> <span data-ttu-id="97875-380">업그레이드는 OMI 및 SCX 패키지가 hello 컴퓨터 tooa 최신 버전을 hello 현재 Operations Manager에서 관리 하는 시스템에 Linux 용 OMS 에이전트 hello를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-380">Installing hello OMS Agent for Linux on a system currently managed by Operations Manager upgrades hello OMI and SCX packages on hello computer tooa newer version.</span></span> <span data-ttu-id="97875-381">Linux 및 System Center 2012 r 2 용 OMS 에이전트 hello 호환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-381">hello OMS Agent for Linux and System Center 2012 R2 are compatible.</span></span> <span data-ttu-id="97875-382">그러나 **System Center 2012 SP1 및 이전 버전은 현재 되지 호환 또는 지원 되는 Linux 용 OMS 에이전트 hello로 합니다.**</span><span class="sxs-lookup"><span data-stu-id="97875-382">However, **System Center 2012 SP1 and earlier versions are currently not compatible or supported with hello OMS Agent for Linux.**</span></span>

> [!NOTE]
> <span data-ttu-id="97875-383">Hello Linux 용 OMS 에이전트는 Operations Manager에서 관리 되지 않는 tooa 설치 된 컴퓨터를 Operations Manager를 사용 하 여 toomanage hello 컴퓨터를 나중에 원하는 hello 컴퓨터를 검색 하기 전에 hello OMI 구성을 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-383">If hello OMS Agent for Linux is installed tooa computer that is not currently managed by Operations Manager, and you later want toomanage hello computer with Operations Manager, you must modify hello OMI configuration before you discover hello computer.</span></span> <span data-ttu-id="97875-384">**Linux 용 OMS 에이전트 hello 전에 hello Operations Manager 에이전트가 설치 된 경우에이 단계가 필요 하지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="97875-384">**This step is not needed if hello Operations Manager agent is installed before hello OMS Agent for Linux.**</span></span>
>
>

### <a name="tooenable-hello-oms-agent-for-linux-toocommunicate-with-operations-manager"></a><span data-ttu-id="97875-385">Operations Manager와 함께 Linux toocommunicate에 대 한 tooenable hello OMS 에이전트</span><span class="sxs-lookup"><span data-stu-id="97875-385">tooenable hello OMS Agent for Linux toocommunicate with Operations Manager</span></span>
1. <span data-ttu-id="97875-386">Hello 파일 /etc/opt/omi/conf/omiserver.conf를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-386">Edit hello file /etc/opt/omi/conf/omiserver.conf</span></span>
2. <span data-ttu-id="97875-387">로 시작 하는 hello 줄 확인 **httpsport =** hello 포트 1270을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-387">Ensure that hello line beginning with **httpsport=** defines hello port 1270.</span></span> <span data-ttu-id="97875-388">예: `httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="97875-388">Such as `httpsport=1270`</span></span>
3. <span data-ttu-id="97875-389">Hello OMI 서버를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-389">Restart hello OMI server:</span></span>

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="97875-390">Database permissions required for MySQL performance counters</span><span class="sxs-lookup"><span data-stu-id="97875-390">Database permissions required for MySQL performance counters</span></span>
<span data-ttu-id="97875-391">toogrant 권한 tooa MySQL 모니터링 사용자, 부여할 hello 권한 뿐만 아니라 ' GRANT option ' hello hello 사용자 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-391">toogrant permissions tooa MySQL monitoring user, hello granting user must have hello 'GRANT option' privilege as well as hello privilege being granted.</span></span>

<span data-ttu-id="97875-392">MySQL 사용자 hello에 대 한 순서 대로 tooreturn 성능 데이터 hello 사용자가 쿼리를 다음 toohello 액세스할 필요:</span><span class="sxs-lookup"><span data-stu-id="97875-392">In order for hello MySQL User tooreturn performance data hello user will need access toohello following queries:</span></span>

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

<span data-ttu-id="97875-393">또한 toothese 쿼리 hello MySQL 사용자에 대 한 SELECT 권한도 toohello를 다음 기본 표 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-393">In addition toothese queries hello MySQL user requires SELECT access toohello following default tables:</span></span>

* <span data-ttu-id="97875-394">information_schema</span><span class="sxs-lookup"><span data-stu-id="97875-394">information_schema</span></span>
* <span data-ttu-id="97875-395">mysql</span><span class="sxs-lookup"><span data-stu-id="97875-395">mysql</span></span>

<span data-ttu-id="97875-396">Hello 다음 grant 명령을 실행 하 여 이러한 권한은 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-396">These privileges can be granted by running hello following grant commands.</span></span>

```
GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
GRANT SELECT ON mysql.* too‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-hello-authentication-file"></a><span data-ttu-id="97875-397">MySQL 모니터링 hello 인증 파일에서 자격 증명 관리</span><span class="sxs-lookup"><span data-stu-id="97875-397">Manage MySQL monitoring credentials in hello authentication file</span></span>
<span data-ttu-id="97875-398">hello 다음 섹션에서는 MySQL 자격 증명을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-398">hello following sections help you manage MySQL credentials.</span></span>

### <a name="configure-hello-mysql-omi-provider"></a><span data-ttu-id="97875-399">Hello MySQL OMI 공급자 구성</span><span class="sxs-lookup"><span data-stu-id="97875-399">Configure hello MySQL OMI provider</span></span>
<span data-ttu-id="97875-400">hello MySQL OMI 공급자는 미리 구성 된 MySQL 사용자가 수행 해야 하 고 MySQL 클라이언트 라이브러리가 순서 tooquery hello 성능/상태 정보 hello MySQL 인스턴스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-400">hello MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order tooquery hello performance/health information from hello MySQL instance.</span></span>

### <a name="mysql-omi-authentication-file"></a><span data-ttu-id="97875-401">MySQL OMI 인증 파일</span><span class="sxs-lookup"><span data-stu-id="97875-401">MySQL OMI authentication file</span></span>
<span data-ttu-id="97875-402">MySQL OMI 공급자에서 어떤 바인딩 주소 및 포트 hello MySQL 인스턴스가 수신 대기 하는 인증 파일 toodetermine 및 toouse toogather 메트릭을 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-402">MySQL OMI provider uses an authentication file toodetermine what bind-address and port hello MySQL instance is listening on and what credentials toouse toogather metrics.</span></span> <span data-ttu-id="97875-403">하는 동안 설치 hello MySQL OMI 공급자가 바인딩 주소 및 포트와 집합 hello MySQL OMI 인증 파일을 부분적으로 한 MySQL my.cnf 구성 파일 (기본 위치)을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-403">During installation hello MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set hello MySQL OMI authentication file.</span></span>

<span data-ttu-id="97875-404">MySQL 서버 인스턴스에 대 한 모니터링을 toocomplete hello 올바른 디렉터리에 미리 생성 된 MySQL OMI 인증 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-404">toocomplete monitoring of a MySQL server instance, add a pre-generated MySQL OMI authentication file into hello correct directory.</span></span>

### <a name="authentication-file-format"></a><span data-ttu-id="97875-405">인증 파일 형식</span><span class="sxs-lookup"><span data-stu-id="97875-405">Authentication file format</span></span>
<span data-ttu-id="97875-406">hello MySQL OMI 인증 파일은에 대 한 정보를 포함 하는 텍스트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-406">hello MySQL OMI authentication file is a text file that contains information about:</span></span>

* <span data-ttu-id="97875-407">포트</span><span class="sxs-lookup"><span data-stu-id="97875-407">Port</span></span>
* <span data-ttu-id="97875-408">바인딩 주소</span><span class="sxs-lookup"><span data-stu-id="97875-408">Bind-Address</span></span>
* <span data-ttu-id="97875-409">MySQL 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="97875-409">MySQL username</span></span>
* <span data-ttu-id="97875-410">Base64로 인코딩된 암호</span><span class="sxs-lookup"><span data-stu-id="97875-410">Base64 encoded password</span></span>

<span data-ttu-id="97875-411">MySQL OMI 인증 파일 hello 생성 한 읽기/쓰기 toohello Linux 사용자에 대 한 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-411">hello MySQL OMI authentication file only grants privileges for read/write toohello Linux user that generated it.</span></span>

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

<span data-ttu-id="97875-412">기본 MySQL OMI 인증 파일에는 기본 인스턴스 및 포트 번호를 사용할 수 있고 hello 발견 된 MySQL 구성 파일에서에서 구문 분석 된 정보에 따라 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-412">A default MySQL OMI authentication file contains a default instance and a port number depending on what information is available and parsed from hello found MySQL configuration file.</span></span>

<span data-ttu-id="97875-413">hello 기본 인스턴스를 보다 쉽게 한 Linux 호스트에서 여러 MySQL 인스턴스를 관리 하는 수단 toomake 이며 포트 0 사용 hello 인스턴스로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-413">hello default instance is a means toomake managing multiple MySQL instances on one Linux host easier, and is denoted by hello instance with port 0.</span></span> <span data-ttu-id="97875-414">추가한 모든 인스턴스는 hello 기본 인스턴스에서 속성 집합을 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-414">All added instances will inherit properties set from hello default instance.</span></span> <span data-ttu-id="97875-415">예를 들어 포트 '3308'에서 수신 대기 중인 MySQL 인스턴스가 추가 되 면 hello 기본 인스턴스의 바인딩 주소, username 및 password Base64 인코딩 tootry 사용된 되며 3308에서 수신 대기 하는 hello 인스턴스를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-415">For example, if MySQL instance listening on port '3308' is added, hello default instance's bind-address, username, and Base64 encoded password will be used tootry and monitor hello instance listening on 3308.</span></span> <span data-ttu-id="97875-416">3308 hello 인스턴스가 바인딩된 tooanother 주소 사용 하 여 hello 동일한 MySQL 사용자 이름 및 암호 쌍에만 다시 지정 하면 되 hello hello 경우 바인딩 주소만 필요 하 고 hello 다른 속성은 상속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-416">If hello instance on 3308 is binded tooanother address and uses hello same MySQL username and password pair only hello respecification of hello bind-address is needed and hello other properties will be inherited.</span></span>

<span data-ttu-id="97875-417">Hello 인증 파일의 예는 hello 다음과 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-417">Examples of hello authentication file resemble hello following.</span></span>

<span data-ttu-id="97875-418">기본 인스턴스 및 포트 3308 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="97875-418">Default instance and instance with port 3308:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

<span data-ttu-id="97875-419">기본 인스턴스 및 포트 3308 및 Base64로 인코딩된 암호가 다른 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="97875-419">Default instance and instance with port 3308 + different Base 64 encoded password:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| <span data-ttu-id="97875-420">**속성**</span><span class="sxs-lookup"><span data-stu-id="97875-420">**Property**</span></span> | <span data-ttu-id="97875-421">**설명**</span><span class="sxs-lookup"><span data-stu-id="97875-421">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="97875-422">포트</span><span class="sxs-lookup"><span data-stu-id="97875-422">Port</span></span> |<span data-ttu-id="97875-423">Hello 현재 포트 hello를 MySQL 인스턴스가 수신 중인 포트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="97875-423">Port represents hello current port hello MySQL instance is listening on.</span></span>  <span data-ttu-id="97875-424">hello 포트 0 다음 hello 속성이 기본 인스턴스에 대 한 사용 됨을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-424">hello port 0 implies that hello properties following are used for default instance.</span></span> |
| <span data-ttu-id="97875-425">바인딩 주소</span><span class="sxs-lookup"><span data-stu-id="97875-425">Bind-Address</span></span> |<span data-ttu-id="97875-426">hello 바인딩 주소는 hello 현재 MySQL 바인딩 주소</span><span class="sxs-lookup"><span data-stu-id="97875-426">hello Bind Address is hello current MySQL bind-address</span></span> |
| <span data-ttu-id="97875-427">username</span><span class="sxs-lookup"><span data-stu-id="97875-427">username</span></span> |<span data-ttu-id="97875-428">Toouse toomonitor hello MySQL server 인스턴스를 원하는 hello MySQL 사용자의이 hello 사용자 이름.</span><span class="sxs-lookup"><span data-stu-id="97875-428">This hello username of hello MySQL user you wish toouse toomonitor hello MySQL server instance.</span></span> |
| <span data-ttu-id="97875-429">Base64로 인코딩된 암호</span><span class="sxs-lookup"><span data-stu-id="97875-429">Base64 encoded Password</span></span> |<span data-ttu-id="97875-430">이 base 64로 인코드된 hello MySQL 모니터링 사용자의 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-430">This is hello password of hello MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="97875-431">AutoUpdate</span><span class="sxs-lookup"><span data-stu-id="97875-431">AutoUpdate</span></span> |<span data-ttu-id="97875-432">Hello MySQL OMI 공급자가 업그레이드 hello 공급자 hello my.cnf 파일에서 변경 내용을 다시 검사 되 고 hello MySQL OMI 인증 파일을 덮어쓰게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-432">When hello MySQL OMI Provider is upgraded hello provider will rescan for changes in hello my.cnf file and overwrite hello MySQL OMI Authentication file.</span></span> <span data-ttu-id="97875-433">이 플래그 tootrue에 따라 또는 false 필수 업데이트 toohello MySQL OMI 인증 파일을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-433">Set this flag tootrue or false depending on required updates toohello MySQL OMI authentication file.</span></span> |

#### <a name="authentication-file-location"></a><span data-ttu-id="97875-434">인증 파일 위치</span><span class="sxs-lookup"><span data-stu-id="97875-434">Authentication file location</span></span>
<span data-ttu-id="97875-435">hello MySQL OMI 인증 파일 hello 수정할 수 있는 위치에에서 있는 하 고 이름이 "mysql-auth" 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-435">hello MySQL OMI Authentication File should be located in hello following location and named "mysql-auth":</span></span>

<span data-ttu-id="97875-436">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span><span class="sxs-lookup"><span data-stu-id="97875-436">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span></span>

<span data-ttu-id="97875-437">hello 파일 (및 auth/omsagent 디렉터리) hello omsagent 사용자가 소유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-437">hello file (and auth/omsagent directory) should be owned by hello omsagent user.</span></span>

## <a name="agent-logs"></a><span data-ttu-id="97875-438">에이전트 로그</span><span class="sxs-lookup"><span data-stu-id="97875-438">Agent logs</span></span>
<span data-ttu-id="97875-439">Linux 용 OMS 에이전트 hello에 대 한 hello 로그에는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-439">hello logs for hello OMS Agent for Linux is at:</span></span>

<span data-ttu-id="97875-440">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span><span class="sxs-lookup"><span data-stu-id="97875-440">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span></span>

<span data-ttu-id="97875-441">hello에 대 한 hello 로그 omsconfig (에이전트 구성) 프로그램에 대 한 Linux 용 OMS 에이전트에는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-441">hello logs for hello OMS Agent for Linux for omsconfig (agent configuration) program is at:</span></span>

<span data-ttu-id="97875-442">/var/opt/microsoft/omsconfig/log/</span><span class="sxs-lookup"><span data-stu-id="97875-442">/var/opt/microsoft/omsconfig/log/</span></span>

<span data-ttu-id="97875-443">Hello OMI 및 SCX 구성 요소 (성능 메트릭 데이터 제공)에 대 한 로그에는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-443">Logs for hello OMI and SCX components (which provide performance metrics data) is at:</span></span>

<span data-ttu-id="97875-444">/var/opt/omi/log/ and /var/opt/microsoft/scx/log</span><span class="sxs-lookup"><span data-stu-id="97875-444">/var/opt/omi/log/ and /var/opt/microsoft/scx/log</span></span>

## <a name="troubleshooting-hello-oms-agent-for-linux"></a><span data-ttu-id="97875-445">Linux 용 OMS 에이전트 hello 문제 해결</span><span class="sxs-lookup"><span data-stu-id="97875-445">Troubleshooting hello OMS Agent for Linux</span></span>
<span data-ttu-id="97875-446">다음 정보 toodiagnose hello를 사용 하 여 및 일반적인 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-446">Use hello following information toodiagnose and troubleshoot common issues.</span></span>

<span data-ttu-id="97875-447">None hello 문제 해결이 섹션의 정보를 사용 하면, 하는 경우 다음 리소스 toohelp 해결 hello를 문제도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-447">If none of hello troubleshooting information in this section helps you, you can also use hello following resources toohelp resolve your problem.</span></span>

* <span data-ttu-id="97875-448">프리미어 지원이 적용되는 고객의 경우 [프리미어](https://premier.microsoft.com/)를 통해 지원 사례를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-448">Customers with Premier support can log a support case via [Premier](https://premier.microsoft.com/)</span></span>
* <span data-ttu-id="97875-449">Azure 지원 계약이 있는 고객 hello 지원 사례 로그인 수 [Azure 포털](https://manage.windowsazure.com/?getsupport=true)</span><span class="sxs-lookup"><span data-stu-id="97875-449">Customers with Azure support agreements can log support cases in hello [Azure portal](https://manage.windowsazure.com/?getsupport=true)</span></span>
* <span data-ttu-id="97875-450">[GitHub 문제](https://github.com/Microsoft/OMS-Agent-for-Linux/issues) 제출</span><span class="sxs-lookup"><span data-stu-id="97875-450">File a [GitHub Issue](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span></span>
* <span data-ttu-id="97875-451">아이디어와 toocreate 버그 보고서에 대 한 피드백 포럼 [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span><span class="sxs-lookup"><span data-stu-id="97875-451">Feedback forum for ideas and toocreate a bug report [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span></span>

### <a name="important-log-locations"></a><span data-ttu-id="97875-452">중요 로그 위치</span><span class="sxs-lookup"><span data-stu-id="97875-452">Important log locations</span></span>
| <span data-ttu-id="97875-453">파일</span><span class="sxs-lookup"><span data-stu-id="97875-453">File</span></span> | <span data-ttu-id="97875-454">Path</span><span class="sxs-lookup"><span data-stu-id="97875-454">Path</span></span> |
| --- | --- |
| <span data-ttu-id="97875-455">Linux 용 OMS 에이전트 로그 파일</span><span class="sxs-lookup"><span data-stu-id="97875-455">OMS Agent for Linux Log File</span></span> |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| <span data-ttu-id="97875-456">OMS 에이전트 구성 로그 파일</span><span class="sxs-lookup"><span data-stu-id="97875-456">OMS Agent Configuration Log File</span></span> |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a><span data-ttu-id="97875-457">중요 구성 파일</span><span class="sxs-lookup"><span data-stu-id="97875-457">Important configuration files</span></span>
| <span data-ttu-id="97875-458">범주</span><span class="sxs-lookup"><span data-stu-id="97875-458">Catergory</span></span> | <span data-ttu-id="97875-459">파일 위치</span><span class="sxs-lookup"><span data-stu-id="97875-459">File Location</span></span> |
| --- | --- |
| <span data-ttu-id="97875-460">syslog</span><span class="sxs-lookup"><span data-stu-id="97875-460">Syslog</span></span> |<span data-ttu-id="97875-461">`/etc/syslog-ng/syslog-ng.conf` 또는 `/etc/rsyslog.conf` 또는 `/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="97875-461">`/etc/syslog-ng/syslog-ng.conf` or `/etc/rsyslog.conf` or `/etc/rsyslog.d/95-omsagent.conf`</span></span> |
| <span data-ttu-id="97875-462">성능, Nagios, Zabbix, OMS 출력 및 일반 에이전트</span><span class="sxs-lookup"><span data-stu-id="97875-462">Performance, Nagios, Zabbix, OMS output and general agent</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| <span data-ttu-id="97875-463">추가 구성</span><span class="sxs-lookup"><span data-stu-id="97875-463">Additional configurations</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> <span data-ttu-id="97875-464">OMS 포털 구성을 사용하도록 설정한 경우 시스템에서 성능 카운터 및 syslog의 편집 구성 파일을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="97875-464">Editing configuration files for performance counters and syslog are overwritten if OMS Portal Configuration is enabled.</span></span> <span data-ttu-id="97875-465">(모든 노드)에 대 한 hello OMS 포털에서에서 구성을 해제할 수 있습니다 또는 hello 다음을 실행 하 여 단일 노드에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-465">You can disable configuration in hello OMS Portal (for all nodes) or for single nodes by running hello following:</span></span>
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a><span data-ttu-id="97875-466">디버그 로깅 활성화</span><span class="sxs-lookup"><span data-stu-id="97875-466">Enable debug logging</span></span>
<span data-ttu-id="97875-467">tooenable 디버그 로깅을 사용할 수 있습니다 hello OMS 출력 플러그 인 및 자세한 정보를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-467">tooenable debug logging, you can use hello OMS output plugin and verbose output.</span></span>

#### <a name="oms-output-plugin"></a><span data-ttu-id="97875-468">OMS 출력 플러그인</span><span class="sxs-lookup"><span data-stu-id="97875-468">OMS output plugin</span></span>
<span data-ttu-id="97875-469">FluentD는 hello 플러그 인 toospecify 입 / 출력에 대 한 다른 로그 수준에 대 한 로깅 수준을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-469">FluentD allows hello plugin toospecify logging levels for different log levels for inputs and outputs.</span></span> <span data-ttu-id="97875-470">hello에 hello 일반 에이전트 구성을 편집 하는 OMS 출력에 대 한 다른 로그 수준을 toospecify `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-470">toospecify a different log level for OMS output, edit hello general agent configuration in hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` file.</span></span>

<span data-ttu-id="97875-471">Hello 아래 근처의 hello 구성 파일을 변경 hello `log_level` 속성 `info` 너무`debug`합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-471">Near hello bottom of hello configuration file, change hello `log_level` property from `info` too`debug`.</span></span>

 ```
 <match oms.** docker.**>
  type out_oms
  log_level debug
  num_threads 5
  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
 ```

<span data-ttu-id="97875-472">디버그 로깅을 사용 하면 데이터 항목 및 toosend에 걸린 시간 단위의 시간을 입력 하 여 OMS 서비스로 구분 된 일괄 처리 toosee 업로드 toohello 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-472">Debug logging allows you toosee batched uploads toohello OMS Service separated by type, number of data items, and time taken toosend.</span></span>

<span data-ttu-id="97875-473">*디버그 사용 로그 예:*</span><span class="sxs-lookup"><span data-stu-id="97875-473">*Example debug enabled log:*</span></span>

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a><span data-ttu-id="97875-474">자세한 정보 출력</span><span class="sxs-lookup"><span data-stu-id="97875-474">Verbose output</span></span>
<span data-ttu-id="97875-475">Hello OMS 출력 플러그 인을 사용 하는 대신 있습니다도 출력 데이터 항목 직접 너무`stdout`는 Linux 로그 파일에 대 한 hello OMS 에이전트에에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-475">Instead of using hello OMS output plugin, you can also output data items directly too`stdout`, which is visible in hello OMS Agent for Linux log file.</span></span>

<span data-ttu-id="97875-476">Hello OMS 일반 에이전트 구성 파일에서 `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, 주석 아웃 hello OMS 추가 하 여 플러그 인을 출력 한 `#` 각 줄 앞에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-476">In hello OMS general agent configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, comment-out hello OMS output plugin by adding a `#` in front of each line.</span></span>

```
#<match oms.** docker.**>
#  type out_oms
#  log_level info
#  num_threads 5
#  buffer_chunk_limit 5m
#  buffer_type file
#  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
#  buffer_queue_limit 10
#  flush_interval 20s
#  retry_limit 10
#  retry_wait 30s
#</match>
```

<span data-ttu-id="97875-477">아래 출력 플러그 인 hello, hello hello를 제거 하 여 섹션 다음에 hello 주석 제거 `#` 각 줄의 시작 hello 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-477">Below hello output plugin, remove hello comment in hello following section by removing hello `#` symbol at hello beginning of each line.</span></span>

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-hello-log"></a><span data-ttu-id="97875-478">전달 된 Syslog 메시지 hello 로그에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-478">Forwarded Syslog messages do not appear in hello log</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="97875-479">가능한 원인</span><span class="sxs-lookup"><span data-stu-id="97875-479">Probable causes</span></span>
* <span data-ttu-id="97875-480">hello 적용 된 구성 toohello Linux 서버 않습니다 하지 컬렉션 hello 전송 기능을 허용 및/또는 로그 수준</span><span class="sxs-lookup"><span data-stu-id="97875-480">hello configuration applied toohello Linux server does not allow collection of hello sent facilities and/or log levels</span></span>
* <span data-ttu-id="97875-481">Syslog는 전달 되지 않고 올바르게 toohello Linux 서버</span><span class="sxs-lookup"><span data-stu-id="97875-481">Syslog is not being forwarded correctly toohello Linux server</span></span>
* <span data-ttu-id="97875-482">hello에 대 한 Linux toohandle hello OMS 에이전트의 기본 구성에 대 한 초당 전달 된 메시지의 hello 수가 너무 큽니다.</span><span class="sxs-lookup"><span data-stu-id="97875-482">hello number of messages being forwarded per second are too large for hello base configuration of hello OMS Agent for Linux toohandle</span></span>

#### <a name="resolutions"></a><span data-ttu-id="97875-483">해결 방법</span><span class="sxs-lookup"><span data-stu-id="97875-483">Resolutions</span></span>
* <span data-ttu-id="97875-484">Syslog 모든 hello 시설 및 hello 올바른 로그 수준에 대 한 hello OMS 포털에서에서 해당 hello 구성 확인</span><span class="sxs-lookup"><span data-stu-id="97875-484">Verify that hello configuration in hello OMS Portal for Syslog has all hello facilities and hello correct log levels</span></span>
  * <span data-ttu-id="97875-485">**OMS 포털 > 설정 > 데이터 > Syslog**</span><span class="sxs-lookup"><span data-stu-id="97875-485">**OMS Portal > Settings > Data > Syslog**</span></span>
* <span data-ttu-id="97875-486">해당 기본 syslog 디먼 메시징 확인 (`rsyslog`, `syslog-ng`)는 수 tooreceive 전달 hello 메시지</span><span class="sxs-lookup"><span data-stu-id="97875-486">Verify that native syslog messaging daemons (`rsyslog`, `syslog-ng`) are able tooreceive hello forwarded messages</span></span>
* <span data-ttu-id="97875-487">메시지가 차단 되는 hello Syslog 서버 tooensure에서 방화벽 설정을 확인합니다</span><span class="sxs-lookup"><span data-stu-id="97875-487">Check firewall settings on hello Syslog server tooensure that messages are not being blocked</span></span>
* <span data-ttu-id="97875-488">Hello를 사용 하 여 Syslog 메시지 tooOMS 시뮬레이션 `logger` 명령-예:</span><span class="sxs-lookup"><span data-stu-id="97875-488">Simulate a Syslog message tooOMS using hello `logger` command - for example:</span></span>
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-toooms-when-using-a-proxy"></a><span data-ttu-id="97875-489">프록시를 사용할 때 tooOMS 연결 문제</span><span class="sxs-lookup"><span data-stu-id="97875-489">Problems connecting tooOMS when using a proxy</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="97875-490">가능한 원인</span><span class="sxs-lookup"><span data-stu-id="97875-490">Probable causes</span></span>
* <span data-ttu-id="97875-491">hello 프록시가 지정 hello 에이전트를 설치 및 구성 올바르지 않은 경우</span><span class="sxs-lookup"><span data-stu-id="97875-491">hello proxy specified when installing and configuring hello agent is incorrect</span></span>
* <span data-ttu-id="97875-492">사용할 수 없는 데이터 센터에서 whitelistested hello OMS 서비스 끝점</span><span class="sxs-lookup"><span data-stu-id="97875-492">hello OMS Service endpoints are not whitelistested in your datacenter</span></span>

#### <a name="resolutions"></a><span data-ttu-id="97875-493">해결 방법</span><span class="sxs-lookup"><span data-stu-id="97875-493">Resolutions</span></span>
* <span data-ttu-id="97875-494">다음 명령을 hello 옵션을 사용 하는 hello를 사용 하 여 Linux 용 OMS 에이전트 hello를 다시 설치 `-v` 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-494">Reinstall hello OMS Agent for Linux using hello following command with hello option `-v` enabled.</span></span> <span data-ttu-id="97875-495">이렇게 하면 hello 프록시 toohello OMS 서비스를 통해 연결 하는 hello 에이전트의 자세한 정보를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-495">This allows verbose output of hello agent connecting through hello proxy toohello OMS Service.</span></span>
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * <span data-ttu-id="97875-496">OMS에는 프록시에 대 한 hello 설명서를 검토 [HTTP 프록시 서버와 함께 사용할 hello 에이전트 구성](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span><span class="sxs-lookup"><span data-stu-id="97875-496">Review hello documentation for OMS proxy at [Configuring hello agent for use with an HTTP proxy server](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span></span>
* <span data-ttu-id="97875-497">OMS 서비스 끝점을 다음 해당 hello 허용 목록 확인</span><span class="sxs-lookup"><span data-stu-id="97875-497">Verify that hello following OMS Service endpoints are whitelisted</span></span>

| <span data-ttu-id="97875-498">에이전트 리소스</span><span class="sxs-lookup"><span data-stu-id="97875-498">Agent Resource</span></span> | <span data-ttu-id="97875-499">포트</span><span class="sxs-lookup"><span data-stu-id="97875-499">Ports</span></span> |
| --- | --- |
| <span data-ttu-id="97875-500">&#42;.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="97875-500">&#42;.ods.opinsights.azure.com</span></span> |<span data-ttu-id="97875-501">포트 443</span><span class="sxs-lookup"><span data-stu-id="97875-501">Port 443</span></span> |
| <span data-ttu-id="97875-502">&#42;.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="97875-502">&#42;.oms.opinsights.azure.com</span></span> |<span data-ttu-id="97875-503">포트 443</span><span class="sxs-lookup"><span data-stu-id="97875-503">Port 443</span></span> |
| <span data-ttu-id="97875-504">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="97875-504">ods.systemcenteradvisor.com</span></span> |<span data-ttu-id="97875-505">포트 443</span><span class="sxs-lookup"><span data-stu-id="97875-505">Port 443</span></span> |
| <span data-ttu-id="97875-506">&#42;.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="97875-506">&#42;.blob.core.windows.net/</span></span> |<span data-ttu-id="97875-507">포트 443</span><span class="sxs-lookup"><span data-stu-id="97875-507">Port 443</span></span> |

### <a name="a-403-error-is-displayed-when-onboarding"></a><span data-ttu-id="97875-508">등록 시 403 오류가 표시됨</span><span class="sxs-lookup"><span data-stu-id="97875-508">A 403 error is displayed when onboarding</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="97875-509">가능한 원인</span><span class="sxs-lookup"><span data-stu-id="97875-509">Probable causes</span></span>
* <span data-ttu-id="97875-510">hello 날짜 및 시간 Linux 서버에서 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-510">hello date and time are incorrect on Linux Server</span></span>
* <span data-ttu-id="97875-511">hello 작업 영역 ID 및 사용 되는 작업 영역 키 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-511">hello Workspace ID and Workspace Key used are incorrect</span></span>

#### <a name="resolution"></a><span data-ttu-id="97875-512">해결 방법</span><span class="sxs-lookup"><span data-stu-id="97875-512">Resolution</span></span>
* <span data-ttu-id="97875-513">Linux 서버 hello hello 시간 확인 `date` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-513">Verify hello time on your Linux server with hello `date` command.</span></span> <span data-ttu-id="97875-514">데이터 보다 큽니다. hello 또는에서 15 분 미만 hello 현재 시간, 온 보 딩 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-514">If hello data is greater than or less than 15 minutes from hello current time, then onboarding fails.</span></span> <span data-ttu-id="97875-515">toocorrect이 hello 날짜 및/또는 Linux 서버에의 표준 시간대를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-515">toocorrect this, update hello date and/or timezone of your Linux server.</span></span>
* <span data-ttu-id="97875-516">hello Linux 용 OMS 에이전트의 최신 버전 hello 알림을 표시 시간 차이가 온 보 딩 오류로 인해 발생 한 경우</span><span class="sxs-lookup"><span data-stu-id="97875-516">hello latest version of hello OMS Agent for Linux notifies you if a time difference is causing onboarding failure</span></span>
* <span data-ttu-id="97875-517">올바른 작업 영역 ID와 작업 영역 키 hello 사용 하 여 다시 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-517">Re-onboard using hello correct Workspace ID and Workspace Key.</span></span> <span data-ttu-id="97875-518">참조 [hello 명령줄을 사용 하는 온 보 딩](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-518">See  [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>

### <a name="a-500-error-or-404-error-appears-in-hello-log-file-after-onboarding"></a><span data-ttu-id="97875-519">500 오류 또는 404 오류 뒤에 표시 hello 로그 파일에 온 보 딩</span><span class="sxs-lookup"><span data-stu-id="97875-519">A 500 error or 404 error appears in hello log file after onboarding</span></span>
<span data-ttu-id="97875-520">OMS 작업 영역에 Linux 데이터의 hello 첫 번째 업로드 중에 발생 하는 알려진된 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-520">This is a known issue that occurs during hello first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="97875-521">이 문제는 전송되는 데이터 또는 다른 문제에 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-521">This does not affect data being sent or other problems.</span></span> <span data-ttu-id="97875-522">Hello 오류 때 처음에 무시할 수 있습니다 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-522">You can ignore hello errors when initially onboarding.</span></span>

### <a name="nagios-data-does-not-appear-in-hello-oms-portal"></a><span data-ttu-id="97875-523">Nagios 데이터 hello OMS 포털에에서 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-523">Nagios data does not appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="97875-524">가능한 원인</span><span class="sxs-lookup"><span data-stu-id="97875-524">Probable causes</span></span>
* <span data-ttu-id="97875-525">hello omsagent 사용자가 없는 사용 권한을 tooread hello Nagios 로그 파일에서</span><span class="sxs-lookup"><span data-stu-id="97875-525">hello omsagent user does not have permissions tooread from hello Nagios log file</span></span>
* <span data-ttu-id="97875-526">hello Nagios 원본 및 필터 섹션 hello omsagent.conf 파일에서 여전히 주석</span><span class="sxs-lookup"><span data-stu-id="97875-526">hello Nagios source and filter sections are still commented in hello omsagent.conf file</span></span>

#### <a name="resolutions"></a><span data-ttu-id="97875-527">해결 방법</span><span class="sxs-lookup"><span data-stu-id="97875-527">Resolutions</span></span>
* <span data-ttu-id="97875-528">Hello Nagios 파일에서 순서 tooread에 hello omsagent 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-528">Add hello omsagent user in order tooread from hello Nagios file.</span></span> <span data-ttu-id="97875-529">자세한 내용은 [Nagios 경고](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97875-529">See [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) for more information.</span></span>
* <span data-ttu-id="97875-530">에 OMS 에이전트에서 Linux 일반 구성 파일에 대 한 hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, 되도록 **둘 다** Nagios 제거 의견을 포함 하는 원본 및 필터 섹션에서는 다음 예제와 비슷한 toohello hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-530">In hello OMS Agent for Linux general configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, ensure that **both** hello Nagios source and filter sections have comments removed, similar toohello following example.</span></span>

```
<source>
  type tail
  path /var/log/nagios/nagios.log
  format none
  tag oms.nagios
</source>

<filter oms.nagios>
  type filter_nagios_log
</filter>
```


### <a name="linux-data-doesnt-appear-in-hello-oms-portal"></a><span data-ttu-id="97875-531">Linux 데이터 hello OMS 포털에에서 표시 되지 않으면</span><span class="sxs-lookup"><span data-stu-id="97875-531">Linux data doesn't appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="97875-532">가능한 원인</span><span class="sxs-lookup"><span data-stu-id="97875-532">Probable causes</span></span>
* <span data-ttu-id="97875-533">온 보 딩 toohello OMS 서비스 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-533">Onboarding toohello OMS Service failed</span></span>
* <span data-ttu-id="97875-534">OMS 서비스에서 차단 되는 연결 toohello</span><span class="sxs-lookup"><span data-stu-id="97875-534">Connection toohello OMS Service is blocked</span></span>
* <span data-ttu-id="97875-535">Linux 데이터에 대 한 OMS 에이전트 hello는 백업</span><span class="sxs-lookup"><span data-stu-id="97875-535">hello OMS Agent for Linux data is backed-up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="97875-536">해결 방법</span><span class="sxs-lookup"><span data-stu-id="97875-536">Resolutions</span></span>
* <span data-ttu-id="97875-537">해당 hello를 확인 하 여 해당 온 보 딩 toohello OMS 서비스에 성공 했는지 확인 `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-537">Verify that onboarding toohello OMS Service was successful by verifying that hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` exists.</span></span>
* <span data-ttu-id="97875-538">Omsadmin.sh 명령줄 hello 사용 하 여 다시 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-538">Re-onboard using hello omsadmin.sh command line.</span></span> <span data-ttu-id="97875-539">참조 [hello 명령줄을 사용 하는 온 보 딩](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-539">See [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="97875-540">Hello 프록시 문제 해결 위의 단계를 사용 하 여 프록시를 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="97875-540">If using a proxy, use hello proxy troubleshooting steps above</span></span>
* <span data-ttu-id="97875-541">경우에 따라 Linux 용 OMS 에이전트 hello hello OMS 서비스와 통신할 수 없는 경우 hello 에이전트에서 데이터에는 50MB의 백업 toohello 가득 찬 버퍼 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-541">In some cases, when hello OMS Agent for Linux cannot communicate with hello OMS Service, data on hello Agent is backed-up toohello full buffer size of 50 MB.</span></span> <span data-ttu-id="97875-542">Hello를 실행 하 여 Linux 용 OMS 에이전트 hello를 다시 시작 `/opt/microsoft/omsagent/bin/service_control restart` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-542">Restart hello OMS Agent for Linux by running hello `/opt/microsoft/omsagent/bin/service_control restart` command.</span></span>
  >[AZURE.NOTE] <span data-ttu-id="97875-543">이 문제는 에이전트 버전 1.1.0-28 및 이상에서 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-543">This issue is fixed in Agent version 1.1.0-28 and later.</span></span>

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-hello-oms-portal"></a><span data-ttu-id="97875-544">Syslog Linux 성능 카운터 구성 hello OMS 포털에서 적용 되지 않음</span><span class="sxs-lookup"><span data-stu-id="97875-544">Syslog Linux performance counter configuration is not applied in hello OMS portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="97875-545">가능한 원인</span><span class="sxs-lookup"><span data-stu-id="97875-545">Probable causes</span></span>
* <span data-ttu-id="97875-546">Linux 용 OMS 에이전트 hello에 hello 구성 에이전트 hello OMS 포털에서 hello 최신 구성을 검색 했습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-546">hello configuration agent in hello OMS Agent for Linux has not retrieved hello latest configuration from hello OMS portal.</span></span>
* <span data-ttu-id="97875-547">hello hello 포털에서 수정 된 설정은 적용 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-547">hello revised settings in hello portal were not applied</span></span>

#### <a name="resolutions"></a><span data-ttu-id="97875-548">해결 방법</span><span class="sxs-lookup"><span data-stu-id="97875-548">Resolutions</span></span>
<span data-ttu-id="97875-549">`omsconfig`linux 5 분 마다 OMS 포털 구성 변경 내용을 검색 하는 hello OMS 에이전트의에서 hello 구성 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-549">`omsconfig` is hello configuration agent in hello OMS Agent for Linux that retrieves OMS portal configuration changes every 5 minutes.</span></span> <span data-ttu-id="97875-550">이 구성은 Linux 구성 파일에 대 한 적용 된 toohello OMS 에이전트에 있는 다음 `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-550">This configuration is then applied toohello OMS Agent for Linux configuration files located at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span></span>

* <span data-ttu-id="97875-551">경우에 따라 Linux 구성 에이전트에 대 한 OMS 에이전트 hello hello 포털 구성 서비스에 최신 구성을 적용 하지 수 toocommunicate 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-551">In some cases, hello OMS Agent for Linux configuration agent might not be able toocommunicate with hello portal configuration service resulting in latest configuration not being applied.</span></span>
* <span data-ttu-id="97875-552">해당 hello 확인 `omsconfig` 에이전트 hello 다음와 함께 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-552">Verify that hello `omsconfig` agent is installed with hello following:</span></span>

  * <span data-ttu-id="97875-553">`dpkg --list omsconfig` 또는 `rpm -qi omsconfig`</span><span class="sxs-lookup"><span data-stu-id="97875-553">`dpkg --list omsconfig` or `rpm -qi omsconfig`</span></span>
  * <span data-ttu-id="97875-554">설치 되어 있지 않으면 Linux 용 hello 최신 버전의 hello OMS 에이전트를 다시 설치</span><span class="sxs-lookup"><span data-stu-id="97875-554">If not installed, reinstall hello latest version of hello OMS Agent for Linux</span></span>
* <span data-ttu-id="97875-555">해당 hello 확인 `omsconfig` 에이전트 hello OMS 서비스와 통신할 수</span><span class="sxs-lookup"><span data-stu-id="97875-555">Verify that hello `omsconfig` agent can communicate with hello OMS service</span></span>

  * <span data-ttu-id="97875-556">Hello 실행 `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` 명령</span><span class="sxs-lookup"><span data-stu-id="97875-556">Run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
    * <span data-ttu-id="97875-557">hello 위의 명령을 반환 hello 구성 해당 에이전트에서 Syslog 설정, Linux 성능 카운터 및 사용자 지정 로그를 포함 하 여 hello 포털 검색</span><span class="sxs-lookup"><span data-stu-id="97875-557">hello command above returns hello configuration that agent retrieves from hello portal, including Syslog settings, Linux performance counters, and custom logs</span></span>
    * <span data-ttu-id="97875-558">위의 hello 명령이 실패 하면 실행 hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-558">If hello command above fails, run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="97875-559">이 명령은 hello OMS 서비스 tooretrieve hello 최신 구성 사용 하 여 hello omsconfig 에이전트 toocommunicate가 되도록합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-559">This command forces hello omsconfig agent toocommunicate with hello OMS service tooretrieve hello latest configuration.</span></span>

### <a name="custom-linux-log-data-does-not-appear-in-hello-oms-portal"></a><span data-ttu-id="97875-560">사용자 지정 Linux 로그 데이터 hello OMS 포털에에서 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-560">Custom Linux log data does not appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="97875-561">가능한 원인</span><span class="sxs-lookup"><span data-stu-id="97875-561">Probable causes</span></span>
* <span data-ttu-id="97875-562">온 보 딩 tooOMS 서비스 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-562">Onboarding tooOMS Service failed</span></span>
* <span data-ttu-id="97875-563">hello **구성 toomy Linux 서버에 따라 적용 hello** 설정을 선택 하지</span><span class="sxs-lookup"><span data-stu-id="97875-563">hello **Apply hello following configuration toomy Linux Servers** setting has not been selected</span></span>
* <span data-ttu-id="97875-564">omsconfig은 hello hello 포털에서 최신 사용자 지정 로그 선택 되지 않은</span><span class="sxs-lookup"><span data-stu-id="97875-564">omsconfig has not picked up hello latest custom log from hello portal</span></span>
* <span data-ttu-id="97875-565">hello `omsagent` 사용은 없습니다 tooaccess hello tooa 사용 권한 문제로 인해 사용자 지정 로그 또는 `omsagent` 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-565">hello `omsagent` use is unable tooaccess hello custom log due tooa permissions problem or `omsagent` was not found.</span></span> <span data-ttu-id="97875-566">이 경우 hello 출력 뒤에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97875-566">In this case, you'll see hello following output:</span></span>
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* <span data-ttu-id="97875-567">이 Linux 버전 1.1.0-217에 대 한 hello OMS 에이전트에서에서 수정 된 경합 상태 hello로 알려진된 문제</span><span class="sxs-lookup"><span data-stu-id="97875-567">This is a known issue with hello Race Condition that was fixed in hello OMS Agent for Linux version 1.1.0-217</span></span>

#### <a name="resolutions"></a><span data-ttu-id="97875-568">해결 방법</span><span class="sxs-lookup"><span data-stu-id="97875-568">Resolutions</span></span>
* <span data-ttu-id="97875-569">작업이 성공적으로 사용, 되는지 hello 확인 하 여 확인 `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-569">Verify that you've successfully onboarded, by determining whether hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` file exists.</span></span>
  * <span data-ttu-id="97875-570">필요한 경우 hello omsadmin.sh 명령줄을 사용 하 여 다시 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-570">If needed, onboard again using hello omsadmin.sh command line.</span></span> <span data-ttu-id="97875-571">참조 [hello 명령줄을 사용 하는 온 보 딩](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-571">See [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="97875-572">에 OMS 포털을 아래 hello **설정** hello에 **데이터** 탭에서 해당 hello 확인 **적용 hello 구성 toomy Linux 서버 다음** 설정을 선택</span><span class="sxs-lookup"><span data-stu-id="97875-572">In hello OMS Portal, under **Settings** on hello **Data** tab, ensure that hello **Apply hello following configuration toomy Linux Servers** setting is selected</span></span>  
  <span data-ttu-id="97875-573">![구성 적용](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span><span class="sxs-lookup"><span data-stu-id="97875-573">![apply configuration](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span></span>
* <span data-ttu-id="97875-574">해당 hello 확인 `omsconfig` 에이전트 hello OMS 서비스와 통신할 수</span><span class="sxs-lookup"><span data-stu-id="97875-574">Verify that hello `omsconfig` agent can communicate with hello OMS service</span></span>

  * <span data-ttu-id="97875-575">Hello 실행 `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` 명령</span><span class="sxs-lookup"><span data-stu-id="97875-575">Run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
  * <span data-ttu-id="97875-576">hello 위의 명령을 반환 hello 구성 에이전트에 hello Syslog 설정, Linux 성능 카운터 및 사용자 지정 로그를 포함 하 여 포털에서에서 검색</span><span class="sxs-lookup"><span data-stu-id="97875-576">hello command above returns hello configuration that agent retrieves from hello Portal, including Syslog settings, Linux performance counters, and custom Logs</span></span>
  * <span data-ttu-id="97875-577">위의 hello 명령이 실패 하면 실행 hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-577">If hello command above fails, run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="97875-578">이 명령은 OMS 서비스와 hello omsconfig 에이전트 toocommunicate 강제로 hello 최신 구성을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-578">This command forces hello omsconfig agent toocommunicate with OMS service and retrieve hello latest configuration.</span></span>

<span data-ttu-id="97875-579">권한 있는 사용자로 실행 하는 Linux 사용자에 대 한 OMS 에이전트 hello 대신 `root`, Linux hello로 실행에 대 한 OMS 에이전트 hello `omsagent` 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-579">Instead of hello OMS Agent for Linux user running as a privileged user `root`, hello OMS Agent for Linux runs as hello `omsagent` user.</span></span> <span data-ttu-id="97875-580">대부분의 경우에서 명시적 사용 권한이 있어야 toohello 사용자 순서 tooread에 특정 파일을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-580">In most cases, explicit permission must be granted toohello user in order tooread certain files.</span></span>

<span data-ttu-id="97875-581">toogrant 권한이 너무`omsagent` hello 다음 명령을 실행 사용자:</span><span class="sxs-lookup"><span data-stu-id="97875-581">toogrant permission too`omsagent` user, run hello following commands:</span></span>

1. <span data-ttu-id="97875-582">Hello 추가 `omsagent` 으로 사용자 tooa 특정 그룹`sudo usermod -a -G <GROUPNAME> <USERNAME>`</span><span class="sxs-lookup"><span data-stu-id="97875-582">Add hello `omsagent` user tooa specific group with `sudo usermod -a -G <GROUPNAME> <USERNAME>`</span></span>
2. <span data-ttu-id="97875-583">공용 읽기 액세스 toohello 필요한 파일을 부여 합니다.`sudo chmod -R ugo+rw <FILE DIRECTORY>`</span><span class="sxs-lookup"><span data-stu-id="97875-583">Grant universal read access toohello required file with `sudo chmod -R ugo+rw <FILE DIRECTORY>`</span></span>

<span data-ttu-id="97875-584">Hello Linux 버전 1.1.0-217에 대 한 hello OMS 에이전트에서에서 수정 된 경합 상태는 알려진된 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-584">There is a known issue with hello Race Condition that was fixed in hello OMS Agent for Linux version 1.1.0-217.</span></span> <span data-ttu-id="97875-585">Toohello 최신 에이전트를 업데이트 한 후 명령 tooget hello hello 출력 플러그 인을 최신 버전을 다음 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-585">After updating toohello latest agent, run hello following command tooget hello latest version of hello output plugin:</span></span>

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a><span data-ttu-id="97875-586">알려진 제한 사항</span><span class="sxs-lookup"><span data-stu-id="97875-586">Known limitations</span></span>
<span data-ttu-id="97875-587">다음 섹션에서는 toolearn Linux 용 OMS 에이전트 hello의 현재 제한 사항에 대 한 hello를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-587">Review hello following sections toolearn about current limitations of hello OMS Agent for Linux.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="97875-588">Azure 진단</span><span class="sxs-lookup"><span data-stu-id="97875-588">Azure Diagnostics</span></span>
<span data-ttu-id="97875-589">Azure에서 실행 중인 Linux 가상 컴퓨터에 대 한 추가 단계는 Azure 진단 및 Operations Management Suite에서 필요한 tooallow 데이터 수집을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-589">For Linux virtual machines running in Azure, additional steps may be required tooallow data collection by Azure Diagnostics and Operations Management Suite.</span></span> <span data-ttu-id="97875-590">**버전 2.2** hello의 Linux 용 진단 확장은 hello Linux 용 OMS 에이전트와의 호환성에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-590">**Version 2.2** of hello Diagnostics Extension for Linux is required for compatibility with hello OMS Agent for Linux.</span></span>

<span data-ttu-id="97875-591">설치 및 Linux 용 진단 확장 hello 구성에 대 한 자세한 내용은 참조 하십시오. [hello Azure CLI 명령을 tooenable Linux 진단 확장을 사용 하 여](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension)합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-591">For more information on installing and configuring hello Diagnostic Extension for Linux, see [Use hello Azure CLI command tooenable Linux Diagnostic Extension](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span></span>

<span data-ttu-id="97875-592">**Hello Linux 진단 확장에서 2.0 too2.2 Azure CLI ASM으로 업그레이드:**</span><span class="sxs-lookup"><span data-stu-id="97875-592">**Upgrading hello Linux Diagnostics Extension from 2.0 too2.2 Azure CLI ASM:**</span></span>

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="97875-593">**ARM**</span><span class="sxs-lookup"><span data-stu-id="97875-593">**ARM**</span></span>

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="97875-594">이 코드 예제는 PrivateConfig.json이라는 이름의 파일을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-594">These command examples reference a file named PrivateConfig.json.</span></span> <span data-ttu-id="97875-595">해당 파일의 hello 형식은 다음 샘플 hello와 비슷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-595">hello format of that file should resemble hello following sample.</span></span>

```
    {
    "storageAccountName":"hello storage account tooreceive data",
    "storageAccountKey":"hello key of hello account"
    }
```

### <a name="sysklog-is-not-supported"></a><span data-ttu-id="97875-596">Sysklog가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-596">Sysklog is not supported</span></span>
<span data-ttu-id="97875-597">Rsyslog 또는 syslog-ng 중 하나는 필수 toocollect syslog 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-597">Either rsyslog or syslog-ng are required toocollect syslog messages.</span></span> <span data-ttu-id="97875-598">Red Hat Enterprise Linux, CentOS 및 Oracle Linux 버전 (sysklog)의 버전 5에 hello 기본 syslog 디먼은 syslog 이벤트 수집이 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97875-598">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="97875-599">이 버전의,이 배포에서 syslog 데이터 toocollect hello rsyslog 디먼을 설치 해야 하며 tooreplace sysklog를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-599">toocollect syslog data from this version of these distributions, hello rsyslog daemon should be installed and configured tooreplace sysklog.</span></span> <span data-ttu-id="97875-600">Sysklog를 rsyslog로에 대 한 자세한 내용은 참조 하십시오. [hello 새로 빌드된 rsyslog RPM 설치](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM)합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-600">For more information on replacing sysklog with rsyslog, see [Install hello newly built rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span></span>

## <a name="next-steps"></a><span data-ttu-id="97875-601">다음 단계</span><span class="sxs-lookup"><span data-stu-id="97875-601">Next Steps</span></span>
* <span data-ttu-id="97875-602">[로그 분석 솔루션 hello 솔루션 갤러리에서에서 추가](log-analytics-add-solutions.md) tooadd 기능 및 수집 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="97875-602">[Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md) tooadd functionality and gather data.</span></span>
* <span data-ttu-id="97875-603">익숙해질 목적으로 [검색 로그](log-analytics-log-searches.md) tooview 솔루션에서 수집 된 정보를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-603">Get familiar with [log searches](log-analytics-log-searches.md) tooview detailed information gathered by solutions.</span></span>
* <span data-ttu-id="97875-604">사용 하 여 [대시보드](log-analytics-dashboards.md) toosave 및 표시 사용자 지정 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="97875-604">Use [dashboards](log-analytics-dashboards.md) toosave and display your own custom searches.</span></span>
