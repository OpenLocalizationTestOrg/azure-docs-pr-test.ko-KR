---
title: "aaaNever Azure RemoteApp에 대 한 사용자 지정 이미지에 중요 한 데이터 저장소 | Microsoft Docs"
description: "Azure RemoteApp에서 사용자 지정 이미지에 데이터를 저장 하기 위한 지침 hello에 대 한 자세한 내용은"
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
ms.openlocfilehash: 86a0fea218f8826d6d25f50d3c4c36e368e26fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a><span data-ttu-id="093cd-103">사용자 지정 이미지에 중요 데이터를 저장하지 않음</span><span class="sxs-lookup"><span data-stu-id="093cd-103">Never store sensitive data on custom images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="093cd-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="093cd-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="093cd-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="093cd-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="093cd-106">Azure RemoteApp에서 사용자의 응용 프로그램을 호스팅하는 경우 hello 첫 번째 단계는 사용자 지정 이미지 toocreate 것입니다.</span><span class="sxs-lookup"><span data-stu-id="093cd-106">When you host your own application in Azure RemoteApp, hello first step is toocreate a custom image.</span></span> <span data-ttu-id="093cd-107">Tooyour 사용자가 앱을 처리 하는 해당 사용자 지정 이미지 toocreate VM 인스턴스에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="093cd-107">We use that custom image toocreate VM instances that serve your apps tooyour users.</span></span> <span data-ttu-id="093cd-108">hello 사용자 지정 이미지 전용 응용 프로그램과 같은 SQL 데이터베이스, 담당자 파일 또는 QuickBooks 회사 파일 등의 특수 한 데이터 파일 손실 될 수 있는 되지 중요 한 데이터를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="093cd-108">hello custom image should contain ONLY applications and never sensitive data that can be lost, such as SQL databases, personnel files, or special data files like QuickBooks company files.</span></span> <span data-ttu-id="093cd-109">모든 중요 한 데이터는 외부 tooAzure RemoteApp SQL Azure 또는 다른 Azure VM에 파일 서버에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="093cd-109">All sensitive data should reside external tooAzure RemoteApp on a file server, another Azure VM, or in SQL Azure.</span></span> <span data-ttu-id="093cd-110">hello 이미지 호스트 hello 응용 프로그램만 toohello 데이터 원본을 연결 하는 hello 데이터를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="093cd-110">hello image should just host hello application that connects toohello data source and presents hello data.</span></span> <span data-ttu-id="093cd-111">자세한 내용은 [Azure RemoteApp 이미지에 대한 요구 사항](remoteapp-imagereqs.md) 을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="093cd-111">Review [Requirements for Azure RemoteApp images](remoteapp-imagereqs.md) for more information.</span></span> 

<span data-ttu-id="093cd-112">중요 한 데이터를 저장 하면 안 되는 이유는 toounderstand toounderstand Azure RemoteApp의 작동 원리를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="093cd-112">toounderstand why you should not store sensitive data, you need toounderstand how Azure RemoteApp works.</span></span> <span data-ttu-id="093cd-113">컬렉션을 만들거나 업데이트 하는 경우 hello 백그라운드 여러 복제본 또는 hello 이미지의 복사본이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="093cd-113">When a collection is created or updated, behind hello scenes multiple clones or copies of hello image are created.</span></span> <span data-ttu-id="093cd-114">이러한 모든 VM 인스턴스는 이미지를 사용자 지정 하는 hello;의 정확한 복제본 사용자가 응용 프로그램을 시작 하면 이러한 VM 인스턴스의 연결 된 tooone 됩니다.</span><span class="sxs-lookup"><span data-stu-id="093cd-114">All these VM instances are exact replicas of hello custom image; when users launch applications they are connected tooone of these VM instances.</span></span> <span data-ttu-id="093cd-115">하지만 hello 동일한 인스턴스 보장 되지 않으며 비 영구적인 되기 때문에 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="093cd-115">But hello same instance is not guaranteed and should not matter because they are non-persistent.</span></span> <span data-ttu-id="093cd-116">hello hello에 대 한 응용 프로그램을 호스팅할 비 영구적인 되며 수 VM 인스턴스 제거 되거나 삭제 예를 들어 컬렉션 업데이트 하는 동안 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="093cd-116">hello VM instances hosting hello applications are non-persistent and can be destroyed or deleted based, for example, during collection update.</span></span> 

