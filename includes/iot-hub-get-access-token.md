## <a name="obtain-an-azure-resource-manager-token"></a><span data-ttu-id="54828-101">Azure Resource Manager 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="54828-101">Obtain an Azure Resource Manager token</span></span>
<span data-ttu-id="54828-102">Azure Active Directory hello Azure 리소스 관리자를 사용 하 여 리소스에서 수행 하는 모든 hello 작업을 인증 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54828-102">Azure Active Directory must authenticate all hello tasks that you perform on resources using hello Azure Resource Manager.</span></span> <span data-ttu-id="54828-103">hello 여기에 표시 된 예에서는 암호 인증을 사용할 경우 다른 인증 방법 참조 [인증 Azure 리소스 관리자 요청][lnk-authenticate-arm]합니다.</span><span class="sxs-lookup"><span data-stu-id="54828-103">hello example shown here uses password authentication, for other approaches see [Authenticating Azure Resource Manager requests][lnk-authenticate-arm].</span></span>

1. <span data-ttu-id="54828-104">다음 코드 toohello hello 추가 **Main** Program.cs tooretrieve hello 응용 프로그램 id와 암호를 사용 하 여 Azure AD에서 토큰의에서 메서드.</span><span class="sxs-lookup"><span data-stu-id="54828-104">Add hello following code toohello **Main** method in Program.cs tooretrieve a token from Azure AD using hello application id and password.</span></span>
   
    ```
    var authContext = new AuthenticationContext(string.Format  
      ("https://login.microsoftonline.com/{0}", tenantId));
    var credential = new ClientCredential(applicationId, password);
    AuthenticationResult token = authContext.AcquireTokenAsync
      ("https://management.core.windows.net/", credential).Result;
   
    if (token == null)
    {
      Console.WriteLine("Failed tooobtain hello token");
      return;
    }
    ```
2. <span data-ttu-id="54828-105">만들기는 **ResourceManagementClient** 사용 하 여 코드 toohello의 끝 다음 hello hello를 추가 하 여 토큰을 hello 개체 **Main** 메서드:</span><span class="sxs-lookup"><span data-stu-id="54828-105">Create a **ResourceManagementClient** object that uses hello token by adding hello following code toohello end of hello **Main** method:</span></span>
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. <span data-ttu-id="54828-106">만들기, 또는 사용 하는 hello 리소스 그룹에 대 한 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="54828-106">Create, or obtain a reference to, hello resource group you are using:</span></span>
   
    ```
    var rgResponse = client.ResourceGroups.CreateOrUpdate(rgName,
        new ResourceGroup("East US"));
    if (rgResponse.Properties.ProvisioningState != "Succeeded")
    {
      Console.WriteLine("Problem creating resource group");
      return;
    }
    ```

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx