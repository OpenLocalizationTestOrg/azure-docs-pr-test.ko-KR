---
title: "데이터 관리 게이트웨이 발급 aaaTroubleshoot | Microsoft Docs"
description: "팁 tootroubleshoot 문제 관련된 tooData 관리 게이트웨이 제공합니다."
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 85dacc8a1e8d574d6e7d5b556c995cebdc148fde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a>데이터 관리 게이트웨이 사용 관련 문제 해결
이 문서에서는 데이터 관리 게이트웨이 사용과 관련된 문제 해결에 대한 정보를 제공합니다.

> [!NOTE]
> Hello 참조 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) hello 게이트웨이에 대 한 자세한 정보에 대 한 문서입니다. Hello 참조 [온-프레미스와 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) hello 게이트웨이 사용 하 여 온-프레미스 SQL Server 데이터베이스 tooMicrosoft Azure Blob 저장소에서에서 데이터를 이동 하는 연습은 문서입니다.
>
>

## <a name="failed-tooinstall-or-register-gateway"></a>실패 한 tooinstall 또는 레지스터 게이트웨이
### <a name="1-problem"></a>1. 문제
설치 하 고 hello 게이트웨이 설치 파일을 다운로드 하는 동안 특히 게이트웨이 등록 하는 경우이 오류 메시지가 표시 됩니다.

`Unable tooconnect toohello remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a>원인
tooinstall hello 게이트웨이 시도 하는 hello 컴퓨터 toodownload hello 최신 게이트웨이 설치 파일 tooa 네트워크 문제로 인해 hello 다운로드 센터에서 실패 했습니다.

#### <a name="resolution"></a>해결 방법
Hello 설정이 hello 컴퓨터 toohello에서 hello 네트워크 연결을 차단 하면 방화벽 프록시 서버 설정을 toosee 확인 [다운로드 센터](https://download.microsoft.com/), hello 설정을 업데이트 하 고 적절 하 게 합니다.

Hello에서 최신 게이트웨이 hello에 대 한 hello 설치 파일을 다운로드할 수 또는 [다운로드 센터](https://www.microsoft.com/download/details.aspx?id=39717) hello 다운로드 센터에 액세스할 수 있는 다른 컴퓨터에 있습니다. 복사 hello 설치 관리자 파일 toohello 게이트웨이 컴퓨터를 호스트 하 고 수동으로 실행할 tooinstall 및 update hello 게이트웨이 할 수 있습니다.

### <a name="2-problem"></a>2. 문제
클릭 하 여 tooinstall 게이트웨이 시도 중인이 오류가 나타날 **이 컴퓨터에 직접 설치** hello Azure 포털의에서.

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a>원인
게이트웨이 hello 컴퓨터에 이미 설치 되어 있습니다.

#### <a name="resolution"></a>해결 방법
Hello hello 컴퓨터에 기존 게이트웨이 제거 하 고 hello 클릭 **이 컴퓨터에 직접 설치** 다시 연결 합니다.

### <a name="3-problem"></a>3. 문제
새 게이트웨이를 등록할 때 이 오류가 표시될 수 있습니다.

`Error: hello gateway has encountered an error during registration.`

#### <a name="cause"></a>원인
Hello 다음 이유 중 하나에 대해이 메시지가 표시 될 수 있습니다.

* hello 게이트웨이 키의 hello 형식이 올바르지 않습니다.
* hello 게이트웨이 키가 무효화 되었습니다.
* hello 포털에서 hello 게이트웨이 키 다시 생성 했습니다.  

#### <a name="resolution"></a>해결 방법
Hello 포털에서 hello 맞는 올바른 게이트웨이 키를 사용 하 고 있는지 확인 합니다. 필요한 경우 키를 생성 하 고 hello 키 tooregister hello 게이트웨이 사용 합니다.

### <a name="4-problem"></a>4. 문제
Hello 게이트웨이 등록 하는 경우 다음과 같은 오류 메시지가 표시 될 수 있습니다.

`Error: hello content or format of hello gateway key "{gatewayKey}" is invalid, please go tooazure portal toocreate one new gateway or regenerate hello gateway key.`



![키의 내용 또는 형식이 잘못됨](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a>원인
hello 콘텐츠나 hello 입력된 게이트웨이 키의 형식이 올바르지 않습니다. Hello 이유 중 하나로 hello 포털에서 hello 키의 일부만 복사 하거나 잘못 된 키를 사용할 수 있습니다.

#### <a name="resolution"></a>해결 방법
Hello 포털에서 게이트웨이 키를 생성 하 고 hello 복사 단추 toocopy hello 전체 키를 사용 합니다. 그런 다음이 창 tooregister hello 게이트웨이에 붙여넣을.

### <a name="5-problem"></a>5. 문제
Hello 게이트웨이 등록 하는 경우 다음과 같은 오류 메시지가 표시 될 수 있습니다.

`Error: hello gateway key is invalid or empty. Specify a valid gateway key from hello portal.`

![게이트웨이 키가 잘못되었거나 비어 있음](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a>원인
hello 게이트웨이 키 다시 생성 되었으면 또는 hello 게이트웨이 hello Azure 포털에서에서 삭제 되었습니다. 데이터 관리 게이트웨이 설치 hello 최신 없는 경우에 발생할 수 있습니다.

#### <a name="resolution"></a>해결 방법
Microsoft hello에서 hello 최신 버전을 찾을 수 hello 데이터 관리 게이트웨이 설치 hello 최신 버전 인지 확인 [다운로드 센터](https://go.microsoft.com/fwlink/p/?LinkId=271260)합니다.

설치가 현재 / 최신 게이트웨이가 포털에 여전히 존재 하는 경우 hello Azure 포털에서에서 hello 게이트웨이 키 다시 생성 및 사용 하 여 hello 복사 단추 toocopy hello 전체 키를이 창 tooregister hello 게이트웨이에 붙여 넣습니다. 그렇지 않으면 hello 게이트웨이 다시 만들고 처음부터 다시 시작 합니다.

### <a name="6-problem"></a>6. 문제
Hello 게이트웨이 등록 하는 경우 다음과 같은 오류 메시지가 표시 될 수 있습니다.

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with hello status “Gateway key is invalid”`

