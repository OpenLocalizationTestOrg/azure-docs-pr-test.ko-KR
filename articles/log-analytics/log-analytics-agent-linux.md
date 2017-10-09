---
title: "aaaConnect 프로그램 Linux 컴퓨터 tooOperations Management Suite (OMS) | Microsoft Docs"
description: "이 문서에서는 tooconnect Linux 컴퓨터 다른 클라우드 또는 온-프레미스 tooOMS Linux 용 OMS 에이전트 hello를 사용 하 여 Azure에서 호스트 되는 방법을 설명 합니다."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte
ms.openlocfilehash: cb4fc671d0678f9fadc689c6ba7d719213aa61b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toooperations-management-suite-oms"></a>프로그램 Linux 컴퓨터 tooOperations Management Suite (OMS) 연결 

Microsoft OMS(Operations Management Suite)를 사용하여 물리적 서버 또는 가상 컴퓨터로서 온-프레미스 데이터 센터에 상주하는 Linux 컴퓨터 및 컨테이너 솔루션(예: Docker), AWS(Amazon Web Services) 또는 Microsoft Azure와 같은 클라우드 호스티드 서비스에서 생성된 데이터를 수집하고 이러한 데이터로 작업을 수행할 수 있습니다. 업데이트 관리 toomanage 소프트웨어 업데이트 tooproactively Linux Vm의 hello 수명 주기 관리 및 변경 내용 추적, tooidentify 구성 변경 등 OMS에서 사용할 수 있는 관리 솔루션을 사용할 수도 있습니다. 

hello OMS 에이전트 hello 컴퓨터 hello 인터넷을 통해 tooa 방화벽 또는 프록시 서버 toocommunicate 연결 및 TCP 포트 443 통해 Linux OMS 서비스 hello로 아웃 바운드 통신에 대 한 검토 [구성 hello에 사용할 에이전트를 HTTP 프록시 서버 또는 게이트웨이 OMS](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway) 구성을 변경 toounderstand toobe 적용 해야 합니다.  System Center 2016-Operations Manager 또는 Operations Manager 2012 r 2를 사용 하 여 hello 컴퓨터를 모니터링 하는 경우 hello OMS 서비스 toocollect 데이터 및 전달 toohello 서비스를 사용한 다중 홈 일 수 있으며 여전히 Operations Manager로 모니터링할 수 있습니다.  OMS와 통합 된 Operations Manager 관리 그룹에서 모니터링 하는 Linux 컴퓨터는 데이터 원본에 대 한 구성을 수신 하지 않음 및 앞으로 hello 관리 그룹을 통해 데이터를 수집 합니다.  hello OMS 에이전트에는 하나의 작업 영역 보다 구성된 tooreport toomore 일 수 없습니다.  

Hello 에이전트 구성된 tooconnect toohello OMS 게이트웨이 tooreceive 구성 정보 수 있고 있는 hello 솔루션에 따라 수집 된 데이터를 보낼 경우 IT 보안 정책을 네트워크 tooconnect toohello 인터넷에서 컴퓨터를 허용 하지 않으므로, 사용할 수 있습니다. 자세한 내용 및 단계 tooconfigure OMS 게이트웨이 toohello OMS 서비스를 통해 OMS Linux 에이전트 toocommunicate 프로그램 참조에 대 한 [hello OMS 게이트웨이 사용 하 여 컴퓨터 tooOMS 연결](log-analytics-oms-gateway.md)합니다.  

hello 다음 다이어그램은 Linux 컴퓨터를 에이전트 관리 하는 hello와 hello 방향 및 포트를 포함 하 여 OMS로 hello 연결 합니다.

![OMS와 에이전트의 직접 통신 다이어그램](./media/log-analytics-agent-linux/log-analytics-agent-linux-communication.png)

## <a name="system-requirements"></a>시스템 요구 사항
을 시작 하기 전에 다음 세부 정보 tooverify hello 필수 조건을 충족 하는 hello를 검토 합니다.

