---
title: "Hadoop - Microsoft Avro Library에서 데이터 직렬화 - Azure | Microsoft Docs"
description: "Microsoft Avro Library를 사용하여 메모리, 데이터베이스 또는 파일에 유지하기 위해 HDInsight의 Hadoop에서 데이터를 직렬화 및 역직렬화하는 방법을 알아보세요."
keywords: avro,hadoop avro
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: c78dc20d-5d8d-4366-94ac-abbe89aaac58
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jgao
ms.custom: hdiseo17may2017
ms.openlocfilehash: d06bf8ff4a21e4f4b29593bac32bfa2b32601fc4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="serialize-data-in-hadoop-with-the-microsoft-avro-library"></a><span data-ttu-id="06f47-104">Microsoft Avro 라이브러리로 Hadoop의 데이터 직렬화</span><span class="sxs-lookup"><span data-stu-id="06f47-104">Serialize data in Hadoop with the Microsoft Avro Library</span></span>

>[!NOTE]
><span data-ttu-id="06f47-105">Avro SDK는 더 이상 Microsoft에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-105">The Avro SDK is no longer supported by Microsoft.</span></span> <span data-ttu-id="06f47-106">라이브러리는 오픈 소스 커뮤니티에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-106">The library is open source community supported.</span></span> <span data-ttu-id="06f47-107">라이브러리의 소스는 [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-107">The sources for the library are located in [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

<span data-ttu-id="06f47-108">이 항목에서는 [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro)를 사용하여 메모리, 데이터베이스 또는 파일에서 유지되도록 개체와 기타 데이터 구조를 스트림으로 직렬화하는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="06f47-108">This topic shows how to use the [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) to serialize objects and other data structures into streams to persist them to memory, a database, or a file.</span></span> <span data-ttu-id="06f47-109">또한 원래 개체를 복구하기 위해 역직렬화하는 방법도 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-109">It also shows how to deserialize them to recover the original objects.</span></span>

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a><span data-ttu-id="06f47-110">Apache Avro</span><span class="sxs-lookup"><span data-stu-id="06f47-110">Apache Avro</span></span>
<span data-ttu-id="06f47-111"><a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a>는 Microsoft. NET 환경을 위한 Apache Avro 데이터 직렬화 시스템을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-111">The <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implements the Apache Avro data serialization system for the Microsoft.NET environment.</span></span> <span data-ttu-id="06f47-112">Apache Avro는 직렬화를 위한 압축 이진 데이터 교환 형식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-112">Apache Avro provides a compact binary data interchange format for serialization.</span></span> <span data-ttu-id="06f47-113">또한 <a href="http://www.json.org" target="_blank">JSON</a>을 사용하여 언어 상호 운용성을 따르는 언어 중립적 스키마를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-113">It uses <a href="http://www.json.org" target="_blank">JSON</a> to define a language-agnostic schema that underwrites language interoperability.</span></span> <span data-ttu-id="06f47-114">한 언어로 직렬화된 데이터는 다른 언어로 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-114">Data serialized in one language can be read in another.</span></span> <span data-ttu-id="06f47-115">현재 C, C++, C#, Java, PHP, Python 및 Ruby가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-115">Currently C, C++, C#, Java, PHP, Python, and Ruby are supported.</span></span> <span data-ttu-id="06f47-116">이 형식에 대한 자세한 내용은 <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro 사양</a>(영문)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-116">Detailed information on the format can be found in the <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro Specification</a>.</span></span> 

>[!NOTE]
><span data-ttu-id="06f47-117">Microsoft Avro 라이브러리에서는 이 사양의 RPC(원격 프로시저 호출)를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-117">The Microsoft Avro Library does not support the remote procedure calls (RPCs) part of this specification.</span></span>
>

<span data-ttu-id="06f47-118">Avro 시스템에서 직렬화된 개체의 표현은 스키마 및 실제 값 부분으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-118">The serialized representation of an object in the Avro system consists of two parts: schema and actual value.</span></span> <span data-ttu-id="06f47-119">Avro 스키마는 JSON을 사용하여 직렬화된 데이터의 언어 독립적 데이터 모델을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-119">The Avro schema describes the language-independent data model of the serialized data with JSON.</span></span> <span data-ttu-id="06f47-120">이 스키마는 데이터의 이진 표현 옆에 나란히 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-120">It is presented side by side with a binary representation of data.</span></span> <span data-ttu-id="06f47-121">스키마를 이진 표현과 구분하면 값별로 오버헤드가 발생하지 않고 각 개체를 쓸 수 있으므로 직렬화는 빨라지고 표현이 차지하는 공간은 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-121">Having the schema separate from the binary representation permits each object to be written with no per-value overheads, making serialization fast, and the representation small.</span></span>

## <a name="the-hadoop-scenario"></a><span data-ttu-id="06f47-122">Hadoop 시나리오</span><span class="sxs-lookup"><span data-stu-id="06f47-122">The Hadoop scenario</span></span>
<span data-ttu-id="06f47-123">Apache Avro 직렬화 형식은 Azure HDInsight 및 기타 Apache Hadoop 환경에서 널리 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-123">The Apache Avro serialization format is widely used in Azure HDInsight and other Apache Hadoop environments.</span></span> <span data-ttu-id="06f47-124">Avro는 Hadoop MapReduce 작업 내에서 복잡한 데이터 구조를 나타내는 편리한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-124">Avro provides a convenient way to represent complex data structures within a Hadoop MapReduce job.</span></span> <span data-ttu-id="06f47-125">Avro 파일(Avro 개체 컨테이너 파일)의 형식은 분산 MapReduce 프로그래밍 모델을 지원하도록 디자인되었습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-125">The format of Avro files (Avro object container file) has been designed to support the distributed MapReduce programming model.</span></span> <span data-ttu-id="06f47-126">이러한 분산을 가능하게 하는 핵심 기능은 파일이 “분할 가능"하여 파일의 임의 지점을 찾고 특정 블록부터 읽기 시작할 수 있다는 데 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-126">The key feature that enables the distribution is that the files are “splittable” in the sense that one can seek any point in a file and start reading from a particular block.</span></span>

## <a name="serialization-in-avro-library"></a><span data-ttu-id="06f47-127">Avro 라이브러리의 직렬화</span><span class="sxs-lookup"><span data-stu-id="06f47-127">Serialization in Avro Library</span></span>
<span data-ttu-id="06f47-128">.NET Library for Avro는 다음과 같은 두 가지 방식으로 개체를 직렬화할 수 있도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-128">The .NET Library for Avro supports two ways of serializing objects:</span></span>

* <span data-ttu-id="06f47-129">**리플렉션** - 해당 형식에 대한 JSON 스키마는 직렬화될 수 있게 .NET 형식의 데이터 계약 특성에서 자동으로 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-129">**reflection** - The JSON schema for the types is automatically built from the data contract attributes of the .NET types to be serialized.</span></span>
* <span data-ttu-id="06f47-130">**제네릭 레코드** - JSON 스키마는 직렬화할 데이터의 스키마를 설명하기 위해 .NET 형식이 없는 경우 [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx)(영문) 클래스로 표현되는 레코드에 명시적으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-130">**generic record** - A JSON schema is explicitly specified in a record represented by the [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) class when no .NET types are present to describe the schema for the data to be serialized.</span></span>

<span data-ttu-id="06f47-131">데이터 스키마가 스트림의 기록기 및 판독기 둘 다로 알려져 있으면 데이터를 스키마 없이 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-131">When the data schema is known to both the writer and reader of the stream, the data can be sent without its schema.</span></span> <span data-ttu-id="06f47-132">Avro 개체 컨테이너 파일이 사용되는 경우 스키마는 파일 내에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-132">In cases when an Avro object container file is used, the schema is stored within the file.</span></span> <span data-ttu-id="06f47-133">데이터 압축에 사용되는 코덱과 같은 기타 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-133">Other parameters, such as the codec used for data compression, can be specified.</span></span> <span data-ttu-id="06f47-134">이러한 시나리오는 다음 코드 예에 좀 더 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-134">These scenarios are outlined in more detail and illustrated in the following code examples:</span></span>

## <a name="install-avro-library"></a><span data-ttu-id="06f47-135">Avro 라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="06f47-135">Install Avro Library</span></span>
<span data-ttu-id="06f47-136">라이브러리를 설치하기 전에 필요한 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-136">The following are required before you install the library:</span></span>

* <span data-ttu-id="06f47-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span><span class="sxs-lookup"><span data-stu-id="06f47-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span></span>
* <span data-ttu-id="06f47-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a>(6.0.4 이상)</span><span class="sxs-lookup"><span data-stu-id="06f47-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 or later)</span></span>

