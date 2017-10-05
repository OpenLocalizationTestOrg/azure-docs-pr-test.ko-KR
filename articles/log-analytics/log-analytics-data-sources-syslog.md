---
title: "OMS Log Analytics에서 Syslog 메시지 수집 및 분석 | Microsoft Docs"
description: "Syslog는 Linux에 공통되는 이벤트 로깅 프로토콜입니다. 이 문서에서는 Log Analytics의 Syslog 메시지 수집을 구성하는 방법을 설명하고, OMS 리포지토리에 생성되는 레코드에 대한 자세한 정보를 제공합니다."
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
ms.date: 07/12/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 7513f405d5c7c05a8e6e2b7b0e6313f23a319c84
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a><span data-ttu-id="9db0e-104">Log Analytics의 Syslog 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="9db0e-104">Syslog data sources in Log Analytics</span></span>
<span data-ttu-id="9db0e-105">Syslog는 Linux에 공통되는 이벤트 로깅 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-105">Syslog is an event logging protocol that is common to Linux.</span></span>  <span data-ttu-id="9db0e-106">응용 프로그램은 로컬 컴퓨터에 저장되거나 Syslog 수집기에 배달될 수 있는 메시지를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-106">Applications will send messages that may be stored on the local machine or delivered to a Syslog collector.</span></span>  <span data-ttu-id="9db0e-107">Linux용 OMS 에이전트를 설치하면 에이전트에 메시지를 전달하도록 로컬 Syslog 디먼이 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-107">When the OMS Agent for Linux is installed, it configures the local Syslog daemon to forward messages to the agent.</span></span>  <span data-ttu-id="9db0e-108">그러면 에이전트는 Log Analytics에 해당 메시지를 보내며 OMS 리포지토리에 해당 레코드가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-108">The agent then sends the message to Log Analytics where a corresponding record is created in the OMS repository.</span></span>  

