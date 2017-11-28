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
# <a name="sign-in-instructions-for-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="4c680-103">로그인에 대 한 지침 Azure 도구 키트 hello IntelliJ</span><span class="sxs-lookup"><span data-stu-id="4c680-103">Sign-in instructions for hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="4c680-104">hello IntelliJ 용 Azure 도구 키트 tooyour Azure 계정에에서 로그인 하는 두 가지 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-104">hello Azure Toolkit for IntelliJ provides two methods for signing in tooyour Azure account:</span></span>

  * <span data-ttu-id="4c680-105">**대화형**: tooyour Azure 계정에에서 Azure 자격 증명 로그인 할 때마다 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-105">**Interactive**: You enter your Azure credentials each time you sign in tooyour Azure account.</span></span>
  * <span data-ttu-id="4c680-106">**자동화 된**: tooyour Azure 계정에에서 tooautomatically 기호를 사용할 수 있는 자격 증명 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-106">**Automated**: You create a credentials file that you can use tooautomatically sign in tooyour Azure account.</span></span>

<span data-ttu-id="4c680-107">hello 다음 섹션에서는 설명 방법을 toouse 각 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-107">hello following sections describe how toouse each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-tooyour-azure-account-interactively"></a><span data-ttu-id="4c680-108">대화형 tooyour Azure 계정으로 로그인</span><span class="sxs-lookup"><span data-stu-id="4c680-108">Sign in tooyour Azure account interactively</span></span>

<span data-ttu-id="4c680-109">수동으로 Azure 자격 증명을 입력 하 여 tooAzure에 toosign 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-109">toosign in tooAzure by manually entering your Azure credentials, do hello following:</span></span>

1. <span data-ttu-id="4c680-110">IntelliJ IDEA로 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-110">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="4c680-111">클릭 **도구**, 너무 가리킨**Azure**, 클릭 하 고 **Azure 로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-111">Click **Tools**, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![hello IntelliJ Azure Sign In 명령][I01]

3. <span data-ttu-id="4c680-113">Hello에 **Azure 로그인** 창에서 **Interactive'**, 클릭 하 고 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-113">In hello **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![선택한 Interactive' 있는 hello Azure 로그인 창][I02]

4. <span data-ttu-id="4c680-115">Hello에 **Azure 로그인** Azure 자격 증명을 입력 하 고 클릭 한 다음 대화 상자가 나타나면 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-115">In hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![hello Azure 로그인 대화 상자 창][I03]

5. <span data-ttu-id="4c680-117">Hello에 **구독 선택** 대화 상자, 선택 hello 구독 toouse를 원하고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-117">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![hello 구독 선택 대화 상자][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="4c680-119">대화형으로 로그인한 후 Azure 계정에서 로그아웃</span><span class="sxs-lookup"><span data-stu-id="4c680-119">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="4c680-120">계정을 구성한 경우 hello 이전 단계를 사용 하 여 하면 자동으로 로그 아웃 IntelliJ 아이디어 다시 시작할 때마다 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="4c680-120">After you have configured your account by using hello preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="4c680-121">그러나 Azure 계정 toosign 하려는 경우 *없이* 다음 hello 수행 IntelliJ 아이디어를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-121">However, if you want toosign out of your Azure account *without* restarting IntelliJ IDEA, do hello following.</span></span>

1. <span data-ttu-id="4c680-122">Hello에 IntelliJ 아이디어에 **도구** 메뉴 너무 가리킨**Azure**, 클릭 하 고 **Azure 로그 아웃**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-122">In IntelliJ IDEA, on hello **Tools** menu, point too**Azure**, and then click **Azure Sign Out**.</span></span>

   ![hello IntelliJ Azure 로그 아웃 명령][L01]

2. <span data-ttu-id="4c680-124">Hello에 **Azure 로그 아웃** 확인 창이 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-124">In hello **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![확인 창 hello Azure 로그 아웃][L02]

