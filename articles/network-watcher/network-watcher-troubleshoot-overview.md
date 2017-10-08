---
title: "Azure 네트워크 감시자의 연결 문제 해결 aaaIntroduction tooresource | Microsoft Docs"
description: "이 페이지 hello 네트워크 감시자 리소스 문제 해결 기능에 대 한 개요를 제공합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: c1145cd6-d1cf-4770-b1cc-eaf0464cc315
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: ccbe4c1c2364473aba06e709460d67c773cf25ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooresource-troubleshooting-in-azure-network-watcher"></a>Azure 네트워크 감시자의 연결 문제 해결 소개 tooresource

Virtual Network 게이트웨이는 온-프레미스 리소스 및 Azure 내 다른 가상 네트워크 간의 연결을 제공합니다. 이러한 게이트웨이 및 해당 연결을 모니터링 하는 것은 중요 한 tooensuring 통신 손상 되지 않았습니다. 네트워크 감시자 제공 hello 기능 tootroubleshoot 가상 네트워크 게이트웨이 및 연결 합니다. 이 hello 포털, PowerShell, CLI 또는 REST API를 통해 호출할 수 있습니다. 호출 되 면 네트워크 감시자 hello 가상 네트워크 게이트웨이 또는 연결 및 반환 hello 적절 한 결과의 hello 상태를 진단 합니다. 이 요청이 장기 실행 트랜잭션으로 인 hello 진단 완료 되 면 hello 결과가 반환 됩니다.

![portal][2]

## <a name="results"></a>결과

반환 된 hello 예비 결과 hello 리소스의 hello 상태의 전반적인을 제공 합니다. Hello 섹션 다음에 표시 된 대로 리소스에 대 한 심층 정보를 제공:

hello 다음 목록은 API를 해결 하는 hello로 반환 하는 hello 값입니다.

* **startTime** -이 값은 hello 시간이 hello 해결 API 호출을 시작 합니다.
* **endTime** -이 값은 hello 시간이 hello 문제 해결이 종료 되었습니다.
* **code** - 이 값은 단일 진단 오류가 발생할 경우 이 값은 UnHealthy입니다.
* **결과** -결과 hello 연결 또는 hello 가상 네트워크 게이트웨이 반환 된 결과의 컬렉션입니다.
    * **id** -이 값은 hello 오류 형식입니다.
    * **요약** -이 값은 hello 오류의 요약 합니다.
    * **자세한** -이 값은 hello 오류에 대 한 자세한 설명을 제공 합니다.
    * **recommendedActions** -이 속성은 tootake 권장 되는 작업의 컬렉션입니다.
      * **actionText** -이 값에는 어떤 작업 tootake를 설명 하는 hello 텍스트 포함 됩니다.
      * **actionUri** -이 값은 방법에 hello URI toodocumentation 제공 tooact 합니다.
      * **actionUriText** -이 값은 간단한 설명 hello 동작 텍스트입니다.

hello 테이블 hello 서로 다른 오류 형식 표시 (id가 결과 목록 앞에 오는 hello에서) 사용할 수 있는 다음을 선택 하 고 경우 hello 오류 로그를 만듭니다.

### <a name="gateway"></a>게이트웨이

| 오류 유형 | 이유 | 로그|
|---|---|---|
| NoFault | 오류가 발견되지 않은 경우를 나타냅니다. |예|
| GatewayNotFound | 게이트웨이를 찾을 수 없거나 게이트웨이가 프로비저닝되지 않았습니다. |아니요|
| PlannedMaintenance |  게이트웨이 인스턴스가 유지 관리되고 있습니다.  |아니요|
| UserDrivenUpdate | 사용자 업데이트를 진행 중인 경우를 나타냅니다. 크기 조정 작업일 수 있습니다. | 아니요 |
| VipUnResponsive | Hello hello 게이트웨이의 기본 인스턴스를 연결할 수 없습니다. 이 hello 상태 검색에 실패할 때 발생 합니다. | 아니요 |
| PlatformInActive | Hello 플랫폼에 문제가 있습니다. | 아니요|
| ServiceNotRunning | hello 기본 서비스가 실행 되지 않습니다. | 아니요|
| NoConnectionsFoundForGateway | 연결이 없는 hello 게이트웨이에 있습니다. 단지 경고일 뿐입니다.| 아니요|
| ConnectionsNotConnected | 연결이 연결되지 않습니다. 단지 경고일 뿐입니다.| 예|
| GatewayCPUUsageExceeded | hello 현재 게이트웨이 CPU 사용량은 > 95%입니다. | 예 |