<span data-ttu-id="06f47-139">Newtonsoft.Json.dll 종속성은 Microsoft Avro 라이브러리의 설치와 함께 자동으로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-139">Note that the Newtonsoft.Json.dll dependency is downloaded automatically with the installation of the Microsoft Avro Library.</span></span> <span data-ttu-id="06f47-140">이 절차는 다음 섹션에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-140">The procedure is provided in the following section:</span></span>

<span data-ttu-id="06f47-141">Microsoft Avro 라이브러리는 다음 절차를 사용하여 Visual Studio에서 설치할 수 있는 NuGet 패키지로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-141">The Microsoft Avro Library is distributed as a NuGet package that can be installed from Visual Studio via the following procedure:</span></span>

1. <span data-ttu-id="06f47-142">**프로젝트** 탭-> **NuGet 패키지 관리...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-142">Select the **Project** tab -> **Manage NuGet Packages...**</span></span>
2. <span data-ttu-id="06f47-143">**온라인 검색** 상자에서 "Microsoft.Hadoop.Avro"를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-143">Search for "Microsoft.Hadoop.Avro" in the **Search Online** box.</span></span>
3. <span data-ttu-id="06f47-144">**Microsoft Azure HDInsight Avro Library** 옆의 **설치** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-144">Click the **Install** button next to **Microsoft Azure HDInsight Avro Library**.</span></span>

<span data-ttu-id="06f47-145">Newtonsoft.Json.dll(>= 6.0.4) 종속성은 Microsoft Avro 라이브러리와 함께 자동으로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-145">Note that the Newtonsoft.Json.dll (>=6.0.4) dependency is also downloaded automatically with the Microsoft Avro Library.</span></span>

