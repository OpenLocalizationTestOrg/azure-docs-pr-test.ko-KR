---
title: "Azure IoT Suite 및 Logic Apps | Microsoft Docs"
description: "논리 앱을 비즈니스 프로세스에 대한 Azure IoT Suite에 연결하는 방법에 대한 자습서입니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4629a7af-56ca-4b21-a769-5fa18bc3ab07
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: corywink
ms.openlocfilehash: 2e7997e2a8bdeeec6083d40acb55e653f87e140b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-connect-logic-app-to-your-azure-iot-suite-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="ad16f-103">자습서: 미리 구성된 Azure IoT Suite 원격 모니터링 솔루션에 논리 앱 연결</span><span class="sxs-lookup"><span data-stu-id="ad16f-103">Tutorial: Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution</span></span>
<span data-ttu-id="ad16f-104">미리 구성된 [Microsoft Azure IoT Suite][lnk-internetofthings] 원격 모니터링 솔루션은 IoT 솔루션의 예를 보여 주는 종단 간 기능 집합으로 신속하게 시작할 수 있는 훌륭한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-104">The [Microsoft Azure IoT Suite][lnk-internetofthings] remote monitoring preconfigured solution is a great way to get started quickly with an end-to-end feature set that exemplifies an IoT solution.</span></span> <span data-ttu-id="ad16f-105">이 자습서에서는 미리 구성된 Microsoft Azure IoT Suite 원격 모니터링 솔루션에 논리 앱을 추가하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-105">This tutorial walks you through how to add Logic App to your Microsoft Azure IoT Suite remote monitoring preconfigured solution.</span></span> <span data-ttu-id="ad16f-106">이러한 단계에서는 IoT 솔루션을 비즈니스 프로세스에 연결하여 추가로 활용할 수 있는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-106">These steps demonstrate how you can take your IoT solution even further by connecting it to a business process.</span></span>

<span data-ttu-id="ad16f-107">*미리 구성된 원격 모니터링 솔루션을 프로비전하는 방법을 찾고 있는 경우 [자습서: 미리 구성된 IoT 솔루션 시작][lnk-getstarted]을 참조하세요.*</span><span class="sxs-lookup"><span data-stu-id="ad16f-107">*If you’re looking for a walkthrough on how to provision a remote monitoring preconfigured solution, see [Tutorial: Get started with the IoT preconfigured solutions][lnk-getstarted].*</span></span>

<span data-ttu-id="ad16f-108">이 자습서를 시작하기 전에 먼저 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-108">Before you start this tutorial, you should:</span></span>

