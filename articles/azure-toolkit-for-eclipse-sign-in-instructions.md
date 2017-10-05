---
title: "Eclipse용 Azure 도구 키트에 대한 로그인 지침 | Microsoft Docs"
description: "Eclipse용 Azure 도구 키트를 사용하여 Microsoft Azure에 로그인하는 방법을 알아봅니다."
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
ms.openlocfilehash: 02dd9935086c4c40d9ed54cc9ff2412ca96889f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a>Eclipse용 Azure 도구 키트에 대한 Azure 로그인 지침

Eclipse용 Azure 도구 키트는 Azure 계정에 로그인하는 두 가지 방법을 제공합니다.

  * **대화형** - 이 방법을 사용하는 경우 Azure 계정에 로그인할 때마다 Azure 자격 증명을 입력합니다.
  * **자동** - 이 방법을 사용하는 경우 서비스 주체 데이터를 포함하는 자격 증명 파일을 만든 다음 해당 자격 증명 파일을 사용하여 Azure 계정에 자동으로 로그인할 수 있습니다.

다음 섹션의 단계에서는 각 방법을 사용하는 방법을 설명합니다.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a>대화형으로 Azure 계정에 로그인

다음 단계에서는 Azure 자격 증명을 수동으로 입력하여 Azure에 로그인하는 방법을 설명합니다.

1. Eclipse로 프로젝트를 엽니다.

1. **도구**를 클릭한 다음 **Azure**를 클릭하고 **로그인**을 클릭합니다.

   ![Azure 로그인을 위한 Eclipse 메뉴][I01]

1. **Azure 로그인** 대화 상자가 나타나면 **대화형**을 선택한 다음 **로그인**을 클릭합니다.

   ![로그인 대화 상자][I02]

1. **Azure 로그인** 대화 상자가 나타나면 Azure 자격 증명을 입력하고 **로그인**을 클릭합니다.

   ![Azure 로그인 대화 상자][I03]

