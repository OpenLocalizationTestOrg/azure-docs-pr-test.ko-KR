---
title: "Azure RemoteApp 이미지 요구 사항 | Microsoft Docs"
description: "RemoteApp과 함께 사용할 이미지를 만들기 위한 요구 사항 알아보기"
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
ms.openlocfilehash: 75b0f8d6b25a80f11002b683152cfb294cbb68bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a><span data-ttu-id="22297-103">Azure RemoteApp 이미지에 대한 요구 사항</span><span class="sxs-lookup"><span data-stu-id="22297-103">Requirements for Azure RemoteApp images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="22297-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="22297-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="22297-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="22297-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="22297-106">Azure RemoteApp은 Windows Server 2012 R2 이미지를 사용하여 사용자와 공유할 모든 프로그램을 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="22297-106">Azure RemoteApp uses a Windows Server 2012 R2 image to host all the programs that you want to share with your users.</span></span> <span data-ttu-id="22297-107">사용자 지정 이미지를 만들려면, 기존 이미지로 시작하거나 [새 이미지를 만듭니다](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="22297-107">To create a custom image, you can start with an existing image or [create a new one](remoteapp-create-custom-image.md).</span></span>

> [!TIP]
> <span data-ttu-id="22297-108">Azure RemoteApp 구독에서 사용자가 고유의 템플릿 이미지를 만드는데 사용할 수 있는 Azure VM 갤러리의 Windows Server 2012 R2 이미지에 액세스할 수 있다는 사실을 아십니까?</span><span class="sxs-lookup"><span data-stu-id="22297-108">Did you know that your Azure RemoteApp subscription gives you access to a Windows Server 2012 R2 image in the Azure VM gallery that you can use to create your own template image?</span></span> <span data-ttu-id="22297-109">[확인하십시오](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="22297-109">[Check it out](remoteapp-image-on-azurevm.md).</span></span>  
> 
> 

<span data-ttu-id="22297-110">Azure RemoteApp과 사용하기 위해 업로드할 수 있는 이미지의 요구 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="22297-110">The requirements for the image that can be uploaded for use with Azure RemoteApp are:</span></span>

* <span data-ttu-id="22297-111">사용자 지정 응용 프로그램은 이미지에 데이터를 로컬로 저장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22297-111">Custom applications don’t store data locally on the image.</span></span> <span data-ttu-id="22297-112">이러한 이미지는 상태 비저장 방식이며 응용 프로그램만 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22297-112">These images are stateless and should only contain applications.</span></span>
* <span data-ttu-id="22297-113">이미지는 손실될 수 있는 데이터를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22297-113">The image does not contain data that can be lost.</span></span>
* <span data-ttu-id="22297-114">이미지 크기는 MB 단위의 배수여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22297-114">The image size should be a multiple of MBs.</span></span> <span data-ttu-id="22297-115">크기가 정확한 배수가 아닌 이미지는 업로드에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="22297-115">If you try to upload an image that is not an exact multiple, the upload will fail.</span></span>
* <span data-ttu-id="22297-116">이미지 크기는 127GB 이하여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22297-116">The image size must be 127 GB or smaller.</span></span>
* <span data-ttu-id="22297-117">VHD 파일에 있어야 합니다. VHDX 파일은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22297-117">It must be on a VHD file (VHDX files are not currently supported).</span></span>
* <span data-ttu-id="22297-118">VHD는 세대 2 가상 컴퓨터가 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22297-118">The VHD must not be a generation 2 virtual machine.</span></span>
* <span data-ttu-id="22297-119">VHD는 고정 크기이거나 동적으로 확장될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22297-119">The VHD can be either fixed-size or dynamically expanding.</span></span> <span data-ttu-id="22297-120">고정 크기의 VHD 파일보다 Azure에 업로드하는 시간이 짧으므로 동적으로 확장되는 VHD가 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="22297-120">A dynamically expanding VHD is recommended because it takes less time to upload to Azure than a fixed-size VHD file.</span></span>
* <span data-ttu-id="22297-121">디스크는 MBR(마스터 부트 레코드) 파티션 스타일을 사용하여 초기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22297-121">The disk must be initialized using the Master Boot Record (MBR) partitioning style.</span></span> <span data-ttu-id="22297-122">GPT(GUID 파티션 테이블) 파티션 스타일은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22297-122">The GUID partition table (GPT) partition style is not supported.</span></span>
* <span data-ttu-id="22297-123">VHD는 Windows Server 2012 R2의 단일 설치를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22297-123">The VHD must contain a single installation of Windows Server 2012 R2.</span></span> <span data-ttu-id="22297-124">여러 볼륨을 포함할 수 있지만 한 볼륨만 Windows의 설치를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="22297-124">It can contain multiple volumes, but only one that contains an installation of Windows.</span></span>
* <span data-ttu-id="22297-125">RDSH(원격 데스크톱 세션 호스트) 역할 및 데스크톱 경험 기능을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22297-125">The Remote Desktop Session Host (RDSH) role and the Desktop Experience feature must be installed.</span></span>
* <span data-ttu-id="22297-126">원격 데스크톱 연결 브로커 역할은 설치하면 *안 됩니다* .</span><span class="sxs-lookup"><span data-stu-id="22297-126">The Remote Desktop Connection Broker role must *not* be installed.</span></span>
* <span data-ttu-id="22297-127">EFS(파일 시스템 암호화)를 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22297-127">The Encrypting File System (EFS) must be disabled.</span></span>
* <span data-ttu-id="22297-128">이미지는 **/oobe /generalize /shutdown** 매개 변수를 사용하여 SYSPREPed가 되어야 합니다. **/mode:vm** 매개 변수는 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="22297-128">The image must be SYSPREPed using the parameters **/oobe /generalize /shutdown** (DO NOT use the **/mode:vm** parameter).</span></span>
* <span data-ttu-id="22297-129">스냅숏 체인으로부터의 VHD 업로드는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22297-129">Uploading your VHD from a snapshot chain is not supported.</span></span>

<span data-ttu-id="22297-130">Azure RemoteApp에 대한 이미지 만들기에 대한 자세한 내용은 [Azure RemoteApp 이미지 만들기](remoteapp-imageoptions.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22297-130">See [Create an Azure RemoteApp image](remoteapp-imageoptions.md) for more information about creating images for Azure RemoteApp.</span></span>

