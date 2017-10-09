---
title: aaaPublish WebApplicationVM | Microsoft Docs
description: "자세한 내용은 방법 toodeploy 웹 응용 프로그램 tooa 가상 컴퓨터. 이 스크립트는 없는 경우 Azure 구독에서 hello 필요한 리소스를 만듭니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: e4b52b620bebf44b87ddfc3b19c155bb65111814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a><span data-ttu-id="a646a-104">Publish-WebApplicationVM (Windows PowerShell 스크립트)</span><span class="sxs-lookup"><span data-stu-id="a646a-104">Publish-WebApplicationVM (Windows PowerShell script)</span></span>
<span data-ttu-id="a646a-105">웹 응용 프로그램 tooa 가상 컴퓨터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="a646a-105">Deploys a web application tooa virtual machine.</span></span> <span data-ttu-id="a646a-106">hello 스크립트 없는 경우 Azure 구독에 필요한 hello 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a646a-106">hello script creates hello required resources in your Azure subscription if they don't exist.</span></span>

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a><span data-ttu-id="a646a-107">구성</span><span class="sxs-lookup"><span data-stu-id="a646a-107">Configuration</span></span>
<span data-ttu-id="a646a-108">hello 경로 toohello는 JSON 구성 파일 hello 배포의 hello 세부 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a646a-108">hello path toohello JSON configuration file that describes hello details of hello deployment.</span></span>

| <span data-ttu-id="a646a-109">Aliases</span><span class="sxs-lookup"><span data-stu-id="a646a-109">Aliases</span></span> | <span data-ttu-id="a646a-110">없음</span><span class="sxs-lookup"><span data-stu-id="a646a-110">none</span></span> |
| --- | --- |
| <span data-ttu-id="a646a-111">Required?</span><span class="sxs-lookup"><span data-stu-id="a646a-111">Required?</span></span> |<span data-ttu-id="a646a-112">true</span><span class="sxs-lookup"><span data-stu-id="a646a-112">true</span></span> |
| <span data-ttu-id="a646a-113">Position</span><span class="sxs-lookup"><span data-stu-id="a646a-113">Position</span></span> |<span data-ttu-id="a646a-114">named</span><span class="sxs-lookup"><span data-stu-id="a646a-114">named</span></span> |
| <span data-ttu-id="a646a-115">기본값</span><span class="sxs-lookup"><span data-stu-id="a646a-115">Default value</span></span> |<span data-ttu-id="a646a-116">없음</span><span class="sxs-lookup"><span data-stu-id="a646a-116">none</span></span> |
| <span data-ttu-id="a646a-117">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a646a-117">Accept pipeline input?</span></span> |<span data-ttu-id="a646a-118">false</span><span class="sxs-lookup"><span data-stu-id="a646a-118">false</span></span> |
| <span data-ttu-id="a646a-119">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a646a-119">Accept wildcard characters?</span></span> |<span data-ttu-id="a646a-120">false</span><span class="sxs-lookup"><span data-stu-id="a646a-120">false</span></span> |

### <a name="subscriptionname"></a><span data-ttu-id="a646a-121">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="a646a-121">SubscriptionName</span></span>
<span data-ttu-id="a646a-122">hello 이름 hello toocreate hello 가상 컴퓨터를 원하는 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="a646a-122">hello name of hello Azure subscription in which you want toocreate hello virtual machine.</span></span>

| <span data-ttu-id="a646a-123">Aliases</span><span class="sxs-lookup"><span data-stu-id="a646a-123">Aliases</span></span> | <span data-ttu-id="a646a-124">없음</span><span class="sxs-lookup"><span data-stu-id="a646a-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="a646a-125">Required?</span><span class="sxs-lookup"><span data-stu-id="a646a-125">Required?</span></span> |<span data-ttu-id="a646a-126">false</span><span class="sxs-lookup"><span data-stu-id="a646a-126">false</span></span> |
| <span data-ttu-id="a646a-127">Position</span><span class="sxs-lookup"><span data-stu-id="a646a-127">Position</span></span> |<span data-ttu-id="a646a-128">named</span><span class="sxs-lookup"><span data-stu-id="a646a-128">named</span></span> |
| <span data-ttu-id="a646a-129">기본값</span><span class="sxs-lookup"><span data-stu-id="a646a-129">Default value</span></span> |<span data-ttu-id="a646a-130">Hello 구독 파일의 첫 번째 구독 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a646a-130">Uses hello first subscription in hello subscription file</span></span> |
| <span data-ttu-id="a646a-131">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a646a-131">Accept pipeline input?</span></span> |<span data-ttu-id="a646a-132">false</span><span class="sxs-lookup"><span data-stu-id="a646a-132">false</span></span> |
| <span data-ttu-id="a646a-133">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a646a-133">Accept wildcard characters?</span></span> |<span data-ttu-id="a646a-134">false</span><span class="sxs-lookup"><span data-stu-id="a646a-134">false</span></span> |

