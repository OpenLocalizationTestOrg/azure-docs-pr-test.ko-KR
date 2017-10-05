---
title: "Eclipse용 Azure 도구 키트 설치 | Microsoft Docs"
description: "Eclipse용 Azure 도구 키트를 설치하는 방법을 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 35cddba38c364dfb2f6a8646b0014d48ca4cb795
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a>Eclipse용 Azure 도구 키트 설치
Eclipse용 Azure 도구 키트는 Eclipse 개발 환경에서 Azure 응용 프로그램을 쉽게 작성, 개발, 테스트 및 배포할 수 있는 템플릿과 기능을 제공합니다. Eclipse용 Azure 도구 키트는 오픈 소스 프로젝트입니다. 소스 코드는 <https://github.com/microsoft/azure-tools-for-java>의 MIT 라이선스 아래에서 확인할 수 있습니다.

다음 단계는 Eclipse용 Azure 도구 키트를 설치하는 방법을 보여줍니다.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a>Eclipse용 Azure 도구 키트 설치
1. Eclipse를 시작합니다.
2. 다음 그림에 표시된 대로 **Help** 메뉴를 클릭하고 **Install New Software**를 클릭합니다.
   
    ![Eclipse용 Azure 도구 키트 설치][01]
3. **Available Software** 대화 상자의 **Work with** 텍스트 상자에 `http://dl.microsoft.com/eclipse`를 입력하고 **Enter** 키를 누릅니다.
4. **Name** 창에서 **Azure Toolkit for Eclipse**를 선택하고 **Contact all update sites during install to find required software**를 선택하지 않습니다. 화면은 다음과 유사한 모양입니다.
   
    ![Eclipse용 Azure 도구 키트 설치][02]
5. **Azure Toolkit for Eclipse**를 확장하면 다음 항목이 표시됩니다.
   
   * **Application Insights Plugin for Java**: 이 구성 요소는 응용 프로그램 및 서버 인스턴스에 대해 Azure의 원격 분석 로깅 및 분석 서비스를 사용할 수 있도록 합니다.
   * **Azure Access Control Services Filter**:이 구성 요소는 Azure ACS에서 응용 프로그램 사용자를 인증하도록 하고 Single Sign-On 시나리오를 사용하도록 하고 응용 프로그램에서 ID 논리를 외부화합니다.
   * **Azure Common Plugin**: 이 구성 요소는 다른 도구 키트 구성 요소에 필요한 공통 기능을 제공합니다.
   * **Azure Explorer for Eclipse**: 이 구성 요소는 다른 도구 키트 구성 요소에 필요한 공통 기능을 제공합니다.
   * **Azure Plugin for Eclipse with Java**: 이 구성 요소는 Eclipse에서 및 명령줄을 통해 Microsoft Azure 클라우드용 Java 응용 프로그램을 빌드, 테스트 및 배포하도록 지원하는 프로젝트를 개발할 수 있도록 합니다.
   * **Azure Web Apps Plugin with Java**: 이 구성 요소는 Microsoft Azure 웹앱 컨테이너에 Java 웹 응용 프로그램을 배포할 수 있도록 지원합니다.
   * **Microsoft JDBC Driver 4.2 for SQL Server**: 이 구성 요소는 SQL Server용 JDBC API와 Java Platform Enterprise Edition 8용 Microsoft Azure SQL 데이터베이스를 제공합니다.
   * **Package for Apache Qpid Client Libraries for JMS**: 이 구성 요소는 응용 프로그램이 Microsoft Azure 내에서 AMQP 메시징을 사용할 수 있도록 Apache Qpid 프로젝트의 JMS 클라이언트 구성 요소를 제공합니다.
   * **Package for Microsoft Azure Libraries for Java**: 이 구성 요소는 저장소, 서비스 버스, 서비스 런타임 등의 Microsoft Azure 서비스에 액세스하기 위한 API를 제공합니다.
6. **다음**을 누릅니다. (도구 키트를 설치하는 동안 비정상적인 지연이 발생하는 경우에는 **Contact all update sites during install to find required software** 가 선택되어 있지 않은지 확인합니다.)
7. **설치 세부 정보** 대화 상자에서 **다음**을 클릭합니다.
   
    ![설치 세부 정보 검토][03]
8. **Review Licenses** 대화 상자에서 사용권 계약 조건을 검토합니다. 사용권 계약 조건에 동의하면 **동의함**을 클릭한 후 **마침**을 클릭합니다. (나머지 단계에서는 사용권 계약 조건에 동의한다고 가정합니다. 사용권 계약 조건에 동의하지 않으면 설치 프로세스를 종료합니다.)
   
    ![Review Licenses][04]
   
    Eclipse는 필수 패키지를 다운로드하고 설치합니다.
   
    ![설치 진행률][05]
9. 설치를 완료하기 위해 Eclipse를 다시 시작한다는 메시지가 표시되면 **Yes**를 클릭합니다.
   
    ![다시 시작 프롬프트][06]

## <a name="see-also"></a>참고 항목
Java IDE용 Azure 도구 키트에 대한 자세한 내용은 다음 링크를 참조하세요.

* [Eclipse용 Azure 도구 키트]
  * [Eclipse용 Azure 도구 키트의 새로운 기능]
  * *Eclipse용 Azure 도구 키트 설치(이 문서)*
  * [Eclipse용 Azure 도구 키트에 대한 로그인 지침]
  * [Eclipse에서 Azure용 Hello World 웹앱 만들기]
* [IntelliJ용 Azure 도구 키트]
  * [IntelliJ용 Azure 도구 키트의 새로운 기능]
  * [IntelliJ용 Azure 도구 키트 설치]
  * [IntelliJ용 Azure 도구 키트에 대한 로그인 지침]
  * [IntelliJ에서 Azure용 Hello World 웹앱 만들기]

Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Azure Java 개발자 센터]를 참조하세요.

<!-- URL List -->

[Eclipse용 Azure 도구 키트]: ./azure-toolkit-for-eclipse.md
[IntelliJ용 Azure 도구 키트]: ./azure-toolkit-for-intellij.md
[Eclipse에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[IntelliJ에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[IntelliJ용 Azure 도구 키트 설치]: ./azure-toolkit-for-intellij-installation.md
[Eclipse용 Azure 도구 키트에 대한 로그인 지침]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[IntelliJ용 Azure 도구 키트에 대한 로그인 지침]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Eclipse용 Azure 도구 키트의 새로운 기능]: ./azure-toolkit-for-eclipse-whats-new.md
[IntelliJ용 Azure 도구 키트의 새로운 기능]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->