### <a name="supported-linux-operating-systems"></a>지원되는 Linux 운영 체제
다음의 Linux 배포판 hello 공식적으로 지원 됩니다.  그러나 Linux 용 OMS 에이전트 hello 나열 되지 않은 다른 배포 에서도 실행할 수 있습니다.

* Amazon Linux 2012.09 too2015.09 (x86/x64)
* CentOS Linux 5, 6 및 7(x86/x64)
* Oracle Linux 5, 6 및 7(x86/x64)
* Red Hat Enterprise Linux Server 5, 6 및 7(x86/x64)
* Debian GNU/Linux 6, 7, 8(x86/x64)
* Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS(x86/x64)
* SUSE Linux Enterprise Server 11 및 12(x86/x64)

### <a name="network"></a>네트워크
방화벽 구성 정보와 hello 정보 hello 프록시 목록 아래에 필요한 hello OMS와 함께 Linux 에이전트 toocommunicate입니다. 트래픽은은 네트워크 toohello OMS 서비스에서 아웃 바운드입니다. 

|에이전트 리소스| 포트 |  
|------|---------|  
|*.ods.opinsights.azure.com | 포트 443|   
|*.oms.opinsights.azure.com | 포트 443|   
|*.blob.core.windows.net/ | 포트 443|   
|*.azure-automation.net | 포트 443|  

### <a name="package-requirements"></a>패키지 요구 사항

 **필수 패키지**   | **설명**   | **최소 버전**
--------------------- | --------------------- | -------------------
Glibc | GNU C 라이브러리   | 2.5-12 
Openssl | OpenSSL 라이브러리 | 0.9.8e 또는 1.0
Curl | cURL 웹 클라이언트 | 7.15.5
Python-ctypes | | 
PAM | 플러그형 인증 모듈 | 

> [!NOTE]
>  Rsyslog 또는 syslog-ng 중 하나는 필수 toocollect syslog 메시지입니다. Red Hat Enterprise Linux, CentOS 및 Oracle Linux 버전 (sysklog)의 버전 5에 hello 기본 syslog 디먼은 syslog 이벤트 수집이 지원 되지 않습니다. 이 버전의,이 배포에서 syslog 데이터 toocollect hello rsyslog 디먼을 설치 해야 하며 tooreplace sysklog를 구성 합니다. 

hello 에이전트는 여러 패키지에 포함 됩니다. hello 릴리스 파일 hello 포함 되어 있는지와 함께 hello 셸 번들을 실행 하 여 사용할 수 있는 패키지를 다음 `--extract`:

**패키지** | **버전** | **설명**
----------- | ----------- | --------------
omsagent | 1.4.0 | hello Linux 용 Operations Management Suite 에이전트
omsconfig | 1.1.1 | Hello OMS 에이전트에 대 한 구성 에이전트
omi | 1.2.0 | Open Management Infrastructure(OMI) -- 경량 CIM 서버
scx | 1.6.3 | 운영 체제 성능 메트릭용 OMI CIM 공급자
apache-cimprov | 1.0.1 | OMI용 Apache HTTP 서버 성능 모니터링 공급자. Apache HTTP 서버가 감지되면 설치됨.
mysql-cimprov | 1.0.1 | OMI용 MySQL 서버 성능 모니터링 공급자. MySQL/MariaDB 서버가 감지되면 설치됨.
docker-cimprov | 1.0.0 | OMI용 Docker 공급자. Docker가 감지되면 설치됨.

### <a name="compatibility-with-system-center-operations-manager"></a>System Center Operations Manager와의 호환성
Linux 용 OMS 에이전트 hello hello System Center Operations Manager 에이전트와 에이전트 이진 파일을 공유합니다. Operations Manager에서 현재 관리 시스템에 Linux 용 OMS 에이전트 hello를 설치한 경우에 OMI 및 SCX 패키지가 hello 컴퓨터 tooa 최신 버전 hello 합니다. 이 릴리스에서 OMS hello 및 System Center 2016-Linux 용 Operations Manager/Operations Manager 2012 R2 에이전트는 호환입니다. 

