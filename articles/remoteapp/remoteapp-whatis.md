---
title: "Azure RemoteApp이란? | Microsoft Docs"
description: "Azure RemoteApp를 통해 장치에 앱 및 리소스를 공유하는 방법을 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: d7a8a311-e70a-4463-ac85-c7f62c500921
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d4befefcaa0cacdde9cce3d8ad93ae8c4cad47f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-remoteapp"></a><span data-ttu-id="3b198-104">Azure RemoteApp이란?</span><span class="sxs-lookup"><span data-stu-id="3b198-104">What is Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3b198-105">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3b198-106">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="3b198-106">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3b198-107">Azure RemoteApp은 원격 데스크톱 서비스가 지원하는 온-프레미스 Microsoft RemoteApp 프로그램의 기능을 Azure에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-107">Azure RemoteApp brings the functionality of the on-premises Microsoft RemoteApp program, backed by Remote Desktop Services, to Azure.</span></span> <span data-ttu-id="3b198-108">Azure RemoteApp은 다양한 여러 사용자 장치에서 안전하게 원격으로 응용 프로그램에 액세스하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-108">Azure RemoteApp helps you provide secure, remote access to applications from many different user devices.</span></span> <span data-ttu-id="3b198-109">기본적으로 Azure RemoteApp은 클라우드에서 비영구 터미널 서버 세션을 호스팅하고 이를 사용하고 사용자와 공유하기 위해 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-109">Azure RemoteApp basically hosts non-persistent Terminal Server sessions in the cloud, and you get to use them and share them with your users.</span></span>

<span data-ttu-id="3b198-110">Azure RemoteApp를 사용하면 거의 모든 장치의 사용자와도 앱 및 리소스를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-110">With Azure RemoteApp you can share apps and resources with users on almost any device.</span></span> <span data-ttu-id="3b198-111">우리는 사용자의 앱을 클라우드에서 호스팅하므로 하드웨어 및 크기 조정을 사용자 요구에 충족하도록 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-111">We host your apps in the cloud, meaning we take care of the hardware and scaling to meet user demands.</span></span> <span data-ttu-id="3b198-112">우리가 해야 하는 일은 게시가 공유하려고 하는 앱을 업로드한 다음 사용자가 해당 앱을 사용하도록 하는 것이 전부입니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-112">All you have to do is upload the apps you want to share, and then get your users to use those apps.</span></span> <span data-ttu-id="3b198-113">[사용자는 자신의 장치를 유지](remoteapp-clients.md)하는 반면에, 게시자는 Azure 포털을 통해 모든 항목을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-113">[Users get to keep their own devices](remoteapp-clients.md), while you manage everything through the Azure portal.</span></span> <span data-ttu-id="3b198-114">회사 자격 증명을 사용하는 옵션도 있으므로 앱과 데이터의 보안을 확보할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-114">You even have the option of using your corporate credentials, letting you ensure the security of apps and data.</span></span>