* <span data-ttu-id="ad16f-109">Azure 구독에서 미리 구성된 원격 모니터링 솔루션을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-109">Provision the remote monitoring preconfigured solution in your Azure subscription.</span></span>
* <span data-ttu-id="ad16f-110">비즈니스 프로세스를 트리거하는 전자 메일을 보낼 수 있도록 SendGrid 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-110">Create a SendGrid account to enable you to send an email that triggers your business process.</span></span> <span data-ttu-id="ad16f-111">[SendGrid](https://sendgrid.com/) 에서 **무료 평가판**을 클릭하여 무료 평가판 계정을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-111">You can sign up for a free trial account at [SendGrid](https://sendgrid.com/) by clicking **Try for Free**.</span></span> <span data-ttu-id="ad16f-112">무료 평가판 계정을 등록한 후에는 SendGrid에서 메일 전송 권한을 부여하는 [API 키](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) 를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-112">After you have registered for your free trial account, you need to create an [API key](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid that grants permissions to send mail.</span></span> <span data-ttu-id="ad16f-113">이 API 키는 자습서의 뒷부분에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-113">You need this API key later in the tutorial.</span></span>

<span data-ttu-id="ad16f-114">이 자습서를 완료하려면 미리 구성된 솔루션 백 엔드에서 동작을 수정하기 위해 Visual Studio 2015 또는 Visual Studio 2017이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-114">To complete this tutorial, you need Visual Studio 2015 or Visual Studio 2017 to modify the actions in the preconfigured solution back end.</span></span>

<span data-ttu-id="ad16f-115">미리 구성된 원격 모니터링 솔루션을 이미 프로비전했다고 가정하고 [Azure Portal][lnk-azureportal]에서 해당 솔루션에 대한 리소스 그룹으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-115">Assuming you’ve already provisioned your remote monitoring preconfigured solution, navigate to the resource group for that solution in the [Azure portal][lnk-azureportal].</span></span> <span data-ttu-id="ad16f-116">리소스 그룹 이름이 원격 모니터링 솔루션을 프로비전할 때 선택한 솔루션 이름과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-116">The resource group has the same name as the solution name you chose when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="ad16f-117">리소스 그룹에서 Azure 클래식 포털에서 찾을 수 있는 Azure Active Directory 응용 프로그램을 제외하고 솔루션에 대해 프로비전된 모든 Azure 리소스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-117">In the resource group, you can see all the provisioned Azure resources for your solution except for the Azure Active Directory application that you can find in the Azure Classic Portal.</span></span> <span data-ttu-id="ad16f-118">다음 스크린샷은 미리 구성된 원격 모니터링 솔루션에 대한 예제 **리소스 그룹** 블레이드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-118">The following screenshot shows an example **Resource group** blade for a remote monitoring preconfigured solution:</span></span>

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

<span data-ttu-id="ad16f-119">시작하려면 미리 구성된 솔루션과 함께 사용할 논리 앱을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-119">To begin, set up the logic app to use with the preconfigured solution.</span></span>

## <a name="set-up-the-logic-app"></a><span data-ttu-id="ad16f-120">논리 앱 설정</span><span class="sxs-lookup"><span data-stu-id="ad16f-120">Set up the Logic App</span></span>
1. <span data-ttu-id="ad16f-121">Azure Portal의 리소스 그룹 블레이드 맨 위에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-121">Click **Add** at the top of your resource group blade in the Azure portal.</span></span>
2. <span data-ttu-id="ad16f-122">**Logic App**을 검색하여 선택한 후 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-122">Search for **Logic App**, select it and then click **Create**.</span></span>
3. <span data-ttu-id="ad16f-123">**이름**을 입력하고 원격 모니터링 솔루션을 프로비전할 때 사용한 것과 동일한 **구독** 및 **리소스 그룹**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-123">Fill out the **Name** and use the same **Subscription** and **Resource group** that you used when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="ad16f-124">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-124">Click **Create**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. <span data-ttu-id="ad16f-125">배포가 완료되면 논리 앱이 리소스 그룹에 리소스로 나열되는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-125">When your deployment completes, you can see the Logic App is listed as a resource in your resource group.</span></span>
5. <span data-ttu-id="ad16f-126">Logic App을 클릭하여 Logic App 블레이드로 이동하고 **빈 Logic App** 템플릿을 선택하여 **Logic Apps 디자이너**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-126">Click the Logic App to navigate to the Logic App blade, select the **Blank Logic App** template to open the **Logic Apps Designer**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. <span data-ttu-id="ad16f-127">**요청**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-127">Select **Request**.</span></span> <span data-ttu-id="ad16f-128">이 작업은 특정 JSON 형식 페이로드와 함께 들어오는 HTTP 요청이 트리거로 작동하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-128">This action specifies that an incoming HTTP request with a specific JSON formatted payload acts as a trigger.</span></span>
7. <span data-ttu-id="ad16f-129">다음 코드를 요청 본문 JSON 스키마에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-129">Paste the following code into the Request Body JSON Schema:</span></span>
   
    ```json
    {
      "$schema": "http://json-schema.org/draft-04/schema#",
      "id": "/",
      "properties": {
        "DeviceId": {
          "id": "DeviceId",
          "type": "string"
        },
        "measuredValue": {
          "id": "measuredValue",
          "type": "integer"
        },
        "measurementName": {
          "id": "measurementName",
          "type": "string"
        }
      },
      "required": [
        "DeviceId",
        "measurementName",
        "measuredValue"
      ],
      "type": "object"
    }
    ```
   
   > [!NOTE]
   > <span data-ttu-id="ad16f-130">논리 앱을 저장한 후 HTTP POST에 대한 URL을 복사할 수 있지만 먼저 작업을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-130">You can copy the URL for the HTTP post after you save the logic app, but first you must add an action.</span></span>
   > 
   > 
8. <span data-ttu-id="ad16f-131">수동 트리거 아래에서 **+ 새 단계**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-131">Click **+ New step** under your manual trigger.</span></span> <span data-ttu-id="ad16f-132">그런 다음 **작업 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-132">Then click **Add an action**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. <span data-ttu-id="ad16f-133">**SendGrid - 메일 보내기** 를 검색하여 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-133">Search for **SendGrid - Send email** and click it.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. <span data-ttu-id="ad16f-134">연결 이름(예: **SendGridConnection**)을 입력하고 SendGrid 계정을 설정할 때 만든 **SendGrid API 키**를 입력하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-134">Enter a name for the connection, such as **SendGridConnection**, enter the **SendGrid API Key** you created when you set up your SendGrid account, and click **Create**.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. <span data-ttu-id="ad16f-135">소유한 전자 메일 주소를 **보낸 사람** 및 **받는 사람** 필드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-135">Add email addresses you own to both the **From** and **To** fields.</span></span> <span data-ttu-id="ad16f-136">**원격 모니터링 경고[DeviceId]**를 **제목** 필드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-136">Add **Remote monitoring alert [DeviceId]** to the **Subject** field.</span></span> <span data-ttu-id="ad16f-137">**전자 메일 본문** 필드에 **장치[DeviceId]가 [measuredValue] 값과 함께 [measurementName]을 보고했습니다.**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-137">In the **Email Body** field, add **Device [DeviceId] has reported [measurementName] with value [measuredValue].**</span></span> <span data-ttu-id="ad16f-138">**이전 단계에서 데이터를 삽입할 수 있습니다** 섹션을 클릭하여 **[DeviceId]**, **[measurementName]** 및 **[measuredValue]**를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-138">You can add **[DeviceId]**, **[measurementName]**, and **[measuredValue]** by clicking in the **You can insert data from previous steps** section.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. <span data-ttu-id="ad16f-139">최상위 메뉴에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-139">Click **Save** in the top menu.</span></span>
13. <span data-ttu-id="ad16f-140">**요청** 트리거를 클릭하고 **이 URL에 대한 Http 게시** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-140">Click the **Request** trigger and copy the **Http Post to this URL** value.</span></span> <span data-ttu-id="ad16f-141">이 URL은 자습서의 뒷부분에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-141">You need this URL later in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="ad16f-142">논리 앱을 사용하면 Office 365의 작업을 비롯하여 [다양한 유형의 작업][lnk-logic-apps-actions]을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-142">Logic Apps enable you to run [many different types of action][lnk-logic-apps-actions] including actions in Office 365.</span></span> 
> 
> 

## <a name="set-up-the-eventprocessor-web-job"></a><span data-ttu-id="ad16f-143">EventProcessor 웹 작업 설정</span><span class="sxs-lookup"><span data-stu-id="ad16f-143">Set up the EventProcessor Web Job</span></span>
<span data-ttu-id="ad16f-144">이 섹션에서는 미리 구성된 솔루션을 만든 논리 앱에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-144">In this section, you connect your preconfigured solution to the Logic App you created.</span></span> <span data-ttu-id="ad16f-145">이 작업을 완료하려면 URL을 추가하여 장치 센서 값이 임계값을 초과할 때 발생하는 작업에 논리 앱을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-145">To complete this task, you add the URL to trigger the Logic App to the action that fires when a device sensor value exceeds a threshold.</span></span>

1. <span data-ttu-id="ad16f-146">git 클라이언트를 사용하여 최신 버전의 [azure-iot-remote-monitoring github 리포지토리][lnk-rmgithub]를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-146">Use your git client to clone the latest version of the [azure-iot-remote-monitoring github repository][lnk-rmgithub].</span></span> <span data-ttu-id="ad16f-147">예:</span><span class="sxs-lookup"><span data-stu-id="ad16f-147">For example:</span></span>
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. <span data-ttu-id="ad16f-148">Visual Studio에서 리포지토리의 로컬 복사본에서 **RemoteMonitoring.sln**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-148">In Visual Studio, open the **RemoteMonitoring.sln** from the local copy of the repository.</span></span>
3. <span data-ttu-id="ad16f-149">**Infrastructure\\Repository** 폴더에서 **ActionRepository.cs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-149">Open the **ActionRepository.cs** file in the **Infrastructure\\Repository** folder.</span></span>
4. <span data-ttu-id="ad16f-150">다음과 같이 **actionIds** 사전을 Logic App에서 기록한 **이 URL에 대한 Http 게시**로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-150">Update the **actionIds** dictionary with the **Http Post to this URL** you noted from your Logic App as follows:</span></span>
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post to this URL>" },
        { "Raise Alarm", "<Http Post to this URL>" }
    };
    ```
5. <span data-ttu-id="ad16f-151">변경 내용을 솔루션에 저장하고 Visual Studio를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-151">Save the changes in solution and exit Visual Studio.</span></span>

## <a name="deploy-from-the-command-line"></a><span data-ttu-id="ad16f-152">명령줄에서 배포</span><span class="sxs-lookup"><span data-stu-id="ad16f-152">Deploy from the command line</span></span>
<span data-ttu-id="ad16f-153">이 섹션에서는 Azure에서 현재 실행 중인 버전을 대체하도록 원격 모니터링 솔루션의 업데이트된 버전을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-153">In this section, you deploy your updated version of the remote monitoring solution to replace the version currently running in Azure.</span></span>

1. <span data-ttu-id="ad16f-154">[개발 설정][lnk-devsetup] 지침에 따라 배포 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-154">Following the [dev set-up][lnk-devsetup] instructions to set up your environment for deployment.</span></span>
2. <span data-ttu-id="ad16f-155">로컬로 배포하려면 [로컬 배포][lnk-localdeploy] 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-155">To deploy locally, follow the [local deployment][lnk-localdeploy] instructions.</span></span>
3. <span data-ttu-id="ad16f-156">클라우드로 배포하고 기존 클라우드 배포를 업데이트하려면 [클라우드 배포][lnk-clouddeploy] 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-156">To deploy to the cloud and update your existing cloud deployment, follow the [cloud deployment][lnk-clouddeploy] instructions.</span></span> <span data-ttu-id="ad16f-157">원래 배포의 이름을 배포 이름으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-157">Use the name of your original deployment as the deployment name.</span></span> <span data-ttu-id="ad16f-158">예를 들어 원래 배포가 **demologicapp**였다면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-158">For example if the original deployment was called **demologicapp**, use the following command:</span></span>
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   <span data-ttu-id="ad16f-159">빌드 스크립트를 실행하는 경우 솔루션을 프로비전했을 때 사용한 것과 동일한 Azure 계정, 구독, 지역 및 Active Directory 인스턴스를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-159">When the build script runs, be sure to use the same Azure account, subscription, region, and Active Directory instance you used when you provisioned the solution.</span></span>

## <a name="see-your-logic-app-in-action"></a><span data-ttu-id="ad16f-160">작업에서 논리 앱 참조</span><span class="sxs-lookup"><span data-stu-id="ad16f-160">See your Logic App in action</span></span>
<span data-ttu-id="ad16f-161">솔루션을 프로비전할 때 미리 구성된 원격 모니터링 솔루션에는 기본적으로 두 개의 규칙이 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-161">The remote monitoring preconfigured solution has two rules set up by default when you provision a solution.</span></span> <span data-ttu-id="ad16f-162">두 규칙 모두 **SampleDevice001** 장치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-162">Both rules are on the **SampleDevice001** device:</span></span>

* <span data-ttu-id="ad16f-163">온도 > 38.00</span><span class="sxs-lookup"><span data-stu-id="ad16f-163">Temperature > 38.00</span></span>
* <span data-ttu-id="ad16f-164">습도 > 48.00</span><span class="sxs-lookup"><span data-stu-id="ad16f-164">Humidity > 48.00</span></span>

<span data-ttu-id="ad16f-165">온도 규칙은 **경보 발생** 작업을 트리거하고 습도 규칙은 **SendMessage** 작업을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-165">The temperature rule triggers the **Raise Alarm** action and the Humidity rule triggers the **SendMessage** action.</span></span> <span data-ttu-id="ad16f-166">두 작업에 동일한 URL을 사용한다고 가정하면 **ActionRepository** 클래스인 논리 앱은 어느 한쪽의 규칙에 대해 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-166">Assuming you used the same URL for both actions the **ActionRepository** class, your logic app triggers for either rule.</span></span> <span data-ttu-id="ad16f-167">두 규칙은 SendGrid를 사용하여 경고의 세부 정보가 포함된 **받는 사람** 주소에 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-167">Both rules use SendGrid to send an email to the **To** address with details of the alert.</span></span>

> [!NOTE]
> <span data-ttu-id="ad16f-168">임계값에 도달할 때마다 논리 앱이 계속 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-168">The Logic App continues to trigger every time the threshold is met.</span></span> <span data-ttu-id="ad16f-169">불필요한 전자 메일을 피하려면 솔루션 포털에서 규칙을 사용하지 않도록 설정하거나 [Azure Portal][lnk-azureportal]에서 논리 앱을 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-169">To avoid unnecessary emails, you can either disable the rules in your solution portal or disable the Logic App in the [Azure portal][lnk-azureportal].</span></span>
> 
> 

<span data-ttu-id="ad16f-170">전자 메일을 받는 것 외에도 논리 앱이 포털에서 실행될 때 다음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-170">In addition to receiving emails, you can also see when the Logic App runs in the portal:</span></span>

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a><span data-ttu-id="ad16f-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ad16f-171">Next steps</span></span>
<span data-ttu-id="ad16f-172">지금까지 논리 앱을 사용하여 미리 구성된 솔루션을 비즈니스 프로세스에 연결했으므로 미리 구성된 솔루션을 사용자 지정하기 위한 옵션에 대해 자세히 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ad16f-172">Now that you've used a Logic App to connect the preconfigured solution to a business process, you can learn more about the options for customizing the preconfigured solutions:</span></span>

* <span data-ttu-id="ad16f-173">[원격 모니터링 사전 구성 솔루션으로 동적 원격 분석 사용][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="ad16f-173">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="ad16f-174">[미리 구성된 원격 모니터링 솔루션의 장치 정보 메타데이터][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="ad16f-174">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo]</span></span>

[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk-internetofthings]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-getstarted]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-azureportal]: https://portal.azure.com
[lnk-logic-apps-actions]: ../connectors/apis-list.md
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-devsetup]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/dev-setup.md
[lnk-localdeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/local-deployment.md
[lnk-clouddeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
