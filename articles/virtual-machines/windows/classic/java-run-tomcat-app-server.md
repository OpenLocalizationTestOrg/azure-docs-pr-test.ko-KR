---
title: "클래식 Azure VM에서 aaaRun Java 응용 프로그램 서버 | Microsoft Docs"
description: "이 자습서에서는 어떻게 hello 클래식 배포 모델 및 표시를 사용 하 여 만든 리소스 toocreate Windows 가상 컴퓨터 및 toorun Apache Tomcat 응용 프로그램 서버를 구성 합니다."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d627aa09-f7d6-4239-8110-f8fc5111b939
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 03/16/2017
ms.author: robmcm
ms.openlocfilehash: 2d9f586c9f628d3738522b320996b95b078d7454
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-java-application-server-on-a-virtual-machine-created-with-hello-classic-deployment-model"></a>어떻게 toorun 가상 컴퓨터에서 Java 응용 프로그램 서버는 hello 클래식 배포 모델을 사용 하 여을 만든
> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. 리소스 관리자 템플릿 toodeploy Tomcat 8 Java와 webapp 참조 [여기](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/)합니다.

Azure 가상 컴퓨터 tooprovide 서버 기능을 사용할 수 있습니다. 예를 들어 Azure에서 실행 되는 가상 컴퓨터에 구성 된 toohost Apache Tomcat 같은 Java 응용 프로그램 서버 수 있습니다.

이 가이드를 완료 한 후는 방법 이해 해야 합니다 toocreate 가상 컴퓨터를 Azure에서 실행 되 고 toorun Java 응용 프로그램 서버를 구성 합니다. 자세한 되며 hello 다음 작업을 수행 합니다.

* Java 개발 키트 (JDK) 이미 설치 되어에 어떻게 toocreate 가상 된 컴퓨터에 있습니다.
* 어떻게 tooremotely tooyour 가상 컴퓨터에 로그인 합니다.
* 어떻게 tooinstall는 Java 응용 프로그램 서버--Apache Tomcat-가상 컴퓨터에 있습니다.
* 어떻게 toocreate 가상 컴퓨터에 대 한 끝점입니다.
* 어떻게 tooopen 포트 hello에 응용 프로그램 서버에 대 한 방화벽입니다.

hello 가상 컴퓨터에서 실행 되는 Tomcat에서 설치 결과 완료 합니다.

