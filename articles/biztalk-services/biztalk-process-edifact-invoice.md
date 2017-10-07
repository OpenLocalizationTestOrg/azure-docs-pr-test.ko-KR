---
title: "자습서: Azure BizTalk 서비스를 사용하여 EDIFACT 송장 처리 | Microsoft Docs"
description: "어떻게 toocreate hello 상자 커넥터 또는 API 앱을 구성 하 고 Azure 앱 서비스의 논리 앱에서 사용"
services: biztalk-services
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
ms.assetid: 7e0b93fa-3e2b-4a9c-89ef-abf1d3aa8fa9
ms.service: biztalk-services
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/31/2016
ms.author: deonhe
ms.openlocfilehash: 4ca021c9084b9b6540c93ef15fc3d44be0966970
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-process-edifact-invoices-using-azure-biztalk-services"></a>자습서: Azure BizTalk 서비스를 사용하여 EDIFACT 송장 처리

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

BizTalk 서비스 포털 tooconfigure hello를 사용 하 여 하 고 X12 및 EDIFACT 계약을 배포할 수 있습니다. 이 자습서에서는 어떻게 toocreate 교환에 대 한 EDIFACT 규약으로 송장 거래 파트너 간에 살펴봅니다. 이 자습서는 EDIFACT 메시지를 교환하는 두 거래 업체 Northwind와 Contoso를 포함하는 종단 간 비즈니스 솔루션에 대해 작성되었습니다.  

