---
title: "Azure RemoteApp에 대한 사용자 지정 이미지에 중요 데이터를 저장하지 않음 | Microsoft Docs"
description: "Azure RemoteApp의 사용자 지정 이미지에 데이터를 저장하기 위한 지침 알아보기"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 5a19903b-15f9-49d9-9bc1-ae80f2671aa1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 75d5415d33324d957617426e75909a6c6c58b1f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a><span data-ttu-id="ef174-103">사용자 지정 이미지에 중요 데이터를 저장하지 않음</span><span class="sxs-lookup"><span data-stu-id="ef174-103">Never store sensitive data on custom images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ef174-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ef174-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ef174-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="ef174-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ef174-106">Azure RemoteApp에서 사용자 고유의 응용 프로그램을 호스팅할 때는 먼저 사용자 지정 이미지를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef174-106">When you host your own application in Azure RemoteApp, the first step is to create a custom image.</span></span> <span data-ttu-id="ef174-107">사용자 지정 이미지를 사용하여 사용자에게 앱을 서비스하는 VM 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef174-107">We use that custom image to create VM instances that serve your apps to your users.</span></span> <span data-ttu-id="ef174-108">사용자 지정 이미지는 응용 프로그램만 포함해야 하며, SQL 데이터베이스, 개인 파일, 특수 데이터 파일(예: QuickBooks) 등의 손실될 수 있는 중요 데이터는 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ef174-108">The custom image should contain ONLY applications and never sensitive data that can be lost, such as SQL databases, personnel files, or special data files like QuickBooks company files.</span></span> <span data-ttu-id="ef174-109">모든 중요 데이터는 파일 서버에서 Azure RemoteApp 외부, 다른 Azure VM 또는 SQL Azure에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef174-109">All sensitive data should reside external to Azure RemoteApp on a file server, another Azure VM, or in SQL Azure.</span></span> <span data-ttu-id="ef174-110">이미지는 데이터 원본에 연결되고 데이터를 표시하는 응용 프로그램만 호스팅해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef174-110">The image should just host the application that connects to the data source and presents the data.</span></span> <span data-ttu-id="ef174-111">자세한 내용은 [Azure RemoteApp 이미지에 대한 요구 사항](remoteapp-imagereqs.md) 을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="ef174-111">Review [Requirements for Azure RemoteApp images](remoteapp-imagereqs.md) for more information.</span></span> 

<span data-ttu-id="ef174-112">중요 데이터를 저장해서는 안 되는 이유를 이해하려면 Azure RemoteApp의 작동 방식을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef174-112">To understand why you should not store sensitive data, you need to understand how Azure RemoteApp works.</span></span> <span data-ttu-id="ef174-113">컬렉션을 만들거나 업데이트할 때는 백그라운드에서 여러 차례의 이미지 복제 또는 복사본이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ef174-113">When a collection is created or updated, behind the scenes multiple clones or copies of the image are created.</span></span> <span data-ttu-id="ef174-114">이러한 모든 VM 인스턴스는 사용자 지정 이미지의 정확한 복제본입니다. 사용자가 응용 프로그램을 실행할 때 이 VM 인스턴스 중 하나와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef174-114">All these VM instances are exact replicas of the custom image; when users launch applications they are connected to one of these VM instances.</span></span> <span data-ttu-id="ef174-115">그러나 이 인스턴스들은 비영구적이기 때문에 동일한 인스턴스가 보장되는 것은 아니며 문제가 되지도 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ef174-115">But the same instance is not guaranteed and should not matter because they are non-persistent.</span></span> <span data-ttu-id="ef174-116">응용 프로그램을 호스팅하는 VM 인스턴스는 비영구적이며 컬렉션 업데이트 중에 파괴, 삭제 등이 일어날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef174-116">The VM instances hosting the applications are non-persistent and can be destroyed or deleted based, for example, during collection update.</span></span> 

<span data-ttu-id="ef174-117">컬렉션이 프로비전되고 사용자가 VM 연결을 시작하면 사용자 데이터가 c:\users\<userprofile>에 있는 사용자 프로필인 [UPD(사용자 프로필 디스크)](remoteapp-upd.md)라고 하는 VHD 내의 별도 저장소에 저장되므로 영구 보존되고 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef174-117">Once the collection is provisioned and users start connecting to the VMs, user data is persistent and protected because it is saved on separate storage within a VHD that we call a [user profile disk (UPD)](remoteapp-upd.md), which is the user profile in c:\users\<userprofile>.</span></span> <span data-ttu-id="ef174-118">응용 프로그램이 시작되면 UPD가 탑재되며 운영 체제에서 로컬 사용자 프로필과 동일하게 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef174-118">When an application starts, the UPD is mounted and treated just like a local user profile by the operating system.</span></span> <span data-ttu-id="ef174-119">[Azure RemoteApp에서 사용자 데이터와 설정을 저장하는 방법](remoteapp-upd.md)에서 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="ef174-119">Read more about how [Azure RemoteApp saves user data and settings](remoteapp-upd.md).</span></span>

<span data-ttu-id="ef174-120">이미지에 상주할 수 없는 데이터 예:</span><span class="sxs-lookup"><span data-stu-id="ef174-120">Example data that should not reside in the image:</span></span>

* <span data-ttu-id="ef174-121">사용자가 액세스할 수 있는 공유 데이터</span><span class="sxs-lookup"><span data-stu-id="ef174-121">Shared data for users to access</span></span>
* <span data-ttu-id="ef174-122">SQL DB 또는 QuickBooks DB</span><span class="sxs-lookup"><span data-stu-id="ef174-122">SQL DB or QuickBooks DB</span></span>
* <span data-ttu-id="ef174-123">D:\의 모든 데이터</span><span class="sxs-lookup"><span data-stu-id="ef174-123">Any data in D:\\</span></span>

<span data-ttu-id="ef174-124">모든 사용자의 UPD에 복사되는 기본 프로필에 상주할 수 있는 데이터 예:</span><span class="sxs-lookup"><span data-stu-id="ef174-124">Example data that can reside in the default profile to be copied into every users’ UPD:</span></span>

* <span data-ttu-id="ef174-125">사용자별 구성 파일 </span><span class="sxs-lookup"><span data-stu-id="ef174-125">Configuration files per user</span></span>
* <span data-ttu-id="ef174-126">사용자가 자신의 UPD에 보존해야 하는 스크립트</span><span class="sxs-lookup"><span data-stu-id="ef174-126">Scripts that users would need preserved in their UPD</span></span>

<span data-ttu-id="ef174-127">핵심 내용:</span><span class="sxs-lookup"><span data-stu-id="ef174-127">Key points:</span></span>

* <span data-ttu-id="ef174-128">사용자 지정 이미지를 만들 때 이미지에 손실될 수 있는 중요 이미지를 저장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ef174-128">Never store sensitive data that can be lost on the image when creating a custom image.</span></span>
* <span data-ttu-id="ef174-129">중요한 데이터는 항상 별도의 파일 서버, 클라우드의 별도 Azure VM에 상주해야 하며 항상 Azure RemoteApp에서 응용 프로그램을 호스팅하는 VM 인스턴스 외부에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef174-129">Sensitive data should always reside on a separate file server, separate Azure VM, on the cloud, and always external to the VM instances hosting your applications within Azure RemoteApp.</span></span> 
* <span data-ttu-id="ef174-130">사용자 데이터는 사용자 프로필 디스크(UPD)에 저장되어 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef174-130">User data is saved and persists in the user profile disk (UPD)</span></span>

