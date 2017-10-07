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
# <a name="azure-sign-in-instructions-for-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="2f176-103">Azure hello Eclipse 용 Azure 도구 키트에 대 한 지침에 로그인</span><span class="sxs-lookup"><span data-stu-id="2f176-103">Azure Sign In Instructions for hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="2f176-104">Azure Toolkit for Eclipse hello Azure 계정에 로그인 하는 두 가지 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-104">hello Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  * <span data-ttu-id="2f176-105">**대화형** - 이 방법을 사용하는 경우 Azure 계정에 로그인할 때마다 Azure 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-105">**Interactive** - when you are using this method, you will enter your Azure credentials each time you sign into your Azure account.</span></span>
  * <span data-ttu-id="2f176-106">**자동화 된** -이 방법을 사용 하는 경우는 Azure 계정에 hello 자격 증명 파일 tooautomatically 기호를 사용할 수 있습니다 프로그램 서비스 사용자 데이터를 포함 하는 자격 증명 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-106">**Automated** - when you are using this method, you will create a credentials file which contains your service principal data, after which you can use hello credentials file tooautomatically sign into your Azure account.</span></span>

<span data-ttu-id="2f176-107">hello hello 다음 섹션의에서 단계에서는 설명 방법을 toouse 각 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-107">hello steps in hello following sections will describe how toouse each method.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a><span data-ttu-id="2f176-108">대화형으로 Azure 계정에 로그인</span><span class="sxs-lookup"><span data-stu-id="2f176-108">Signing into your Azure account interactively</span></span>

<span data-ttu-id="2f176-109">hello 다음 단계는 설명 어떻게 수동으로 Azure 자격 증명을 입력 하 여 Azure에 toosign 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-109">hello following steps will illustrate how toosign into Azure by manually entering your Azure credentials.</span></span>

1. <span data-ttu-id="2f176-110">Eclipse로 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-110">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="2f176-111">**도구**를 클릭한 다음 **Azure**를 클릭하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-111">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Azure 로그인을 위한 Eclipse 메뉴][I01]

1. <span data-ttu-id="2f176-113">Hello 때 **Azure 로그인** 선택 대화 상자가 나타나면 **Interactive'**, 클릭 하 고 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-113">When hello **Azure Sign In** dialog box appears, select **Interactive**, and then click **Sign In**.</span></span>

   ![로그인 대화 상자][I02]

1. <span data-ttu-id="2f176-115">Hello 때 **Azure 로그인** Azure 자격 증명을 입력 하 고 클릭 한 다음 대화 상자가 나타나면 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-115">When hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Azure 로그인 대화 상자][I03]

1. <span data-ttu-id="2f176-117">Hello 때 **구독 선택** 대화 상자가 나타나면 선택 hello 구독 toouse를 원하고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-117">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![구독 선택 대화 상자 관리][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a><span data-ttu-id="2f176-119">대화형으로 로그인되었을 때 Azure 계정에서 로그아웃</span><span class="sxs-lookup"><span data-stu-id="2f176-119">Signing out of your Azure account when you signed in interactively</span></span>

<span data-ttu-id="2f176-120">Hello 이전 단원의 hello 단계를 구성한 후 Azure 계정 Eclipse 다시 시작할 때마다 자동으로 로그인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-120">After you have configured hello steps in hello previous section, you will automatically signed out of your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="2f176-121">그러나 Azure 계정에서 Eclipse를 다시 시작 하지 않고 toosign를 원하는 경우 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-121">However, if you want toosign out of your Azure account without restarting Eclipse, use hello following steps.</span></span>

1. <span data-ttu-id="2f176-122">Eclipse에서 **도구**를 클릭한 다음 **Azure**를 클릭하고 **로그아웃**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-122">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Azure 로그아웃을 위한 Eclipse 메뉴][L01]

1. <span data-ttu-id="2f176-124">Hello 때 **Azure 로그 아웃** 대화 상자가 나타나면 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-124">When hello **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![로그아웃 대화 상자][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-toouse-in-hello-future"></a><span data-ttu-id="2f176-126">Azure 계정에 자동으로 로그인 하 고 자격 증명 만들어 파일 toouse hello 이후</span><span class="sxs-lookup"><span data-stu-id="2f176-126">Signing into your Azure account automatically and creating a credentials file toouse in hello future</span></span>