> [!NOTE]
> <span data-ttu-id="9db0e-109">Log Analytics는 rsyslog 또는 syslog-ng에서 보낸 메시지의 컬렉션을 지원합니다. 여기서 rsyslog는 기본 디먼입니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-109">Log Analytics supports collection of messages sent by rsyslog or syslog-ng, where rsyslog is the default daemon.</span></span> <span data-ttu-id="9db0e-110">Red Hat Enterprise Linux 버전 5, CentOS 및 Oracle Linux 버전(sysklog)에서는 syslog 이벤트 수집을 위한 기본 syslog 디먼이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-110">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="9db0e-111">이 배포의 해당 버전에서 syslog 데이터를 수집하려면 [rsyslog 디먼](http://rsyslog.com)을 설치하고 sysklog를 대체하도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-111">To collect syslog data from this version of these distributions, the [rsyslog daemon](http://rsyslog.com) should be installed and configured to replace sysklog.</span></span>
>
>

![Syslog 수집](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a><span data-ttu-id="9db0e-113">Syslog 구성</span><span class="sxs-lookup"><span data-stu-id="9db0e-113">Configuring Syslog</span></span>
<span data-ttu-id="9db0e-114">Linux용 OMS 에이전트는 해당 구성에 지정된 기능 및 심각도에 따라서만 이벤트를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-114">The OMS Agent for Linux will only collect events with the facilities and severities that are specified in its configuration.</span></span>  <span data-ttu-id="9db0e-115">OMS 포털을 통해 또는 Linux 에이전트의 구성 파일을 관리하여 Syslog를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-115">You can configure Syslog through the OMS portal or by managing configuration files on your Linux agents.</span></span>

### <a name="configure-syslog-in-the-oms-portal"></a><span data-ttu-id="9db0e-116">OMS 포털에서 Syslog 구성</span><span class="sxs-lookup"><span data-stu-id="9db0e-116">Configure Syslog in the OMS portal</span></span>
<span data-ttu-id="9db0e-117">[Log Analytics 설정의 데이터 메뉴](log-analytics-data-sources.md#configuring-data-sources)에서 Syslog를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-117">Configure Syslog from the [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="9db0e-118">이 구성은 각 Linux 에이전트의 구성 파일에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-118">This configuration is delivered to the configuration file on each Linux agent.</span></span>

<span data-ttu-id="9db0e-119">해당 이름을 입력하고 **+**에서 Syslog를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-119">You can add a new facility by typing in its name and clicking **+**.</span></span>  <span data-ttu-id="9db0e-120">각 기능에 대해, 선택한 심각도의 메시지만 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-120">For each facility, only messages with the selected severities will be collected.</span></span>  <span data-ttu-id="9db0e-121">수집하려는 특정 기능의 심각도를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-121">Check the severities for the particular facility that you want to collect.</span></span>  <span data-ttu-id="9db0e-122">이벤트를 필터링하는 추가 조건을 제공할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-122">You cannot provide any additional criteria to filter messages.</span></span>

![Syslog 구성](media/log-analytics-data-sources-syslog/configure.png)

<span data-ttu-id="9db0e-124">기본적으로, 모든 구성 변경은 모든 에이전트로 자동 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-124">By default, all configuration changes are automatically pushed to all agents.</span></span>  <span data-ttu-id="9db0e-125">각 Linux 에이전트에서 Syslog를 수동으로 구성하려면 *내 Linux 컴퓨터에 아래 구성 적용*확인란을 선택 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-125">If you want to configure Syslog manually on each Linux agent, then uncheck the box *Apply below configuration to my Linux machines*.</span></span>

### <a name="configure-syslog-on-linux-agent"></a><span data-ttu-id="9db0e-126">Linux 에이전트에서 Syslog 구성</span><span class="sxs-lookup"><span data-stu-id="9db0e-126">Configure Syslog on Linux agent</span></span>
<span data-ttu-id="9db0e-127">[OMS 에이전트가 Linux 클라이언트에 설치](log-analytics-linux-agents.md)되어 있으면 OMS 에이전트는 수집되는 메시지의 기능 및 심각도를 정의하는 기본 syslog 구성 파일을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-127">When the [OMS agent is installed on a Linux client](log-analytics-linux-agents.md), it installs a default syslog configuration file that defines the facility and severity of the messages that are collected.</span></span>  <span data-ttu-id="9db0e-128">이 파일을 수정하여 구성을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-128">You can modify this file to change the configuration.</span></span>  <span data-ttu-id="9db0e-129">구성 파일은 클라이언트가 설치한 Syslog 디먼에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-129">The configuration file is different depending on the Syslog daemon that the client has installed.</span></span>

> [!NOTE]
> <span data-ttu-id="9db0e-130">Syslog 구성을 편집하는 경우, 변경 내용을 적용하려면 syslog 디먼을 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-130">If you edit the syslog configuration, you must restart the syslog daemon for the changes to take effect.</span></span>
>
>

#### <a name="rsyslog"></a><span data-ttu-id="9db0e-131">rsyslog</span><span class="sxs-lookup"><span data-stu-id="9db0e-131">rsyslog</span></span>
<span data-ttu-id="9db0e-132">rsyslog에 대한 구성 파일은 **/etc/rsyslog.d/95-omsagent.conf**에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-132">The configuration file for rsyslog is located at **/etc/rsyslog.d/95-omsagent.conf**.</span></span>  <span data-ttu-id="9db0e-133">기본 내용은 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-133">Its default contents are shown below.</span></span>  <span data-ttu-id="9db0e-134">이 파일은 경고 이상 수준의 모든 기능에 대해 로컬 에이전트에서 전송된 syslog 메시지를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-134">This collects syslog messages sent from the local agent for all facilities with a level of warning or higher.</span></span>

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

<span data-ttu-id="9db0e-135">구성 파일의 해당 섹션을 제거하여 기능을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-135">You can remove a facility by removing its section of the configuration file.</span></span>  <span data-ttu-id="9db0e-136">해당 기능 항목을 수정하여 특정 기능에 대해 수집되는 심각도를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-136">You can limit the severities that are collected for a particular facility by modifying that facility's entry.</span></span>  <span data-ttu-id="9db0e-137">예를 들어 오류 또는 더 높은 심각도의 메시지로 사용자 기능을 제한하려면 다음 구성 파일 줄을 다음과 같이 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-137">For example, to limit the user facility to messages with a severity of error or higher you would modify that line of the configuration file to the following:</span></span>

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a><span data-ttu-id="9db0e-138">syslog-ng</span><span class="sxs-lookup"><span data-stu-id="9db0e-138">syslog-ng</span></span>
<span data-ttu-id="9db0e-139">syslog-ng의 구성 파일은 **/etc/syslog-ng/syslog-ng.conf**에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-139">The configuration file for syslog-ng is location at **/etc/syslog-ng/syslog-ng.conf**.</span></span>  <span data-ttu-id="9db0e-140">기본 내용은 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-140">Its default contents are shown below.</span></span>  <span data-ttu-id="9db0e-141">이 파일은 모든 기능 및 모든 심각도에 대해 로컬 에이전트에서 전송된 syslog 메시지를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-141">This collects syslog messages sent from the local agent for all facilities and all severities.</span></span>   

    #
    # Warnings (except iptables) in one file:
    #
    destination warn { file("/var/log/warn" fsync(yes)); };
    log { source(src); filter(f_warn); destination(warn); };

    #OMS_Destination
    destination d_oms { udp("127.0.0.1" port(25224)); };

    #OMS_facility = auth
    filter f_auth_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(auth); };
    log { source(src); filter(f_auth_oms); destination(d_oms); };

    #OMS_facility = authpriv
    filter f_authpriv_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(authpriv); };
    log { source(src); filter(f_authpriv_oms); destination(d_oms); };

    #OMS_facility = cron
    filter f_cron_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(cron); };
    log { source(src); filter(f_cron_oms); destination(d_oms); };

    #OMS_facility = daemon
    filter f_daemon_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(daemon); };
    log { source(src); filter(f_daemon_oms); destination(d_oms); };

    #OMS_facility = kern
    filter f_kern_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(kern); };
    log { source(src); filter(f_kern_oms); destination(d_oms); };

    #OMS_facility = local0
    filter f_local0_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local0); };
    log { source(src); filter(f_local0_oms); destination(d_oms); };

    #OMS_facility = local1
    filter f_local1_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local1); };
    log { source(src); filter(f_local1_oms); destination(d_oms); };

    #OMS_facility = mail
    filter f_mail_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(mail); };
    log { source(src); filter(f_mail_oms); destination(d_oms); };

    #OMS_facility = syslog
    filter f_syslog_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(syslog); };
    log { source(src); filter(f_syslog_oms); destination(d_oms); };

    #OMS_facility = user
    filter f_user_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };

