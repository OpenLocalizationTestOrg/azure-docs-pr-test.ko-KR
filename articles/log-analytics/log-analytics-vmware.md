---
title: "로그 분석에서 모니터링 솔루션 aaaVMware | Microsoft Docs"
description: "로그 관리 및 ESXi 호스트 모니터링 hello VMware 모니터링 솔루션 도울 수 있는 방법에 대해 알아봅니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 16516639-cc1e-465c-a22f-022f3be297f1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.openlocfilehash: 959d5c2201fc5c7947f8b8870d055cdf9eea8e01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="vmware-monitoring-preview-solution-in-log-analytics"></a>Log Analytics의 VMware 모니터링(미리 보기) 솔루션

![VMware 기호](./media/log-analytics-vmware/vmware-symbol.png)

로그 분석에서 VMware 모니터링 솔루션 hello는 큰 VMware 로그에 대 한 모니터링 접근 방식 및 중앙된 로깅을 만들 수 있는 솔루션입니다. 이 문서에서는 문제 해결, 캡처, 하는 방법을 hello 솔루션을 사용 하 여 단일 위치에서 hello ESXi 호스트를 관리를 설명 합니다. Hello 솔루션을 사용 하 여 단일 위치에서 모든 ESXi 호스트에 대 한 자세한 데이터를 볼 수 있습니다. 최상위 이벤트 수, 상태 및 hello ESXi 호스트 로그를 통해 제공 되는 VM 및 ESXi 호스트의 추세를 볼 수 있습니다. 중앙 집중식 ESXi 호스트 로그를 보고 검색하여 문제를 해결할 수 있습니다. 그리고 로그 검색 쿼리에 기반한 경고를 만들 수 있습니다.

hello 솔루션 hello ESXi 호스트 toopush 데이터 tooa 대상 VM에 OMS 에이전트의 기본 syslog 기능을 사용 합니다. 그러나 hello 솔루션 파일 hello 대상 VM 내에서 syslog을 기록 하지 않습니다. hello OMS 에이전트는 포트 1514 열고 toothis 수신 대기 합니다. Hello 데이터를 받으면 hello OMS 에이전트 hello 데이터를 OMS로 푸시합니다.

## <a name="installing-and-configuring-hello-solution"></a>설치 하 고 hello 솔루션 구성
다음 정보 tooinstall hello를 사용 하 고 hello 솔루션을 구성 합니다.

* Hello VMware 모니터링 솔루션 tooyour hello 프로세스를 사용 하 여 OMS 작업 영역에 설명 된 추가 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.

#### <a name="supported-vmware-esxi-hosts"></a>지원되는 VMware ESXi 호스트
vSphere ESXi 호스트 5.5 및 6.0

#### <a name="prepare-a-linux-server"></a>Linux 서버 준비
Hello ESXi 호스트에서 Linux 운영 체제 VM tooreceive 모든 syslog 데이터를 만듭니다. hello [OMS Linux 에이전트](log-analytics-linux-agents.md) hello 컬렉션 지점 모든 ESXi 호스트 syslog 데이터입니다. 여러 ESXi 호스트 tooforward 로그 tooa 단일 Linux 서버, 다음 예제는 hello와 같이 사용할 수 있습니다.  

   ![syslog 흐름](./media/log-analytics-vmware/diagram.png)

### <a name="configure-syslog-collection"></a>Syslog 수집 구성
1. vSphere에 syslog를 전달하도록 설정합니다. Syslog 전달을 설정 하는 자세한 정보 toohelp, 참조 [ESXi에서 syslog 구성 5.x 및 6.0 (2003322)](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2003322)합니다. 너무 이동**ESXi 호스트 구성** > **소프트웨어** > **고급 설정** > **Syslog**.
   ![vsphereconfig](./media/log-analytics-vmware/vsphere1.png)  