![Apache Tomcat을 실행하는 가상 컴퓨터][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a>toocreate 가상 컴퓨터
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.  
2. 클릭 **새로**, 클릭 **계산**, 클릭 **스크롤하게** hello에 **추천 앱**합니다.
3. 클릭 **JDK**, 클릭 **JDK 8** hello에 **JDK** 창.  
   가상 컴퓨터 이미지를 지 원하는 **JDK 6** 및 **JDK 7** JDK 8에서 준비 toorun 되지 않는 레거시 응용 프로그램의 경우에 사용할 수 있습니다.
4. JDK 8 hello 창에서 선택 **클래식**, 클릭 **만들기**합니다.
5. Hello에 **기본 사항** 블레이드:
   1. Hello 가상 컴퓨터에 대 한 이름을 지정 합니다.
   2. Hello에 hello 관리자에 대 한 이름을 입력 **사용자 이름** 필드입니다. 이 이름은 기억 하 고 hello hello 다음 필드에 연결 된 암호입니다. 필요할 때 toohello 가상 컴퓨터를 원격으로 로그인 합니다.
   3. Hello에 암호를 입력 **새 암호** hello에 다시 입력 하 고 필드 **암호 확인** 필드입니다. 이 암호는 hello 관리자 계정에 대 한 합니다.
   4. 적절 한 선택 hello **구독**합니다.
   5. Hello에 대 한 **리소스 그룹**, 클릭 **새로 만들기** 새 리소스 그룹의 hello 이름을 입력 합니다. 클릭 또는 **기존 항목 사용** hello 사용 가능한 리소스 그룹 중 하나를 선택 합니다.
   6. 위치와 같은 hello 가상 컴퓨터가 있는 위치를 선택 **미국 중남부**합니다.
6. **다음**을 누릅니다.
7. Hello에 **가상 컴퓨터 이미지 크기** 블레이드를 **표준 A1** 또는 다른 적절 한 이미지입니다.
8. **선택**을 클릭합니다.

9. Hello에 **설정** 블레이드에서 클릭 **확인**합니다. Azure에서 제공 하는 hello 기본 값을 사용할 수 있습니다.  
10. Hello에 **요약** 블레이드에서 클릭 **확인**합니다.

## <a name="tooremotely-sign-in-tooyour-virtual-machine"></a>tooremotely 로그인 tooyour 가상 컴퓨터
1. Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.
2. **가상 컴퓨터(클래식)**를 클릭합니다. 필요한 경우 클릭 **더 많은 서비스** hello 왼쪽된 아래 모서리에 hello 서비스 범주에서 합니다. hello **가상 컴퓨터 (클래식)** hello에 항목이 나타납니다 **계산** 그룹입니다.
3. Hello 하려는 toosign에 hello 가상 컴퓨터 이름을 클릭 합니다.
4. Hello 가상 컴퓨터 시작 후 hello hello 창 위쪽에 메뉴 연결을 허용 합니다.
5. **Connect**를 클릭합니다.
6. 필요한 tooconnect toohello 가상 컴퓨터로 toohello 표시 되는 메시지에 응답 합니다. 일반적으로 저장 하거나 hello 연결 정보를 포함 하는 hello.rdp 파일을 엽니다. Hello hello hello.rdp 파일의 첫 번째 줄의 마지막 부분으로 toocopy hello url: 포트를 가질 수도 있으며 원격 로그인 응용 프로그램에 붙여 넣습니다.

## <a name="tooinstall-a-java-application-server-on-your-virtual-machine"></a>tooinstall 가상 컴퓨터에서 Java 응용 프로그램 서버
Java 응용 프로그램 서버 tooyour 가상 컴퓨터를 복사할 수 있습니다 또는 설치 관리자를 통해 Java 응용 프로그램 서버를 설치할 수 있습니다.

이 자습서는 hello Java 응용 프로그램 서버 tooinstall으로 Tomcat을 사용합니다.

1. Tooyour 가상 컴퓨터에 로그인 한 상태, 브라우저 세션을 너무 열[Apache Tomcat](http://tomcat.apache.org/download-80.cgi)합니다.
2. 에 대 한 hello 링크를 두 번 클릭 **32 비트/64 비트 Windows 서비스 설치 관리자**합니다. 이 기술을 사용하면 Tomcat이 Windows 서비스로 설치됩니다.
3. 대화 상자가 나타나면 toorun hello 설치 관리자를 선택 합니다.
4. Hello 내 **Apache Tomcat 설치** 마법사를 따라 hello tooinstall Tomcat 라는 메시지를 표시 합니다. 이 자습서의 hello에서는 hello 기본값을 그대로 문제가 없습니다. Hello 나타나면 **Apache Tomcat 설치 마법사 완료 hello** 대화 상자에서 필요에 따라를 확인할 수 있습니다 **Apache Tomcat 실행** toohave 이제 Tomcat 시작 합니다. 클릭 **마침** toocomplete hello Tomcat 설치 프로세스입니다.

## <a name="toostart-tomcat"></a>Tomcat toostart

가상 컴퓨터와 실행 중인 hello 명령을 명령 프롬프트를 열어 Tomcat를 수동으로 시작할 수 있습니다 **net&nbsp;시작&nbsp;Tomcat8**합니다.

Hello URL을 입력 하 여 Tomcat Tomcat 실행 되 면 액세스할 수 있습니다 <http://localhost:8080> hello 가상 컴퓨터의 브라우저에서 합니다.

toosee 외부 컴퓨터에서 실행 되는 Tomcat toocreate 끝점 및 해야 포트를 엽니다.

## <a name="toocreate-an-endpoint-for-your-virtual-machine"></a>가상 컴퓨터에 대 한 끝점 toocreate
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. **가상 컴퓨터(클래식)**를 클릭합니다.
3. Java 응용 프로그램 서버에서 실행 되는 hello 가상 컴퓨터의 hello 이름을 클릭 합니다.
4. **Endpoints**를 클릭합니다.
5. **추가**를 클릭합니다.
6. Hello에 **끝점 추가** 대화 상자:
   1. Hello 끝점에 대 한 이름을 지정 합니다. 예를 들어 **HttpIn**합니다.
   2. 선택 **TCP** hello 프로토콜에 대 한 합니다.
   3. 지정 **80** hello 공용 포트에 대 한 합니다.
   4. 지정 **8080** hello 개인 포트에 대 한 합니다.
   5. 선택 **비활성화** hello 부동 IP 주소에 대 한 합니다.
   6. Hello 액세스 제어 목록을 그대로 둡니다.
   7. Hello 클릭 **확인** tooclose hello 대화 상자 단추 및 hello 끝점을 만듭니다.

## <a name="tooopen-a-port-in-hello-firewall-for-your-virtual-machine"></a>가상 컴퓨터에 대 한 hello 방화벽에서 포트 tooopen
1. Tooyour 가상 컴퓨터에 로그인 합니다.
2. **Windows 시작**을 클릭합니다.
3. **제어판**을 클릭합니다.
4. **시스템 및 보안**, **Windows 방화벽**, **고급 설정**을 차례로 클릭합니다.
5. **인바운드 규칙**을 선택하고 **새 규칙**을 클릭합니다.  
   ![새 인바운드 규칙][NewIBRule]
6. Hello에 대 한 **규칙 유형**선택, **포트**, 클릭 하 고 **다음**합니다.  
   ![새 인바운드 규칙 포트][NewRulePort]
7. Hello에 **프로토콜 및 포트** 화면에서 **TCP**, 지정 **8080** hello로 **특정 로컬 포트**, 클릭하고**다음**합니다.  
  ![새 인바운드 규칙][NewRuleProtocol]
8. Hello에 **동작** 화면에서 **hello 연결 허용**, 클릭 하 고 **다음**합니다.
   ![새 인바운드 규칙 동작][NewRuleAction]
9. Hello에 **프로필** 화면에서 **도메인**, **개인**, 및 **공용** 를 선택한 다음 클릭 **다음** .
   ![새 인바운드 규칙 프로필][NewRuleProfile]
10. 그러나 Hello에 **이름** 화면에서 같이 hello 규칙에 대 한 이름을 지정 **HttpIn** (hello 규칙 이름이 하지 않으면 필요한 toomatch hello 끝점 이름을), 클릭 하 고 **마침**합니다.  
    ![새 인바운드 규칙 이름][NewRuleName]

이제 외부 브라우저에서 Tomcat 웹 사이트를 볼 수 있어야 합니다. Hello 브라우저의 주소 창에 hello 폼의 URL을 입력  **http://*프로그램\_DNS\_이름*. cloudapp.net**, 여기서 ***프로그램\_DNS\_이름*** hello 가상 컴퓨터를 만들 때 지정한 hello DNS 이름입니다.

## <a name="application-lifecycle-considerations"></a>응용 프로그램 수명 주기 고려 사항
* 사용자 고유의 웹 응용 프로그램 보관 파일 (WAR)를 만들고 toohello 추가할 수 있습니다 **webapps** 폴더입니다. 예를 들어 기본 JSP(Java 서비스 페이지) 동적 웹 프로젝트를 만들어 WAR 파일로 내보냅니다. 이제 hello WAR toohello Apache Tomcat 복사 **webapps** 후 브라우저에서 실행 되는 hello 가상 컴퓨터의 폴더에 있습니다.
* 기본적으로 hello Tomcat 서비스를 설치 하는 경우 설정은 toostart 수동으로입니다. 전환할 수도 있습니다 toostart 자동으로 hello 서비스 스냅인을 사용 하 여 합니다. 클릭 하 여 hello 서비스 스냅인 시작 **Windows 시작**, **관리 도구**, 차례로 **서비스**합니다. Hello를 두 번 클릭 **Apache Tomcat** 서비스 설정 및 **시작 유형** 너무**자동**합니다.

    ![서비스 toostart를 자동으로 설정][service_automatic_startup]

    hello 있으면 자동으로 시작 하는 Tomcat는 hello 가상 컴퓨터 (예를 들어 한 후 다시 부팅 해야 하는 소프트웨어 업데이트 설치 되어 있음)를 다시 부팅 될 때 실행 되 고 시작 하도록 합니다.

## <a name="next-steps"></a>다음 단계
사용할 수 있는 다른 서비스 (예: Azure 저장소, 서비스 버스, SQL 데이터베이스)에 대 한 학습할 수 있는 Java 응용 프로그램과 함께 tooinclude 합니다. Hello에서 사용할 수 있는 hello 정보를 확인할 [Java 개발자 센터](https://azure.microsoft.com/develop/java/)합니다.

[virtual_machine_tomcat]:media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from hello "toocreate an ednpoint for your virtual mache" 3/17/2017,
     toouse hello new portal.
6. In hello **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In hello **New endpoint details** dialog box:
-->
