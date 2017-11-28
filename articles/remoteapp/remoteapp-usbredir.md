---
title: "Azure RemoteApp에서 USB 장치를 리디렉션하려면 어떻게 합니까? | Microsoft Docs"
description: "Azure RemoteApp에서 USB 장치에 대해 리디렉션을 사용하는 방법을 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 191d98af-2f5a-4307-9042-aae0e4049f9f
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3d7165d2c3dafe87b829e588b9e7f2c377552a35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-do-you-redirect-usb-devices-in-azure-remoteapp"></a><span data-ttu-id="5e42c-104">Azure RemoteApp에서 USB 장치를 리디렉션하려면 어떻게 합니까?</span><span class="sxs-lookup"><span data-stu-id="5e42c-104">How do you redirect USB devices in Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5e42c-105">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="5e42c-106">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="5e42c-106">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="5e42c-107">장치 리디렉션을 통해 사용자가 자신의 컴퓨터나 Azure RemoteApp의 앱과 태블릿에 연결된 USB 장치를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-107">Device redirection lets users use the USB devices attached to their computer or tablet with the apps in Azure RemoteApp.</span></span> <span data-ttu-id="5e42c-108">예를 들어 Azure RemoteApp을 통해 Skype를 공유한 경우 사용자가 자신의 장치 카메라를 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-108">For example, if you shared Skype through Azure RemoteApp, your users need to be able to use their device cameras.</span></span>

<span data-ttu-id="5e42c-109">계속 진행하기 전에 [Azure RemoteApp에서 리디렉션 사용](remoteapp-redirection.md)의 USB 리디렉션 정보를 읽으세요.</span><span class="sxs-lookup"><span data-stu-id="5e42c-109">Before you go further, make sure you read the USB redirection information in [Using redirection in Azure RemoteApp](remoteapp-redirection.md).</span></span> <span data-ttu-id="5e42c-110">그러나 권장되는 nusbdevicestoredirect:s:*는 USB 웹 카메라에서 작동하지 않으며, 일부 USB 프린터 또는 USB 다기능 장치에서는 작동하지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-110">However the recommended  nusbdevicestoredirect:s:* won't work for USB web cameras and may not work for some USB printers or USB multifunctional devices.</span></span> <span data-ttu-id="5e42c-111">설계 특성상 그리고 보안상의 이유로 Azure RemoteApp 관리자가 장치 클래스 GUID 또는 장치 인스턴스 ID에 의해 리디렉션을 사용하도록 설정해야 사용자가 해당 장치를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-111">By design and for security reasons, the Azure RemoteApp administrator has to enable redirection either by device class GUID or by device instance ID before your users can use those devices.</span></span>

<span data-ttu-id="5e42c-112">이 문서에서는 웹 카메라 리디렉션에 대해 이야기하고 있지만 USB 프린터 및 **nusbdevicestoredirect:s:*** 명령으로 리디렉션하지 않는 기타 USB 다기능 장치를 리디렉션할 때에도 유사한 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-112">Although this article talks about web camera redirection, you can use a similar approach to redirect USB printers and other USB multifunctional devices that are not redirected by the **nusbdevicestoredirect:s:*** command.</span></span>

## <a name="redirection-options-for-usb-devices"></a><span data-ttu-id="5e42c-113">USB 장치에 대한 리디렉션 옵션</span><span class="sxs-lookup"><span data-stu-id="5e42c-113">Redirection options for USB devices</span></span>
<span data-ttu-id="5e42c-114">Azure RemoteApp은 원격 데스크톱 서비스에 대해 사용할 수 있는 것과 매우 유사한 메커니즘을 USB 장치 리디렉션에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-114">Azure RemoteApp uses very similar mechanisms for redirecting USB devices as the ones available for Remote Desktop Services.</span></span> <span data-ttu-id="5e42c-115">기반 기술을 통해 지정된 장치에 알맞은 리디렉션 방법을 선택하고 **usbdevicestoredirect:s:** 명령을 사용하여 고급 및 RemoteFX USB 장치 리디렉션을 모두 최대한 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-115">The underlying technology lets you choose the correct redirection method for a given device, to get the best of both high-level and RemoteFX USB device redirection using the **usbdevicestoredirect:s:** command.</span></span> <span data-ttu-id="5e42c-116">이 명령에 4개의 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-116">There are four elements to this command:</span></span>