<span data-ttu-id="3b198-115">Azure RemoteApp에 대한 자세한 내용을 읽거나 이미 확신을 가진 경우 [지금 사용해 보세요](https://azure.microsoft.com/services/remoteapp/).</span><span class="sxs-lookup"><span data-stu-id="3b198-115">Read on for more information about Azure RemoteApp, or, if we have already convinced you, [try it out now](https://azure.microsoft.com/services/remoteapp/).</span></span>

<span data-ttu-id="3b198-116">Azure RemoteApp과 관련된 질문이 있는 경우</span><span class="sxs-lookup"><span data-stu-id="3b198-116">Have questions about Azure RemoteApp?</span></span> <span data-ttu-id="3b198-117">[FAQ](remoteapp-faq.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="3b198-117">Check out our [FAQ](remoteapp-faq.md).</span></span>

<span data-ttu-id="3b198-118">Azure RemoteApp은 [Microsoft 가상 데스크톱 인프라](http://www.microsoft.com/server-cloud/products/virtual-desktop-infrastructure/explore.aspx)의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-118">Azure RemoteApp is part of the [Microsoft Virtual Desktop Infrastructure](http://www.microsoft.com/server-cloud/products/virtual-desktop-infrastructure/explore.aspx).</span></span>

<span data-ttu-id="3b198-119">**신규!**</span><span class="sxs-lookup"><span data-stu-id="3b198-119">**New!**</span></span> <span data-ttu-id="3b198-120">Azure RemoteApp에 대해 더 알아보고 싶으세요?</span><span class="sxs-lookup"><span data-stu-id="3b198-120">Want to learn more about Azure RemoteApp?</span></span> <span data-ttu-id="3b198-121">아니면 Azure RemoteApp을 확인할 준비가 되셨나요?</span><span class="sxs-lookup"><span data-stu-id="3b198-121">Or ready to validate Azure RemoteApp at scale?</span></span> <span data-ttu-id="3b198-122">매주 열리는 [전문가에게 물어보세요. 웹 세미나](https://azureinfo.microsoft.com/AzureRemoteAppAskTheExperts-Registration-Page.html?ls=Website)에 참여해 보세요.</span><span class="sxs-lookup"><span data-stu-id="3b198-122">Join our weekly [ask the experts webinar](https://azureinfo.microsoft.com/AzureRemoteAppAskTheExperts-Registration-Page.html?ls=Website).</span></span>

## <a name="azure-remoteapp-collections"></a><span data-ttu-id="3b198-123">Azure RemoteApp 컬렉션</span><span class="sxs-lookup"><span data-stu-id="3b198-123">Azure RemoteApp collections</span></span>
<span data-ttu-id="3b198-124">다음과 같은 두 가지 종류의 [Azure RemoteApp 컬렉션](remoteapp-collections.md)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-124">There are two kinds of [Azure RemoteApp collections](remoteapp-collections.md):</span></span>

* <span data-ttu-id="3b198-125">**클라우드 컬렉션** 은 클라우드에 호스트되며 프로그램에 대한 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-125">A **cloud collection** is hosted in and stores data for programs in the cloud.</span></span> <span data-ttu-id="3b198-126">사용자는 Microsoft 계정이나 Azure Active Directory와 동기화 또는 페더레이션된 회사 자격 증명으로 로그인하여 앱에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-126">Users can access apps by logging in with their Microsoft account or corporate credentials synchronized or federated with Azure Active Directory.</span></span>
  
    <span data-ttu-id="3b198-127">공유하려는 응용 프로그램이 회사의 사설 네트워크에 있는 리소스에 연결(예: VPN 장치를 통해)할 필요가 없는 경우 클라우드 컬렉션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-127">Choose a cloud collection when the application you want to share does not require a connection to any resource your company's private network (for example, through a VPN device).</span></span> <span data-ttu-id="3b198-128">응용 프로그램이 인터넷, OneDrive 또는 Azure의 리소스를 사용하는 경우 클라우드 컬렉션이 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-128">If the application uses resources on the Internet, OneDrive, or Azure, a cloud collection will work for you.</span></span> <span data-ttu-id="3b198-129">가장 빨리 만들 수 있는 컬렉션이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-129">It's also the quickest to create.</span></span>
* <span data-ttu-id="3b198-130">**하이브리드 컬렉션** 은 Azure 클라우드에 호스트되고 데이터를 저장하지만 사용자가 로컬 네트워크에 저장된 데이터 및 리소스에 액세스할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-130">A **hybrid collection** is hosted in and stores data in the Azure cloud but also lets users access data and resources stored on your local network.</span></span> <span data-ttu-id="3b198-131">사용자는 Azure Active Directory와 동기화 또는 페더레이션된 회사 자격 증명으로 로그인하여 앱에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-131">Users can access apps by logging in with their corporate credentials synchronized or federated with Azure Active Directory.</span></span>
  
    <span data-ttu-id="3b198-132">회사의 사설 네트워크에 있는 리소스에 연결해야 할 경우 하이브리드 컬렉션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-132">Choose a hybrid collection if you require a connection to resources on your company's private network.</span></span> <span data-ttu-id="3b198-133">예를 들어 응용 프로그램에서 다음에 액세스해야 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-133">For example, if the application needs access to one of the following:</span></span>
  
  * <span data-ttu-id="3b198-134">인트라넷에 위치한 파일 서버</span><span class="sxs-lookup"><span data-stu-id="3b198-134">File servers located on your intranet</span></span>
  * <span data-ttu-id="3b198-135">Quicken</span><span class="sxs-lookup"><span data-stu-id="3b198-135">Quicken</span></span>
  * <span data-ttu-id="3b198-136">방화벽 뒤에 있는 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="3b198-136">Databases behind a firewall</span></span>
    
    <span data-ttu-id="3b198-137">일반적으로 클라우드로 옮길 수 없는 많은 양의 리소스가 사설 네트워크에 있는 대규모 회사에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-137">This is generally more useful for large companies with lots of resources on their private networks that can't be moved to the cloud.</span></span>

<span data-ttu-id="3b198-138">다양한 컬렉션에 네트워크를 포함한 다양한 옵션이 있으므로 가장 적합한 [컬렉션](remoteapp-collections.md) 을 알아낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-138">The different collections have different options, including networks, so figure out [which collection](remoteapp-collections.md) works best for you.</span></span> 

### <a name="updating-your-collection"></a><span data-ttu-id="3b198-139">컬렉션 업데이트</span><span class="sxs-lookup"><span data-stu-id="3b198-139">Updating your collection</span></span>
<span data-ttu-id="3b198-140">하이브리드 컬렉션과 클라우드 컬렉션 간의 주요 차이점 중 하나는 소프트웨어 업데이트가 처리되는 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-140">One of the key differences between the hybrid and cloud collections is how software updates are handled.</span></span> <span data-ttu-id="3b198-141">사전 설치된 Office 365 ProPlus 또는 Office 2013 이미지를 사용하는 클라우드 컬렉션의 경우 업데이트에 대해 염려하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-141">With a cloud collection that uses the preinstalled Office 365 ProPlus or Office 2013 image, you do not have to worry about any updates.</span></span> <span data-ttu-id="3b198-142">서비스가 자체적으로 유지 관리되며 지속적으로 앱과 운영 체제의 업데이트를 출시합니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-142">The service maintains itself and rolls out updates on an ongoing basis, to both apps and the operating system.</span></span>

<span data-ttu-id="3b198-143">사용자 지정 템플릿 이미지를 사용하는 클라우드 컬렉션은 물론 하이브리드 컬렉션의 경우 이미지와 앱을 유지 관리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-143">For hybrid collections, as well as cloud collections that use a custom template image, you are in charge of maintaining the image and apps.</span></span> <span data-ttu-id="3b198-144">도메인에 가입된 이미지의 경우 Windows 업데이트, 그룹 정책 또는 System Center와 같은 도구를 사용하여 업데이트를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-144">For domain-joined images, you can control updates by using tools such as Windows Update, Group Policy, or System Center.</span></span>

<span data-ttu-id="3b198-145">사용자 지정 템플릿 이미지를 업데이트한 후 새 이미지를 Azure 클라우드로 업로드하고 새 이미지를 사용하도록 컬렉션을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-145">After you update your custom template image, you upload the new image to the Azure cloud and then update the collection to use the new image.</span></span> <span data-ttu-id="3b198-146">(Azure RemoteApp **빠른 시작** 페이지나 대시보드에서 이 작업을 할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="3b198-146">(You can do this from the Azure RemoteApp **Quick Start** page or the Dashboard.)</span></span>

<span data-ttu-id="3b198-147">자세한 내용은 [컬렉션 업데이트](remoteapp-update.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b198-147">See [Update your collection](remoteapp-update.md) for more information.</span></span>

## <a name="supported-remoteapp-clients"></a><span data-ttu-id="3b198-148">지원되는 RemoteApp 클라이언트</span><span class="sxs-lookup"><span data-stu-id="3b198-148">Supported RemoteApp clients</span></span>
<span data-ttu-id="3b198-149">Azure RemoteApp은 Windows 및 Windows RT용 RemoteApp 클라이언트 앱과 Mac, iOS 및 Android용 Microsoft 원격 데스크톱 앱에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-149">Azure RemoteApp is supported on the RemoteApp client apps for Windows and Windows RT, as well as the Microsoft Remote Desktop apps for Mac, iOS and Android.</span></span> <span data-ttu-id="3b198-150">사용자는 휴대폰이나 계산 장치에서 이러한 앱을 사용하여 새 Azure RemoteApp 프로그램에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-150">Your users can use these apps on their mobile or compute devices to access the new Azure RemoteApp programs.</span></span>

<span data-ttu-id="3b198-151">클라이언트에 대한 자세한 내용은 [Azure RemoteApp의 앱에 액세스](remoteapp-clients.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b198-151">See [Accessing your apps in Azure RemoteApp](remoteapp-clients.md) for more information about the clients.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b198-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3b198-152">Next steps</span></span>
<span data-ttu-id="3b198-153">지금</span><span class="sxs-lookup"><span data-stu-id="3b198-153">Go!</span></span> <span data-ttu-id="3b198-154">사용해 보세요!</span><span class="sxs-lookup"><span data-stu-id="3b198-154">Try it out!</span></span> <span data-ttu-id="3b198-155">다음은 Azure RemoteApp를 시작하는 데 도움이 되는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-155">These articles help get you started with Azure RemoteApp:</span></span>

* [<span data-ttu-id="3b198-156">Azure RemoteApp에 필요한 컬렉션의 종류는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="3b198-156">What kind of collection do you need for Azure RemoteApp?</span></span>](remoteapp-collections.md)
* [<span data-ttu-id="3b198-157">Azure RemoteApp 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="3b198-157">Create an Azure RemoteApp image</span></span>](remoteapp-imageoptions.md)
* [<span data-ttu-id="3b198-158">Azure RemoteApp의 클라우드 컬렉션을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="3b198-158">How to create a cloud collection of Azure RemoteApp</span></span>](remoteapp-create-cloud-deployment.md)
* [<span data-ttu-id="3b198-159">Azure RemoteApp의 하이브리드 컬렉션을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="3b198-159">How to create a hybrid collection of Azure RemoteApp</span></span>](remoteapp-create-hybrid-deployment.md)
* [<span data-ttu-id="3b198-160">Azure RemoteApp의 라이선스 작동 방식</span><span class="sxs-lookup"><span data-stu-id="3b198-160">How does licensing work in Azure RemoteApp?</span></span>](remoteapp-licensing.md)
* [<span data-ttu-id="3b198-161">Azure RemoteApp 사용 모범 사례</span><span class="sxs-lookup"><span data-stu-id="3b198-161">Best practices for using Azure RemoteApp</span></span>](remoteapp-bestpractices.md)
* [<span data-ttu-id="3b198-162">Azure RemoteApp FAQ</span><span class="sxs-lookup"><span data-stu-id="3b198-162">Azure RemoteApp FAQ</span></span>](remoteapp-faq.md)

### <a name="help-us-help-you"></a><span data-ttu-id="3b198-163">의견 보내기</span><span class="sxs-lookup"><span data-stu-id="3b198-163">Help us help you</span></span>
<span data-ttu-id="3b198-164">이 기사에 대한 등급을 매기고 아래에 의견을 다는 것은 물론 문서를 직접 변경할 수 있다는 사실을 알고 계셨나요?</span><span class="sxs-lookup"><span data-stu-id="3b198-164">Did you know that in addition to rating this article and making comments down below, you can make changes to the article itself?</span></span> <span data-ttu-id="3b198-165">누락된 부분이 있나요?</span><span class="sxs-lookup"><span data-stu-id="3b198-165">Something missing?</span></span> <span data-ttu-id="3b198-166">잘못된 부분이 있나요?</span><span class="sxs-lookup"><span data-stu-id="3b198-166">Something wrong?</span></span> <span data-ttu-id="3b198-167">혼동을 줄 수 있는 부분이 있나요?</span><span class="sxs-lookup"><span data-stu-id="3b198-167">Did I write something that's just confusing?</span></span> <span data-ttu-id="3b198-168">위로 스크롤하여 **GitHub에서 편집** 또는 **편집**을 클릭하면 변경할 수 있습니다. 당사에서 변경 사항을 검토하고 승인하면 변경 및 개선 사항을 바로 여기서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b198-168">Scroll up and click **Edit on GitHub** or **Edit** to make changes - those will come to us for review, and then, once we sign off on them, you'll see your changes and improvements right here.</span></span>

