---
title: "aaaSign에에 대 한 지침 Azure 도구 키트 hello IntelliJ | Microsoft Docs"
description: "사용 하 여 Azure tooMicrosoft toosign Azure 도구 키트 IntelliJ에 대 한 hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 2de781fc19267cce133b1e6456481497e165fce4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-instructions-for-hello-azure-toolkit-for-intellij"></a>로그인에 대 한 지침 Azure 도구 키트 hello IntelliJ

hello IntelliJ 용 Azure 도구 키트 tooyour Azure 계정에에서 로그인 하는 두 가지 방법을 제공 합니다.

  * **대화형**: tooyour Azure 계정에에서 Azure 자격 증명 로그인 할 때마다 입력 합니다.
  * **자동화 된**: tooyour Azure 계정에에서 tooautomatically 기호를 사용할 수 있는 자격 증명 파일을 만듭니다.

hello 다음 섹션에서는 설명 방법을 toouse 각 방법입니다.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-tooyour-azure-account-interactively"></a>대화형 tooyour Azure 계정으로 로그인

수동으로 Azure 자격 증명을 입력 하 여 tooAzure에 toosign 다음 hello지 않습니다.

1. IntelliJ IDEA로 프로젝트를 엽니다.

2. 클릭 **도구**, 너무 가리킨**Azure**, 클릭 하 고 **Azure 로그인**합니다.

   ![hello IntelliJ Azure Sign In 명령][I01]

