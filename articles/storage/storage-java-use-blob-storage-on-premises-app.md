---
title: "blob 저장소 (Java) aaaOn 온-프레미스 응용 프로그램 | Microsoft Docs"
description: "Toocreate 업로드 한 이미지 tooAzure 차례로 표시 하는 콘솔 응용 프로그램 브라우저에서 이미지를 hello 하는 방법에 대해 알아봅니다. 코드 샘플은 Java로 작성되었습니다."
services: storage
documentationcenter: java
author: mmacy
manager: carmonm
editor: tysonn
ms.assetid: ccc9a7d7-6fe4-467b-b7fd-a73f17539e3f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/17/2016
ms.author: marsma
ms.openlocfilehash: ed8eb4c1045691c25abe94bf6c1b18b797adc3e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="on-premises-application-with-blob-storage"></a>Blob 저장소를 사용하는 온-프레미스 응용 프로그램
## <a name="overview"></a>개요
hello 다음 예제에 나와 Azure 저장소를 사용 하 여 Azure에서 이미지를 저장 하는 방법을 합니다. 이 문서에 hello 코드 이미지 tooAzure를 업로드 하 고 다음 브라우저에서 hello 이미지를 표시 하는 HTML 파일을 만듭니다는 콘솔 응용 프로그램입니다.

