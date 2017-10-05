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
# <a name="azure-sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="a2639-103">Eclipse용 Azure 도구 키트에 대한 Azure 로그인 지침</span><span class="sxs-lookup"><span data-stu-id="a2639-103">Azure Sign In Instructions for the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="a2639-104">Eclipse용 Azure 도구 키트는 Azure 계정에 로그인하는 두 가지 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-104">The Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  * <span data-ttu-id="a2639-105">**대화형** - 이 방법을 사용하는 경우 Azure 계정에 로그인할 때마다 Azure 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-105">**Interactive** - when you are using this method, you will enter your Azure credentials each time you sign into your Azure account.</span></span>
  * <span data-ttu-id="a2639-106">**자동** - 이 방법을 사용하는 경우 서비스 주체 데이터를 포함하는 자격 증명 파일을 만든 다음 해당 자격 증명 파일을 사용하여 Azure 계정에 자동으로 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-106">**Automated** - when you are using this method, you will create a credentials file which contains your service principal data, after which you can use the credentials file to automatically sign into your Azure account.</span></span>

<span data-ttu-id="a2639-107">다음 섹션의 단계에서는 각 방법을 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-107">The steps in the following sections will describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a><span data-ttu-id="a2639-108">대화형으로 Azure 계정에 로그인</span><span class="sxs-lookup"><span data-stu-id="a2639-108">Signing into your Azure account interactively</span></span>

<span data-ttu-id="a2639-109">다음 단계에서는 Azure 자격 증명을 수동으로 입력하여 Azure에 로그인하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-109">The following steps will illustrate how to sign into Azure by manually entering your Azure credentials.</span></span>

1. <span data-ttu-id="a2639-110">Eclipse로 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-110">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="a2639-111">**도구**를 클릭한 다음 **Azure**를 클릭하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-111">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Azure 로그인을 위한 Eclipse 메뉴][I01]

1. <span data-ttu-id="a2639-113">**Azure 로그인** 대화 상자가 나타나면 **대화형**을 선택한 다음 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-113">When the **Azure Sign In** dialog box appears, select **Interactive**, and then click **Sign In**.</span></span>

   ![로그인 대화 상자][I02]

1. <span data-ttu-id="a2639-115">**Azure 로그인** 대화 상자가 나타나면 Azure 자격 증명을 입력하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-115">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Azure 로그인 대화 상자][I03]

1. <span data-ttu-id="a2639-117">**구독 선택** 대화 상자가 나타나면 사용하려는 구독을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-117">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![구독 선택 대화 상자 관리][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a><span data-ttu-id="a2639-119">대화형으로 로그인되었을 때 Azure 계정에서 로그아웃</span><span class="sxs-lookup"><span data-stu-id="a2639-119">Signing out of your Azure account when you signed in interactively</span></span>

<span data-ttu-id="a2639-120">이전 섹션의 단계를 구성한 후에는 Eclipse를 다시 시작할 때마다 Azure 계정에서 자동으로 로그아웃됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-120">After you have configured the steps in the previous section, you will automatically signed out of your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="a2639-121">그러나 Eclipse를 다시 시작하지 않고 Azure 계정에서 로그아웃하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-121">However, if you want to sign out of your Azure account without restarting Eclipse, use the following steps.</span></span>

1. <span data-ttu-id="a2639-122">Eclipse에서 **도구**를 클릭한 다음 **Azure**를 클릭하고 **로그아웃**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-122">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Azure 로그아웃을 위한 Eclipse 메뉴][L01]

1. <span data-ttu-id="a2639-124">**Azure 로그아웃** 대화 상자가 나타나면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-124">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![로그아웃 대화 상자][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-to-use-in-the-future"></a><span data-ttu-id="a2639-126">Azure 계정에 자동으로 로그인 및 나중에 사용할 자격 증명 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="a2639-126">Signing into your Azure account automatically and creating a credentials file to use in the future</span></span>

