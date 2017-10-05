---
title: "IntelliJ용 Azure 도구 키트 설치 | Microsoft Docs"
description: "IntelliJ IDEA용 Azure 도구 키트를 설치하는 방법을 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: c6817c7b-f28c-4c06-8216-41c7a8117de3
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: bf11a8580500f78c4a96a02953f221501eeffe6c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="installing-the-azure-toolkit-for-intellij"></a><span data-ttu-id="b7e64-103">IntelliJ용 Azure 도구 키트 설치</span><span class="sxs-lookup"><span data-stu-id="b7e64-103">Installing the Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="b7e64-104">IntelliJ용 Azure 도구 키트는 IntelliJ IDEA 개발 환경에서 Azure 응용 프로그램을 쉽게 작성, 개발, 테스트 및 배포할 수 있는 템플릿과 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e64-104">The Azure Toolkit for IntelliJ provides templates and functionality that allow you to easily create, develop, test, and deploy Azure applications using the IntelliJ IDEA development environment.</span></span> <span data-ttu-id="b7e64-105">IntelliJ용 Azure 도구 키트는 다음 URL에 있는 GitHub의 프로젝트 사이트를 통해 MIT 라이선스에 따라 소스 코드 사용이 허가된 오픈 소스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="b7e64-105">The Azure Toolkit for IntelliJ is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span>

<span data-ttu-id="b7e64-106"><https://github.com/microsoft/azure-tools-for-java></span><span class="sxs-lookup"><span data-stu-id="b7e64-106"><https://github.com/microsoft/azure-tools-for-java></span></span>

<span data-ttu-id="b7e64-107">IntelliJ용 Azure 도구 키트는 설정 대화 상자와 시작 화면의 구성 메뉴에서 설치할 수 있습니다. 다음 단계에서는 두 설치 방법을 모두 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e64-107">There are two methods of installing the Azure Toolkit for IntelliJ, from the Settings dialog box and from the Configure menu on the start screen; both installation methods will be demonstrated in the following steps.</span></span>