| <span data-ttu-id="5e42c-117">처리 순서</span><span class="sxs-lookup"><span data-stu-id="5e42c-117">Processing order</span></span> | <span data-ttu-id="5e42c-118">매개 변수</span><span class="sxs-lookup"><span data-stu-id="5e42c-118">Parameter</span></span> | <span data-ttu-id="5e42c-119">설명</span><span class="sxs-lookup"><span data-stu-id="5e42c-119">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5e42c-120">1</span><span class="sxs-lookup"><span data-stu-id="5e42c-120">1</span></span> |* |<span data-ttu-id="5e42c-121">고급 리디렉션에 의해 선택되지 않은 모든 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-121">Selects all devices that aren't picked up by high-level redirection.</span></span> <span data-ttu-id="5e42c-122">참고: 설계상 USB 웹 카메라에 대해서는 *가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-122">Note: By design, * doesn't work for USB web cameras.</span></span> |
| <span data-ttu-id="5e42c-123">{장치 클래스 GUID}</span><span class="sxs-lookup"><span data-stu-id="5e42c-123">{Device class GUID}</span></span> |<span data-ttu-id="5e42c-124">지정된 장치 설정 클래스와 일치하는 모든 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-124">Selects all devices that match the specified device setup class.</span></span> | |
| <span data-ttu-id="5e42c-125">USB\InstanceID</span><span class="sxs-lookup"><span data-stu-id="5e42c-125">USB\InstanceID</span></span> |<span data-ttu-id="5e42c-126">지정된 인스턴스 ID에 대해 지정된 USB 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-126">Selects a USB device specified for the given instance ID.</span></span> | |
| <span data-ttu-id="5e42c-127">2</span><span class="sxs-lookup"><span data-stu-id="5e42c-127">2</span></span> |<span data-ttu-id="5e42c-128">-USB\인스턴스 ID</span><span class="sxs-lookup"><span data-stu-id="5e42c-128">-USB\Instance ID</span></span> |<span data-ttu-id="5e42c-129">지정된 장치에 대한 리디렉션 설정을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-129">Removes the redirection settings for the specified device.</span></span> |

## <a name="redirecting-a-usb-device-by-using-the-device-class-guid"></a><span data-ttu-id="5e42c-130">장치 클래스 GUID를 사용하여 USB 장치 리디렉션</span><span class="sxs-lookup"><span data-stu-id="5e42c-130">Redirecting a USB device by using the device class GUID</span></span>
<span data-ttu-id="5e42c-131">두 가지 방법으로 리디렉션에 사용할 수 있는 장치 클래스 GUID를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-131">There are two ways to find the device class GUID that can be used for redirection.</span></span> 

