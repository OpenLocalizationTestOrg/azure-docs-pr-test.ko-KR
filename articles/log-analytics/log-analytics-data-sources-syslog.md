---
title: "aaaCollect OMS 로그 분석에서 Syslog 메시지를 분석 하 고 | Microsoft Docs"
description: "Syslog는 일반적인 tooLinux 이벤트 로깅 프로토콜입니다. 이 문서에서는 로그 분석에서 Syslog 메시지의 tooconfigure 컬렉션 및 hello 레코드의 세부 정보 작성 방법과 hello OMS 리포지토리에 설명 합니다."
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
ms.openlocfilehash: 8bfa0bca3f2f18287d1352c98bbaa2a70e41e276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a>Log Analytics의 Syslog 데이터 원본
Syslog는 일반적인 tooLinux 이벤트 로깅 프로토콜입니다.  응용 프로그램에서 hello 로컬 컴퓨터에 저장 하거나 tooa Syslog 수집기를 배달할 수 있는 메시지를 보냅니다.  Hello Linux 용 OMS 에이전트가 설치 되 면 hello 로컬 Syslog 디먼 tooforward 메시지 toohello 에이전트를 구성 합니다.  그런 다음 hello 에이전트 hello OMS 리포지토리에 해당 레코드를 만들 위치 hello 메시지 tooLog 분석 보냅니다.  