<span data-ttu-id="a2639-127">다음 단계에서는 서비스 주체 데이터를 포함하는 자격 증명 파일을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-127">The following steps will walk you through creating a credentials file which contains your service principal data.</span></span> <span data-ttu-id="a2639-128">이러한 단계를 완료한 후 Eclipse에서는 사용자가 프로젝트를 열 때마다 해당 자격 증명 파일을 자동으로 사용해서 Azure에 자동으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-128">Once you have completed these steps, Eclipse will automatically use the credentials file to automatically sign you into Azure each time you open your project.</span></span>

1. <span data-ttu-id="a2639-129">Eclipse로 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-129">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="a2639-130">**도구**를 클릭한 다음 **Azure**를 클릭하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-130">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Azure 로그인을 위한 Eclipse 메뉴][A01]

1. <span data-ttu-id="a2639-132">**Azure 로그인** 대화 상자가 나타나면 **자동**을 선택한 다음 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-132">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **New**.</span></span>

   ![로그인 대화 상자][A02]

1. <span data-ttu-id="a2639-134">**Azure 로그인** 대화 상자가 나타나면 Azure 자격 증명을 입력하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-134">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Azure 로그인 대화 상자][A03]

1. <span data-ttu-id="a2639-136">**인증 파일 만들기** 대화 상자가 나타나면 사용할 구독을 선택하고 대상 디렉터리를 선택한 후 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-136">When the **Create authentication files** dialog box appears, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Azure 로그인 대화 상자][A04]

1. <span data-ttu-id="a2639-138">**서비스 주체 만들기 상태** 대화 상자가 표시됩니다. 파일이 성공적으로 만들어진 후에 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-138">The **Service Principal Creatation Status** dialog box will be displayed, and after your files have been created successfully, click **OK**.</span></span>

   ![서비스 주체 만들기 상태 대화 상자][A05]

1. <span data-ttu-id="a2639-140">**Azure 로그인** 대화 상자가 나타나면 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-140">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Azure 로그인 대화 상자][A06]

1. <span data-ttu-id="a2639-142">**구독 선택** 대화 상자가 나타나면 사용하려는 구독을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-142">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![구독 선택 대화 상자 관리][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a><span data-ttu-id="a2639-144">자동으로 로그인되었을 때 Azure 계정에서 로그아웃</span><span class="sxs-lookup"><span data-stu-id="a2639-144">Signing out of your Azure account when you signed in automatically</span></span>

<span data-ttu-id="a2639-145">이전 섹션의 단계를 구성한 후에는 Eclipse를 다시 시작할 때마다 Azure 도구 키트를 통해 Azure 계정에서 자동으로 로그인됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-145">After you have configured the steps in the previous section, the Azure Toolkit will automatically sign you into your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="a2639-146">그러나 Azure 계정에서 로그아웃하고 Azure 도구 키트를 통해 자동으로 로그인되지 않게 하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-146">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, use the following steps.</span></span>

1. <span data-ttu-id="a2639-147">Eclipse에서 **도구**를 클릭한 다음 **Azure**를 클릭하고 **로그아웃**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-147">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Azure 로그아웃을 위한 Eclipse 메뉴][L01]

1. <span data-ttu-id="a2639-149">**Azure 로그아웃** 대화 상자가 나타나면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-149">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![로그아웃 대화 상자][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a><span data-ttu-id="a2639-151">이미 만든 자격 증명 파일을 사용하여 Azure 계정에 자동으로 로그인</span><span class="sxs-lookup"><span data-stu-id="a2639-151">Signing into your Azure account automatically using a credentials file which you have already created</span></span>