## <a name="sign-in-tooyour-azure-account-automatically"></a><span data-ttu-id="4c680-126">Tooyour Azure 계정에에서 자동으로 로그인</span><span class="sxs-lookup"><span data-stu-id="4c680-126">Sign in tooyour Azure account automatically</span></span>

<span data-ttu-id="4c680-127">이 섹션에서는 서비스 주체 데이터를 포함하는 자격 증명 파일을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-127">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="4c680-128">이 프로세스를 완료 한 후 Eclipse 사용 하 여 hello 자격 증명 파일 tooautomatically 기호 때마다 각 tooAzure에서 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-128">After you have completed this process, Eclipse uses hello credentials file tooautomatically sign you in tooAzure each time you open your project.</span></span>

1. <span data-ttu-id="4c680-129">IntelliJ IDEA로 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-129">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="4c680-130">Hello에 **도구** 메뉴 너무 가리킨**Azure**, 클릭 하 고 **Azure 로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-130">On hello **Tools** menu, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![hello IntelliJ Azure Sign In 명령][A01]

3. <span data-ttu-id="4c680-132">Hello에 **Azure 로그인** 창에서 **자동**, 클릭 하 고 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-132">In hello **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![자동 선택 된 hello Azure 로그인 창][A02]

4. <span data-ttu-id="4c680-134">Hello에 **Azure 로그인 대화 상자** 창 Azure 자격 증명을 입력 한 다음 클릭 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-134">In hello **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![hello Azure 로그인 대화 상자 창][A03]

5. <span data-ttu-id="4c680-136">Hello에 **인증 파일 만들기** 창, 선택 hello 구독 toouse 원하는, 대상 디렉터리를 선택한 다음 클릭 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-136">In hello **Create Authentication Files** window, select hello subscriptions that you want toouse, choose your destination directory, and then click **Start**.</span></span>

   ![hello 인증 파일 만들기 창][A04]

6. <span data-ttu-id="4c680-138">Hello에 **서비스 사용자 만들기 상태** 대화 상자에서 파일 성공적으로 만든 후 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-138">In hello **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![hello 서비스 사용자 만들기 상태 대화 상자][A05]

7. <span data-ttu-id="4c680-140">Hello에 **Azure 로그인** 창 클릭 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-140">In hello **Azure Sign In** window, click **Sign in**.</span></span>

   ![Azure 로그인 대화 상자][A06]

8. <span data-ttu-id="4c680-142">Hello에 **구독 선택** 대화 상자, 선택 hello 구독 toouse를 원하고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-142">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![hello 구독 선택 대화 상자][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="4c680-144">자동으로 로그인한 후 Azure 계정에서 로그아웃</span><span class="sxs-lookup"><span data-stu-id="4c680-144">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="4c680-145">계정을 구성한 경우 hello 이전 단계를 사용 하 여 hello Azure 도구 키트 자동으로 로그인 tooyour IntelliJ 아이디어 다시 시작할 때마다 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="4c680-145">After you have configured your account by using hello preceding steps, hello Azure Toolkit automatically signs you in tooyour Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="4c680-146">그러나 Toosign의 Azure 계정 및 hello Azure 도구 키트를 방지 합니다. 다음 hello 수행 자동 로그인에서:</span><span class="sxs-lookup"><span data-stu-id="4c680-146">However, toosign out of your Azure account and prevent hello Azure Toolkit from signing you in automatically, do hello following:</span></span>

1. <span data-ttu-id="4c680-147">Hello에 IntelliJ 아이디어에 **도구** 메뉴 너무 가리킨**Azure**, 클릭 하 고 **Azure 로그 아웃**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-147">In IntelliJ IDEA, on hello **Tools** menu, point too**Azure**, and then click **Azure Sign Out**.</span></span>

   ![hello IntelliJ Azure 로그 아웃 명령][L01]