<span data-ttu-id="06f47-146">Microsoft Avro 라이브러리 소스 코드는 [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-146">The Microsoft Avro Library source code is available at [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

## <a name="compile-schemas-using-avro-library"></a><span data-ttu-id="06f47-147">Avro 라이브러리를 사용하여 스키마 컴파일</span><span class="sxs-lookup"><span data-stu-id="06f47-147">Compile schemas using Avro Library</span></span>
<span data-ttu-id="06f47-148">Microsoft Avro 라이브러리에는 이전에 정의된 JSON 스키마에 따라 자동으로 C# 형식을 만들 수 있는 코드 생성 유틸리티가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-148">The Microsoft Avro Library contains a code generation utility that allows creating C# types automatically based on the previously defined JSON schema.</span></span> <span data-ttu-id="06f47-149">코드 생성 유틸리티는 이진 실행 파일로 배포되지 않지만, 다음 절차에 따라 쉽게 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-149">The code generation utility is not distributed as a binary executable, but can be easily built via the following procedure:</span></span>

1. <span data-ttu-id="06f47-150"><a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK For Hadoop</a>에서 HDInsight SDK 소스 코드의 최신 버전이 포함된 .zip 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-150">Download the .zip file with the latest version of HDInsight SDK source code from <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK For Hadoop</a>.</span></span> <span data-ttu-id="06f47-151">(**다운로드** 탭이 아니라 **다운로드** 아이콘을 클릭합니다.)</span><span class="sxs-lookup"><span data-stu-id="06f47-151">(Click the **Download** icon, not the **Downloads** tab.)</span></span>
2. <span data-ttu-id="06f47-152">필요한 종속성 NuGet 패키지를 다운로드하기 위해 .NET Framework 4가 설치되고 인터넷에 연결된 컴퓨터에 있는 디렉터리에 HDInsight SDK의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-152">Extract the HDInsight SDK to a directory on the machine with .NET Framework 4 installed and connected to the Internet for downloading necessary dependency NuGet packages.</span></span> <span data-ttu-id="06f47-153">여기서는 소스 코드가 C:\SDK에 추출된다고 간주합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-153">Below, we assume that the source code is extracted to C:\SDK.</span></span>
3. <span data-ttu-id="06f47-154">C:\SDK\src\Microsoft.Hadoop.Avro.Tools 폴더로 이동하고 build.bat를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-154">Go to the folder C:\SDK\src\Microsoft.Hadoop.Avro.Tools and run build.bat.</span></span> <span data-ttu-id="06f47-155">(이 파일은 .NET Framework 32비트 배포에서 MSBuild를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-155">(The file calls MSBuild from the 32-bit distribution of the .NET Framework.</span></span> <span data-ttu-id="06f47-156">64비트 버전을 사용하려는 경우 파일 내부의 주석에 따라 build.bat를 편집합니다.) 성공적으로 빌드되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-156">If you would like to use the 64-bit version, edit build.bat, following the comments inside the file.) Ensure that the build is successful.</span></span> <span data-ttu-id="06f47-157">(일부 시스템에서는 MSBuild로 인해 경고가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-157">(On some systems, MSBuild may produce warnings.</span></span> <span data-ttu-id="06f47-158">빌드 오류가 없으면 이러한 경고가 유틸리티에 영향을 미치지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="06f47-158">These warnings do not affect the utility as long as there are no build errors.)</span></span>
4. <span data-ttu-id="06f47-159">컴파일된 유틸리티는 C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-159">The compiled utility is located in C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span></span>

<span data-ttu-id="06f47-160">명령줄 구문에 익숙해지려면 코드 생성 유틸리티가 있는 폴더에서 다음 명령을 실행합니다. `Microsoft.Hadoop.Avro.Tools help /c:codegen`</span><span class="sxs-lookup"><span data-stu-id="06f47-160">To get familiar with the command-line syntax, execute the following command from the folder where the code generation utility is located: `Microsoft.Hadoop.Avro.Tools help /c:codegen`</span></span>

<span data-ttu-id="06f47-161">유틸리티를 테스트하기 위해 소스 코드와 함께 제공되는 샘플 JSON 스키마 파일에서 C# 클래스를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-161">To test the utility, you can generate C# classes from the sample JSON schema file provided with the source code.</span></span> <span data-ttu-id="06f47-162">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-162">Execute the following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

<span data-ttu-id="06f47-163">그러면 현재 디렉터리에 두 개의 C# 파일, 즉 SensorData.cs와 Location.cs가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-163">This is supposed to produce two C# files in the current directory: SensorData.cs and Location.cs.</span></span>

<span data-ttu-id="06f47-164">JSON 스키마를 C# 형식으로 변환하는 동안 코드 생성 유틸리티에서 사용되는 논리를 이해하려면 C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc에 있는 GenerationVerification.feature를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06f47-164">To understand the logic that the code generation utility is using while converting the JSON schema to C# types, see the file GenerationVerification.feature located in C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span></span>

<span data-ttu-id="06f47-165">네임스페이스는 이전 단락에서 언급한 파일에 설명된 논리를 사용하여 JSON 스키마에서 추출됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-165">Namespaces are extracted from the JSON schema, using the logic described in the file mentioned in the previous paragraph.</span></span> <span data-ttu-id="06f47-166">스키마에서 추출된 네임스페이스는 유틸리티 명령줄에서 /n 매개 변수로 제공되는 항목보다 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-166">Namespaces extracted from the schema take precedence over whatever is provided with the /n parameter in the utility command line.</span></span> <span data-ttu-id="06f47-167">스키마 내에 포함된 네임스페이스를 재정의하려면 /nf 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-167">If you want to override the namespaces contained within the schema, use the /nf parameter.</span></span> <span data-ttu-id="06f47-168">예를 들어 SampleJSONSchema.avsc에서 모든 네임스페이스를 my.own.nspace로 변경하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-168">For example, to change all namespaces from the SampleJSONSchema.avsc to my.own.nspace, execute the following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-the-samples"></a><span data-ttu-id="06f47-169">예제 정보</span><span class="sxs-lookup"><span data-stu-id="06f47-169">About the samples</span></span>
<span data-ttu-id="06f47-170">이 항목에 제공되는 여섯 가지 예제는 Microsoft Avro 라이브러리에서 지원되는 다양한 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-170">Six examples provided in this topic illustrate different scenarios supported by the Microsoft Avro Library.</span></span> <span data-ttu-id="06f47-171">Microsoft Avro 라이브러리는 어떤 스트림에서도 작동하도록 디자인되었습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-171">The Microsoft Avro Library is designed to work with any stream.</span></span> <span data-ttu-id="06f47-172">이러한 예에서는 간편성과 일관성을 위해 데이터가 파일 스트림이나 데이터베이스가 아닌 메모리 스트림을 사용하여 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-172">In these examples, data is manipulated via memory streams rather than file streams or databases for simplicity and consistency.</span></span> <span data-ttu-id="06f47-173">프로덕션 환경에서 수행하는 방법은 정확한 시나리오 요구 사항, 데이터 원본과 볼륨, 성능 제약 조건 및 기타 요인에 따라 좌우됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-173">The approach taken in a production environment depends on the exact scenario requirements, data source and volume, performance constraints, and other factors.</span></span>

<span data-ttu-id="06f47-174">처음 2개 예는 리플렉션과 제네릭 레코드를 사용하여 데이터를 메모리 스트림 버퍼로 직렬화 및 역직렬화하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-174">The first two examples show how to serialize and deserialize data into memory stream buffers by using reflection and generic records.</span></span> <span data-ttu-id="06f47-175">이 두 가지 경우의 스키마는 판독기와 기록기 간에 공유되는 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-175">The schema in these two cases is assumed to be shared between the readers and writers out-of-band.</span></span>

<span data-ttu-id="06f47-176">세 번째 및 네 번째 예는 Avro 개체 컨테이너 파일을 사용하여 데이터를 직렬화 및 역직렬화하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-176">The third and fourth examples show how to serialize and deserialize data by using the Avro object container files.</span></span> <span data-ttu-id="06f47-177">데이터가 Avro 컨테이너 파일에 저장되는 경우 역직렬화를 위해 스키마를 공유해야 하므로 스키마도 항상 이 파일에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-177">When data is stored in an Avro container file, its schema is always stored with it because the schema must be shared for deserialization.</span></span>

<span data-ttu-id="06f47-178">처음 4개의 예를 포함하는 샘플은 <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure 코드 샘플</a> 사이트에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-178">The sample containing the first four examples can be downloaded from the <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="06f47-179">5번째 예는 Avro 개체 컨테이너 파일에 대해 사용자 지정 압축 코덱을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-179">The fifth example shows how to use a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="06f47-180">이 예에 대한 코드를 포함하는 샘플은 <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure 코드 샘플</a> (영문) 사이트에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-180">A sample containing the code for this example can be downloaded from the <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="06f47-181">6번째 샘플은 Avro 직렬화를 사용하여 데이터를 Azure Blob 저장소에 업로드하고 HDInsight(Hadoop) 클러스터에서 Hive를 사용하여 데이터를 분석하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-181">The sixth sample shows how to use Avro serialization to upload data to Azure Blob storage and then analyze it by using Hive with an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="06f47-182"><a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure 코드 샘플</a> 사이트에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-182">It can be downloaded from the <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="06f47-183">이 항목에서 설명된 6개 샘플의 링크는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-183">Here are links to the six samples discussed in the topic:</span></span>

* <span data-ttu-id="06f47-184"><a href="#Scenario1">**리플렉션으로 직렬화**</a> - 직렬화할 형식에 대한 JSON 스키마는 데이터 계약 특성에서 자동으로 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-184"><a href="#Scenario1">**Serialization with reflection**</a> - The JSON schema for types to be serialized is automatically built from the data contract attributes.</span></span>
* <span data-ttu-id="06f47-185"><a href="#Scenario2">**제네릭 레코드로 직렬화**</a> - 리플렉션에 사용할 수 있는 .NET 형식을 사용할 수 없는 경우 JSON 스키마가 레코드에 명시적으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-185"><a href="#Scenario2">**Serialization with generic record**</a> - The JSON schema is explicitly specified in a record when no .NET type is available for reflection.</span></span>
* <span data-ttu-id="06f47-186"><a href="#Scenario3">**리플렉션과 함께 개체 컨테이너 파일을 사용하여 직렬화**</a> - JSON 스키마는 Avro 개체 컨테이너 파일을 통해 직렬화된 데이터와 함께 자동으로 빌드되고 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-186"><a href="#Scenario3">**Serialization using object container files with reflection**</a> - The JSON schema is automatically built and shared together with the serialized data via an Avro object container file.</span></span>
* <span data-ttu-id="06f47-187"><a href="#Scenario4">**제네릭 레코드와 함께 개체 컨테이너 파일을 사용하여 직렬화**</a> - JSON 스키마는 직렬화되기 전에 명시적으로 지정되고 Avro 개체 컨테이너 파일을 통해 데이터와 함께 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-187"><a href="#Scenario4">**Serialization using object container files with generic record**</a> - The JSON schema is explicitly specified before the serialization and shared together with the data via an Avro object container file.</span></span>
* <span data-ttu-id="06f47-188"><a href="#Scenario5">**사용자 지정 압축 코덱과 함께 개체 컨테이너 파일을 사용하여 직렬화**</a> - 이 예제에서는 Deflate 데이터 압축 코덱의 사용자 지정 .NET 구현을 사용하여 Avro 개체 컨테이너 파일을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-188"><a href="#Scenario5">**Serialization using object container files with a custom compression codec**</a> - The example shows how to create an Avro object container file with a customized .NET implementation of the Deflate data compression codec.</span></span>
* <span data-ttu-id="06f47-189"><a href="#Scenario6">**Avro를 사용하여 Microsoft Azure HDInsight 서비스를 위한 데이터 업로드**</a> - 이 예제에서는 Avro 직렬화가 HDInsight 서비스와 상호 작용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-189"><a href="#Scenario6">**Using Avro to upload data for the Microsoft Azure HDInsight service**</a> - The example illustrates how Avro serialization interacts with the HDInsight service.</span></span> <span data-ttu-id="06f47-190">이 예를 실행하려면 활성 Azure 구독 및 Azure HDInsight 클러스터에 대한 액세스 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-190">An active Azure subscription and access to an Azure HDInsight cluster are required to run this example.</span></span>

## <span data-ttu-id="06f47-191"><a name="Scenario1"></a>샘플 1: 리플렉션을 사용한 직렬화</span><span class="sxs-lookup"><span data-stu-id="06f47-191"><a name="Scenario1"></a>Sample 1: Serialization with reflection</span></span>
<span data-ttu-id="06f47-192">해당 형식에 대한 JSON 스키마는 직렬화될 수 있게 C# 개체의 데이터 계약 특성을 통한 리플렉션을 사용하여 Microsoft Avro 라이브러리에서 자동으로 빌드될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-192">The JSON schema for the types can be automatically built by the Microsoft Avro Library via reflection from the data contract attributes of the C# objects to be serialized.</span></span> <span data-ttu-id="06f47-193">Microsoft Avro Library는 직렬화할 필드를 식별하기 위해 [**IAvroSeralizer<T>**](http://msdn.microsoft.com/library/dn627341.aspx)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-193">The Microsoft Avro Library creates an [**IAvroSeralizer<T>**](http://msdn.microsoft.com/library/dn627341.aspx) to identify the fields to be serialized.</span></span>

<span data-ttu-id="06f47-194">이 예제에서 **Location** 멤버 구조체를 갖는**SensorData** 클래스 개체가 메모리 스트림에 직렬화되며, 이 스트림은 역직렬화됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-194">In this example, objects (a **SensorData** class with a member **Location** struct) are serialized to a memory stream, and this stream is in turn deserialized.</span></span> <span data-ttu-id="06f47-195">그런 다음 초기 인스턴스와 결과를 비교하여 복구된 **SensorData** 개체가 원본과 동일한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-195">The result is then compared to the initial instance to confirm that the **SensorData** object recovered is identical to the original.</span></span>

<span data-ttu-id="06f47-196">이 예의 스키마는 Avro 개체 컨테이너 형식이 필요 없도록 판독기와 기록기 간에 공유되는 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-196">The schema in this example is assumed to be shared between the readers and writers, so the Avro object container format is not required.</span></span> <span data-ttu-id="06f47-197">스키마를 데이터와 공유해야 할 때 개체 컨테이너 형식과 리플렉션을 사용하여 데이터를 메모리 버퍼로 직렬화 및 역직렬화하는 방법의 예를 보려면 <a href="#Scenario3">개체 컨테이너 파일과 리플렉션을 사용한 직렬화</a>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06f47-197">For an example of how to serialize and deserialize data into memory buffers by using reflection with the object container format when the schema must be shared with the data, see <a href="#Scenario3">Serialization using object container files with reflection</a>.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //the usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serialize and deserialize sample data set represented as an object using reflection.
            //No explicit schema definition is required - schema of serialized objects is automatically built.
            public void SerializeDeserializeObjectUsingReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION\n");
                Console.WriteLine("Serializing Sample Data Set...");

                //Create a new AvroSerializer instance and specify a custom serialization strategy AvroDataContractResolver
                //for serializing only properties attributed with DataContract/DateMember
                var avroSerializer = AvroSerializer.Create<SensorData>();

                //Create a memory stream buffer
                using (var buffer = new MemoryStream())
                {
                    //Create a data set by using sample class and struct
                    var expected = new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } };

                    //Serialize the data to the specified stream
                    avroSerializer.Serialize(buffer, expected);


                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Deserialize data from the stream and cast it to the same type used for serialization
                    var actual = avroSerializer.Deserialize(buffer);

                    Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                    //Finally, verify that deserialized data matches the original one
                    bool isEqual = this.Equal(expected, actual);

                    Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);

                }
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }



            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization to memory using reflection
                Sample.SerializeDeserializeObjectUsingReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING REFLECTION
    //
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.


