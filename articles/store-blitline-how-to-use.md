---
title: "이미지 처리에 Blitline을 사용하는 방법 - Azure 기능 가이드"
description: "Azure 응용 프로그램 내에서 Blitline 서비스를 사용하여 이미지를 처리하는 방법에 대해 알아봅니다."
services: 
documentationcenter: .net
author: blitline-dev
manager: jason@blitline.com
editor: jason@blitline.com
ms.assetid: 6c711248-0e52-4895-ba9e-8395628de924
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2014
ms.author: support@blitline.com
ms.openlocfilehash: 1d90599e028b3407a513b04b878e3aefc39928a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-blitline-with-azure-and-azure-storage"></a><span data-ttu-id="e8ee5-103">Azure 및 Azure 저장소로 Blitline을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="e8ee5-103">How to use Blitline with Azure and Azure Storage</span></span>
<span data-ttu-id="e8ee5-104">이 가이드는 Blitline 서비스를 액세스하는 방법 및 작업을 Blitline에 전송하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-104">This guide will explain how to access Blitline services and how to submit jobs to Blitline.</span></span>

## <a name="what-is-blitline"></a><span data-ttu-id="e8ee5-105">Blitline 정의</span><span class="sxs-lookup"><span data-stu-id="e8ee5-105">What is Blitline?</span></span>
<span data-ttu-id="e8ee5-106">Blitline은 직접 빌드하는 비용보다 훨씬 저렴한 가격으로 엔터프라이즈 수준의 이미지 처리를 제공하는 클라우드 기반 이미지 처리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-106">Blitline is a cloud-based image processing service that provides enterprise level image processing at a fraction of the price that it would cost to build it yourself.</span></span>

<span data-ttu-id="e8ee5-107">사실 이미지 처리는 반복적으로 이루어지며 보통 각 웹 사이트 및 모든 웹 사이트에 대해 완전히 다시 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-107">The fact is that image processing has been done over and over again, usually rebuilt from the ground up for each and every website.</span></span> <span data-ttu-id="e8ee5-108">이미지를 수백만 번 다시 빌드했기 때문에 이러한 사실을 알 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-108">We realize this because we’ve built them a million times too.</span></span> <span data-ttu-id="e8ee5-109">그러다 문득 모든 사용자를 위해 이 작업을 수행하기로 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-109">One day we decided that perhaps it‘s time we just do it for everyone.</span></span> <span data-ttu-id="e8ee5-110">작업하는 방법 및 빠르고 효율적으로 하는 방법을 알고 있으며 동시에 모든 작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-110">We know how to do it, to do it fast and efficiently, and save everyone work in the meantime.</span></span>