![게이트웨이 키가 잘못되었거나 비어 있음](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a>원인
Hello 게이트웨이가 삭제 되었다는 또는 hello 연결 된 게이트웨이 키 다시 생성 되었으면 때문에이 오류가 발생할 수 있습니다.

#### <a name="resolution"></a>해결 방법
Hello 게이트웨이 삭제 하는 경우 hello 포털에서 hello 게이트웨이 다시 만들기를 클릭 **등록**hello 포털에서 hello 키를 복사를 붙여 넣고 tooregister hello 게이트웨이 시도 하십시오.

Hello 게이트웨이 여전히 존재 하는 경우 해당 키 다시 생성 되었으면 hello 새로운 키 tooregister hello 게이트웨이 사용 합니다. Hello 키가 없는 경우에 hello 포털에서 다시 hello 키 다시 생성 합니다.

### <a name="7-problem"></a>7. 문제
게이트웨이 등록 하는 경우 인증서에 대 한 tooenter 경로 암호를 할 수 있습니다.

![인증서 지정](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a>원인
hello 게이트웨이 하기 전에 다른 컴퓨터에 등록 되었습니다. 게이트웨이의 hello 초기 등록 하는 동안 암호화 인증서 hello 게이트웨이와 관련 된 합니다. hello 인증서 hello 게이트웨이 의해 생성 된 자체 또는 hello 사용자가 제공한 수 있습니다.  이 인증서는 hello 데이터 저장소 (연결 된 서비스)의 사용 되는 tooencrypt 자격 증명.  

![인증서 내보내기](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

때이 인증서를 사용 하 여 암호화 복원 다른 호스트 컴퓨터에서 게이트웨이 hello hello 등록 마법사 인증서 toodecrypt이 이전에 자격 증명에 대 한 합니다.  이 인증서가 없으면 새 게이트웨이 hello로 hello 자격 증명을 해독할 수 및이 새 게이트웨이에 연결 된 후속 복사 활동 실행이 실패 합니다.  

#### <a name="resolution"></a>해결 방법
Hello를 사용 하 여 hello 자격 증명 인증서 hello 원래 게이트웨이 컴퓨터에서 내보낸 경우 **내보내기** hello 단추 **설정** hello를 사용 하 여, 데이터 관리 게이트웨이 구성 관리자에서 탭 여기에 해당 인증서입니다.

게이트웨이를 복구할 때 이 단계를 건너뛸 수 없습니다. Hello 인증서가 없으면 hello 포털에서 toodelete hello 게이트웨이가 필요 하 고 다시 새 게이트웨이 만듭니다.  또한 모든 연결 된 서비스 자격 증명을 다시 입력 하 여 관련된 toohello 게이트웨이 업데이트 합니다.

### <a name="8-problem"></a>8. 문제
Hello 다음과 같은 오류 메시지가 표시 될 수 있습니다.

`Error: hello remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a>원인
이 오류는 인터넷 리소스에는 HTTP 프록시 tooaccess 해야 하는 환경에 게이트웨이가 있으면 발생 또는 사용자 프록시 인증 암호 변경 되지만 적절 하 게 업데이트 되지 않습니다 게이트웨이에 있습니다.

#### <a name="resolution"></a>해결 방법
Hello에 hello 지침에 따라 [프록시 서버 고려 사항](#proxy-server-considerations) 의이 섹션을 검토 한 데이터 관리 게이트웨이 구성 관리자와 프록시 설정을 구성 합니다.

## <a name="gateway-is-online-with-limited-functionality"></a>게이트웨이는 기능이 제한된 온라인입니다.
### <a name="1-problem"></a>1. 문제
제한 된 기능이 있는 hello 게이트웨이의 hello 상태가 온라인으로 표시 합니다.

#### <a name="cause"></a>원인
Hello 다음 이유 중 하나에 대 한 제한 된 기능이 있는 hello 게이트웨이의 hello 상태를 온라인으로 참조 합니다.

* 게이트웨이 Azure 서비스 버스를 통해 toocloud 서비스를 연결할 수 없습니다.
* 클라우드 서비스는 서비스 버스를 통해 toogateway를 연결할 수 없습니다.

Hello 게이트웨이 기능이 제한 온라인 상태 이면 수 toouse hello 데이터 팩터리 복사 마법사 toocreate 데이터 파이프라인에서 온-프레미스 데이터 저장소 데이터 tooor 복사 하기 위한 아닐 수 있습니다. 이 문제를 해결 hello 포털, Visual Studio 또는 Azure PowerShell에서에서 데이터 팩터리 편집기를 사용할 수 있습니다.

#### <a name="resolution"></a>해결 방법
이 문제에 대 한 확인 (제한 된 기능으로 온라인) hello 게이트웨이 수 없습니다 toohello 클라우드 서비스를 연결 하거나 다른 방법으로 hello 함에 따라 됩니다. 다음 섹션 hello 이러한 해결 방법을 제공 합니다.

### <a name="2-problem"></a>2. 문제
Hello 다음 오류가 표시 됩니다.

`Error: Gateway cannot connect toocloud service through service bus`

![게이트웨이는 toocloud 서비스에 연결할 수 없습니다.](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a>원인
게이트웨이는 서비스 버스를 통해 toohello 클라우드 서비스를 연결할 수 없습니다.

#### <a name="resolution"></a>해결 방법
이러한 단계 tooget hello 게이트웨이 다시 온라인를 수행 합니다.

1. Hello 게이트웨이 컴퓨터와 회사 방화벽 hello에 대 한 아웃 바운드 규칙 IP 주소를 허용 합니다. Hello Windows 이벤트 로그에서에서 IP 주소를 찾을 수 있습니다 (ID 401 = =): 시도 된 tooaccess 소켓 XX 액세스 권한에 의해 방식으로 수행 합니다. XX 합니다. XX 합니다. XX:9350 합니다.
* Hello 게이트웨이 프록시 설정을 구성 합니다. Hello 참조 [프록시 서버 고려 사항](#proxy-server-considerations) 자세한 내용은 섹션.
* 아웃 바운드 포트 5671 및 9350에서 9354 hello 게이트웨이 컴퓨터와 회사 방화벽 hello 두 hello Windows 방화벽에서 사용 하도록 설정 합니다. Hello 참조 [포트 및 방화벽](#ports-and-firewall) 자세한 내용은 섹션. 이 단계는 선택 사항이지만 성능을 고려하여 권장됩니다.

### <a name="3-problem"></a>3. 문제
Hello 다음 오류가 표시 됩니다.

`Error: Cloud service cannot connect toogateway through service bus.`

#### <a name="cause"></a>원인
네트워크 연결에서 일시적인 오류가 발생했습니다.

#### <a name="resolution"></a>해결 방법
이러한 단계 tooget hello 게이트웨이 다시 온라인를 수행 합니다.

1. 몇 분 정도 기다린, hello 오류가 삭제 되 면 hello 연결이 자동으로 복구 됩니다.
* Hello 오류가 계속 되 면 hello 게이트웨이 서비스를 다시 시작 합니다.

## <a name="failed-tooauthor-linked-service"></a>실패 한 tooauthor 연결 된 서비스
### <a name="problem"></a>문제
새 연결 된 서비스에 대 한 hello 포털 tooinput 자격 증명에 자격 증명 관리자 toouse를 시도 하거나 기존 연결 된 서비스에 대 한 자격 증명을 업데이트 하는 경우이 오류가 발생할 수 있습니다.

`Error: hello data store '<Server>/<Database>' cannot be reached. Check connection settings for hello data source.`

이 오류가 표시 되 면 hello 설정 페이지의 데이터 관리 게이트웨이 구성 관리자 스크린 샷 다음 hello 같을 수 있습니다.

![데이터베이스에 연결할 수 없음](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a>원인
hello SSL 인증서 hello 게이트웨이 컴퓨터에서 손실 될 수 있습니다. hello 게이트웨이 컴퓨터 hello 인증서 현재 SSL 암호화에 사용 되는 로드할 수 없습니다. 메시지의 뒤에 유사한 toohello는 hello 이벤트 로그에 오류 메시지가 참고할 수 있습니다.

 `Unable tooget hello gateway settings from cloud service. Check hello gateway key and hello network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a>해결 방법
이러한 단계 toosolve hello 문제를 수행 합니다.

1. 데이터 관리 게이트웨이 구성 관리자를 시작합니다.
2. Toohello 전환 **설정을** 탭 합니다.  
3. Hello 클릭 **변경** 단추 toochange hello SSL 인증서입니다.

   ![인증서 변경 단추](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. Hello SSL 인증서로 새 인증서를 선택 합니다. 사용자 또는 다른 조직에서 만든 SSL 인증서를 사용할 수 있습니다.

   ![인증서 지정](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a>복사 작업 실패
### <a name="problem"></a>문제
Hello hello 포털에서 파이프라인을 설정한 후 "UserErrorFailedToConnectToSqlserver" 실패 이후에 나타날 수 있습니다.

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect tooSQL Server`

#### <a name="cause"></a>원인
이 오류는 여러 가지 이유로 발생할 수 있으며 그에 따라 완화하는 방법이 달라집니다.

#### <a name="resolution"></a>해결 방법
Tooan SQL 데이터베이스를 연결 하기 전에 hello 데이터 관리 게이트웨이 클라이언트 쪽에 TCP/1433 포트를 통해 아웃 바운드 TCP 연결을 허용 합니다.

Azure SQL 데이터베이스 hello 대상 데이터베이스의 경우 SQL Server 방화벽 설정을 확인 Azure에 대 한도입니다.

Hello 섹션 tootest hello 연결 toohello 온-프레미스 데이터 저장소를 다음을 참조 하십시오.

## <a name="data-store-connection-or-driver-related-errors"></a>데이터 저장소 연결 또는 드라이버 관련 오류
데이터 저장소 연결이 나 드라이버 관련 오류가 표시 되 면 hello 다음 단계를 완료 합니다.

1. Hello 게이트웨이 컴퓨터에서 데이터 관리 게이트웨이 구성 관리자를 시작 합니다.
2. Toohello 전환 **진단** 탭 합니다.
3. **연결 테스트**, hello 게이트웨이 그룹 값을 추가 합니다.
4. 클릭 **테스트** toosee toohello 연결할 수 있는 경우 온-프레미스 hello 게이트웨이 컴퓨터에서 데이터 원본 hello 연결 정보와 자격 증명을 사용 하 여 합니다. 연결 테스트 hello 계속 실패 하면 드라이버를 설치한 후 다시 시작 hello 게이트웨이 대 한 toopick hello 최신 변경 합니다.

![진단 탭의 연결 테스트](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a>게이트웨이 로그
### <a name="send-gateway-logs-toomicrosoft"></a>게이트웨이 로그 tooMicrosoft 보내기
게이트웨이 문제 해결 tooget 도움말 Microsoft 지원에 문의할 경우 메시지가 나타날 수 있습니다 tooshare 게이트웨이 로그 합니다. Hello 게이트웨이의 hello 릴리스로 두 단추 클릭에 데이터 관리 게이트웨이 구성 관리자를 사용 하 여 필요한 게이트웨이 로그를 공유할 수 있습니다.    

1. Toohello 전환 **진단** 탭에서 데이터 관리 게이트웨이 구성 관리자.

    ![데이터 관리 게이트웨이 - 진단 탭](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. 클릭 **로그 보내기** toosee hello 대화 상자를 수행 합니다.

    ![데이터 관리 게이트웨이 - 로그 보내기](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. (선택 사항) 클릭 **로그를 볼** tooreview hello 이벤트 뷰어에 기록 합니다.
4. (선택 사항) 클릭 **개인 정보 보호** tooreview Microsoft 웹 서비스 개인정보취급방침 합니다.
5. 만족 스 러 우면 tooupload에 대 한는, 클릭 **로그 보내기** tooactually 문제 해결을 위한 마지막 7 일 tooMicrosoft hello에서에서 hello 로그를 보내는 합니다. 다음 스크린 샷에서 hello와 같이 hello 로그 보내기 작업의 상태를 hello 나타납니다.

    ![데이터 관리 게이트웨이 - 로그 보내기 상태](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. Hello 작업이 완료 되 면 hello 스크린 샷 뒤에 표시 된 대로 대화 상자가 표시 됩니다.

    ![데이터 관리 게이트웨이 - 로그 보내기 상태](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. Hello 저장 **보고서 ID** Microsoft 기술 지원 서비스와 공유 합니다. hello 보고서 ID가 사용 되는 toolocate hello 게이트웨이 로그 문제 해결을 위해 업로드 합니다.  hello 보고서 ID hello 이벤트 뷰어에서 저장 됩니다.  Hello 이벤트 ID "25", 확인 하 여 찾을 수 있으며 hello 날짜 및 시간을 확인 하십시오.

    ![데이터 관리 게이트웨이 - 로그 보내기 보고서 ID](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a>게이트웨이 호스트 컴퓨터에 게이트웨이 로그 보관
게이트웨이에 문제가 있고 게이트웨이 로그를 직접 공유할 수 없는 일부 시나리오가 있습니다.

* 수동으로 hello 게이트웨이 설치 하 고 hello 게이트웨이 등록 합니다.
* 데이터 관리 게이트웨이 구성 관리자에서 다시 생성 된 키가 있는 tooregister hello 게이트웨이 시도 합니다.
* Toosend 로그를 시도 하 고 hello 게이트웨이 호스트 서비스에 연결할 수 없습니다.

이러한 시나리오에서는 게이트웨이 로그를 zip 파일로 저장하고 나중에 Microsoft 지원에 문의할 때 공유할 수 있습니다. 예를 들어 hello 게이트웨이 등록 하는 동안 오류가 발생 하는 경우 hello 스크린 샷 뒤에 표시 합니다.   

![데이터 관리 게이트웨이 - 등록 오류](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

Hello 클릭 **게이트웨이 로그를 보관** tooarchive 연결 하 고 로그를 저장 한 다음 Microsoft 기술 지원 서비스 hello zip 파일을 공유 합니다.

![데이터 관리 게이트웨이 - 로그 보관](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a>게이트웨이 로그 찾기
Hello Windows 이벤트 로그에서 자세한 게이트웨이 로그 정보를 찾을 수 있습니다.

1. Windows **이벤트 뷰어**를 시작합니다.
2. Hello에서 로그를 찾을 **응용 프로그램 및 서비스 로그** > **데이터 관리 게이트웨이** 폴더입니다.

 사용자 게이트웨이 관련 문제를 해결 하는 때에 hello 이벤트 뷰어에서 오류 수준 이벤트를 확인 합니다.

![데이터 관리 게이트웨이 - 이벤트 뷰어의 로그](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
