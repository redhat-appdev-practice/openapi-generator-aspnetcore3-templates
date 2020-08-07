# Custom OpenAPI Generator Templates For ASP.NET Core 3.x

## Overview
The default templates in OpenAPI Generator for ASP.NET Core produce API Controllers which are not type-safe:

```csharp
        /// <summary>
        /// Find an Employee resource by ID
        /// </summary>
        /// <remarks>Returns a single employee matching the given ID.</remarks>
        /// <param name="employeeId">Kerberos ID of the employee.</param>
        /// <response code="200">A representation of the employee matching the given employeeId.</response>
        /// <response code="404">An employee matching the given employeeId was not found.</response>
        [HttpGet]
        [Route("/employee/{employeeId}")]
        [ValidateModelState]
        [SwaggerOperation("GetEmployeeById")]
        [SwaggerResponse(statusCode: 200, type: typeof(Employee), description: "A representation of the employee matching the given employeeId.")]
        public abstract IActionResult GetEmployeeById([FromRoute][Required]string employeeId);
```

This set of templates changes that behaviour such that they **ARE** type-safe using the return type of the 2XX response.

```csharp
        /// <summary>
        /// Find an Employee resource by ID
        /// </summary>
        /// <remarks>Returns a single employee matching the given ID.</remarks>
        /// <param name="employeeId">Kerberos ID of the employee.</param>
        /// <response code="200">A representation of the employee matching the given employeeId.</response>
        /// <response code="404">An employee matching the given employeeId was not found.</response>
        [HttpGet]
        [Route("/employee/{employeeId}")]
        [ValidateModelState]
        [SwaggerOperation("GetEmployeeById")]
        [SwaggerResponse(statusCode: 200, type: typeof(Employee), description: "A representation of the employee matching the given employeeId.")]
        public abstract ActionResult<Employee> GetEmployeeById([FromRoute][Required]string employeeId);
```

## How To Use These Templates
1. Install [OpenAPI Generator](https://openapi-generator.tech/docs/installation)
1. Run the generator and set the template override to point to a cloned copy of this repository
   ```bash
   openapi-generator generate -g aspnetcore -t /path/to/template/directory ....
   ```