<span data-ttu-id="e8ee5-111">자세한 내용은 [http://www.blitline.com](http://www.blitline.com)(영문)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-111">For more information, see [http://www.blitline.com](http://www.blitline.com).</span></span>

## <a name="what-blitline-is-not"></a><span data-ttu-id="e8ee5-112">Blitline이 수행할 수 없는 작업</span><span class="sxs-lookup"><span data-stu-id="e8ee5-112">What Blitline is NOT...</span></span>
<span data-ttu-id="e8ee5-113">계속 진행하기 전에 Blitline이 수행할 수 없는 작업을 확인하는 것이 Blitline이 유용한 이유를 명확하게 하는 데 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-113">To clarify what Blitline is useful for, it is often easier to identify what Blitline does NOT do before moving forward.</span></span>

* <span data-ttu-id="e8ee5-114">Blitline에는 이미지를 업로드할 HTML 위젯이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-114">Blitline does NOT have HTML widgets to upload images.</span></span> <span data-ttu-id="e8ee5-115">공개적으로 사용할 수 있는 이미지를 가지고 있거나 Blitline가 접근할 수 있는 제한된 권한을 가진 이미지를 가지고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-115">You must have images available publicly or with restricted permissions available for Blitline to reach.</span></span>
* <span data-ttu-id="e8ee5-116">Blitline은 Aviary.com처럼 라이브로 이미지를 처리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-116">Blitline does NOT do live image processing, like Aviary.com</span></span>
* <span data-ttu-id="e8ee5-117">Blitline은 이미지 업로드를 허용하지 않아 이미지를 Blitline에 직접 푸시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-117">Blitline does NOT accept image uploads, you cannot push your images to Blitline directly.</span></span> <span data-ttu-id="e8ee5-118">이미지를 Azure 저장소에 푸시하거나 Blitline이 지원하는 다른 위치에 푸시한 다음 Blitline에 그 위치를 알려주어 가져올 수 있게 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-118">You must push them to Azure Storage or other places Blitline supports and then tell Blitline where to go get them.</span></span>
* <span data-ttu-id="e8ee5-119">Blitline은 대량 병렬식이어서 동기식 처리를 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-119">Blitline is massively parallel and does NOT do any synchronous processing.</span></span> <span data-ttu-id="e8ee5-120">즉, postback_url을 보내주어야 처리가 완료되는 시점을 알려줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-120">Meaning you must give us a postback_url and we can tell you when we are done processing.</span></span>

## <a name="create-a-blitline-account"></a><span data-ttu-id="e8ee5-121">Blitline 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="e8ee5-121">Create a Blitline account</span></span>
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-to-create-a-blitline-job"></a><span data-ttu-id="e8ee5-122">Blitline 작업을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="e8ee5-122">How to create a Blitline job</span></span>
<span data-ttu-id="e8ee5-123">Blitline은 JSON을 사용하여 이미지에 적용할 동작을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-123">Blitline uses JSON to define the actions you want to take on an image.</span></span> <span data-ttu-id="e8ee5-124">이 JSON은 간단한 필드 몇 개로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-124">This JSON is composed of a few simple fields.</span></span>

<span data-ttu-id="e8ee5-125">다음은 가장 간단한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-125">The simplest example is as follows:</span></span>

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

<span data-ttu-id="e8ee5-126">이 JSON에서는 "src" 이미지 "...boys.jpeg"을 사용한 다음 그 이미지 크기를 240x140으로 다시 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-126">Here we have JSON that will take a "src" image "...boys.jpeg" and then resize that image to 240x140.</span></span>

<span data-ttu-id="e8ee5-127">응용 프로그램 ID는 Azure의 **연결 정보** 또는 **관리** 탭에서 찾을 수 있는 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-127">The Application ID is something you can find in your **CONNECTION INFO** or **MANAGE** tab on Azure.</span></span> <span data-ttu-id="e8ee5-128">Blitline에서 작업을 실행할 수 있도록 해주는 비밀 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-128">It is your secret identifier that allows you to run jobs on Blitline.</span></span>

<span data-ttu-id="e8ee5-129">"save" 매개 변수는 처리한 이미지를 저장할 위치에 대한 정보를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-129">The "save" parameter identifies information about where you want to put the image once we have processed it.</span></span> <span data-ttu-id="e8ee5-130">간단한 이 경우에서는 정의하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-130">In this trivial case, we haven't defined one.</span></span> <span data-ttu-id="e8ee5-131">위치를 정의하지 않으면 Blitline은 고유 클라우드 위치에 이미지를 로컬로(및 일시적으로) 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-131">If no location is defined Blitline will store it locally (and temporarily) at a unique cloud location.</span></span> <span data-ttu-id="e8ee5-132">Blitline을 만들 때 Blitline이 반환한 JSON에서 그 위치를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-132">You will be able to get that location from the JSON returned by Blitline when you make the Blitline.</span></span> <span data-ttu-id="e8ee5-133">"image" 식별자는 필수이며 저장된 이 특정 이미지를 식별할 때 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-133">The "image" identifier is required and is returned to you when to identify this particular saved image.</span></span>

<span data-ttu-id="e8ee5-134">여기서 지원하는 *함수*에 대한 자세한 정보는 다음에서 찾을 수 있습니다. <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="e8ee5-134">You can find more information about the *functions* we support here: <http://www.blitline.com/docs/functions></span></span>

<span data-ttu-id="e8ee5-135">또한 여기서 나온 작업 옵션에 대한 설명서는 다음에서 찾을 수 있습니다. <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="e8ee5-135">You can also find documentation about the job options here: <http://www.blitline.com/docs/api></span></span>

<span data-ttu-id="e8ee5-136">JSON이 있으면 `http://api.blitline.com/job`에 **게시**하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-136">Once you have your JSON all you need to do is **POST** it to `http://api.blitline.com/job`</span></span>

<span data-ttu-id="e8ee5-137">다음과 유사한 JSON이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-137">You will get JSON back that looks something like this:</span></span>

    {
     "results":
         {"images":
            [{
              "image_identifier":"external_sample_1",
              "s3_url":"https://s3.amazonaws.com/dev.blitline/2011110722/YOUR_APP_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg"
            }],
          "job_id":"4eb8c9f72a50ee2a9900002f"
         }
    }


<span data-ttu-id="e8ee5-138">이는 Blitline에서 요청을 받았음을 나타내고 그 요청을 처리 큐에 넣은 후 완료되면 다음에서 이미지를 사용할 수 있습니다. **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg**</span><span class="sxs-lookup"><span data-stu-id="e8ee5-138">This tells you that Blitline has recieved your request, it has put it in a processing queue, and when it has completed the image will be available at: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg**</span></span>

## <a name="how-to-save-an-image-to-your-azure-storage-account"></a><span data-ttu-id="e8ee5-139">Azure 저장소 계정에 이미지를 저장하는 방법</span><span class="sxs-lookup"><span data-stu-id="e8ee5-139">How to save an image to your Azure Storage account</span></span>
<span data-ttu-id="e8ee5-140">Azure 저장소 계정이 있으면 Blitline이 처리된 이미지를 쉽게 Azure 컨테이너에 푸시하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-140">If you have an Azure Storage account, you can easily have Blitline push the processed images into your Azure container.</span></span> <span data-ttu-id="e8ee5-141">"azure_destination"을 추가하여 푸시할 Blitline의 위치와 권한을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-141">By adding an "azure_destination" you define the location and permissions for Blitline to push to.</span></span>

<span data-ttu-id="e8ee5-142">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-142">Here is an example:</span></span>

    job : '{
      "application_id": "YOUR_APP_ID",
      "src" : "http://www.google.com/logos/2011/houdini11-hp.jpg",
         "functions" : [{
         "name": "blur",
         "save" : {
             "image_identifier" : "YOUR_IMAGE_IDENTIFIER",
             "azure_destination" : {
                 "account_name" : "YOUR_AZURE_CONTAINER_NAME",
                 "shared_access_signature" : "SAS_THAT_GIVES_BLITLINE_PERMISSION_TO_WRITE_THIS_OBJECT_TO_CONTAINER",
               }
           }
         }]
       }'


