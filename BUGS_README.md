# Library System API - Bug Documentation

This is a buggy Library Management System API built with .NET and n-tier architecture. The system contains **20 intentional bugs** across different layers (Models, Repositories, Services, Controllers, and Configuration).

## Architecture

The application follows n-tier architecture:
- **Models Layer**: Data models (Book, Member, Transaction)
- **Repository Layer**: Data access logic
- **Service Layer**: Business logic
- **Controller Layer**: API endpoints
- **Program.cs**: Dependency injection configuration

---

## Please List all of the bugs you find & where you found it


### EXAMPLE **Bug #1: Wrong HTTP Request method in MemberController**
**Location**: `Controllers/MemberController.cs` - Line 38  
**Type**: API Design Error  

**Bug 1**:
```csharp
    [HttpDelete("{id}")]
    public ActionResult<Member> Update(int id, [FromBody] Member member)
```

**Bug 2**:
**Location**: `BuggyBackend.csproj` - Line 4 
**Type**: Framework version error
 ```csharp
  <PropertyGroup>
    <TargetFramework>net10.0</TargetFramework> 
```

**Bug 3**:
**Location**: `BuggyBackend.csproj` - Line 10
**Type**: Version error
 ```csharp
    <PackageReference Include="Microsoft.AspNetCore.OpenApi" Version="10.0.1" />
```


**Bug 4**:
**Location**: `BuggyBackend\repositories\MemberRepository.cs(23,69)`
**Type**: syntax, missing quotation mark
 ```csharp
    new Member { Id = 3, Name = "Ken Martinez", Email = "jmartenezlopez@sjcoe.net, MembershipDate = DateTime.Now.AddMonths(-6) }
  ```


**Bug 5**:
**Location**: `BuggyBackend\repositories\MemberRepository.cs(40, 49)`
**Type**: syntax, missing equals sign
 ```csharp
              return _members.FirstOrDefault(m => m.Email = email);
  ```

**Bug 6**:
**Location**: `BuggyBackend\repositories\BookRepository.cs(37,47)`
**Type**: syntax, missing equals sign
 ```csharp
              return _members.FirstOrDefault(m => m.Email = email);
  ```

**Bug 7**:
**Location**: `BuggyBackend\Controllers\BooksController.cs(69,20)`
**Type**: validation, duplicate catch
 ```csharp
        catch (ArgumentNullException ex)
            {
                return BadRequest(ex.Message);
            }
  ```


**Bug 8**:
**Location**: `BuggyBackend\Program.cs - Line 11`
**Type**: dependency injection
 ```csharp
  builder.Services.AddSingleton<IBookRepository, BookRepository>();

  ```


**Bug 9**:
**Location**: `BuggyBackend\BuggyBackend.csproj - Line 11`
**Type**: configuration, missing swagger packages
 ```csharp
    <PackageReference Include="Swashbuckle.AspNetCore" Version="9.0.0" />
    <PackageReference Include="Swashbuckle.AspNetCore.SwaggerGen" Version="9.0.0" />
    <PackageReference Include="Swashbuckle.AspNetCore.SwaggerUI" Version="9.0.0" />
  ```


**Bug 10**:
**Location**: `BuggyBackend\Program.cs - Line 16`
**Type**: configuration, missing Endpoints
 ```csharp
builder.Services.AddEndpointsApiExplorer();
  ``` 


**Bug 11**:
**Location**: `BuggyBackend\Program.cs - Line 17`
**Type**: configuration, missing AddSwaggerGen
 ```csharp
builder.Services.AddSwaggerGen();
  ``` 

**Bug 12**:
**Location**: `BuggyBackend\Program.cs - Line 33`
**Type**: configuration, missing swagger configs
 ```csharp
    app.UseSwagger();
    app.UseSwaggerUI();
  ``` 


**Bug 13**:
**Location**: `BuggyBackend\Properties\launchSettings.json - Line 7, 16`
**Type**: configuration, launch browser set to false and missing launchUrl
 ```csharp
      "launchBrowser": false,
  ``` 

  **Bug 14**:
**Location**: `BuggyBackend\repositories\MemberRepository.cs - Line 17`
**Type**: dependency injection
 ```csharp
        private void InitializeData()
  ``` 

  **Bug 15**:
**Location**: `BuggyBackend\Services\LibraryServices.cs - Line 93`
**Type**: logic, should be 14 days after DateTime.Now - not before
 ```csharp
              var overdueDate = DateTime.Now.AddDays(-14);
  ``` 

**Bug 16**:
**Location**: `BuggyBackend\Services\LibraryServices.cs - Line 96`
**Type**: logic, should be greater than
 ```csharp
                .Where(t => t.BorrowDate < overdueDate)
  ``` 


**Bug 17-20**:
**Location**: `MemberRepository Lines 21-23`
**Type**: logic, borrowedbookids should be initialized
 ```csharp
                   new Member { Id = 1, Name = "Isaiah Ferguson", Email = "ifergusonlll@sjcoe.net", MembershipDate = DateTime.Now.AddYears(-2) },
                new Member { Id = 2, Name = "Jacob Dekok", Email = "jdekok@sjcoe.net", MembershipDate = DateTime.Now.AddYears(-1), },
                new Member { Id = 3, Name = "Ken Martinez", Email = "jmartenezlopez@sjcoe.net", MembershipDate = DateTime.Now.AddMonths(-6) }   
  ``` 



