---
title: "aaaOn 온-프레미스 데이터 게이트웨이 | Microsoft Docs"
description: "온-프레미스 게이트웨이 Azure에서 Analysis Services 서버는 tooon 온-프레미스 데이터 원본에 연결할 경우에 필요 합니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: cd596155-b608-4a34-935e-e45c95d884a9
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: fc7b9c69e6f81b41deb7a5d6d963225593845d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-tooon-premises-data-sources-with-azure-on-premises-data-gateway"></a>Azure 온-프레미스 데이터 게이트웨이 사용 하 여 tooon 온-프레미스 데이터 원본 연결
hello 온-프레미스 데이터 게이트웨이 온-프레미스 데이터 원본 및 hello 클라우드에서 Azure Analysis Services 서버 간에 안전한 데이터 전송을 제공 하는 브리지 역할을 합니다. 또한 tooworking hello에 여러 Azure Analysis Services 서버와 동일한 지역, 최신 버전의 hello 게이트웨이 hello Azure 논리 앱, Power BI, 전원 응용 프로그램, Microsoft Flow와 에서도 작동합니다. Hello에 여러 서비스에 연결할 수 있습니다 단일 게이트웨이 사용 하 여 동일한 영역입니다. 

 Azure Analysis Services를 사용 하려면 hello에 게이트웨이 리소스가 동일한 지역입니다. 예를 들어 Azure Analysis Services 서버 hello 2 미국 동부 지역에 있으면 게이트웨이 리소스가 hello 미국 동부 2 지역에 필요 합니다. 미국 동부 2에서에서 여러 서버 hello를 사용 하 여 동일한 게이트웨이에 합니다.

Hello 게이트웨이 hello 사용 하 여 설치를 처음으로 가져오기는 네 부분으로 이루어진 프로세스입니다.

- **설치 프로그램 다운로드 및 실행** - 이 단계는 조직의 컴퓨터에 게이트웨이 서비스를 설치합니다.

- **게이트웨이 등록** -이 단계는 이름 지정 및 복구, 게이트웨이 키 hello 게이트웨이 클라우드 서비스에 게이트웨이 등록 하는 지역을 선택 합니다.

- **Azure에서 게이트웨이 리소스 만들기** - 이 단계에서는 Azure 구독에서 게이트웨이 리소스를 만듭니다.

- **서버 tooyour 게이트웨이 리소스를 연결** -게이트웨이 리소스를 구독에 있으면 서버 tooit 연결을 시작할 수 있습니다.

구독에 대해 구성 된 게이트웨이 리소스를 만든 후에 다른 서비스 tooit 및 여러 서버를 연결할 수 있습니다. 만 tooinstall 다른 게이트웨이 필요 하 고 서버 또는 다른 서비스를 다른 지역에 있는 경우 추가 게이트웨이 리소스를 만듭니다.

지금 바로 시작 tooget 참조 [설치 하 고 온-프레미스 데이터 게이트웨이 구성](analysis-services-gateway-install.md)합니다.

## <a name="how-it-works"> </a>작동 방법
조직에서 컴퓨터에 설치 하는 hello 게이트웨이 Windows 서비스로 실행 **온-프레미스 데이터 게이트웨이**합니다. 이 로컬 서비스는 hello Azure 서비스 버스를 통해 게이트웨이 클라우드 서비스에 등록 됩니다. 그런 다음 Azure 구독에 대한 게이트웨이 리소스 게이트웨이 클라우드 서비스를 만듭니다. Azure Analysis Services 서버는 다음 tooyour 게이트웨이 리소스를 연결 합니다. 때 서버 필요 tooconnect tooyour 프로그램에 대 한 모델 온-프레미스 데이터 원본 쿼리 또는 처리를 위해, 로컬 온-프레미스 데이터 게이트웨이 서비스 및 데이터 원본 쿼리 및 데이터 흐름 트래버스하여 hello 게이트웨이 리소스에 Azure 서비스 버스 hello 합니다. 

![작동 방법](./media/analysis-services-gateway/aas-gateway-how-it-works.png)

쿼리 및 데이터 흐름:

