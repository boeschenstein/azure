# New Frontend/Backend Project with Angular 13

(no DevOps: source locally handled)

Ideas from <https://www.c-sharpcorner.com/article/easily-create-spa-with-net-6-0-and-angular-13-and-deploy-to-azure/>

## Create new Angular App

- open Vs2022, create new Project, select template 'ASP.NET Core with Angular'
- run it to test the app, you should see a page with header (Home, Counter, Fetch data) and a title 'Hello, world!'

## Deploy it to Azure

### Azure Portal: create Web App

- in `pp Service`: Create `Web App`
- select subscription, select or create Resource Group
- enter name: `angular13webapi`
- Runtime stack: `.NET 6 (LTS)`
- Region: close to your place
- Optional: disable Application Insights

### Publish

- in VS 2022, right-click on project, click on `Publish...`
- select `Azure`, next
- select `Azure App Service (Windows)`, next
- select the Web Api you created (I created `angular13webapi`)
- Press `Finish`
- Check config
- Press `Publish`

## Add SQL Server

- Add nugets
  - `dotnet add package Microsoft.EntityFrameworkCore.SqlServer`
  - `dotnet add package Microsoft.EntityFrameworkCore.Tools`

- Add a table (I'm using the existing table `WeatherForecast`). Just add a property for PK (otherwise EF will throw an error:
'The entity type 'WeatherForecast' requires a primary key to be defined. If you intended to use a keyless entity type, call 'HasNoKey' in 'OnModelCreating'. For more information on keyless entity types, see https://go.microsoft.com/fwlink/?linkid=2141943.')

```cs
// add PK to WeatherForecast:
public int Id { get; set; }

// or add the following to OnModelCreating(ModelBuilder builder)
builder.Entity<WeatherForecast>().HasNoKey();
```

- Add DBContext:

```cs
public class MyDbContext : DbContext
{
    public MyDbContext(DbContextOptions<MyDbContext> options)
        : base(options) { }

    public DbSet<WeatherForecast>? WeatherForecasts { get; set; }

    protected override void OnModelCreating(ModelBuilder builder)
    {
        base.OnModelCreating(builder);
    }
}
```

- Use MyDbContext in `Program.cs`:

```cs
builder.Services.AddDbContext<MyDbContext>(options => options.UseSqlServer(builder.Configuration.GetConnectionString("ConnStr")));
```

- Add Connection String to `appSettings.json`

```json
{
  "Logging": { ... }
  "AllowedHosts": "*",
  "ConnectionStrings": {
    "ConnStr": "Data Source=(localdb)\\MSSQLLocalDB;Initial Catalog=MyAngular13TestDB;Integrated Security=True;ApplicationIntent=ReadWrite;MultiSubnetFailover=False"
  }
}
```

- Change the Controller to use EF (MyDbContext)

```cs
private readonly MyDbContext _dbContext;

public WeatherForecastController(MyDbContext context)
{
    _dbContext = context;
}

[HttpGet]
public IEnumerable<WeatherForecast> Get()
{
    return _dbContext.WeatherForecasts.ToArray();
}
```

- Create the database `MyAngular13TestDB` and add a table:

```sql
CREATE TABLE [dbo].[WeatherForecasts](
	[Date] [date] NOT NULL,
	[TemperatureC] [int] NOT NULL,
	[TemperatureF] [int] NOT NULL,
	[Summary] [nvarchar](50) NULL
)
GO
```

- Add some records into the table `MyAngular13TestDB.dbo.WeatherForecasts`
- Run the app and see the created records in web page (header item `Fetch Data`)
