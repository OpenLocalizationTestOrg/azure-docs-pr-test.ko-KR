---
title: "Eclipse 용 Azure 도구 키트 hello에 대 한 지침에 aaaSign | Microsoft Docs"
description: "사용 하 여 Microsoft Azure에 toosign Azure Toolkit for Eclipse hello 하는 방법에 대해 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 95be64750ca0147f76dae8f364fad80cb9ccc969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sign-in-instructions-for-hello-azure-toolkit-for-eclipse"></a>Azure hello Eclipse 용 Azure 도구 키트에 대 한 지침에 로그인

Azure Toolkit for Eclipse hello Azure 계정에 로그인 하는 두 가지 방법을 제공 합니다.

  * **대화형** - 이 방법을 사용하는 경우 Azure 계정에 로그인할 때마다 Azure 자격 증명을 입력합니다.
  * **자동화 된** -이 방법을 사용 하는 경우는 Azure 계정에 hello 자격 증명 파일 tooautomatically 기호를 사용할 수 있습니다 프로그램 서비스 사용자 데이터를 포함 하는 자격 증명 파일을 만듭니다.

hello hello 다음 섹션의에서 단계에서는 설명 방법을 toouse 각 방법입니다.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a>대화형으로 Azure 계정에 로그인

hello 다음 단계는 설명 어떻게 수동으로 Azure 자격 증명을 입력 하 여 Azure에 toosign 합니다.

1. Eclipse로 프로젝트를 엽니다.

1. **도구**를 클릭한 다음 **Azure**를 클릭하고 **로그인**을 클릭합니다.

   ![Azure 로그인을 위한 Eclipse 메뉴][I01]

1. Hello 때 **Azure 로그인** 선택 대화 상자가 나타나면 **Interactive'**, 클릭 하 고 **로그인**합니다.

   ![로그인 대화 상자][I02]

1. Hello 때 **Azure 로그인** Azure 자격 증명을 입력 하 고 클릭 한 다음 대화 상자가 나타나면 **로그인**합니다.

   ![Azure 로그인 대화 상자][I03]