<span data-ttu-id="2f176-127">hello 다음 단계는 만드는 과정을 안내 서비스 주요 데이터를 포함 하는 자격 증명 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-127">hello following steps will walk you through creating a credentials file which contains your service principal data.</span></span> <span data-ttu-id="2f176-128">이러한 단계, Eclipse가 자동으로 완료 한 후 사용 하 여 hello 자격 증명 파일 tooautomatically 기호 때마다 하면 각 Azure 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-128">Once you have completed these steps, Eclipse will automatically use hello credentials file tooautomatically sign you into Azure each time you open your project.</span></span>

1. <span data-ttu-id="2f176-129">Eclipse로 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-129">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="2f176-130">**도구**를 클릭한 다음 **Azure**를 클릭하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-130">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Azure 로그인을 위한 Eclipse 메뉴][A01]

1. <span data-ttu-id="2f176-132">Hello 때 **Azure 로그인** 선택 대화 상자가 나타나면 **자동**, 클릭 하 고 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-132">When hello **Azure Sign In** dialog box appears, select **Automated**, and then click **New**.</span></span>

   ![로그인 대화 상자][A02]

1. <span data-ttu-id="2f176-134">Hello 때 **Azure 로그인** Azure 자격 증명을 입력 하 고 클릭 한 다음 대화 상자가 나타나면 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-134">When hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Azure 로그인 대화 상자][A03]

1. <span data-ttu-id="2f176-136">Hello 때 **인증 파일을 만들** 대화 상자가 나타나면 원하는 toouse, 대상 디렉터리를 선택한 다음 클릭 선택 hello 구독 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-136">When hello **Create authentication files** dialog box appears, select hello subscriptions that you want toouse, choose your destination directory, and then click **Start**.</span></span>

   ![Azure 로그인 대화 상자][A04]

1. <span data-ttu-id="2f176-138">hello **서비스 사용자 Creatation 상태** 대화 상자가 표시 됩니다, 파일이 성공적으로 만든 후를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-138">hello **Service Principal Creatation Status** dialog box will be displayed, and after your files have been created successfully, click **OK**.</span></span>

   ![서비스 주체 만들기 상태 대화 상자][A05]

1. <span data-ttu-id="2f176-140">Hello 때 **Azure 로그인** 대화 상자가 나타나면 클릭 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-140">When hello **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Azure 로그인 대화 상자][A06]

1. <span data-ttu-id="2f176-142">Hello 때 **구독 선택** 대화 상자가 나타나면 선택 hello 구독 toouse를 원하고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-142">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![구독 선택 대화 상자 관리][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a><span data-ttu-id="2f176-144">자동으로 로그인되었을 때 Azure 계정에서 로그아웃</span><span class="sxs-lookup"><span data-stu-id="2f176-144">Signing out of your Azure account when you signed in automatically</span></span>

<span data-ttu-id="2f176-145">Hello 이전 단원의 hello 단계를 구성 하 고 나면 hello Azure 도구 키트가 자동으로 로그인 하면 Eclipse 다시 시작할 때마다 Azure 계정에 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-145">After you have configured hello steps in hello previous section, hello Azure Toolkit will automatically sign you into your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="2f176-146">그러나 toosign의 Azure 계정, 사용 하 여 hello 단계 자동으로 로그인 할 hello Azure 도구 키트 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-146">However, toosign out of your Azure account and prevent hello Azure Toolkit from signing you in automatically, use hello following steps.</span></span>

1. <span data-ttu-id="2f176-147">Eclipse에서 **도구**를 클릭한 다음 **Azure**를 클릭하고 **로그아웃**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-147">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Azure 로그아웃을 위한 Eclipse 메뉴][L01]