## <a name="sample-based-on-this-tutorial"></a>이 자습서를 기반으로 하는 샘플
이 자습서에서는 샘플을 중심으로 작성 되었습니다 **EDIFACT 송장 BizTalk를 사용 하 여 서비스를 보내는**, hello에서 사용할 수 있는 toodownload 변수인 [MSDN 코드 갤러리](http://go.microsoft.com/fwlink/?LinkId=401005)합니다. Hello 샘플을 사용 하 고 hello 샘플이 작성 된 방식을 자습서 toounderstand이를 통해 이동할 수 있습니다. 이 자습서 toocreate를 사용할 수 있습니다 또는 처음부터 고유한 솔루션입니다. 이 자습서는 hello 두 번째 접근 방식을 대상이 솔루션이 빌드된 방식을 이해할 수 있도록 합니다. 또한, 가능한 한 hello 자습서는 hello 예제와 일치 하 고 사용 하 여 hello 아티팩트 (예: 스키마, 변환) hello 샘플에 사용 된 것과 동일한 이름을 합니다.  

> [!NOTE]
> Hello 다시 사용 하므로이 솔루션에서는 EAI 브리지 tooan EDI 브리지에서 메시지를 전송, [BizTalk 서비스 브리지 체인 샘플](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104) 샘플.  
> 
> 

## <a name="what-does-hello-solution-do"></a>Hello 솔루션의 기능은 무엇입니까?
이 솔루션에서 Northwind는 Contoso에서 EDIFACT 송장을 받습니다. 이 송장은 표준 EDI 형식이 아닙니다. 따라서 hello 송장 tooNorthwind를 보내기 전에 변형 된 tooan EDIFACT 송장 (INVOIC 라고도 함) 문서로 이어야 합니다. 수신 했을 때 Northwind는 hello EDIFACT 송장을 처리 하 고 컨트롤 (CONTRL이 라고도 함) 메시지 tooContoso 반환 해야 합니다.

![][1]  

tooachieve이 비즈니스 시나리오에서는 Contoso는 Microsoft Azure BizTalk 서비스와 함께 제공 하는 hello 기능을 사용 합니다.

* Contoso는 EAI 브리지 tootransform hello 원래 송장 tooEDIFACT INVOIC를 사용합니다.
* hello EAI 브리지로 EDI hello BizTalk 서비스 포털에에서 구성 된 규약의 일부로 배포 된 브리지를 송신 하는 hello 메시지 tooan을 보냅니다.
* hello EDI 송신 브리지는 hello EDIFACT INVOIC를 처리 하 고 tooNorthwind 라우팅합니다.
* Hello 청구서를 받은 후 Northwind는 EDI 수신 브리지 hello 규약의 일부분으로 배포 된 CONTRL 메시지 toohello를 반환 합니다.  

> [!NOTE]
> 필요에 따라이 솔루션 일괄 처리로 수행 하는 대신 각 송장을 별도로 보내지 toouse toosend hello 일괄 처리 송장 방법을 또한 설명 합니다.  
> 
> 

toocomplete hello 시나리오 toosend tooNorthwind Contoso에서에서 송장을 또는 Northwind 로부터 승인을 받는 서비스 버스 큐를 사용 합니다. 다운로드로 서 사용할 수 있는 hello 샘플 패키지에 포함 되는 클라이언트 응용 프로그램을 사용 하 여 이러한 큐를 만들 수 있습니다이 자습서의 일부로 합니다.  

## <a name="prerequisites"></a>필수 조건
* 서비스 버스 네임스페이스가 있어야 합니다. 네임스페이스를 만드는 방법에 대한 지침은 [방법: 서비스 버스 서비스 네임스페이스 만들기 또는 수정](https://msdn.microsoft.com/library/azure/hh674478.aspx)을 참조하세요. **edifactbts**라는 프로비전된 서비스 버스 네임스페이스가 있다고 가정합니다.
* BizTalk 서비스 구독이 있어야 합니다. 자세한 내용은 [Azure 클래식 포털을 사용하여 BizTalk 서비스 만들기](http://go.microsoft.com/fwlink/?LinkID=302280)를 참조하세요. 이 자습서의 경우 **contosowabs**라는 BizTalk 서비스 구독을 보유했다고 가정합니다.
* Hello BizTalk 서비스 포털에서 BizTalk 서비스 구독을 등록 합니다. 자세한 내용은 [hello BizTalk 서비스 포털에서 BizTalk 서비스 배포를 등록 하는 중](https://msdn.microsoft.com/library/hh689837.aspx)
* Visual Studio가 설치되어 있어야 합니다.
* BizTalk 서비스 SDK가 설치되어 있어야 합니다. 다운로드할 수에서 SDK hello [http://go.microsoft.com/fwlink/?LinkId=235057](http://go.microsoft.com/fwlink/?LinkId=235057)  

## <a name="step-1-create-hello-service-bus-queues"></a>1 단계: hello 서비스 버스 큐 만들기
이 솔루션에서는 거래 파트너 간에 서비스 버스 큐 tooexchange 메시지를 사용 합니다. Contoso와 Northwind에서 메시지를 보낼 큐 toohello 게 hello EAI 및/또는 EDI 브리지 사용 합니다. 이 솔루션에서는 세 개의 서비스 버스 큐가 필요합니다.

* **northwindreceive** – Northwind는이 큐를 통해 Contoso에서 hello 송장을 받습니다.
* **contosoreceive** – Contoso Northwind 로부터이 큐를 통해 hello 승인의 받습니다.
* **일시 중단** – 모든 일시 중단 된 메시지는 라우트된 toothis 큐입니다. 처리 중 실패하는 경우 메시지는 일시 중단됩니다.

Hello 예제 패키지에 포함 하는 클라이언트 응용 프로그램을 사용 하 여 이러한 서비스 버스 큐를 만들 수 있습니다.  

1. Hello 샘플을 다운로드 하는 hello 위치에서 열고 **자습서 보내는 청구서를 사용 하 여 BizTalk Services EDI Bridges.sln**합니다.
2. 키를 눌러 **F5** toobuild 및 시작 hello **자습서 클라이언트** 응용 프로그램입니다.
3. Hello 화면에 hello 서비스 버스 ACS 네임 스페이스, 발급자 이름 및 발급자 키를 입력 합니다.
   
   ![][2]  
4. 서비스 버스 네임스페이스에서 세 개의 큐가 만들어진다는 메시지 상자가 나타납니다. **확인**을 클릭합니다.
5. Hello 자습서 클라이언트 실행 상태로 유지 합니다. Hello를 열고 **서비스 버스** > ***서비스 버스 네임 스페이스*** > **큐**, 3 hello 큐 만들어졌는지 확인 합니다.  

## <a name="step-2-create-and-deploy-trading-partner-agreement"></a>2단계: 거래 업체 규약 만들기 및 배포
Contoso와 Northwind 간의 거래 업체 규약을 만듭니다. 메시지 스키마 toouse 같은 hello 두 비즈니스 파트너 간의 거래 계약을 정의 하는 거래 업체 규약 메시징 프로토콜 toouse, 등입니다. 거래 파트너 계약 EDI 브리지 두 포함, 하나의 toosend tootrading 파트너를 메시지 (hello 라는 이름의 **EDI 송신 브리지**) 및 거래 파트너 로부터 하나 tooreceive 메시지 (hello 라는 이름의 **EDI 수신 브리지**).

이 솔루션의 hello 컨텍스트에서 hello EDI 송신 브리지 toohello 송신 측 hello 계약에 해당 하 고 Contoso tooNorthwind에서 사용 되는 toosend hello EDIFACT 송장 합니다. 마찬가지로, hello EDI 수신 브리지 toohello 수신 측 hello 계약의 해당 하며 Northwind 로부터 승인을 사용 하는 tooreceive 됩니다.  

### <a name="create-hello-trading-partners"></a>Hello 거래 파트너 만들기
toostart, Contoso와 Northwind에 대 한 거래 파트너를 만듭니다.  

1. Hello에 hello BizTalk 서비스 포털에서에서 **파트너** 탭을 클릭 **추가**합니다.
2. Hello 새 파트너 페이지에서 입력 **Contoso** 파트너 이름 및 클릭으로 **저장**합니다.
3. 반복 hello 단계 toocreate hello 두 번째 파트너를 **Northwind**합니다.  

### <a name="create-hello-agreement"></a>Hello 규약 만들기
거래 업체 규약은 거래 업체의 비즈니스 프로필 간에 생성됩니다. 이 솔루션에서는 hello hello 파트너를 만들 때 자동으로 만들어지는 기본 파트너 프로필을 사용 합니다.  

1. BizTalk 서비스 포털 hello 클릭 **계약** > **추가**합니다.
2. Hello 새 계약에 **일반 설정** 페이지 hello 이미지 아래에 나와 있는 것 처럼 hello 값을 지정 하 고 클릭 **계속**합니다.
   
   ![][3]  
   
   **계속**을 클릭하면 두 개의 탭 **수신 설정** 및 **송신 설정**을 사용할 수 있습니다.
3. Contoso와 Northwind 간의 송신 규약을 hello을 만듭니다. 이 규약은 Contoso hello EDIFACT 송장 tooNorthwind 보내는 방법을 관리 합니다.
   
   1. **송신 설정**을 클릭합니다.
   2. Hello에 hello 기본 값을 유지 **인바운드 URL**, **변환**, 및 **일괄 처리가** 탭 합니다.
   3. Hello에 **프로토콜** 탭 hello 아래 **스키마** 섹션에서 hello 업로드 **EFACT_D93A_INVOIC.xsd** 스키마입니다. 이 스키마는 hello 샘플 패키지와 함께 사용할 수 있습니다.
      
      ![][4]  
   4. Hello에 **전송** 탭에서 서비스 버스 큐 hello에 대 한 hello 세부 정보를 지정 합니다. Hello 송신 측 규약에서는 hello 사용 **northwindreceive** toosend hello EDIFACT 송장 tooNorthwind 대기 및 hello **일시 중단** tooroute 되며 처리 중 실패 하는 모든 메시지 큐 일시 중지 됩니다. 이러한 큐에서 만든 **1 단계: hello 서비스 버스 큐 만들기** 이 항목의 합니다.
      
      ![][5]  
      
      아래 **전송 설정 > 전송 방식이** 및 **메시지 일시 중단 설정 > 전송 방식이**, Azure 서비스 버스를 선택 하 고 hello 그림과 같이 hello 값을 제공 합니다.
4. Hello 만들기 수신 Contoso와 Northwind 간의 계약입니다. 이 규약은 Contoso가 Northwind 로부터 승인을 hello을 수신 하는 방법을 관리 합니다.
   
   1. **수신 설정**을 클릭합니다.
   2. Hello에 hello 기본 값을 유지 **전송** 및 **변환** 탭 합니다.
   3. Hello에 **프로토콜** 탭 hello 아래 **스키마** 섹션에서 hello 업로드 **EFACT_4.1_CONTRL.xsd** 스키마입니다. 이 스키마는 hello 샘플 패키지와 함께 사용할 수 있습니다.
   4. Hello에 **경로** 탭에서 Northwind의 승인을 라우트된 tooContoso만 필터 tooensure를 만듭니다. 아래 **경로 설정**, 클릭 **추가** toocreate hello 라우팅 필터입니다.
      
      ![][6]  
      
      1. 에 대 한 값을 제공 **규칙 이름**, **경로 규칙**, 및 **경로 대상** hello 이미지에 나와 있는 것 처럼 합니다.
      2. **Save**를 클릭합니다.
   5. Hello에 **경로** 다시 탭을 일시 중단 된 승인 (처리 중 실패 하는 승인)를 라우팅할 위치를 지정 합니다. Hello 전송 형식 tooAzure 서비스 버스 설정, 라우팅 대상 유형을 너무**큐**, 인증 유형을 너무**공유 액세스 서명을** hello 서비스 버스에 대 한 hello SAS 연결 문자열을 제공 하는 (SAS) 네임 스페이스를 다음으로 hello 큐 이름을 입력 하 고 **일시 중단**합니다.
5. 마지막으로, 클릭 **배포** toodeploy hello 계약입니다. 참고 hello 끝점 hello 송신 및 수신 규약에 배포 합니다.
   
   * Hello에 **송신 설정** 탭의 **인바운드 URL**, hello 끝점을 확인 합니다. toosend hello를 사용 하 여 Contoso tooNorthwind의 메시지를 EDI 송신 브리지로 메시지 toothis 끝점과 전송 해야 합니다.
   * Hello에 **수신 설정** 탭의 **전송**, hello 끝점을 확인 합니다. toosend hello EDI를 사용 하 여 Northwind tooContoso에서 메시지 수신 브리지, 메시지 toothis 끝점을 보내야 합니다.  

## <a name="step-3-create-and-deploy-hello-biztalk-services-project"></a>3 단계: 프로젝트 만들기 및 배포 hello BizTalk 서비스
Hello 이전 단계에서 EDI 송신 및 수신 규약 tooprocess EDIFACT 송장 및 승인을 hello 배포. 이러한 계약 toohello 표준 EDIFACT 메시지 스키마를 따르는 메시지만을 처리할 수 있습니다. 그러나이 솔루션에 대 한 hello 시나리오 마다 Contoso 송장 tooNorthwind에에서 보냅니다는 내부 소유 스키마. 따라서 hello 메시지를 보낼 EDI 송신 브리지로 toohello 전에 hello 내부 스키마 toohello 표준 EDIFACT 송장 스키마에서 변환 되어야 합니다. hello BizTalk 서비스 EAI 프로젝트는 그렇게 진행 합니다.

hello BizTalk 서비스 프로젝트 **InvoiceProcessingBridge**, 다운로드 한 hello 샘플의 일부분으로 포함 되어 변환 환영 메시지가 있습니다. hello 프로젝트 아티팩트를 수행 하는 hello를 포함 되어 있습니다.

* **INHOUSEINVOICE 합니다. XSD** – tooNorthwind 보내지는 hello 내부 송장 스키마입니다.
* **EFACT_D93A_INVOIC 합니다. XSD** – hello 표준 EDIFACT 송장 스키마입니다.
* **EFACT_4.1_CONTRL 합니다. XSD** – Northwind tooContoso 보냅니다는 hello EDIFACT 승인의 스키마입니다.
* **INHOUSEINVOICE_to_D93AINVOIC 합니다. TRFM** – hello hello 내부 송장 스키마 toohello 표준 EDIFACT 송장 스키마를 매핑하는 변환입니다.  

### <a name="create-hello-biztalk-services-project"></a>Hello BizTalk 서비스 프로젝트 만들기
1. Hello Visual Studio 솔루션에서에서 hello InvoiceProcessingBridge 프로젝트를 열고 다음 hello **MessageFlowItinerary.bcs** 파일입니다.
2. Hello 캔버스에서 아무 곳 이나 클릭 하 고 hello 설정 **BizTalk 서비스 URL** 에 hello 속성 상자 toospecify BizTalk 서비스 구독 이름입니다. 예: `https://contosowabs.biztalk.windows.net`.
   
   ![][7]  
3. Hello 도구 상자에서 끌어는 **Xml 단방향 브리지** toohello 캔버스입니다. 집합 hello **엔터티 이름** 및 **상대 주소** hello의 속성을 너무 브리징**ProcessInvoiceBridge**합니다. 두 번 클릭 **ProcessInvoiceBridge** tooopen hello 브리지 구성 화면입니다.
4. Hello 내에서 **메시지 유형** 상자 hello 더하기 기호 (**+**) hello 들어오는 메시지의 단추 toospecify hello 스키마입니다. EAI 브리지 hello에 대 한 들어오는 메시지 hello hello 내부 송장 항상 이기 때문에이 설정 너무**INHOUSEINVOICE**합니다.
   
   ![][8]  
5. Hello 클릭 **Xml 변환** 셰이프를 hello에 대 한 hello 속성 상자 **지도** 속성을 hello 줄임표를 클릭 (**...** ) 단추입니다. Hello에 **맵 선택** 대화 상자, 선택 hello **INHOUSEINVOICE_to_D93AINVOIC** 변환 파일을 클릭 하 고 **확인**합니다.
   
   ![][9]  
6. 너무 돌아가서**MessageFlowItinerary.bcs**, hello 도구 상자에서 끌어는 **양방향 외부 서비스 끝점** hello의 오른쪽 toohello **ProcessInvoiceBridge**합니다. 설정의 **엔터티 이름** 속성 너무**EDIBridge**합니다.
7. Hello 솔루션 탐색기에서에서 확장 hello **MessageFlowItinerary.bcs** hello를 두 번 클릭 하 고 **EDIBridge.config** 파일입니다. Hello의 hello 내용 바꾸기 **EDIBridge.config** hello 다음과 같이 합니다.
   
   > [!NOTE]
   > Tooedit hello.config 파일 필요한 이유는 무엇입니까? hello 외부 서비스 끝점 toohello 브리지 디자이너 캔버스에 추가한 이유는 이전에 배포한 hello EDI 브리지를 나타냅니다. EDI 브리지는 양방향 브리지이며 송신 측과 수신 측이 있습니다. 그러나 hello toohello 브리지 디자이너 추가한 EAI 브리지는 단방향 브리지입니다. 따라서 hello 서로 다른 메시지 교환 패턴 hello 두 브리지의 toohandle 하 고, 사용 사용자 지정 브리지 동작 hello.config 파일에 구성을 포함 하 여 합니다. 또한 사용자 지정 동작 hello는 hello 인증 toohello EDI 송신 브리지 끝점도 처리합니다. 이 사용자 지정 동작에서 별도 샘플으로 제공 됩니다. [BizTalk 서비스 브리지 체인 샘플-EAI tooEDI](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104)합니다. 이 솔루션 다시 hello 샘플을 사용합니다.  
   > 
   > 
   
   ```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
     <system.serviceModel>
       <extensions>
         <behaviorExtensions>
           <add name="BridgeAuthentication" 
                 type="Microsoft.BizTalk.Bridge.Behaviour.BridgeBehaviorElement, Microsoft.BizTalk.Bridge.Behaviour, Version=1.0.0.0, Culture=neutral, PublicKeyToken=ae58f69b69495c05" />
         </behaviorExtensions>
       </extensions>
       <behaviors>
         <endpointBehaviors>
           <behavior name="BridgeAuthenticationConfiguration">
             <!-- Enter hello ACS namespace, issuer name and issuer secret of hello BizTalk Services deployment -->
             <BridgeAuthentication acsnamespace="[YOUR ACS NAMESPACE]" 
                                   issuername="owner" 
                                   issuersecret="[YOUR ACS SECRET]" />
             <webHttp />
           </behavior>
         </endpointBehaviors>
       </behaviors>
       <bindings>
         <webHttpBinding>
           <binding name="BridgeBindingConfiguration">
             <security mode="Transport" />
           </binding>
         </webHttpBinding>
       </bindings>
       <client>
         <clear />
         <!--
           Go BizTalk Portal > Agreement > Send Settings > Inbound URL
           Copy hello Endpoint URL and paste it in hello below address field
         -->
         <endpoint name="TwoWayExternalServiceEndpointReference1" 
                   address="[YOUR EDI BRIDGE SEND URI]" 
                   behaviorConfiguration="BridgeAuthenticationConfiguration" 
                   binding="webHttpBinding" 
                   bindingConfiguration="BridgeBindingConfiguration" 
                   contract="System.ServiceModel.Routing.IRequestReplyRouter" />
       </client>
     </system.serviceModel>
   </configuration>
   
   ```
8. Hello EDIBridge.config 파일 tooinclude 구성 세부 정보 업데이트
   
   * 아래  *<behaviors>* hello ACS 네임 스페이스를 제공 하 고 BizTalk 서비스 구독 hello와 관련 된 키, 합니다.
   * 아래  *<client>* , EDI 송신 규약 hello를 배포 하는 hello 끝점을 제공 합니다.
   
   변경 내용을 저장 하 고 hello 구성 파일을 닫습니다.
9. 도구 상자 hello에서 클릭 hello **커넥터** 및 조인 hello **ProcessInvoiceBridge** 및 **EDIBridge** 구성 요소입니다. Hello 커넥터를 선택 하 고 속성 상자에서 설정 **필터 조건** 너무**모두 일치**합니다. 이렇게 하면 hello EAI 브리지에서 처리 하는 모든 메시지가 라우팅되는 toohello EDI 브리지입니다.
   
   ![][10]  
10. 변경 toohello 솔루션을 저장 합니다.  

### <a name="deploy-hello-project"></a>Hello 프로젝트 배포
1. Hello hello BizTalk 서비스 프로젝트를 만들 위치를 컴퓨터에서 다운로드 하 여 BizTalk 서비스 구독에 대 한 hello SSL 인증서를 설치 합니다. BizTalk 서비스에서 **대시보드**를 클릭한 다음 **SSL 인증서 다운로드**를 클릭합니다. Hello 인증서를 두 번 클릭 하 고 hello 프롬프트 toocomplete hello 설치를 수행 합니다. 아래의 hello 인증서가 설치 되었는지 확인 **신뢰할 수 있는 루트 인증 기관** 인증서 저장소입니다.
2. Visual Studio 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **InvoiceProcessingBridge** 프로젝트를 마우스 클릭 **배포**합니다.
3. Hello 이미지에 나와 있는 것 처럼 hello 값을 입력 한 다음 **배포**합니다. 클릭 하 여 BizTalk 서비스에 대 한 hello ACS 자격 증명을 가져올 수 있습니다 **연결 정보** hello BizTalk 서비스 대시보드에서.
   
   ![][11]  
   
   Hello 출력 창에서 복사 hello EAI 브리지가 배포 되는 위치, 예를 들어 hello 끝점 `https://contosowabs.biztalk.windows.net/default/ProcessInvoiceBridge`합니다. 이 끝점 URL은 나중에 필요합니다.  

## <a name="step-4-test-hello-solution"></a>4 단계: hello 솔루션 테스트
이 항목에서는 tootest hello를 사용 하 여 솔루션을 hello 하는 방법을 살펴보겠습니다 **자습서 클라이언트** hello 샘플의 일부로 제공 되는 응용 프로그램입니다.  

1. Visual Studio에서 F5 toostart hello 키를 누릅니다. **자습서 클라이언트**합니다.
2. 만든 hello 서비스 버스 큐 hello 값 hello 단계도 미리 채워져 hello 화면에 있어야 합니다. **다음**을 누릅니다.
3. Hello 다음 창에서 BizTalk 서비스 구독에 대 한 ACS 자격 증명을 제공 하 고 끝점 hello 여기서 EAI 및 EDI (수신) 브리지가 배포 된 합니다.
   
   Hello EAI 브리지 끝점 hello 이전 단계에서 복사 했습니다. Hello BizTalk 서비스 포털에서에서 브리지 끝점에서 수신 하는 EDI에 대 한 이동 toohello 규약 > 수신 설정 > 전송 > 끝점입니다.
   
   ![][12]  
4. Hello 다음 창에서 Contoso, 클릭 hello **내부 송장 보내기** 단추입니다. Hello 파일 대화 상자를 열고, hello INHOUSEINVOICE.txt 파일을 엽니다. Hello 파일의 hello 내용을 검토 하 고 클릭 **확인** toosend hello 송장 합니다.
   
   ![][13]  
5. 몇 초 hello에서 Northwind에 송장이 전송 합니다. Hello 클릭 **메시지 보기** Northwind가 받은 링크 toosee hello 송장을 합니다. Contoso 보낸 hello 동안 표준 EDIFACT 스키마에서 Northwind가 받은 hello 송장을 어떻게가 내부 스키마입니다.
   
   ![][14]  
6. Hello 청구서를 선택한 다음 클릭 **승인 보내기**합니다. 팝업 되 hello 대화 상자에서 해당 hello 교환 ID가 동일한 보낸 받은 송장 및 hello 승인 hello 확인 합니다. Hello에서 확인을 클릭 **승인 보내기** 대화 상자.
   
   ![][15]  
7. 몇 초 후에서 contoso hello 승인은 성공적으로 수신 됩니다.
   
   ![][16]  

## <a name="step-5-optional-send-edifact-invoice-in-batches"></a>5단계(선택): 일괄 처리로 EDIFACT 송장 보내기
BizTalk 서비스 EDI 브리지는 나가는 메시지의 일괄 처리도 지원합니다. 이 기능은 tooreceive 일괄 처리 메시지 (특정 모임 조건) 개별 메시지 대신 선호 하는 파트너를 수신 하는 데 유용 합니다.

일괄 처리를 작업할 때 가장 중요 한 측면 hello는 hello 릴리스 조건이 라고도 hello 일괄 처리의 hello 실제 릴리스입니다. hello 릴리스 조건은 어떻게 hello 받는 파트너가 원하는 메시지 tooreceive 메시지 기반 될 수 있습니다. 일괄 처리가 활성화 되는 경우 EDI 브리지 hello hello 나가는 메시지 toohello hello 릴리스 조건이 충족 될 때까지 파트너 받는 보내지 않습니다. 예를 들어 메시지 크기에 따른 일괄 처리 기준은 'n' 메시지가 일괄 처리된 경우에만 일괄 처리를 디스패치합니다. 일괄 처리가 매일 정해진 시간에 전송되도록 일괄 처리 조건은 시간 기반이 될 수도 있습니다. 이 솔루션에서는 hello 메시지 크기를 기준 시도 합니다.

1. Hello BizTalk 서비스 포털에서에서 앞에서 만든 hello 규약을 클릭 합니다. 송신 설정 > 일괄 처리 > 일괄 처리 추가를 클릭합니다.
2. 일괄 처리 이름으로 **InvoiceBatch**를 입력하고 설명을 제공한 다음 **다음**을 클릭합니다.
3. 일괄 처리해야 하는 메시지를 정의하는 일괄 처리 조건을 지정합니다. 이 솔루션에서는 모든 메시지를 일괄 처리합니다. 따라서 hello 고급 정의 사용 옵션을 선택 하 고 입력 **1 = 1**합니다. 이는 항상 true가 되는 조건이므로 모든 메시지가 일괄 처리됩니다. **다음**을 누릅니다.
   
   ![][17]  
4. 일괄 처리 릴리스 조건을 지정합니다. Hello 드롭다운 상자에서 선택 **MessageCountBased**, 및에 대 한 **Count**, 지정 **3**합니다. 이 세 개의 메시지 일괄 처리 tooNorthwind 전송 될 것을 의미 합니다. **다음**을 누릅니다.
   
   ![][18]  
5. Hello 요약을 검토 한 다음 클릭 **저장**합니다. 클릭 **배포** tooredeploy hello 계약입니다.
6. Toohello 돌아가서 **자습서 클라이언트**, 클릭 **내부 송장 보내기**, hello 프롬프트 toosend hello 청구서를 따릅니다. 송장이 전송 되지 Northwind에서 hello 일괄 처리 크기가 맞지 않아 때문에 확인할 수 있습니다. 이 단계를 두 번 더으로 반복 tooNorthwind 보낸 송장 메시지 세 갖도록 합니다. 3 개의 메시지 일괄 처리 릴리스 기준을 hello 및 Northwind에서 청구서 이제 표시 충족 합니다.

<!--Image references-->
[1]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-1.PNG  
[2]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-2.PNG  
[3]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-3.PNG
[4]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-4.PNG  
[5]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-5.PNG  
[6]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-6.PNG  
[7]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-7.PNG  
[8]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-8.PNG
[9]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-9.PNG  
[10]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-10.PNG  
[11]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-11.PNG  
[12]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-12.PNG  
[13]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-13.PNG
[14]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-14.PNG  
[15]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-15.PNG  
[16]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-16.PNG  
[17]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-17.PNG  
[18]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-18.PNG