## <a name="sample-2-serialization-with-a-generic-record"></a><span data-ttu-id="06f47-198">샘플 2: 제네릭 레코드로 직렬화</span><span class="sxs-lookup"><span data-stu-id="06f47-198">Sample 2: Serialization with a generic record</span></span>
<span data-ttu-id="06f47-199">.NET 클래스와 데이터 계약을 사용하여 데이터를 표현할 수 없으므로 리플렉션을 사용할 수 없는 경우 제네릭 레코드에 JSON 스키마를 명시적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-199">A JSON schema can be explicitly specified in a generic record when reflection cannot be used because the data cannot be represented via .NET classes with a data contract.</span></span> <span data-ttu-id="06f47-200">이 방법은 리플렉션 사용보다 더 느립니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-200">This method is slower than using reflection.</span></span> <span data-ttu-id="06f47-201">이러한 경우 데이터의 스키마가 동적이므로 컴파일 시간에 알려지지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-201">In such cases, the schema for the data may also be dynamic, that is, not known at compile time.</span></span> <span data-ttu-id="06f47-202">해당 스키마가 런타임에 Avro 형식으로 변환될 때까지 알려지지 않는 CSV(쉼표로 구분한 값) 파일로 표현된 데이터가 이러한 종류의 동적 시나리오의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-202">Data represented as comma-separated values (CSV) files whose schema is unknown until it is transformed to the Avro format at run time is an example of this sort of dynamic scenario.</span></span>

