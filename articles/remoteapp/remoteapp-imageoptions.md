---
title: "Azure RemoteApp 이미지 aaaCreate | Microsoft Docs"
description: "Azure RemoteApp에 대 한 이미지를 만드는 데 사용할 수 있는 hello 옵션에 알아보기"
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
ms.openlocfilehash: 54e63b6fa13addfcda96ce581910e1ac48d91e70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-remoteapp-image"></a><span data-ttu-id="a4fbc-103">Azure RemoteApp 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="a4fbc-103">Create an Azure RemoteApp image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a4fbc-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a4fbc-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="a4fbc-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4fbc-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="a4fbc-106">Azure RemoteApp 사용자와 공유 하는 이미지 toohold hello 앱을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4fbc-106">Azure RemoteApp uses images toohold hello apps that you share with your users.</span></span> <span data-ttu-id="a4fbc-107">(म 이미지 걸리고 hello 사용자 Azure RemoteApp에 로그인 할 때 액세스의 toocreate Vm-를 사용 합니다.) 응용 프로그램을 선택 하 여 Azure RemoteApp 컬렉션 toocreate 클라우드 또는 하이브리드, 먼저 설치 된 해당 응용 프로그램을 사용 하 여 이미지 만들기 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4fbc-107">(We take your image and use it toocreate VMs - that's what hello users access when they sign into Azure RemoteApp.) toocreate an Azure RemoteApp collection with your choice of applications, whether it is cloud or hybrid, you  start by creating an image with those applications installed.</span></span> <span data-ttu-id="a4fbc-108">그런 다음 해당 이미지를 사용 하는 컬렉션을 만듭니다, 그리고 toohello 컬렉션, 사용자를 할당 및 toothose 사용자가 앱을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4fbc-108">Then, create a collection that uses that image, assign users toohello collection, and publish apps toothose users.</span></span>

<span data-ttu-id="a4fbc-109">이미지를 만들거나 사용하기 위한 다양한 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4fbc-109">You have several options for creating or using images.</span></span> <span data-ttu-id="a4fbc-110">기본 hello [요구 사항](remoteapp-imagereqs.md) 이미지는 Windows Server 2012 r 2를 실행 hello RDSH 원격 데스크톱 세션 호스트 () 역할이 설치 되어 있고 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4fbc-110">hello basic [requirement](remoteapp-imagereqs.md) for an image is that it run Windows Server 2012 R2 and have hello Remote Desktop Session Host (RDSH) role installed.</span></span> <span data-ttu-id="a4fbc-111">이미지를 얻는 방법이 흥미롭습니다.</span><span class="sxs-lookup"><span data-stu-id="a4fbc-111">How you get that is where things get interesting.</span></span>

<span data-ttu-id="a4fbc-112">Hello tooimages 상태가 되 면 다음 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4fbc-112">You have hello following options when it comes tooimages:</span></span>

* <span data-ttu-id="a4fbc-113">[Azure 가상 컴퓨터를 기반으로 이미지](remoteapp-image-on-azurevm.md)를 가져와서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4fbc-113">You can import and use an [image based on an Azure virtual machine](remoteapp-image-on-azurevm.md).</span></span> <span data-ttu-id="a4fbc-114">이 방법은 사용자 지정 설정이 필요한 LOB(기간 업무) 앱에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="a4fbc-114">This is good for line-of-business apps that require custom settings.</span></span> <span data-ttu-id="a4fbc-115">Hello 앱에 대 한 이미지 toowork hello를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4fbc-115">You can customize hello image toowork for hello app.</span></span>
* <span data-ttu-id="a4fbc-116">[사용자 지정 이미지를 만든 후 업로드](remoteapp-create-custom-image.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4fbc-116">You can [create and upload a custom image](remoteapp-create-custom-image.md).</span></span> <span data-ttu-id="a4fbc-117">이 방법은 온-프레미스 원격 데스크톱 서비스 배포에 사용할 이미지가 이미 있는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="a4fbc-117">This is good if you already have an image that you use for your on-premises Remote Desktop Services deployment.</span></span>
* <span data-ttu-id="a4fbc-118">Hello 중 하나를 사용 [템플릿 이미지](remoteapp-images.md) RemoteApp 구독에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4fbc-118">You can use one of hello [template images](remoteapp-images.md) included in your RemoteApp subscription.</span></span> <span data-ttu-id="a4fbc-119">이러한 이미지를 만든 및 hello a p p 팀에서 유지 관리을 일부 표준 응용 프로그램 (예: hello Office 제품군) tooyour 사용할 수 있는 사용자를 만들 수 있는지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4fbc-119">These images are created and maintained by hello RemoteApp team and contain some standard applications (like hello Office suite) that you can make available tooyour users.</span></span> <span data-ttu-id="a4fbc-120">Note 프로덕션 설정에서 해당만 hello Office 365 Pro Plus 이미지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4fbc-120">Note that only hello Office 365 Pro Plus image can be used in a production setting.</span></span>

<span data-ttu-id="a4fbc-121">이미지를 가져오는 위치 또는 만드는 방법에 관계 없이 toomake hello 이해 해도 됩니다 [응용 프로그램 요구 사항](remoteapp-appreqs.md) tooensure 앱 RemoteApp에서 잘 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4fbc-121">Regardless of where you get your image or how you create it, you'll want toomake sure you understand hello [app requirements](remoteapp-appreqs.md) tooensure that your app works well in RemoteApp.</span></span> <span data-ttu-id="a4fbc-122">그렇다면 hello 다음 단계는 toocreate는 [클라우드](remoteapp-create-cloud-deployment.md) 또는 [하이브리드](remoteapp-create-hybrid-deployment.md) 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="a4fbc-122">Then, hello next step is toocreate a [cloud](remoteapp-create-cloud-deployment.md) or [hybrid](remoteapp-create-hybrid-deployment.md) collection.</span></span>

