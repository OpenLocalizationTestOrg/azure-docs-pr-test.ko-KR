---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: TRUE
ROBOTS: NOINDEX
ms.openlocfilehash: 8332bdd39effab8c2ac9a75ca9a1e2510c940719
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-your-linux-computers-to-log-analytics"></a><span data-ttu-id="1b9ca-101">Log Analytics에 Linux 컴퓨터 연결</span><span class="sxs-lookup"><span data-stu-id="1b9ca-101">Connect your Linux computers to Log Analytics</span></span>
<span data-ttu-id="1b9ca-102">Log Analytics를 사용하여 Linux 컴퓨터에서 생성되는 데이터를 수집하고 그에 따른 조치를 취할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-102">Using Log Analytics, you can collect and act on data generated from Linux computers.</span></span> <span data-ttu-id="1b9ca-103">Linux에서 수집된 데이터를 OMS에 추가하면 컴퓨터 위치에 상관없이(사실상 모든 곳에서), Linux 시스템 및 Docker 같은 컨테이너 솔루션을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-103">Adding data collected from Linux to OMS allows you to manage Linux systems and container solutions like Docker, regardless of where your computers are located — virtually anywhere.</span></span> <span data-ttu-id="1b9ca-104">데이터 원본은 물리적 서버로서 온-프레미스 데이터 센터, Amazon Web Services(AWS) 또는 Microsoft Azure 같은 클라우드 호스티드 서비스의 가상 컴퓨터나 사용자 책상 위 노트북에도 상주할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-104">Data sources might reside in your on-premises datacenter as physical servers, virtual computers in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure, or even the laptop on your desk.</span></span> <span data-ttu-id="1b9ca-105">뿐만 아니라 OMS는 Windows 컴퓨터에서도 유사하게 데이터를 수집하기 때문에 진정한 하이브리드 IT 환경을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-105">In addition, OMS also collects data from Windows computers similarly, so it supports a truly hybrid IT environment.</span></span>

<span data-ttu-id="1b9ca-106">하나의 관리 포털을 통해 OMS의 Log Analytics에서 이 모든 소스의 데이터를 보고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-106">You can view and manage data from all of those sources with Log Analytics in OMS with a single management portal.</span></span> <span data-ttu-id="1b9ca-107">이렇게 하면 많은 다양한 시스템을 사용하여 데이터를 모니터링할 필요가 줄어들고, 데이터를 사용하기가 쉬워지고, 원하는 데이터를 무엇이든 이미 보유하고 있는 비즈니스 분석 솔루션이나 시스템에 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-107">This reduces the need to monitor it using many different systems, makes it easy to consume, and you can export any data you like to whatever business analytics solution or system that you already have.</span></span>