> [!NOTE]
> System Center 2012 SP1 및 이전 버전 현재 호환 또는 아닌 지원 되는 Linux 용 OMS 에이전트 hello로 합니다.<br>
> Hello Linux 용 OMS 에이전트는 Operations Manager에서 모니터링 하지 않는 tooa 설치 된 컴퓨터 이며 toomonitor hello 컴퓨터를 Operations Manager를 다음 원하는 수정 해야 hello [OMI 구성을](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager) 이전 toodiscovering hello 컴퓨터입니다. **이 단계는 *하지* Linux 용 OMS 에이전트 hello 전에 hello Operations Manager 에이전트가 설치 된 경우에 필요 합니다.**

### <a name="system-configuration-changes"></a>시스템 구성 변경 내용
Linux 패키지에 대 한 hello OMS 에이전트를 설치한 후 hello 다음과 같은 추가 시스템 차원 구성 변경 내용이 적용 됩니다. 이러한 아티팩트는 omsagent 패키지 hello 때 제거 됩니다.

* `omsagent` 라는 이름의 권한 없는 사용자가 생성됩니다. 이 hello 계정을 hello omsagent 디먼이 실행으로입니다.
* sudoers "include" 파일은 /etc/sudoers.d/omsagent에 생성됩니다. Omsagent toorestart hello syslog 및 omsagent 디먼을이 권한을 부여합니다. Sudo "include" 지시문은 hello 설치 된 버전의 sudo에서 지원 되지 않는, 이러한 항목에는 너무/등/sudoers 기록 됩니다.
* hello syslog 구성이 수정 된 tooforward 이벤트 toohello 에이전트의 하위 집합입니다. 자세한 내용은 참조 hello **데이터 수집 구성** 아래 섹션

### <a name="upgrade-from-a-previous-release"></a>이전 릴리스에서 업그레이드
이 릴리스에서는 1.0.0-47보다 이전 버전에서 업그레이드하도록 지원됩니다. Hello로 hello 설치 수행 `--upgrade` hello 에이전트 toohello 최신 버전의 모든 구성 요소를 업그레이드 하는 명령입니다.

## <a name="installing-hello-agent"></a>Hello 에이전트 설치

이 섹션에서는 각 hello 에이전트 구성 요소에 대 한 tooinstall hello Debian 및 RPM을 포함 하는 bunndle를 사용 하 여 Linux 용 OMS 에이전트 패키지 하는 방법을 설명 합니다.  직접 설치 하거나, tooretrieve hello 개별 패키지를 추출 합니다.  

