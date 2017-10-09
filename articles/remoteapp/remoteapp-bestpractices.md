---
title: "aaaAzure RemoteApp에 대 한 유용한 정보 | Microsoft Docs"
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
ms.openlocfilehash: f4d09ef30816eaebb74b69f26f3242c69ea27591
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a><span data-ttu-id="c8e62-103">Azure RemoteApp 구성 및 사용 모범 사례</span><span class="sxs-lookup"><span data-stu-id="c8e62-103">Best practices for configuring and using Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c8e62-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="c8e62-105">읽기 hello [알림](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-105">Read hello [announcement](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) for details.</span></span>
> 
> 

<span data-ttu-id="c8e62-106">다음 정보는 hello 구성 및 Azure RemoteApp을 생산적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-106">hello following information can help you configure and use Azure RemoteApp productively.</span></span>

## <a name="connectivity"></a><span data-ttu-id="c8e62-107">연결</span><span class="sxs-lookup"><span data-stu-id="c8e62-107">Connectivity</span></span>
* <span data-ttu-id="c8e62-108">항상 hello 최신 클라이언트 버전을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-108">Always use hello latest client version.</span></span> <span data-ttu-id="c8e62-109">이전 클라이언트를 사용하면 연결 문제 및 기타 성능 저하가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-109">Using older clients might result in connectivity issues and other degraded experiences.</span></span> <span data-ttu-id="c8e62-110">장치에 대 한 자동 응용 프로그램 업데이트를 사용 하도록 설정 하면 해당 hello 최신 클라이언트는 항상 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-110">Enabling automatic application updates for your device will ensure that hello latest client is always installed.</span></span>
* <span data-ttu-id="c8e62-111">Hello 가장 안정적이 고 신뢰할 수 있는 인터넷 연결 사용 가능한 tooyou를 항상 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-111">Always use hello most stable and reliable internet connection available tooyou.</span></span>  
* <span data-ttu-id="c8e62-112">최적 연결 성능을 위해 지원되는 프록시 연결만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-112">Use only supported proxy connections for optimal connectivity performance.</span></span>  <span data-ttu-id="c8e62-113">hello SOCKS 프록시 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-113">hello SOCKS proxy is not supported.</span></span>

## <a name="applications"></a><span data-ttu-id="c8e62-114">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="c8e62-114">Applications</span></span>
* <span data-ttu-id="c8e62-115">저장 하 고 hello 응용 프로그램으로 작업할 때 RemoteApp 응용 프로그램을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-115">Save and close RemoteApp applications when you are done with hello application.</span></span> <span data-ttu-id="c8e62-116">하지 hello 응용 프로그램을 닫으면 데이터 손실이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-116">Not closing hello application might result in data loss.</span></span>
* <span data-ttu-id="c8e62-117">Azure RemoteApp에서 사용하기 전에 사용자 지정 응용 프로그램의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-117">Validate custom applications before using them in Azure RemoteApp.</span></span> <span data-ttu-id="c8e62-118">여기에 다중 세션 플랫폼에서 작동 하 고 다른 사용자 hello에 메모리가 부족할 수 있는 CPU 메모리 등의 불필요 한 리소스를 소비 하지은 동일한 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-118">This includes ensuring they work on a multi-session platform and don’t consume unnecessary resources such as memory and CPU that might starve another user in hello same collection.</span></span> <span data-ttu-id="c8e62-119">정보를 다운로드 하 고 hello 검토 [원격 데스크톱 서비스에 대 한 응용 프로그램 호환성 모범 사례](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf)합니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-119">For information, download and review hello [Application Compatibility Best Practices for Remote Desktop Services](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).</span></span>

## <a name="configuration-and-management"></a><span data-ttu-id="c8e62-120">구성 및 관리</span><span class="sxs-lookup"><span data-stu-id="c8e62-120">Configuration and management</span></span>
* <span data-ttu-id="c8e62-121">필요에 따라 소프트웨어 업데이트 및 기타 주요 수정 프로그램을 설치 toodate 템플릿 이미지를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-121">Keep your template images up toodate, installing software updates and other critical fixes as needed.</span></span> <span data-ttu-id="c8e62-122">이렇게 하면으로 Azure RemoteApp 자동 눈금 toomeet 용량, 각 인스턴스 패치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-122">This ensures that as Azure RemoteApp auto-scales toomeet your capacity, each instance is patched.</span></span>  
* <span data-ttu-id="c8e62-123">AD FS(Active Directory Federation Services) 배포가 안전하고 신뢰할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-123">Make sure your Active Directory Federation Services (AD FS) deployment is secure and reliable.</span></span> <span data-ttu-id="c8e62-124">그렇지 않으면 클라이언트 인증이 실패하여 사용자가 Azure RemoteApp에 액세스하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-124">Otherwise client authentications might fail, preventing users from accessing Azure RemoteApp.</span></span>
* <span data-ttu-id="c8e62-125">설치된 응용 프로그램, 역할 또는 기능이 포함된 템플릿 이미지를 상태 비저장이 되도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-125">Configure template images with installed applications, roles, or features such that they are stateless.</span></span> <span data-ttu-id="c8e62-126">하지 hello 영구 상태로 RemoteApp 서비스 가상 컴퓨터의 모든 인스턴스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-126">They should not rely on any instances of hello virtual machines in a RemoteApp service being in a persistent state.</span></span>
  * <span data-ttu-id="c8e62-127">온-프레미스 파일 공유 나 OneDrive와 같은 사용자 프로필 또는 다른 저장소 위치 외부 toohello 서비스의 모든 사용자 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-127">Store all user data in user profiles or other storage locations external toohello service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="c8e62-128">온-프레미스 파일 공유 나 OneDrive와 같은 공유 데이터 저장소 위치 외부 toohello 서비스에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-128">Store shared data in storage locations external toohello service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="c8e62-129">서비스에서 개별 가상 컴퓨터 대신 hello 템플릿 이미지에 모든 시스템 수준 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-129">Configure any system-wide settings in hello template image rather than on individual virtual machines in a service.</span></span>
  * <span data-ttu-id="c8e62-130">게시 된 응용 프로그램에 대 한 자동 소프트웨어 업데이트 사용 안 함-대신 수동으로 적용 toohello 템플릿 이미지 및 hello 서식 파일에서 배포 하기 전에 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8e62-130">Disable automatic software updates for published applications - instead apply them manually toohello template image and test them before you deploy  from hello template.</span></span>

