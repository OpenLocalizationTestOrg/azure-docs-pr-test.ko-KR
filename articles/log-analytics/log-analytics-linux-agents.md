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
# <a name="connect-your-linux-computers-toolog-analytics"></a>Linux 컴퓨터 tooLog 분석 연결
Log Analytics를 사용하여 Linux 컴퓨터에서 생성되는 데이터를 수집하고 그에 따른 조치를 취할 수 있습니다. Linux tooOMS에서 수집 된 데이터를 추가 하면 toomanage Linux 시스템 및 컴퓨터의 위치에 상관 없이 Docker와 같은 컨테이너 솔루션-어디에서 나 합니다. 데이터 원본 서비스 AWS (Amazon Web) 또는 Microsoft Azure 같은 클라우드 호스팅 서비스의 가상 컴퓨터 물리적 서버로 온-프레미스 데이터 센터에 있는 또는 책상 노트북에도 hello 될 수 있습니다. 뿐만 아니라 OMS는 Windows 컴퓨터에서도 유사하게 데이터를 수집하기 때문에 진정한 하이브리드 IT 환경을 지원합니다.

하나의 관리 포털을 통해 OMS의 Log Analytics에서 이 모든 소스의 데이터를 보고 관리할 수 있습니다. Hello 필요성을 줄이고이 toomonitor 여러 시스템을 사용 하 여 사용 하면 쉽게 tooconsume 있으며 toowhatever 비즈니스 분석 솔루션이 나 시스템에 이미 있는 원하는 모든 데이터를 내보낼 수 있습니다.