3. Hello에 **Azure 로그인** 창에서 **Interactive'**, 클릭 하 고 **로그인**합니다.

   ![선택한 Interactive' 있는 hello Azure 로그인 창][I02]

4. Hello에 **Azure 로그인** Azure 자격 증명을 입력 하 고 클릭 한 다음 대화 상자가 나타나면 **로그인**합니다.

   ![hello Azure 로그인 대화 상자 창][I03]

5. Hello에 **구독 선택** 대화 상자, 선택 hello 구독 toouse를 원하고 클릭 **확인**합니다.

   ![hello 구독 선택 대화 상자][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a>대화형으로 로그인한 후 Azure 계정에서 로그아웃

계정을 구성한 경우 hello 이전 단계를 사용 하 여 하면 자동으로 로그 아웃 IntelliJ 아이디어 다시 시작할 때마다 Azure 계정. 그러나 Azure 계정 toosign 하려는 경우 *없이* 다음 hello 수행 IntelliJ 아이디어를 다시 시작 합니다.

1. Hello에 IntelliJ 아이디어에 **도구** 메뉴 너무 가리킨**Azure**, 클릭 하 고 **Azure 로그 아웃**합니다.

   ![hello IntelliJ Azure 로그 아웃 명령][L01]

2. Hello에 **Azure 로그 아웃** 확인 창이 클릭 **예**합니다.

   ![확인 창 hello Azure 로그 아웃][L02]

## <a name="sign-in-tooyour-azure-account-automatically"></a>Tooyour Azure 계정에에서 자동으로 로그인

이 섹션에서는 서비스 주체 데이터를 포함하는 자격 증명 파일을 만드는 과정을 안내합니다. 이 프로세스를 완료 한 후 Eclipse 사용 하 여 hello 자격 증명 파일 tooautomatically 기호 때마다 각 tooAzure에서 프로젝트를 엽니다.

1. IntelliJ IDEA로 프로젝트를 엽니다.

2. Hello에 **도구** 메뉴 너무 가리킨**Azure**, 클릭 하 고 **Azure 로그인**합니다.

   ![hello IntelliJ Azure Sign In 명령][A01]

3. Hello에 **Azure 로그인** 창에서 **자동**, 클릭 하 고 **새로**합니다.

   ![자동 선택 된 hello Azure 로그인 창][A02]

4. Hello에 **Azure 로그인 대화 상자** 창 Azure 자격 증명을 입력 한 다음 클릭 **로그인**합니다.

   ![hello Azure 로그인 대화 상자 창][A03]

5. Hello에 **인증 파일 만들기** 창, 선택 hello 구독 toouse 원하는, 대상 디렉터리를 선택한 다음 클릭 **시작**합니다.

   ![hello 인증 파일 만들기 창][A04]

6. Hello에 **서비스 사용자 만들기 상태** 대화 상자에서 파일 성공적으로 만든 후 클릭 **확인**합니다.

   ![hello 서비스 사용자 만들기 상태 대화 상자][A05]

7. Hello에 **Azure 로그인** 창 클릭 **로그인**합니다.

   ![Azure 로그인 대화 상자][A06]

8. Hello에 **구독 선택** 대화 상자, 선택 hello 구독 toouse를 원하고 클릭 **확인**합니다.

   ![hello 구독 선택 대화 상자][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a>자동으로 로그인한 후 Azure 계정에서 로그아웃

계정을 구성한 경우 hello 이전 단계를 사용 하 여 hello Azure 도구 키트 자동으로 로그인 tooyour IntelliJ 아이디어 다시 시작할 때마다 Azure 계정. 그러나 Toosign의 Azure 계정 및 hello Azure 도구 키트를 방지 합니다. 다음 hello 수행 자동 로그인에서:

1. Hello에 IntelliJ 아이디어에 **도구** 메뉴 너무 가리킨**Azure**, 클릭 하 고 **Azure 로그 아웃**합니다.

   ![hello IntelliJ Azure 로그 아웃 명령][L01]

2. Hello에 **Azure 로그 아웃** 확인 창이 클릭 **예**합니다.

   ![확인 창 hello Azure 로그 아웃][L03]

## <a name="sign-in-tooyour-azure-account-automatically-by-using-an-existing-credentials-file"></a>계정에에서 로그인 tooyour Azure 자동으로 기존 자격 증명 파일을 사용 하 여

IntelliJ 아이디어를 사용 하는 경우 Azure 계정에서 로그인 하는 경우에 기존 자격 증명 파일 tooautomatically 부호 toohello 계정에 다시 사용 해야 합니다. tooconfigure hello Azure 도구 키트에 Eclipse toouse 기존 자격 증명 파일을 다음 hello지 않습니다.

1. IntelliJ IDEA로 프로젝트를 엽니다.

2. Hello에 **도구** 메뉴 너무 가리킨**Azure**, 클릭 하 고 **Azure 로그인**합니다.

   ![hello IntelliJ Azure Sign In 명령][A01]

3. Hello에 **Azure 로그인** 창에서 **자동**, 클릭 하 고 **찾아보기**합니다.

   ![자동 선택 된 hello Azure 로그인 창][A02]

4. Hello에 **인증 파일 선택** 대화 상자에서 이전에 만든된 자격 증명 파일을 선택한 다음 클릭 **선택**합니다.

   ![hello 인증 파일 선택 대화 상자][A08]

5. Hello에 **Azure 로그인** 창 클릭 **로그인**합니다.

   ![자동 선택 된 hello Azure 로그인 창][A06]

6. Hello에 **구독 선택** 대화 상자, 선택 hello 구독 toouse를 원하고 클릭 **확인**합니다.

   ![hello 구독 선택 대화 상자][A07]

## <a name="next-steps"></a>다음 단계
Java Ide에 대 한 hello Azure 도구 키트에 대 한 자세한 내용은 hello 다음 링크 참조:

* [Eclipse용 Azure 도구 키트]
  * [Hello Eclipse 용 Azure 도구 키트의에서 새로운 기능]
  * [Hello Eclipse 용 Azure 도구 키트 설치]
  * [Eclipse 용 Azure 도구 키트 hello에 대 한 로그인 지침]
  * [Eclipse에서 Azure용 Hello World 웹앱 만들기]
* [IntelliJ용 Azure 도구 키트]
  * [Hello IntelliJ 용 Azure 도구 키트의에서 새로운 기능]
  * [IntelliJ 용 hello Azure 도구 키트 설치]
  * *로그인에 대 한 지침 Azure 도구 키트 hello IntelliJ* (이 문서)
  * [IntelliJ에서 Azure용 Hello World 웹앱 만들기]

Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터] 및 hello [Visual Studio Team Services에 대 한 Java 도구]합니다.

<!-- URL List -->

[Eclipse용 Azure 도구 키트]: ./azure-toolkit-for-eclipse.md
[IntelliJ용 Azure 도구 키트]: ./azure-toolkit-for-intellij.md
[Eclipse에서 Azure용 헬로 월드 웹앱 만들기]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[IntelliJ에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Hello Eclipse 용 Azure 도구 키트 설치]: ./azure-toolkit-for-eclipse-installation.md
[IntelliJ 용 hello Azure 도구 키트 설치]: ./azure-toolkit-for-intellij-installation.md
[Eclipse 용 Azure 도구 키트 hello에 대 한 로그인 지침]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign-in instructions for hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Hello Eclipse 용 Azure 도구 키트의에서 새로운 기능]: ./azure-toolkit-for-eclipse-whats-new.md
[Hello IntelliJ 용 Azure 도구 키트의에서 새로운 기능]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/
[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