2. Hello에 *Syslog.global.logHost* 필드, Linux 서버 및 hello 포트 번호를 추가 *1514*합니다. 예를 들어 `tcp://hostname:1514` 또는 `tcp://123.456.789.101:1514`와 같습니다.
3. Syslog에 대 한 hello ESXi 호스트 방화벽을 엽니다. **ESXi 호스트 구성** > **소프트웨어** > **보안 프로필** > **방화벽**으로 이동한 다음 **속성**을 엽니다.  

    ![vspherefw](./media/log-analytics-vmware/vsphere2.png)  

    ![vspherefwproperties](./media/log-analytics-vmware/vsphere3.png)  
4. 해당 syslog 올바르게 설정 하는 hello vSphere 콘솔 tooverify를 확인 합니다. Hello에 ESXI 호스트 해당 포트를 확인 **1514** 구성 됩니다.
5. 다운로드 하 고 hello Linux 서버에 Linux 용 OMS 에이전트 hello를 설치 합니다. 자세한 내용은 참조 hello [Linux 용 OMS 에이전트에 대 한 설명서](https://github.com/Microsoft/OMS-Agent-for-Linux)합니다.
6. Hello Linux 용 OMS 에이전트를 설치한 후 toohello /etc/opt/microsoft/omsagent/sysconf/omsagent.d 디렉터리 및 복사 hello vmware_esxi.conf 파일 toohello /etc/opt/microsoft/omsagent/conf/omsagent.d 디렉터리를 이동 하 고 hello hello 소유자/그룹 변경 및 hello 파일의 사용 권한을 지정 합니다. 예:

    ```
    sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/vmware_esxi.conf /etc/opt/microsoft/omsagent/conf/omsagent.d
   sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf
    ```
7. 실행 하 여 Linux 용 OMS 에이전트 hello를 다시 시작 `sudo /opt/microsoft/omsagent/bin/service_control restart`합니다.
8. Hello를 사용 하 여 hello Linux 서버 hello ESXi 호스트와 hello 연결 테스트 `nc` hello ESXi 호스트에 명령 합니다. 예:

    ```
    [root@ESXiHost:~] nc -z 123.456.789.101 1514
    Connection too123.456.789.101 1514 port [tcp/*] succeeded!
    ```

9. Hello OMS 포털에서에서 수행 된 로그 검색에 대 한 `Type=VMware_CL`합니다. OMS는 hello syslog 데이터 수집 hello syslog 형식을 유지 됩니다. Hello 포털에서 일부 특정 필드 캡처됩니다와 같은 *Hostname* 및 *ProcessName*합니다.  

    ![type](./media/log-analytics-vmware/type.png)  

    로그 검색 결과 보기 위의 이와 유사한 toohello 이미지 인 toouse hello OMS VMware 모니터링 솔루션 대시보드를 설정 합니다.  

## <a name="vmware-data-collection-details"></a>VMware 데이터 수집 세부 정보
hello VMware 모니터링 솔루션 사용 하도록 설정한 Linux 용 OMS 에이전트를 hello를 사용 하 여 ESXi 호스트에서 다양 한 성능 메트릭 및 로그 데이터를 수집 합니다.

hello 다음 표에서 데이터 수집 방법과 데이터가 수집 되는 방법에 대 한 기타 세부 정보입니다.

| 플랫폼 | Linux 용 OMS 에이전트 | SCOM 에이전트 | Azure 저장소 | SCOM 필요? | 관리 그룹을 통해 전송되는 SCOM 에이전트 데이터 | 수집 빈도 |
| --- | --- | --- | --- | --- | --- | --- |
| Linux |&#8226; |  |  |  |  |매 3분 |

다음 표에 hello hello VMware 모니터링 솔루션에 의해 수집 된 데이터 필드의 예를 보여 줍니다.

| 필드 이름 | 설명 |
| --- | --- |
| Device_s |VMware 저장소 장치 |
| ESXIFailure_s |오류 유형 |
| EventTime_t |이벤트가 발생한 시간 |
| HostName_s |ESXi 호스트 이름 |
| Operation_s |VM 만들기 또는 삭제 |
| ProcessName_s |이벤트 이름 |
| ResourceId_s |hello VMware 호스트의 이름 |
| ResourceLocation_s |VMware |
| ResourceName_s |VMware |
| ResourceType_s |Hyper-V |
| SCSIStatus_s |VMware SCSI 상태 |
| SyslogMessage_s |Syslog 데이터 |
| UserName_s |VM을 만들거나 삭제한 사용자 |
| VMName_s |VM 이름 |
| Computer |호스트 컴퓨터 |
| TimeGenerated |생성 된 시간 hello 데이터 |
| DataCenter_s |VMware 데이터 센터 |
| StorageLatency_s |저장소 대기 시간(밀리초) |

## <a name="vmware-monitoring-solution-overview"></a>VMware 모니터링 솔루션 개요
hello VMware 타일 hello OMS 포털에에서 표시 됩니다. 발생한 모든 오류에 대한 상위 수준 보기를 제공합니다. Hello 타일을 클릭 하면 대시보드 보기로 이동 합니다.

![타일](./media/log-analytics-vmware/tile.png)

#### <a name="navigate-hello-dashboard-view"></a>Hello 대시보드 보기를 탐색
Hello에 **VMware** 대시보드 보기 블레이드로 구성 됩니다.

* 오류 상태 수
* 이벤트 수 기준 상위 호스트
* 상위 이벤트 수
* 가상 컴퓨터 활동
* ESXi 호스트 디스크 이벤트

![solution1](./media/log-analytics-vmware/solutionview1-1.png)

![solution2](./media/log-analytics-vmware/solutionview1-2.png)

모든 블레이드 tooopen hello 블레이드에 대 한 특정 세부 정보를 표시 하는 로그 분석 검색 창을 클릭 합니다.

여기에서는 hello 검색 쿼리 toomodify를 편집할 수 있습니다에 특정 합니다. OMS 검색의 hello 기본 사항에 대 한 자습서에 대 한 체크 아웃 hello [OMS 로그 검색 자습서입니다.](log-analytics-log-searches.md)

#### <a name="find-esxi-host-events"></a>ESXi 호스트 이벤트 찾기
단일 ESXi 호스트에서는 프로세스에 따라 여러 로그를 생성합니다. hello VMware 모니터링 솔루션을 중앙 집중화 하 고 hello 이벤트 수를 요약 합니다. 이처럼 중앙 집중화된 보기를 사용하면 대량의 이벤트가 발생한 ESXi 호스트 및 사용자 환경에서 가장 빈번하게 발생한 이벤트를 손쉽게 파악할 수 있습니다.

![event](./media/log-analytics-vmware/events.png)

ESXi 호스트 또는 이벤트 유형을 클릭하면 관련 정보를 자세히 파악할 수 있습니다.

ESXi 호스트 이름을 클릭하여 해당 ESXi 호스트의 정보를 살펴봅니다. Hello 이벤트 형식을 가진 toonarrow 결과 찾으려는 경우 추가 `“ProcessName_s=EVENT TYPE”` 검색 쿼리에 합니다. 선택할 수 있습니다 **ProcessName** hello 검색 필터에서. 사용자를 위해 hello 정보 범위를 좁히는 합니다.

![연습](./media/log-analytics-vmware/eventhostdrilldown.png)

#### <a name="find-high-vm-activities"></a>빈번한 VM 활동 찾기
ESXi 호스트마다 가상 컴퓨터를 만들고 삭제할 수 있습니다. 한 유용 관리자 tooidentify 개수 Vm ESXi 호스트를 만듭니다. 하 고, toounderstand 성능 및 용량 계획는 데 도움이 됩니다. 사용자 환경을 관리할 때는 VM 활동 이벤트를 추적하는 것이 중요합니다.

![연습](./media/log-analytics-vmware/vmactivities1.png)

Toosee 추가 ESXi 호스트 VM 만들기 데이터 ESXi 호스트 이름을 클릭 합니다.

![연습](./media/log-analytics-vmware/createvm.png)

#### <a name="common-search-queries"></a>일반적 검색 쿼리
hello 솔루션 높은 저장 공간, 저장소 대기 시간 및 경로 오류와 같은 프로그램 ESXi 호스트를 관리 하는 데 도움이 되는 다른 유용한 쿼리를 포함 합니다.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![쿼리](./media/log-analytics-vmware/queries.png)


#### <a name="save-queries"></a>쿼리 저장
OMS 표준 기능인 검색 쿼리 저장은 유용한 것으로 확인된 쿼리를 유지하는 데 도움이 됩니다. 유용한 쿼리를 만든 후 hello를 클릭 하 여 저장 **즐겨찾기**합니다. 저장된 된 쿼리를 사용 하면 쉽게 나중에 다시 사용할 hello에서 [내 대시보드](log-analytics-dashboards.md) 페이지 사용자 지정 대시보드를 만들 수 있습니다.

![DockerDashboardView](./media/log-analytics-vmware/dockerdashboardview.png)

#### <a name="create-alerts-from-queries"></a>쿼리에서 경고 만들기
Toouse hello 쿼리 tooalert 경우가 쿼리를 만든 후 특정 이벤트가 발생할 때 있습니다. 참조 [로그 분석에서 경고](log-analytics-alerts.md) 방법에 대 한 정보에 대 한 toocreate 경고 합니다. 쿼리 및 다른 쿼리 예제를 보려면 경고의 예 참조 hello [OMS 로그 분석을 사용 하 여 모니터 VMware](https://blogs.technet.microsoft.com/msoms/2016/06/15/monitor-vmware-using-oms-log-analytics) 블로그 게시물입니다.

## <a name="frequently-asked-questions"></a>질문과 대답
### <a name="what-do-i-need-toodo-on-hello-esxi-host-setting-what-impact-will-it-have-on-my-current-environment"></a>어떻게 해야 합니까 hello ESXi 호스트 설정에서 toodo? 현재 환경에 미치는 영향은 무엇입니까?
hello 솔루션 hello 네이티브 ESXi 호스트 Syslog 전달 메커니즘을 사용합니다. Hello ESXi 호스트 toocapture hello 로그에서 추가 Microsoft 소프트웨어가 필요는 없습니다. 많은 영향을 미치지 tooyour 기존 환경이 필요 합니다. 그러나 ESXI 기능은 tooset syslog 전달이 필요지 않습니다.

### <a name="do-i-need-toorestart-my-esxi-host"></a>해야 toorestart 내 ESXi 호스트?
아니요. 이 프로세스는 호스트를 다시 시작하지 않아도 됩니다. 경우에 따라 vSphere hello syslog을 제대로 업데이트 되지 않습니다. 이 경우 toohello ESXi 호스트에 로그온 하 고 hello syslog를 다시 로드 합니다. 다시, 않아도 toorestart hello 호스트 하므로이 프로세스가 중단 tooyour 환경 되지 있습니다.

### <a name="can-i-increase-or-decrease-hello-volume-of-log-data-sent-toooms"></a>있습니까 거 나 낮출 수 tooOMS 전송 된 로그 데이터의 볼륨 hello?
예. 그러나 vsphere에서 hello ESXi 호스트 로그 수준 설정에 사용할 수 있습니다. 로그 컬렉션은 hello에 기반 *정보* 수준입니다. 따라서 tooaudit VM 만들기 또는 삭제 하려면, 필요한 tookeep hello *정보* Hostd에 수준입니다. 자세한 내용은 참조 hello [VMware 기술 자료](https://kb.vmware.com/selfservice/microsites/search.do?&cmd=displayKC&externalId=1017658)합니다.

### <a name="why-is-hostd-not-providing-data-toooms-my-log-setting-is-set-tooinfo"></a>이유 Hostd 제공 하지 않을 데이터 tooOMS? 내 로그 설정은 tooinfo를 설정 됩니다.
Hello syslog 타임 스탬프에 대 한 ESXi 호스트 버그를 했습니다. 자세한 내용은 참조 hello [VMware 기술 자료](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2111202)합니다. Hello 해결 방법을 적용 한 후 Hostd 정상적으로 작동 합니다.

### <a name="can-i-have-multiple-esxi-hosts-forwarding-syslog-data-tooa-single-vm-with-omsagent"></a>사용할 수 있습니까 여러 ESXi 호스트 syslog 데이터 tooa 전달 omsagent와 VM을 단일?
예. 여러 ESXi 점이 tooa 전달 호스트 omsagent와 VM을 단일 합니다.

### <a name="why-dont-i-see-data-flowing-into-oms"></a>OMS로 이동하는 데이터가 보이지 않는 이유는 무엇입니까?
여러 가지 이유가 있을 수 있습니다.

* hello ESXi 호스트 올바르게 데이터 toohello VM 실행 중인 omsagent를 보내지 됩니다. tootest, hello 다음 단계를 수행 합니다.

  1. tooconfirm, ssh를 사용 하 여 toohello ESXi 호스트에 로그인 하 고 hello 다음 명령을 실행 합니다.`nc -z ipaddressofVM 1514`

      이것이 성공 vSphere 설정 고급 구성은 아마 hello에 해결 되지입니다. 참조 [syslog 컬렉션 구성](#configure-syslog-collection) syslog 전달 하기 위해 tooset hello ESXi 호스트 하는 방법에 대 한 정보에 대 한 합니다.
  2. Syslog 포트 연결에 성공 했지만 데이터를 여전히 표시 되지 않으면, 경우에 hello syslog hello ESXi 호스트를 다시 로드를 사용 하 여 ssh 다음 명령을 toorun hello:` esxcli system syslog reload`
* OMS 에이전트를 사용 하 여 VM hello 올바르게 설정 되지 않았습니다. tootest이 hello 다음 단계를 수행 합니다.

  1. OMS는 toohello 포트 1514 하 고 데이터를 OMS에 넣습니다. 가 열려 tooverify hello 다음 명령을 실행 합니다.`netstat -a | grep 1514`
  2. 포트 `1514/tcp`가 열려 있는지 확인해야 합니다. 그렇지 않으면 해당 hello omsagent 올바르게 설치 되었는지 확인 합니다. Hello 포트 정보를 표시 되지 않으면 hello syslog 포트로 VM hello에 열려 있지 않습니다.

     1. 사용 하 여 OMS 에이전트가 실행 되 고 해당 hello 확인 `ps -ef | grep oms`합니다. 실행 되지 않는 경우 hello 명령을 실행 하 여 hello 프로세스 시작` sudo /opt/microsoft/omsagent/bin/service_control start`
     2. 열기 hello `/etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf` 파일입니다.

         Hello 적절 한 사용자 및 그룹 설정 인지 확인 유효 하 고 비슷합니다.`-rw-r--r-- 1 omsagent omiusers 677 Sep 20 16:46 vmware_esxi.conf`

         Hello 파일 존재 하지 않거나 hello 사용자 및 그룹 설정이 잘못 되었을 경우 하 여 수정 조치 수행 [Linux 서버 준비](#prepare-a-linux-server)합니다.

## <a name="next-steps"></a>다음 단계
* 사용 하 여 [로그 검색](log-analytics-log-searches.md) tooview 로그 분석에 데이터를 호스트 하는 VMware를 자세히 설명 합니다.
* VMware 호스트 데이터를 보여 주는 [사용자 고유의 대시보드 만들기](log-analytics-dashboards.md)
* 특정 VMware 호스트 이벤트가 발생하는 경우의 [경고 만들기](log-analytics-alerts.md)