<span data-ttu-id="093cd-117">사용자 데이터는 영구 hello 컬렉션이 프로 비전 되 고 연결 toohello Vm을 시작 하는 사용자가 이라고 하는 VHD 내에서 별도 저장소에 저장 되기 때문에 보호 한 [사용자 프로필 디스크 (UPD)](remoteapp-upd.md), 변수인 hello 사용자 프로필 c:\users의\<userprofile > 합니다.</span><span class="sxs-lookup"><span data-stu-id="093cd-117">Once hello collection is provisioned and users start connecting toohello VMs, user data is persistent and protected because it is saved on separate storage within a VHD that we call a [user profile disk (UPD)](remoteapp-upd.md), which is hello user profile in c:\users\<userprofile>.</span></span> <span data-ttu-id="093cd-118">응용 프로그램이 시작 되 면 hello UPD 탑재 되 고 hello 운영 체제에서 로컬 사용자 프로필이 처럼 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="093cd-118">When an application starts, hello UPD is mounted and treated just like a local user profile by hello operating system.</span></span> <span data-ttu-id="093cd-119">[Azure RemoteApp에서 사용자 데이터와 설정을 저장하는 방법](remoteapp-upd.md)에서 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="093cd-119">Read more about how [Azure RemoteApp saves user data and settings](remoteapp-upd.md).</span></span>

<span data-ttu-id="093cd-120">Hello 이미지의 노드에 있지 않고 예제 데이터:</span><span class="sxs-lookup"><span data-stu-id="093cd-120">Example data that should not reside in hello image:</span></span>

* <span data-ttu-id="093cd-121">사용자가 tooaccess에 대 한 공유 데이터</span><span class="sxs-lookup"><span data-stu-id="093cd-121">Shared data for users tooaccess</span></span>
* <span data-ttu-id="093cd-122">SQL DB 또는 QuickBooks DB</span><span class="sxs-lookup"><span data-stu-id="093cd-122">SQL DB or QuickBooks DB</span></span>
* <span data-ttu-id="093cd-123">D:\의 모든 데이터</span><span class="sxs-lookup"><span data-stu-id="093cd-123">Any data in D:\\</span></span>

<span data-ttu-id="093cd-124">예제 데이터의 기본 프로필 toobe hello에에서 존재할 수 있는 모든 사용자의 UPD에 복사.</span><span class="sxs-lookup"><span data-stu-id="093cd-124">Example data that can reside in hello default profile toobe copied into every users’ UPD:</span></span>

* <span data-ttu-id="093cd-125">사용자별 구성 파일 </span><span class="sxs-lookup"><span data-stu-id="093cd-125">Configuration files per user</span></span>
* <span data-ttu-id="093cd-126">사용자가 자신의 UPD에 보존해야 하는 스크립트</span><span class="sxs-lookup"><span data-stu-id="093cd-126">Scripts that users would need preserved in their UPD</span></span>

<span data-ttu-id="093cd-127">핵심 내용:</span><span class="sxs-lookup"><span data-stu-id="093cd-127">Key points:</span></span>

* <span data-ttu-id="093cd-128">사용자 지정 이미지를 만들 때는 hello 이미지에서 손실 될 수 있는 중요 한 데이터를 저장 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="093cd-128">Never store sensitive data that can be lost on hello image when creating a custom image.</span></span>
* <span data-ttu-id="093cd-129">중요 한 데이터는 항상 별도 파일 서버에 상주, hello 클라우드 및 Azure RemoteApp 내 응용 프로그램을 호스팅하는 항상 외부 toohello VM 인스턴스에서 Azure VM을 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="093cd-129">Sensitive data should always reside on a separate file server, separate Azure VM, on hello cloud, and always external toohello VM instances hosting your applications within Azure RemoteApp.</span></span> 
* <span data-ttu-id="093cd-130">사용자 데이터가 저장 되 고 hello 사용자 프로필 디스크 (UPD)에 유지</span><span class="sxs-lookup"><span data-stu-id="093cd-130">User data is saved and persists in hello user profile disk (UPD)</span></span>