### <a name="connection"></a>연결

| 오류 유형 | 이유 | 로그|
|---|---|---|
| NoFault | 오류가 발견되지 않은 경우를 나타냅니다. |예|
| GatewayNotFound | 게이트웨이를 찾을 수 없거나 게이트웨이가 프로비저닝되지 않았습니다. |아니요|
| PlannedMaintenance | 게이트웨이 인스턴스가 유지 관리되고 있습니다.  |아니요|
| UserDrivenUpdate | 사용자 업데이트를 진행 중인 경우를 나타냅니다. 크기 조정 작업일 수 있습니다.  | 아니요 |
| VipUnResponsive | Hello hello 게이트웨이의 기본 인스턴스를 연결할 수 없습니다. Hello 상태 검색이 실패 하면 발생 합니다. | 아니요 |
| ConnectionEntityNotFound | 연결 구성이 없습니다. | 아니요 |
| ConnectionIsMarkedDisconnected | hello 연결 "연결이 끊긴 된"으로 표시 됩니다. |아니요|
| ConnectionNotConfiguredOnGateway | hello 기본 서비스 연결을 구성 하는 hello를 않아도 됩니다. | 예 |
| ConnectionMarkedStandy | 기본 서비스가 hello 대기로 표시 되어 있습니다.| 예|
| 인증 | 미리 공유한 키가 일치하지 않습니다. | 예|
| PeerReachability | hello 피어 게이트웨이 연결할 수 없습니다. | 예|
| IkePolicyMismatch | hello 피어 게이트웨이 Azure에서 지원 되지 않는 IKE 정책에 있습니다. | 예|
| WfpParse 오류 | Hello WFP 로그 구문 분석 오류가 있습니다. |예|

## <a name="supported-gateway-types"></a>지원되는 게이트웨이 유형

hello 다음 목록은 hello 지원 표시는 게이트웨이 및 연결은 지원 네트워크 감시자 문제 해결 합니다.
|  |  |
|---------|---------|
|**게이트웨이 유형**   |         |
|VPN      | 지원됨        |
|ExpressRoute | 지원되지 않음 |
|HyperNet | 지원되지 않음|
|**VPN 유형** | |
|경로 기반 | 지원됨|
|정책 기반 | 지원되지 않음|
|**연결 유형**||
|IPSec| 지원됨|
|VNet2Vnet| 지원됨|
|ExpressRoute| 지원되지 않음|
|HyperNet| 지원되지 않음|
|VPNClient| 지원되지 않음|

## <a name="log-files"></a>로그 파일

hello 리소스 문제 해결 로그 파일은 리소스 문제 해결 완료 된 후 저장소 계정에 저장 됩니다. hello 다음 이미지 hello 예의 내용을 보여줍니다 오류가 발생 하는 호출.

![Zip 파일][1]

> [!NOTE]
> 경우에 따라 hello 로그 파일의 하위 집합만 toostorage를 기록 됩니다.