1. 쿼리는 hello 온-프레미스 데이터 원본에 대 한 hello 암호화 된 자격 증명으로 hello 클라우드 서비스에 의해 생성 됩니다. 그런 다음 게이트웨이 tooprocess hello에 대 한 큐를 tooa 보냈습니다.
2. hello 게이트웨이 클라우드 서비스 hello 쿼리를 분석 하 고 hello 요청 toohello 푸시 [Azure 서비스 버스](https://azure.microsoft.com/documentation/services/service-bus/)합니다.
3. hello 온-프레미스 데이터 게이트웨이 보류 중인 요청 hello에 대 한 Azure 서비스 버스를 폴링합니다.
4. hello 쿼리 가져오고 hello 자격 증명의 암호를 해독 toohello 데이터 원본 자격 증명으로 연결 하는 hello 게이트웨이 합니다.
5. hello 게이트웨이 hello 쿼리 toohello 실행할 데이터 소스에 보냅니다.
6. 뒤로 toohello 게이트웨이 hello 데이터 원본의 그리고 hello 클라우드 서비스와 서버 hello 결과 전송 됩니다.

## <a name="windows-service-account"> </a>Windows 서비스 계정
hello 온-프레미스 데이터 게이트웨이 구성 된 toouse *NT SERVICE\PBIEgwService* hello Windows 서비스 로그온 자격 증명에 대 한 합니다. 기본적으로 서비스로; hello 로그온의 오른쪽에 hello의 컨텍스트에서 hello 게이트웨이 설치 하는 hello 컴퓨터입니다. 이 자격 증명은 동일한 계정 사용 tooconnect tooon 온-프레미스 데이터 원본 또는 Azure 계정에 하지 안녕 됩니다.  

인해 프록시 서버와 함께 문제가 발생 한 경우 tooauthentication, 좋습니다 toochange hello Windows 서비스 계정 tooa 도메인 사용자 또는 관리 되는 서비스 계정.

## <a name="ports"> </a>포트
hello 게이트웨이 아웃 바운드 연결 tooAzure 서비스 버스를 만듭니다. 아웃바운드 포트 TCP 443(기본값), 5671, 5672, 9350-9354에서 통신합니다.  hello 게이트웨이 인바운드 포트가 필요 하지 않습니다.

방화벽의 프로그램 데이터 영역에 대 한 hello IP 주소를 화이트 리스트 좋습니다. Hello를 다운로드할 수 있습니다 [Microsoft Azure 데이터 센터 IP 목록](https://www.microsoft.com/download/details.aspx?id=41653)합니다. 이 목록은 매주 업데이트됩니다.

> [!NOTE]
> hello Azure 데이터 센터 IP 목록에 나열 된 hello IP 주소는 CIDR 표기법 형식입니다. 예를 들어, 10.0.0.0/24는 10.0.0.0-10.0.0.24를 의미하지 않습니다. Hello에 대 한 자세한 [CIDR 표기법](http://whatismyipaddress.com/cidr)합니다.
>
>

hello 다음은 hello 게이트웨이에서 사용 되는 hello 정규화 된 도메인 이름입니다.

| 도메인 이름 | 아웃바운드 포트 | 설명 |
| --- | --- | --- |
| *.powerbi.com |80 |HTTP은 toodownload hello 설치 관리자를 사용 합니다. |
| *.powerbi.com |443 |HTTPS |
| *.analysis.windows.net |443 |HTTPS |
| *.login.windows.net |443 |HTTPS |
| *.servicebus.windows.net |5671-5672 |AMQP(고급 메시지 큐 프로토콜) |
| *.servicebus.windows.net |443, 9350-9354 |TCP의 서비스 버스 릴레이에 대한 수신기(액세스 제어 토큰 획득에 443 필요) |
| *.frontend.clouddatahub.net |443 |HTTPS |
| *.core.windows.net |443 |HTTPS |
| login.microsoftonline.com |443 |HTTPS |
| *.msftncsi.com |443 |Hello 게이트웨이 hello Power BI 서비스에서 연결할 수 없는 경우 tootest 인터넷 연결을 사용 합니다. |
| *.microsoftonline-p.com |443 |구성에 따라 인증에 사용합니다. |

### <a name="force-https"></a>Azure Service Bus와의 HTTPS 통신 강제 적용
직접 TCP; 대신 HTTPS를 사용 하 여 Azure 서비스 버스 게이트웨이 toocommunicate hello를 강제할 수 있습니다. 그러나 이렇게 하면 지금 크게 줄일 수 있습니다 성능입니다. Hello를 수정할 수 있습니다 *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* hello 값을 변경 하 여 파일 `AutoDetect` 너무`Https`합니다. 이 파일은 기본적으로 *C:\Program Files\On-premises data gateway*에 위치합니다.

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```

## <a name="faq"></a>질문과 대답

### <a name="general"></a>일반

**Q:**: Azure SQL 데이터베이스 같은 hello 클라우드에서의 데이터 원본에는 게이트웨이 필요 한가요? <br/>
**A**: 아니요. 게이트웨이는 tooon 온-프레미스 데이터 원본만 연결합니다.

**Q:**: hello 게이트웨이 toobe hello hello 데이터 원본으로 동일한 컴퓨터에 설치 되어 있습니까? <br/>
**A**: 아니요. hello 게이트웨이 제공 된 hello 연결 정보를 사용 하 여 toohello 데이터 소스를 연결 합니다. 이런이 의미에서 클라이언트 응용 프로그램으로 hello 게이트웨이 것이 좋습니다. hello 게이트웨이 하기만 hello 기능 tooconnect toohello 서버 이름을 제공 된, 일반적으로 hello에 동일한 네트워크입니다.

<a name="why-azure-work-school-account"></a>

**Q:**: 이유 toouse 작업 필요 하거나 하에서 계정 toosign 학교? <br/>
**A**: Azure 작업을 사용 하 여 또는 학교 계정을 hello 온-프레미스 데이터 게이트웨이 설치할 때만 있습니다. 로그인 계정은 Azure AD(Azure Active Directory)에서 관리하는 테넌트에 저장됩니다. 일반적으로 Azure AD 계정의 사용자 계정 이름 (UPN)는 hello 전자 메일 주소와 일치 합니다.

**Q**: 자격 증명은 어디에 저장되나요? <br/>
**A**: hello 입력 한 자격 증명이 데이터 원본에 대 한 암호화 및 hello 게이트웨이 클라우드 서비스에에서 저장 됩니다. hello 온-프레미스 데이터 게이트웨이에 hello 자격 증명의 암호가 해독 됩니다.

**Q**: 네트워크 대역폭에 대한 요구 사항이 있나요? <br/>
**A**: 네트워크 연결의 처리량이 높은 것이 좋습니다. 모든 환경은 다름와 전송 중인 데이터 양을 hello hello 결과 영향을 줍니다. ExpressRoute를 사용 하 여 온-프레미스 및 hello Azure 데이터 센터 간 처리량의 수준을 tooguarantee를 도움이 될 수 있습니다.
처리량 hello 타사 도구 Azure 속도 테스트 앱 toohelp 계기를 사용할 수 있습니다.

**Q:**: hello 게이트웨이에서 실행 중인 쿼리 tooa 데이터 원본에 대 한 hello 대기 시간 이란? Hello 최상의 아키텍처는 무엇입니까? <br/>
**A**: tooreduce 네트워크 대기 시간, 가능한 데이터 원본 닫기 toohello로 hello 게이트웨이 설치 합니다. Hello 실제 데이터 원본에 hello 게이트웨이 설치할 수 있습니다,이 근접 단어는 발생 하는 hello 대기 시간을 최소화 합니다. 너무 hello 데이터 센터를 것이 좋습니다. 예를 들어 해당 서비스는 hello 미국 서 부 데이터 센터를 사용 하는 경우 Azure VM에서 호스팅되는 SQL Server 있으면 Azure VM에에서 있어야 hello West US 너무 합니다. 이 근접 대기 시간을 최소화 하 고 hello Azure VM에서 송신 요금을 방지 합니다.

**Q:**: 보낸 결과 백 toohello 클라우드 인가요? <br/>
**A**: 결과 hello Azure 서비스 버스를 통해 전송 됩니다.

**Q:**: hello 클라우드에서 한 인바운드 연결 toohello 게이트웨이가 있습니까? <br/>
**A**: 아니요. hello 게이트웨이 아웃 바운드 연결 tooAzure 서비스 버스를 사용합니다.

**Q**: 아웃바운드 연결을 차단하면 어떻게 되나요? 수행할 작업 tooopen 필요 합니까? <br/>
**A**: hello 포트 및 호스트 게이트웨이 사용 하 여 hello를 참조 하십시오.

**Q:**: hello 실제 Windows 서비스 섞어?<br/>
**A**: 서비스에서 hello 게이트웨이 온-프레미스 데이터 게이트웨이 서비스 라고 합니다.

**Q:**: Azure Active Directory 계정으로 실행 하는 게이트웨이 Windows 서비스 hello 수 있습니까? <br/>
**A**: 아니요. hello Windows 서비스에는 유효한 Windows 계정이 있어야 합니다. 기본적으로 hello 서비스는 NT SERVICE\PBIEgwService hello 서비스 SID로 실행 됩니다.

### <a name="high-availability"></a>고가용성 및 재해 복구

**Q**: 재해 복구를 위해 어떤 옵션을 사용할 수 있나요? <br/>
**A**: hello 복구 키 toorestore 사용 하거나 게이트웨이 이동할 수 있습니다. Hello 게이트웨이 설치할 때 hello 복구 키를 지정 합니다.

**Q:**: hello 복구 키의 hello 이점은 무엇입니까? <br/>
**A**: hello 복구 키 방식으로 toomigrate 제공 하거나 재해가 발생 한 후 게이트웨이 설정을 복구 합니다.

## <a name="troubleshooting"> </a>문제 해결

**Q:**: 어떻게 하는 쿼리를 보내는 toohello 온-프레미스 데이터 원본을 볼 수 있습니까? <br/>
**A**: hello 전송 된 쿼리를 포함 하는 쿼리 추적을 설정할 수 있습니다. Toochange 쿼리 문제 해결를 수행할 때 toohello 원래 값을 추적 해야 합니다. 쿼리 추적 기능을 그대로 두면 큰 로그가 만들어집니다.

또한 추적 쿼리를 위해 데이터 원본이 포함하는 도구를 살펴볼 수도 있습니다. 예를 들어 SQL Server 및 Analysis Services의 경우 확장 이벤트 또는 SQL 프로파일러를 사용할 수 있습니다.

**Q:**: hello 게이트웨이 로그는 어디에 있습니까? <br/>
**A**: 이 항목 뒷부분에 나오는 로그를 참조하세요.

### <a name="update"></a>Toohello 최신 버전을 업데이트 합니다.

Hello 게이트웨이 버전이 오래 되 면 많은 문제가 발생할 수 있습니다. 좋은 일반 사례로 hello 최신 버전을 사용 해야 합니다. 한 달 이상 hello 게이트웨이 업데이트 하지 않은 경우 hello 최신 버전의 hello 게이트웨이 설치 하는 것이 좋습니다. 수도 있으며 hello 문제를 재현할 수 있는지를 볼 수 있습니다.

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a>오류: tooadd 사용자 toogroup을 못했습니다. (-2147463168 PBIEgwService 성능 로그 사용자)

지원 되지 않는 도메인 컨트롤러에 tooinstall hello 게이트웨이 시도 하면이 오류가 발생할 수 있습니다. 도메인 컨트롤러가 아닌 컴퓨터에 hello 게이트웨이 배포 하 고 있는지 확인 합니다.

## <a name="logs"></a>로그

로그 파일은 문제를 해결할 때 중요한 리소스입니다.

#### <a name="enterprise-gateway-service-logs"></a>엔터프라이즈 게이트웨이 서비스 로그

`C:\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\<yyyyymmdd>.<Number>.log`

#### <a name="configuration-logs"></a>구성 로그

`C:\Users\<username>\AppData\Local\Microsoft\On-premises data gateway\GatewayConfigurator.log`




#### <a name="event-logs"></a>이벤트 로그

데이터 관리 게이트웨이 및 PowerBIGateway 로그 hello를 찾을 수 있습니다 **응용 프로그램 및 서비스 로그**합니다.


## <a name="telemetry"></a>원격 분석
원격 분석은 모니터링 및 문제 해결에 사용할 수 있습니다. 기본적으로

**원격 분석 tooturn**

1.  Hello 온-프레미스 데이터 게이트웨이 클라이언트 컴퓨터의 디렉터리에 hello 확인 합니다. 일반적으로 **%systemdrive%\Program Files\On-premises data gateway**입니다. 또는 서비스 콘솔을 열고 hello 경로 tooexecutable를 확인할 수 있습니다: hello 온-프레미스 데이터 게이트웨이 서비스의 속성입니다.
2.  클라이언트 디렉터리에서 hello Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config 파일입니다. Hello SendTelemetry 설정 tootrue를 변경 합니다.
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  변경 내용을 저장 하 고 hello Windows 서비스를 다시 시작: 온-프레미스 데이터 게이트웨이 서비스입니다.




## <a name="next-steps"></a>다음 단계
* [Analysis Services 관리](analysis-services-manage.md)
* [Azure Analysis Services에서 데이터 가져오기](analysis-services-connect.md)
