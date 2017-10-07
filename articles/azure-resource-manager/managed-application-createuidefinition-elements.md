---
title: "관리 되는 응용 프로그램 aaaAzure UI 정의 함수를 만들 | Microsoft Docs"
description: "Azure 관리 되는 응용 프로그램에 대 한 UI 정의 생성할 때 hello 함수 toouse 설명"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: a34c6202372168cda769c471b1c9fdd539dd0f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-elements"></a><span data-ttu-id="eba00-103">CreateUiDefinition 요소</span><span class="sxs-lookup"><span data-stu-id="eba00-103">CreateUiDefinition elements</span></span>
<span data-ttu-id="eba00-104">이 문서에서는 hello 스키마와는 CreateUiDefinition의 지원 되는 모든 요소에 대 한 속성을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-104">This article describes hello schema and properties for all supported elements of a CreateUiDefinition.</span></span> <span data-ttu-id="eba00-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-105">You use these elements when [creating an Azure Managed Application](managed-application-publishing.md).</span></span> <span data-ttu-id="eba00-106">대부분의 요소에 대 한 hello 스키마는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-106">hello schema for most elements is as follows:</span></span>

```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Keep calm and visit hello [Azure Portal](portal.azure.com).",
  "constraints": {},
  "options": {},
  "visible": true
}
```
| <span data-ttu-id="eba00-107">속성</span><span class="sxs-lookup"><span data-stu-id="eba00-107">Property</span></span> | <span data-ttu-id="eba00-108">필수</span><span class="sxs-lookup"><span data-stu-id="eba00-108">Required</span></span> | <span data-ttu-id="eba00-109">설명</span><span class="sxs-lookup"><span data-stu-id="eba00-109">Description</span></span> |
| -------- | -------- | ----------- |
| <span data-ttu-id="eba00-110">name</span><span class="sxs-lookup"><span data-stu-id="eba00-110">name</span></span> | <span data-ttu-id="eba00-111">예</span><span class="sxs-lookup"><span data-stu-id="eba00-111">Yes</span></span> | <span data-ttu-id="eba00-112">내부 식별자 tooreference 요소의 특정 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="eba00-112">An internal identifier tooreference a specific instance of an element.</span></span> <span data-ttu-id="eba00-113">hello hello 요소 이름의 가장 일반적으로 사용 중인 `outputs`hello의 hello 출력 값 요소는 hello 서식 파일의 매핑된 toohello 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-113">hello most common usage of hello element name is in `outputs`, where hello output values of hello specified elements are mapped toohello parameters of hello template.</span></span> <span data-ttu-id="eba00-114">사용할 수 있습니다도 toobind hello 출력 값의 요소 toohello `defaultValue` 다른 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-114">You can also use it toobind hello output value of an element toohello `defaultValue` of another element.</span></span> |
| <span data-ttu-id="eba00-115">type</span><span class="sxs-lookup"><span data-stu-id="eba00-115">type</span></span> | <span data-ttu-id="eba00-116">예</span><span class="sxs-lookup"><span data-stu-id="eba00-116">Yes</span></span> | <span data-ttu-id="eba00-117">hello UI toorender hello 요소에 대 한 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-117">hello UI control toorender for hello element.</span></span> <span data-ttu-id="eba00-118">지원되는 형식 목록은 [요소](#elements)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eba00-118">For a list of supported types, see [Elements](#elements).</span></span> |
| <span data-ttu-id="eba00-119">label</span><span class="sxs-lookup"><span data-stu-id="eba00-119">label</span></span> | <span data-ttu-id="eba00-120">예</span><span class="sxs-lookup"><span data-stu-id="eba00-120">Yes</span></span> | <span data-ttu-id="eba00-121">hello는 hello 요소의 텍스트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-121">hello display text of hello element.</span></span> <span data-ttu-id="eba00-122">일부 요소 형식은 레이블이 여러 개 포함할 hello 값에는 여러 문자열을 포함 하는 개체 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-122">Some element types contain multiple labels, so hello value could be an object containing multiple strings.</span></span> |
| <span data-ttu-id="eba00-123">defaultValue</span><span class="sxs-lookup"><span data-stu-id="eba00-123">defaultValue</span></span> | <span data-ttu-id="eba00-124">아니요</span><span class="sxs-lookup"><span data-stu-id="eba00-124">No</span></span> | <span data-ttu-id="eba00-125">hello hello 요소의 기본 값입니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-125">hello default value of hello element.</span></span> <span data-ttu-id="eba00-126">일부 요소 형식은 hello 값 개체 일 수 있으므로 복잡 한 기본값을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-126">Some element types support complex default values, so hello value could be an object.</span></span> |
| <span data-ttu-id="eba00-127">toolTip</span><span class="sxs-lookup"><span data-stu-id="eba00-127">toolTip</span></span> | <span data-ttu-id="eba00-128">아니요</span><span class="sxs-lookup"><span data-stu-id="eba00-128">No</span></span> | <span data-ttu-id="eba00-129">hello 요소의 hello 도구 설명에 hello 텍스트 toodisplay 합니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-129">hello text toodisplay in hello tool tip of hello element.</span></span> <span data-ttu-id="eba00-130">비슷한 너무`label`, 일부 요소는 여러 도구 설명 문자열을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-130">Similar too`label`, some elements support multiple tool tip strings.</span></span> <span data-ttu-id="eba00-131">Markdown 구문을 사용하여 인라인 링크를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-131">Inline links can be embedded using Markdown syntax.</span></span>
| <span data-ttu-id="eba00-132">constraints</span><span class="sxs-lookup"><span data-stu-id="eba00-132">constraints</span></span> | <span data-ttu-id="eba00-133">아니요</span><span class="sxs-lookup"><span data-stu-id="eba00-133">No</span></span> | <span data-ttu-id="eba00-134">Hello 요소의 hello 유효성 검사 동작을 사용 하는 toocustomize 있는 하나 이상의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-134">One or more properties that are used toocustomize hello validation behavior of hello element.</span></span> <span data-ttu-id="eba00-135">제약 조건에 대 한 지원 hello 속성 요소 유형에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-135">hello supported properties for constraints vary by element type.</span></span> <span data-ttu-id="eba00-136">일부 요소 형식은 hello 유효성 검사 동작을 사용자 지정을 지원 하지 않으며 제약 조건 속성이 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-136">Some element types do not support customization of hello validation behavior, and thus have no constraints property.</span></span> |
| <span data-ttu-id="eba00-137">options</span><span class="sxs-lookup"><span data-stu-id="eba00-137">options</span></span> | <span data-ttu-id="eba00-138">아니요</span><span class="sxs-lookup"><span data-stu-id="eba00-138">No</span></span> | <span data-ttu-id="eba00-139">Hello 요소의 hello 동작을 사용자 지정 하는 추가 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-139">Additional properties that customize hello behavior of hello element.</span></span> <span data-ttu-id="eba00-140">비슷한 너무`constraints`, 지원 되는 hello 속성 요소 유형에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-140">Similar too`constraints`, hello supported properties vary by element type.</span></span> |
| <span data-ttu-id="eba00-141">visible</span><span class="sxs-lookup"><span data-stu-id="eba00-141">visible</span></span> | <span data-ttu-id="eba00-142">아니요</span><span class="sxs-lookup"><span data-stu-id="eba00-142">No</span></span> | <span data-ttu-id="eba00-143">Hello 요소가 표시 되는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-143">Indicates whether hello element is displayed.</span></span> <span data-ttu-id="eba00-144">경우 `true`, hello 요소 및 해당 자식 요소가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-144">If `true`, hello element and applicable child elements are displayed.</span></span> <span data-ttu-id="eba00-145">hello 기본값은 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-145">hello default value is `true`.</span></span> <span data-ttu-id="eba00-146">사용 하 여 [논리 함수](managed-application-createuidefinition-functions.md#logical-functions) toodynamically이이 속성의이 값을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-146">Use [logical functions](managed-application-createuidefinition-functions.md#logical-functions) toodynamically control this property's value.</span></span>

## <a name="elements"></a><span data-ttu-id="eba00-147">요소</span><span class="sxs-lookup"><span data-stu-id="eba00-147">Elements</span></span>

<span data-ttu-id="eba00-148">설명서 hello 스키마 hello 요소 (일반적으로 관련 유효성 검사 및 지원 되는 사용자 지정) 및 샘플 출력의 hello 동작에 주의 각 요소는 UI 샘플에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-148">hello documentation for each element contains a UI sample, schema, remarks on hello behavior of hello element (usually concerning validation and supported customization), and sample output.</span></span>

- [<span data-ttu-id="eba00-149">Microsoft.Common.DropDown</span><span class="sxs-lookup"><span data-stu-id="eba00-149">Microsoft.Common.DropDown</span></span>](managed-application-microsoft-common-dropdown.md)
- [<span data-ttu-id="eba00-150">Microsoft.Common.FileUpload</span><span class="sxs-lookup"><span data-stu-id="eba00-150">Microsoft.Common.FileUpload</span></span>](managed-application-microsoft-common-fileupload.md)
- [<span data-ttu-id="eba00-151">Microsoft.Common.OptionsGroup</span><span class="sxs-lookup"><span data-stu-id="eba00-151">Microsoft.Common.OptionsGroup</span></span>](managed-application-microsoft-common-optionsgroup.md)
- [<span data-ttu-id="eba00-152">Microsoft.Common.PasswordBox</span><span class="sxs-lookup"><span data-stu-id="eba00-152">Microsoft.Common.PasswordBox</span></span>](managed-application-microsoft-common-passwordbox.md)
- [<span data-ttu-id="eba00-153">Microsoft.Common.Section</span><span class="sxs-lookup"><span data-stu-id="eba00-153">Microsoft.Common.Section</span></span>](managed-application-microsoft-common-section.md)
- [<span data-ttu-id="eba00-154">Microsoft.Common.TextBox</span><span class="sxs-lookup"><span data-stu-id="eba00-154">Microsoft.Common.TextBox</span></span>](managed-application-microsoft-common-textbox.md)
- [<span data-ttu-id="eba00-155">Microsoft.Compute.CredentialsCombo</span><span class="sxs-lookup"><span data-stu-id="eba00-155">Microsoft.Compute.CredentialsCombo</span></span>](managed-application-microsoft-compute-credentialscombo.md)
- [<span data-ttu-id="eba00-156">Microsoft.Compute.SizeSelector</span><span class="sxs-lookup"><span data-stu-id="eba00-156">Microsoft.Compute.SizeSelector</span></span>](managed-application-microsoft-compute-sizeselector.md)
- [<span data-ttu-id="eba00-157">Microsoft.Compute.UserNameTextBox</span><span class="sxs-lookup"><span data-stu-id="eba00-157">Microsoft.Compute.UserNameTextBox</span></span>](managed-application-microsoft-compute-usernametextbox.md)
- [<span data-ttu-id="eba00-158">Microsoft.Network.PublicIpAddressCombo</span><span class="sxs-lookup"><span data-stu-id="eba00-158">Microsoft.Network.PublicIpAddressCombo</span></span>](managed-application-microsoft-network-publicipaddresscombo.md)
- [<span data-ttu-id="eba00-159">Microsoft.Network.VirtualNetworkCombo</span><span class="sxs-lookup"><span data-stu-id="eba00-159">Microsoft.Network.VirtualNetworkCombo</span></span>](managed-application-microsoft-network-virtualnetworkcombo.md)
- [<span data-ttu-id="eba00-160">Microsoft.Storage.MultiStorageAccountCombo</span><span class="sxs-lookup"><span data-stu-id="eba00-160">Microsoft.Storage.MultiStorageAccountCombo</span></span>](managed-application-microsoft-storage-multistorageaccountcombo.md)
- [<span data-ttu-id="eba00-161">Microsoft.Storage.StorageAccountSelector</span><span class="sxs-lookup"><span data-stu-id="eba00-161">Microsoft.Storage.StorageAccountSelector</span></span>](managed-application-microsoft-storage-storageaccountselector.md)

## <a name="next-steps"></a><span data-ttu-id="eba00-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eba00-162">Next steps</span></span>
* <span data-ttu-id="eba00-163">소개 toomanaged 응용 프로그램에 대 한 참조 [Azure 관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-163">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="eba00-164">소개 toocreating UI 정의 대 한 참조 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eba00-164">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
