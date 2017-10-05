---
title: "Azure Managed Application UI 정의 만들기 함수 | Microsoft Docs"
description: "Azure Managed Applications에 대한 UI 정의를 생성할 때 사용하는 함수에 대해 설명합니다."
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
ms.openlocfilehash: 635e44a7ec6f9244f5fe75eb5ad947cdd8ae59a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="createuidefinition-elements"></a><span data-ttu-id="e29c6-103">CreateUiDefinition 요소</span><span class="sxs-lookup"><span data-stu-id="e29c6-103">CreateUiDefinition elements</span></span>
<span data-ttu-id="e29c6-104">이 문서에서는 CreateUiDefinition에 지원되는 모든 요소에 대한 스키마와 속성에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-104">This article describes the schema and properties for all supported elements of a CreateUiDefinition.</span></span> <span data-ttu-id="e29c6-105">[Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-105">You use these elements when [creating an Azure Managed Application](managed-application-publishing.md).</span></span> <span data-ttu-id="e29c6-106">대부분의 요소에 대한 스키마는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-106">The schema for most elements is as follows:</span></span>

```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Keep calm and visit the [Azure Portal](portal.azure.com).",
  "constraints": {},
  "options": {},
  "visible": true
}
```
| <span data-ttu-id="e29c6-107">속성</span><span class="sxs-lookup"><span data-stu-id="e29c6-107">Property</span></span> | <span data-ttu-id="e29c6-108">필수</span><span class="sxs-lookup"><span data-stu-id="e29c6-108">Required</span></span> | <span data-ttu-id="e29c6-109">설명</span><span class="sxs-lookup"><span data-stu-id="e29c6-109">Description</span></span> |
| -------- | -------- | ----------- |
| <span data-ttu-id="e29c6-110">name</span><span class="sxs-lookup"><span data-stu-id="e29c6-110">name</span></span> | <span data-ttu-id="e29c6-111">예</span><span class="sxs-lookup"><span data-stu-id="e29c6-111">Yes</span></span> | <span data-ttu-id="e29c6-112">요소의 특정 인스턴스를 참조하는 내부 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-112">An internal identifier to reference a specific instance of an element.</span></span> <span data-ttu-id="e29c6-113">요소 이름의 가장 일반적인 사용법은 `outputs`에 있으며, 지정된 요소의 출력 값이 템플릿의 매개 변수에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-113">The most common usage of the element name is in `outputs`, where the output values of the specified elements are mapped to the parameters of the template.</span></span> <span data-ttu-id="e29c6-114">또한 요소의 출력 값을 다른 요소의 `defaultValue`에 바인딩하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-114">You can also use it to bind the output value of an element to the `defaultValue` of another element.</span></span> |
| <span data-ttu-id="e29c6-115">type</span><span class="sxs-lookup"><span data-stu-id="e29c6-115">type</span></span> | <span data-ttu-id="e29c6-116">예</span><span class="sxs-lookup"><span data-stu-id="e29c6-116">Yes</span></span> | <span data-ttu-id="e29c6-117">요소에 대해 렌더링할 UI 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-117">The UI control to render for the element.</span></span> <span data-ttu-id="e29c6-118">지원되는 형식 목록은 [요소](#elements)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e29c6-118">For a list of supported types, see [Elements](#elements).</span></span> |
| <span data-ttu-id="e29c6-119">label</span><span class="sxs-lookup"><span data-stu-id="e29c6-119">label</span></span> | <span data-ttu-id="e29c6-120">예</span><span class="sxs-lookup"><span data-stu-id="e29c6-120">Yes</span></span> | <span data-ttu-id="e29c6-121">요소의 표시 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-121">The display text of the element.</span></span> <span data-ttu-id="e29c6-122">일부 요소 형식에는 여러 개의 레이블이 포함되므로 값은 여러 문자열을 포함하는 개체가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-122">Some element types contain multiple labels, so the value could be an object containing multiple strings.</span></span> |
| <span data-ttu-id="e29c6-123">defaultValue</span><span class="sxs-lookup"><span data-stu-id="e29c6-123">defaultValue</span></span> | <span data-ttu-id="e29c6-124">아니요</span><span class="sxs-lookup"><span data-stu-id="e29c6-124">No</span></span> | <span data-ttu-id="e29c6-125">요소의 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-125">The default value of the element.</span></span> <span data-ttu-id="e29c6-126">일부 요소 형식에서 복잡한 기본값을 지원하므로 이 값은 개체가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-126">Some element types support complex default values, so the value could be an object.</span></span> |
| <span data-ttu-id="e29c6-127">toolTip</span><span class="sxs-lookup"><span data-stu-id="e29c6-127">toolTip</span></span> | <span data-ttu-id="e29c6-128">아니요</span><span class="sxs-lookup"><span data-stu-id="e29c6-128">No</span></span> | <span data-ttu-id="e29c6-129">요소의 도구 설명에 표시할 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-129">The text to display in the tool tip of the element.</span></span> <span data-ttu-id="e29c6-130">`label`과 마찬가지로 일부 요소에서 여러 개의 도구 설명 문자열을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-130">Similar to `label`, some elements support multiple tool tip strings.</span></span> <span data-ttu-id="e29c6-131">Markdown 구문을 사용하여 인라인 링크를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-131">Inline links can be embedded using Markdown syntax.</span></span>
| <span data-ttu-id="e29c6-132">constraints</span><span class="sxs-lookup"><span data-stu-id="e29c6-132">constraints</span></span> | <span data-ttu-id="e29c6-133">아니요</span><span class="sxs-lookup"><span data-stu-id="e29c6-133">No</span></span> | <span data-ttu-id="e29c6-134">요소의 유효성 검사 동작을 사용자 지정하는 데 사용되는 하나 이상의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-134">One or more properties that are used to customize the validation behavior of the element.</span></span> <span data-ttu-id="e29c6-135">제약 조건에 지원되는 속성은 요소 형식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-135">The supported properties for constraints vary by element type.</span></span> <span data-ttu-id="e29c6-136">일부 요소 형식에서는 유효성 검사 동작의 사용자 지정을 지원하지 않으므로 제약 조건 속성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-136">Some element types do not support customization of the validation behavior, and thus have no constraints property.</span></span> |
| <span data-ttu-id="e29c6-137">options</span><span class="sxs-lookup"><span data-stu-id="e29c6-137">options</span></span> | <span data-ttu-id="e29c6-138">아니요</span><span class="sxs-lookup"><span data-stu-id="e29c6-138">No</span></span> | <span data-ttu-id="e29c6-139">요소의 동작을 사용자 지정하는 추가 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-139">Additional properties that customize the behavior of the element.</span></span> <span data-ttu-id="e29c6-140">`constraints`과 마찬가지로 지원되는 속성은 요소 형식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-140">Similar to `constraints`, the supported properties vary by element type.</span></span> |
| <span data-ttu-id="e29c6-141">visible</span><span class="sxs-lookup"><span data-stu-id="e29c6-141">visible</span></span> | <span data-ttu-id="e29c6-142">아니요</span><span class="sxs-lookup"><span data-stu-id="e29c6-142">No</span></span> | <span data-ttu-id="e29c6-143">요소가 표시되는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-143">Indicates whether the element is displayed.</span></span> <span data-ttu-id="e29c6-144">`true`이면 요소 및 적용 가능한 자식 요소가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-144">If `true`, the element and applicable child elements are displayed.</span></span> <span data-ttu-id="e29c6-145">기본값은 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-145">The default value is `true`.</span></span> <span data-ttu-id="e29c6-146">[논리 함수](managed-application-createuidefinition-functions.md#logical-functions)를 사용하여 이 속성의 값을 동적으로 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-146">Use [logical functions](managed-application-createuidefinition-functions.md#logical-functions) to dynamically control this property's value.</span></span>

## <a name="elements"></a><span data-ttu-id="e29c6-147">요소</span><span class="sxs-lookup"><span data-stu-id="e29c6-147">Elements</span></span>

<span data-ttu-id="e29c6-148">각 요소에 대한 설명서에는 UI 샘플, 스키마, 요소의 동작에 대한 설명(일반적으로 유효성 검사 및 지원되는 사용자 지정과 관련됨) 및 샘플 출력이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e29c6-148">The documentation for each element contains a UI sample, schema, remarks on the behavior of the element (usually concerning validation and supported customization), and sample output.</span></span>

- [<span data-ttu-id="e29c6-149">Microsoft.Common.DropDown</span><span class="sxs-lookup"><span data-stu-id="e29c6-149">Microsoft.Common.DropDown</span></span>](managed-application-microsoft-common-dropdown.md)
- [<span data-ttu-id="e29c6-150">Microsoft.Common.FileUpload</span><span class="sxs-lookup"><span data-stu-id="e29c6-150">Microsoft.Common.FileUpload</span></span>](managed-application-microsoft-common-fileupload.md)
- [<span data-ttu-id="e29c6-151">Microsoft.Common.OptionsGroup</span><span class="sxs-lookup"><span data-stu-id="e29c6-151">Microsoft.Common.OptionsGroup</span></span>](managed-application-microsoft-common-optionsgroup.md)
- [<span data-ttu-id="e29c6-152">Microsoft.Common.PasswordBox</span><span class="sxs-lookup"><span data-stu-id="e29c6-152">Microsoft.Common.PasswordBox</span></span>](managed-application-microsoft-common-passwordbox.md)
- [<span data-ttu-id="e29c6-153">Microsoft.Common.Section</span><span class="sxs-lookup"><span data-stu-id="e29c6-153">Microsoft.Common.Section</span></span>](managed-application-microsoft-common-section.md)
- [<span data-ttu-id="e29c6-154">Microsoft.Common.TextBox</span><span class="sxs-lookup"><span data-stu-id="e29c6-154">Microsoft.Common.TextBox</span></span>](managed-application-microsoft-common-textbox.md)
- [<span data-ttu-id="e29c6-155">Microsoft.Compute.CredentialsCombo</span><span class="sxs-lookup"><span data-stu-id="e29c6-155">Microsoft.Compute.CredentialsCombo</span></span>](managed-application-microsoft-compute-credentialscombo.md)
- [<span data-ttu-id="e29c6-156">Microsoft.Compute.SizeSelector</span><span class="sxs-lookup"><span data-stu-id="e29c6-156">Microsoft.Compute.SizeSelector</span></span>](managed-application-microsoft-compute-sizeselector.md)
- [<span data-ttu-id="e29c6-157">Microsoft.Compute.UserNameTextBox</span><span class="sxs-lookup"><span data-stu-id="e29c6-157">Microsoft.Compute.UserNameTextBox</span></span>](managed-application-microsoft-compute-usernametextbox.md)
- [<span data-ttu-id="e29c6-158">Microsoft.Network.PublicIpAddressCombo</span><span class="sxs-lookup"><span data-stu-id="e29c6-158">Microsoft.Network.PublicIpAddressCombo</span></span>](managed-application-microsoft-network-publicipaddresscombo.md)
- [<span data-ttu-id="e29c6-159">Microsoft.Network.VirtualNetworkCombo</span><span class="sxs-lookup"><span data-stu-id="e29c6-159">Microsoft.Network.VirtualNetworkCombo</span></span>](managed-application-microsoft-network-virtualnetworkcombo.md)
- [<span data-ttu-id="e29c6-160">Microsoft.Storage.MultiStorageAccountCombo</span><span class="sxs-lookup"><span data-stu-id="e29c6-160">Microsoft.Storage.MultiStorageAccountCombo</span></span>](managed-application-microsoft-storage-multistorageaccountcombo.md)
- [<span data-ttu-id="e29c6-161">Microsoft.Storage.StorageAccountSelector</span><span class="sxs-lookup"><span data-stu-id="e29c6-161">Microsoft.Storage.StorageAccountSelector</span></span>](managed-application-microsoft-storage-storageaccountselector.md)

## <a name="next-steps"></a><span data-ttu-id="e29c6-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e29c6-162">Next steps</span></span>
* <span data-ttu-id="e29c6-163">관리되는 응용 프로그램에 대한 소개는 [Azure Managed Application 개요](managed-application-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e29c6-163">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="e29c6-164">UI 정의 만들기에 대한 소개는 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e29c6-164">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