[!INCLUDE [azure-toolkit-for-IntelliJ-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-settings-dialog-box"></a><span data-ttu-id="b7e64-108">설정 대화 상자에서 IntelliJ용 Azure 도구 키트를 설치하려면</span><span class="sxs-lookup"><span data-stu-id="b7e64-108">To install the Azure Toolkit for IntelliJ from the settings dialog box</span></span>
1. <span data-ttu-id="b7e64-109">IntelliJ IDEA를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e64-109">Start IntelliJ IDEA.</span></span>
2. <span data-ttu-id="b7e64-110">IntelliJ IDEA가 열리면 **File**을 클릭한 다음 **Settings**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e64-110">When the IntelliJ IDEA opens, click **File**, then click **Settings**.</span></span>
   
    ![IntelliJ IDEA Settings 대화 상자 열기][01a]
3. <span data-ttu-id="b7e64-112">설정 대화 상자에서 **Plugins**를 클릭하고 **Browse repositories**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e64-112">In the Settings dialog box, click **Plugins**, and then click **Browse repositories**.</span></span>
   
    ![IntelliJ IDEA Settings 대화 상자][02a]
4. <span data-ttu-id="b7e64-114">**Browse repositories** 대화 상자에서 검색 상자에 "Azure"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e64-114">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="b7e64-115">**IntelliJ용 Azure 도구 키트**를 강조 표시하고 **Install**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e64-115">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
    ![IntelliJ용 Azure 도구 키트 검색][03]
   
    <span data-ttu-id="b7e64-117">IntelliJ IDEA 대화 상자에서 설치 진행 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7e64-117">IntelliJ IDEA will display the installation progress in a dialog box.</span></span>
   
    ![설치 진행률][04]
5. <span data-ttu-id="b7e64-119">설치가 완료되면 **Restart IntelliJ IDEA**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e64-119">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
    ![Restart IntelliJ IDEA][05]
6. <span data-ttu-id="b7e64-121">**OK** 를 클릭하여 Settings 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b7e64-121">Click **OK** to close the Settings dialog box.</span></span>
   
    ![IntelliJ IDEA Settings 대화 상자 닫기][06]
7. <span data-ttu-id="b7e64-123">IntelliJ IDEA를 다시 시작할지 또는 연기할지 묻는 메시지가 나타나면 **Restart**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e64-123">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
    ![Restart IntelliJ IDEA][07]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-start-screen"></a><span data-ttu-id="b7e64-125">시작 화면에서 IntelliJ용 Azure 도구 키트를 설치하려면</span><span class="sxs-lookup"><span data-stu-id="b7e64-125">To install the Azure Toolkit for IntelliJ from the start screen</span></span>
1. <span data-ttu-id="b7e64-126">IntelliJ IDEA를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e64-126">Start IntelliJ IDEA.</span></span>
2. <span data-ttu-id="b7e64-127">IntelliJ IDEA 시작 화면이 나타나면 **Configure**를 클릭하고 **Plugins**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e64-127">When the IntelliJ IDEA start screen appears, click **Configure**, then click **Plugins**.</span></span>
   
    ![IntelliJ IDEA 플러그 인 설치][01b]
3. <span data-ttu-id="b7e64-129">**Plugins** 대화 상자에서 **Browse repositories**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e64-129">In the **Plugins** dialog box, click **Browse repositories**.</span></span>
   
    ![IntelliJ 아이디어 플러그 인 저장소 찾아보기][02b]
4. <span data-ttu-id="b7e64-131">**Browse repositories** 대화 상자에서 검색 상자에 "Azure"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e64-131">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="b7e64-132">**IntelliJ용 Azure 도구 키트**를 강조 표시하고 **Install**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e64-132">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
    ![IntelliJ용 Azure 도구 키트 검색][03]
   
    <span data-ttu-id="b7e64-134">IntelliJ IDEA 대화 상자에서 설치 진행 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7e64-134">IntelliJ IDEA will display the installation progress in a dialog box.</span></span>
   
    ![설치 진행률][04]
5. <span data-ttu-id="b7e64-136">설치가 완료되면 **Restart IntelliJ IDEA**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e64-136">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
    ![Restart IntelliJ IDEA][05]
6. <span data-ttu-id="b7e64-138">IntelliJ IDEA를 다시 시작할지 또는 연기할지 묻는 메시지가 나타나면 **Restart**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e64-138">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
    ![Restart IntelliJ IDEA][07]

## <a name="see-also"></a><span data-ttu-id="b7e64-140">참고 항목</span><span class="sxs-lookup"><span data-stu-id="b7e64-140">See Also</span></span>
<span data-ttu-id="b7e64-141">Java IDE용 Azure 도구 키트에 대한 자세한 내용은 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7e64-141">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="b7e64-142">[Eclipse용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="b7e64-142">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b7e64-143">[Eclipse용 Azure 도구 키트의 새로운 기능]</span><span class="sxs-lookup"><span data-stu-id="b7e64-143">[What's New in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b7e64-144">[Eclipse용 Azure 도구 키트 설치]</span><span class="sxs-lookup"><span data-stu-id="b7e64-144">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b7e64-145">[Eclipse용 Azure 도구 키트에 대한 로그인 지침]</span><span class="sxs-lookup"><span data-stu-id="b7e64-145">[Sign In Instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b7e64-146">[Eclipse에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="b7e64-146">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="b7e64-147">[IntelliJ용 Azure 도구 키트]</span><span class="sxs-lookup"><span data-stu-id="b7e64-147">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b7e64-148">[IntelliJ용 Azure 도구 키트의 새로운 기능]</span><span class="sxs-lookup"><span data-stu-id="b7e64-148">[What's New in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b7e64-149">*IntelliJ용 Azure 도구 키트 설치(이 문서)*</span><span class="sxs-lookup"><span data-stu-id="b7e64-149">*Installing the Azure Toolkit for IntelliJ (This Article)*</span></span>
  * <span data-ttu-id="b7e64-150">[IntelliJ용 Azure 도구 키트에 대한 로그인 지침]</span><span class="sxs-lookup"><span data-stu-id="b7e64-150">[Sign In Instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b7e64-151">[IntelliJ에서 Azure용 Hello World 웹앱 만들기]</span><span class="sxs-lookup"><span data-stu-id="b7e64-151">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="b7e64-152">Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Azure Java 개발자 센터]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7e64-152">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="b7e64-153">[Eclipse용 Azure 도구 키트]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="b7e64-153">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="b7e64-154">[IntelliJ용 Azure 도구 키트]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="b7e64-154">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="b7e64-155">[Eclipse에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="b7e64-155">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="b7e64-156">[IntelliJ에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="b7e64-156">[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="b7e64-157">[Eclipse용 Azure 도구 키트 설치]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="b7e64-157">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
<span data-ttu-id="b7e64-158">[Eclipse용 Azure 도구 키트에 대한 로그인 지침]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="b7e64-158">[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="b7e64-159">[IntelliJ용 Azure 도구 키트에 대한 로그인 지침]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="b7e64-159">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="b7e64-160">[Eclipse용 Azure 도구 키트의 새로운 기능]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="b7e64-160">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="b7e64-161">[IntelliJ용 Azure 도구 키트의 새로운 기능]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="b7e64-161">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="b7e64-162">[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="b7e64-162">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>

<!-- IMG List -->

[01a]: ./media/azure-toolkit-for-intellij-installation/01-intellij-file-settings.png
[01b]: ./media/azure-toolkit-for-intellij-installation/01-intellij-configure-dropdown.png
[02a]: ./media/azure-toolkit-for-intellij-installation/02-intellij-settings-dialog.png
[02b]: ./media/azure-toolkit-for-intellij-installation/02-intellij-plugins-dialog.png
[03]: ./media/azure-toolkit-for-intellij-installation/03-intellij-browse-repositories.png
[04]: ./media/azure-toolkit-for-intellij-installation/04-install-progress.png
[05]: ./media/azure-toolkit-for-intellij-installation/05-restart-intellij.png
[06]: ./media/azure-toolkit-for-intellij-installation/06-intellij-settings-dialog.png
[07]: ./media/azure-toolkit-for-intellij-installation/07-restart-intellij.png