<span data-ttu-id="06f47-203">이 예에서는 [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) (영문)를 만들고 사용하여 JSON 스키마를 명시적으로 지정하는 방법과 데이터로 채운 후 직렬화 및 역직렬화하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-203">This example shows how to create and use an [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) to explicitly specify a JSON schema, how to populate it with the data, and then how to serialize and deserialize it.</span></span> <span data-ttu-id="06f47-204">그런 다음 초기 인스턴스와 결과를 비교하여 복구된 레코드가 원본과 동일한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-204">The result is then compared to the initial instance to confirm that the record recovered is identical to the original.</span></span>

<span data-ttu-id="06f47-205">이 예의 스키마는 Avro 개체 컨테이너 형식이 필요 없도록 판독기와 기록기 간에 공유되는 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-205">The schema in this example is assumed to be shared between the readers and writers, so the Avro object container format is not required.</span></span> <span data-ttu-id="06f47-206">스키마를 직렬화된 데이터에 포함해야 할 경우 제네릭 레코드와 개체 컨테이너 형식을 사용하여 데이터를 메모리 버퍼로 직렬화 및 역직렬화하는 방법의 예를 보려면 <a href="#Scenario4">개체 컨테이너 파일과 제네릭 레코드를 사용한 직렬화</a>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06f47-206">For an example of how to serialize and deserialize data into memory buffers by using a generic record with the object container format when the schema must be included with the serialized data, see the <a href="#Scenario4">Serialization using object container files with generic record</a> example.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Runtime.Serialization;
    using Microsoft.Hadoop.Avro.Container;
    using Microsoft.Hadoop.Avro.Schema;
    using Microsoft.Hadoop.Avro;

    //This class contains all methods demonstrating
    //the usage of Microsoft Avro Library
    public class AvroSample
    {

        //Serialize and deserialize sample data set by using a generic record.
        //A generic record is a special class with the schema explicitly defined in JSON.
        //All serialized data should be mapped to the fields of the generic record,
        //which in turn is then serialized.
        public void SerializeDeserializeObjectUsingGenericRecords()
        {
            Console.WriteLine("SERIALIZATION USING GENERIC RECORD\n");
            Console.WriteLine("Defining the Schema and creating Sample Data Set...");

            //Define the schema in JSON
            const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

            //Create a generic serializer based on the schema
            var serializer = AvroSerializer.CreateGeneric(Schema);
            var rootSchema = serializer.WriterSchema as RecordSchema;

            //Create a memory stream buffer
            using (var stream = new MemoryStream())
            {
                //Create a generic record to represent the data
                dynamic location = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location.Floor = 1;
                location.Room = 243;

                dynamic expected = new AvroRecord(serializer.WriterSchema);
                expected.Location = location;
                expected.Value = new byte[] { 1, 2, 3, 4, 5 };

                Console.WriteLine("Serializing Sample Data Set...");

                //Serialize the data
                serializer.Serialize(stream, expected);

                stream.Seek(0, SeekOrigin.Begin);

                Console.WriteLine("Deserializing Sample Data Set...");

                //Deserialize the data into a generic record
                dynamic actual = serializer.Deserialize(stream);

                Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                //Finally, verify the results
                bool isEqual = expected.Location.Floor.Equals(actual.Location.Floor);
                isEqual = isEqual && expected.Location.Room.Equals(actual.Location.Room);
                isEqual = isEqual && ((byte[])expected.Value).SequenceEqual((byte[])actual.Value);
                Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);
            }
        }

        static void Main()
        {

            string sectionDivider = "---------------------------------------- ";

            //Create an instance of AvroSample class and invoke methods
            //illustrating different serializing approaches
            AvroSample Sample = new AvroSample();

            //Serialization to memory using generic record
            Sample.SerializeDeserializeObjectUsingGenericRecords();

            Console.WriteLine(sectionDivider);
            Console.WriteLine("Press any key to exit.");
            Console.Read();
        }
    }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING GENERIC RECORD
    //
    // Defining the Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a><span data-ttu-id="06f47-207">샘플 3: 개체 컨테이너 파일을 사용한 직렬화 및 리플렉션을 사용한 직렬화</span><span class="sxs-lookup"><span data-stu-id="06f47-207">Sample 3: Serialization using object container files and serialization with reflection</span></span>
<span data-ttu-id="06f47-208">이 예는 리플렉션을 통해 스키마를 내재적으로 지정하는 <a href="#Scenario1"> 첫 번째 예</a>의 시나리오와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-208">This example is similar to the scenario in the <a href="#Scenario1"> first example</a>, where the schema is implicitly specified with reflection.</span></span> <span data-ttu-id="06f47-209">여기에서는 역직렬화하는 판독기에서 스키마를 알지 못한다는 점이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-209">The difference is that here, the schema is not assumed to be known to the reader that deserializes it.</span></span> <span data-ttu-id="06f47-210">직렬화할 **SensorData** 개체와 암시적으로 지정된 스키마는 [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) 클래스로 표시되는 Avro 개체 컨테이너 파일에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-210">The **SensorData** objects to be serialized and their implicitly specified schema are stored in an Avro object container file represented by the [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span>

<span data-ttu-id="06f47-211">이 예제에서 데이터는 [**SequentialWriter<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx)를 사용하여 직렬화되고 [**SequentialReader<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx)를 사용하여 역직렬화됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-211">The data is serialized in this example with [**SequentialWriter<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx) and deserialized with [**SequentialReader<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx).</span></span> <span data-ttu-id="06f47-212">그런 후 초기 인스턴스와 결과를 비교하여 ID를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-212">The result then is compared to the initial instances to ensure identity.</span></span>