1. **구독 선택** 대화 상자가 나타나면 사용하려는 구독을 선택하고 **확인**을 클릭합니다.

   ![구독 선택 대화 상자 관리][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a>대화형으로 로그인되었을 때 Azure 계정에서 로그아웃

이전 섹션의 단계를 구성한 후에는 Eclipse를 다시 시작할 때마다 Azure 계정에서 자동으로 로그아웃됩니다. 그러나 Eclipse를 다시 시작하지 않고 Azure 계정에서 로그아웃하려면 다음 단계를 따릅니다.

1. Eclipse에서 **도구**를 클릭한 다음 **Azure**를 클릭하고 **로그아웃**을 클릭합니다.

   ![Azure 로그아웃을 위한 Eclipse 메뉴][L01]

1. **Azure 로그아웃** 대화 상자가 나타나면 **예**를 클릭합니다.

   ![로그아웃 대화 상자][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-to-use-in-the-future"></a>Azure 계정에 자동으로 로그인 및 나중에 사용할 자격 증명 파일 만들기

다음 단계에서는 서비스 주체 데이터를 포함하는 자격 증명 파일을 만드는 과정을 안내합니다. 이러한 단계를 완료한 후 Eclipse에서는 사용자가 프로젝트를 열 때마다 해당 자격 증명 파일을 자동으로 사용해서 Azure에 자동으로 로그인합니다.

1. Eclipse로 프로젝트를 엽니다.

1. **도구**를 클릭한 다음 **Azure**를 클릭하고 **로그인**을 클릭합니다.

   ![Azure 로그인을 위한 Eclipse 메뉴][A01]

1. **Azure 로그인** 대화 상자가 나타나면 **자동**을 선택한 다음 **새로 만들기**를 클릭합니다.

   ![로그인 대화 상자][A02]

1. **Azure 로그인** 대화 상자가 나타나면 Azure 자격 증명을 입력하고 **로그인**을 클릭합니다.

   ![Azure 로그인 대화 상자][A03]

1. **인증 파일 만들기** 대화 상자가 나타나면 사용할 구독을 선택하고 대상 디렉터리를 선택한 후 **시작**을 클릭합니다.

   ![Azure 로그인 대화 상자][A04]

1. **서비스 주체 만들기 상태** 대화 상자가 표시됩니다. 파일이 성공적으로 만들어진 후에 **확인**을 클릭합니다.

   ![서비스 주체 만들기 상태 대화 상자][A05]

1. **Azure 로그인** 대화 상자가 나타나면 **로그인**을 클릭합니다.

   ![Azure 로그인 대화 상자][A06]

1. **구독 선택** 대화 상자가 나타나면 사용하려는 구독을 선택하고 **확인**을 클릭합니다.

   ![구독 선택 대화 상자 관리][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a>자동으로 로그인되었을 때 Azure 계정에서 로그아웃

이전 섹션의 단계를 구성한 후에는 Eclipse를 다시 시작할 때마다 Azure 도구 키트를 통해 Azure 계정에서 자동으로 로그인됩니다. 그러나 Azure 계정에서 로그아웃하고 Azure 도구 키트를 통해 자동으로 로그인되지 않게 하려면 다음 단계를 사용합니다.

1. Eclipse에서 **도구**를 클릭한 다음 **Azure**를 클릭하고 **로그아웃**을 클릭합니다.

   ![Azure 로그아웃을 위한 Eclipse 메뉴][L01]

1. **Azure 로그아웃** 대화 상자가 나타나면 **예**를 클릭합니다.

   ![로그아웃 대화 상자][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a>이미 만든 자격 증명 파일을 사용하여 Azure 계정에 자동으로 로그인

Eclipse를 사용할 때 Azure에서 로그아웃된 경우 Azure 계정으로 자동으로 로그인하려면 만든 자격 증명을 사용하도록 Eclipse용 Azure 도구 키트를 다시 구성해야 합니다. 다음 단계에서는 기존 자격 증명 파일을 사용하도록 Azure 도구 키트를 구성하는 과정을 안내합니다.

1. Eclipse로 프로젝트를 엽니다.

1. **도구**를 클릭한 다음 **Azure**를 클릭하고 **로그인**을 클릭합니다.

   ![Azure 로그인을 위한 Eclipse 메뉴][A01]

1. **Azure 로그인** 대화 상자가 나타나면 **자동**을 선택한 다음 **찾아보기**를 클릭합니다.

   ![로그인 대화 상자][A02]

1. **인증된 파일 선택** 대화 상자가 나타나면 이전에 만든 자격 증명 파일을 선택한 다음 **선택**을 클릭합니다.

   ![로그인 대화 상자][A08]

1. **Azure 로그인** 대화 상자가 나타나면 **로그인**을 클릭합니다.

   ![Azure 로그인 대화 상자][A06]

1. **구독 선택** 대화 상자가 나타나면 사용하려는 구독을 선택하고 **확인**을 클릭합니다.

   ![구독 선택 대화 상자 관리][A07]

## <a name="see-also"></a>참고 항목
Java IDE용 Azure 도구 키트에 대한 자세한 내용은 다음 링크를 참조하세요.

* [Eclipse용 Azure 도구 키트]
  * [Eclipse용 Azure 도구 키트의 새로운 기능]
  * [Eclipse용 Azure 도구 키트 설치]
  * *Eclipse용 Azure 도구 키트에 대한 로그인 지침(이 문서)*
  * [Eclipse에서 Azure용 Hello World 웹앱 만들기]
* [IntelliJ용 Azure 도구 키트]
  * [IntelliJ용 Azure 도구 키트의 새로운 기능]
  * [IntelliJ용 Azure 도구 키트 설치]
  * [IntelliJ용 Azure 도구 키트에 대한 로그인 지침]
  * [IntelliJ에서 Azure용 Hello World 웹앱 만들기]

Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Azure Java 개발자 센터] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.

<!-- URL List -->

[Eclipse용 Azure 도구 키트]: ./azure-toolkit-for-eclipse.md
[IntelliJ용 Azure 도구 키트]: ./azure-toolkit-for-intellij.md
[Eclipse에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[IntelliJ에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Eclipse용 Azure 도구 키트 설치]: ./azure-toolkit-for-eclipse-installation.md
[IntelliJ용 Azure 도구 키트 설치]: ./azure-toolkit-for-intellij-installation.md
[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[IntelliJ용 Azure 도구 키트에 대한 로그인 지침]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Eclipse용 Azure 도구 키트의 새로운 기능]: ./azure-toolkit-for-eclipse-whats-new.md
[IntelliJ용 Azure 도구 키트의 새로운 기능]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/
[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/

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