이 문서는 Linux 용 OMS 에이전트 hello를 사용 하 여 Linux 컴퓨터에 대 한 데이터 수집 및 관리 하는 데 도움이 되는 빠른 시작 가이드입니다. 프록시 서버 구성, CollectD 메트릭에 대한 정보, 사용자 지정 JSON 데이터 원본과 같은 자세한 기술 정보는 GitHub의 [Linux용 OMS 에이전트 개요](https://github.com/Microsoft/OMS-Agent-for-Linux)(영문) 및 [Linux용 OMS 에이전트 전체 설명서](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md)(영문)를 참조하세요.

현재 Linux 컴퓨터에서 데이터 형식을 따르는 hello를 수집할 수 있습니다.

* 성능 메트릭
* Syslog 이벤트
* Nagios 및 Zabbix의 경고
* Docker 컨테이너 성능 메트릭, 인벤토리 및 로그

## <a name="supported-linux-versions"></a>지원되는 Linux 버전
x86 및 x64 버전 모두 다양한 Linux 배포에 대해 공식적으로 지원됩니다. 그러나 Linux 용 OMS 에이전트 hello 나열 되지 않은 다른 배포 에서도 실행할 수 있습니다.

* Amazon Linux 2012.09~2015.09
* CentOS Linux 5, 6, 7
* Oracle Linux 5, 6, 7
* Red Hat Enterprise Linux Server 5, 6, 7
* Debian GNU/Linux 6, 7, 8
* Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10
* SUSE Linux Enterprise Server 11 및 12

## <a name="oms-agent-for-linux"></a>Linux 용 OMS 에이전트
hello Linux 용 Operations Management Suite 에이전트는 여러 패키지로 구성 됩니다. hello 릴리스 파일 hello 포함 되어 있는지와 함께 hello 셸 번들을 실행 하 여 사용할 수 있는 패키지를 다음 `--extract`합니다.

| **패키지** | **버전** | **설명** |
| --- | --- | --- |
| omsagent |1.1.0 |hello Linux 용 Operations Management Suite 에이전트 |
| omsconfig |1.1.1 |Hello OMS 에이전트에 대 한 구성 에이전트 |
| omi |1.0.8.3 |Open Management Infrastructure(OMI) -- 경량 CIM 서버 |
| scx |1.6.2 |운영 체제 성능 메트릭용 OMI CIM 공급자 |
| apache-cimprov |1.0.0 |OMI용 Apache HTTP 서버 성능 모니터링 공급자. Apache HTTP 서버가 감지되는 경우에만 설치됨. |
| mysql-cimprov |1.0.0 |OMI용 MySQL 서버 성능 모니터링 공급자. MySQL/MariaDB 서버가 감지되는 경우에만 설치됨. |
| docker-cimprov |0.1.0 |OMI용 Docker 공급자. Docker가 감지되는 경우에만 설치됨. |

### <a name="additional-installation-artifacts"></a>추가적인 설치 아티팩트
Linux 패키지에 대 한 hello OMS 에이전트를 설치한 후 hello 다음과 같은 추가 시스템 차원 구성 변경 내용이 적용 됩니다. 이러한 아티팩트는 omsagent 패키지 hello 때 제거 됩니다.

* `omsagent` 라는 이름의 권한 없는 사용자가 생성됩니다. 이 hello 계정을 hello omsagent 디먼이 실행으로
* Sudoers "include" 파일이 만들어집니다 /etc/sudoers.d/omsagent에 권한을 부여 omsagent toorestart hello syslog 및 omsagent 디먼을 합니다. Sudo "include" 지시문은 hello 설치 된 버전의 sudo에서 지원 되지 않는, 너무/등/sudoers 이러한 항목이 기록 됩니다.
* hello syslog 구성이 수정 된 tooforward 이벤트 toohello 에이전트의 하위 집합입니다. 자세한 내용은 참조 hello **데이터 수집 구성** 아래 섹션

### <a name="linux-data-collection-details"></a>Linux 데이터 수집 세부 정보
hello 다음 표에서 데이터 수집 방법과 데이터가 수집 되는 방법에 대 한 기타 세부 정보입니다.

| 원본 | 직접 에이전트 | SCOM 에이전트 | Azure 저장소 | SCOM 필요? | 관리 그룹을 통해 전송되는 SCOM 에이전트 데이터 | 수집 빈도 |
| --- | --- | --- | --- | --- | --- | --- |
| Zabbix |![예](./media/log-analytics-linux-agents/oms-bullet-green.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |1분 |
| Nagios |![예](./media/log-analytics-linux-agents/oms-bullet-green.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |도착 시 |
| syslog |![예](./media/log-analytics-linux-agents/oms-bullet-green.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |Azure 저장소: 10분, 에이전트: 도착 시 |
| Linux 성능 카운터 |![예](./media/log-analytics-linux-agents/oms-bullet-green.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |예약된 대로, 최소 10초 |
| 변경 내용 추적 |![예](./media/log-analytics-linux-agents/oms-bullet-green.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |![아니요](./media/log-analytics-linux-agents/oms-bullet-red.png) |매시간 |

### <a name="package-requirements"></a>패키지 요구 사항
| **필수 패키지** | **설명** | **최소 버전** |
| --- | --- | --- |
| Glibc |GNU C 라이브러리 |2.5-12 |
| Openssl |OpenSSL 라이브러리 |0.9.8e 또는 1.0 |
| Curl |cURL 웹 클라이언트 |7.15.5 |
| Python-ctypes |함수 라이브러리 |해당 없음 |
| PAM |플러그형 인증 모듈 |해당 없음 |

> [!NOTE]
> Rsyslog 또는 syslog-ng 중 하나는 필수 toocollect syslog 메시지입니다. Red Hat Enterprise Linux, CentOS 및 Oracle Linux 버전 (sysklog)의 버전 5에 hello 기본 syslog 디먼은 syslog 이벤트 수집이 지원 되지 않습니다. 이 버전의,이 배포에서 syslog 데이터 toocollect hello rsyslog 디먼을 설치 해야 하며 tooreplace sysklog를 구성 합니다.
>
>

## <a name="quick-install"></a>빠른 설치
다음 명령을 toodownload hello omsagent hello 실행, hello 체크섬 다음 설치 및 등록 hello 에이전트의 유효성을 검사 합니다. 명령은 64비트용입니다. hello 작업 영역 ID와 기본 키에서에서 발견 되 hello OMS 포털에서 **설정** hello에 **연결 된 원본** 탭 합니다.

![작업 영역 정보](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

다양 한 다른 메서드 tooinstall 에이전트 hello을 업그레이드 합니다. 자세한 내용은 [단계 tooinstall hello Linux 용 OMS 에이전트](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux)합니다.

Hello를 볼 수도 있습니다 [Azure 동영상 연습](https://www.youtube.com/watch?v=mF1wtHPEzT0)합니다.

## <a name="choose-your-linux-data-collection-method"></a>Linux 데이터 수집 방법 선택
어떻게 hello toocollect toouse hello OMS 포털을 사용할 것인지에 따라 다릅니다. like 또는 Linux 클라이언트에서 직접 다양 한 구성 파일을 편집 하려는 경우에 데이터 유형을 선택 합니다. Toouse hello 포털을 선택 하면 hello 구성이 tooall Linux 클라이언트를 자동으로 전송 됩니다. Linux 클라이언트 마다 다른 구성 해야 할 경우 tooedit 클라이언트 파일을 개별적으로 필요 하거나 PowerShell DSC, Chef 또는 puppet과 같은 대안을 사용 합니다.

Hello syslog 이벤트를 지정할 수 있습니다 및 toocollect hello Linux 컴퓨터의 구성 파일을 사용 하 여 원하는 성능 카운터입니다. *에이전트 구성 파일을 편집 하 여 tooconfigure 데이터 컬렉션을 선택한 경우 hello 중앙 집중식된 구성을 비활성화 해야 합니다.*  Hello 에이전트의 구성 파일 뿐만 아니라 Linux 또는 개별 컴퓨터에 대 한 모든 OMS 에이전트에 대 한 toodisable 중앙 구성에서 데이터 수집 tooconfigure 아래 설명 되어 있습니다.

### <a name="disable-oms-management-for-an-individual-linux-computer"></a>개별 Linux 컴퓨터에 대한 OMS 관리 비활성화
OMS_MetaConfigHelper.py 스크립트 hello 하 여 개별 Linux 컴퓨터에 대 한 구성 데이터에 대 한 중앙 집중식된 데이터 수집 비활성화 됩니다. 이것은 컴퓨터 하위 집합에 특별한 구성이 필요한 경우에 유용합니다.

toodisable 중앙 집중식된 구성:

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

중앙 집중식된 구성 toore 사용:

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a>Linux 성능 카운터
Linux 성능 카운터는 비슷한 tooWindows 성능 카운터를 둘 다 동일 하 게 작동 합니다. 프로시저 tooadd 다음 hello를 사용 하 고 구성할 수 있습니다. TooOMS, 추가 된 후 데이터 30 초 마다에 수집 됩니다.

### <a name="tooadd-a-linux-performance-counter-in-oms"></a>tooadd OMS에서 Linux 성능 카운터
1. hello OMS 포털을 사용 하 여 Linux 용 OMS 에이전트 tooconfigure Linux 성능 카운터를 추가할 수 있습니다 hello 설정 페이지에서 클릭 **데이터**합니다.  
2. Hello에 **설정** 페이지 **데이터** , 클릭 **Linux 성능 카운터** 이름과 다음 선택 또는 입력 hello tooadd hello 카운터의 원하는 합니다.  
    ![데이터](./media/log-analytics-linux-agents/oms-settings-data01.png)
3. Hello 카운터의 전체 이름을 hello를 모르는 경우 이름의 일부를 입력을 시작할 수 있습니다 하 고 사용 가능한 카운터 목록이 표시 됩니다. Tooadd 원하는 하 hello 목록에 hello 이름을 클릭 한 다음 hello 플러스 tooadd hello 아이콘을 클릭 하 hello 카운터를 찾을 때 카운터입니다.
4. Hello 카운터를 추가한 후 색 막대로 강조 표시 하는 카운터의 hello 목록에 나타납니다.
5. 기본적으로 hello **구성 toomy 컴퓨터 아래 적용** 옵션을 선택 합니다. 구성 데이터를 보내는 toodisable 원한다 면 hello 선택을 취소 합니다.
6. 클릭 하 여 hello hello 페이지 맨 아래에 성능 카운터 수정을 마쳤으면 **저장** toofinalize 변경 내용을 합니다. 일반적으로 5 분 이내에 등록 된 OMS에 Linux 용 hello 구성 변경 내용 아 tooall hello OMS 에이전트로 전송 됩니다.

### <a name="configure-linux-performance-counters-in-oms"></a>OMS에서 Linux 성능 카운터 구성
Windows 성능 카운터의 경우, 각 성능 카운터에 대해 특정 인스턴스를 선택할 수 있습니다. 그러나 Linux 성능 카운터에 대 한 사용자가 선택한 카운터의 카운터 인스턴스가 hello 부모 카운터의 tooall 자식 카운터를 적용 합니다. hello 다음 표에서 hello 공용 인스턴스 사용 가능한 tooboth Linux 맟 Windows 성능 카운터입니다.

| **인스턴스 이름** | **의미** |
| --- | --- |
| \_합계 |모든 hello 인스턴스 |
| \* |모든 인스턴스 |
| (/&#124;/var) |/ 또는 /var로 명명된 인스턴트와 일치 |

마찬가지로, 부모 카운터에 대 한 사용자가 선택한 hello 샘플 간격 자식 카운터 tooall를 적용 합니다. 즉, 모든 hello 자식 카운터의 샘플 간격과 인스턴스가 연결 됩니다.

### <a name="add-and-configure-performance-metrics-with-linux"></a>Linux에서 성능 메트릭 추가 및 구성
성능 메트릭 toocollect/등/옵트인/microsoft/omsagent hello 구성에 의해 제어 됩니다/&lt;작업 영역 id&gt;/conf/omsagent.conf 합니다. 참조 [사용 가능한 성능 메트릭](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) hello Linux 용 OMS 에이전트에 대 한 메트릭 및 사용 가능한 클래스에 대 한 합니다.

각 개체 또는 성능 메트릭 toocollect의 범주는 단일 hello 구성 파일에 정의 되어야 합니다 `<source>` 요소입니다. hello 구문 아래 hello 패턴을 따릅니다.

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

이 요소의 hello 구성 가능한 매개 변수는.

* **개체\_이름**: hello 컬렉션에 대 한 hello 개체 이름입니다.
* **인스턴스\_regex**:는 *정규식* 어떤 인스턴스 toocollect를 정의 합니다. 값 hello: `.*` 모든 인스턴스를 지정 합니다. 만 hello에 대 한 프로세서 메트릭 toocollect \_지정 총 인스턴스 `_Total`합니다. 에 대 한 toocollect 프로세스 메트릭만 crond 또는 sshd 인스턴스에 hello, 지정할 수 있습니다: `(crond|sshd)`합니다.
* **카운터\_이름\_regex**:는 *정규식* 어떤 (hello 개체)에 대 한 카운터 toocollect를 정의 합니다. toocollect hello 개체에 대 한 모든 카운터 지정: `.*`합니다. hello 메모리 개체에 대 한만 스왑 공간 카운터만 toocollect, 다음을 지정할 수 있습니다.`.+Swap.+`
* **간격:**: hello 주파수는 hello 개체의 카운터를 수집 합니다.

성능 메트릭에 대 한 hello 기본 구성은 다음과 같습니다.

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

### <a name="enable-mysql-performance-counters-using-linux-commands"></a>Linux 명령을 사용하여 MySQL 성능 카운터 활성화
Hello omsagent 번들을 설치할 때 hello 컴퓨터에서 MySQL Server 또는 MariaDB 서버가 검색 되 면 한 성능 모니터링 MySQL Server에 대 한 공급자가 자동으로 설치 합니다. 이 공급자는 toohello 로컬 MySQL/MariaDB 서버 tooexpose 성능 통계를 연결합니다. Hello 공급자 액세스할 수 있도록 MySQL 서버 hello tooconfigure MySQL 사용자 자격 증명이 필요 합니다.

toodefine 기본 사용자 계정 MySQL 서버 hello에 대 한 localhost를 사용 하 여 hello 다음 명령 예제에 합니다.

> [!NOTE]
> hello 자격 증명 파일 hello omsagent 계정이 읽을 수 있어야 합니다. 로 hello mycimprovauth 명령을 실행 하는 것이 좋습니다.
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


또는 지정할 수 있습니다 hello hello 파일을 만들어 파일에서 MySQL 자격 증명 필요: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. Hello mysql-auth 파일을 통해 모니터링할 MySQL 자격 증명을 관리 하는 방법에 대 한 자세한 내용은 참조 [관리 MySQL 모니터링 자격 증명 hello 인증 파일에](#manage-mysql-monitoring-credentials-in-the-authentication-file)합니다.

참조 [MySQL 성능 카운터에 필요한 데이터베이스 권한](#database-permissions-required-for-mysql-performance-counters) hello MySQL 사용자 toocollect MySQL Server 성능 데이터에 필요한 개체 사용 권한에 대 한 자세한 내용은 합니다.

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a>Linux 명령을 사용하여 Apache HTTP 서버 성능 카운터 활성화
Apache HTTP Server hello omsagent 번들을 설치할 때 hello 컴퓨터에서 검색 되 면 한 성능 모니터링 공급자 Apache HTTP server가 자동으로 설치 합니다. 이 공급자는 사용 하는 Apache "모듈" 순서 tooaccess 성능 데이터에 hello Apache HTTP Server에 로드 해야 합니다.

다음 명령을 hello로 hello 모듈을 로드할 수 있습니다.

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

toounload hello Apache 모니터링 모듈을 hello 다음 명령을 실행 합니다.

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="tooview-performance-data-with-log-analytics"></a>로그 분석을 사용 하 여 tooview 성능 데이터
1. Hello Operations Management Suite 포털에서 hello 로그 검색 타일을 클릭 합니다.
2. Hello 검색 표시줄에 입력 `* (Type=Perf)` tooview 모든 성능 카운터입니다.

OMS에 Windows 성능 카운터 데이터도 수집 하므로 범위를 좁혀야 hello tooLinux 관련 데이터를 검색 합니다. 따라서 hello 다음 예제에서는 보여 Chorizo21 이라는 성능 데이터 특정 tooan 예제 Linux 서버입니다.

```
Type=Perf Computer=chorizo*
```

![검색 결과에 표시된 예제 서버](./media/log-analytics-linux-agents/oms-perfsearch01.png)

Hello 결과에서 클릭할 수 있는 **메트릭** tooview hello 카운터에 대해 수집 된 데이터입니다. 각 카운터에 대한 실시간 데이터가 그래프로 표시됩니다.

![메트릭](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a>syslog
Syslog는 이벤트 로깅 프로토콜 비슷한 tooWindows 이벤트 로그-둘 다 동일 하 게 작동 OMS에 표시 될 때입니다.

### <a name="tooadd-a-new-linux-syslog-facility-in-oms"></a>tooadd OMS에서 새로운 Linux syslog 기능
1. Hello에 **설정** 페이지의 **데이터** , 클릭 **Syslog** toohello 왼쪽 hello 더하기 아이콘의 이름을 입력 합니다 hello tooadd 원하는 hello syslog 기능입니다.
    ![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)
2. Hello 시설의 전체 이름을 hello를 모르는 경우 이름의 일부를 입력을 시작할 수 있습니다 및 사용 가능한 syslog 기능 목록이 표시 됩니다. Tooadd 원하는 하 hello 목록에서 hello 이름을 클릭 한 다음 hello 및 아이콘 tooadd hello를 클릭 하는 hello syslog 기능을 찾을 때 syslog 기능입니다.
3. Hello 기능을 추가 하면 hello 목록에 나타나고 색된 막대로 강조 표시 됩니다. 다음으로 hello 심각도 (syslog 기능 정보 범주)을 선택 toocollect 되도록 합니다.
4. Hello hello 페이지 맨 아래에 클릭 **저장** toofinalize 변경 내용을 합니다. 일반적으로 5 분 이내에 등록 된 OMS에 Linux 용 hello 구성 변경 내용 아 tooall hello OMS 에이전트로 전송 됩니다.

### <a name="configure-linux-syslog-facilities-in-linux"></a>Linux에서 Linux syslog 기능 구성
Syslog 이벤트는 syslog 디먼 hello 전송 됩니다, 그리고 예를 들어 rsyslog 또는 syslog ng, tooa 로컬 포트 해당 hello 에이전트에서 수신 대기 합니다. 기본 포트는 25224입니다. Hello 에이전트를 설치할 때 기본 syslog 구성이 적용 됩니다. 위치는 다음과 같습니다.

Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf

Syslog-ng: /etc/syslog-ng/syslog-ng.conf

hello 기본 OMS 에이전트 syslog 구성은 심각도 경고 이상인 모든 기능의 syslog 이벤트를에서 업로드합니다.

> [!NOTE]
> Hello syslog 구성을 편집 하는 경우 hello 변경 tootake 효과 대 한 hello syslog 디먼을 다시 시작 해야 합니다.
>
>

hello 기본 syslog 구성은 hello OMS 에이전트에 대 한 Linux 용 OMS에 대 한 다음과 같습니다.

#### <a name="rsyslog"></a>Rsyslog
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

#### <a name="syslog-ng"></a>Syslog-ng
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="tooview-all-syslog-events-with-log-analytics"></a>tooview 로그 분석을 갖는 모든 Syslog 이벤트
1. Hello Operations Management Suite 포털에서 클릭 hello **로그 검색** 바둑판식으로 배열입니다.
2. Hello에 **로그 관리** 미리 정의 된 syslog 검색을 선택한 다음 한 toorun 선택 그룹화 것입니다.

이 예제는 모든 Syslog 이벤트를 보여줍니다.

![로그 검색에 표시된 Syslog 이벤트](./media/log-analytics-linux-agents/oms-linux-syslog.png)

이제 검색 결과를 세부적으로 들여다 볼 수 있습니다.

## <a name="linux-alerts"></a>Linux 경고
Toomanage Nagios 또는 Zabbix를 사용 하 여 Linux 컴퓨터 다음 OMS는 이러한 도구에서 생성 된 hello 경고를 받을 수 있습니다. 그러나 현재 없습니다 메서드 tooconfigure 들어오는 경고 데이터는 hello OMS 포털을 사용 하 여. 대신, tooedit는 config 파일 toostart 보내는 경고 tooOMS 필요 합니다.

### <a name="collect-alerts-from-nagios"></a>Nagios의 경고 수집
Nagios 서버에서 경고 toocollect toomake hello 구성 변경 내용을 수행 해야 합니다.

1. Grant hello 사용자 **omsagent** 읽기 액세스 toohello Nagios 로그 파일 (예: /var/log/nagios/nagios.log). Hello 그룹 hello nagios.log 파일을 소유 하는 것으로 가정 **nagios** , hello 사용자를 추가할 수 있습니다 **omsagent** toohello **nagios** 그룹입니다.

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. Hello omsagent.confconfiguration 파일 수정 (/ 등/옵트인/microsoft/omsagent/&lt;작업 영역 id&gt;/conf/omsagent.conf). 충족 했는지 확인 hello 다음 항목이 있고 주석으로 하지 않습니다.

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
3. Hello omsagent 디먼을 다시 시작 합니다.

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a>Zabbix의 경고 수집
Zabbix 서버에서 경고 toocollect 해야 toospecify 사용자와 암호를 제외 하 고 위의 nagios와 유사한 단계 toothose를 수행 합니다 *일반 텍스트*합니다. 바람직하지는 않지만 곧 변경될 것입니다. tooaddress이이 문제를 좋습니다 hello 사용자 만들고 권한 toomonitor만 권한을 부여 합니다.

Hello omsagent.conf 구성 파일의 예제 섹션 (/ 등/옵트인/microsoft/omsagent/&lt;작업 영역 id&gt;/conf/omsagent.conf)에 대 한 Zabbix hello 다음:

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

### <a name="view-alerts-in-log-analytics-search"></a>Log Analytics 검색에서 경고 보기
프로그램 Linux 컴퓨터 toosend 경고 tooOMS를 구성한 후에 몇 가지 간단한 로그 검색 쿼리 tooview hello 알림을 사용할 수 있습니다. hello 다음 검색 쿼리 예제에서는 반환 생성 된 모든 기록 된 hello 경고 합니다. 예를 들어 IT 인프라에서 일종의 문제가 발생 하는 경우 다음에 대 한 결과 hello 다음 예제 쿼리 hello 문제가 문제가 발생 한 위치를 나타낼 수 있습니다. 및 드릴 수 있습니다 쉽게 toohello 경고 소스 시스템 toohelp 좁은 하 여 조사 합니다. hello 혜택은 반드시 없을 정도로 toogo toovarious 관리 시스템의 hello 시작-있는 경고 tooOMS 보내기 시작할 수 있습니다.

```
Type=Alert
```

#### <a name="tooview-all-nagios-alerts-with-log-analytics"></a>tooview 로그 분석와 모든 Nagios 경고
1. Hello Operations Management Suite 포털에서 클릭 hello **로그 검색** 바둑판식으로 배열입니다.
2. Hello 쿼리 표시줄에 다음 검색 쿼리 hello를 입력 합니다.

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![로그 검색에 표시된 Nagios 경고](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

Hello 검색 결과 본 후 있습니다 수 정보를 상세히 추가 같은 *AlertState*합니다.

### <a name="tooview-all-zabbix-alerts-with-log-analytics"></a>tooview 로그 분석과 함께 모든 Zabbix 경고
1. Hello Operations Management Suite 포털에서 클릭 hello **로그 검색** 바둑판식으로 배열입니다.
2. Hello 쿼리 표시줄에 다음 검색 쿼리 hello를 입력 합니다.

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![로그 검색에 표시된 Zabbix 경고](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

Hello 검색 결과 본 후 있습니다 수 정보를 상세히 추가 같은 *AlertName*합니다.

## <a name="compatibility-with-system-center-operations-manager"></a>System Center Operations Manager와의 호환성
Linux 용 OMS 에이전트 hello hello System Center Operations Manager 에이전트와 에이전트 이진 파일을 공유합니다. 업그레이드는 OMI 및 SCX 패키지가 hello 컴퓨터 tooa 최신 버전을 hello 현재 Operations Manager에서 관리 하는 시스템에 Linux 용 OMS 에이전트 hello를 설치 합니다. Linux 및 System Center 2012 r 2 용 OMS 에이전트 hello 호환 됩니다. 그러나 **System Center 2012 SP1 및 이전 버전은 현재 되지 호환 또는 지원 되는 Linux 용 OMS 에이전트 hello로 합니다.**

> [!NOTE]
> Hello Linux 용 OMS 에이전트는 Operations Manager에서 관리 되지 않는 tooa 설치 된 컴퓨터를 Operations Manager를 사용 하 여 toomanage hello 컴퓨터를 나중에 원하는 hello 컴퓨터를 검색 하기 전에 hello OMI 구성을 수정 해야 합니다. **Linux 용 OMS 에이전트 hello 전에 hello Operations Manager 에이전트가 설치 된 경우에이 단계가 필요 하지 않습니다.**
>
>

### <a name="tooenable-hello-oms-agent-for-linux-toocommunicate-with-operations-manager"></a>Operations Manager와 함께 Linux toocommunicate에 대 한 tooenable hello OMS 에이전트
1. Hello 파일 /etc/opt/omi/conf/omiserver.conf를 편집 합니다.
2. 로 시작 하는 hello 줄 확인 **httpsport =** hello 포트 1270을 정의 합니다. 예: `httpsport=1270`
3. Hello OMI 서버를 다시 시작 합니다.

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a>Database permissions required for MySQL performance counters
toogrant 권한 tooa MySQL 모니터링 사용자, 부여할 hello 권한 뿐만 아니라 ' GRANT option ' hello hello 사용자 있어야 합니다.

MySQL 사용자 hello에 대 한 순서 대로 tooreturn 성능 데이터 hello 사용자가 쿼리를 다음 toohello 액세스할 필요:

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

또한 toothese 쿼리 hello MySQL 사용자에 대 한 SELECT 권한도 toohello를 다음 기본 표 필요 합니다.

* information_schema
* mysql

Hello 다음 grant 명령을 실행 하 여 이러한 권한은 부여할 수 있습니다.

```
GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
GRANT SELECT ON mysql.* too‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-hello-authentication-file"></a>MySQL 모니터링 hello 인증 파일에서 자격 증명 관리
hello 다음 섹션에서는 MySQL 자격 증명을 관리 합니다.

### <a name="configure-hello-mysql-omi-provider"></a>Hello MySQL OMI 공급자 구성
hello MySQL OMI 공급자는 미리 구성 된 MySQL 사용자가 수행 해야 하 고 MySQL 클라이언트 라이브러리가 순서 tooquery hello 성능/상태 정보 hello MySQL 인스턴스를 설치 합니다.

### <a name="mysql-omi-authentication-file"></a>MySQL OMI 인증 파일
MySQL OMI 공급자에서 어떤 바인딩 주소 및 포트 hello MySQL 인스턴스가 수신 대기 하는 인증 파일 toodetermine 및 toouse toogather 메트릭을 자격 증명을 사용 합니다. 하는 동안 설치 hello MySQL OMI 공급자가 바인딩 주소 및 포트와 집합 hello MySQL OMI 인증 파일을 부분적으로 한 MySQL my.cnf 구성 파일 (기본 위치)을 검사 합니다.

MySQL 서버 인스턴스에 대 한 모니터링을 toocomplete hello 올바른 디렉터리에 미리 생성 된 MySQL OMI 인증 파일을 추가 합니다.

### <a name="authentication-file-format"></a>인증 파일 형식
hello MySQL OMI 인증 파일은에 대 한 정보를 포함 하는 텍스트 파일입니다.

* 포트
* 바인딩 주소
* MySQL 사용자 이름
* Base64로 인코딩된 암호

MySQL OMI 인증 파일 hello 생성 한 읽기/쓰기 toohello Linux 사용자에 대 한 권한을 부여 합니다.

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

기본 MySQL OMI 인증 파일에는 기본 인스턴스 및 포트 번호를 사용할 수 있고 hello 발견 된 MySQL 구성 파일에서에서 구문 분석 된 정보에 따라 포함 되어 있습니다.

hello 기본 인스턴스를 보다 쉽게 한 Linux 호스트에서 여러 MySQL 인스턴스를 관리 하는 수단 toomake 이며 포트 0 사용 hello 인스턴스로 표시 됩니다. 추가한 모든 인스턴스는 hello 기본 인스턴스에서 속성 집합을 상속 합니다. 예를 들어 포트 '3308'에서 수신 대기 중인 MySQL 인스턴스가 추가 되 면 hello 기본 인스턴스의 바인딩 주소, username 및 password Base64 인코딩 tootry 사용된 되며 3308에서 수신 대기 하는 hello 인스턴스를 모니터링 합니다. 3308 hello 인스턴스가 바인딩된 tooanother 주소 사용 하 여 hello 동일한 MySQL 사용자 이름 및 암호 쌍에만 다시 지정 하면 되 hello hello 경우 바인딩 주소만 필요 하 고 hello 다른 속성은 상속 됩니다.

Hello 인증 파일의 예는 hello 다음과 유사 합니다.

기본 인스턴스 및 포트 3308 인스턴스:

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

기본 인스턴스 및 포트 3308 및 Base64로 인코딩된 암호가 다른 인스턴스:

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| **속성** | **설명** |
| --- | --- |
| 포트 |Hello 현재 포트 hello를 MySQL 인스턴스가 수신 중인 포트를 나타냅니다.  hello 포트 0 다음 hello 속성이 기본 인스턴스에 대 한 사용 됨을 의미 합니다. |
| 바인딩 주소 |hello 바인딩 주소는 hello 현재 MySQL 바인딩 주소 |
| username |Toouse toomonitor hello MySQL server 인스턴스를 원하는 hello MySQL 사용자의이 hello 사용자 이름. |
| Base64로 인코딩된 암호 |이 base 64로 인코드된 hello MySQL 모니터링 사용자의 hello 암호입니다. |
| AutoUpdate |Hello MySQL OMI 공급자가 업그레이드 hello 공급자 hello my.cnf 파일에서 변경 내용을 다시 검사 되 고 hello MySQL OMI 인증 파일을 덮어쓰게 됩니다. 이 플래그 tootrue에 따라 또는 false 필수 업데이트 toohello MySQL OMI 인증 파일을 설정 합니다. |

#### <a name="authentication-file-location"></a>인증 파일 위치
hello MySQL OMI 인증 파일 hello 수정할 수 있는 위치에에서 있는 하 고 이름이 "mysql-auth" 해야 합니다.

/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth

hello 파일 (및 auth/omsagent 디렉터리) hello omsagent 사용자가 소유 해야 합니다.

## <a name="agent-logs"></a>에이전트 로그
Linux 용 OMS 에이전트 hello에 대 한 hello 로그에는 있습니다.

/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/

hello에 대 한 hello 로그 omsconfig (에이전트 구성) 프로그램에 대 한 Linux 용 OMS 에이전트에는 있습니다.

/var/opt/microsoft/omsconfig/log/

Hello OMI 및 SCX 구성 요소 (성능 메트릭 데이터 제공)에 대 한 로그에는 있습니다.

/var/opt/omi/log/ and /var/opt/microsoft/scx/log

## <a name="troubleshooting-hello-oms-agent-for-linux"></a>Linux 용 OMS 에이전트 hello 문제 해결
다음 정보 toodiagnose hello를 사용 하 여 및 일반적인 문제를 해결 합니다.

None hello 문제 해결이 섹션의 정보를 사용 하면, 하는 경우 다음 리소스 toohelp 해결 hello를 문제도 사용할 수 있습니다.

* 프리미어 지원이 적용되는 고객의 경우 [프리미어](https://premier.microsoft.com/)를 통해 지원 사례를 기록할 수 있습니다.
* Azure 지원 계약이 있는 고객 hello 지원 사례 로그인 수 [Azure 포털](https://manage.windowsazure.com/?getsupport=true)
* [GitHub 문제](https://github.com/Microsoft/OMS-Agent-for-Linux/issues) 제출
* 아이디어와 toocreate 버그 보고서에 대 한 피드백 포럼 [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)

### <a name="important-log-locations"></a>중요 로그 위치
| 파일 | Path |
| --- | --- |
| Linux 용 OMS 에이전트 로그 파일 |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| OMS 에이전트 구성 로그 파일 |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a>중요 구성 파일
| 범주 | 파일 위치 |
| --- | --- |
| syslog |`/etc/syslog-ng/syslog-ng.conf` 또는 `/etc/rsyslog.conf` 또는 `/etc/rsyslog.d/95-omsagent.conf` |
| 성능, Nagios, Zabbix, OMS 출력 및 일반 에이전트 |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| 추가 구성 |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> OMS 포털 구성을 사용하도록 설정한 경우 시스템에서 성능 카운터 및 syslog의 편집 구성 파일을 덮어씁니다. (모든 노드)에 대 한 hello OMS 포털에서에서 구성을 해제할 수 있습니다 또는 hello 다음을 실행 하 여 단일 노드에 대 한 합니다.
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a>디버그 로깅 활성화
tooenable 디버그 로깅을 사용할 수 있습니다 hello OMS 출력 플러그 인 및 자세한 정보를 출력 합니다.

#### <a name="oms-output-plugin"></a>OMS 출력 플러그인
FluentD는 hello 플러그 인 toospecify 입 / 출력에 대 한 다른 로그 수준에 대 한 로깅 수준을 수 있습니다. hello에 hello 일반 에이전트 구성을 편집 하는 OMS 출력에 대 한 다른 로그 수준을 toospecify `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` 파일입니다.

Hello 아래 근처의 hello 구성 파일을 변경 hello `log_level` 속성 `info` 너무`debug`합니다.

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

디버그 로깅을 사용 하면 데이터 항목 및 toosend에 걸린 시간 단위의 시간을 입력 하 여 OMS 서비스로 구분 된 일괄 처리 toosee 업로드 toohello 있습니다.

*디버그 사용 로그 예:*

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a>자세한 정보 출력
Hello OMS 출력 플러그 인을 사용 하는 대신 있습니다도 출력 데이터 항목 직접 너무`stdout`는 Linux 로그 파일에 대 한 hello OMS 에이전트에에서 표시 됩니다.

Hello OMS 일반 에이전트 구성 파일에서 `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, 주석 아웃 hello OMS 추가 하 여 플러그 인을 출력 한 `#` 각 줄 앞에 있습니다.

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

아래 출력 플러그 인 hello, hello hello를 제거 하 여 섹션 다음에 hello 주석 제거 `#` 각 줄의 시작 hello 기호입니다.

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-hello-log"></a>전달 된 Syslog 메시지 hello 로그에 표시 되지 않습니다.
#### <a name="probable-causes"></a>가능한 원인
* hello 적용 된 구성 toohello Linux 서버 않습니다 하지 컬렉션 hello 전송 기능을 허용 및/또는 로그 수준
* Syslog는 전달 되지 않고 올바르게 toohello Linux 서버
* hello에 대 한 Linux toohandle hello OMS 에이전트의 기본 구성에 대 한 초당 전달 된 메시지의 hello 수가 너무 큽니다.

#### <a name="resolutions"></a>해결 방법
* Syslog 모든 hello 시설 및 hello 올바른 로그 수준에 대 한 hello OMS 포털에서에서 해당 hello 구성 확인
  * **OMS 포털 > 설정 > 데이터 > Syslog**
* 해당 기본 syslog 디먼 메시징 확인 (`rsyslog`, `syslog-ng`)는 수 tooreceive 전달 hello 메시지
* 메시지가 차단 되는 hello Syslog 서버 tooensure에서 방화벽 설정을 확인합니다
* Hello를 사용 하 여 Syslog 메시지 tooOMS 시뮬레이션 `logger` 명령-예:
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-toooms-when-using-a-proxy"></a>프록시를 사용할 때 tooOMS 연결 문제
#### <a name="probable-causes"></a>가능한 원인
* hello 프록시가 지정 hello 에이전트를 설치 및 구성 올바르지 않은 경우
* 사용할 수 없는 데이터 센터에서 whitelistested hello OMS 서비스 끝점

#### <a name="resolutions"></a>해결 방법
* 다음 명령을 hello 옵션을 사용 하는 hello를 사용 하 여 Linux 용 OMS 에이전트 hello를 다시 설치 `-v` 사용 하도록 설정 합니다. 이렇게 하면 hello 프록시 toohello OMS 서비스를 통해 연결 하는 hello 에이전트의 자세한 정보를 출력 합니다.
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * OMS에는 프록시에 대 한 hello 설명서를 검토 [HTTP 프록시 서버와 함께 사용할 hello 에이전트 구성](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)
* OMS 서비스 끝점을 다음 해당 hello 허용 목록 확인

| 에이전트 리소스 | 포트 |
| --- | --- |
| &#42;.ods.opinsights.azure.com |포트 443 |
| &#42;.oms.opinsights.azure.com |포트 443 |
| ods.systemcenteradvisor.com |포트 443 |
| &#42;.blob.core.windows.net/ |포트 443 |

### <a name="a-403-error-is-displayed-when-onboarding"></a>등록 시 403 오류가 표시됨
#### <a name="probable-causes"></a>가능한 원인
* hello 날짜 및 시간 Linux 서버에서 올바르지 않습니다.
* hello 작업 영역 ID 및 사용 되는 작업 영역 키 올바르지 않습니다.

#### <a name="resolution"></a>해결 방법
* Linux 서버 hello hello 시간 확인 `date` 명령입니다. 데이터 보다 큽니다. hello 또는에서 15 분 미만 hello 현재 시간, 온 보 딩 실패 합니다. toocorrect이 hello 날짜 및/또는 Linux 서버에의 표준 시간대를 업데이트 합니다.
* hello Linux 용 OMS 에이전트의 최신 버전 hello 알림을 표시 시간 차이가 온 보 딩 오류로 인해 발생 한 경우
* 올바른 작업 영역 ID와 작업 영역 키 hello 사용 하 여 다시 등록 합니다. 참조 [hello 명령줄을 사용 하는 온 보 딩](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) 자세한 정보에 대 한 합니다.

### <a name="a-500-error-or-404-error-appears-in-hello-log-file-after-onboarding"></a>500 오류 또는 404 오류 뒤에 표시 hello 로그 파일에 온 보 딩
OMS 작업 영역에 Linux 데이터의 hello 첫 번째 업로드 중에 발생 하는 알려진된 문제입니다. 이 문제는 전송되는 데이터 또는 다른 문제에 영향을 미치지 않습니다. Hello 오류 때 처음에 무시할 수 있습니다 등록 합니다.

### <a name="nagios-data-does-not-appear-in-hello-oms-portal"></a>Nagios 데이터 hello OMS 포털에에서 표시 되지 않습니다.
#### <a name="probable-causes"></a>가능한 원인
* hello omsagent 사용자가 없는 사용 권한을 tooread hello Nagios 로그 파일에서
* hello Nagios 원본 및 필터 섹션 hello omsagent.conf 파일에서 여전히 주석

#### <a name="resolutions"></a>해결 방법
* Hello Nagios 파일에서 순서 tooread에 hello omsagent 사용자를 추가 합니다. 자세한 내용은 [Nagios 경고](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts)를 참조하세요.
* 에 OMS 에이전트에서 Linux 일반 구성 파일에 대 한 hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, 되도록 **둘 다** Nagios 제거 의견을 포함 하는 원본 및 필터 섹션에서는 다음 예제와 비슷한 toohello hello 합니다.

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


### <a name="linux-data-doesnt-appear-in-hello-oms-portal"></a>Linux 데이터 hello OMS 포털에에서 표시 되지 않으면
#### <a name="probable-causes"></a>가능한 원인
* 온 보 딩 toohello OMS 서비스 하지 못했습니다.
* OMS 서비스에서 차단 되는 연결 toohello
* Linux 데이터에 대 한 OMS 에이전트 hello는 백업

#### <a name="resolutions"></a>해결 방법
* 해당 hello를 확인 하 여 해당 온 보 딩 toohello OMS 서비스에 성공 했는지 확인 `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` 존재 합니다.
* Omsadmin.sh 명령줄 hello 사용 하 여 다시 등록 합니다. 참조 [hello 명령줄을 사용 하는 온 보 딩](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) 자세한 정보에 대 한 합니다.
* Hello 프록시 문제 해결 위의 단계를 사용 하 여 프록시를 사용 하는 경우
* 경우에 따라 Linux 용 OMS 에이전트 hello hello OMS 서비스와 통신할 수 없는 경우 hello 에이전트에서 데이터에는 50MB의 백업 toohello 가득 찬 버퍼 크기입니다. Hello를 실행 하 여 Linux 용 OMS 에이전트 hello를 다시 시작 `/opt/microsoft/omsagent/bin/service_control restart` 명령입니다.
  >[AZURE.NOTE] 이 문제는 에이전트 버전 1.1.0-28 및 이상에서 해결되었습니다.

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-hello-oms-portal"></a>Syslog Linux 성능 카운터 구성 hello OMS 포털에서 적용 되지 않음
#### <a name="probable-causes"></a>가능한 원인
* Linux 용 OMS 에이전트 hello에 hello 구성 에이전트 hello OMS 포털에서 hello 최신 구성을 검색 했습니다.
* hello hello 포털에서 수정 된 설정은 적용 되지 않았습니다.

#### <a name="resolutions"></a>해결 방법
`omsconfig`linux 5 분 마다 OMS 포털 구성 변경 내용을 검색 하는 hello OMS 에이전트의에서 hello 구성 에이전트입니다. 이 구성은 Linux 구성 파일에 대 한 적용 된 toohello OMS 에이전트에 있는 다음 `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`합니다.

* 경우에 따라 Linux 구성 에이전트에 대 한 OMS 에이전트 hello hello 포털 구성 서비스에 최신 구성을 적용 하지 수 toocommunicate 아닐 수 있습니다.
* 해당 hello 확인 `omsconfig` 에이전트 hello 다음와 함께 설치 됩니다.

  * `dpkg --list omsconfig` 또는 `rpm -qi omsconfig`
  * 설치 되어 있지 않으면 Linux 용 hello 최신 버전의 hello OMS 에이전트를 다시 설치
* 해당 hello 확인 `omsconfig` 에이전트 hello OMS 서비스와 통신할 수

  * Hello 실행 `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` 명령
    * hello 위의 명령을 반환 hello 구성 해당 에이전트에서 Syslog 설정, Linux 성능 카운터 및 사용자 지정 로그를 포함 하 여 hello 포털 검색
    * 위의 hello 명령이 실패 하면 실행 hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` 명령입니다. 이 명령은 hello OMS 서비스 tooretrieve hello 최신 구성 사용 하 여 hello omsconfig 에이전트 toocommunicate가 되도록합니다.

### <a name="custom-linux-log-data-does-not-appear-in-hello-oms-portal"></a>사용자 지정 Linux 로그 데이터 hello OMS 포털에에서 표시 되지 않습니다.
#### <a name="probable-causes"></a>가능한 원인
* 온 보 딩 tooOMS 서비스 하지 못했습니다.
* hello **구성 toomy Linux 서버에 따라 적용 hello** 설정을 선택 하지
* omsconfig은 hello hello 포털에서 최신 사용자 지정 로그 선택 되지 않은
* hello `omsagent` 사용은 없습니다 tooaccess hello tooa 사용 권한 문제로 인해 사용자 지정 로그 또는 `omsagent` 찾을 수 없습니다. 이 경우 hello 출력 뒤에 표시 됩니다.
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* 이 Linux 버전 1.1.0-217에 대 한 hello OMS 에이전트에서에서 수정 된 경합 상태 hello로 알려진된 문제

#### <a name="resolutions"></a>해결 방법
* 작업이 성공적으로 사용, 되는지 hello 확인 하 여 확인 `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` 파일이 있습니다.
  * 필요한 경우 hello omsadmin.sh 명령줄을 사용 하 여 다시 등록 합니다. 참조 [hello 명령줄을 사용 하는 온 보 딩](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) 자세한 정보에 대 한 합니다.
* 에 OMS 포털을 아래 hello **설정** hello에 **데이터** 탭에서 해당 hello 확인 **적용 hello 구성 toomy Linux 서버 다음** 설정을 선택  
  ![구성 적용](./media/log-analytics-linux-agents/customloglinuxenabled.png)
* 해당 hello 확인 `omsconfig` 에이전트 hello OMS 서비스와 통신할 수

  * Hello 실행 `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` 명령
  * hello 위의 명령을 반환 hello 구성 에이전트에 hello Syslog 설정, Linux 성능 카운터 및 사용자 지정 로그를 포함 하 여 포털에서에서 검색
  * 위의 hello 명령이 실패 하면 실행 hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` 명령입니다. 이 명령은 OMS 서비스와 hello omsconfig 에이전트 toocommunicate 강제로 hello 최신 구성을 검색 합니다.

권한 있는 사용자로 실행 하는 Linux 사용자에 대 한 OMS 에이전트 hello 대신 `root`, Linux hello로 실행에 대 한 OMS 에이전트 hello `omsagent` 사용자입니다. 대부분의 경우에서 명시적 사용 권한이 있어야 toohello 사용자 순서 tooread에 특정 파일을 부여 합니다.

toogrant 권한이 너무`omsagent` hello 다음 명령을 실행 사용자:

1. Hello 추가 `omsagent` 으로 사용자 tooa 특정 그룹`sudo usermod -a -G <GROUPNAME> <USERNAME>`
2. 공용 읽기 액세스 toohello 필요한 파일을 부여 합니다.`sudo chmod -R ugo+rw <FILE DIRECTORY>`

Hello Linux 버전 1.1.0-217에 대 한 hello OMS 에이전트에서에서 수정 된 경합 상태는 알려진된 문제가 있습니다. Toohello 최신 에이전트를 업데이트 한 후 명령 tooget hello hello 출력 플러그 인을 최신 버전을 다음 hello를 실행 합니다.

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a>알려진 제한 사항
다음 섹션에서는 toolearn Linux 용 OMS 에이전트 hello의 현재 제한 사항에 대 한 hello를 검토 합니다.

### <a name="azure-diagnostics"></a>Azure 진단
Azure에서 실행 중인 Linux 가상 컴퓨터에 대 한 추가 단계는 Azure 진단 및 Operations Management Suite에서 필요한 tooallow 데이터 수집을 수 있습니다. **버전 2.2** hello의 Linux 용 진단 확장은 hello Linux 용 OMS 에이전트와의 호환성에 필요 합니다.

설치 및 Linux 용 진단 확장 hello 구성에 대 한 자세한 내용은 참조 하십시오. [hello Azure CLI 명령을 tooenable Linux 진단 확장을 사용 하 여](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension)합니다.

**Hello Linux 진단 확장에서 2.0 too2.2 Azure CLI ASM으로 업그레이드:**

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

**ARM**

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

이 코드 예제는 PrivateConfig.json이라는 이름의 파일을 참조합니다. 해당 파일의 hello 형식은 다음 샘플 hello와 비슷해야 합니다.

```
    {
    "storageAccountName":"hello storage account tooreceive data",
    "storageAccountKey":"hello key of hello account"
    }
```

### <a name="sysklog-is-not-supported"></a>Sysklog가 지원되지 않습니다.
Rsyslog 또는 syslog-ng 중 하나는 필수 toocollect syslog 메시지입니다. Red Hat Enterprise Linux, CentOS 및 Oracle Linux 버전 (sysklog)의 버전 5에 hello 기본 syslog 디먼은 syslog 이벤트 수집이 지원 되지 않습니다. 이 버전의,이 배포에서 syslog 데이터 toocollect hello rsyslog 디먼을 설치 해야 하며 tooreplace sysklog를 구성 합니다. Sysklog를 rsyslog로에 대 한 자세한 내용은 참조 하십시오. [hello 새로 빌드된 rsyslog RPM 설치](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM)합니다.

## <a name="next-steps"></a>다음 단계
* [로그 분석 솔루션 hello 솔루션 갤러리에서에서 추가](log-analytics-add-solutions.md) tooadd 기능 및 수집 데이터입니다.
* 익숙해질 목적으로 [검색 로그](log-analytics-log-searches.md) tooview 솔루션에서 수집 된 정보를 자세히 설명 합니다.
* 사용 하 여 [대시보드](log-analytics-dashboards.md) toosave 및 표시 사용자 지정 검색 합니다.