> [!NOTE]
> 로그 분석 여기서 rsyslog는 hello 기본 디먼 rsyslog 또는 syslog-ng가 보낸 메시지의 컬렉션을 지원 합니다. Red Hat Enterprise Linux, CentOS 및 Oracle Linux 버전 (sysklog)의 버전 5에 hello 기본 syslog 디먼은 syslog 이벤트 수집이 지원 되지 않습니다. 이 버전의,이 배포에서 syslog 데이터 toocollect hello [rsyslog 디먼을](http://rsyslog.com) tooreplace sysklog를 구성 하 고 설치 해야 합니다.
>
>

![Syslog 수집](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a>Syslog 구성
hello Linux 용 OMS 에이전트는 hello 시설 및 해당 구성에 지정 된 심각도 이벤트를 수집 합니다.  Hello OMS 포털을 통해 또는 Linux 에이전트의 구성 파일을 관리 하 여 Syslog를 구성할 수 있습니다.

### <a name="configure-syslog-in-hello-oms-portal"></a>Hello OMS 포털에서 Syslog를 구성 합니다.
Hello에서 Syslog를 구성할 [로그 분석 설정의 데이터 메뉴](log-analytics-data-sources.md#configuring-data-sources)합니다.  이 구성은 각 Linux 에이전트에서 toohello 구성 파일을 배달 됩니다.

해당 이름을 입력하고 **+**에서 Syslog를 구성합니다.  각 기능에 대 한 메시지만 선택 hello 심각도 인 경우 수집 됩니다.  원하는 toocollect hello 특정 기능에 대 한 hello 심각도 확인 합니다.  추가 조건을 toofilter 메시지를 제공할 수 없습니다.

![Syslog 구성](media/log-analytics-data-sources-syslog/configure.png)

기본적으로 모든 구성 변경 내용은 tooall 에이전트를 자동으로 이동 됩니다.  각 Linux 에이전트에서 수동으로 Syslog tooconfigure 원하는 hello 확인란의 선택을 취소 한 다음 *구성 toomy Linux 컴퓨터 아래 적용*합니다.

### <a name="configure-syslog-on-linux-agent"></a>Linux 에이전트에서 Syslog 구성
Hello 때 [Linux 클라이언트에 OMS 에이전트가 설치 되어](log-analytics-linux-agents.md)hello 기능을 정의 하는 기본 syslog 구성 파일을 설치 하 고 심각도의 hello 메시지를 수집 합니다.  이 파일 toochange hello 구성을 수정할 수 있습니다.  hello 구성 파일을 hello Syslog 클라이언트 hello 디먼 설치에 따라 다릅니다.

> [!NOTE]
> Hello syslog 구성을 편집 하는 경우 hello 변경 tootake 효과 대 한 hello syslog 디먼을 다시 시작 해야 합니다.
>
>

#### <a name="rsyslog"></a>rsyslog
hello rsyslog에 대 한 구성 파일에 위치한 **/etc/rsyslog.d/95-omsagent.conf**합니다.  기본 내용은 아래와 같습니다.  모든 기능의가 경고 이상인 수준에 대 한 hello 로컬 에이전트에서 보낸 syslog 메시지를 수집 합니다.

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

Hello 구성 파일의 해당 섹션을 제거 하 여 기능을 제거할 수 있습니다.  해당 기능 항목을 수정 하 여 특정 기능에 대 한 수집 하는 hello 심각도 제한할 수 있습니다.  예를 들어 오류 이상의 심각도 toolimit hello 사용자 시설 toomessages hello 구성 파일 toohello 다음 줄을 수정할 때 있습니다.

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a>syslog-ng
syslog ng hello 구성 파일은 위치 **/etc/syslog-ng/syslog-ng.conf**합니다.  기본 내용은 아래와 같습니다.  모든 기능 및 모든 심각도 대 한 hello 로컬 에이전트에서 보낸 syslog 메시지를 수집 합니다.   

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

Hello 구성 파일의 해당 섹션을 제거 하 여 기능을 제거할 수 있습니다.  해당 목록에서 제거 하 여 특정 기능에 대 한 수집 하는 hello 심각도 제한할 수 있습니다.  예를 들어 toolimit hello 사용자 시설 toojust 경고 및 중요 한 메시지 hello 구성 파일 toohello 뒤의 해당 섹션을 수정할 때:

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a>추가 Syslog 포트에서 데이터 수집
hello OMS 에이전트 Syslog 메시지 hello 포트 25224에서 로컬 클라이언트에서 수신 대기합니다.  Hello 에이전트를 설치할 때 기본 syslog 구성이 적용 하 고 수정할 수 있는 위치 hello에:

* Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`
* Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`

두 개의 구성 파일을 만들어 hello 포트 번호를 변경할 수 있습니다: hello Syslog 디먼 설치에 따라 rsyslog 또는 syslog ng 파일과 FluentD 구성 파일입니다.  

* hello FluentD 구성 파일에 있는 새 파일 이어야 합니다: `/etc/opt/microsoft/omsagent/conf/omsagent.d` hello에 hello 값 대체 및 **포트** 사용자 지정 포트 번호를 가진 항목입니다.

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

* Rsyslog에 대 한에 새 구성 파일을 만들어야 합니다: `/etc/rsyslog.d/` 를 사용자 지정 포트 번호를 hello 값 % SYSLOG_PORT %를 바꿉니다.  

    > [!NOTE]
    > Hello 구성 파일에서이 값을 수정 하는 경우 `95-omsagent.conf`, hello 에이전트가 기본 구성을 적용할 때 덮어쓰게 됩니다.
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* hello syslog ng 구성 수정 해야 hello 아래에 표시 된 구성의 예를 복사 하 여 있고 추가 사용자 지정 수정 된 설정은 toohello hello hello syslog ng.conf 구성 파일의 끝에 `/etc/syslog-ng/`합니다.  수행 **하지** hello 기본 레이블을 사용 하 여 **% WORKSPACE_ID % _oms** 또는 **%WORKSPACE_ID_OMS**, 정의 사용자 지정 레이블 toohelp 변경 내용을 구분할 합니다.  

    > [!NOTE]
    > Hello 구성 파일에 hello 기본 값을 수정할 hello 에이전트가 기본 구성을 적용할 때 덮어쓰게 됩니다.
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

OMS 에이전트 서비스는 hello 변경, Syslog hello 및 hello를 완료 한 후 다시 시작 toobe tooensure hello 구성 변경 내용이 적용이 필요 합니다.   

## <a name="syslog-record-properties"></a>Syslog 레코드 속성
Syslog 레코드가 유형의 **Syslog** 한 hello 속성의 다음 표에 hello 합니다.

| 속성 | 설명 |
|:--- |:--- |
| 컴퓨터 |이벤트를 hello 하는 컴퓨터에서 수집 되었습니다. |
| Facility |Hello 메시지를 생성 한 hello 시스템의 hello 부분을 정의 합니다. |
| HostIP |Hello 메시지를 보내는 hello 시스템의 IP 주소입니다. |
| HostName |Hello 메시지를 보내는 hello 시스템의 이름입니다. |
| SeverityLevel |Hello 이벤트의 심각도 수준입니다. |
| SyslogMessage |Hello 메시지 텍스트입니다. |
| ProcessID |Hello 메시지를 생성 하는 hello 프로세스의 ID입니다. |
| EventTime |날짜 및 시간을 이벤트 hello 생성 되었습니다. |

## <a name="log-queries-with-syslog-records"></a>Syslog 레코드를 포함하는 로그 쿼리
hello 다음 표에서 다른 로그 하는 예제 쿼리 Syslog 레코드를 검색 합니다.

| 쿼리 | 설명 |
|:--- |:--- |
| Type=Syslog |모든 Syslog입니다. |
| Type=Syslog SeverityLevel=error |심각도가 오류인 모든 Syslog 레코드입니다. |
| Type=Syslog &#124; measure count() by Computer |컴퓨터별 Syslog 레코드 수입니다. |
| Type=Syslog &#124; measure count() by Facility |기능별 Syslog 레코드 수입니다. |

>[!NOTE]
> 작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 쿼리 위에 hello toohello 다음 변경 합니다.

> | 쿼리 | 설명 |
|:--- |:--- |
| syslog |모든 Syslog입니다. |
| Syslog &#124; where SeverityLevel == "error" |심각도가 오류인 모든 Syslog 레코드입니다. |
| Syslog &#124; summarize AggregatedValue = count() by Computer |컴퓨터별 Syslog 레코드 수입니다. |
| Syslog &#124; summarize AggregatedValue = count() by Facility |기능별 Syslog 레코드 수입니다. |

## <a name="next-steps"></a>다음 단계
* 에 대 한 자세한 내용은 [검색 로그](log-analytics-log-searches.md) tooanalyze hello 데이터가 데이터 원본 및 솔루션에서 수집 합니다.
* 사용 하 여 [사용자 정의 필드](log-analytics-custom-fields.md) tooparse 레코드에서에서 데이터를 syslog 개별 계획을 선택 합니다.
* [Linux 에이전트를 구성](log-analytics-linux-agents.md) toocollect 다른 종류의 데이터입니다.
