---
title: "Azure RemoteApp 이미지 만들기 | Microsoft 문서"
description: "Azure RemoteApp에 대한 이미지를 만드는 데 사용할 수 있는 옵션에 대해 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: cb0f9424-6185-45a1-abe9-c23f1edf34f2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 4b8ba6f264f982e03930c5ad4ccdb2d80f2c8665
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-remoteapp-image"></a><span data-ttu-id="b2c2a-103">Azure RemoteApp 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="b2c2a-103">Create an Azure RemoteApp image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b2c2a-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2a-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="b2c2a-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="b2c2a-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="b2c2a-106">Azure RemoteApp에서는 이미지를 사용하여 사용자와 공유할 앱을 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2a-106">Azure RemoteApp uses images to hold the apps that you share with your users.</span></span> <span data-ttu-id="b2c2a-107">(이미지를 가져와서 VM을 만드는 데 사용합니다. 사용자가 Azure RemoteApp에 로그인 할 때 여기에 액세스합니다.) 클라우드 또는 하이브리드 여부에 상관없이 선택한 응용 프로그램에서 Azure RemoteApp 컬렉션을 만들려면 먼저 해당 응용 프로그램이 설치된 이미지를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2a-107">(We take your image and use it to create VMs - that's what the users access when they sign into Azure RemoteApp.) To create an Azure RemoteApp collection with your choice of applications, whether it is cloud or hybrid, you  start by creating an image with those applications installed.</span></span> <span data-ttu-id="b2c2a-108">그런 다음 해당 이미지를 사용하는 컬렉션을 만들고 컬렉션에 사용자를 할당한 후 해당 사용자에게 앱을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2a-108">Then, create a collection that uses that image, assign users to the collection, and publish apps to those users.</span></span>

<span data-ttu-id="b2c2a-109">이미지를 만들거나 사용하기 위한 다양한 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2a-109">You have several options for creating or using images.</span></span> <span data-ttu-id="b2c2a-110">이미지에 대한 기본 [요구 사항](remoteapp-imagereqs.md) 으로는 Windows Server 2012 R2를 실행하고 RDSH(원격 데스크톱 세션 호스트) 역할이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2a-110">The basic [requirement](remoteapp-imagereqs.md) for an image is that it run Windows Server 2012 R2 and have the Remote Desktop Session Host (RDSH) role installed.</span></span> <span data-ttu-id="b2c2a-111">이미지를 얻는 방법이 흥미롭습니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2a-111">How you get that is where things get interesting.</span></span>

<span data-ttu-id="b2c2a-112">다음과 같은 옵션을 사용하여 이미지에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2a-112">You have the following options when it comes to images:</span></span>

* <span data-ttu-id="b2c2a-113">[Azure 가상 컴퓨터를 기반으로 이미지](remoteapp-image-on-azurevm.md)를 가져와서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2a-113">You can import and use an [image based on an Azure virtual machine](remoteapp-image-on-azurevm.md).</span></span> <span data-ttu-id="b2c2a-114">이 방법은 사용자 지정 설정이 필요한 LOB(기간 업무) 앱에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2a-114">This is good for line-of-business apps that require custom settings.</span></span> <span data-ttu-id="b2c2a-115">앱에서 작동하도록 이미지를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2a-115">You can customize the image to work for the app.</span></span>
* <span data-ttu-id="b2c2a-116">[사용자 지정 이미지를 만든 후 업로드](remoteapp-create-custom-image.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2a-116">You can [create and upload a custom image](remoteapp-create-custom-image.md).</span></span> <span data-ttu-id="b2c2a-117">이 방법은 온-프레미스 원격 데스크톱 서비스 배포에 사용할 이미지가 이미 있는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2a-117">This is good if you already have an image that you use for your on-premises Remote Desktop Services deployment.</span></span>
* <span data-ttu-id="b2c2a-118">RemoteApp 구독에 포함된 [템플릿 이미지](remoteapp-images.md) 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2a-118">You can use one of the [template images](remoteapp-images.md) included in your RemoteApp subscription.</span></span> <span data-ttu-id="b2c2a-119">이러한 이미지는 RemoteApp 팀에서 만들어서 유지 관리하며 사용자에게 제공할 수 있는 일부 표준 응용 프로그램(예: Office 제품군)을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2a-119">These images are created and maintained by the RemoteApp team and contain some standard applications (like the Office suite) that you can make available to your users.</span></span> <span data-ttu-id="b2c2a-120">프로덕션 설정에서는 Office 365 Pro Plus 이미지만 사용할 수 습니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2a-120">Note that only the Office 365 Pro Plus image can be used in a production setting.</span></span>

<span data-ttu-id="b2c2a-121">이미지를 가져오는 위치 또는 만드는 방법에 관계없이 앱이 RemoteApp에서 올바르게 작동하려면 [앱 요구 사항](remoteapp-appreqs.md) 을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2a-121">Regardless of where you get your image or how you create it, you'll want to make sure you understand the [app requirements](remoteapp-appreqs.md) to ensure that your app works well in RemoteApp.</span></span> <span data-ttu-id="b2c2a-122">다음 단계에서는 [클라우드](remoteapp-create-cloud-deployment.md) 또는 [하이브리드](remoteapp-create-hybrid-deployment.md) 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2a-122">Then, the next step is to create a [cloud](remoteapp-create-cloud-deployment.md) or [hybrid](remoteapp-create-hybrid-deployment.md) collection.</span></span>

