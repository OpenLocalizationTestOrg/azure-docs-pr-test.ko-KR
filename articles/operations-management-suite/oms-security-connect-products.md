---
title: "aaaConnecting 보안 제품 toohello Operations Management Suite (OMS) 보안 및 감사 솔루션 | Microsoft Docs"
description: "이 문서는 관리 도구 모음 보안 및 감사 솔루션 일반적인 이벤트 형식을 사용 하 여 보안 제품 tooOperations tooconnect 있습니다를 수 있습니다."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 46eee484-e078-4bad-8c89-c88a3508f6aa
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 0f4b372d0379987c4e249628a3c8d52733be65c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-your-security-products-toohello-operations-management-suite-oms-security-and-audit-solution"></a>보안 제품 toohello Operations Management Suite (OMS) 보안 및 감사 솔루션에 연결 
이 문서를 사용 하면 보안 제품 hello OMS 보안 및 감사 솔루션에 연결할 수 있습니다. 원본 hello 지원 됩니다.

- CEF(일반 이벤트 형식) 이벤트
- Cisco ASA 이벤트


## <a name="what-is-cef"></a>CEF란 무엇인가요?
공통 이벤트 형식 (CEF)는 많은 보안 공급 업체 tooallow 이벤트 간의 상호 운용성 서로 다른 플랫폼에서 사용 되는 Syslog 메시지를 기반으로 한 산업 표준 형식입니다. OMS 보안 및 감사 솔루션 OMS 보안이 포함 된 보안 제품 CEF tooconnect 있습니다를 사용 하 여 데이터 수집을 지원 합니다. 

데이터 원본 tooOMS를 연결 하 여이 플랫폼의 일부인 기능을 수행 하는 hello 수 tootake 활용 됩니다.

- 검색 및 상관 관계
- 감사
- 경고
- 위협 인텔리전스
- 주목할 만한 문제

## <a name="collection-of-security-solution-logs"></a>보안 솔루션 로그 수집

OMS 보안은 Syslogs 및 [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) 로그에 CEF를 사용하는 로그의 컬렉션을 지원합니다. 이 예제에서는 hello 소스 (hello 로그를 생성 하는 컴퓨터) ng syslog 디먼을 실행 하는 Linux 컴퓨터 이며 hello 대상이 OMS 보안. 작업을 tooprepare hello Linux 컴퓨터 tooperform hello를 수행 해야 합니다.

- 이상 버전 1.2.0-25 Linux 용 OMS 에이전트 hello를 다운로드 합니다.
- Hello 섹션에 따라 **빠른 설치 가이드** 에서 [이 여기서](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall 및 온보드 hello 에이전트 tooyour 작업 영역입니다.

일반적으로 hello 에이전트 hello hello 로그에서 생성 되는 다른 컴퓨터에 설치 됩니다. 전달 hello 로그 toohello 에이전트 컴퓨터는 단계를 수행 하는 hello를 일반적으로 필요 합니다.

- 제품/컴퓨터 tooforward hello 필요한 이벤트 toohello syslog 디먼 (예: rsyslog 또는 syslog-ng) 로깅 hello hello 에이전트 컴퓨터에서 구성 합니다.
- 원격 시스템에서 hello 에이전트 컴퓨터 tooreceive 메시지에 syslog 디먼 hello를 사용 하도록 설정 합니다.

Hello 에이전트 컴퓨터에서 hello 이벤트 hello syslog 디먼 toolocal UDP 포트 25226에서에서 보낸 toobe가 필요 합니다. hello 에이전트는이 포트에서 들어오는 이벤트에 대 한 수신 대기 합니다. hello 다음은 구성 (수정 가능 hello 구성 toofit 로컬 설정) 하는 hello 로컬 시스템 toohello 에이전트에서 모든 이벤트를 전송에 대 한 예입니다.

1. 터미널 창 열기 hello 및 이동 toohello 디렉터리 */etc/syslog-ng /* 
2. 새 파일을 만들 *보안-구성-omsagent.conf* hello 다음 콘텐츠를 추가 하 고: OMS_facility local4 =
    
    filter f_local4_oms { facility(local4); };

    destination security_oms { tcp("127.0.0.1" port(25226)); };

    log { source(src); filter(f_local4_oms); destination(security_oms); };
    
3. Hello 파일을 다운로드 *security_events.conf* 에 배치 하 고 */etc/opt/microsoft/omsagent/conf/omsagent.d/* hello OMS 에이전트 컴퓨터에 있습니다.
4. Toorestart hello syslog 디먼 아래 hello 명령을 입력: *syslog ng 실행에 대 한:*
    
    ```
    sudo service rsyslog restart
    ```

    *rsyslog를 실행하기 위해*
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. OMS 에이전트 toorestart hello 아래 hello 명령을 입력 합니다.

    *rsyslog-ng를 실행하기 위해*
    
    ```
    sudo service omsagent restart
    ```

    *rsyslog를 실행하기 위해*
    
    ```
    systemctl restart omsagent
    ```
6. 아래 hello 명령을 입력 하 고 hello 결과 tooconfirm hello OMS 에이전트 로그에 오류가 있는지 검토 키를 누릅니다.

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a>수집된 보안 이벤트 검토

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

Hello 구성 끝난 후, OMS 보안에 의해 수집 된 toobe hello 보안 이벤트에 시작 됩니다. toovisualize hello 명령을 입력 하는 이벤트만 열기 hello 로그 검색 *유형 = CommonSecurityLog* 에 검색 필드 hello 하 고 ENTER 키를 누릅니다. hello 다음 예제에서는 결과 보여 줍니다 hello이 명령의이 경우 OMS 보안 이미 수집 된 여러 공급 업체에서 보안 로그를 확인 합니다.
   
![OMS 보안 및 감사 기준 평가](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

단일 공급 업체, 예를 들어 온라인 Cisco 로그 toovisualize, 형식에 대 한이 검색을 구체화할 수 있습니다: *형식 CommonSecurityLog DeviceVendor = Cisco =*합니다. "CommonSecurityLog" hello에 미리 정의 된 필드에 다른 확장 하는 동안 hello 기본 extensios 여부 등 "사용자 지정 확장 프로그램" or not CEF 헤더 "AdditionalExtensions" 필드에 삽입 됩니다. 여기에서 hello 기능 tooget 전용 필드를 사용자 지정 필드를 사용할 수 있습니다. 

### <a name="accessing-computers-missing-baseline-assessment"></a>기준 평가가 누락된 컴퓨터에 액세스
OMS는 tooWindows Server 2012 r 2를 Windows Server 2008 r 2에서 hello 도메인 구성원 기본 프로필을 지원합니다. Windows Server 2016 기준은 계획은 아직 최종본이 아니며 게시되는 즉시 추가됩니다. OMS 보안 및 감사 초기 평가 통해 검색 된 다른 모든 운영 체제 hello 아래에 표시 **초기 평가 누락 된 컴퓨터** 섹션.

## <a name="see-also"></a>참고 항목
이 문서에서는 방법에 대해 배웠습니다 tooconnect CEF 솔루션 tooOMS 합니다. OMS 보안에 대해 자세히 toolearn hello 다음 문서 참조:

* [OMS(Operations Management Suite) 개요](operations-management-suite-overview.md)
* [모니터링 및 Operations Management Suite 보안 및 감사 솔루션에 응답 중 tooSecurity 경고](oms-security-responding-alerts.md)
* [Operations Management Suite 보안 및 감사 솔루션의 리소스 모니터링](oms-security-monitoring-resources.md)