<span data-ttu-id="9db0e-142">구성 파일의 해당 섹션을 제거하여 기능을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-142">You can remove a facility by removing its section of the configuration file.</span></span>  <span data-ttu-id="9db0e-143">특정 기능을 목록에서 제거하여 해당 기능에 대해 수집되는 심각도를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-143">You can limit the severities that are collected for a particular facility by removing them from its list.</span></span>  <span data-ttu-id="9db0e-144">예를 들어 경고 또는 위험 메시지만으로 사용자 기능을 제한하려면 구성 파일의 해당 섹션을 다음과 같이 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-144">For example, to limit the user facility to just alert and critical messages, you would modify that section of the configuration file to the following:</span></span>

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a><span data-ttu-id="9db0e-145">추가 Syslog 포트에서 데이터 수집</span><span class="sxs-lookup"><span data-stu-id="9db0e-145">Collecting data from additional Syslog ports</span></span>
<span data-ttu-id="9db0e-146">OMS 에이전트는 포트 25224에서 로컬 클라이언트의 Syslog 메시지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-146">The OMS agent listens for Syslog messages on the local client on port 25224.</span></span>  <span data-ttu-id="9db0e-147">에이전트가 설치될 때 기본 syslog 구성이 적용되며 다음 위치에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-147">When the agent is installed, a default syslog configuration is applied and found in the following location:</span></span>

* <span data-ttu-id="9db0e-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="9db0e-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span></span>
* <span data-ttu-id="9db0e-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span><span class="sxs-lookup"><span data-stu-id="9db0e-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span></span>

<span data-ttu-id="9db0e-150">두 개의 구성 파일을 만들어 포트 번호를 변경할 수 있습니다. 설치한 Syslog 디먼에 따라 rsyslog 또는 syslog-ng 파일과 FluentD 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-150">You can change the port number by creating two configuration files: a FluentD config file and a rsyslog-or-syslog-ng file depending on the Syslog daemon you have installed.</span></span>  

* <span data-ttu-id="9db0e-151">FluentD 구성 파일은 `/etc/opt/microsoft/omsagent/conf/omsagent.d`에 있는 새 파일이어야 합니다. **포트** 항목의 값을 사용자 지정 포트 번호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-151">The FluentD config file should be a new file located in: `/etc/opt/microsoft/omsagent/conf/omsagent.d` and replace the value in the **port** entry with your custom port number.</span></span>

        <source>
          type syslog
          port %SYSLOG_PORT%
          bind 127.0.0.1
          protocol_type udp
          tag oms.syslog
        </source>
        <filter oms.syslog.**>
          type filter_syslog
        </filter>