<span data-ttu-id="1b9ca-108">이 문서는 Linux용 OMS 에이전트를 사용하여 Linux 컴퓨터에 대한 데이터를 수집하고 관리하도록 돕는 빠른 시작 가이드입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-108">This article is a quick start guide that will help you collect and manage data for your Linux computers using the OMS Agent for Linux.</span></span> <span data-ttu-id="1b9ca-109">프록시 서버 구성, CollectD 메트릭에 대한 정보, 사용자 지정 JSON 데이터 원본과 같은 자세한 기술 정보는 GitHub의 [Linux용 OMS 에이전트 개요](https://github.com/Microsoft/OMS-Agent-for-Linux)(영문) 및 [Linux용 OMS 에이전트 전체 설명서](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-109">For more technical details such as proxy server configuration, information about CollectD metrics, and custom JSON data sources, you’ll find that information at [OMS Agent for Linux overview](https://github.com/Microsoft/OMS-Agent-for-Linux) and [OMS Agent for Linux full documentation](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) on GitHub.</span></span>

<span data-ttu-id="1b9ca-110">현재는 Linux 컴퓨터에서 다음과 같은 유형의 데이터를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-110">Currently, you can collect the following types of data from Linux computers:</span></span>

* <span data-ttu-id="1b9ca-111">성능 메트릭</span><span class="sxs-lookup"><span data-stu-id="1b9ca-111">Performance metrics</span></span>
* <span data-ttu-id="1b9ca-112">Syslog 이벤트</span><span class="sxs-lookup"><span data-stu-id="1b9ca-112">Syslog events</span></span>
* <span data-ttu-id="1b9ca-113">Nagios 및 Zabbix의 경고</span><span class="sxs-lookup"><span data-stu-id="1b9ca-113">Alerts from Nagios and Zabbix</span></span>
* <span data-ttu-id="1b9ca-114">Docker 컨테이너 성능 메트릭, 인벤토리 및 로그</span><span class="sxs-lookup"><span data-stu-id="1b9ca-114">Docker container performance metrics, inventory and logs</span></span>

## <a name="supported-linux-versions"></a><span data-ttu-id="1b9ca-115">지원되는 Linux 버전</span><span class="sxs-lookup"><span data-stu-id="1b9ca-115">Supported Linux versions</span></span>
<span data-ttu-id="1b9ca-116">x86 및 x64 버전 모두 다양한 Linux 배포에 대해 공식적으로 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-116">Both x86 and x64 versions are officially supported on a variety of Linux distributions.</span></span> <span data-ttu-id="1b9ca-117">하지만, Linux용 OMS 에이전트는 나열되지 않은 그 밖의 배포에서 실행이 가능할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-117">However, the OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="1b9ca-118">Amazon Linux 2012.09~2015.09</span><span class="sxs-lookup"><span data-stu-id="1b9ca-118">Amazon Linux 2012.09 through 2015.09</span></span>
* <span data-ttu-id="1b9ca-119">CentOS Linux 5, 6, 7</span><span class="sxs-lookup"><span data-stu-id="1b9ca-119">CentOS Linux 5, 6, and 7</span></span>
* <span data-ttu-id="1b9ca-120">Oracle Linux 5, 6, 7</span><span class="sxs-lookup"><span data-stu-id="1b9ca-120">Oracle Linux 5, 6, and 7</span></span>
* <span data-ttu-id="1b9ca-121">Red Hat Enterprise Linux Server 5, 6, 7</span><span class="sxs-lookup"><span data-stu-id="1b9ca-121">Red Hat Enterprise Linux Server 5, 6 and 7</span></span>
* <span data-ttu-id="1b9ca-122">Debian GNU/Linux 6, 7, 8</span><span class="sxs-lookup"><span data-stu-id="1b9ca-122">Debian GNU/Linux 6, 7, and 8</span></span>
* <span data-ttu-id="1b9ca-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span><span class="sxs-lookup"><span data-stu-id="1b9ca-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span></span>
* <span data-ttu-id="1b9ca-124">SUSE Linux Enterprise Server 11 및 12</span><span class="sxs-lookup"><span data-stu-id="1b9ca-124">SUSE Linux Enterprise Server 11 and 12</span></span>

## <a name="oms-agent-for-linux"></a><span data-ttu-id="1b9ca-125">Linux 용 OMS 에이전트</span><span class="sxs-lookup"><span data-stu-id="1b9ca-125">OMS Agent for Linux</span></span>
<span data-ttu-id="1b9ca-126">Linux용 Operations Management Suite 에이전트는 여러 패키지로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-126">The Operations Management Suite Agent for Linux comprises multiple packages.</span></span> <span data-ttu-id="1b9ca-127">다음 패키지를 포함하는 릴리스 파일은 `--extract`와 함께 shell 번들을 실행하면 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-127">The release file contains the following packages, available by running the shell bundle with `--extract`.</span></span>

| <span data-ttu-id="1b9ca-128">**패키지**</span><span class="sxs-lookup"><span data-stu-id="1b9ca-128">**Package**</span></span> | <span data-ttu-id="1b9ca-129">**버전**</span><span class="sxs-lookup"><span data-stu-id="1b9ca-129">**Version**</span></span> | <span data-ttu-id="1b9ca-130">**설명**</span><span class="sxs-lookup"><span data-stu-id="1b9ca-130">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1b9ca-131">omsagent</span><span class="sxs-lookup"><span data-stu-id="1b9ca-131">omsagent</span></span> |<span data-ttu-id="1b9ca-132">1.1.0</span><span class="sxs-lookup"><span data-stu-id="1b9ca-132">1.1.0</span></span> |<span data-ttu-id="1b9ca-133">Linux용 Operations Management Suite 에이전트</span><span class="sxs-lookup"><span data-stu-id="1b9ca-133">The Operations Management Suite Agent for Linux</span></span> |
| <span data-ttu-id="1b9ca-134">omsconfig</span><span class="sxs-lookup"><span data-stu-id="1b9ca-134">omsconfig</span></span> |<span data-ttu-id="1b9ca-135">1.1.1</span><span class="sxs-lookup"><span data-stu-id="1b9ca-135">1.1.1</span></span> |<span data-ttu-id="1b9ca-136">OMS 에이전트용 구성 에이전트</span><span class="sxs-lookup"><span data-stu-id="1b9ca-136">Configuration agent for the OMS Agent</span></span> |
| <span data-ttu-id="1b9ca-137">omi</span><span class="sxs-lookup"><span data-stu-id="1b9ca-137">omi</span></span> |<span data-ttu-id="1b9ca-138">1.0.8.3</span><span class="sxs-lookup"><span data-stu-id="1b9ca-138">1.0.8.3</span></span> |<span data-ttu-id="1b9ca-139">Open Management Infrastructure(OMI) -- 경량 CIM 서버</span><span class="sxs-lookup"><span data-stu-id="1b9ca-139">Open Management Infrastructure (OMI) -- a lightweight CIM Server</span></span> |
| <span data-ttu-id="1b9ca-140">scx</span><span class="sxs-lookup"><span data-stu-id="1b9ca-140">scx</span></span> |<span data-ttu-id="1b9ca-141">1.6.2</span><span class="sxs-lookup"><span data-stu-id="1b9ca-141">1.6.2</span></span> |<span data-ttu-id="1b9ca-142">운영 체제 성능 메트릭용 OMI CIM 공급자</span><span class="sxs-lookup"><span data-stu-id="1b9ca-142">OMI CIM Providers for operating system performance metrics</span></span> |
| <span data-ttu-id="1b9ca-143">apache-cimprov</span><span class="sxs-lookup"><span data-stu-id="1b9ca-143">apache-cimprov</span></span> |<span data-ttu-id="1b9ca-144">1.0.0</span><span class="sxs-lookup"><span data-stu-id="1b9ca-144">1.0.0</span></span> |<span data-ttu-id="1b9ca-145">OMI용 Apache HTTP 서버 성능 모니터링 공급자.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-145">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="1b9ca-146">Apache HTTP 서버가 감지되는 경우에만 설치됨.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-146">Only installed if Apache HTTP Server is detected.</span></span> |
| <span data-ttu-id="1b9ca-147">mysql-cimprov</span><span class="sxs-lookup"><span data-stu-id="1b9ca-147">mysql-cimprov</span></span> |<span data-ttu-id="1b9ca-148">1.0.0</span><span class="sxs-lookup"><span data-stu-id="1b9ca-148">1.0.0</span></span> |<span data-ttu-id="1b9ca-149">OMI용 MySQL 서버 성능 모니터링 공급자.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-149">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="1b9ca-150">MySQL/MariaDB 서버가 감지되는 경우에만 설치됨.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-150">Only installed if MySQL/MariaDB server is detected.</span></span> |
| <span data-ttu-id="1b9ca-151">docker-cimprov</span><span class="sxs-lookup"><span data-stu-id="1b9ca-151">docker-cimprov</span></span> |<span data-ttu-id="1b9ca-152">0.1.0</span><span class="sxs-lookup"><span data-stu-id="1b9ca-152">0.1.0</span></span> |<span data-ttu-id="1b9ca-153">OMI용 Docker 공급자.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-153">Docker provider for OMI.</span></span> <span data-ttu-id="1b9ca-154">Docker가 감지되는 경우에만 설치됨.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-154">Only installed if Docker is detected.</span></span> |

### <a name="additional-installation-artifacts"></a><span data-ttu-id="1b9ca-155">추가적인 설치 아티팩트</span><span class="sxs-lookup"><span data-stu-id="1b9ca-155">Additional installation artifacts</span></span>
<span data-ttu-id="1b9ca-156">Linux용 OMS 에이전트 패키지를 설치한 후에는 다음과 같은 시스템 수준의 구성 변경이 추가로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-156">After installing the OMS agent for Linux packages, the following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="1b9ca-157">이러한 아티팩트는 omsagent 패키지가 제거되면 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-157">These artifacts are removed when the omsagent package is uninstalled.</span></span>

* <span data-ttu-id="1b9ca-158">`omsagent` 라는 이름의 권한 없는 사용자가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-158">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="1b9ca-159">이 계정으로 omsagent 디먼이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-159">This is the account the omsagent daemon runs as</span></span>
* <span data-ttu-id="1b9ca-160">sudoer의 “include” 파일은 /etc/sudoers.d/omsagent에 생성됩니다 syslog 및 omsagent 디먼을 다시 시작하도록 omsagent에게 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-160">A sudoers “include” file is created at /etc/sudoers.d/omsagent This authorizes omsagent to restart the syslog and omsagent daemons.</span></span> <span data-ttu-id="1b9ca-161">설치된 sudo 버전에서 sudo “include” 지시문이 지원되지 않으면, 이 항목은 /etc/sudoers에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-161">If sudo “include” directives are not supported in the installed version of sudo, these entries will be written to /etc/sudoers.</span></span>
* <span data-ttu-id="1b9ca-162">syslog 구성은 이벤트 하위 집합을 에이전트에 전달하도록 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-162">The syslog configuration is modified to forward a subset of events to the agent.</span></span> <span data-ttu-id="1b9ca-163">자세한 내용은 아래의 **데이터 수집 구성** 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-163">For more information, see the **Configuring Data Collection** section below</span></span>

### <a name="linux-data-collection-details"></a><span data-ttu-id="1b9ca-164">Linux 데이터 수집 세부 정보</span><span class="sxs-lookup"><span data-stu-id="1b9ca-164">Linux data collection details</span></span>
<span data-ttu-id="1b9ca-165">다음 테이블은 데이터 수집 방법 및 데이터가 수집되는 방식에 대한 기타 세부 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-165">The following table shows data collection methods and other details about how data is collected.</span></span>

| <span data-ttu-id="1b9ca-166">원본</span><span class="sxs-lookup"><span data-stu-id="1b9ca-166">source</span></span> | <span data-ttu-id="1b9ca-167">직접 에이전트</span><span class="sxs-lookup"><span data-stu-id="1b9ca-167">Direct Agent</span></span> | <span data-ttu-id="1b9ca-168">SCOM 에이전트</span><span class="sxs-lookup"><span data-stu-id="1b9ca-168">SCOM agent</span></span> | <span data-ttu-id="1b9ca-169">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="1b9ca-169">Azure Storage</span></span> | <span data-ttu-id="1b9ca-170">SCOM 필요?</span><span class="sxs-lookup"><span data-stu-id="1b9ca-170">SCOM required?</span></span> | <span data-ttu-id="1b9ca-171">관리 그룹을 통해 전송되는 SCOM 에이전트 데이터</span><span class="sxs-lookup"><span data-stu-id="1b9ca-171">SCOM agent data sent via management group</span></span> | <span data-ttu-id="1b9ca-172">수집 빈도</span><span class="sxs-lookup"><span data-stu-id="1b9ca-172">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="1b9ca-173">Zabbix</span><span class="sxs-lookup"><span data-stu-id="1b9ca-173">Zabbix</span></span> |![예](./media/log-analytics-linux-agents/oms-bullet-green.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="1b9ca-179">1분</span><span class="sxs-lookup"><span data-stu-id="1b9ca-179">1 minute</span></span> |
| <span data-ttu-id="1b9ca-180">Nagios</span><span class="sxs-lookup"><span data-stu-id="1b9ca-180">Nagios</span></span> |![예](./media/log-analytics-linux-agents/oms-bullet-green.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="1b9ca-186">도착 시</span><span class="sxs-lookup"><span data-stu-id="1b9ca-186">on arrival</span></span> |
| <span data-ttu-id="1b9ca-187">syslog</span><span class="sxs-lookup"><span data-stu-id="1b9ca-187">syslog</span></span> |![예](./media/log-analytics-linux-agents/oms-bullet-green.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="1b9ca-193">Azure 저장소: 10분, 에이전트: 도착 시</span><span class="sxs-lookup"><span data-stu-id="1b9ca-193">from Azure storage: 10 minutes; from agent: on arrival</span></span> |
| <span data-ttu-id="1b9ca-194">Linux 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="1b9ca-194">Linux performance counters</span></span> |![예](./media/log-analytics-linux-agents/oms-bullet-green.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="1b9ca-200">예약된 대로, 최소 10초</span><span class="sxs-lookup"><span data-stu-id="1b9ca-200">As scheduled, minimum of 10 seconds</span></span> |
| <span data-ttu-id="1b9ca-201">변경 내용 추적</span><span class="sxs-lookup"><span data-stu-id="1b9ca-201">change tracking</span></span> |![예](./media/log-analytics-linux-agents/oms-bullet-green.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="1b9ca-207">매시간</span><span class="sxs-lookup"><span data-stu-id="1b9ca-207">hourly</span></span> |

### <a name="package-requirements"></a><span data-ttu-id="1b9ca-208">패키지 요구 사항</span><span class="sxs-lookup"><span data-stu-id="1b9ca-208">Package Requirements</span></span>
| <span data-ttu-id="1b9ca-209">**필수 패키지**</span><span class="sxs-lookup"><span data-stu-id="1b9ca-209">**Required package**</span></span> | <span data-ttu-id="1b9ca-210">**설명**</span><span class="sxs-lookup"><span data-stu-id="1b9ca-210">**Description**</span></span> | <span data-ttu-id="1b9ca-211">**최소 버전**</span><span class="sxs-lookup"><span data-stu-id="1b9ca-211">**Minimum version**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1b9ca-212">Glibc</span><span class="sxs-lookup"><span data-stu-id="1b9ca-212">Glibc</span></span> |<span data-ttu-id="1b9ca-213">GNU C 라이브러리</span><span class="sxs-lookup"><span data-stu-id="1b9ca-213">GNU C library</span></span> |<span data-ttu-id="1b9ca-214">2.5-12</span><span class="sxs-lookup"><span data-stu-id="1b9ca-214">2.5-12</span></span> |
| <span data-ttu-id="1b9ca-215">Openssl</span><span class="sxs-lookup"><span data-stu-id="1b9ca-215">Openssl</span></span> |<span data-ttu-id="1b9ca-216">OpenSSL 라이브러리</span><span class="sxs-lookup"><span data-stu-id="1b9ca-216">OpenSSL libraries</span></span> |<span data-ttu-id="1b9ca-217">0.9.8e 또는 1.0</span><span class="sxs-lookup"><span data-stu-id="1b9ca-217">0.9.8e or 1.0</span></span> |
| <span data-ttu-id="1b9ca-218">Curl</span><span class="sxs-lookup"><span data-stu-id="1b9ca-218">Curl</span></span> |<span data-ttu-id="1b9ca-219">cURL 웹 클라이언트</span><span class="sxs-lookup"><span data-stu-id="1b9ca-219">cURL web client</span></span> |<span data-ttu-id="1b9ca-220">7.15.5</span><span class="sxs-lookup"><span data-stu-id="1b9ca-220">7.15.5</span></span> |
| <span data-ttu-id="1b9ca-221">Python-ctypes</span><span class="sxs-lookup"><span data-stu-id="1b9ca-221">Python-ctypes</span></span> |<span data-ttu-id="1b9ca-222">함수 라이브러리</span><span class="sxs-lookup"><span data-stu-id="1b9ca-222">function libraries</span></span> |<span data-ttu-id="1b9ca-223">해당 없음</span><span class="sxs-lookup"><span data-stu-id="1b9ca-223">n/a</span></span> |
| <span data-ttu-id="1b9ca-224">PAM</span><span class="sxs-lookup"><span data-stu-id="1b9ca-224">PAM</span></span> |<span data-ttu-id="1b9ca-225">플러그형 인증 모듈</span><span class="sxs-lookup"><span data-stu-id="1b9ca-225">Pluggable authentication Modules</span></span> |<span data-ttu-id="1b9ca-226">해당 없음</span><span class="sxs-lookup"><span data-stu-id="1b9ca-226">n/a</span></span> |

> [!NOTE]
> <span data-ttu-id="1b9ca-227">Syslog 메시지를 수집하려면 rsyslog 또는 syslog-ng가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-227">Either rsyslog or syslog-ng are required to collect syslog messages.</span></span> <span data-ttu-id="1b9ca-228">Red Hat Enterprise Linux 버전 5, CentOS 및 Oracle Linux 버전(sysklog)에서는 syslog 이벤트 수집을 위한 기본 syslog 디먼이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-228">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="1b9ca-229">이 배포의 해당 버전에서 syslog 데이터를 수집하려면 rsyslog 디먼을 설치하고 sysklog를 대체하도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-229">To collect syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog.</span></span>
>
>

## <a name="quick-install"></a><span data-ttu-id="1b9ca-230">빠른 설치</span><span class="sxs-lookup"><span data-stu-id="1b9ca-230">Quick install</span></span>
<span data-ttu-id="1b9ca-231">다음 명령을 실행하여 omsagent를 다운로드하고, 체크섬의 유효성을 검사한 다음 에이전트를 설치하고 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-231">Run the following commands to download the omsagent, validate the checksum, then  install and onboard the agent.</span></span> <span data-ttu-id="1b9ca-232">명령은 64비트용입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-232">Commands are for 64-bit.</span></span> <span data-ttu-id="1b9ca-233">작업 영역 ID 및 기본 키는 OMS 포털에서 **연결된 원본** 탭의 **설정**에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-233">The Workspace ID and Primary Key are found in the OMS portal under **Settings** on the **Connected Sources** tab.</span></span>

![작업 영역 정보](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

<span data-ttu-id="1b9ca-235">에이전트를 설치하고 업그레이드하는 방법은 매우 다양합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-235">There are a variety of other methods to install the agent and upgrade it.</span></span> <span data-ttu-id="1b9ca-236">자세한 내용은 [Steps to install the OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux)(Linux용 OMS 에이전트를 설치하는 단계)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-236">You can read more about them at [Steps to install the OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span></span>

<span data-ttu-id="1b9ca-237">[Azure 연습 동영상](https://www.youtube.com/watch?v=mF1wtHPEzT0)을 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-237">You can also view the [Azure video walkthrough](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span></span>

## <a name="choose-your-linux-data-collection-method"></a><span data-ttu-id="1b9ca-238">Linux 데이터 수집 방법 선택</span><span class="sxs-lookup"><span data-stu-id="1b9ca-238">Choose your Linux data collection method</span></span>
<span data-ttu-id="1b9ca-239">수집할 데이터 유형을 선택하는 방식은 OMS 포털을 사용할지 또는 자신의 Linux 클라이언트에서 다양한 구성 파일을 직접 편집할지에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-239">How you choose the data types you'd like to collect depends on whether you want to use the OMS portal or if you want edit various configuration files directly on your Linux clients.</span></span> <span data-ttu-id="1b9ca-240">포털을 사용하기로 선택하면, 구성은 사용자의 모든 Linux 클라이언트에 자동으로 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-240">If you choose to use the portal, the configuration is sent to all of your Linux clients automatically.</span></span> <span data-ttu-id="1b9ca-241">여러 Linux 클라이언트에 다른 구성이 필요하면, 클라이언트 파일을 개별적으로 편집하거나 PowerShell DSC, Chef, 또는 Puppet 같은 대안을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-241">If you need different configurations for different Linux clients, you will need to edit client files individually – or use an alternative like PowerShell DSC, Chef, or Puppet.</span></span>

<span data-ttu-id="1b9ca-242">Linux 컴퓨터의 구성 파일을 사용하여 수집할 성능 카운터와 syslog 이벤트를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-242">You can specify the syslog events and performance counters that you want to collect using configuration files on the Linux computers.</span></span> <span data-ttu-id="1b9ca-243">*에이전트 구성 파일을 편집하여 데이터 수집을 구성하기로 선택하면, 중앙 집중식 구성을 비활성화해야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="1b9ca-243">*If you chose to configure data collection by editing agent configuration files, you should disable the centralized configuration.*</span></span>  <span data-ttu-id="1b9ca-244">에이전트 구성 파일에서 데이터 수집을 구성하는 것은 물론 Linux용 OMS 에이전트 또는 개별 컴퓨터에 대해 중앙 집중식 구성을 비활성화하는 지침이 아래에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-244">Instructions are provided below to configure data collection in the agent's configuration files as well as to disable central configuration for all OMS Agents for Linux, or individual computers.</span></span>

### <a name="disable-oms-management-for-an-individual-linux-computer"></a><span data-ttu-id="1b9ca-245">개별 Linux 컴퓨터에 대한 OMS 관리 비활성화</span><span class="sxs-lookup"><span data-stu-id="1b9ca-245">Disable OMS management for an individual Linux computer</span></span>
<span data-ttu-id="1b9ca-246">구성 데이터에 대한 중앙 집중식 데이터 수집은 OMS_MetaConfigHelper.py 스크립트를 통해 개별 Linux 컴퓨터에 대해 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-246">Centralized data collection for configuration data is disabled for an individual Linux computer with the OMS_MetaConfigHelper.py script.</span></span> <span data-ttu-id="1b9ca-247">이것은 컴퓨터 하위 집합에 특별한 구성이 필요한 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-247">This can be useful if a subset of computers should have a specialized configuration.</span></span>

<span data-ttu-id="1b9ca-248">중앙 집중식 구성을 비활성화하려면:</span><span class="sxs-lookup"><span data-stu-id="1b9ca-248">To disable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

<span data-ttu-id="1b9ca-249">중앙 집중식 구성을 다시 활성화하려면:</span><span class="sxs-lookup"><span data-stu-id="1b9ca-249">To re-enable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a><span data-ttu-id="1b9ca-250">Linux 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="1b9ca-250">Linux performance counters</span></span>
<span data-ttu-id="1b9ca-251">Linux 성능 카운터는 Windows 성능 카운터와 유사합니다. 둘 다 비슷하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-251">Linux performance counters are similar to Windows performance counters—both operate similarly.</span></span> <span data-ttu-id="1b9ca-252">다음 절차를 사용하여 추가하고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-252">You can use the following procedures to add and configure them.</span></span> <span data-ttu-id="1b9ca-253">OMS에 추가되면, 30초마다 데이터가 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-253">After they are added to OMS, data is collected for them every 30 seconds.</span></span>

### <a name="to-add-a-linux-performance-counter-in-oms"></a><span data-ttu-id="1b9ca-254">OMS에서 Linux 성능 카운터를 추가하려면:</span><span class="sxs-lookup"><span data-stu-id="1b9ca-254">To add a Linux performance counter in OMS</span></span>
1. <span data-ttu-id="1b9ca-255">OMS 포털을 사용하여 Linux용 OMS 에이전트를 구성하려면, 설정 페이지에서 Linux 성능 카운터를 추가하고 **데이터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-255">To configure OMS Agents for Linux using the OMS portal, you can add Linux performance counters on the Settings page, click **Data**.</span></span>  
2. <span data-ttu-id="1b9ca-256">**데이터**의 **설정** 페이지에서, **Linux 성능 카운터**를 클릭한 다음 추가하려는 카운터의 이름을 선택하거나 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-256">On the **Settings** page under **Data** , click **Linux performance counters** and then select or type the name of the counter you want to add.</span></span>  
    <span data-ttu-id="1b9ca-257">![데이터](./media/log-analytics-linux-agents/oms-settings-data01.png)</span><span class="sxs-lookup"><span data-stu-id="1b9ca-257">![data](./media/log-analytics-linux-agents/oms-settings-data01.png)</span></span>
3. <span data-ttu-id="1b9ca-258">카운터의 전체 이름을 모르는 경우, 이름의 일부를 입력하기 시작하면 사용 가능한 카운터 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-258">If you don't know the full name of the counter, you can start typing a partial name and a list of available counters will appear.</span></span> <span data-ttu-id="1b9ca-259">추가할 카운터를 발견하면, 목록에서 이름을 클릭한 다음 더하기 아이콘을 클릭하여 카운터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-259">When you find the counter you want to add, click the name in the list and then click the plus icon to add the counter.</span></span>
4. <span data-ttu-id="1b9ca-260">카운터를 추가하면, 카운터 목록에 컬러 막대로 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-260">After you add the counter, it appears in the list of counters highlighted with a colored bar.</span></span>
5. <span data-ttu-id="1b9ca-261">**Apply below configuration to my machines** (내 컴퓨터에 아래 구성 적용) 옵션은 기본적으로 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-261">By default, the **Apply below configuration to my machines** option is selected.</span></span> <span data-ttu-id="1b9ca-262">구성 데이터 보내기를 비활성화하려면, 이 선택을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-262">If you want to disable sending configuration data, clear the selection.</span></span>
6. <span data-ttu-id="1b9ca-263">성능 카운터 수정을 완료하면, 페이지 맨 아래에서 **저장** 을 클릭하여 변경을 마무리합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-263">When you are done modifying performance counters, at the bottom of the page click **Save** to finalize your changes.</span></span> <span data-ttu-id="1b9ca-264">그러면 변경한 구성 내용이 OMS에 등록된 모든 Linux용 OMS 에이전트로 보내집니다(일반적으로 5분 이내).</span><span class="sxs-lookup"><span data-stu-id="1b9ca-264">The configuration changes that you've made are then sent to all the OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-performance-counters-in-oms"></a><span data-ttu-id="1b9ca-265">OMS에서 Linux 성능 카운터 구성</span><span class="sxs-lookup"><span data-stu-id="1b9ca-265">Configure Linux performance counters in OMS</span></span>
<span data-ttu-id="1b9ca-266">Windows 성능 카운터의 경우, 각 성능 카운터에 대해 특정 인스턴스를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-266">For Windows performance counters, you can choose a specific instance for each performance counter.</span></span> <span data-ttu-id="1b9ca-267">하지만 Linux 성능 카운터의 경우, 어떤 카운터 인스턴스를 선택하든, 부모 카운터의 모든 자식 카운터에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-267">However, for Linux performance counters, whatever instance of a counter that you choose applies to all child counters of the parent counter.</span></span> <span data-ttu-id="1b9ca-268">다음 테이블은 Linux와 Windows 성능 카운터 모두에서 사용할 수 있는 공통 인스턴스를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-268">The following table shows the common instances available to both Linux and Windows performance counters.</span></span>

| <span data-ttu-id="1b9ca-269">**인스턴스 이름**</span><span class="sxs-lookup"><span data-stu-id="1b9ca-269">**Instance name**</span></span> | <span data-ttu-id="1b9ca-270">**의미**</span><span class="sxs-lookup"><span data-stu-id="1b9ca-270">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="1b9ca-271">\_합계</span><span class="sxs-lookup"><span data-stu-id="1b9ca-271">\_Total</span></span> |<span data-ttu-id="1b9ca-272">모든 인스턴스의 총계</span><span class="sxs-lookup"><span data-stu-id="1b9ca-272">Total of all the instances</span></span> |
| \* |<span data-ttu-id="1b9ca-273">모든 인스턴스</span><span class="sxs-lookup"><span data-stu-id="1b9ca-273">All instances</span></span> |
| <span data-ttu-id="1b9ca-274">(/&#124;/var)</span><span class="sxs-lookup"><span data-stu-id="1b9ca-274">(/&#124;/var)</span></span> |<span data-ttu-id="1b9ca-275">/ 또는 /var로 명명된 인스턴트와 일치</span><span class="sxs-lookup"><span data-stu-id="1b9ca-275">Matches instances named: / or /var</span></span> |

<span data-ttu-id="1b9ca-276">마찬가지로, 부모 카운터에 대해 선택한 샘플 간격은 모든 자식 카운터에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-276">Similarly, the sample interval that you choose for a parent counter applies to all its child counters.</span></span> <span data-ttu-id="1b9ca-277">즉, 모든 자식 카운터 샘플 간격 및 인스턴스는 함께 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-277">In other words, all the child counter sample intervals and instances are tied together.</span></span>

### <a name="add-and-configure-performance-metrics-with-linux"></a><span data-ttu-id="1b9ca-278">Linux에서 성능 메트릭 추가 및 구성</span><span class="sxs-lookup"><span data-stu-id="1b9ca-278">Add and configure performance metrics with Linux</span></span>
<span data-ttu-id="1b9ca-279">수집할 성능 메트릭은 /etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf의 구성으로 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-279">Performance metrics to collect are controlled by the configuration in /etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf.</span></span> <span data-ttu-id="1b9ca-280">Linux 용 OMS 에이전트에 사용할 수 있는 클래스 및 메트릭은 [Available performance metrics](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) (사용 가능한 성능 메트릭)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-280">See [Available performance metrics](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) for available classes and metrics for the OMS Agent for Linux.</span></span>

<span data-ttu-id="1b9ca-281">수집할 성능 메트릭의 각 개체나 범주는 구성 파일 내에 단일 `<source>` 요소로 정의되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-281">Each object, or category, of performance metrics to collect should be defined in the configuration file as a single `<source>` element.</span></span> <span data-ttu-id="1b9ca-282">구문은 아래와 같은 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-282">The syntax follows the pattern below.</span></span>

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

<span data-ttu-id="1b9ca-283">이 요소에서 구성할 수 있는 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-283">The configurable parameters of this element are:</span></span>

* <span data-ttu-id="1b9ca-284">**Object\_name**: 수집하는 개체의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-284">**Object\_name**: the object name for the collection.</span></span>
* <span data-ttu-id="1b9ca-285">**Instance\_regex**: 수집할 인스턴스를 정의하는 *정규식*입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-285">**Instance\_regex**: a *regular expression* defining which instances to collect.</span></span> <span data-ttu-id="1b9ca-286">`.*` 값은 모든 인스턴스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-286">The value: `.*` specifies all instances.</span></span> <span data-ttu-id="1b9ca-287">\_Total 인스턴스에 대해서만 프로세서 메트릭을 수집하려면 `_Total`을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-287">To collect processor metrics for only the \_Total instance, you could specify `_Total`.</span></span> <span data-ttu-id="1b9ca-288">crond 또는 sshd 인스턴스에 대해서만 프로세서 메트릭을 수집하려면 `(crond|sshd)`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-288">To collect process metrics for only the crond or sshd instances, you could specify: `(crond|sshd)`.</span></span>
* <span data-ttu-id="1b9ca-289">**Counter\_name\_regex**: 수집할 (개체에 대한) 카운터를 정의하는 *정규식*입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-289">**Counter\_name\_regex**: a *regular expression* defining which counters (for the object) to collect.</span></span> <span data-ttu-id="1b9ca-290">개체에 대한 모든 카운터를 수집하려면 `.*`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-290">To collect all counters for the object, specify: `.*`.</span></span> <span data-ttu-id="1b9ca-291">메모리 개체에 대한 스왑 공간 카운터만 수집하려면 `.+Swap.+`</span><span class="sxs-lookup"><span data-stu-id="1b9ca-291">To collect only swap space counters for the memory object, you could specify: `.+Swap.+`</span></span>
* <span data-ttu-id="1b9ca-292">**Interval:**: 개체의 카운터가 수집되는 빈도입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-292">**Interval:**: the frequency at which the object's counters are collected.</span></span>

<span data-ttu-id="1b9ca-293">성능 메트릭에 대한 기본 구성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-293">The default configuration for performance metrics is:</span></span>

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

### <a name="enable-mysql-performance-counters-using-linux-commands"></a><span data-ttu-id="1b9ca-294">Linux 명령을 사용하여 MySQL 성능 카운터 활성화</span><span class="sxs-lookup"><span data-stu-id="1b9ca-294">Enable MySQL performance counters using Linux commands</span></span>
<span data-ttu-id="1b9ca-295">omsagent 번들이 설치된 경우 컴퓨터에서 MySQL 서버나 MariaDB 서버가 감지되면, MySQL 서버용 성능 모니터링 공급자가 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-295">If MySQL Server or MariaDB Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for MySQL Server is automatically installed.</span></span> <span data-ttu-id="1b9ca-296">이 공급자는 성능 통계를 공개하기 위해 로컬 MySQL/MariaDB 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-296">This provider connects to the local MySQL/MariaDB server to expose performance statistics.</span></span> <span data-ttu-id="1b9ca-297">공급자가 MySQL 서버에 액세스할 수 있도록 MySQL 사용자 자격 증명을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-297">You need to configure MySQL user credentials so that the provider can access the MySQL Server.</span></span>

<span data-ttu-id="1b9ca-298">localhost에서 MySQL 서버의 기본 사용자 계정을 정의하려면 다음 명령 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-298">To define a default user account for the MySQL server on localhost, use the following command example.</span></span>

> [!NOTE]
> <span data-ttu-id="1b9ca-299">자격 증명 파일은 omsagent 계정이 읽을 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-299">The credentials file must be readable by the omsagent account.</span></span> <span data-ttu-id="1b9ca-300">omsgent로 mycimprovauth 명령을 실행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-300">Running the mycimprovauth command as omsgent is recommended.</span></span>
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


<span data-ttu-id="1b9ca-301">또는 /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth 파일을 생성하여, 필요한 MySQL 자격 증명을 파일 내에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-301">Alternatively, you can specify the required MySQL credentials in a file, by creating the file: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth.</span></span> <span data-ttu-id="1b9ca-302">mysql-auth 파일을 통해 모니터링을 위한 MySQL 자격 증명을 관리하는 방법에 대한 자세한 내용은 [Manage MySQL monitoring credentials in the authentication file](#manage-mysql-monitoring-credentials-in-the-authentication-file)(인증 파일에서 MySQL 모니터링 자격 증명 관리)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-302">For more information about managing MySQL credentials for monitoring through the mysql-auth file, see [Manage MySQL monitoring credentials in the authentication file](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span></span>

<span data-ttu-id="1b9ca-303">MySQL 서버 성능 데이터를 수집하기 위해 MySQL 사용자에게 필요한 개체 권한에 대한 자세한 내용은 [Database permissions required for MySQL performance counters](#database-permissions-required-for-mysql-performance-counters) (MySQL 성능 카운터에 필요한 데이터베이스 권한)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-303">See [Database permissions required for MySQL performance counters](#database-permissions-required-for-mysql-performance-counters) for details about object permissions required by the MySQL user to collect MySQL Server performance data.</span></span>

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a><span data-ttu-id="1b9ca-304">Linux 명령을 사용하여 Apache HTTP 서버 성능 카운터 활성화</span><span class="sxs-lookup"><span data-stu-id="1b9ca-304">Enable Apache HTTP Server performance counters using Linux commands</span></span>
<span data-ttu-id="1b9ca-305">omsagent 번들이 설치된 경우 컴퓨터에서 Apache HTTP 서버가 감지되면, Apache HTTP 서버용 성능 모니터링 공급자가 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-305">If Apache HTTP Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server is automatically installed.</span></span> <span data-ttu-id="1b9ca-306">이 공급자는 성능 데이터에 액세스하기 위해 Apache HTTP 서버에 로드되어야 하는 Apache "모듈"에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-306">This provider relies on an Apache "module" that must be loaded into the Apache HTTP Server in order to access performance data.</span></span>

<span data-ttu-id="1b9ca-307">모듈은 다음 명령을 사용하여 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-307">You can load the module with the following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="1b9ca-308">Apache 모니터링 모듈을 언로드하려면, 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-308">To unload the Apache monitoring module, run the following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="to-view-performance-data-with-log-analytics"></a><span data-ttu-id="1b9ca-309">Log Analytics에서 성능 데이터를 보려면</span><span class="sxs-lookup"><span data-stu-id="1b9ca-309">To view performance data with Log Analytics</span></span>
1. <span data-ttu-id="1b9ca-310">Operations Management Suite 포털에서 로그 검색 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-310">In the Operations Management Suite portal, click the Log Search tile.</span></span>
2. <span data-ttu-id="1b9ca-311">모든 성능 카운터를 보려면, 검색 창에 `* (Type=Perf)` 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-311">In the search bar, type `* (Type=Perf)` to view all performance counters.</span></span>

<span data-ttu-id="1b9ca-312">OMS는 Windows 성능 카운터 데이터도 수집하기 때문에 Linux에 해당하는 데이터로 검색 범위를 좁혀야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-312">Because OMS also collects Windows performance counter data, you should scope-down the search to Linux-specific data.</span></span> <span data-ttu-id="1b9ca-313">다음 예제는 Chorizo21이라는 이름의 예제 Linux 서버에 해당하는 성능 데이터를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-313">So, the following example would show performance data specific to an example Linux server named Chorizo21.</span></span>

```
Type=Perf Computer=chorizo*
```

![검색 결과에 표시된 예제 서버](./media/log-analytics-linux-agents/oms-perfsearch01.png)

<span data-ttu-id="1b9ca-315">결과에서 **메트릭** 을 클릭하면 데이터가 수집된 카운터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-315">In the results, you can click **Metrics** to view the counters that data was collected for.</span></span> <span data-ttu-id="1b9ca-316">각 카운터에 대한 실시간 데이터가 그래프로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-316">Real-time data is shown as graphs for each counter.</span></span>

![메트릭](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a><span data-ttu-id="1b9ca-318">syslog</span><span class="sxs-lookup"><span data-stu-id="1b9ca-318">Syslog</span></span>
<span data-ttu-id="1b9ca-319">Syslog는 Windows 이벤트 로그와 유사한 이벤트 기록 프로토콜입니다. OMS에 표시되면 둘 다 유사하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-319">Syslog is an event logging protocol similar to Windows Event logs—both operate similarly when displayed in OMS.</span></span>

### <a name="to-add-a-new-linux-syslog-facility-in-oms"></a><span data-ttu-id="1b9ca-320">OMS에서 새 Linux syslog 기능을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="1b9ca-320">To add a new Linux syslog facility in OMS</span></span>
1. <span data-ttu-id="1b9ca-321">**데이터**의 **설정** 페이지에서, **Syslog**를 클릭한 다음 더하기 아이콘 왼쪽에 추가할 syslog 기능의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-321">On the **Settings** page under **Data** , click **Syslog** and then to the left of the plus icon, type the name of the syslog facility that you want to add.</span></span>
    <span data-ttu-id="1b9ca-322">![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span><span class="sxs-lookup"><span data-stu-id="1b9ca-322">![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span></span>
2. <span data-ttu-id="1b9ca-323">기능의 전체 이름을 모르는 경우, 이름의 일부를 입력하기 시작하면 사용 가능한 syslog 기능 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-323">If you don’t know the full name of the facility, you can start typing a partial name and a list of available syslog facilities will appear.</span></span> <span data-ttu-id="1b9ca-324">추가할 syslog 기능을 발견하면, 목록에서 이름을 클릭한 다음 더하기 아이콘을 클릭하여 syslog 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-324">When you find the syslog facility that you want to add, click the name in the list and then click the plus icon to add the syslog facility.</span></span>
3. <span data-ttu-id="1b9ca-325">기능을 추가하면, 컬러 막대로 강조 표시된 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-325">After you add the facility, it appears in the list of highlighted with a colored bar.</span></span> <span data-ttu-id="1b9ca-326">다음으로 수집할 심각도(syslog 기능 범주 정보)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-326">Next, choose the severities (categories of syslog facility information) that you want to collect.</span></span>
4. <span data-ttu-id="1b9ca-327">페이지 맨 아래에서 **저장** 을 클릭하여 변경을 마무리합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-327">At the bottom of the page click **Save** to finalize your changes.</span></span> <span data-ttu-id="1b9ca-328">그러면 변경한 구성 내용이 OMS에 등록된 모든 Linux용 OMS 에이전트로 보내집니다(일반적으로 5분 이내).</span><span class="sxs-lookup"><span data-stu-id="1b9ca-328">The configuration changes that you’ve made are then sent to all the OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-syslog-facilities-in-linux"></a><span data-ttu-id="1b9ca-329">Linux에서 Linux syslog 기능 구성</span><span class="sxs-lookup"><span data-stu-id="1b9ca-329">Configure Linux syslog facilities in Linux</span></span>
<span data-ttu-id="1b9ca-330">Syslog 이벤트는 Syslog 디먼(예 rsyslog 또는 syslog-ng)에서 에이전트가 수신 대기 중인 로컬 포트로 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-330">Syslog events are sent from the syslog daemon, for example rsyslog or syslog-ng, to a local port that the agent is listening on.</span></span> <span data-ttu-id="1b9ca-331">기본 포트는 25224입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-331">By default, port 25224.</span></span> <span data-ttu-id="1b9ca-332">에이전트가 설치될 때 기본 syslog 구성이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-332">When the agent is installed, a default syslog configuration is applied.</span></span> <span data-ttu-id="1b9ca-333">위치는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-333">This is found at:</span></span>

<span data-ttu-id="1b9ca-334">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span><span class="sxs-lookup"><span data-stu-id="1b9ca-334">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span></span>

<span data-ttu-id="1b9ca-335">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span><span class="sxs-lookup"><span data-stu-id="1b9ca-335">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span></span>

<span data-ttu-id="1b9ca-336">기본 OMS 에이전트 syslog 구성은 심각도가 경고 이상인 모든 기능의 syslog 이벤트를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-336">The default OMS agent syslog configuration uploads syslog events from all facilities with a severity of warning or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="1b9ca-337">Syslog 구성을 편집하는 경우, 변경 내용을 적용하려면 syslog 디먼을 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-337">If you edit the syslog configuration, you must restart the syslog daemon for the changes to take effect.</span></span>
>
>

<span data-ttu-id="1b9ca-338">OMS의 Linux 용 OMS 에이전트에 대한 기본 syslog 구성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-338">The default syslog configuration for the OMS Agent for Linux for OMS is:</span></span>

#### <a name="rsyslog"></a><span data-ttu-id="1b9ca-339">Rsyslog</span><span class="sxs-lookup"><span data-stu-id="1b9ca-339">Rsyslog</span></span>
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

#### <a name="syslog-ng"></a><span data-ttu-id="1b9ca-340">Syslog-ng</span><span class="sxs-lookup"><span data-stu-id="1b9ca-340">Syslog-ng</span></span>
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="to-view-all-syslog-events-with-log-analytics"></a><span data-ttu-id="1b9ca-341">Log Analytics에서 모든 Syslog 이벤트를 보려면</span><span class="sxs-lookup"><span data-stu-id="1b9ca-341">To view all Syslog events with Log Analytics</span></span>
1. <span data-ttu-id="1b9ca-342">Operations Management Suite 포털에서 **로그 검색** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-342">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="1b9ca-343">**로그 관리** 그룹화에서 미리 정의된 syslog 검색을 선택한 다음 실행할 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-343">In the **Log Management** grouping, choose a predefined syslog search and then select one to run it.</span></span>

<span data-ttu-id="1b9ca-344">이 예제는 모든 Syslog 이벤트를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-344">This example shows all Syslog events.</span></span>

![로그 검색에 표시된 Syslog 이벤트](./media/log-analytics-linux-agents/oms-linux-syslog.png)

<span data-ttu-id="1b9ca-346">이제 검색 결과를 세부적으로 들여다 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-346">Now you can drill into search results.</span></span>

## <a name="linux-alerts"></a><span data-ttu-id="1b9ca-347">Linux 경고</span><span class="sxs-lookup"><span data-stu-id="1b9ca-347">Linux alerts</span></span>
<span data-ttu-id="1b9ca-348">Nagios 또는 Zabbix를 사용하여 Linux 컴퓨터를 관리하는 경우라면, OMS는 이런 도구에서 생성되는 경고를 수신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-348">If you use Nagios or Zabbix to manage your Linux machines, then OMS can receive the alerts generated from those tools.</span></span> <span data-ttu-id="1b9ca-349">하지만, OMS 포털을 사용하여 들어오는 경고 데이터를 구성하는 방법이 현재는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-349">However, there is currently no method to configure incoming alert data using the OMS portal.</span></span> <span data-ttu-id="1b9ca-350">대신, OMS에 경고 보내기를 시작하도록 구성 파일을 편집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-350">Instead, you will need to edit a config file to start sending alerts to OMS.</span></span>

### <a name="collect-alerts-from-nagios"></a><span data-ttu-id="1b9ca-351">Nagios의 경고 수집</span><span class="sxs-lookup"><span data-stu-id="1b9ca-351">Collect alerts from Nagios</span></span>
<span data-ttu-id="1b9ca-352">Nagios 서버의 경고를 수집하려면, 다음 구성을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-352">To collect alerts from a Nagios server, you need to make the following configuration changes.</span></span>

1. <span data-ttu-id="1b9ca-353">**omsagent** 사용자에게 Nagios 로그 파일(예: /var/log/nagios/nagios.log)에 대한 읽기 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-353">Grant the user **omsagent** read access to the Nagios log file (i.e. /var/log/nagios/nagios.log).</span></span> <span data-ttu-id="1b9ca-354">nagios.log 파일이 **nagios** 그룹의 소유라는 가정 하에, **omsagent** 사용자를 **nagios** 그룹에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-354">Assuming the nagios.log file is owned by the group **nagios** , you can add the user **omsagent** to the **nagios** group.</span></span>

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. <span data-ttu-id="1b9ca-355">omsagent.conf 구성 파일(/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf)을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-355">Modify the omsagent.confconfiguration file (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf).</span></span> <span data-ttu-id="1b9ca-356">다음 항목이 포함되고 주석 처리되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-356">Ensure the following entries are present and not commented out:</span></span>

    ```
    <source>
    type tail
    #Update path to point to your nagios.log
    path /var/log/nagios/nagios.log
    format none
    tag oms.nagios
    </source>

    <filter oms.nagios>
    type filter_nagios_log
    </filter>
    ```
3. <span data-ttu-id="1b9ca-357">omsagent 디먼을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-357">Restart the omsagent daemon:</span></span>

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a><span data-ttu-id="1b9ca-358">Zabbix의 경고 수집</span><span class="sxs-lookup"><span data-stu-id="1b9ca-358">Collect alerts from Zabbix</span></span>
<span data-ttu-id="1b9ca-359">Zabbix 서버의 경고를 수집하려면 위의 Nagios와 유사한 단계를 수행합니다. 단, 사용자 및 암호를 *일반 텍스트*로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-359">To collect alerts from a Zabbix server, you'll perform similar steps to those for Nagios above, except you'll need to specify a user and password in *clear text*.</span></span> <span data-ttu-id="1b9ca-360">바람직하지는 않지만 곧 변경될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-360">This is not ideal, but will likely change soon.</span></span> <span data-ttu-id="1b9ca-361">이 문제에 대처하려면, 사용자를 생성하고 모니터링 권한만 부여하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-361">To address this issue, we recommend that you create the user and grant it permission to monitor only.</span></span>

<span data-ttu-id="1b9ca-362">Zabbix용 omsagent.conf 구성 파일(/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf)의 예제 섹션은 다음과 비슷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-362">An example section of the omsagent.conf configuration file  (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf) for Zabbix should resemble the following:</span></span>

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

### <a name="view-alerts-in-log-analytics-search"></a><span data-ttu-id="1b9ca-363">Log Analytics 검색에서 경고 보기</span><span class="sxs-lookup"><span data-stu-id="1b9ca-363">View alerts in Log Analytics search</span></span>
<span data-ttu-id="1b9ca-364">OMS에 경고를 보내도록 Linux 컴퓨터를 구성한 후에, 몇 가지 간단한 로그 검색 쿼리를 사용하여 경고를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-364">After you've configured your Linux computers to send alerts to OMS, you can use a few simple log search queries to view the alerts.</span></span> <span data-ttu-id="1b9ca-365">다음 검색 쿼리 예제는 생성되어 기록된 모든 경고를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-365">The following search query example returns all the recorded alerts that were generated.</span></span> <span data-ttu-id="1b9ca-366">예를 들어, IT 인프라 내에서 어떤 문제가 발생하면, 다음 예제 쿼리의 결과는 문제가 발생했을 만한 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-366">For example, if some sort of problem occurs in your IT infrastructure, then results for the following example query might indicate where the problem might originate.</span></span> <span data-ttu-id="1b9ca-367">그러면, 원본 시스템의 경고를 손쉽게 세부적으로 들여다 보고 조사 범위를 좁힐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-367">And, you can easily drill in to the alerts by source system to help narrow your investigation.</span></span> <span data-ttu-id="1b9ca-368">장점은 처음부터 다양한 관리 시스템으로 이동할 필요가 없다는 점입니다. 경고가 OMS로 보내지기만 한다면, OMS에서 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-368">The benefit is that you don't necessarily have to go to various management systems from the start—provided that your alerts are sent to OMS, you can start there.</span></span>

```
Type=Alert
```

#### <a name="to-view-all-nagios-alerts-with-log-analytics"></a><span data-ttu-id="1b9ca-369">Log Analytics에서 모든 Nagios 경고를 보려면</span><span class="sxs-lookup"><span data-stu-id="1b9ca-369">To view all Nagios alerts with Log Analytics</span></span>
1. <span data-ttu-id="1b9ca-370">Operations Management Suite 포털에서 **로그 검색** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-370">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="1b9ca-371">쿼리 표시줄에 다음 검색 쿼리를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-371">In the query bar, type the following search query</span></span>

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![로그 검색에 표시된 Nagios 경고](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

<span data-ttu-id="1b9ca-373">검색 결과를 본 다음, *AlertState*같은 추가적인 세부 정보를 들여다 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-373">After you see the search results, you can drill into additional details such as *AlertState*.</span></span>

### <a name="to-view-all-zabbix-alerts-with-log-analytics"></a><span data-ttu-id="1b9ca-374">Log Analytics에서 모든 Zabbix 경고를 보려면</span><span class="sxs-lookup"><span data-stu-id="1b9ca-374">To view all Zabbix alerts with Log Analytics</span></span>
1. <span data-ttu-id="1b9ca-375">Operations Management Suite 포털에서 **로그 검색** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-375">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="1b9ca-376">쿼리 표시줄에 다음 검색 쿼리를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-376">In the query bar, type the following search query</span></span>

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![로그 검색에 표시된 Zabbix 경고](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

<span data-ttu-id="1b9ca-378">검색 결과를 본 다음, *AlertName*같은 추가적인 세부 정보를 들여다 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-378">After you see the search results, you can drill into additional details such as *AlertName*.</span></span>

## <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="1b9ca-379">System Center Operations Manager와의 호환성</span><span class="sxs-lookup"><span data-stu-id="1b9ca-379">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="1b9ca-380">Linux 용 OMS 에이전트는 System Center Operations Manager 에이전트와 에이전트 바이너리를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-380">The OMS Agent for Linux shares agent binaries with the System Center Operations Manager agent.</span></span> <span data-ttu-id="1b9ca-381">Operations Manager로 관리되는 시스템에 Linux용 OMS 에이전트를 설치하면, 컴퓨터의 OMI 및 SCX 패키지가 새 버전으로 업그레이드됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-381">Installing the OMS Agent for Linux on a system currently managed by Operations Manager upgrades the OMI and SCX packages on the computer to a newer version.</span></span> <span data-ttu-id="1b9ca-382">Linux용 OMS 에이전트와 System Center 2012 R2는 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-382">The OMS Agent for Linux and System Center 2012 R2 are compatible.</span></span> <span data-ttu-id="1b9ca-383">하지만, **System Center 2012 SP1 이전 버전은 현재 Linux용 OMS 에이전트와 호환되거나 지원되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="1b9ca-383">However, **System Center 2012 SP1 and earlier versions are currently not compatible or supported with the OMS Agent for Linux.**</span></span>

> [!NOTE]
> <span data-ttu-id="1b9ca-384">Operations Manager로 관리되지 않는 컴퓨터에 Linux용 OMS 에이전트를 설치한 다음, 나중에 Operations Manager로 컴퓨터를 관리하려는 경우에는, 컴퓨터를 검색하기 전에 OMI 구성을 반드시 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-384">If the OMS Agent for Linux is installed to a computer that is not currently managed by Operations Manager, and you later want to manage the computer with Operations Manager, you must modify the OMI configuration before you discover the computer.</span></span> <span data-ttu-id="1b9ca-385">**Operations Manager 에이전트가 Linux용 OMS 에이전트보다 먼저 설치되면 이 단계가 필요하지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="1b9ca-385">**This step is not needed if the Operations Manager agent is installed before the OMS Agent for Linux.**</span></span>
>
>

### <a name="to-enable-the-oms-agent-for-linux-to-communicate-with-operations-manager"></a><span data-ttu-id="1b9ca-386">Linux용 OMS 에이전트가 Operations Manager와 통신하도록 설정하려면</span><span class="sxs-lookup"><span data-stu-id="1b9ca-386">To enable the OMS Agent for Linux to communicate with Operations Manager</span></span>
1. <span data-ttu-id="1b9ca-387">/etc/opt/omi/conf/omiserver.conf 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-387">Edit the file /etc/opt/omi/conf/omiserver.conf</span></span>
2. <span data-ttu-id="1b9ca-388">**httpsport=** 로 시작되는 줄이 1270 포트를 지정하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-388">Ensure that the line beginning with **httpsport=** defines the port 1270.</span></span> <span data-ttu-id="1b9ca-389">예: `httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="1b9ca-389">Such as `httpsport=1270`</span></span>
3. <span data-ttu-id="1b9ca-390">OMI 서버를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-390">Restart the OMI server:</span></span>

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="1b9ca-391">Database permissions required for MySQL performance counters</span><span class="sxs-lookup"><span data-stu-id="1b9ca-391">Database permissions required for MySQL performance counters</span></span>
<span data-ttu-id="1b9ca-392">MySQL 모니터링 사용자에게 권한을 부여하려면, 권한을 부여하는 사용자에게 'GRANT option' 권한은 물론 부여되는 권한에 대한 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-392">To grant permissions to a MySQL monitoring user, the granting user must have the 'GRANT option' privilege as well as the privilege being granted.</span></span>

<span data-ttu-id="1b9ca-393">MySQL 사용자가 성능 데이터를 반환하려면 해당 사용자는 다음 쿼리에 대한 액세스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-393">In order for the MySQL User to return performance data the user will need access to the following queries:</span></span>

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

<span data-ttu-id="1b9ca-394">이러한 쿼리 외에, MySQL 사용자는 다음과 같은 기본 테이블에 대해 SELECT 액세스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-394">In addition to these queries the MySQL user requires SELECT access to the following default tables:</span></span>

* <span data-ttu-id="1b9ca-395">information_schema</span><span class="sxs-lookup"><span data-stu-id="1b9ca-395">information_schema</span></span>
* <span data-ttu-id="1b9ca-396">mysql</span><span class="sxs-lookup"><span data-stu-id="1b9ca-396">mysql</span></span>

<span data-ttu-id="1b9ca-397">이러한 권한은 다음과 같은 권한 부여 명령을 실행하여 부여될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-397">These privileges can be granted by running the following grant commands.</span></span>

```
GRANT SELECT ON information_schema.* TO ‘monuser’@’localhost’;
GRANT SELECT ON mysql.* TO ‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-the-authentication-file"></a><span data-ttu-id="1b9ca-398">Manage MySQL monitoring credentials in the authentication file</span><span class="sxs-lookup"><span data-stu-id="1b9ca-398">Manage MySQL monitoring credentials in the authentication file</span></span>
<span data-ttu-id="1b9ca-399">다음 섹션은 MySQL 자격 증명을 관리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-399">The following sections help you manage MySQL credentials.</span></span>

### <a name="configure-the-mysql-omi-provider"></a><span data-ttu-id="1b9ca-400">MySQL OMI 공급자 구성</span><span class="sxs-lookup"><span data-stu-id="1b9ca-400">Configure the MySQL OMI provider</span></span>
<span data-ttu-id="1b9ca-401">MySQL OMI 공급자가 MySQL 인스턴스의 성능/상태 정보를 쿼리하려면, 미리 정의된 MySQL 사용자와 설치되어 있는 MySQL 클라이언트 라이브러리가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-401">The MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order to query the performance/health information from the MySQL instance.</span></span>

### <a name="mysql-omi-authentication-file"></a><span data-ttu-id="1b9ca-402">MySQL OMI 인증 파일</span><span class="sxs-lookup"><span data-stu-id="1b9ca-402">MySQL OMI authentication file</span></span>
<span data-ttu-id="1b9ca-403">MySQL OMI 공급자는 인증 파일을 사용하여 MySQL 인스턴스가 수신 대기할 바인딩 주소와 포트를 결정하고 메트릭 수집에 사용할 자격 증명을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-403">MySQL OMI provider uses an authentication file to determine what bind-address and port the MySQL instance is listening on and what credentials to use to gather metrics.</span></span> <span data-ttu-id="1b9ca-404">설치하는 동안 MySQL OMI 공급자는 MySQL my.cnf 구성 파일(기본 위치)에서 바인딩 주소와 포트를 검색하고, MySQL OMI 인증 파일을 부분적으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-404">During installation the MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set the MySQL OMI authentication file.</span></span>

<span data-ttu-id="1b9ca-405">MySQL 서버 인스턴스에 대한 모니터링을 완료하려면, 미리 생성된 MySQL OMI 인증 파일을 올바른 디렉터리에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-405">To complete monitoring of a MySQL server instance, add a pre-generated MySQL OMI authentication file into the correct directory.</span></span>

### <a name="authentication-file-format"></a><span data-ttu-id="1b9ca-406">인증 파일 형식</span><span class="sxs-lookup"><span data-stu-id="1b9ca-406">Authentication file format</span></span>
<span data-ttu-id="1b9ca-407">MySQL OMI 인증 파일은 다음 항목에 대한 정보를 포함하는 텍스트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-407">The MySQL OMI authentication file is a text file that contains information about:</span></span>

* <span data-ttu-id="1b9ca-408">포트</span><span class="sxs-lookup"><span data-stu-id="1b9ca-408">Port</span></span>
* <span data-ttu-id="1b9ca-409">바인딩 주소</span><span class="sxs-lookup"><span data-stu-id="1b9ca-409">Bind-Address</span></span>
* <span data-ttu-id="1b9ca-410">MySQL 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="1b9ca-410">MySQL username</span></span>
* <span data-ttu-id="1b9ca-411">Base64로 인코딩된 암호</span><span class="sxs-lookup"><span data-stu-id="1b9ca-411">Base64 encoded password</span></span>

<span data-ttu-id="1b9ca-412">MySQL OMI 인증 파일은 파일을 생성한 Linux 사용자에게만 읽기/쓰기 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-412">The MySQL OMI authentication file only grants privileges for read/write to the Linux user that generated it.</span></span>

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

<span data-ttu-id="1b9ca-413">기본 MySQL OMI 인증 파일은 MySQL 구성 파일에서 찾은 정보 중 사용이 가능하고 구문 분석된 정보에 따라 기본 인스턴스 및 포트 번호를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-413">A default MySQL OMI authentication file contains a default instance and a port number depending on what information is available and parsed from the found MySQL configuration file.</span></span>

<span data-ttu-id="1b9ca-414">기본 인스턴스는 하나의 Linux 호스트에서 여러 개의 MySQL 인스턴스를 쉽게 관리하도록 만드는 수단이며, 포트가 0인 인스턴스로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-414">The default instance is a means to make managing multiple MySQL instances on one Linux host easier, and is denoted by the instance with port 0.</span></span> <span data-ttu-id="1b9ca-415">추가된 모든 인스턴스는 기본 인스턴스로부터 속성 집합을 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-415">All added instances will inherit properties set from the default instance.</span></span> <span data-ttu-id="1b9ca-416">예를 들어, '3308' 포드에서 수신 대기 중인 MySQL 인스턴스가 추가되면, 3308 포트에서 수신 대기 중인 인스턴스를 시도하고 모니터링하기 위해, 기본 인스턴스의 바인딩 주소, 사용자 이름, Base64로 인코딩된 암호가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-416">For example, if MySQL instance listening on port '3308' is added, the default instance's bind-address, username, and Base64 encoded password will be used to try and monitor the instance listening on 3308.</span></span> <span data-ttu-id="1b9ca-417">3308 포트에서 수신 대기 중인 인스턴스가 다른 주소로 바인딩되고 동일한 MySQL 사용자 이름과 암호 쌍이 사용되면, 바인딩 주소만 다시 지정하면 되고 다른 속성은 상속됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-417">If the instance on 3308 is binded to another address and uses the same MySQL username and password pair only the respecification of the bind-address is needed and the other properties will be inherited.</span></span>

<span data-ttu-id="1b9ca-418">인증 파일의 예제는 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-418">Examples of the authentication file resemble the following.</span></span>

<span data-ttu-id="1b9ca-419">기본 인스턴스 및 포트 3308 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="1b9ca-419">Default instance and instance with port 3308:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

<span data-ttu-id="1b9ca-420">기본 인스턴스 및 포트 3308 및 Base64로 인코딩된 암호가 다른 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="1b9ca-420">Default instance and instance with port 3308 + different Base 64 encoded password:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| <span data-ttu-id="1b9ca-421">**속성**</span><span class="sxs-lookup"><span data-stu-id="1b9ca-421">**Property**</span></span> | <span data-ttu-id="1b9ca-422">**설명**</span><span class="sxs-lookup"><span data-stu-id="1b9ca-422">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="1b9ca-423">포트</span><span class="sxs-lookup"><span data-stu-id="1b9ca-423">Port</span></span> |<span data-ttu-id="1b9ca-424">포트는 MySQL 인스턴스가 수신 대기 중인 현재 포트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-424">Port represents the current port the MySQL instance is listening on.</span></span>  <span data-ttu-id="1b9ca-425">포트 0은 뒤에 나오는 속성이 기본 인스턴스에 사용된다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-425">The port 0 implies that the properties following are used for default instance.</span></span> |
| <span data-ttu-id="1b9ca-426">바인딩 주소</span><span class="sxs-lookup"><span data-stu-id="1b9ca-426">Bind-Address</span></span> |<span data-ttu-id="1b9ca-427">바인딩 주소는 현재 MySQL 바인딩 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-427">the Bind Address is the current MySQL bind-address</span></span> |
| <span data-ttu-id="1b9ca-428">username</span><span class="sxs-lookup"><span data-stu-id="1b9ca-428">username</span></span> |<span data-ttu-id="1b9ca-429">MySQL 서버 인스턴스를 모니터링하는 데 사용할 MySQL 사용자의 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-429">This the username of the MySQL user you wish to use to monitor the MySQL server instance.</span></span> |
| <span data-ttu-id="1b9ca-430">Base64로 인코딩된 암호</span><span class="sxs-lookup"><span data-stu-id="1b9ca-430">Base64 encoded Password</span></span> |<span data-ttu-id="1b9ca-431">Base64로 인코딩된 MySQL 모니터링 사용자의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-431">This is the password of the MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="1b9ca-432">AutoUpdate</span><span class="sxs-lookup"><span data-stu-id="1b9ca-432">AutoUpdate</span></span> |<span data-ttu-id="1b9ca-433">MySQL OMI 공급자가 업그레이드되면 공급자는 my.cnf 파일에서 변경 내용을 검색하고 MySQL OMI 인증 파일을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-433">When the MySQL OMI Provider is upgraded the provider will rescan for changes in the my.cnf file and overwrite the MySQL OMI Authentication file.</span></span> <span data-ttu-id="1b9ca-434">MySQL OMI 인증 파일에 필요한 업데이트에 따라 이 플래그를 true 또는 false로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-434">Set this flag to true or false depending on required updates to the MySQL OMI authentication file.</span></span> |

#### <a name="authentication-file-location"></a><span data-ttu-id="1b9ca-435">인증 파일 위치</span><span class="sxs-lookup"><span data-stu-id="1b9ca-435">Authentication file location</span></span>
<span data-ttu-id="1b9ca-436">MySQL OMI 인증 파일은 다음 경로에 위치해야 하며 이름을 "mysql-auth"라고 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-436">The MySQL OMI Authentication File should be located in the following location and named "mysql-auth":</span></span>

<span data-ttu-id="1b9ca-437">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span><span class="sxs-lookup"><span data-stu-id="1b9ca-437">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span></span>

<span data-ttu-id="1b9ca-438">파일(및 auth/omsagent 디렉터리)는 omsagent 사용자가 소유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-438">The file (and auth/omsagent directory) should be owned by the omsagent user.</span></span>

## <a name="agent-logs"></a><span data-ttu-id="1b9ca-439">에이전트 로그</span><span class="sxs-lookup"><span data-stu-id="1b9ca-439">Agent logs</span></span>
<span data-ttu-id="1b9ca-440">Linux 용 OMS 에이전트 로그의 위치:</span><span class="sxs-lookup"><span data-stu-id="1b9ca-440">The logs for the OMS Agent for Linux is at:</span></span>

<span data-ttu-id="1b9ca-441">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span><span class="sxs-lookup"><span data-stu-id="1b9ca-441">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span></span>

<span data-ttu-id="1b9ca-442">omsconfig(에이전트 구성) 프로그램에 대한 Linux 용 OMS 에이전트 로그의 위치:</span><span class="sxs-lookup"><span data-stu-id="1b9ca-442">The logs for the OMS Agent for Linux for omsconfig (agent configuration) program is at:</span></span>

<span data-ttu-id="1b9ca-443">/var/opt/microsoft/omsconfig/log/</span><span class="sxs-lookup"><span data-stu-id="1b9ca-443">/var/opt/microsoft/omsconfig/log/</span></span>

<span data-ttu-id="1b9ca-444">OMI 및 SCX 구성 요소(성능 메트릭 데이터를 제공하는) 로그의 위치:</span><span class="sxs-lookup"><span data-stu-id="1b9ca-444">Logs for the OMI and SCX components (which provide performance metrics data) is at:</span></span>

<span data-ttu-id="1b9ca-445">/var/opt/omi/log/ and /var/opt/microsoft/scx/log</span><span class="sxs-lookup"><span data-stu-id="1b9ca-445">/var/opt/omi/log/ and /var/opt/microsoft/scx/log</span></span>

## <a name="troubleshooting-the-oms-agent-for-linux"></a><span data-ttu-id="1b9ca-446">Linux 용 OMS 에이전트 문제 해결</span><span class="sxs-lookup"><span data-stu-id="1b9ca-446">Troubleshooting the OMS Agent for Linux</span></span>
<span data-ttu-id="1b9ca-447">다음 정보를 사용하여 일반적 문제를 진단 및 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-447">Use the following information to diagnose and troubleshoot common issues.</span></span>

<span data-ttu-id="1b9ca-448">이 섹션의 문제 해결 정보로 해결되지 않는 경우 다음 리소스를 사용하여 문제를 해결해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-448">If none of the troubleshooting information in this section helps you, you can also use the following resources to help resolve your problem.</span></span>

* <span data-ttu-id="1b9ca-449">프리미어 지원이 적용되는 고객의 경우 [프리미어](https://premier.microsoft.com/)를 통해 지원 사례를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-449">Customers with Premier support can log a support case via [Premier](https://premier.microsoft.com/)</span></span>
* <span data-ttu-id="1b9ca-450">Azure 지원 계약이 있는 고객은 [Azure Portal](https://manage.windowsazure.com/?getsupport=true)에서 지원 사례를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-450">Customers with Azure support agreements can log support cases in the [Azure portal](https://manage.windowsazure.com/?getsupport=true)</span></span>
* <span data-ttu-id="1b9ca-451">[GitHub 문제](https://github.com/Microsoft/OMS-Agent-for-Linux/issues) 제출</span><span class="sxs-lookup"><span data-stu-id="1b9ca-451">File a [GitHub Issue](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span></span>
* <span data-ttu-id="1b9ca-452">아이디어를 얻고 버그 보고서를 작성할 수 있는 피드백 포럼 [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span><span class="sxs-lookup"><span data-stu-id="1b9ca-452">Feedback forum for ideas and to create a bug report [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span></span>

### <a name="important-log-locations"></a><span data-ttu-id="1b9ca-453">중요 로그 위치</span><span class="sxs-lookup"><span data-stu-id="1b9ca-453">Important log locations</span></span>
| <span data-ttu-id="1b9ca-454">파일</span><span class="sxs-lookup"><span data-stu-id="1b9ca-454">File</span></span> | <span data-ttu-id="1b9ca-455">Path</span><span class="sxs-lookup"><span data-stu-id="1b9ca-455">Path</span></span> |
| --- | --- |
| <span data-ttu-id="1b9ca-456">Linux 용 OMS 에이전트 로그 파일</span><span class="sxs-lookup"><span data-stu-id="1b9ca-456">OMS Agent for Linux Log File</span></span> |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| <span data-ttu-id="1b9ca-457">OMS 에이전트 구성 로그 파일</span><span class="sxs-lookup"><span data-stu-id="1b9ca-457">OMS Agent Configuration Log File</span></span> |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a><span data-ttu-id="1b9ca-458">중요 구성 파일</span><span class="sxs-lookup"><span data-stu-id="1b9ca-458">Important configuration files</span></span>
| <span data-ttu-id="1b9ca-459">범주</span><span class="sxs-lookup"><span data-stu-id="1b9ca-459">Catergory</span></span> | <span data-ttu-id="1b9ca-460">파일 위치</span><span class="sxs-lookup"><span data-stu-id="1b9ca-460">File Location</span></span> |
| --- | --- |
| <span data-ttu-id="1b9ca-461">syslog</span><span class="sxs-lookup"><span data-stu-id="1b9ca-461">Syslog</span></span> |<span data-ttu-id="1b9ca-462">`/etc/syslog-ng/syslog-ng.conf` 또는 `/etc/rsyslog.conf` 또는 `/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="1b9ca-462">`/etc/syslog-ng/syslog-ng.conf` or `/etc/rsyslog.conf` or `/etc/rsyslog.d/95-omsagent.conf`</span></span> |
| <span data-ttu-id="1b9ca-463">성능, Nagios, Zabbix, OMS 출력 및 일반 에이전트</span><span class="sxs-lookup"><span data-stu-id="1b9ca-463">Performance, Nagios, Zabbix, OMS output and general agent</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| <span data-ttu-id="1b9ca-464">추가 구성</span><span class="sxs-lookup"><span data-stu-id="1b9ca-464">Additional configurations</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> <span data-ttu-id="1b9ca-465">OMS 포털 구성을 사용하도록 설정한 경우 시스템에서 성능 카운터 및 syslog의 편집 구성 파일을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-465">Editing configuration files for performance counters and syslog are overwritten if OMS Portal Configuration is enabled.</span></span> <span data-ttu-id="1b9ca-466">OMS 포털에서 구성을 비활성화하거나(전체 노드) 단일 노드의 경우 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-466">You can disable configuration in the OMS Portal (for all nodes) or for single nodes by running the following:</span></span>
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a><span data-ttu-id="1b9ca-467">디버그 로깅 활성화</span><span class="sxs-lookup"><span data-stu-id="1b9ca-467">Enable debug logging</span></span>
<span data-ttu-id="1b9ca-468">디버그 로깅을 활성화하려면 OMS 출력 플러그인 및 자세한 정보 출력을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-468">To enable debug logging, you can use the OMS output plugin and verbose output.</span></span>

#### <a name="oms-output-plugin"></a><span data-ttu-id="1b9ca-469">OMS 출력 플러그인</span><span class="sxs-lookup"><span data-stu-id="1b9ca-469">OMS output plugin</span></span>
<span data-ttu-id="1b9ca-470">FluentD를 사용하면 플러그인에서 입력 및 출력의 다양한 로그 수준에 대해 로깅 수준을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-470">FluentD allows the plugin to specify logging levels for different log levels for inputs and outputs.</span></span> <span data-ttu-id="1b9ca-471">OMS 출력에 대해 다른 로그 수준을 지정하려면 `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` 파일에서 일반 에이전트 구성을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-471">To specify a different log level for OMS output, edit the general agent configuration in the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` file.</span></span>

<span data-ttu-id="1b9ca-472">구성 파일 아래쪽에서 `log_level` 속성을 `info`에서 `debug`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-472">Near the bottom of the configuration file, change the `log_level` property from `info` to `debug`.</span></span>

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

<span data-ttu-id="1b9ca-473">디버그 로깅을 사용하면 OMS 서비스에 대한 배치 업로드를 형식, 데이터 항목 수, 전송 소요 시간으로 구분하여 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-473">Debug logging allows you to see batched uploads to the OMS Service separated by type, number of data items, and time taken to send.</span></span>

<span data-ttu-id="1b9ca-474">*디버그 사용 로그 예:*</span><span class="sxs-lookup"><span data-stu-id="1b9ca-474">*Example debug enabled log:*</span></span>

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a><span data-ttu-id="1b9ca-475">자세한 정보 출력</span><span class="sxs-lookup"><span data-stu-id="1b9ca-475">Verbose output</span></span>
<span data-ttu-id="1b9ca-476">OMS 출력 플러그인을 사용하는 대신 데이터 항목을 `stdout`으로 직접 출력할 수 있으며, 이 데이터 항목은 Linux용 OMS 에이전트 로그 파일에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-476">Instead of using the OMS output plugin, you can also output data items directly to `stdout`, which is visible in the OMS Agent for Linux log file.</span></span>

<span data-ttu-id="1b9ca-477">`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`의 OMS 일반 에이전트 구성 파일에서 각 라인 앞에 `#` 추가하여 OMS 출력 플러그인을 주석 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-477">In the OMS general agent configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, comment-out the OMS output plugin by adding a `#` in front of each line.</span></span>

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

<span data-ttu-id="1b9ca-478">출력 플러그인 아래에서 각 라인의 맨 앞에 있는 `#` 기호를 제거하여 다음 섹션의 주석을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-478">Below the output plugin, remove the comment in the following section by removing the `#` symbol at the beginning of each line.</span></span>

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-the-log"></a><span data-ttu-id="1b9ca-479">전달된 Syslog 메시지가 로그에 나타나지 않음</span><span class="sxs-lookup"><span data-stu-id="1b9ca-479">Forwarded Syslog messages do not appear in the log</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="1b9ca-480">가능한 원인</span><span class="sxs-lookup"><span data-stu-id="1b9ca-480">Probable causes</span></span>
* <span data-ttu-id="1b9ca-481">Linux 서버에 적용된 구성에서는 전송된 시설 및/또는 로그 수준을 수집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-481">The configuration applied to the Linux server does not allow collection of the sent facilities and/or log levels</span></span>
* <span data-ttu-id="1b9ca-482">Syslog가 Linux 서버로 올바르게 전달되지 않고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-482">Syslog is not being forwarded correctly to the Linux server</span></span>
* <span data-ttu-id="1b9ca-483">초당 전달되는 메시지 수가 너무 많아 Linux용 OMS 에이전트의 기본 구성에서 처리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-483">The number of messages being forwarded per second are too large for the base configuration of the OMS Agent for Linux to handle</span></span>

#### <a name="resolutions"></a><span data-ttu-id="1b9ca-484">해결 방법</span><span class="sxs-lookup"><span data-stu-id="1b9ca-484">Resolutions</span></span>
* <span data-ttu-id="1b9ca-485">Syslog용 OMS 포털의 구성에 모든 설비 및 올바른 로그 수준이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-485">Verify that the configuration in the OMS Portal for Syslog has all the facilities and the correct log levels</span></span>
  * <span data-ttu-id="1b9ca-486">**OMS 포털 > 설정 > 데이터 > Syslog**</span><span class="sxs-lookup"><span data-stu-id="1b9ca-486">**OMS Portal > Settings > Data > Syslog**</span></span>
* <span data-ttu-id="1b9ca-487">네이티브 syslog 메시징 디먼(`rsyslog`, `syslog-ng`)이 전달된 메시지를 수신할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-487">Verify that native syslog messaging daemons (`rsyslog`, `syslog-ng`) are able to receive the forwarded messages</span></span>
* <span data-ttu-id="1b9ca-488">Syslog 서버에서 방화벽 설정을 확인하여 메시지가 차단되지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-488">Check firewall settings on the Syslog server to ensure that messages are not being blocked</span></span>
* <span data-ttu-id="1b9ca-489">`logger` 명령을 사용하여 OMS에 대한 Syslog 메시지를 시뮬레이션합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="1b9ca-489">Simulate a Syslog message to OMS using the `logger` command - for example:</span></span>
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-to-oms-when-using-a-proxy"></a><span data-ttu-id="1b9ca-490">프록시를 사용할 때 OMS에 연결되지 않음</span><span class="sxs-lookup"><span data-stu-id="1b9ca-490">Problems connecting to OMS when using a proxy</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="1b9ca-491">가능한 원인</span><span class="sxs-lookup"><span data-stu-id="1b9ca-491">Probable causes</span></span>
* <span data-ttu-id="1b9ca-492">에이전트를 설치 및 구성할 때 지정한 프록시가 잘못되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-492">The proxy specified when installing and configuring the agent is incorrect</span></span>
* <span data-ttu-id="1b9ca-493">OMS 서비스 끝점이 데이터 센터의 허용 목록에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-493">The OMS Service endpoints are not whitelistested in your datacenter</span></span>

#### <a name="resolutions"></a><span data-ttu-id="1b9ca-494">해결 방법</span><span class="sxs-lookup"><span data-stu-id="1b9ca-494">Resolutions</span></span>
* <span data-ttu-id="1b9ca-495">다음 명령과 `-v` 옵션을 사용하여 Linux용 OMS 에이전트를 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-495">Reinstall the OMS Agent for Linux using the following command with the option `-v` enabled.</span></span> <span data-ttu-id="1b9ca-496">OMS 서비스에 대한 프록시를 통해 연결되는 에이전트의 자세한 정보를 출력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-496">This allows verbose output of the agent connecting through the proxy to the OMS Service.</span></span>
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * <span data-ttu-id="1b9ca-497">[HTTP 프록시 서버에 사용할 에이전트 구성](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)에서 OMS 프록시에 대한 문서를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-497">Review the documentation for OMS proxy at [Configuring the agent for use with an HTTP proxy server](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span></span>
* <span data-ttu-id="1b9ca-498">다음 OMS 서비스 끝점이 허용 목록에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-498">Verify that the following OMS Service endpoints are whitelisted</span></span>

| <span data-ttu-id="1b9ca-499">에이전트 리소스</span><span class="sxs-lookup"><span data-stu-id="1b9ca-499">Agent Resource</span></span> | <span data-ttu-id="1b9ca-500">포트</span><span class="sxs-lookup"><span data-stu-id="1b9ca-500">Ports</span></span> |
| --- | --- |
| <span data-ttu-id="1b9ca-501">&#42;.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="1b9ca-501">&#42;.ods.opinsights.azure.com</span></span> |<span data-ttu-id="1b9ca-502">포트 443</span><span class="sxs-lookup"><span data-stu-id="1b9ca-502">Port 443</span></span> |
| <span data-ttu-id="1b9ca-503">&#42;.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="1b9ca-503">&#42;.oms.opinsights.azure.com</span></span> |<span data-ttu-id="1b9ca-504">포트 443</span><span class="sxs-lookup"><span data-stu-id="1b9ca-504">Port 443</span></span> |
| <span data-ttu-id="1b9ca-505">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="1b9ca-505">ods.systemcenteradvisor.com</span></span> |<span data-ttu-id="1b9ca-506">포트 443</span><span class="sxs-lookup"><span data-stu-id="1b9ca-506">Port 443</span></span> |
| <span data-ttu-id="1b9ca-507">&#42;.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="1b9ca-507">&#42;.blob.core.windows.net/</span></span> |<span data-ttu-id="1b9ca-508">포트 443</span><span class="sxs-lookup"><span data-stu-id="1b9ca-508">Port 443</span></span> |

### <a name="a-403-error-is-displayed-when-onboarding"></a><span data-ttu-id="1b9ca-509">등록 시 403 오류가 표시됨</span><span class="sxs-lookup"><span data-stu-id="1b9ca-509">A 403 error is displayed when onboarding</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="1b9ca-510">가능한 원인</span><span class="sxs-lookup"><span data-stu-id="1b9ca-510">Probable causes</span></span>
* <span data-ttu-id="1b9ca-511">Linux 서버의 날짜 및 시간이 올바르지 않습니다</span><span class="sxs-lookup"><span data-stu-id="1b9ca-511">The date and time are incorrect on Linux Server</span></span>
* <span data-ttu-id="1b9ca-512">사용된 작업 영역 ID 및 작업 영역 키가 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-512">The Workspace ID and Workspace Key used are incorrect</span></span>

#### <a name="resolution"></a><span data-ttu-id="1b9ca-513">해결 방법</span><span class="sxs-lookup"><span data-stu-id="1b9ca-513">Resolution</span></span>
* <span data-ttu-id="1b9ca-514">`date` 명령을 사용하여 Linux 서버에서 시간을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-514">Verify the time on your Linux server with the `date` command.</span></span> <span data-ttu-id="1b9ca-515">데이터가 현재 시간보다 15분 넘게 빠르거나 느릴 경우 등록이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-515">If the data is greater than or less than 15 minutes from the current time, then onboarding fails.</span></span> <span data-ttu-id="1b9ca-516">이 문제를 해결하려면 Linux 서버의 날짜 및/또는 시간대를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-516">To correct this, update the date and/or timezone of your Linux server.</span></span>
* <span data-ttu-id="1b9ca-517">최신 버전의 Linux용 OMS 에이전트는 시간 차이로 인해 등록 실패가 발생하는지 여부를 알려줍니다</span><span class="sxs-lookup"><span data-stu-id="1b9ca-517">The latest version of the OMS Agent for Linux notifies you if a time difference is causing onboarding failure</span></span>
* <span data-ttu-id="1b9ca-518">올바른 작업 영역 ID 및 작업 영역 키를 사용하여 다시 등록하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-518">Re-onboard using the correct Workspace ID and Workspace Key.</span></span> <span data-ttu-id="1b9ca-519">자세한 내용은 [명령줄 도구를 사용하여 등록](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-519">See  [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>

### <a name="a-500-error-or-404-error-appears-in-the-log-file-after-onboarding"></a><span data-ttu-id="1b9ca-520">등록 후 로그 파일에 500 오류 또는 404 오류가 나타남</span><span class="sxs-lookup"><span data-stu-id="1b9ca-520">A 500 error or 404 error appears in the log file after onboarding</span></span>
<span data-ttu-id="1b9ca-521">이 문제는 알려진 문제이며 Linux 데이터를 OMS 작업 영역으로 처음 업로드할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-521">This is a known issue that occurs during the first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="1b9ca-522">이 문제는 전송되는 데이터 또는 다른 문제에 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-522">This does not affect data being sent or other problems.</span></span> <span data-ttu-id="1b9ca-523">처음 등록할 때에는 이 오류를 무시해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-523">You can ignore the errors when initially onboarding.</span></span>

### <a name="nagios-data-does-not-appear-in-the-oms-portal"></a><span data-ttu-id="1b9ca-524">OMS 포털에 Nagios 데이터가 나타나지 않음</span><span class="sxs-lookup"><span data-stu-id="1b9ca-524">Nagios data does not appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="1b9ca-525">가능한 원인</span><span class="sxs-lookup"><span data-stu-id="1b9ca-525">Probable causes</span></span>
* <span data-ttu-id="1b9ca-526">omsagent 사용자는 Nagios 로그 파일에서 읽을 수 있는 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-526">The omsagent user does not have permissions to read from the Nagios log file</span></span>
* <span data-ttu-id="1b9ca-527">Nagios 원본 및 필터 섹션이 omsagent.conf 파일에서 아직 주석 처리되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-527">The Nagios source and filter sections are still commented in the omsagent.conf file</span></span>

#### <a name="resolutions"></a><span data-ttu-id="1b9ca-528">해결 방법</span><span class="sxs-lookup"><span data-stu-id="1b9ca-528">Resolutions</span></span>
* <span data-ttu-id="1b9ca-529">Nagios 파일에서 읽을 수 있도록 omsagent 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-529">Add the omsagent user in order to read from the Nagios file.</span></span> <span data-ttu-id="1b9ca-530">자세한 내용은 [Nagios 경고](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-530">See [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) for more information.</span></span>
* <span data-ttu-id="1b9ca-531">`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`의 Linux용 OMS 에이전트 일반 구성 파일에서 다음과 같이 Nagios 원본 및 필터 섹션의 주석이 **모두** 제거되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-531">In the OMS Agent for Linux general configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, ensure that **both** the Nagios source and filter sections have comments removed, similar to the following example.</span></span>

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


### <a name="linux-data-doesnt-appear-in-the-oms-portal"></a><span data-ttu-id="1b9ca-532">OMS 포털에 Linux 데이터가 나타나지 않음</span><span class="sxs-lookup"><span data-stu-id="1b9ca-532">Linux data doesn't appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="1b9ca-533">가능한 원인</span><span class="sxs-lookup"><span data-stu-id="1b9ca-533">Probable causes</span></span>
* <span data-ttu-id="1b9ca-534">OMS 서비스 등록이 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-534">Onboarding to the OMS Service failed</span></span>
* <span data-ttu-id="1b9ca-535">OMS 서비스에 대한 연결이 차단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-535">Connection to the OMS Service is blocked</span></span>
* <span data-ttu-id="1b9ca-536">Linux용 OMS 에이전트가 백업되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-536">The OMS Agent for Linux data is backed-up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="1b9ca-537">해결 방법</span><span class="sxs-lookup"><span data-stu-id="1b9ca-537">Resolutions</span></span>
* <span data-ttu-id="1b9ca-538">`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`가 있는지 확인하여 OMS 서비스에 성공적으로 등록되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-538">Verify that onboarding to the OMS Service was successful by verifying that the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` exists.</span></span>
* <span data-ttu-id="1b9ca-539">omsadmin.sh 명령줄을 사용하여 다시 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-539">Re-onboard using the omsadmin.sh command line.</span></span> <span data-ttu-id="1b9ca-540">자세한 내용은 [명령줄 도구를 사용하여 등록](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-540">See [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="1b9ca-541">프록시를 사용할 경우 위의 프록시 문제 해결 단계를 사용합니다</span><span class="sxs-lookup"><span data-stu-id="1b9ca-541">If using a proxy, use the proxy troubleshooting steps above</span></span>
* <span data-ttu-id="1b9ca-542">Linux용 OMS 에이전트가 OMS 서비스와 통신할 수 없는 경우 에이전트의 데이터가 최대 버퍼 크기인 50MB로 백업될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-542">In some cases, when the OMS Agent for Linux cannot communicate with the OMS Service, data on the Agent is backed-up to the full buffer size of 50 MB.</span></span> <span data-ttu-id="1b9ca-543">`/opt/microsoft/omsagent/bin/service_control restart` 명령을 실행하여 Linux용 OMS 에이전트를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-543">Restart the OMS Agent for Linux by running the `/opt/microsoft/omsagent/bin/service_control restart` command.</span></span>
  >[AZURE.NOTE] <span data-ttu-id="1b9ca-544">이 문제는 에이전트 버전 1.1.0-28 및 이상에서 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-544">This issue is fixed in Agent version 1.1.0-28 and later.</span></span>

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-the-oms-portal"></a><span data-ttu-id="1b9ca-545">OMS 포털에서 Syslog Linux 성능 카운터 구성이 적용되지 않음</span><span class="sxs-lookup"><span data-stu-id="1b9ca-545">Syslog Linux performance counter configuration is not applied in the OMS portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="1b9ca-546">가능한 원인</span><span class="sxs-lookup"><span data-stu-id="1b9ca-546">Probable causes</span></span>
* <span data-ttu-id="1b9ca-547">Linux용 OMS 에이전트의 구성 에이전트가 OSM 포털에서 최신 구성을 검색하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-547">The configuration agent in the OMS Agent for Linux has not retrieved the latest configuration from the OMS portal.</span></span>
* <span data-ttu-id="1b9ca-548">포털에서 수정한 설정이 적용되지 않았습니다</span><span class="sxs-lookup"><span data-stu-id="1b9ca-548">The revised settings in the portal were not applied</span></span>

#### <a name="resolutions"></a><span data-ttu-id="1b9ca-549">해결 방법</span><span class="sxs-lookup"><span data-stu-id="1b9ca-549">Resolutions</span></span>
<span data-ttu-id="1b9ca-550">`omsconfig`는 Linux용 OMS 에이전트에서 OMS 포털 구성 변경 사항을 5분마다 검색하는 구성 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-550">`omsconfig` is the configuration agent in the OMS Agent for Linux that retrieves OMS portal configuration changes every 5 minutes.</span></span> <span data-ttu-id="1b9ca-551">그런 다음 이 구성은 `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`에 있는 Linux용 OMS 에이전트 구성 파일에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-551">This configuration is then applied to the OMS Agent for Linux configuration files located at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span></span>

* <span data-ttu-id="1b9ca-552">Linux용 OMS 에이전트 구성 에이전트가 포털 구성 서비스와 통신할 수 없어 최신 구성이 적용되지 않는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-552">In some cases, the OMS Agent for Linux configuration agent might not be able to communicate with the portal configuration service resulting in latest configuration not being applied.</span></span>
* <span data-ttu-id="1b9ca-553">`omsconfig` 에이전트에 다음이 적용되어 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-553">Verify that the `omsconfig` agent is installed with the following:</span></span>

  * <span data-ttu-id="1b9ca-554">`dpkg --list omsconfig` 또는 `rpm -qi omsconfig`</span><span class="sxs-lookup"><span data-stu-id="1b9ca-554">`dpkg --list omsconfig` or `rpm -qi omsconfig`</span></span>
  * <span data-ttu-id="1b9ca-555">Linux용 OMS 에이전트 최신 버전이 설치되지 않은 경우 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-555">If not installed, reinstall the latest version of the OMS Agent for Linux</span></span>
* <span data-ttu-id="1b9ca-556">`omsconfig` 에이전트가 OMS 서비스와 통신할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-556">Verify that the `omsconfig` agent can communicate with the OMS service</span></span>

  * <span data-ttu-id="1b9ca-557">`sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-557">Run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
    * <span data-ttu-id="1b9ca-558">이 명령은 Syslog 설정, Linux 성능 카운터, 사용자 지정 로그 등 에이전트가 포털에서 검색하는 구성을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-558">The command above returns the configuration that agent retrieves from the portal, including Syslog settings, Linux performance counters, and custom logs</span></span>
    * <span data-ttu-id="1b9ca-559">위 명령이 실패할 경우 `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-559">If the command above fails, run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="1b9ca-560">이 명령에서는 omsconfig 에이전트가 OMS 서비스와 통신하여 최신 구성을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-560">This command forces the omsconfig agent to communicate with the OMS service to retrieve the latest configuration.</span></span>

### <a name="custom-linux-log-data-does-not-appear-in-the-oms-portal"></a><span data-ttu-id="1b9ca-561">OMS 포털에서 사용자 지정 Linux 로그 데이터가 나타나지 않음</span><span class="sxs-lookup"><span data-stu-id="1b9ca-561">Custom Linux log data does not appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="1b9ca-562">가능한 원인</span><span class="sxs-lookup"><span data-stu-id="1b9ca-562">Probable causes</span></span>
* <span data-ttu-id="1b9ca-563">OMS 서비스 등록이 실패했습니다</span><span class="sxs-lookup"><span data-stu-id="1b9ca-563">Onboarding to OMS Service failed</span></span>
* <span data-ttu-id="1b9ca-564">**다음 구성을 Linux 서버에 적용** 설정을 선택하지 않았습니다</span><span class="sxs-lookup"><span data-stu-id="1b9ca-564">The **Apply the following configuration to my Linux Servers** setting has not been selected</span></span>
* <span data-ttu-id="1b9ca-565">omsconfig가 포털의 최신 사용자 지정 로그를 적용하지 않았습니다</span><span class="sxs-lookup"><span data-stu-id="1b9ca-565">omsconfig has not picked up the latest custom log from the portal</span></span>
* <span data-ttu-id="1b9ca-566">`omsagent` 사용 시 권한 문제 또는 `omsagent`가 검색되지 않아 사용자 지정 로그에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-566">The `omsagent` use is unable to access the custom log due to a permissions problem or `omsagent` was not found.</span></span> <span data-ttu-id="1b9ca-567">이 경우 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-567">In this case, you'll see the following output:</span></span>
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* <span data-ttu-id="1b9ca-568">이 문제는 경합 상태의 알려진 문제이며 Linux용 OMS Agent 버전 1.1.0-217에서 해결되었습니다</span><span class="sxs-lookup"><span data-stu-id="1b9ca-568">This is a known issue with the Race Condition that was fixed in the OMS Agent for Linux version 1.1.0-217</span></span>

#### <a name="resolutions"></a><span data-ttu-id="1b9ca-569">해결 방법</span><span class="sxs-lookup"><span data-stu-id="1b9ca-569">Resolutions</span></span>
* <span data-ttu-id="1b9ca-570">`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` 파일이 있는지 확인하여 성공적으로 등록되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-570">Verify that you've successfully onboarded, by determining whether the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` file exists.</span></span>
  * <span data-ttu-id="1b9ca-571">필요할 경우 omsadmin.sh 명령줄을 사용하여 다시 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-571">If needed, onboard again using the omsadmin.sh command line.</span></span> <span data-ttu-id="1b9ca-572">자세한 내용은 [명령줄 도구를 사용하여 등록](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-572">See [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="1b9ca-573">OMS 포털의 **데이터** 탭의 **설정**에서 **내 Linux 서버에 다음 구성 적용 설정**이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-573">In the OMS Portal, under **Settings** on the **Data** tab, ensure that the **Apply the following configuration to my Linux Servers** setting is selected</span></span>  
  <span data-ttu-id="1b9ca-574">![구성 적용](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span><span class="sxs-lookup"><span data-stu-id="1b9ca-574">![apply configuration](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span></span>
* <span data-ttu-id="1b9ca-575">`omsconfig` 에이전트가 OMS 서비스와 통신할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-575">Verify that the `omsconfig` agent can communicate with the OMS service</span></span>

  * <span data-ttu-id="1b9ca-576">`sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-576">Run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
  * <span data-ttu-id="1b9ca-577">이 명령은 Syslog 설정, Linux 성능 카운터, 사용자 지정 로그 등 에이전트가 포털에서 검색하는 구성을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-577">The command above returns the configuration that agent retrieves from the Portal, including Syslog settings, Linux performance counters, and custom Logs</span></span>
  * <span data-ttu-id="1b9ca-578">위 명령이 실패할 경우 `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-578">If the command above fails, run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="1b9ca-579">이 명령에서는 omsconfig 에이전트가 OMS 서비스와 통신하여 최신 구성을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-579">This command forces the omsconfig agent to communicate with OMS service and retrieve the latest configuration.</span></span>

<span data-ttu-id="1b9ca-580">Linux용 OMS Agent 사용자는 권한 있는 사용자 `root`로 실행되지 않고 `omsagent` 사용자로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-580">Instead of the OMS Agent for Linux user running as a privileged user `root`, the OMS Agent for Linux runs as the `omsagent` user.</span></span> <span data-ttu-id="1b9ca-581">대부분의 경우 사용자가 특정 파일을 읽으려면 명시적 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-581">In most cases, explicit permission must be granted to the user in order to read certain files.</span></span>

<span data-ttu-id="1b9ca-582">`omsagent` 사용자에게 권한을 부여하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-582">To grant permission to `omsagent` user, run the following commands:</span></span>

1. <span data-ttu-id="1b9ca-583">`omsagent`를 사용하여 특정 그룹에 `sudo usermod -a -G <GROUPNAME> <USERNAME>` 사용자를 추가합니다</span><span class="sxs-lookup"><span data-stu-id="1b9ca-583">Add the `omsagent` user to a specific group with `sudo usermod -a -G <GROUPNAME> <USERNAME>`</span></span>
2. <span data-ttu-id="1b9ca-584">`sudo chmod -R ugo+rw <FILE DIRECTORY>`를 사용하여 필수 파일에 공용 읽기 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-584">Grant universal read access to the required file with `sudo chmod -R ugo+rw <FILE DIRECTORY>`</span></span>

<span data-ttu-id="1b9ca-585">이 문제는 경합 상태의 알려진 문제이며 Linux용 OMS Agent 버전 1.1.0-217에서 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-585">There is a known issue with the Race Condition that was fixed in the OMS Agent for Linux version 1.1.0-217.</span></span> <span data-ttu-id="1b9ca-586">최신 에이전트로 업데이트한 후 다음 명령을 사용하여 최신 버전의 출력 플러그인을 가져오십시오.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-586">After updating to the latest agent, run the following command to get the latest version of the output plugin:</span></span>

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a><span data-ttu-id="1b9ca-587">알려진 제한 사항</span><span class="sxs-lookup"><span data-stu-id="1b9ca-587">Known limitations</span></span>
<span data-ttu-id="1b9ca-588">Linux 용 OMS 에이전트의 현재 제한 사항에 대해 알아보려면 다음 섹션을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-588">Review the following sections to learn about current limitations of the OMS Agent for Linux.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="1b9ca-589">Azure 진단</span><span class="sxs-lookup"><span data-stu-id="1b9ca-589">Azure Diagnostics</span></span>
<span data-ttu-id="1b9ca-590">Azure에서 실행되는 Linux 가상 컴퓨터의 경우, Azure 진단 및 Operations Management Suite의 데이터 수집을 허용하려면 추가적인 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-590">For Linux virtual machines running in Azure, additional steps may be required to allow data collection by Azure Diagnostics and Operations Management Suite.</span></span> <span data-ttu-id="1b9ca-591">**버전 2.2** 가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-591">**Version 2.2** of the Diagnostics Extension for Linux is required for compatibility with the OMS Agent for Linux.</span></span>

<span data-ttu-id="1b9ca-592">Linux용 진단 확장 설치 및 구성에 대한 자세한 내용은 [Azure CLI 명령을 사용하여 Linux 진단 확장을 사용하도록 설정](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-592">For more information on installing and configuring the Diagnostic Extension for Linux, see [Use the Azure CLI command to enable Linux Diagnostic Extension](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span></span>

<span data-ttu-id="1b9ca-593">**Linux 진단 확장을 2.0에서 2.2로 업그레이드 Azure CLI ASM:**</span><span class="sxs-lookup"><span data-stu-id="1b9ca-593">**Upgrading the Linux Diagnostics Extension from 2.0 to 2.2 Azure CLI ASM:**</span></span>

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="1b9ca-594">**ARM**</span><span class="sxs-lookup"><span data-stu-id="1b9ca-594">**ARM**</span></span>

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="1b9ca-595">이 코드 예제는 PrivateConfig.json이라는 이름의 파일을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-595">These command examples reference a file named PrivateConfig.json.</span></span> <span data-ttu-id="1b9ca-596">그 파일의 형식은 다음 샘플과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-596">The format of that file should resemble the following sample.</span></span>

```
    {
    "storageAccountName":"the storage account to receive data",
    "storageAccountKey":"the key of the account"
    }
```

### <a name="sysklog-is-not-supported"></a><span data-ttu-id="1b9ca-597">Sysklog가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-597">Sysklog is not supported</span></span>
<span data-ttu-id="1b9ca-598">Syslog 메시지를 수집하려면 rsyslog 또는 syslog-ng가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-598">Either rsyslog or syslog-ng are required to collect syslog messages.</span></span> <span data-ttu-id="1b9ca-599">Red Hat Enterprise Linux 버전 5, CentOS 및 Oracle Linux 버전(sysklog)에서는 syslog 이벤트 수집을 위한 기본 syslog 디먼이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-599">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="1b9ca-600">이 배포의 해당 버전에서 syslog 데이터를 수집하려면 rsyslog 디먼을 설치하고 sysklog를 대체하도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-600">To collect syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog.</span></span> <span data-ttu-id="1b9ca-601">sysklog를 rsyslog로 대체하는 방법에 대한 자세한 내용은 [Install the newly built rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM)(새로 작성한 rsyslog RPM 설치)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-601">For more information on replacing sysklog with rsyslog, see [Install the newly built rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b9ca-602">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1b9ca-602">Next Steps</span></span>
* <span data-ttu-id="1b9ca-603">[솔루션 갤러리에서 Log Analytics 솔루션을 추가](log-analytics-add-solutions.md) 하여 기능을 추가하고 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-603">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) to add functionality and gather data.</span></span>
* <span data-ttu-id="1b9ca-604">[로그 검색](log-analytics-log-searches.md) 을 숙지하여 솔루션에서 수집한 자세한 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-604">Get familiar with [log searches](log-analytics-log-searches.md) to view detailed information gathered by solutions.</span></span>
* <span data-ttu-id="1b9ca-605">[대시보드](log-analytics-dashboards.md) 를 사용하여 자신만의 사용자 지정 검색을 저장하고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1b9ca-605">Use [dashboards](log-analytics-dashboards.md) to save and display your own custom searches.</span></span>
