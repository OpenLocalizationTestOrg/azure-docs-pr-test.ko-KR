<span data-ttu-id="53fd1-101">저장소 계정에 tooresources 액세스 권한을 부여 하는 공유 액세스 서명 (SAS) URL을가지고 있으면 hello SAS 연결 문자열에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53fd1-101">If you possess a shared access signature (SAS) URL that grants you access tooresources in a storage account, you can use hello SAS in a connection string.</span></span> <span data-ttu-id="53fd1-102">Hello SAS hello 정보 필요한 tooauthenticate hello 요청에 포함 되어 있으므로 SAS 가진 연결 문자열이 hello 프로토콜, hello 서비스 끝점 및 hello 필요한 자격 증명 tooaccess hello 리소스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="53fd1-102">Because hello SAS contains hello information required tooauthenticate hello request, a connection string with a SAS provides hello protocol, hello service endpoint, and hello necessary credentials tooaccess hello resource.</span></span>

<span data-ttu-id="53fd1-103">toocreate 공유 액세스 서명을 포함 하는 연결 문자열 형식에 따라 hello에 hello 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="53fd1-103">toocreate a connection string that includes a shared access signature, specify hello string in hello following format:</span></span>

```
BlobEndpoint=myBlobEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
FileEndpoint=myFileEndpoint;
SharedAccessSignature=sasToken
```

<span data-ttu-id="53fd1-104">Hello 연결 문자열 하나 이상 포함 해야 하지만 각 서비스 끝점은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="53fd1-104">Each service endpoint is optional, although hello connection string must contain at least one.</span></span>

> [!NOTE]
> <span data-ttu-id="53fd1-105">SAS와 함께 HTTPS를 사용하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="53fd1-105">Using HTTPS with a SAS is recommended as a best practice.</span></span>
>
> <span data-ttu-id="53fd1-106">SAS를 구성 파일에서 연결 문자열을 지정 하는 경우 tooencode hello URL의 특수 문자를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53fd1-106">If you are specifying a SAS in a connection string in a configuration file, you may need tooencode special characters in hello URL.</span></span>
>
>

### <a name="service-sas-example"></a><span data-ttu-id="53fd1-107">서비스 SAS 예</span><span class="sxs-lookup"><span data-stu-id="53fd1-107">Service SAS example</span></span>
<span data-ttu-id="53fd1-108">다음은 Blob 저장소에 대한 서비스 SAS를 포함하는 연결 문자열의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="53fd1-108">Here's an example of a connection string that includes a service SAS for Blob storage:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&sr=b&si=tutorial-policy-635959936145100803&sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

<span data-ttu-id="53fd1-109">Hello의 예로 및 특수 문자 인코딩을 사용 하 여 동일한 연결 문자열:</span><span class="sxs-lookup"><span data-stu-id="53fd1-109">And here's an example of hello same connection string with encoding of special characters:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&amp;sr=b&amp;si=tutorial-policy-635959936145100803&amp;sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

### <a name="account-sas-example"></a><span data-ttu-id="53fd1-110">계정 SAS 예</span><span class="sxs-lookup"><span data-stu-id="53fd1-110">Account SAS example</span></span>
<span data-ttu-id="53fd1-111">다음은 Blob 및 파일 저장소에 대한 계정 SAS를 포함하는 연결 문자열의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="53fd1-111">Here's an example of a connection string that includes an account SAS for Blob and File storage.</span></span> <span data-ttu-id="53fd1-112">두 서비스에 대한 끝점이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="53fd1-112">Note that endpoints for both services are specified:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&spr=https&st=2016-04-12T03%3A24%3A31Z&se=2016-04-13T03%3A29%3A31Z&srt=s&ss=bf&sp=rwl
```

<span data-ttu-id="53fd1-113">Hello의 예로 및 URL 인코딩을 사용 하 여 동일한 연결 문자열:</span><span class="sxs-lookup"><span data-stu-id="53fd1-113">And here's an example of hello same connection string with URL encoding:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&amp;sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&amp;spr=https&amp;st=2016-04-12T03%3A24%3A31Z&amp;se=2016-04-13T03%3A29%3A31Z&amp;srt=s&amp;ss=bf&amp;sp=rwl
```

