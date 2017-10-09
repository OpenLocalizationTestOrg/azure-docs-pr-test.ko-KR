---
title: "Azure 논리 앱 워크플로-에서 메시지를 XML로 aaaWorking | Microsoft Docs"
description: "처리, 유효성 검사, 변환 및 보강 XML 메시지에서 비즈니스 tooscenarios 사용 하 여 논리 앱 hello 엔터프라이즈 통합 팩"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 47672dc4-1caa-44e5-b8cb-68ec3a76b7dc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 02/27/2017
ms.author: LADocs; mandia
ms.openlocfilehash: f90ae89fef0a4bd17286adbce398e573940bb790
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a><span data-ttu-id="e73fc-103">논리 앱에서 XML 유효성을 검사 및 변환하고, 플랫 파일을 인코딩 및 디코딩하며, 메시지 기능 보강</span><span class="sxs-lookup"><span data-stu-id="e73fc-103">Validate and transform XML, encode and decode flat files, and enrich messages features in logic apps</span></span>

<span data-ttu-id="e73fc-104">논리 앱을 사용 하 여 hello 기능 tooprocess XML 메시지를 송신 및 수신 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e73fc-104">Using logic apps, you have hello ability tooprocess XML messages that you send and receive.</span></span> <span data-ttu-id="e73fc-105">이 기능은 hello 엔터프라이즈 통합 팩에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e73fc-105">This feature is included with hello Enterprise Integration Pack.</span></span> <span data-ttu-id="e73fc-106">BizTalk Server의 백그라운드 이러한 사용자에 대해서 hello 엔터프라이즈 통합 팩 비슷한 능력 tootransform 제공 및 메시지의 유효성을, 된 플랫 파일로 작업 하 고도 tooenrich XPath를 사용 하 여 또는 메시지에서 특정 속성을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e73fc-106">For those users with a BizTalk Server background, hello Enterprise Integration Pack gives you similar abilities tootransform and validate messages, work with flat files, and even use XPath tooenrich or extract specific properties from a message.</span></span> 

<span data-ttu-id="e73fc-107">해당 사용자에 게 새 toothis 공간, 이러한 기능은 워크플로 내에서 메시지를 처리 하는 방법은 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e73fc-107">For those users who are new toothis space, these features expand how you process messages within your workflow.</span></span> <span data-ttu-id="e73fc-108">예를 들어, 기업 간 시나리오에 있으며 hello 엔터프라이즈 통합 팩 tooenhance 사용 하 여 특정 XML 스키마와 함께 작동 하는 경우 어떻게 회사 이러한 메시지 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e73fc-108">For example, if you are in a business-to-business scenario, and work with specific XML schemas, then you can use hello Enterprise Integration Pack tooenhance how your company processes these messages.</span></span> 

<span data-ttu-id="e73fc-109">hello 엔터프라이즈 통합 팩에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e73fc-109">hello Enterprise Integration Pack includes:</span></span> 

* <span data-ttu-id="e73fc-110">[XML 유효성 검사](logic-apps-enterprise-integration-xml-validation.md "XML 메시지 유효성 검사에 대해 알아보기") - 특정 스키마에 대해 들어오거나 나가는 XML 메시지의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="e73fc-110">[XML validation](logic-apps-enterprise-integration-xml-validation.md "Learn about XML message validation") - Validate an incoming or outgoing XML message against a specific schema.</span></span>
* <span data-ttu-id="e73fc-111">[XML 변환](../logic-apps/logic-apps-enterprise-integration-transform.md "XML 메시지 변환 및 지도에 대해 알아보기") -변환 하거나 요구 사항 또는 파트너의 hello 요구 사항에 따라 XML 메시지를 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e73fc-111">[XML transform](../logic-apps/logic-apps-enterprise-integration-transform.md "Learn about XML message transformations and maps") - Convert or customize an XML message based on your requirements, or hello requirements of a partner.</span></span>
* <span data-ttu-id="e73fc-112">[플랫 파일 인코딩 및 플랫 파일 디코딩](logic-apps-enterprise-integration-flatfile.md "플랫 파일 인코딩/디코딩에 대해 알아보기") - 플랫 파일을 인코딩 또는 디코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="e73fc-112">[Flat file encoding and flat file decoding](logic-apps-enterprise-integration-flatfile.md "Learn about flat file encoding/decoding") - Encode or decode a flat file.</span></span> <span data-ttu-id="e73fc-113">예를 들어 SAP에서 플랫 파일로 IDOC 파일을 수락하고 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e73fc-113">For example, SAP accepts and sends IDOC files in flat file format.</span></span> <span data-ttu-id="e73fc-114">많은 통합 플랫폼에서는 Logic Apps를 포함하여 XML 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e73fc-114">Many integration platforms create XML messages, including Logic Apps.</span></span> <span data-ttu-id="e73fc-115">따라서을 사용 하 여 hello 플랫 파일 인코더 너무 "변환" XML 파일 tooflat 파일 논리 앱을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e73fc-115">So, you can create a logic app that uses hello flat file encoder too"convert" XML files tooflat files.</span></span> 
* <span data-ttu-id="e73fc-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) -메시지를 보강 하 고 hello 메시지에서 특정 속성을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e73fc-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - Enrich a message and extract specific properties from hello message.</span></span> <span data-ttu-id="e73fc-117">사용 하 여 hello 추출 속성 tooroute hello 메시지 tooa 대상 또는 중간 끝점 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e73fc-117">You can then use hello extracted properties tooroute hello message tooa destination, or an intermediary endpoint.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="e73fc-118">체험</span><span class="sxs-lookup"><span data-stu-id="e73fc-118">Try it out</span></span>
<span data-ttu-id="e73fc-119">[완벽 하 게 작동 논리 앱을 배포 ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub 샘플) Azure 논리 앱의 hello XML 기능을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="e73fc-119">[Deploy a fully operational logic app ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub sample) by using hello XML features in Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="e73fc-120">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="e73fc-120">Learn more</span></span>
[<span data-ttu-id="e73fc-121">엔터프라이즈 통합 팩 hello에 대 한 자세한</span><span class="sxs-lookup"><span data-stu-id="e73fc-121">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대 한 자세한 정보")