* <span data-ttu-id="9db0e-152">rsyslog의 경우 `/etc/rsyslog.d/`에 있는 새 구성 파일을 만들어야 합니다. %SYSLOG_PORT% 값을 사용자 지정 포트 번호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-152">For rsyslog, you should create a new configuration file located in: `/etc/rsyslog.d/` and replace the value %SYSLOG_PORT% with your custom port number.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="9db0e-153">구성 파일 `95-omsagent.conf`에서 이 값을 수정하는 경우 에이전트가 기본 구성을 적용할 때 덮어쓰게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-153">If you modify this value in the configuration file `95-omsagent.conf`, it will be overwritten when the agent applies a default configuration.</span></span>
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* <span data-ttu-id="9db0e-154">syslog-ng 구성 파일은 아래 표시된 예제 구성을 복사하고 사용자 지정 수정된 설정을 `/etc/syslog-ng/`에 있는 syslog-ng.conf 구성 파일의 끝에 추가하여 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-154">The syslog-ng config should be modified by copying the example configuration shown below and adding the custom modified settings to the end of the syslog-ng.conf configuration file located in `/etc/syslog-ng/`.</span></span>  <span data-ttu-id="9db0e-155">기본 레이블 **% WORKSPACE_ID % _oms** 또는 **%WORKSPACE_ID_OMS**를 사용하지 **않습니다**. 변경 내용을 구분하기 위해 사용자 지정 레이블을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-155">Do **not** use the default label **%WORKSPACE_ID%_oms** or **%WORKSPACE_ID_OMS**, define a custom label to help distinguish your changes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="9db0e-156">구성 파일에서 기본 값을 수정하는 경우 에이전트가 기본 구성을 적용할 때 덮어쓰게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-156">If you modify the default values in the configuration file, they will be overwritten when the agent applies a default configuration.</span></span>
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

<span data-ttu-id="9db0e-157">변경을 완료한 후, Syslog와 OMS 에이전트 서비스를 다시 시작하여 구성 변경 내용이 적용되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-157">After completing the changes, the Syslog and the OMS agent service needs to be restarted to ensure the configuration changes take effect.</span></span>   

## <a name="syslog-record-properties"></a><span data-ttu-id="9db0e-158">Syslog 레코드 속성</span><span class="sxs-lookup"><span data-stu-id="9db0e-158">Syslog record properties</span></span>
<span data-ttu-id="9db0e-159">Syslog 레코드는 **Syslog** 형식이며, 다음 표의 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-159">Syslog records have a type of **Syslog** and have the properties in the following table.</span></span>

| <span data-ttu-id="9db0e-160">속성</span><span class="sxs-lookup"><span data-stu-id="9db0e-160">Property</span></span> | <span data-ttu-id="9db0e-161">설명</span><span class="sxs-lookup"><span data-stu-id="9db0e-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9db0e-162">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="9db0e-162">Computer</span></span> |<span data-ttu-id="9db0e-163">이벤트가 수집된 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-163">Computer that the event was collected from.</span></span> |
| <span data-ttu-id="9db0e-164">Facility</span><span class="sxs-lookup"><span data-stu-id="9db0e-164">Facility</span></span> |<span data-ttu-id="9db0e-165">메시지를 생성한 시스템의 부분을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-165">Defines the part of the system that generated the message.</span></span> |
| <span data-ttu-id="9db0e-166">HostIP</span><span class="sxs-lookup"><span data-stu-id="9db0e-166">HostIP</span></span> |<span data-ttu-id="9db0e-167">메시지를 보내는 시스템의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-167">IP address of the system sending the message.</span></span> |
| <span data-ttu-id="9db0e-168">HostName</span><span class="sxs-lookup"><span data-stu-id="9db0e-168">HostName</span></span> |<span data-ttu-id="9db0e-169">메시지를 보내는 시스템의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-169">Name of the system sending the message.</span></span> |
| <span data-ttu-id="9db0e-170">SeverityLevel</span><span class="sxs-lookup"><span data-stu-id="9db0e-170">SeverityLevel</span></span> |<span data-ttu-id="9db0e-171">이벤트의 심각도 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-171">Severity level of the event.</span></span> |
| <span data-ttu-id="9db0e-172">SyslogMessage</span><span class="sxs-lookup"><span data-stu-id="9db0e-172">SyslogMessage</span></span> |<span data-ttu-id="9db0e-173">메시지의 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-173">Text of the message.</span></span> |
| <span data-ttu-id="9db0e-174">ProcessID</span><span class="sxs-lookup"><span data-stu-id="9db0e-174">ProcessID</span></span> |<span data-ttu-id="9db0e-175">메시지를 생성한 프로세스의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-175">ID of the process that generated the message.</span></span> |
| <span data-ttu-id="9db0e-176">EventTime</span><span class="sxs-lookup"><span data-stu-id="9db0e-176">EventTime</span></span> |<span data-ttu-id="9db0e-177">이벤트가 생성된 날짜 및 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-177">Date and time that the event was generated.</span></span> |

