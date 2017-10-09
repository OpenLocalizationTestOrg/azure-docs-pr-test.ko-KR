---
title: "aaaAzure RemoteApp 이미지 요구 사항 | Microsoft Docs"
description: "Azure RemoteApp과 함께 사용 되는 이미지 toobe를 만들기 위한 hello 요구 사항에 알아보기"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7cbb90f4-6dc9-462c-a429-088cdb57414e
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 4e35203eb93a866d4e0bd591d42b34746c7ffa4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a><span data-ttu-id="c8821-103">Azure RemoteApp 이미지에 대한 요구 사항</span><span class="sxs-lookup"><span data-stu-id="c8821-103">Requirements for Azure RemoteApp images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c8821-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c8821-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="c8821-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8821-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="c8821-106">Azure RemoteApp에서 사용자와 tooshare 되도록 모든 hello 프로그램 Windows Server 2012 R2 이미지 toohost를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8821-106">Azure RemoteApp uses a Windows Server 2012 R2 image toohost all hello programs that you want tooshare with your users.</span></span> <span data-ttu-id="c8821-107">사용자 지정 이미지 toocreate 기존 이미지로 시작할 수 있습니다 또는 [새로 만들](remoteapp-create-custom-image.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c8821-107">toocreate a custom image, you can start with an existing image or [create a new one](remoteapp-create-custom-image.md).</span></span>

> [!TIP]
> <span data-ttu-id="c8821-108">에 Azure RemoteApp 구독 액세스할 수 있도록 tooa Windows Server 2012 R2 이미지를 사용할 수 있는 toocreate 사용자 고유의 템플릿 이미지는 Azure VM 갤러리 hello 있는지 알고 계십니까?</span><span class="sxs-lookup"><span data-stu-id="c8821-108">Did you know that your Azure RemoteApp subscription gives you access tooa Windows Server 2012 R2 image in hello Azure VM gallery that you can use toocreate your own template image?</span></span> <span data-ttu-id="c8821-109">[확인하십시오](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="c8821-109">[Check it out](remoteapp-image-on-azurevm.md).</span></span>  
> 
> 

<span data-ttu-id="c8821-110">에 Azure RemoteApp과 함께 사용 하기 위해 업로드할 수 있는 hello 이미지에 대 한 hello 요구 사항:</span><span class="sxs-lookup"><span data-stu-id="c8821-110">hello requirements for hello image that can be uploaded for use with Azure RemoteApp are:</span></span>

* <span data-ttu-id="c8821-111">사용자 지정 응용 프로그램 hello 이미지에 데이터를 로컬로 저장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8821-111">Custom applications don’t store data locally on hello image.</span></span> <span data-ttu-id="c8821-112">이러한 이미지는 상태 비저장 방식이며 응용 프로그램만 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8821-112">These images are stateless and should only contain applications.</span></span>
* <span data-ttu-id="c8821-113">hello 이미지 데이터가 손실 될 수 있는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8821-113">hello image does not contain data that can be lost.</span></span>
* <span data-ttu-id="c8821-114">hello 이미지 크기를 Mb의 배수 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8821-114">hello image size should be a multiple of MBs.</span></span> <span data-ttu-id="c8821-115">Tooupload 정확한 배수가 아닌 이미지에서 하면 hello 업로드가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8821-115">If you try tooupload an image that is not an exact multiple, hello upload will fail.</span></span>
* <span data-ttu-id="c8821-116">hello 이미지 크기는 127GB 이어야 하거나 축소 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8821-116">hello image size must be 127 GB or smaller.</span></span>
* <span data-ttu-id="c8821-117">VHD 파일에 있어야 합니다. VHDX 파일은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8821-117">It must be on a VHD file (VHDX files are not currently supported).</span></span>
* <span data-ttu-id="c8821-118">hello VHD 2 세대 가상 컴퓨터 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c8821-118">hello VHD must not be a generation 2 virtual machine.</span></span>
* <span data-ttu-id="c8821-119">hello VHD는 고정 크기 또는 동적 확장 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8821-119">hello VHD can be either fixed-size or dynamically expanding.</span></span> <span data-ttu-id="c8821-120">크기가 고정 된 VHD 파일 보다 작은 시간 tooupload tooAzure 사용 하기 때문에 동적 확장 VHD 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c8821-120">A dynamically expanding VHD is recommended because it takes less time tooupload tooAzure than a fixed-size VHD file.</span></span>
* <span data-ttu-id="c8821-121">hello 레코드 MBR (마스터 부트) 파티션 스타일을 사용 하 여 hello 디스크를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8821-121">hello disk must be initialized using hello Master Boot Record (MBR) partitioning style.</span></span> <span data-ttu-id="c8821-122">hello GUID 파티션 테이블 (GPT) 파티션 스타일을 사용 하는 것이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c8821-122">hello GUID partition table (GPT) partition style is not supported.</span></span>
* <span data-ttu-id="c8821-123">hello VHD에는 Windows Server 2012 r 2를 설치 하는 단일 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8821-123">hello VHD must contain a single installation of Windows Server 2012 R2.</span></span> <span data-ttu-id="c8821-124">여러 볼륨을 포함할 수 있지만 한 볼륨만 Windows의 설치를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c8821-124">It can contain multiple volumes, but only one that contains an installation of Windows.</span></span>
* <span data-ttu-id="c8821-125">hello RDSH 원격 데스크톱 세션 호스트 () 역할 및 hello 데스크톱 경험 기능을 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8821-125">hello Remote Desktop Session Host (RDSH) role and hello Desktop Experience feature must be installed.</span></span>
* <span data-ttu-id="c8821-126">hello 원격 데스크톱 연결 브로커 역할 해야 *하지* 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8821-126">hello Remote Desktop Connection Broker role must *not* be installed.</span></span>
* <span data-ttu-id="c8821-127">hello 암호화 EFS (파일 시스템) 사용 하지 않도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8821-127">hello Encrypting File System (EFS) must be disabled.</span></span>
* <span data-ttu-id="c8821-128">hello 이미지 있어야 hello 매개 변수를 사용 하 여 SYSPREPed **/oobe /generalize /shutdown** (hello를 사용 하지 않는 **/mode: vm** 매개 변수).</span><span class="sxs-lookup"><span data-stu-id="c8821-128">hello image must be SYSPREPed using hello parameters **/oobe /generalize /shutdown** (DO NOT use hello **/mode:vm** parameter).</span></span>
* <span data-ttu-id="c8821-129">스냅숏 체인으로부터의 VHD 업로드는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8821-129">Uploading your VHD from a snapshot chain is not supported.</span></span>

<span data-ttu-id="c8821-130">Azure RemoteApp에 대한 이미지 만들기에 대한 자세한 내용은 [Azure RemoteApp 이미지 만들기](remoteapp-imageoptions.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8821-130">See [Create an Azure RemoteApp image](remoteapp-imageoptions.md) for more information about creating images for Azure RemoteApp.</span></span>