1. Hello 때 **구독 선택** 대화 상자가 나타나면 선택 hello 구독 toouse를 원하고 클릭 **확인**합니다.

   ![구독 선택 대화 상자 관리][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a>대화형으로 로그인되었을 때 Azure 계정에서 로그아웃

Hello 이전 단원의 hello 단계를 구성한 후 Azure 계정 Eclipse 다시 시작할 때마다 자동으로 로그인 됩니다. 그러나 Azure 계정에서 Eclipse를 다시 시작 하지 않고 toosign를 원하는 경우 단계를 수행 하는 hello를 사용 합니다.

1. Eclipse에서 **도구**를 클릭한 다음 **Azure**를 클릭하고 **로그아웃**을 클릭합니다.

   ![Azure 로그아웃을 위한 Eclipse 메뉴][L01]

1. Hello 때 **Azure 로그 아웃** 대화 상자가 나타나면 클릭 **예**합니다.

   ![로그아웃 대화 상자][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-toouse-in-hello-future"></a>Azure 계정에 자동으로 로그인 하 고 자격 증명 만들어 파일 toouse hello 이후

hello 다음 단계는 만드는 과정을 안내 서비스 주요 데이터를 포함 하는 자격 증명 파일입니다. 이러한 단계, Eclipse가 자동으로 완료 한 후 사용 하 여 hello 자격 증명 파일 tooautomatically 기호 때마다 하면 각 Azure 프로젝트를 엽니다.

1. Eclipse로 프로젝트를 엽니다.

1. **도구**를 클릭한 다음 **Azure**를 클릭하고 **로그인**을 클릭합니다.

   ![Azure 로그인을 위한 Eclipse 메뉴][A01]

1. Hello 때 **Azure 로그인** 선택 대화 상자가 나타나면 **자동**, 클릭 하 고 **새로**합니다.

   ![로그인 대화 상자][A02]

1. Hello 때 **Azure 로그인** Azure 자격 증명을 입력 하 고 클릭 한 다음 대화 상자가 나타나면 **로그인**합니다.

   ![Azure 로그인 대화 상자][A03]

1. Hello 때 **인증 파일을 만들** 대화 상자가 나타나면 원하는 toouse, 대상 디렉터리를 선택한 다음 클릭 선택 hello 구독 **시작**합니다.

   ![Azure 로그인 대화 상자][A04]

1. hello **서비스 사용자 Creatation 상태** 대화 상자가 표시 됩니다, 파일이 성공적으로 만든 후를 클릭 하 고 **확인**합니다.

   ![서비스 주체 만들기 상태 대화 상자][A05]

1. Hello 때 **Azure 로그인** 대화 상자가 나타나면 클릭 **로그인**합니다.

   ![Azure 로그인 대화 상자][A06]

1. Hello 때 **구독 선택** 대화 상자가 나타나면 선택 hello 구독 toouse를 원하고 클릭 **확인**합니다.

   ![구독 선택 대화 상자 관리][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a>자동으로 로그인되었을 때 Azure 계정에서 로그아웃

Hello 이전 단원의 hello 단계를 구성 하 고 나면 hello Azure 도구 키트가 자동으로 로그인 하면 Eclipse 다시 시작할 때마다 Azure 계정에 합니다. 그러나 toosign의 Azure 계정, 사용 하 여 hello 단계 자동으로 로그인 할 hello Azure 도구 키트 되지 않습니다.

1. Eclipse에서 **도구**를 클릭한 다음 **Azure**를 클릭하고 **로그아웃**을 클릭합니다.

   ![Azure 로그아웃을 위한 Eclipse 메뉴][L01]

1. Hello 때 **Azure 로그 아웃** 대화 상자가 나타나면 클릭 **예**합니다.

   ![로그아웃 대화 상자][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a>이미 만든 자격 증명 파일을 사용하여 Azure 계정에 자동으로 로그인

Eclipse를 사용 하는 경우 로그 아웃 Azure tooreconfigure hello Azure 도구 키트에 Eclipse toouse 자격 증명 파일을 Azure 계정을 사용자로 자동으로 서명할 수 전에 만든 할 수 있습니다. hello 다음 단계는 과정을 단계별로 hello Azure 도구 키트 toouse 구성 기존 자격 증명 파일입니다.

1. Eclipse로 프로젝트를 엽니다.

1. **도구**를 클릭한 다음 **Azure**를 클릭하고 **로그인**을 클릭합니다.

   ![Azure 로그인을 위한 Eclipse 메뉴][A01]

1. Hello 때 **Azure 로그인** 선택 대화 상자가 나타나면 **자동**, 클릭 하 고 **찾아보기**합니다.

   ![로그인 대화 상자][A02]

1. Hello 때 **인증 파일 선택** 앞에서 만든 자격 증명 파일을 선택 하 고 클릭 한 다음 대화 상자가 나타나면 **선택**합니다.

   ![로그인 대화 상자][A08]

1. Hello 때 **Azure 로그인** 대화 상자가 나타나면 클릭 **로그인**합니다.

   ![Azure 로그인 대화 상자][A06]

1. Hello 때 **구독 선택** 대화 상자가 나타나면 선택 hello 구독 toouse를 원하고 클릭 **확인**합니다.

   ![구독 선택 대화 상자 관리][A07]

## <a name="see-also"></a>참고 항목
Java Ide에 대 한 hello Azure 도구 키트에 대 한 자세한 내용은 hello 다음 링크 참조:

* [Eclipse용 Azure 도구 키트]
  * [Hello Azure Toolkit for Eclipse에서 새로운 이란]
  * [Hello Eclipse 용 Azure 도구 키트 설치]
  * *Azure Toolkit for Eclipse (이 문서의 내용) hello에 대 한 지침에 로그인*
  * [Eclipse에서 Azure용 Hello World 웹앱 만들기]
* [IntelliJ용 Azure 도구 키트]
  * [Hello IntelliJ 용 Azure 도구 키트에서 새로운 이란]
  * [IntelliJ 용 hello Azure 도구 키트 설치]
  * [Hello IntelliJ 용 Azure 도구 키트에 대 한 지침에 로그인]
  * [IntelliJ에서 Azure용 Hello World 웹앱 만들기]

Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터] 및 hello [Visual Studio Team Services에 대 한 Java 도구]합니다.

<!-- URL List -->

[Eclipse용 Azure 도구 키트]: ./azure-toolkit-for-eclipse.md
[IntelliJ용 Azure 도구 키트]: ./azure-toolkit-for-intellij.md
[Eclipse에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[IntelliJ에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Hello Eclipse 용 Azure 도구 키트 설치]: ./azure-toolkit-for-eclipse-installation.md
[IntelliJ 용 hello Azure 도구 키트 설치]: ./azure-toolkit-for-intellij-installation.md
[Sign In Instructions for hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Hello IntelliJ 용 Azure 도구 키트에 대 한 지침에 로그인]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Hello Azure Toolkit for Eclipse에서 새로운 이란]: ./azure-toolkit-for-eclipse-whats-new.md
[Hello IntelliJ 용 Azure 도구 키트에서 새로운 이란]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/
[Visual Studio Team Services에 대 한 Java 도구]: https://java.visualstudio.com/

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