## <a name="log-queries-with-syslog-records"></a><span data-ttu-id="9db0e-178">Syslog 레코드를 포함하는 로그 쿼리</span><span class="sxs-lookup"><span data-stu-id="9db0e-178">Log queries with Syslog records</span></span>
<span data-ttu-id="9db0e-179">다음 표에는 Syslog 레코드를 검색하는 로그 쿼리의 여러 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-179">The following table provides different examples of log queries that retrieve Syslog records.</span></span>

| <span data-ttu-id="9db0e-180">쿼리</span><span class="sxs-lookup"><span data-stu-id="9db0e-180">Query</span></span> | <span data-ttu-id="9db0e-181">설명</span><span class="sxs-lookup"><span data-stu-id="9db0e-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9db0e-182">Type=Syslog</span><span class="sxs-lookup"><span data-stu-id="9db0e-182">Type=Syslog</span></span> |<span data-ttu-id="9db0e-183">모든 Syslog입니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-183">All Syslogs.</span></span> |
| <span data-ttu-id="9db0e-184">Type=Syslog SeverityLevel=error</span><span class="sxs-lookup"><span data-stu-id="9db0e-184">Type=Syslog SeverityLevel=error</span></span> |<span data-ttu-id="9db0e-185">심각도가 오류인 모든 Syslog 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-185">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="9db0e-186">Type=Syslog &#124; measure count() by Computer</span><span class="sxs-lookup"><span data-stu-id="9db0e-186">Type=Syslog &#124; measure count() by Computer</span></span> |<span data-ttu-id="9db0e-187">컴퓨터별 Syslog 레코드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-187">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="9db0e-188">Type=Syslog &#124; measure count() by Facility</span><span class="sxs-lookup"><span data-stu-id="9db0e-188">Type=Syslog &#124; measure count() by Facility</span></span> |<span data-ttu-id="9db0e-189">기능별 Syslog 레코드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-189">Count of Syslog records by facility.</span></span> |

>[!NOTE]
> <span data-ttu-id="9db0e-190">작업 영역을 [새 Log Analytics 쿼리 언어](log-analytics-log-search-upgrade.md)로 업그레이드한 경우에는 위의 쿼리가 다음과 같이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-190">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above queries would change to the following.</span></span>

> | <span data-ttu-id="9db0e-191">쿼리</span><span class="sxs-lookup"><span data-stu-id="9db0e-191">Query</span></span> | <span data-ttu-id="9db0e-192">설명</span><span class="sxs-lookup"><span data-stu-id="9db0e-192">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9db0e-193">syslog</span><span class="sxs-lookup"><span data-stu-id="9db0e-193">Syslog</span></span> |<span data-ttu-id="9db0e-194">모든 Syslog입니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-194">All Syslogs.</span></span> |
| <span data-ttu-id="9db0e-195">Syslog &#124; where SeverityLevel == "error"</span><span class="sxs-lookup"><span data-stu-id="9db0e-195">Syslog &#124; where SeverityLevel == "error"</span></span> |<span data-ttu-id="9db0e-196">심각도가 오류인 모든 Syslog 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-196">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="9db0e-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span><span class="sxs-lookup"><span data-stu-id="9db0e-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span></span> |<span data-ttu-id="9db0e-198">컴퓨터별 Syslog 레코드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-198">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="9db0e-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span><span class="sxs-lookup"><span data-stu-id="9db0e-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span></span> |<span data-ttu-id="9db0e-200">기능별 Syslog 레코드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-200">Count of Syslog records by facility.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9db0e-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9db0e-201">Next steps</span></span>
* <span data-ttu-id="9db0e-202">데이터 원본 및 솔루션에서 수집한 데이터를 분석하기 위해 [로그 검색](log-analytics-log-searches.md) 에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-202">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span>
* <span data-ttu-id="9db0e-203">[사용자 지정 필드](log-analytics-custom-fields.md)를 사용하여 syslog 레코드의 데이터를 개별 필드로 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-203">Use [Custom Fields](log-analytics-custom-fields.md) to parse data from syslog records into individual fields.</span></span>
* <span data-ttu-id="9db0e-204">[Linux 에이전트를 구성](log-analytics-linux-agents.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9db0e-204">[Configure Linux agents](log-analytics-linux-agents.md) to collect other types of data.</span></span>