<span data-ttu-id="06f47-213">개체 컨테이너 파일의 데이터는 .NET Framework 4의 기본 [**Deflate**][deflate-100] 압축 코덱을 사용하여 압축됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-213">The data in the object container file is compressed via the default [**Deflate**][deflate-100] compression codec from .NET Framework 4.</span></span> <span data-ttu-id="06f47-214">.NET Framework 4.5에 제공되는 더 나은 최신 버전의 [**Deflate**][deflate-110] 압축 코덱을 사용하는 방법은 이 항목의 <a href="#Scenario5"> 다섯 번째 예</a>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06f47-214">See the <a href="#Scenario5"> fifth example</a> in this topic to learn how to use a more recent and superior version of the [**Deflate**][deflate-110] compression codec available in .NET Framework 4.5.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //the usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes the sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with the Deflate codec.
            public void SerializeDeserializeUsingObjectContainersReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data to file.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects to stream.
                    //Data is compressed using the Deflate codec.
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize the data to stream by using the sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream to file
                    Console.WriteLine("Saving serialized data to file...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from the given stream.
                    //It allows iterating over the deserialized objects because it implements the IEnumerable<T> interface.
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true)))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches the original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            bool isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual);
                            count++;
                        }
                    }
                }

                //Delete the file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream to a new file with the given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during creation and writing to the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using the given path to a memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("The following exception was thrown during reading from the file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during deleting the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection to Avro object container file
                Sample.SerializeDeserializeUsingObjectContainersReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES
    //
    // Serializing Sample Data Set...
    // Saving serialized data to file...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a><span data-ttu-id="06f47-215">샘플 4: 개체 컨테이너 파일을 사용한 직렬화 및 일반 레코드를 사용한 직렬화</span><span class="sxs-lookup"><span data-stu-id="06f47-215">Sample 4: Serialization using object container files and serialization with generic record</span></span>
<span data-ttu-id="06f47-216">이 예는 JSON을 사용하여 명시적으로 스키마를 지정하는 <a href="#Scenario2"> 두 번째 예</a>의 시나리오와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-216">This example is similar to the scenario in the <a href="#Scenario2"> second example</a>, where the schema is explicitly specified with JSON.</span></span> <span data-ttu-id="06f47-217">여기에서는 역직렬화하는 판독기에서 스키마를 알지 못한다는 점이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-217">The difference is that here, the schema is not assumed to be known to the reader that deserializes it.</span></span>

<span data-ttu-id="06f47-218">테스트 데이터 집합은 명시적으로 정의된 JSON 스키마를 통해 [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) 개체 목록으로 수집된 후 [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) 클래스로 표시된 개체 컨테이너 파일에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-218">The test data set is collected into a list of [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) objects via an explicitly defined JSON schema and then stored in an object container file represented by the [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span> <span data-ttu-id="06f47-219">이 컨테이너 파일은 압축 해제된 데이터를 메모리 스트림으로 직렬화하여 파일에 저장하는 데 사용되는 기록기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-219">This container file creates a writer that is used to serialize the data, uncompressed, to a memory stream that is then saved to a file.</span></span> <span data-ttu-id="06f47-220">판독기를 만드는 데 사용되는 [**Codec.Null**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) 매개 변수를 통해 이 데이터가 압축되지 않도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-220">The [**Codec.Null**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parameter used for creating the reader specifies that this data is not compressed.</span></span>

<span data-ttu-id="06f47-221">그런 후 파일에서 이 데이터를 읽은 다음 개체 컬렉션으로 역직렬화합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-221">The data is then read from the file and deserialized into a collection of objects.</span></span> <span data-ttu-id="06f47-222">이 컬렉션은 Avro 레코드 초기 목록과 비교되어 동일한지 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-222">This collection is compared to the initial list of Avro records to confirm that they are identical.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro.Schema;
        using Microsoft.Hadoop.Avro;

        //This class contains all methods demonstrating
        //the usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes a sample data set by using a generic record and Avro object container files.
            //Serialized data is not compressed.
            public void SerializeDeserializeUsingObjectContainersGenericRecord()
            {
                Console.WriteLine("SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleGenericRecordNullCodec.avro";

                Console.WriteLine("Defining the Schema and creating Sample Data Set...");

                //Define the schema in JSON
                const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

                //Create a generic serializer based on the schema
                var serializer = AvroSerializer.CreateGeneric(Schema);
                var rootSchema = serializer.WriterSchema as RecordSchema;

                //Create a generic record to represent the data
                var testData = new List<AvroRecord>();

                dynamic expected1 = new AvroRecord(rootSchema);
                dynamic location1 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location1.Floor = 1;
                location1.Room = 243;
                expected1.Location = location1;
                expected1.Value = new byte[] { 1, 2, 3, 4, 5 };
                testData.Add(expected1);

                dynamic expected2 = new AvroRecord(rootSchema);
                dynamic location2 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location2.Floor = 1;
                location2.Room = 244;
                expected2.Location = location2;
                expected2.Value = new byte[] { 6, 7, 8, 9 };
                testData.Add(expected2);

                //Serializing and saving data to file.
                //Create a MemoryStream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects to stream.
                    //Data is not compressed (Null compression codec).
                    using (var writer = AvroContainer.CreateGenericWriter(Schema, buffer, Codec.Null))
                    {
                        using (var streamWriter = new SequentialWriter<object>(writer, 24))
                        {
                            // Serialize the data to stream by using the sequential writer
                            testData.ForEach(streamWriter.Write);
                        }
                    }

                    Console.WriteLine("Saving serialized data to file...");

                    //Save stream to file
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing the data.
                //Create a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from the given stream.
                    //It allows iterating over the deserialized objects because it implements the IEnumerable<T> interface.
                    using (var reader = AvroContainer.CreateGenericReader(buffer))
                    {
                        using (var streamReader = new SequentialReader<object>(reader))
                        {
                            var results = streamReader.Objects;

                            Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                            //Finally, verify the results
                            var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = (dynamic)serialized, actual = (dynamic)deserialized });
                            int count = 1;
                            foreach (var pair in pairs)
                            {
                                bool isEqual = pair.expected.Location.Floor.Equals(pair.actual.Location.Floor);
                                isEqual = isEqual && pair.expected.Location.Room.Equals(pair.actual.Location.Room);
                                isEqual = isEqual && ((byte[])pair.expected.Value).SequenceEqual((byte[])pair.actual.Value);
                                Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                                count++;
                            }
                        }
                    }
                }

                //Delete the file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Saving memory stream to a new file with the given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during creation and writing to the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using the given path to a memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("The following exception was thrown during reading from the file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using the given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during deleting the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of the AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using generic record to Avro object container file
                Sample.SerializeDeserializeUsingObjectContainersGenericRecord();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES
    //
    // Defining the Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Saving serialized data to file...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a><span data-ttu-id="06f47-223">샘플 5: 사용자 지정 압축 코덱과 함께 개체 컨테이너 파일을 사용한 직렬화</span><span class="sxs-lookup"><span data-stu-id="06f47-223">Sample 5: Serialization using object container files with a custom compression codec</span></span>
<span data-ttu-id="06f47-224">5번째 예는 Avro 개체 컨테이너 파일에 대해 사용자 지정 압축 코덱을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-224">The fifth example shows how to use a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="06f47-225">이 예에 대한 코드를 포함하는 샘플은 [Azure 코드 샘플](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) (영문) 사이트에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-225">A sample containing the code for this example can be downloaded from the [Azure code samples](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) site.</span></span>