2. <span data-ttu-id="4c680-149">Hello에 **Azure 로그 아웃** 확인 창이 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-149">In hello **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![확인 창 hello Azure 로그 아웃][L03]

## <a name="sign-in-tooyour-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="4c680-151">계정에에서 로그인 tooyour Azure 자동으로 기존 자격 증명 파일을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="4c680-151">Sign in tooyour Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="4c680-152">IntelliJ 아이디어를 사용 하는 경우 Azure 계정에서 로그인 하는 경우에 기존 자격 증명 파일 tooautomatically 부호 toohello 계정에 다시 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-152">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file tooautomatically sign back in toohello account.</span></span> <span data-ttu-id="4c680-153">tooconfigure hello Azure 도구 키트에 Eclipse toouse 기존 자격 증명 파일을 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-153">tooconfigure hello Azure Toolkit for Eclipse toouse an existing credentials file, do hello following:</span></span>

1. <span data-ttu-id="4c680-154">IntelliJ IDEA로 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-154">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="4c680-155">Hello에 **도구** 메뉴 너무 가리킨**Azure**, 클릭 하 고 **Azure 로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-155">On hello **Tools** menu, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![hello IntelliJ Azure Sign In 명령][A01]

3. <span data-ttu-id="4c680-157">Hello에 **Azure 로그인** 창에서 **자동**, 클릭 하 고 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-157">In hello **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![자동 선택 된 hello Azure 로그인 창][A02]

4. <span data-ttu-id="4c680-159">Hello에 **인증 파일 선택** 대화 상자에서 이전에 만든된 자격 증명 파일을 선택한 다음 클릭 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-159">In hello **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![hello 인증 파일 선택 대화 상자][A08]

5. <span data-ttu-id="4c680-161">Hello에 **Azure 로그인** 창 클릭 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-161">In hello **Azure Sign In** window, click **Sign in**.</span></span>

   ![자동 선택 된 hello Azure 로그인 창][A06]

6. <span data-ttu-id="4c680-163">Hello에 **구독 선택** 대화 상자, 선택 hello 구독 toouse를 원하고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-163">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![hello 구독 선택 대화 상자][A07]

## <a name="next-steps"></a><span data-ttu-id="4c680-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4c680-165">Next steps</span></span>
<span data-ttu-id="4c680-166">Java Ide에 대 한 hello Azure 도구 키트에 대 한 자세한 내용은 hello 다음 링크 참조:</span><span class="sxs-lookup"><span data-stu-id="4c680-166">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="4c680-167">[Eclipse용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="4c680-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="4c680-168">[Hello Eclipse 용 Azure 도구 키트의에서 새로운 기능]</span><span class="sxs-lookup"><span data-stu-id="4c680-168">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="4c680-169">[Hello Eclipse 용 Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="4c680-169">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="4c680-170">[Eclipse 용 Azure 도구 키트 hello에 대 한 로그인 지침]</span><span class="sxs-lookup"><span data-stu-id="4c680-170">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="4c680-171">[Eclipse에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="4c680-171">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="4c680-172">[IntelliJ용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="4c680-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="4c680-173">[Hello IntelliJ 용 Azure 도구 키트의에서 새로운 기능]</span><span class="sxs-lookup"><span data-stu-id="4c680-173">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="4c680-174">[IntelliJ 용 hello Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="4c680-174">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="4c680-175">*로그인에 대 한 지침 Azure 도구 키트 hello IntelliJ* (이 문서)</span><span class="sxs-lookup"><span data-stu-id="4c680-175">*Sign-in instructions for hello Azure Toolkit for IntelliJ* (this article)</span></span>
  * <span data-ttu-id="4c680-176">[IntelliJ에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="4c680-176">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="4c680-177">Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터] 및 hello [Visual Studio Team Services에 대 한 Java 도구]합니다.</span><span class="sxs-lookup"><span data-stu-id="4c680-177">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

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
