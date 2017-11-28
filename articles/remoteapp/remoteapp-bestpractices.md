---
title: "Azure RemoteApp 모범 사례 | Microsoft 문서"
description: "Azure RemoteApp 구성 및 사용 모범 사례"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b851865b-bec4-4f29-82c0-7b9770c1a520
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ab9c2dafc622e9b6f3bcd2767218cdc03e844847
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a><span data-ttu-id="c231d-103">Azure RemoteApp 구성 및 사용 모범 사례</span><span class="sxs-lookup"><span data-stu-id="c231d-103">Best practices for configuring and using Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c231d-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c231d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="c231d-105">자세한 내용은 [알림](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="c231d-105">Read the [announcement](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) for details.</span></span>
> 
> 

<span data-ttu-id="c231d-106">다음 정보는 Azure RemoteApp을 생산적으로 구성하고 사용하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c231d-106">The following information can help you configure and use Azure RemoteApp productively.</span></span>

## <a name="connectivity"></a><span data-ttu-id="c231d-107">연결</span><span class="sxs-lookup"><span data-stu-id="c231d-107">Connectivity</span></span>
* <span data-ttu-id="c231d-108">항상 최신 클라이언트 버전을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c231d-108">Always use the latest client version.</span></span> <span data-ttu-id="c231d-109">이전 클라이언트를 사용하면 연결 문제 및 기타 성능 저하가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c231d-109">Using older clients might result in connectivity issues and other degraded experiences.</span></span> <span data-ttu-id="c231d-110">장치에 자동 응용 프로그램 업데이트를 사용하면 항상 최신 클라이언트가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="c231d-110">Enabling automatic application updates for your device will ensure that the latest client is always installed.</span></span>
* <span data-ttu-id="c231d-111">항상 사용 가능한 가장 안정적이고 신뢰할 수 있는 인터넷 연결을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c231d-111">Always use the most stable and reliable internet connection available to you.</span></span>  
* <span data-ttu-id="c231d-112">최적 연결 성능을 위해 지원되는 프록시 연결만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c231d-112">Use only supported proxy connections for optimal connectivity performance.</span></span>  <span data-ttu-id="c231d-113">SOCKS 프록시는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c231d-113">The SOCKS proxy is not supported.</span></span>

## <a name="applications"></a><span data-ttu-id="c231d-114">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="c231d-114">Applications</span></span>
* <span data-ttu-id="c231d-115">응용 프로그램에서 작업을 마치면 RemoteApp 응용 프로그램을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c231d-115">Save and close RemoteApp applications when you are done with the application.</span></span> <span data-ttu-id="c231d-116">응용 프로그램을 닫지 않으면 데이터가 손실될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c231d-116">Not closing the application might result in data loss.</span></span>
* <span data-ttu-id="c231d-117">Azure RemoteApp에서 사용하기 전에 사용자 지정 응용 프로그램의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="c231d-117">Validate custom applications before using them in Azure RemoteApp.</span></span> <span data-ttu-id="c231d-118">여기에는 다중 세션 플랫폼에서 작동하는지, 그리고 동일한 컬렉션의 다른 사용자가 이용할 수 없도록 메모리, CPU 등의 리소스를 불필요하게 소모하지 않는지 확인하는 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c231d-118">This includes ensuring they work on a multi-session platform and don’t consume unnecessary resources such as memory and CPU that might starve another user in the same collection.</span></span> <span data-ttu-id="c231d-119">자세한 내용을 보려면 [원격 데스크톱 서비스에 대한 응용 프로그램 호환성 모범 사례](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf)를 다운로드하여 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="c231d-119">For information, download and review the [Application Compatibility Best Practices for Remote Desktop Services](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).</span></span>

## <a name="configuration-and-management"></a><span data-ttu-id="c231d-120">구성 및 관리</span><span class="sxs-lookup"><span data-stu-id="c231d-120">Configuration and management</span></span>
* <span data-ttu-id="c231d-121">필요에 따라 소프트웨어 업데이트 및 기타 중요 수정 프로그램을 설치하여 템플릿 이미지를 최신 상태로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="c231d-121">Keep your template images up to date, installing software updates and other critical fixes as needed.</span></span> <span data-ttu-id="c231d-122">그러면 Azure RemoteApp이 용량을 충족하기 위해 자동으로 크기를 조정할 때 각 인스턴스에 패치가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c231d-122">This ensures that as Azure RemoteApp auto-scales to meet your capacity, each instance is patched.</span></span>  
* <span data-ttu-id="c231d-123">AD FS(Active Directory Federation Services) 배포가 안전하고 신뢰할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c231d-123">Make sure your Active Directory Federation Services (AD FS) deployment is secure and reliable.</span></span> <span data-ttu-id="c231d-124">그렇지 않으면 클라이언트 인증이 실패하여 사용자가 Azure RemoteApp에 액세스하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c231d-124">Otherwise client authentications might fail, preventing users from accessing Azure RemoteApp.</span></span>
* <span data-ttu-id="c231d-125">설치된 응용 프로그램, 역할 또는 기능이 포함된 템플릿 이미지를 상태 비저장이 되도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c231d-125">Configure template images with installed applications, roles, or features such that they are stateless.</span></span> <span data-ttu-id="c231d-126">RemoteApp 서비스의 가상 컴퓨터 인스턴스가 영구 상태에 있는 것으로 간주해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c231d-126">They should not rely on any instances of the virtual machines in a RemoteApp service being in a persistent state.</span></span>
  * <span data-ttu-id="c231d-127">모든 사용자 데이터를 사용자 프로필이나 서비스 외부의 기타 저장소 위치(예: 온-프레미스 파일 공유 또는 OneDrive)에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c231d-127">Store all user data in user profiles or other storage locations external to the service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="c231d-128">공유 데이터를 서비스 외부의 기타 저장소 위치(예: 온-프레미스 파일 공유 또는 OneDrive)에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c231d-128">Store shared data in storage locations external to the service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="c231d-129">서비스의 개별 가상 컴퓨터 대신 템플릿 이미지에서 시스템 수준 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c231d-129">Configure any system-wide settings in the template image rather than on individual virtual machines in a service.</span></span>
  * <span data-ttu-id="c231d-130">게시된 응용 프로그램의 자동 소프트웨어 업데이트를 사용하지 않도록 설정합니다. 대신 이 응용 프로그램을 템플릿 이미지에 수동으로 적용하고, 템플릿에서 배포하기 전에 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c231d-130">Disable automatic software updates for published applications - instead apply them manually to the template image and test them before you deploy  from the template.</span></span>