1. <span data-ttu-id="2f176-149">Hello 때 **Azure 로그 아웃** 대화 상자가 나타나면 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-149">When hello **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![로그아웃 대화 상자][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a><span data-ttu-id="2f176-151">이미 만든 자격 증명 파일을 사용하여 Azure 계정에 자동으로 로그인</span><span class="sxs-lookup"><span data-stu-id="2f176-151">Signing into your Azure account automatically using a credentials file which you have already created</span></span>

<span data-ttu-id="2f176-152">Eclipse를 사용 하는 경우 로그 아웃 Azure tooreconfigure hello Azure 도구 키트에 Eclipse toouse 자격 증명 파일을 Azure 계정을 사용자로 자동으로 서명할 수 전에 만든 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-152">If you sign out of Azure when you are using Eclipse, you will need tooreconfigure hello Azure Toolkit for Eclipse toouse a credentials file which have created before you can automatically sign into your Azure acccount.</span></span> <span data-ttu-id="2f176-153">hello 다음 단계는 과정을 단계별로 hello Azure 도구 키트 toouse 구성 기존 자격 증명 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-153">hello following steps will walk you through configuring hello Azure Toolkit toouse an existing credentials file.</span></span>

1. <span data-ttu-id="2f176-154">Eclipse로 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-154">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="2f176-155">**도구**를 클릭한 다음 **Azure**를 클릭하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-155">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Azure 로그인을 위한 Eclipse 메뉴][A01]

1. <span data-ttu-id="2f176-157">Hello 때 **Azure 로그인** 선택 대화 상자가 나타나면 **자동**, 클릭 하 고 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-157">When hello **Azure Sign In** dialog box appears, select **Automated**, and then click **Browse**.</span></span>

   ![로그인 대화 상자][A02]

1. <span data-ttu-id="2f176-159">Hello 때 **인증 파일 선택** 앞에서 만든 자격 증명 파일을 선택 하 고 클릭 한 다음 대화 상자가 나타나면 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-159">When hello **Select Authenticated File** dialog box appears, select a credentials file which you created earlier, and then click **Select**.</span></span>

   ![로그인 대화 상자][A08]

1. <span data-ttu-id="2f176-161">Hello 때 **Azure 로그인** 대화 상자가 나타나면 클릭 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-161">When hello **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Azure 로그인 대화 상자][A06]

1. <span data-ttu-id="2f176-163">Hello 때 **구독 선택** 대화 상자가 나타나면 선택 hello 구독 toouse를 원하고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-163">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![구독 선택 대화 상자 관리][A07]

## <a name="see-also"></a><span data-ttu-id="2f176-165">참고 항목</span><span class="sxs-lookup"><span data-stu-id="2f176-165">See Also</span></span>
<span data-ttu-id="2f176-166">Java Ide에 대 한 hello Azure 도구 키트에 대 한 자세한 내용은 hello 다음 링크 참조:</span><span class="sxs-lookup"><span data-stu-id="2f176-166">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="2f176-167">[Eclipse용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="2f176-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="2f176-168">[Hello Azure Toolkit for Eclipse에서 새로운 이란]</span><span class="sxs-lookup"><span data-stu-id="2f176-168">[What's New in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="2f176-169">[Hello Eclipse 용 Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="2f176-169">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="2f176-170">*Azure Toolkit for Eclipse (이 문서의 내용) hello에 대 한 지침에 로그인*</span><span class="sxs-lookup"><span data-stu-id="2f176-170">*Sign In Instructions for hello Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="2f176-171">[Eclipse에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="2f176-171">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="2f176-172">[IntelliJ용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="2f176-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="2f176-173">[Hello IntelliJ 용 Azure 도구 키트에서 새로운 이란]</span><span class="sxs-lookup"><span data-stu-id="2f176-173">[What's New in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="2f176-174">[IntelliJ 용 hello Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="2f176-174">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="2f176-175">[Hello IntelliJ 용 Azure 도구 키트에 대 한 지침에 로그인]</span><span class="sxs-lookup"><span data-stu-id="2f176-175">[Sign In Instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="2f176-176">[IntelliJ에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="2f176-176">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="2f176-177">Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터] 및 hello [Visual Studio Team Services에 대 한 Java 도구]합니다.</span><span class="sxs-lookup"><span data-stu-id="2f176-177">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

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