<span data-ttu-id="5e42c-132">첫 번째 옵션은 [공급업체에 사용할 수 있도록 시스템에서 정의한 장치 설정 클래스](https://msdn.microsoft.com/library/windows/hardware/ff553426.aspx)를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-132">The first option is to use the [System-Defined Device Setup Classes Available to Vendors](https://msdn.microsoft.com/library/windows/hardware/ff553426.aspx).</span></span> <span data-ttu-id="5e42c-133">로컬 컴퓨터에 연결된 장치와 가장 가깝게 일치하는 클래스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-133">Pick the class that most closely matches the device attached to the local computer.</span></span> <span data-ttu-id="5e42c-134">디지털 카메라의 경우 이 클래스는 이미징 장치 클래스 또는 비디오 캡처 장치 클래스일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-134">For digital cameras this could be an Imaging Device class or Video Capture Device class.</span></span> <span data-ttu-id="5e42c-135">로컬 컴퓨터에 연결된 USB 장치(이 경우 웹 카메라)에서 작동하는 정확한 클래스 GUID를 찾으려면 장치 클래스를 몇 번 실험해 보아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-135">You'll need to do some experimentation with the device classes to find the correct class GUID that works with the locally attached USB device (in our case the web camera).</span></span>

<span data-ttu-id="5e42c-136">더 나은 방법 또는 두 번째 옵션은 다음 단계를 수행하여 특정 장치 클래스 GUID를 찾는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-136">A better way, or the second option, is to follow these steps to find the specific device class GUID:</span></span>

1. <span data-ttu-id="5e42c-137">장치 관리자를 열고 리디렉션할 장치를 찾아서 마우스 오른쪽 단추로 클릭한 다음 속성을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-137">Open the Device Manager, locate the device that will be redirected and right-click it, and then open the properties.</span></span>
   <span data-ttu-id="5e42c-138">![장치 관리자 열기](./media/remoteapp-usbredir/ra-devicemanager.png)</span><span class="sxs-lookup"><span data-stu-id="5e42c-138">![Open the Device Manager](./media/remoteapp-usbredir/ra-devicemanager.png)</span></span>
2. <span data-ttu-id="5e42c-139">**세부 정보** 탭에서 속성 **클래스 Guid**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-139">On the **Details** tab, choose the property **Class Guid**.</span></span> <span data-ttu-id="5e42c-140">이때 나타나는 값이 해당 유형의 장치에 대한 클래스 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-140">The value which appears is the Class GUID for that type of device.</span></span>
   <span data-ttu-id="5e42c-141">![카메라 속성](./media/remoteapp-usbredir/ra-classguid.png)</span><span class="sxs-lookup"><span data-stu-id="5e42c-141">![Camera properties](./media/remoteapp-usbredir/ra-classguid.png)</span></span>
3. <span data-ttu-id="5e42c-142">클래스 Guid 값을 사용하여 일치하는 장치를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-142">Use the Class Guid value to redirect devices that match it.</span></span>

<span data-ttu-id="5e42c-143">예:</span><span class="sxs-lookup"><span data-stu-id="5e42c-143">For example:</span></span>

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s:<Class Guid value>"

<span data-ttu-id="5e42c-144">동일한 Cmdlet에서 여러 장치 리디렉션을 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-144">You can combine multiple device redirections in the same cmdlet.</span></span> <span data-ttu-id="5e42c-145">예: 로컬 저장소와 USB 웹 카메라를 리디렉션하려면 Cmdlet은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-145">For example: to redirect local storage and a USB web camera, cmdlet looks like this:</span></span>

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:<Class Guid value>"

<span data-ttu-id="5e42c-146">클래스 GUID에 의해 장치 리디렉션을 설정하면 지정된 컬렉션에서 해당 클래스 GUID와 일치하는 모든 장치가 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-146">When you set device redirection by class GUID all devices that match that class GUID in the specified collection are redirected.</span></span> <span data-ttu-id="5e42c-147">예를 들어 로컬 네트워크에 동일한 USB 웹 카메라를 가진 여러 대의 컴퓨터가 있는 경우 단일 Cmdlet을 실행하여 모든 웹 카메라를 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-147">For example, if there are multiple computers on the local network that have the same USB web cameras, you can run a single cmdlet to redirect all of the web cameras.</span></span>

## <a name="redirecting-a-usb-device-by-using-the-device-instance-id"></a><span data-ttu-id="5e42c-148">장치 인스턴스 GUID를 사용하여 USB 장치 리디렉션</span><span class="sxs-lookup"><span data-stu-id="5e42c-148">Redirecting a USB device by using the device instance ID</span></span>
<span data-ttu-id="5e42c-149">더 정밀한 제어를 원하고 장치별로 리디렉션을 제어하려면 **USB\InstanceID** 리디렉션 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-149">If you want more fine-grained control and want to control redirection per device, you can use the **USB\InstanceID** redirection parameter.</span></span>

<span data-ttu-id="5e42c-150">이 방법의 가장 어려운 부분은 USB 장치 인스턴스 ID를 찾는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-150">The hardest part of this method is finding the USB device instance ID.</span></span> <span data-ttu-id="5e42c-151">컴퓨터 및 특정 USB 장치에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-151">You'll need access to the computer and the specific USB device.</span></span> <span data-ttu-id="5e42c-152">그러고 나서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-152">Then follow these steps:</span></span>

1. <span data-ttu-id="5e42c-153">[원격 데스크톱 세션에서 내 장치와 리소스를 어떻게 사용할 수 있습니까?](http://windows.microsoft.com/en-us/windows7/How-can-I-use-my-devices-and-resources-in-a-Remote-Desktop-session)에서 설명한 대로 [원격 데스크톱 세션]에서 장치 리디렉션을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-153">Enable the device redirection in Remote Desktop Session as described in [How can I use my devices and resources in a Remote Desktop session?](http://windows.microsoft.com/en-us/windows7/How-can-I-use-my-devices-and-resources-in-a-Remote-Desktop-session)</span></span>
2. <span data-ttu-id="5e42c-154">원격 데스크톱 연결을 열고 **옵션 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-154">Open a Remote Desktop Connection and click **Show Options**.</span></span>
3. <span data-ttu-id="5e42c-155">**다른 이름으로 저장** 을 클릭하여 현재 연결 설정을 RDP 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-155">Click **Save as** to save the current connection settings to an RDP file.</span></span>  
    <span data-ttu-id="5e42c-156">![설정을 RDP 파일로 저장](./media/remoteapp-usbredir/ra-saveasrdp.png)</span><span class="sxs-lookup"><span data-stu-id="5e42c-156">![Save the settings as an RDP file](./media/remoteapp-usbredir/ra-saveasrdp.png)</span></span>
4. <span data-ttu-id="5e42c-157">파일 이름과 위치, 예를 들어 MyConnection.rdp 및 This PC\Documents를 선택하고 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-157">Choose a file name and a location, for example MyConnection.rdp and This PC\Documents, and save the file.</span></span>
5. <span data-ttu-id="5e42c-158">텍스트 편집기를 사용하여 MyConnection.rdp 파일을 열고 리디렉션할 장치의 인스턴스 ID를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-158">Open the MyConnection.rdp file using a text editor and find the instance ID of the device you want to redirect.</span></span>

<span data-ttu-id="5e42c-159">이제 다음 Cmdlet에서 인스턴스 ID를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-159">Now, use the instance ID in the following cmdlet:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s: USB\<Device InstanceID value>"



### <a name="help-us-help-you"></a><span data-ttu-id="5e42c-160">의견 보내기</span><span class="sxs-lookup"><span data-stu-id="5e42c-160">Help us help you</span></span>
<span data-ttu-id="5e42c-161">이 기사에 대한 등급을 매기고 아래에 의견을 다는 것은 물론 문서를 직접 변경할 수 있다는 사실을 알고 계셨나요?</span><span class="sxs-lookup"><span data-stu-id="5e42c-161">Did you know that in addition to rating this article and making comments down below, you can make changes to the article itself?</span></span> <span data-ttu-id="5e42c-162">누락된 부분이 있나요?</span><span class="sxs-lookup"><span data-stu-id="5e42c-162">Something missing?</span></span> <span data-ttu-id="5e42c-163">잘못된 부분이 있나요?</span><span class="sxs-lookup"><span data-stu-id="5e42c-163">Something wrong?</span></span> <span data-ttu-id="5e42c-164">혼동을 줄 수 있는 부분이 있나요?</span><span class="sxs-lookup"><span data-stu-id="5e42c-164">Did I write something that's just confusing?</span></span> <span data-ttu-id="5e42c-165">위로 스크롤하여 **GitHub에서 편집**을 클릭하면 변경할 수 있습니다. 당사에서 변경 사항을 검토하고 승인하면 변경 및 개선 사항을 바로 여기서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e42c-165">Scroll up and click **Edit on GitHub** to make changes - those will come to us for review, and then, once we sign off on them, you'll see your changes and improvements right here.</span></span>