Azure 저장소 계정에서 파일을 다운로드 하는 방법은 참조 너무[.NET을 사용 하 여 Azure Blob 저장소 시작](../storage/blobs/storage-dotnet-how-to-use-blobs.md)합니다. 사용할 수 있는 다른 도구는 저장소 탐색기입니다. 저장소 탐색기에 대 한 자세한 내용은 여기에 있습니다 링크 hello: [저장소 탐색기](http://storageexplorer.com/)

### <a name="connectionstatstxt"></a>ConnectionStats.txt

hello **ConnectionStats.txt** 파일 hello 송 / 수신 바이트, 연결 상태 및 연결 하는 hello 시간 hello를 포함 하 여 연결의 전체 통계를 포함 합니다.

> [!NOTE]
> API 문제를 해결 하는 hello 호출 toohello 정상 상태를 반환 하면 hello hello zip 파일에 반환 되는는 **ConnectionStats.txt** 파일입니다.

hello이이 파일의 내용이 다음 예제와 비슷한 toohello:

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a>CPUStats.txt

hello **CPUStats.txt** CPU 사용량과 메모리가 테스트 hello 시점에서 사용 가능한 파일에 포함 되어 있습니다.  이 파일의 내용을 hello은 다음 예제와 비슷한 toohello입니다.

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a>IKEErrors.txt

hello **IKEErrors.txt** 파일 모니터링 하는 동안 발견 된 IKE 오류를 포함 합니다.

hello 다음 예제에서는 IKEErrors.txt 파일의 내용을 hello 오류는 hello 문제에 따라 달라질 수 있습니다.

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a>Scrubbed-wfpdiag.txt

hello **Scrubbed wfpdiag.txt** hello wfp 로그를 포함 하는 로그 파일입니다. 이 로그에는 패킷 삭제 및 IKE/AuthIP 오류에 대한 기록이 포함됩니다.

hello 다음 예제에서는 hello Scrubbed wfpdiag.txt 파일의 내용을 hello 이 예제에서는 연결의 공유 키 hello hello hello 아래에서 세 번째 줄에서 볼 수 있듯이 잘못 되었습니다. 다음 예제는 hello hello 전체 로그의 코드 조각은 방금는 hello 로그 hello 문제에 따라 시간이 오래 걸릴 수 있습니다.

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from hello high priority thread pool list
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|IKE diagnostic event:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Event Header:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Timestamp: 1601-01-01T00:00:00.000Z
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Flags: 0x00000106
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Local address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Remote address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IP version field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP version: IPv4
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP protocol: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local address: 13.78.238.92
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote address: 52.161.24.36
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Application ID:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  User SID: <invalid>
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Failure type: IKE/Authip Main Mode Failure
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Type specific info:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure error code:0x000035e9
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IKE authentication credentials are unacceptable
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure point: Remote
...
```

### <a name="wfpdiagtxtsum"></a>wfpdiag.txt.sum

hello **wfpdiag.txt.sum** hello 버퍼 및 처리 된 이벤트를 표시 하는 로그 파일이 있습니다.

hello 다음 예제는 hello 내용의 wfpdiag.txt.sum 파일.
```
Files Processed:
    C:\Resources\directory\924336c47dd045d5a246c349b8ae57f2.GatewayTenantWorker.DiagnosticsStorage\2017-02-02T17-34-23\wfpdiag.etl
Total Buffers Processed 8
Total Events  Processed 2169
Total Events  Lost      0
Total Format  Errors    0
Total Formats Unknown   486
Elapsed Time            330 sec
+-----------------------------------------------------------------------------------+
|EventCount    EventName            EventType   TMF                                 |
+-----------------------------------------------------------------------------------+
|        36    ikeext               ike_addr_utils_c844  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        12    ikeext               ike_addr_utils_c857  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        96    ikeext               ike_addr_utils_c832  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|         6    ikeext               ike_bfe_callbacks_c133  1dc2d67f-8381-6303-e314-6c1452eeb529|
|         6    ikeext               ike_bfe_callbacks_c61  1dc2d67f-8381-6303-e314-6c1452eeb529|
|        12    ikeext               ike_sa_management_c5698  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c8447  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c494  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c642  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c3162  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c3307  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
```

## <a name="next-steps"></a>다음 단계

어떻게 toodiagnose VPN 게이트웨이 및 연결을 통해 hello 포털 방문 하 여 자세한 [게이트웨이 문제 해결-Azure 포털](network-watcher-troubleshoot-manage-portal.md)합니다.
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