## <a name="prerequisites"></a>필수 조건
* JDK(Java Developer Kit) 버전 1.6 이상이 설치되어 있어야 합니다.
* hello Azure SDK가 설치 되어 있습니다.
* Java 용 Azure 라이브러리 hello JAR hello 및 모든 해당 종속성 Jar 설치 되 고 Java 컴파일러에서 사용 하는 hello 빌드 경로에 됩니다. Java 용 Azure 라이브러리 hello를 설치 하는 방법에 대 한 정보를 참조 하십시오. [다운로드 hello Azure SDK for Java](../java-download-azure-sdk.md)합니다.
* Azure 저장소 계정이 설정되어 있어야 합니다. hello 계정 이름과 계정 키 hello 저장소 계정에 대 한 사용 됩니다이 문서의 hello 코드에서. 참조 [어떻게 tooCreate 저장소 계정을](storage-create-storage-account.md#create-a-storage-account) 저장소 계정을 만드는 방법에 대 한 내용은 및 [저장소 액세스 키 보기 및 복사](storage-create-storage-account.md#view-and-copy-storage-access-keys) hello 계정 키를 검색 하는 방법에 대 한 정보에 대 한 합니다.
* 명명 된 로컬 이미지 파일을 만든 hello path c:에 저장 되지만\\myimages\\image1.jpg 합니다. 또는 수정할는 **FileInputStream** hello 예제 toouse 다른 이미지 경로 및 파일 이름에에서는 생성자입니다.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="toouse-azure-blob-storage-tooupload-a-file"></a>toouse Azure blob 저장소 tooupload 파일
여기서는 단계별 절차를 제공합니다. Tooskip 미리, 원하는 경우 hello 전체 코드는이 문서의 뒷부분에 표시 됩니다.

Hello Azure 핵심 저장소 클래스, hello Azure blob 클라이언트 클래스, hello Java IO 클래스 및 hello에 대 한 가져오기를 포함 하 여 hello 코드 시작 **URISyntaxException** 클래스입니다.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

이라는 클래스를 선언 **StorageSample**, hello 괄호를 포함 하 고 **{**합니다.

```java
public class StorageSample {
```

Hello 내 **StorageSample** 클래스, 기본 끝점 프로토콜 hello, 저장소 계정 이름 및 Azure 저장소 계정에 지정 된 저장소 액세스 키를 포함 될 문자열 변수를 선언 합니다. Hello 자리 표시자 값을 대체 **프로그램\_계정\_이름** 및 **프로그램\_계정\_키** 사용자 고유의 계정 이름과 계정 키를 각각.

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

에 대 한 선언에서 추가 **주**, 포함 한 **시도** 블록과 hello 필요한 여는 괄호를 포함 **{**합니다.

```java
    public static void main(String[] args)
    {
        try
        {
```

Hello 형식 (이 예제에서 사용 방법에 대 한 설명은 됩니다 hello) 다음의 변수를 선언 합니다.

* **CloudStorageAccount**: 사용 되는 tooinitialize hello 계정 blob 클라이언트 개체를 Azure 저장소 계정 이름 및 키 및 toocreate 포함 개체입니다.
* **CloudBlobClient**: tooaccess hello blob 서비스를 사용 합니다.
* **CloudBlobContainer**: blob 컨테이너를 사용 하는 toocreate hello 컨테이너 및 delete hello 컨테이너에 blob를 나열 합니다.
* **CloudBlockBlob**: 사용 되는 tooupload 로컬 이미지 파일 toothe 컨테이너입니다.

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

할당 값 toohello **계정** 변수입니다.

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

할당 값 toohello **serviceClient** 변수입니다.

```java
serviceClient = account.createCloudBlobClient();
```

할당 값 toohello **컨테이너** 변수입니다. 라는 참조 tooa 컨테이너 살펴보겠습니다 **gettingstarted**합니다.

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

Hello 컨테이너를 만듭니다. 사이트 존재 하지 않는 경우이 메서드는 hello 컨테이너를 만듭니다 (다음 다시 돌아와 **true**). Hello 컨테이너가 존재 하는 경우 반환 **false**합니다. 대신 너무**경고는 createIfNotExists** 는 hello **만들** 메서드 (hello 컨테이너가 이미 존재 하는 경우 오류가 반환 됩니다).

```java
container.createIfNotExists();
```

Hello 컨테이너에 대 한 익명 액세스를 설정 합니다.

```java
// Set anonymous access on hello container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

Azure 저장소에 blob hello를 나타내는 참조 toohello 블록 blob을 가져옵니다.

```java
blob = container.getBlockBlobReference("image1.jpg");
```

사용 하 여 hello **파일** 생성자 tooget 참조 toohello 로컬로 만들어진 파일을 업로드 합니다. Hello 코드를 실행 하기 전에이 파일을 만들었는지 확인 합니다.

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

호출 toohello 통해 hello 로컬 파일을 업로드 **CloudBlockBlob.upload** 메서드. 첫 번째 매개 변수 toohello hello **CloudBlockBlob.upload** 메서드는 한 **FileInputStream** 될 해당 나타냅니다 hello 로컬 파일 업로드 tooAzure 저장소 개체입니다. hello 두 번째 매개 변수는 hello 파일의 바이트에서 hello 크기입니다.

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

도우미 함수를 호출 **MakeHTMLPage**, toomake 기본 HTML 페이지를 포함 하는  **&lt;이미지&gt;**  이제 Azure에 있는 hello 소스 집합 toohello blob과 함께 요소 저장소 계정입니다. 에 대 한 코드 hello **MakeHTMLPage** 이 문서의 뒷부분에서 설명 됩니다.

```java
MakeHTMLPage(container);
```

상태 메시지 및 생성 된 HTML 페이지 hello에 대 한 정보를 출력 합니다.

```java
System.out.println("Processing complete.");
System.out.println("Open index.html toosee hello images stored in your storage account.");
```

닫기 hello **시도** 닫는 괄호를 삽입 하 여 블록: **}**

Hello 다음 예외를 처리 합니다.

* **FileNotFoundException**: hello throw 될 수 있는 **FileInputStream** 또는 **FileOutputStream** 생성자입니다.
* **StorageException**: hello Azure 클라이언트 저장소 라이브러리에 의해 throw 될 수 있습니다.
* **URISyntaxException**: hello throw 될 수 있는 **ListBlobItem.getUri** 메서드.
* **Exception**: 일반적인 예외 처리입니다.

<!-- -->

```java
catch (FileNotFoundException fileNotFoundException)
{
    System.out.print("FileNotFoundException encountered: ");
    System.out.println(fileNotFoundException.getMessage());
    System.exit(-1);
}
catch (StorageException storageException)
{
    System.out.print("StorageException encountered: ");
    System.out.println(storageException.getMessage());
    System.exit(-1);
}
catch (URISyntaxException uriSyntaxException)
{
    System.out.print("URISyntaxException encountered: ");
    System.out.println(uriSyntaxException.getMessage());
    System.exit(-1);
}
catch (Exception e)
{
    System.out.print("Exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

닫는 중괄호(**}**)를 삽입하여 **main**을 닫습니다.

라는 메서드를 만듭니다 **MakeHTMLPage** toocreate 기본 HTML 페이지입니다. 이 메서드는 형식 매개 변수가 **CloudBlobContainer**, 업로드 된 blob의 hello 목록에서 사용 되는 tooiterate 됩니다. 이 메서드는 형식의 예외를 throw **FileNotFoundException**, hello에 의해 throw 될 수 있는 **FileOutputStream** 생성자 및 **URISyntaxException**를 수 있습니다 hello를 통해 throw 될 **ListBlobItem.getUri** 메서드. 여는 중괄호( **{**)를 포함합니다.

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

이름이 **index.html**인 로컬 파일을 만듭니다.

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

Hello에 추가 하는 toohello 로컬 파일을 작성할  **&lt;html&gt;**,  **&lt;헤더&gt;**, 및  **&lt;본문&gt;**  요소입니다.

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

업로드 된 blob의 hello 목록을 반복 합니다. 각 blob에 대 한 만들기에 hello HTML 페이지에는  **&lt;img&gt;**  를 가진 요소가 해당 **src** 특성을 Azure 저장소 계정에 있는 hello hello blob의 URI에 전송 합니다.
이 샘플에서는 이미지를 하나만 추가했지만 더 추가하면 이 코드는 모든 이미지를 반복합니다.

간단히 하기 위해 이 예제는 업로드된 각 Blob이 이미지라고 가정합니다. 이미지 이외의 blob 또는 페이지 blob 대신 블록 blob 업데이트 한 경우 필요에 따라 hello 코드를 조정 합니다.

```java
// Enumerate hello uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in hello HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

닫기 hello  **&lt;본문&gt;**  요소와 hello  **&lt;html&gt;**  요소입니다.

```java
stream.println("</body>");
stream.println("</html>");
```

로컬 파일을 닫기 hello입니다.

```java
stream.close();
```

닫는 중괄호(**}**)를 삽입하여 **MakeHTMLPage**를 닫습니다.

닫는 중괄호(**}**)를 삽입하여 **StorageSample**을 닫습니다.

hello 다음은이 예제에 대 한 hello 전체 코드입니다. Toomodify hello 자리 표시자 값을 기억 **프로그램\_계정\_이름** 및 **프로그램\_계정\_키** toouse 계정 이름 및 계정 키를, 각각.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;

// Create an image, c:\myimages\image1.jpg, prior toorunning this sample.
// Alternatively, change hello value used by hello FileInputStream constructor
// toouse a different image path and file that you have already created.
public class StorageSample {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                    "AccountName=your_account_name;" +
                    "AccountKey=your_account_name";

    public static void main(String[] args) {
        try {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;
            CloudBlockBlob blob;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.createIfNotExists();

            // Set anonymous access on hello container.
            BlobContainerPermissions containerPermissions;
            containerPermissions = new BlobContainerPermissions();
            containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
            container.uploadPermissions(containerPermissions);

            // Upload an image file.
            blob = container.getBlockBlobReference("image1.jpg");

            File fileReference = new File("c:\\myimages\\image1.jpg");
            blob.upload(new FileInputStream(fileReference), fileReference.length());

            // At this point hello image is uploaded.
            // Next, create an HTML page that lists all of hello uploaded images.
            MakeHTMLPage(container);

            System.out.println("Processing complete.");
            System.out.println("Open index.html toosee hello images stored in your storage account.");

        } catch (FileNotFoundException fileNotFoundException) {
            System.out.print("FileNotFoundException encountered: ");
            System.out.println(fileNotFoundException.getMessage());
            System.exit(-1);
        } catch (StorageException storageException) {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        } catch (URISyntaxException uriSyntaxException) {
            System.out.print("URISyntaxException encountered: ");
            System.out.println(uriSyntaxException.getMessage());
            System.exit(-1);
        } catch (Exception e) {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }

    // Create an HTML page that can be used toodisplay hello uploaded images.
    // This example assumes all of hello blobs are for images.
    public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
    {
        PrintStream stream;
        stream = new PrintStream(new FileOutputStream("index.html"));

        // Create hello opening <html>, <header>, and <body> elements.
        stream.println("<html>");
        stream.println("<header/>");
        stream.println("<body>");

        // Enumerate hello uploaded blobs.
        for (ListBlobItem blobItem : container.listBlobs()) {
            // List each blob as an <img> element in hello HTML body.
            stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
        }

        stream.println("</body>");

        // Complete hello <html> element and close hello file.
        stream.println("</html>");
        stream.close();
    }
}
```

또한 toouploading 로컬 이미지 파일 tooAzure 저장소 hello 예제 코드를 만듭니다 브라우저 toosee에서 열 수 있는 한 로컬 파일 namedindex.html 업로드 된 이미지입니다.

Hello 코드 계정 이름과 계정 키에 포함 되어 있으므로 소스 코드 보안 인지 확인 합니다.

## <a name="toodelete-a-container"></a>toodelete 컨테이너
저장소에 대 한 요금이 청구 되므로 toodelete 경우가 **gettingstarted** 컨테이너 완료 한 후이 예제에서는 작업할 수 있도록 합니다. toodelete 컨테이너를 사용 하 여 hello **CloudBlobContainer.delete** 메서드.

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

toocall hello **CloudBlobContainer.delete** 메서드를 초기화 하는 hello 프로세스 **CloudStorageAccount**, **ClodBlobClient**, 및  **CloudBlobContainer** 개체에 대 한 표시 된 것 처럼 동일 hello는 **createIfNotExist** 메서드. hello 다음은 hello 라는 컨테이너를 삭제 하는 전체 예제 **gettingstarted**합니다.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;

public class DeleteContainer {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                "AccountName=your_account_name;" +
                "AccountKey=your_account_key";

    public static void main(String[] args)
    {
        try
        {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.delete();

            System.out.println("Container deleted.");

        }
        catch (StorageException storageException)
        {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        }
        catch (Exception e)
        {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }
}
```

다른 blob 저장소 클래스와 메서드의 개요를 참조 하십시오. [어떻게 toouse Java에서 Blob 저장소](storage-java-how-to-use-blob-storage.md)합니다.

## <a name="next-steps"></a>다음 단계
이러한 링크 toolearn 더 복잡 한 저장소 작업에 대 한 자세한를 따릅니다.

* [Java용 Azure 저장소 SDK](https://github.com/azure/azure-storage-java)
* [Azure 저장소 클라이언트 SDK 참조](http://dl.windowsazure.com/storage/javadoc/)
* [Azure Storage 서비스 REST API](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Azure 저장소 팀 블로그](http://blogs.msdn.com/b/windowsazurestorage/)

