# MicroORM.Oracle : Overview
A high performance Micro-ORM supporting Oracle Database Server. This is the extension version for easy to configure and use.
# Packages
NuGet library: https://www.nuget.org/packages/MicroORM.Oracle
# Installation

````
NuGet\Install-Package MicroORM.Oracle
````
# Features
````
Query
QueryAsync
QueryFirst
QueryFirstAsync
QuerySingle
QuerySingleAsync
QueryFirstOrDefault
QueryFirstOrDefaultAsync
QuerySingleOrDefault
QuerySingleOrDefaultAsync
QueryMultiple
QueryMultipleAsync
Execute
ExecuteAsync
ExecuteReader
ExecuteReaderAsync
ExecuteScalar
ExecuteScalarAsync
````

# How to use
You can configure this package in two ways. I will explain both two ways. you can use your suitable one.
### One 
You have to create a new class like ApplicationDbContext inherited from the DatabaseContext class that comes from this library.
you have to add using MicroORM.Oracle namespace.
````
    public class ApplicationDbContext:DatabaseContext
    {
        public ApplicationDbContext():base("DatabaseConnectionString")
        {
        }
    }   
 
````
Controller code sample.
````
    [ApiController]
    [Route("[controller]/[action]")]
    public class TestController : ControllerBase
    {                      
        [HttpGet]
        public IActionResult GetAll()
        {
            ApplicationDbContext dbContext = new ApplicationDbContext();
            var data= dbContext.Query<ReturnType>("Query").ToList();
            return Ok(data);
        }        
    }
````

### Two
If you use dependency injection then this option is for you.
````
    using MicroORM.Oracle;
    
    builder.Services.AddDatabaseContext(options =>
    {
        options.ConnectionString = "DatabaseConnectionString"
    });
````
Controller code sample.
````
    [ApiController]
    [Route("[controller]/[action]")]
    public class TestController : ControllerBase
    {
        ApplicationDbContext _dbContext;
        public TestController(ApplicationDbContext dbContext) 
        { 
          _dbContext=dbContext;
        }               
        [HttpGet]
        public IActionResult GetAll()
        {            
            var data= _dbContext.Query<ReturnType>("Query").ToList();
            return Ok(data);
        }        
    }
````