<span data-ttu-id="e8ee5-143">CAPITALIZED 값을 자체 값으로 채우면 이 JSON을 http://api.blitline.com/job에 제출할 수 있으며 "src" 이미지가 흐리게 하는 필터로 처리된 다음 Azure 대상에 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-143">By filling in the CAPITALIZED values with your own, you can submit this JSON to http://api.blitline.com/job and the "src" image will be processed with a blur filter and then pushed to you Azure destination.</span></span>

### <a name="please-note"></a><span data-ttu-id="e8ee5-144">참고:</span><span class="sxs-lookup"><span data-stu-id="e8ee5-144">Please note:</span></span>
<span data-ttu-id="e8ee5-145">SAS에는 대상 파일의 파일 이름을 포함하여 전체 SAS URL이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-145">The SAS must contain the entire SAS url, including the filename of the destination file.</span></span>

<span data-ttu-id="e8ee5-146">예제:</span><span class="sxs-lookup"><span data-stu-id="e8ee5-146">Example:</span></span>

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


<span data-ttu-id="e8ee5-147">Blitline의 Azure 저장소 문서의 최신 버전을 [여기](http://www.blitline.com/docs/azure_storage)에서 읽을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-147">You can also read the latest edition of Blitline's Azure Storage docs [here](http://www.blitline.com/docs/azure_storage).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8ee5-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e8ee5-148">Next Steps</span></span>
<span data-ttu-id="e8ee5-149">다른 모든 기능에 대한 내용을 보려면 다음 blitline.com을 방문하십시오.</span><span class="sxs-lookup"><span data-stu-id="e8ee5-149">Visit blitline.com to read about all our other features:</span></span>

* <span data-ttu-id="e8ee5-150">Blitline API 끝점 문서 <http://www.blitline.com/docs/api>(영문)</span><span class="sxs-lookup"><span data-stu-id="e8ee5-150">Blitline API Endpoint Docs <http://www.blitline.com/docs/api></span></span>
* <span data-ttu-id="e8ee5-151">Blitline API 함수 <http://www.blitline.com/docs/functions>(영문)</span><span class="sxs-lookup"><span data-stu-id="e8ee5-151">Blitline API Functions <http://www.blitline.com/docs/functions></span></span>
* <span data-ttu-id="e8ee5-152">Blitline API 예제 <http://www.blitline.com/docs/examples>(영문)</span><span class="sxs-lookup"><span data-stu-id="e8ee5-152">Blitline API Examples <http://www.blitline.com/docs/examples></span></span>
* <span data-ttu-id="e8ee5-153">타사 Nuget 라이브러리 <http://nuget.org/packages/Blitline.Net>(영문)</span><span class="sxs-lookup"><span data-stu-id="e8ee5-153">Third Part Nuget Library <http://nuget.org/packages/Blitline.Net></span></span>