<span data-ttu-id="a2639-152">Eclipse를 사용할 때 Azure에서 로그아웃된 경우 Azure 계정으로 자동으로 로그인하려면 만든 자격 증명을 사용하도록 Eclipse용 Azure 도구 키트를 다시 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-152">If you sign out of Azure when you are using Eclipse, you will need to reconfigure the Azure Toolkit for Eclipse to use a credentials file which have created before you can automatically sign into your Azure acccount.</span></span> <span data-ttu-id="a2639-153">다음 단계에서는 기존 자격 증명 파일을 사용하도록 Azure 도구 키트를 구성하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-153">The following steps will walk you through configuring the Azure Toolkit to use an existing credentials file.</span></span>

1. <span data-ttu-id="a2639-154">Eclipse로 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-154">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="a2639-155">**도구**를 클릭한 다음 **Azure**를 클릭하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-155">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Azure 로그인을 위한 Eclipse 메뉴][A01]

1. <span data-ttu-id="a2639-157">**Azure 로그인** 대화 상자가 나타나면 **자동**을 선택한 다음 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-157">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **Browse**.</span></span>

   ![로그인 대화 상자][A02]

1. <span data-ttu-id="a2639-159">**인증된 파일 선택** 대화 상자가 나타나면 이전에 만든 자격 증명 파일을 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-159">When the **Select Authenticated File** dialog box appears, select a credentials file which you created earlier, and then click **Select**.</span></span>

   ![로그인 대화 상자][A08]

1. <span data-ttu-id="a2639-161">**Azure 로그인** 대화 상자가 나타나면 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-161">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Azure 로그인 대화 상자][A06]

1. <span data-ttu-id="a2639-163">**구독 선택** 대화 상자가 나타나면 사용하려는 구독을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2639-163">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![구독 선택 대화 상자 관리][A07]

## <a name="see-also"></a><span data-ttu-id="a2639-165">참고 항목</span><span class="sxs-lookup"><span data-stu-id="a2639-165">See Also</span></span>
<span data-ttu-id="a2639-166">Java IDE용 Azure 도구 키트에 대한 자세한 내용은 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a2639-166">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="a2639-167">[Eclipse용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="a2639-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="a2639-168">[Eclipse용 Azure 도구 키트의 새로운 기능]</span><span class="sxs-lookup"><span data-stu-id="a2639-168">[What's New in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="a2639-169">[Eclipse용 Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="a2639-169">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="a2639-170">*Eclipse용 Azure 도구 키트에 대한 로그인 지침(이 문서)*</span><span class="sxs-lookup"><span data-stu-id="a2639-170">*Sign In Instructions for the Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="a2639-171">[Eclipse에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="a2639-171">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="a2639-172">[IntelliJ용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="a2639-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="a2639-173">[IntelliJ용 Azure 도구 키트의 새로운 기능]</span><span class="sxs-lookup"><span data-stu-id="a2639-173">[What's New in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="a2639-174">[IntelliJ용 Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="a2639-174">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="a2639-175">[IntelliJ용 Azure 도구 키트에 대한 로그인 지침]</span><span class="sxs-lookup"><span data-stu-id="a2639-175">[Sign In Instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="a2639-176">[IntelliJ에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="a2639-176">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="a2639-177">Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Azure Java 개발자 센터] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a2639-177">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="a2639-178">[Eclipse용 Azure 도구 키트]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="a2639-178">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="a2639-179">[IntelliJ용 Azure 도구 키트]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="a2639-179">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="a2639-180">[Eclipse에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="a2639-180">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="a2639-181">[IntelliJ에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="a2639-181">[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="a2639-182">[Eclipse용 Azure 도구 키트 설치]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="a2639-182">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="a2639-183">[IntelliJ용 Azure 도구 키트 설치]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="a2639-183">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
<span data-ttu-id="a2639-184">[IntelliJ용 Azure 도구 키트에 대한 로그인 지침]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="a2639-184">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="a2639-185">[Eclipse용 Azure 도구 키트의 새로운 기능]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="a2639-185">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="a2639-186">[IntelliJ용 Azure 도구 키트의 새로운 기능]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="a2639-186">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="a2639-187">[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="a2639-187">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="a2639-188">[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="a2639-188">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

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