### <a name="webdeploypackage"></a><span data-ttu-id="a646a-135">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="a646a-135">WebDeployPackage</span></span>
<span data-ttu-id="a646a-136">hello 경로 toohello 웹 배포 패키지 toopublish toohello 가상 컴퓨터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a646a-136">hello path toohello web deployment package toopublish toohello virtual machine.</span></span> <span data-ttu-id="a646a-137">Visual Studio에서 hello 웹 게시 마법사를 사용 하 여이 패키지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a646a-137">You can create this package by using hello Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="a646a-138">[방법: Visual Studio에서 웹 배포 패키지 만들기](https://msdn.microsoft.com/library/dd465323.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a646a-138">See [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span>

| <span data-ttu-id="a646a-139">Aliases</span><span class="sxs-lookup"><span data-stu-id="a646a-139">Aliases</span></span> | <span data-ttu-id="a646a-140">없음</span><span class="sxs-lookup"><span data-stu-id="a646a-140">none</span></span> |
| --- | --- |
| <span data-ttu-id="a646a-141">Required?</span><span class="sxs-lookup"><span data-stu-id="a646a-141">Required?</span></span> |<span data-ttu-id="a646a-142">false</span><span class="sxs-lookup"><span data-stu-id="a646a-142">false</span></span> |
| <span data-ttu-id="a646a-143">Position</span><span class="sxs-lookup"><span data-stu-id="a646a-143">Position</span></span> |<span data-ttu-id="a646a-144">named</span><span class="sxs-lookup"><span data-stu-id="a646a-144">named</span></span> |
| <span data-ttu-id="a646a-145">기본값</span><span class="sxs-lookup"><span data-stu-id="a646a-145">Default value</span></span> |<span data-ttu-id="a646a-146">없음</span><span class="sxs-lookup"><span data-stu-id="a646a-146">none</span></span> |
| <span data-ttu-id="a646a-147">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a646a-147">Accept pipeline input?</span></span> |<span data-ttu-id="a646a-148">false</span><span class="sxs-lookup"><span data-stu-id="a646a-148">false</span></span> |
| <span data-ttu-id="a646a-149">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a646a-149">Accept wildcard characters?</span></span> |<span data-ttu-id="a646a-150">false</span><span class="sxs-lookup"><span data-stu-id="a646a-150">false</span></span> |

### <a name="allowuntrusted"></a><span data-ttu-id="a646a-151">AllowUntrusted</span><span class="sxs-lookup"><span data-stu-id="a646a-151">AllowUntrusted</span></span>
<span data-ttu-id="a646a-152">True 인 경우에 신뢰할 수 있는 루트 인증 기관에서 서명 하지 않은 인증서 hello 사용할을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a646a-152">If true, allow hello use of certificates that aren't signed by a trusted root authority.</span></span>

| <span data-ttu-id="a646a-153">Aliases</span><span class="sxs-lookup"><span data-stu-id="a646a-153">Aliases</span></span> | <span data-ttu-id="a646a-154">없음</span><span class="sxs-lookup"><span data-stu-id="a646a-154">none</span></span> |
| --- | --- |
| <span data-ttu-id="a646a-155">Required?</span><span class="sxs-lookup"><span data-stu-id="a646a-155">Required?</span></span> |<span data-ttu-id="a646a-156">false</span><span class="sxs-lookup"><span data-stu-id="a646a-156">false</span></span> |
| <span data-ttu-id="a646a-157">Position</span><span class="sxs-lookup"><span data-stu-id="a646a-157">Position</span></span> |<span data-ttu-id="a646a-158">named</span><span class="sxs-lookup"><span data-stu-id="a646a-158">named</span></span> |
| <span data-ttu-id="a646a-159">기본값</span><span class="sxs-lookup"><span data-stu-id="a646a-159">Default value</span></span> |<span data-ttu-id="a646a-160">false</span><span class="sxs-lookup"><span data-stu-id="a646a-160">false</span></span> |
| <span data-ttu-id="a646a-161">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a646a-161">Accept pipeline input?</span></span> |<span data-ttu-id="a646a-162">false</span><span class="sxs-lookup"><span data-stu-id="a646a-162">false</span></span> |
| <span data-ttu-id="a646a-163">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a646a-163">Accept wildcard characters?</span></span> |<span data-ttu-id="a646a-164">false</span><span class="sxs-lookup"><span data-stu-id="a646a-164">false</span></span> |

### <a name="vmpassword"></a><span data-ttu-id="a646a-165">VMPassword</span><span class="sxs-lookup"><span data-stu-id="a646a-165">VMPassword</span></span>
<span data-ttu-id="a646a-166">hello 가상 컴퓨터 계정에 대 한 hello 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="a646a-166">hello credentials for hello virtual machine account.</span></span> <span data-ttu-id="a646a-167">예: VMPassword @{Name = "admin"; 암호 = "password"}</span><span class="sxs-lookup"><span data-stu-id="a646a-167">Example: -VMPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="a646a-168">Aliases</span><span class="sxs-lookup"><span data-stu-id="a646a-168">Aliases</span></span> | <span data-ttu-id="a646a-169">없음</span><span class="sxs-lookup"><span data-stu-id="a646a-169">none</span></span> |
| --- | --- |
| <span data-ttu-id="a646a-170">Required?</span><span class="sxs-lookup"><span data-stu-id="a646a-170">Required?</span></span> |<span data-ttu-id="a646a-171">false</span><span class="sxs-lookup"><span data-stu-id="a646a-171">false</span></span> |
| <span data-ttu-id="a646a-172">Position</span><span class="sxs-lookup"><span data-stu-id="a646a-172">Position</span></span> |<span data-ttu-id="a646a-173">named</span><span class="sxs-lookup"><span data-stu-id="a646a-173">named</span></span> |
| <span data-ttu-id="a646a-174">기본값</span><span class="sxs-lookup"><span data-stu-id="a646a-174">Default value</span></span> |<span data-ttu-id="a646a-175">없음</span><span class="sxs-lookup"><span data-stu-id="a646a-175">none</span></span> |
| <span data-ttu-id="a646a-176">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a646a-176">Accept pipeline input?</span></span> |<span data-ttu-id="a646a-177">false</span><span class="sxs-lookup"><span data-stu-id="a646a-177">false</span></span> |
| <span data-ttu-id="a646a-178">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a646a-178">Accept wildcard characters?</span></span> |<span data-ttu-id="a646a-179">false</span><span class="sxs-lookup"><span data-stu-id="a646a-179">false</span></span> |

### <a name="databaseserverpassword"></a><span data-ttu-id="a646a-180">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="a646a-180">DatabaseServerPassword</span></span>
<span data-ttu-id="a646a-181">Azure의 hello SQL 데이터베이스에 대 한 hello 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="a646a-181">hello credentials for hello SQL database in Azure.</span></span> <span data-ttu-id="a646a-182">예: DatabaseServerPassword @{Name = "admin"; 암호 = "password"}</span><span class="sxs-lookup"><span data-stu-id="a646a-182">Example: -DatabaseServerPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="a646a-183">Aliases</span><span class="sxs-lookup"><span data-stu-id="a646a-183">Aliases</span></span> | <span data-ttu-id="a646a-184">없음</span><span class="sxs-lookup"><span data-stu-id="a646a-184">none</span></span> |
| --- | --- |
| <span data-ttu-id="a646a-185">Required?</span><span class="sxs-lookup"><span data-stu-id="a646a-185">Required?</span></span> |<span data-ttu-id="a646a-186">false</span><span class="sxs-lookup"><span data-stu-id="a646a-186">false</span></span> |
| <span data-ttu-id="a646a-187">Position</span><span class="sxs-lookup"><span data-stu-id="a646a-187">Position</span></span> |<span data-ttu-id="a646a-188">named</span><span class="sxs-lookup"><span data-stu-id="a646a-188">named</span></span> |
| <span data-ttu-id="a646a-189">기본값</span><span class="sxs-lookup"><span data-stu-id="a646a-189">Default value</span></span> |<span data-ttu-id="a646a-190">없음</span><span class="sxs-lookup"><span data-stu-id="a646a-190">none</span></span> |
| <span data-ttu-id="a646a-191">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a646a-191">Accept pipeline input?</span></span> |<span data-ttu-id="a646a-192">false</span><span class="sxs-lookup"><span data-stu-id="a646a-192">false</span></span> |
| <span data-ttu-id="a646a-193">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a646a-193">Accept wildcard characters?</span></span> |<span data-ttu-id="a646a-194">false</span><span class="sxs-lookup"><span data-stu-id="a646a-194">false</span></span> |

### <a name="sendhostmessagestooutput"></a><span data-ttu-id="a646a-195">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="a646a-195">SendHostMessagesToOutput</span></span>
<span data-ttu-id="a646a-196">True 이면 hello 스크립트 toohello에서 메시지를 인쇄 출력 스트림에입니다.</span><span class="sxs-lookup"><span data-stu-id="a646a-196">If true, print messages from hello script toohello output stream.</span></span>

| <span data-ttu-id="a646a-197">Aliases</span><span class="sxs-lookup"><span data-stu-id="a646a-197">Aliases</span></span> | <span data-ttu-id="a646a-198">없음</span><span class="sxs-lookup"><span data-stu-id="a646a-198">none</span></span> |
| --- | --- |
| <span data-ttu-id="a646a-199">Required?</span><span class="sxs-lookup"><span data-stu-id="a646a-199">Required?</span></span> |<span data-ttu-id="a646a-200">false</span><span class="sxs-lookup"><span data-stu-id="a646a-200">false</span></span> |
| <span data-ttu-id="a646a-201">Position</span><span class="sxs-lookup"><span data-stu-id="a646a-201">Position</span></span> |<span data-ttu-id="a646a-202">named</span><span class="sxs-lookup"><span data-stu-id="a646a-202">named</span></span> |
| <span data-ttu-id="a646a-203">기본값</span><span class="sxs-lookup"><span data-stu-id="a646a-203">Default value</span></span> |<span data-ttu-id="a646a-204">false</span><span class="sxs-lookup"><span data-stu-id="a646a-204">false</span></span> |
| <span data-ttu-id="a646a-205">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a646a-205">Accept pipeline input?</span></span> |<span data-ttu-id="a646a-206">false</span><span class="sxs-lookup"><span data-stu-id="a646a-206">false</span></span> |
| <span data-ttu-id="a646a-207">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a646a-207">Accept wildcard characters?</span></span> |<span data-ttu-id="a646a-208">false</span><span class="sxs-lookup"><span data-stu-id="a646a-208">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="a646a-209">설명</span><span class="sxs-lookup"><span data-stu-id="a646a-209">Remarks</span></span>
<span data-ttu-id="a646a-210">자세한 설명은 toouse hello 스크립트 toocreate 개발 및 테스트 환경을 참조 하는 방법에 대 한 [Windows PowerShell 스크립트를 사용 하 여 tooPublish tooDev 및 시험 환경](vs-azure-tools-publishing-using-powershell-scripts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a646a-210">For a complete explanation of how toouse hello script toocreate Dev and Test environments, see [Using Windows PowerShell Scripts tooPublish tooDev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="a646a-211">hello JSON 구성 파일의 배포 toobe 이란 hello 세부 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a646a-211">hello JSON configuration file specifies hello details of what is toobe deployed.</span></span> <span data-ttu-id="a646a-212">Hello 이름, 선호도 그룹, VHD 이미지 및 hello 가상 컴퓨터의 크기와 같은 hello 프로젝트를 만들 때 지정한 hello 정보가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a646a-212">It includes hello information that you specified when you created hello project, such as hello name, affinity group, VHD image, and size of hello virtual machine.</span></span> <span data-ttu-id="a646a-213">도 있는 경우 hello 끝점 hello 데이터베이스 tooprovision hello 가상 컴퓨터를 포함 하 고 웹 배포 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="a646a-213">It also includes hello endpoints on hello virtual machine, hello databases tooprovision, if any, and web deployment parameters.</span></span> <span data-ttu-id="a646a-214">hello 코드 다음 JSON 구성 파일을 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a646a-214">hello following code shows an example JSON configuration file:</span></span>

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

<span data-ttu-id="a646a-215">프로 비전 된 hello JSON 구성 파일 toochange를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a646a-215">You can edit hello JSON configuration file toochange what is provisioned.</span></span> <span data-ttu-id="a646a-216">가상 컴퓨터 및 클라우드 서비스 필요 하지만 hello 데이터베이스 섹션은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="a646a-216">A virtual machine and a cloud service are required, but hello database section is optional.</span></span>