OMS 작업 영역 ID 및 toohello 전환 하 여 찾을 수 있는 키를 먼저 [OMS 클래식 포털](https://mms.microsoft.com)합니다.  Hello에 **개요** hello 상단 메뉴 선택에서 페이지에서 **설정**를 이동한 후 너무**Sources\Linux 연결 된 서버**합니다.  Hello 값 toohello 오른쪽의 참조 **작업 영역 ID** 및 **기본 키**합니다.  두 항목을 복사하여 선호하는 편집기에 붙여넣습니다.    

1. 최신 버전 다운로드 hello [(x64) Linux 용 OMS 에이전트](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) 또는 [x86 Linux 용 OMS 에이전트](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh) GitHub에서 합니다.  
2. Hello 적절 한 번들 (x86 또는 x64) tooyour Linux 컴퓨터 scp/sftp를 사용 하 여 전송 합니다.
3. Hello를 사용 하 여 설치 hello 번들 `--install` 또는 `--upgrade` 인수입니다. 

    > [!NOTE]
    > Linux 용 System Center Operations Manager 에이전트 hello 이미 설치 되어 같은 기존 패키지가 설치 된 경우 사용 하 여 hello `--upgrade` 인수입니다. 설치 하는 동안 tooconnect tooOperations 관리 제품군을 제공 hello `-w <WorkspaceID>` 및 `-s <Shared Key>` 매개 변수입니다.


#### <a name="tooinstall-and-onboard-directly"></a>tooinstall 직접 등록
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key>
```

#### <a name="tooupgrade-hello-agent-package"></a>tooupgrade hello 에이전트 패키지
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade
```

#### <a name="tooinstall-and-onboard-tooa-workspace-in-us-government-cloud"></a>tooinstall 및 미국 정부 클라우드에서 온보드 tooa 작업 영역
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key> -d opinsights.azure.us
```

## <a name="configuring-hello-agent-for-use-with-an-http-proxy-server-or-oms-gateway"></a>HTTP 프록시 서버 또는 게이트웨이 OMS와 사용 하기 위해 hello 에이전트 구성
hello Linux 용 OMS 에이전트는 HTTP 또는 HTTPS 프록시 서버 또는 게이트웨이 OMS toohello OMS 서비스를 통해 통신을 지원 합니다.  익명 및 기본 인증(사용자 이름/암호) 둘 다 지원됩니다.  

### <a name="proxy-configuration"></a>프록시 구성
hello 프록시 구성 값 hello 구문 다음에 있습니다.

`[protocol://][user:password@]proxyhost[:port]`

속성|설명
-|-
프로토콜|HTTP 또는 HTTPS
사용자|프록시 인증을 위한 선택적 사용자 이름
password|프록시 인증을 위한 선택적 암호
proxyhost|주소 또는 FQDN hello 프록시 서버/oms 게이트웨이
포트|Hello 프록시 서버/OMS 게이트웨이 대 한 선택적 포트 번호

예: `http://user01:password@proxy01.contoso.com:8080`

설치 중에 또는 설치 후 hello proxy.conf 구성 파일을 수정 하 여 hello 프록시 서버를 지정할 수 있습니다.   

### <a name="specify-proxy-configuration-during-installation"></a>설치 중 프록시 구성 지정
hello `-p` 또는 `--proxy` hello omsagent 설치 번들에 대 한 인수는 hello 프록시 구성 toouse를 지정 합니다. 

```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -p http://<proxy user>:<proxy password>@<proxy address>:<proxy port> -w <workspace id> -s <shared key>
```

### <a name="define-hello-proxy-configuration-in-a-file"></a>Hello 프록시 구성 파일에 정의
hello 프록시 구성을 hello 파일에서 설정할 수 있습니다 `/etc/opt/microsoft/omsagent/proxy.conf` 및 `/etc/opt/microsoft/omsagent/conf/proxy.conf `합니다. hello 파일을 직접 생성 하거나, 편집 하지만 해당 사용 권한을 업데이트 toogrant hello omiuser 사용자 hello 파일에 대해 읽기 권한을 이어야 합니다. 예:
```
proxyconf="https://proxyuser:proxypassword@proxyserver01:8080"
sudo echo $proxyconf >>/etc/opt/microsoft/omsagent/proxy.conf
sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf
sudo chmod 600 /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf  
sudo /opt/microsoft/omsagent/bin/service_control restart [<workspace id>]
```

### <a name="removing-hello-proxy-configuration"></a>Hello 프록시 구성을 제거 하는
이전에 정의 된 프록시 구성 tooremove toodirect 연결 되돌릴, hello proxy.conf 파일을 제거 하 고 있습니다.
```
sudo rm /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf
sudo /opt/microsoft/omsagent/bin/service_control restart 
```

## <a name="onboarding-with-operations-management-suite"></a>Operations Management Suite에 등록
작업 영역 ID 및 키 hello 번들 설치 도중 제공 되지 않았습니다 hello 에이전트 Operations Management Suite로 이후에 등록 합니다.

### <a name="onboarding-using-hello-command-line"></a>Hello 명령줄을 사용 하는 온 보 딩
작업 영역에 대 한 키 및 hello 작업 영역 id를 제공 하는 hello omsadmin.sh 명령을 실행 합니다. 이 명령은 루트 권한(sudo 권한 상승)으로 실행해야 합니다.
```
cd /opt/microsoft/omsagent/bin
sudo ./omsadmin.sh -w <WorkspaceID> -s <Shared Key>
```

### <a name="onboarding-using-a-file"></a>파일을 사용하는 등록
1.  Hello 파일을 만들 `/etc/omsagent-onboard.conf`합니다. 읽기 및 쓰기 가능한 루트에 대 한 hello 파일 이어야 합니다.
`sudo vi /etc/omsagent-onboard.conf`
2.  작업 영역 ID와 공유 키 hello 파일에 있는 줄을 다음 hello를 삽입 합니다.

        WORKSPACE_ID=<WorkspaceID>  
        SHARED_KEY=<Shared Key>  
   
3.  다음 명령은 tooOnboard tooOMS hello를 실행 합니다.`sudo /opt/microsoft/omsagent/bin/omsadmin.sh`
4.  등록에 hello 파일이 삭제 됩니다.

## <a name="enable-hello-oms-agent-for-linux-tooreport-toosystem-center-operations-manager"></a>Linux tooreport tooSystem Center Operations Manager에 대 한 hello OMS 에이전트를 사용 하도록 설정
Hello Linux tooreport tooa System Center Operations Manager 관리 그룹에 대 한 단계 tooconfigure hello OMS 에이전트를 다음을 수행 합니다.  

1. Hello 파일 편집`/etc/opt/omi/conf/omiserver.conf`
2. 로 시작 하는 hello 줄 확인 **httpsport =** hello 포트 1270을 정의 합니다. 예: `httpsport=1270`
3. Hello OMI 서버를 다시 시작 합니다.`sudo /opt/omi/bin/service_control restart`

## <a name="agent-logs"></a>에이전트 로그
hello Linux 용 OMS 에이전트에서 찾을 수 있습니다에 대 한 로그를 hello: `/var/opt/microsoft/omsagent/<workspace id>/log/` hello omsconfig (에이전트 구성) 프로그램에서 확인할 수 있습니다에 대 한 로그를 hello: `/var/opt/microsoft/omsconfig/log/` hello OMI 및 SCX 구성 요소 (성능 메트릭 데이터 제공)에 대 한 로그에서 찾을 수 있습니다.`/var/opt/omi/log/ and /var/opt/microsoft/scx/log`

### <a name="log-rotation-configuration"></a>로그 순환 구성##
omsagent에 대 한 hello 로그 회전 구성에서 찾을 수 있습니다.`/etc/logrotate.d/omsagent-<workspace id>`

hello 기본 설정은 다음과 같습니다. 
```
/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log {
    rotate 5
    missingok
    notifempty
    compress
    size 50k
    copytruncate
}
```

## <a name="uninstalling-hello-oms-agent-for-linux"></a>Linux 용 OMS 에이전트 제거 hello
hello 에이전트 패키지는 제거할 수 hello로 실행 중인 hello 번들.sh 파일 `--purge` hello 에이전트와 해당 구성의 hello 컴퓨터에서 완전히 제거 하는 인수입니다.   

```
> sudo rpm -e omsconfig
> sudo rpm -e omsagent
> sudo /opt/microsoft/scx/bin/uninstall
```

## <a name="troubleshooting"></a>문제 해결

### <a name="issue-unable-tooconnect-through-proxy-toooms"></a>프록시 tooOMS 통해 없습니다 tooconnect 문제:

#### <a name="probable-causes"></a>가능한 원인
* 온 보 딩 하는 동안 지정 된 hello 프록시 잘못 되었습니다.
* 사용할 수 없는 데이터 센터에서 whitelistested hello OMS 서비스 끝점 

#### <a name="resolutions"></a>해결 방법
1. 다음 명령을 hello 옵션을 사용 하는 hello를 사용 하 여 hello Linux 용 OMS 에이전트와 OMS 서비스 Reonboard toohello `-v` 사용 하도록 설정 합니다. 이렇게 하면 hello 프록시 toohello OMS 서비스를 통해 연결 하는 hello 에이전트의 자세한 정보를 출력 합니다. 
`/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`

2. Hello 섹션을 검토 [구성 hello에 사용할 에이전트를 HTTP 프록시 server(#configuring the-agent-for-use-with-a-http-proxy-server) tooverify 제대로 구성한 프록시 서버를 통해 에이전트 toocommunicate hello 합니다.    
* OMS 서비스 끝점 다음 hello 다시 확인은 허용 목록.

    |에이전트 리소스| 포트 |  
    |------|---------|  
    |*.ods.opinsights.azure.com | 포트 443|   
    |*.oms.opinsights.azure.com | 포트 443|   
    |ods.systemcenteradvisor.com | 포트 443|   
    |*.blob.core.windows.net/ | 포트 443|   

### <a name="issue-you-receive-a-403-error-when-trying-tooonboard"></a>문제: tooonboard 동안 403 오류 수신

#### <a name="probable-causes"></a>가능한 원인
* Linux 서버의 날짜 및 시간이 올바르지 않습니다 
* 사용된 작업 영역 ID 및 작업 영역 키가 올바르지 않습니다.

#### <a name="resolution"></a>해결 방법

1. Hello 시 Linux 서버 hello 명령 날짜를 확인 합니다. Hello 시간이 현재 시간 으로부터 15 분 + /-경우에 온 보 딩 실패 합니다. toocorrect이 업데이트 hello 날짜 및/또는 Linux 서버에의 표준 시간대입니다. 
2. Linux 용 hello 최신 버전의 hello OMS 에이전트를 설치 했는지 확인 합니다.  최신 버전 hello 이제 알려 줍니다 시간차 hello 온 보 딩 오류로 인해 발생 한 경우.
3. 올바른 작업 영역 ID와이 항목의 앞부분에 나오는 hello 설치 지침에 따라 작업 영역 키를 사용 하 여 Reonboard 합니다.

### <a name="issue-you-see-a-500-and-404-error-in-hello-log-file-right-after-onboarding"></a>온 보 딩 직후 hello 로그 파일에서 500 및 404 오류를 참조 문제:
이 문제는 알려진 문제이며 Linux 데이터를 OMS 작업 영역으로 처음 업로드할 때 발생합니다. 이 문제는 전송되는 데이터 또는 서비스 환경에 영향을 미치지 않습니다.

### <a name="issue--you-are-not-seeing-any-data-in-hello-oms-portal"></a>문제:이 표시 되지 않는 hello OMS 포털에서 모든 데이터

#### <a name="probable-causes"></a>가능한 원인

- 온 보 딩 toohello OMS 서비스 하지 못했습니다.
- OMS 서비스에서 차단 되는 연결 toohello
- Linux용 OMS 에이전트가 백업되었습니다.

#### <a name="resolutions"></a>해결 방법
1. 온 보 딩 hello OMS 서비스로 hello 다음 파일이 있는 경우를 확인 하 여 성공 했는지 여부를 확인 합니다.`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`
2. Hello를 사용 하 여 Reonboard `omsadmin.sh` 명령줄 지침
3. 프록시를 사용 하는 경우 이전에 제공 된 toohello 프록시 해결 단계를 참조 하십시오.
4. 경우에 따라 Linux 용 OMS 에이전트 hello hello OMS 서비스와 통신할 수 없는 경우 hello 에이전트 데이터가 큐에 대기 중인된 toohello 가득 찬 버퍼 크기는 50MB입니다. hello 다음 명령을 실행 하 여 hello Linux 용 OMS 에이전트를 다시 시작 해야: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`합니다. 

    >[!NOTE]
    >이 문제는 에이전트 버전 1.1.0-28 및 이상에서 해결되었습니다.
> 