<span data-ttu-id="06f47-226">[Avro 사양](http://avro.apache.org/docs/current/spec.html#Required+Codecs)에서는 **Null** 및 **Deflate** 기본값 외에도 선택적 압축 코덱을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-226">The [Avro Specification](http://avro.apache.org/docs/current/spec.html#Required+Codecs) allows usage of an optional compression codec (in addition to **Null** and **Deflate** defaults).</span></span> <span data-ttu-id="06f47-227">이 예는 Snappy( [Avro 사양](http://avro.apache.org/docs/current/spec.html#snappy)에 지원되는 선택적 코덱으로 명시) 같은 새로운 코덱을 구현하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-227">This example is not implementing a new codec such as Snappy (mentioned as a supported optional codec in the [Avro Specification](http://avro.apache.org/docs/current/spec.html#snappy)).</span></span> <span data-ttu-id="06f47-228">여기서는 기본 .NET Framework 4 버전보다 더 나은 [zlib](http://zlib.net/) 압축 라이브러리 기반의 압축 알고리즘을 제공하는 .NET Framework 4.5에서 구현된 [**Deflate**][deflate-110] 코덱 사용 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-228">It shows how to use the .NET Framework 4.5 implementation of the [**Deflate**][deflate-110] codec, which provides a better compression algorithm based on the [zlib](http://zlib.net/) compression library than the default .NET Framework 4 version.</span></span>

    //
    // This code needs to be compiled with the parameter Target Framework set as ".NET Framework 4.5"
    // to ensure the desired implementation of the Deflate compression algorithm is used.
    // Ensure your C# project is set up accordingly.
    //

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.IO;
        using System.IO.Compression;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        #region Defining objects for serialization
        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }
        #endregion

        #region Defining custom codec based on .NET Framework V.4.5 Deflate
        //Avro.NET codec class contains two methods,
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed),
        //which are the key ones for data compression.
        //To enable a custom codec, one needs to implement these methods for the required codec.

        #region Defining Compression and Decompression Streams
        //DeflateStream (class from System.IO.Compression namespace that implements Deflate algorithm)
        //cannot be directly used for Avro because it does not support vital operations like Seek.
        //Thus one needs to implement two classes inherited from stream
        //(one for compressed and one for decompressed stream)
        //that use Deflate compression and implement all required features.
        internal sealed class CompressionStreamDeflate45 : Stream
        {
            private readonly Stream buffer;
            private DeflateStream compressionStream;

            public CompressionStreamDeflate45(Stream buffer)
            {
                Debug.Assert(buffer != null, "Buffer is not allowed to be null.");

                this.compressionStream = new DeflateStream(buffer, CompressionLevel.Fastest, true);
                this.buffer = buffer;
            }

            public override bool CanRead
            {
                get { return this.buffer.CanRead; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return this.buffer.CanWrite; }
            }

            public override void Flush()
            {
                this.compressionStream.Close();
            }

            public override long Length
            {
                get { return this.buffer.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.buffer.Position;
                }

                set
                {
                    this.buffer.Position = value;
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.buffer.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                return this.buffer.Seek(offset, origin);
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                this.compressionStream.Write(buffer, offset, count);
            }

            protected override void Dispose(bool disposed)
            {
                base.Dispose(disposed);

                if (disposed)
                {
                    this.compressionStream.Dispose();
                    this.compressionStream = null;
                }
            }
        }

        internal sealed class DecompressionStreamDeflate45 : Stream
        {
            private readonly DeflateStream decompressed;

            public DecompressionStreamDeflate45(Stream compressed)
            {
                this.decompressed = new DeflateStream(compressed, CompressionMode.Decompress, true);
            }

            public override bool CanRead
            {
                get { return true; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return false; }
            }

            public override void Flush()
            {
                this.decompressed.Close();
            }

            public override long Length
            {
                get { return this.decompressed.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.decompressed.Position;
                }

                set
                {
                    throw new NotSupportedException();
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.decompressed.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                throw new NotSupportedException();
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                throw new NotSupportedException();
            }

            protected override void Dispose(bool disposing)
            {
                base.Dispose(disposing);

                if (disposing)
                {
                    this.decompressed.Dispose();
                }
            }
        }
        #endregion

        #region Define Codec
        //Define the actual codec class containing the required methods for manipulating streams:
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed).
        //Codec class uses classes for compressed and decompressed streams defined above.
        internal sealed class DeflateCodec45 : Codec
        {

            //We merely use different IMPLEMENTATIONS of Deflate, so CodecName remains "deflate"
            public static readonly string CodecName = "deflate";

            public DeflateCodec45()
                : base(CodecName)
            {
            }

            public override Stream GetCompressedStreamOver(Stream decompressed)
            {
                if (decompressed == null)
                {
                    throw new ArgumentNullException("decompressed");
                }

                return new CompressionStreamDeflate45(decompressed);
            }

            public override Stream GetDecompressedStreamOver(Stream compressed)
            {
                if (compressed == null)
                {
                    throw new ArgumentNullException("compressed");
                }

                return new DecompressionStreamDeflate45(compressed);
            }
        }
        #endregion

        #region Define modified Codec Factory
        //Define modified codec factory to be used in the reader.
        //It catches the attempt to use "Deflate" and provide  a custom codec.
        //For all other cases, it relies on the base class (CodecFactory).
        internal sealed class CodecFactoryDeflate45 : CodecFactory
        {

            public override Codec Create(string codecName)
            {
                if (codecName == DeflateCodec45.CodecName)
                    return new DeflateCodec45();
                else
                    return base.Create(codecName);
            }
        }
        #endregion

        #endregion

        #region Sample Class with demonstration methods
        //This class contains methods demonstrating
        //the usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with the custom compression codec (Deflate of .NET Framework 4.5).
            //
            //This sample uses memory stream for all operations related to serialization, deserialization and
            //object container manipulation, though file stream could be easily used.
            public void SerializeDeserializeUsingObjectContainersReflectionCustomCodec()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate45.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data to file.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects to stream.
                    //Here the custom codec is introduced. For convenience, the next commented code line shows how to use built-in Deflate.
                    //Note that because the sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, new DeflateCodec45()))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize the data to stream using the sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream to file
                    Console.WriteLine("Saving serialized data to file...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Because of SequentialReader<T> constructor signature, an AvroSerializerSettings instance is required
                    //when codec factory is explicitly specified.
                    //You may comment the line below if you want to use built-in Deflate (see next comment).
                    AvroSerializerSettings settings = new AvroSerializerSettings();

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from the given stream.
                    //It allows iterating over the deserialized objects because it implements the IEnumerable<T> interface.
                    //Here the custom codec factory is introduced.
                    //For convenience, the next commented code line shows how to use built-in Deflate
                    //(no explicit Codec Factory parameter is required in this case).
                    //Note that because the sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var reader = new SequentialReader<SensorData>(AvroContainer.CreateReader<SensorData>(buffer, true)))
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true, settings, new CodecFactoryDeflate45())))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches the original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        bool isEqual;
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                            count++;
                        }
                    }
                }

                //Delete the file
                RemoveFile(path);
            }
        #endregion

            #region Helper Methods

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream to a new file with the given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during creation and writing to the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading file content by using the given path to a memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("The following exception was thrown during reading from the file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during deleting the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }
            #endregion

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection to Avro object container file using custom codec
                Sample.SerializeDeserializeUsingObjectContainersReflectionCustomCodec();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC
    //
    // Serializing Sample Data Set...
    // Saving serialized data to file...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    //For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.

## <a name="sample-6-using-avro-to-upload-data-for-the-microsoft-azure-hdinsight-service"></a><span data-ttu-id="06f47-229">샘플 6: Avro를 사용하여 Microsoft Azure HDInsight 서비스에 대한 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="06f47-229">Sample 6: Using Avro to upload data for the Microsoft Azure HDInsight service</span></span>
<span data-ttu-id="06f47-230">6번째 예는 Azure HDInsight 서비스 조작과 관련된 몇 가지 프로그래밍 기법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-230">The sixth example illustrates some programming techniques related to interacting with the Azure HDInsight service.</span></span> <span data-ttu-id="06f47-231">이 예에 대한 코드를 포함하는 샘플은 [Azure 코드 샘플](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) (영문) 사이트에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-231">A sample containing the code for this example can be downloaded from the [Azure code samples](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) site.</span></span>

<span data-ttu-id="06f47-232">이 샘플은 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-232">The sample does the following tasks:</span></span>

* <span data-ttu-id="06f47-233">기존 HDInsight 서비스 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-233">Connects to an existing HDInsight service cluster.</span></span>
* <span data-ttu-id="06f47-234">여러 CSV 파일을 직렬화하고 결과를 Azure Blob 저장소에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-234">Serializes several CSV files and uploads the result to Azure Blob storage.</span></span> <span data-ttu-id="06f47-235">(CSV 파일은 샘플과 함께 배포되고 1970-2010 기간에 [Infochimps](http://www.infochimps.com/) 로 배포된 AMEX 증권 기록 데이터의 추출을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-235">(The CSV files are distributed together with the sample and represent an extract from AMEX Stock historical data distributed by [Infochimps](http://www.infochimps.com/) for the period 1970-2010.</span></span> <span data-ttu-id="06f47-236">이 샘플은 CSV 파일 데이터를 읽고, 레코드를 **Stock** 클래스 인스턴스로 변환하고, 리플렉션을 사용하여 직렬화합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-236">The sample reads CSV file data, converts the records to instances of the **Stock** class, and then serializes them by using reflection.</span></span> <span data-ttu-id="06f47-237">Stock 형식 정의는 Microsoft Avro 라이브러리 코드 생성 유틸리티를 사용하여 JSON 스키마에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-237">Stock type definition is created from a JSON schema via the Microsoft Avro Library code generation utility.</span></span>
* <span data-ttu-id="06f47-238">Hive에서 **Stocks** 라는 새 외부 테이블을 만들고 이전 단계에서 업로드한 데이터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-238">Creates a new external table called **Stocks** in Hive, and links it to the data uploaded in the previous step.</span></span>
* <span data-ttu-id="06f47-239">Hive를 사용하여 **Stocks** 테이블에 대해 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-239">Executes a query by using Hive over the **Stocks** table.</span></span>

<span data-ttu-id="06f47-240">또한 주요 작업을 수행하기 전과 수행한 후에 정리 절차를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-240">In addition, the sample performs a clean-up procedure before and after performing major operations.</span></span> <span data-ttu-id="06f47-241">정리하는 동안 모든 관련된 Azure Blob 데이터 및 폴더가 제거되고 Hive 테이블이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-241">During the clean-up, all of the related Azure Blob data and folders are removed, and the Hive table is dropped.</span></span> <span data-ttu-id="06f47-242">샘플 명령줄에서 정리 프로시저를 호출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-242">You can also invoke the clean-up procedure from the sample command line.</span></span>

<span data-ttu-id="06f47-243">이 샘플을 사용하려면 다음 필수 조건이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-243">The sample has the following prerequisites:</span></span>

* <span data-ttu-id="06f47-244">활성 Microsoft Azure 구독 및 해당 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-244">An active Microsoft Azure subscription and its subscription ID.</span></span>
* <span data-ttu-id="06f47-245">해당 개인 키가 포함된 구독에 대한 관리 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-245">A management certificate for the subscription with the corresponding private key.</span></span> <span data-ttu-id="06f47-246">인증서는 샘플을 실행하는 데 사용되는 컴퓨터에 있는 현재 사용자 개인 저장소에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-246">The certificate should be installed in the current user private storage on the machine used to run the sample.</span></span>
* <span data-ttu-id="06f47-247">활성 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-247">An active HDInsight cluster.</span></span>
* <span data-ttu-id="06f47-248">해당 주 또는 보조 액세스 키와 함께 이전 필수 조건에서 HDInsight 클러스터에 연결된 Azure Storage 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-248">An Azure Storage account linked to the HDInsight cluster from the previous prerequisite, together with the corresponding primary, or secondary access key.</span></span>

<span data-ttu-id="06f47-249">샘플을 실행하기 전에 샘플 구성 파일에 필수 조건의 모든 정보를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-249">All of the information from the prerequisites should be entered to the sample configuration file before the sample is run.</span></span> <span data-ttu-id="06f47-250">입력하는 방법에는 다음 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-250">There are two possible ways to do it:</span></span>

* <span data-ttu-id="06f47-251">샘플 루트 디렉터리에서 app.config 파일을 편집하고 샘플 빌드</span><span class="sxs-lookup"><span data-stu-id="06f47-251">Edit the app.config file in the sample root directory and then build the sample</span></span>
* <span data-ttu-id="06f47-252">먼저 샘플을 빌드하고 빌드 디렉터리에서 AvroHDISample.exe.config 편집</span><span class="sxs-lookup"><span data-stu-id="06f47-252">First build the sample, and then edit AvroHDISample.exe.config in the build directory</span></span>

<span data-ttu-id="06f47-253">두 경우 모두에서 모든 편집은 **<appSettings>** 설정 섹션에서 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-253">In both cases, all edits should be done in the **<appSettings>** settings section.</span></span> <span data-ttu-id="06f47-254">파일의 주석을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="06f47-254">Follow the comments in the file.</span></span>
<span data-ttu-id="06f47-255">샘플을 실행하려면 명령줄에서 다음 명령을 실행합니다. 여기서는 샘플이 포함된 ZIP 파일은 C:\AvroHDISample로 추출된다고 간주했고, 이외의 경우에는 상대 파일 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-255">The sample is run from the command line by executing the following command (where the .zip file with the sample was assumed to be extracted to C:\AvroHDISample; if otherwise, use the relevant file path):</span></span>

    AvroHDISample run C:\AvroHDISample\Data

<span data-ttu-id="06f47-256">클러스터를 정리하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="06f47-256">To clean up the cluster, run the following command:</span></span>

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx
