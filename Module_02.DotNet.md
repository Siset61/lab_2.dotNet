# Module 02 - Documentation with GitHub Copilot - Hands-On Lab

## Overview

In this lab, you will use GitHub Copilot's documentation features to generate, improve, and maintain professional documentation for the Claims Management ASP.NET Core API. You'll master Chat modes (Ask, Edit, Agent, Plan), Smart Actions, Custom Instructions, chat participants, and autonomous documentation workflows.

**What You'll Learn:**
- Use Smart Actions and Chat modes to understand and document existing code
- Generate comprehensive XML documentation comments with consistent formatting
- Establish and enforce repository-wide documentation standards
- Create specialized documentation workflows with custom chat modes
- Automate complete documentation suites using Agent Mode

**What You'll Build:**
- Complete XML documentation comments across the Claims API codebase
- Repository documentation standards (`.github/copilot-instructions.md`)
- Custom documentation specialist chat mode
- Comprehensive documentation suite (API.md, ARCHITECTURE.md, CONTRIBUTING.md)

## Lab Learning Path

1. **Introductory (30 min)**: Set up Copilot Chat modes, use Smart Actions to understand existing code, and generate initial XML documentation comments with consistent formatting
2. **Intermediate (30 min)**: Establish repository-wide documentation standards with Custom Instructions, generate comprehensive API documentation, and apply standards across multiple files
3. **Advanced (30 min)**: Tune instruction priority (personal vs. repository), create specialized documentation workflows with custom chat modes, and automate complete documentation suites using Agent Mode

## Prerequisites

> **📋 See [Module_02.Requirements.DotNet.md](Requirements.md) for detailed setup instructions.**

## Repository Structure

The repository contains **only one exercise folder** so, all participans should follow the exercises without problem.

I will be passing each ejercise after complete every one if any participants need to star fron that point.


# Introductory Level

## Exercise 1: Explore Copilot Chat Modes and Analyze Existing Code

### Prerequisites

- VS Code with GitHub Copilot extension enabled
- **Project opened in DevContainer** (see Prerequisites section)
- Claims ASP.NET Core project loaded in VS Code

### Objective

Understand the four Copilot Chat modes (Ask, Edit, Agent, Plan) and use Smart Actions to analyze existing code in the Claims API. Learn when to use each mode for documentation tasks and how they differ in functionality.

### Description

You'll explore Copilot's chat interface, verify access to all four modes, and use the "Explain" Smart Action to understand the existing `ClaimsController.cs` before documenting it. This exercise introduces non-destructive code analysis techniques that form the foundation for effective documentation.

**Key Concepts:**
- **Ask Mode**: Question-and-answer mode for understanding code (non-destructive)
- **Edit Mode**: Interactive code modification with preview and approval
- **Agent Mode**: Autonomous multi-file operations for complex tasks
- **Plan Mode**: Task planning and decomposition for structured work
- **Smart Actions**: Context-aware shortcuts accessed via right-click context menu

### Steps

1. **Open Project and Verify Copilot Chat Modes**
   - Ensure you have the `GENERALI.Module_02_ClaimsAPI.DotNet` project open in VS Code
   - Open the Copilot Chat panel:
     - Click the Copilot icon in the left sidebar, OR
     - Use keyboard shortcut: `Ctrl/Cmd + Shift + I`
   - Locate the **mode selector** at the bottom of the chat panel
   - Verify you can see four mode buttons/tabs:
     - **Ask**
     - **Edit**
     - **Agent**
     - **Plan**
   - Expected behavior:
     - Clicking each mode changes the chat interface
     - Ask mode is usually selected by default

2. **Use Smart Actions to Analyze Code**
   - Open the file: `src/ClaimsApi/Controllers/ClaimsController.cs`
   - Scroll to the `CreateClaim` method
   - Select the **entire method** including the attributes (`[HttpPost]`, `[Authorize]`)
   - Right-click on the selection
   - Choose **Copilot** -> **Explain** from the context menu
   - Observe:
     - Explanation appears automatically in the Chat panel
     - Chat switches to Ask mode (if not already)
     - Explanation is context-aware (knows it's an ASP.NET Core controller action)
     - Smart Action is **non-destructive** (no code changes)

3. **Ask Follow-up Questions Using Ask Mode**
   - With the explanation visible in Chat, ensure you're in **Ask mode**
   - Type this follow-up question in the chat input:
     ```text
     What security measures does this endpoint implement and why are they important for a claims management system?
     ```
   - Press Enter and review the response
   - Observe how Copilot:
     - References the code context from the previous explanation
     - Mentions authorization requirements (`[Authorize(Roles = "Adjuster,Admin")]`)
     - Explains role-based access control (Adjuster/Admin)

4. **Compare Single-File vs. Project-Wide Context**
   - In Ask mode, try a single-file question:
     ```text
     What are the main responsibilities of the ClaimsController?
     ```
   - Now try using the `@workspace` participant for broader context:
     ```text
     @workspace Summarize all authentication requirements across the controllers in this project. Which endpoints require authentication and what roles are needed?
     ```
   - Observe the difference:
     - First question focuses only on `ClaimsController.cs`
     - `@workspace` analyzes multiple files (`ClaimsController.cs`, `ReportsController.cs`, `AuthController.cs`, `HealthController.cs`)
     - Provides a comprehensive project-wide summary

5. **Explore Other Smart Actions (Optional)**
   - Select a different method (e.g., `UpdateClaim`)
   - Right-click and explore other Smart Actions:
     - **Fix** (suggests improvements)
     - **Generate Docs** (creates XML documentation comments)
     - **Generate Tests** (creates test cases)
     - **Run the Tests** and fix the problems that may arise using the Agent Mode:

     ```
     Execute the tests and fix the problems that may arise. Don't change the code, just adjust the tests.
     ```

### Success Criteria

- Copilot Chat panel displays Ask, Edit, Agent, and Plan mode selectors clearly
- Smart Action "Explain" successfully generates a context-aware explanation
- Follow-up questions in Ask mode receive relevant, code-aware responses
- `@workspace` participant provides broader project context than single-file queries
- You understand when to use each chat mode (Ask for Q&A, Edit for changes, Agent for multi-file tasks, Plan for structured work)

### Verification Steps

**Quick Test:**
1. Click through all four chat modes - each should show different UI elements
2. Smart Action "Explain" should open results in Chat panel automatically
3. Ask mode responses should reference your specific code
4. `@workspace` responses should mention multiple files from the project

### Connection to Next Exercise

Next, you'll use Edit mode to generate comprehensive XML documentation comments for undocumented methods, applying what you learned about code analysis. The understanding gained from Ask mode and Smart Actions will help you write better documentation prompts.

### Estimated Time

12 minutes

> **Instructor Note:**
> **Common Issues:**
> - If students don't see all four modes, verify they have Business/Enterprise Copilot access (Individual plan only has Ask mode)
> - Smart Actions menu may vary by VS Code version - ensure Copilot extension is up to date
> - If `@workspace` doesn't work, ensure the entire project folder is open in VS Code (not just a single file)
>
> **Key Teaching Points:**
> - Emphasize that Ask is non-destructive (safe to experiment)
> - Edit mode shows preview before applying changes
> - Agent mode requires more supervision due to autonomous nature
> - Smart Actions save time by providing instant context

---

## Exercise 2: Generate XML Documentation Comments with Edit Mode and Smart Actions

### Prerequisites

- Completion of Exercise 1
- File open: `src/ClaimsApi/Controllers/ClaimsController.cs`
- Understanding of Copilot Chat modes from Exercise 1

### Objective

Use Edit mode to generate comprehensive XML documentation comments for all methods in `ClaimsController.cs`. Learn to provide clear instructions, review proposed changes, and verify documentation quality before accepting.

### Description

The `ClaimsController.cs` currently has minimal documentation. You'll use Edit mode to add comprehensive XML documentation comments with parameter descriptions, return types, response codes, and usage examples. This demonstrates the difference between Ask mode (questions) and Edit mode (code changes).

**XML Documentation Comment Structure:**
```csharp
/// <summary>
/// Brief one-line description.
/// </summary>
/// <param name="paramName">Parameter description.</param>
/// <returns>Return value description.</returns>
/// <response code="200">Success response description.</response>
/// <response code="404">Not found response description.</response>
/// <exception cref="InvalidOperationException">When this exception occurs.</exception>
/// <example>
/// <code>
/// // Usage example
/// var result = await controller.Method(param);
/// </code>
/// </example>
/// <remarks>
/// Additional implementation details or notes.
/// </remarks>
```

### Steps

1. **Inspect Current Documentation State**
   - Open `src/ClaimsApi/Controllers/ClaimsController.cs` if not already open
   - Review existing documentation:
     - The `UpdateStatus` method has some XML documentation comments
     - Other methods like `CreateClaim` and `GetClaim` lack proper documentation
   - Note the use of `[ProducesResponseType]` attributes for OpenAPI/Swagger

2. **Switch to Edit Mode and Generate Documentation**
   - Click the **Edit** tab/button in Copilot Chat panel (at the bottom of the panel)
   - Ensure `src/ClaimsApi/Controllers/ClaimsController.cs` is the active file in VS Code
   - In the Edit mode prompt box, enter this comprehensive prompt:
     ```text
     Add comprehensive XML documentation comments to all public methods in this file.

     For each method, include:
     - <summary> with a brief description of what the method does (imperative mood)
     - <param> for each parameter with type and description
     - <returns> with return type and description
     - <response> for each HTTP status code (200, 201, 400, 401, 404)
     - <remarks> for authentication requirements and business rules
     - <example> section for main CRUD operations showing curl request

     Use this format:
     /// <summary>
     /// Create a new insurance claim.
     /// </summary>
     /// <param name="createDto">The claim creation data containing policy details.</param>
     /// <returns>The created claim with generated ID.</returns>
     /// <response code="201">Returns the newly created claim.</response>
     /// <response code="400">If the request data is invalid.</response>
     /// <response code="401">If the user is not authenticated.</response>
     /// <example>
     /// <code>
     /// curl -X POST "http://localhost:8080/api/v1/claims" \
     ///   -H "Authorization: Bearer TOKEN" \
     ///   -H "Content-Type: application/json" \
     ///   -d '{"policyNumber": "POL-2025-001", ...}'
     /// </code>
     /// </example>
     ```
   - Press Enter to execute

3. **Review Proposed Changes Carefully**
   - Edit mode will show a **diff preview** (before/after comparison)
   - Scroll through all proposed changes
   - For the `CreateClaim` method, verify the new documentation includes:
     - **summary**: Brief description of creating a claim
     - **param createDto**: Description of ClaimCreateDto parameter
     - **returns**: ClaimReadDto description
     - **response 201**: Created successfully
     - **response 400**: Validation errors
     - **response 401**: Not authenticated
     - **example**: Working curl command with realistic data
   - Check other methods (`GetClaim`, `UpdateStatus`) for similar completeness

4. **Apply Changes and Verify**
   - If the documentation looks correct, click **Accept** button
   - If you see issues (incorrect types, missing information), click **Reject** and refine your prompt
   - After accepting, save the file (`Ctrl/Cmd + S`)
   - Verify changes were applied:
     - Scroll through the file manually
     - All methods should now have complete XML documentation
     - No syntax errors should be introduced

5. **Test Documentation with IntelliSense**
   - Hover your mouse over the method name `CreateClaim` in VS Code
   - IntelliSense tooltip should display the **complete documentation** with all sections
   - Test with other methods:
     - Hover over `GetClaim` -> should show full documentation
     - Hover over `UpdateClaim` -> should show parameters and responses
   - This confirms the XML documentation is properly formatted and accessible

### Success Criteria

- All methods in `ClaimsController.cs` have complete XML documentation comments
- Documentation includes complete summary, param, returns, and response sections
- Main endpoint methods (`CreateClaim`, `UpdateStatus`) have example sections
- IntelliSense displays complete documentation when hovering over methods
- No syntax errors introduced by the documentation additions
- File saved and changes ready to commit

### Verification Steps

**Quick Validation:**
- Open VS Code Problems panel (View -> Problems)
- Verify no C# syntax errors are shown for `ClaimsController.cs`
- Open `ClaimsController.cs` and visually inspect:
  - All methods should have multi-line XML documentation (not single line)
  - Documentation should include sections like `<summary>`, `<param>`, `<returns>`, `<response>`

**Manual Checks:**
1. Open `ClaimsController.cs` and scroll to any method
2. Each should have multi-line XML documentation (/// comments)
3. Hover over method name -> tooltip shows summary/params/returns

### Connection to Next Exercise

Next, you'll establish repository-wide documentation standards using Custom Instructions. This will ensure all future documentation follows consistent formatting without repeating instructions in every prompt.

### Estimated Time

10 minutes

> **Instructor Note:**
> **Common Issues:**
> - **Edit mode suggests wrong types**: Students can reject and refine prompt with more specific type information
> - **Documentation too verbose**: Add "be concise" to prompt
> - **Missing examples**: Emphasize "Example section for main endpoints only"
>
> **Key Teaching Points:**
> - Always review diff before accepting (Edit mode safety)
> - Edit mode is for code changes, Ask mode is for questions
> - IntelliSense is the best way to verify XML documentation works
> - Documentation should help developers, not just satisfy requirements
>
> **Best Practices:**
> - Reject and refine if output isn't perfect
> - Use specific language ("XML documentation", "include response codes")
> - Verify no regressions (syntax errors, broken imports)

---

# Intermediate Level

## Exercise 3: Establish Documentation Standards with Repository Custom Instructions

### Prerequisites

- Completion of Exercises 1-2
- Files: `src/ClaimsApi/Controllers/ClaimsController.cs` (with complete documentation from Exercise 2)
- Understanding of Copilot Chat modes and XML documentation generation

### Objective

Create `.github/copilot-instructions.md` to define repository-wide documentation standards that Copilot will automatically apply to all interactions. Learn how Custom Instructions eliminate the need to repeat standards in every prompt.

### Description

Repository Custom Instructions are automatically used by Copilot for all chat responses, code review, and the coding agent. By defining documentation standards in `.github/copilot-instructions.md`, you ensure consistency across the entire codebase without manual repetition.

**What Custom Instructions Do:**
- Automatically applied to all Copilot interactions in this repository
- Used by Chat (Ask/Edit/Agent modes), Code Review, and Pull Request Summaries
- Override default Copilot behavior with your project-specific standards
- Centralize "project knowledge" that Copilot should always know

**Instruction Hierarchy (highest to lowest priority):**
1. **Personal Instructions** (`*.instructions.md` in VS Code User data)
2. **Repository Instructions** (`.github/copilot-instructions.md`)
3. **Organization Instructions** (org-level settings)

### Steps

1. **Verify `.github` Folder Exists**
   - In VS Code Explorer, check if `.github/` folder exists in the project root
   - If it doesn't exist:
     - Right-click in Explorer -> New Folder
     - Name it `.github`
   - This folder will contain repository-level configuration files

2. **Create the Custom Instructions File**
   - Switch to **Edit mode** in Copilot Chat
   - Provide this prompt to create the file with comprehensive documentation standards:
     ```text
     Create a new file at .github/copilot-instructions.md with comprehensive documentation standards for this Claims Management ASP.NET Core API project.

     The file should include:

     # Claims Management API - GitHub Copilot Instructions

     ## Project Overview
     This is an insurance claims management REST API built with ASP.NET Core 8, Entity Framework Core, and SQLite. The system handles claim creation, status workflows, file attachments, and role-based authentication (JWT) for adjusters and administrators.

     ## Documentation Standards

     ### XML Documentation Style
     - **Format**: XML documentation comments (///) for all public classes, methods, and properties
     - **Required Elements**:
       - `<summary>`: Brief description (first line, imperative mood)
       - `<param>`: All parameters with type and description
       - `<returns>`: Return type and description
       - `<response>`: HTTP status codes for controller actions
       - `<exception>`: All exceptions that can be thrown
       - `<example>`: Usage example (required for public API endpoints)
     - **Type References**: Use `<see cref="TypeName"/>` for type references
     - **Completeness**: Document all parameters, even those with obvious names

     ### Method Documentation Requirements
     - **Public Controllers/Endpoints**: Must have complete XML documentation with all sections
     - **Service Methods**: Must document exceptions even if unlikely
     - **Helper Methods**: Brief description acceptable if logic is self-explanatory
     - **Private Methods**: Single-line summary minimum
     - **API Endpoints**: Must include `<example>` section with curl request using realistic data

     ### Documentation Tone and Style
     - **Voice**: Imperative mood ("Create a claim", not "Creates a claim")
     - **Clarity**: Clear, concise, developer-focused
     - **Terminology**: Use domain terms consistently (adjuster = insurance claims processor)
     - **Examples**: Always use realistic data (actual policy numbers like POL-2025-001, real dates, meaningful amounts)
     - **Brevity**: Avoid unnecessary verbosity; be direct and practical
     - **Audience**: Assume technical audience familiar with ASP.NET Core and REST APIs

     ### Class-Level Documentation
     - **Required**: Every public class must have XML documentation
     - **Location**: Above the class declaration
     - **Content**: Brief description of the class's role in the application (1-3 sentences)
     - **Example**:

         ```csharp
         /// <summary>
         /// Provides CRUD endpoints for insurance claim management.
         /// Handles claim creation, retrieval, updates, and status transitions
         /// with role-based access control for adjusters and administrators.
         /// </summary>
         [ApiController]
         [Route("api/v1/[controller]")]
         public class ClaimsController : ControllerBase
         ```

     ### API Documentation Files (docs/)
     - **Required Sections**: Overview, Authentication, Endpoints (grouped by resource), Error Handling, Examples
     - **Endpoint Documentation**: Method, URL, Auth requirements, Request schema, Response schema, Error codes
     - **Code Examples**: Working examples that can be copy-pasted (curl and HttpClient)
     - **Status Codes**: Document all possible HTTP status codes with scenarios
     - **Keep Updated**: When code changes, update documentation in the same commit

     ### README Requirements
     - **Mandatory Sections**: Overview, Features, Getting Started, API Documentation, Architecture, Testing, Deployment
     - **Code Examples**: Always provide working examples that can be executed
     - **Prerequisites**: List all requirements with version numbers (.NET 8+)
     - **Status Badges**: Include test coverage, build status when available
     - **Changelog**: Maintain version history for significant changes

     ### Cross-References and Consistency
     - **Link Related Docs**: Use relative links between documentation files
     - **Consistent Terminology**: Use same terms across all documentation (e.g., always "claim" not "request")
     - **Version References**: When mentioning endpoints, include full path (e.g., POST /api/v1/claims)
     - **Update Together**: When changing code, update related XML docs and docs/ files in same commit

     ## Architecture Principles

     ### Layered Architecture
     - **Controllers** (Controllers/): Handle HTTP requests/responses, input validation, authorization
     - **Services** (Services/): Business logic, orchestration, validation
     - **DTOs** (DTOs/): Data transfer objects for request/response validation
     - **Models** (Models/): Entity Framework Core database models
     - **Data** (Data/): DbContext and database configuration

     ### Critical Design Principles
     - **DTO/Model Mapping**: DTO and model properties should map cleanly
     - **Dependency Injection**: Use ASP.NET Core's built-in DI for services
     - **Separation of Concerns**: Keep business logic in services, HTTP handling in controllers

     ## Coding Standards

     ### C# Style
     - Use C# 12+ features where appropriate
     - Follow Microsoft .NET naming conventions
     - Use nullable reference types (enable `<Nullable>enable</Nullable>`)
     - Maximum line length: 120 characters

     ### ASP.NET Core Patterns
     - Use record types for DTOs where appropriate
     - Controller actions must have OpenAPI documentation via attributes
     - Use appropriate HTTP status codes (201 for creation, 204 for deletion)
     - Apply `[Authorize]` attributes where required

     ### Error Handling
     - Return appropriate `ActionResult<T>` types
     - Include descriptive error messages in problem details
     - Log exceptions with claim ID context when available
     - Document all possible exceptions in XML documentation

     ## Testing Standards
     - Write xUnit tests for all controllers and services
     - Include both happy path and error scenarios
     - Use WebApplicationFactory for integration tests
     - Aim for >80% code coverage

     ## Security Standards
     - All endpoints requiring authentication must use JWT Bearer tokens
     - Implement role-based access control (Adjuster vs. Admin)
     - Validate and sanitize all file uploads
     - Never log sensitive information (passwords, tokens)
     ```
   - Press Enter and review the proposed file creation in Edit mode

3. **Review and Accept the File Creation**
   - Carefully review the generated `.github/copilot-instructions.md` file
   - Verify all major sections are present:
     - Project Overview
     - Documentation Standards (comprehensive)
     - Architecture Principles
     - Coding Standards
     - Testing Standards
     - Security Standards
   - If everything looks correct, click **Accept**
   - If anything needs adjustment, click **Reject** and refine the prompt

4. **Verify Copilot Recognizes the New Standards**
   - Open `src/ClaimsApi/Controllers/ClaimsController.cs` (has some documentation)
   - Switch to **Ask mode** in Copilot Chat
   - Ask this verification question:
     ```text
     Review the XML documentation in src/ClaimsApi/Controllers/ClaimsController.cs against our repository documentation standards. List any gaps or non-compliant elements.
     ```
   - Copilot should:
     - Reference standards from `.github/copilot-instructions.md` automatically
     - Identify missing sections (e.g., missing examples, incomplete response codes)
     - Suggest specific improvements based on the standards
   - This confirms Copilot is loading and applying your custom instructions

5. **Test Automatic Application**
   - Switch to **Edit mode** still using `src/ClaimsApi/Controllers/ClaimsController.cs`
   - Give a simple prompt without mentioning standards:
     ```text
     Add documentation to all methods in this file.
     ```
   - Observe that Copilot applies XML documentation format automatically
   - This demonstrates that standards are now "always on" for this repository

### Success Criteria

- `.github/copilot-instructions.md` contains comprehensive "Documentation Standards" section
- Section includes specific rules for XML docs, tone, class docs, API docs, and README
- File is saved and committed to Git with descriptive message
- Copilot automatically references these standards when asked about documentation compliance
- Standards are clear, specific, and actionable (not vague or generic)

### Verification Steps

**Immediate Verification:**
- Open VS Code Source Control panel
- Verify `.github/copilot-instructions.md` appears in changes
- Check the file contains the new "Documentation Standards" section:
  - Open the file and scroll through
  - Look for `## Documentation Standards` heading

**Functional Test:**
- Ask Copilot: `@workspace What are our XML documentation requirements?`
- Response should reference `.github/copilot-instructions.md` and list XML documentation format rules

### Connection to Next Exercise

Next, you'll apply these standards systematically across multiple controller files using Edit mode and `@workspace`. The Custom Instructions will ensure consistency without repetitive prompting.

### Estimated Time

15 minutes

> **Instructor Note:**
> **Common Issues:**
> - **Copilot not referencing standards**: Ensure file is saved and properly formatted (markdown syntax)
> - **Standards too generic**: Encourage specific, actionable rules (not "write good docs")
> - **File location wrong**: Must be `.github/copilot-instructions.md` exactly (case-sensitive)
>
> **Key Teaching Points:**
> - Custom Instructions are automatic - no need to mention them in prompts
> - They work across all Copilot features (Chat, Code Review, PR Summary)
> - Repository instructions are project-specific, personal are user-specific
> - More specific standards = better Copilot output
>
> **Best Practices:**
> - Include examples in standards (e.g., example XML documentation format)
> - Reference existing files when possible ("like ClaimsController.cs")
> - Keep standards updated as project evolves
> - Make standards specific and testable

---

## Exercise 4: Apply Standards Across Multiple Files with Workspace Context

### Prerequisites

- Completion of Exercises 1-3
- Files: `.github/copilot-instructions.md` (with documentation standards)
- Understanding of Repository Custom Instructions

### Objective

Use Edit mode and `@workspace` participant to systematically apply documentation standards across all controller files (`ClaimsController.cs`, `AuthController.cs`, `HealthController.cs`, `ReportsController.cs`). Learn efficient multi-file documentation workflows and how to verify consistency project-wide.

### Description

Rather than documenting each file manually one-by-one, you'll use Copilot's project-wide context via `@workspace` to identify all files needing documentation updates, then apply standards efficiently. This demonstrates how Custom Instructions scale across a codebase and how to maintain consistency.

**Files to Document:**
- `src/ClaimsApi/Controllers/ReportsController.cs` - File upload endpoints
- `src/ClaimsApi/Controllers/AuthController.cs` - Authentication and token generation
- `src/ClaimsApi/Controllers/HealthController.cs` - Health check endpoint
- `src/ClaimsApi/Services/ClaimsService.cs` - Business logic layer

### Steps

1. **Audit Current Documentation Coverage**
   - Switch to **Ask mode** in Copilot Chat
   - Use `@workspace` to get a project-wide documentation audit:
     ```text
     @workspace Analyze all controller files under src/ClaimsApi/Controllers/ and create a summary table showing:
     1. Filename
     2. Whether XML documentation is complete according to our documentation standards
     3. Specific missing elements (summary, params, returns, response codes, examples)
     4. Priority level (High/Medium/Low) based on method complexity
     ```
   - Expected response format (example):

     | File | Complete | Missing Elements | Priority |
     |------|----------|------------------|----------|
     | ClaimsController.cs | Yes | None | - |
     | ReportsController.cs | Partial | Examples in UploadAttachment | High |
     | AuthController.cs | No | All sections, Examples | Medium |
     | HealthController.cs | No | Returns, Examples | Low |

   - Review the audit to plan your work order (start with High priority)

2. **Document AuthController.cs (Authentication Controller)**
   - Open `src/ClaimsApi/Controllers/AuthController.cs`
   - This file handles JWT token generation
   - Switch to **Edit mode**
   - Provide this prompt emphasizing examples:
     ```text
     Add complete XML documentation to all methods in this file following repository documentation standards.

     For the token endpoint:
     - Document JWT Bearer token flow
     - Explain token response structure (access_token, expiration)
     - Include two examples: one with curl, one with HttpClient
     - Document possible errors (401 for invalid credentials)

     Example curl:
     curl -X POST "http://localhost:8080/api/auth/token" \
       -H "Content-Type: application/json" \
       -d '{"username":"adjuster","password":"adjuster"}'

     Example C#:
     var client = new HttpClient();
     var response = await client.PostAsJsonAsync(
         "http://localhost:8080/api/auth/token",
         new { username = "adjuster", password = "adjuster" }
     );
     var token = await response.Content.ReadFromJsonAsync<TokenResponseDto>();
     ```
   - Review and accept if correct

4. **Document HealthController.cs (Health Check Controller)**
   - Open `src/ClaimsApi/Controllers/HealthController.cs`
   - This is a simple endpoint but still needs proper documentation
   - Switch to **Edit mode**
   - Provide this concise prompt:
     ```text
     Add complete XML documentation to all methods in this file following repository documentation standards.

     For health check endpoint:
     - Add class-level documentation explaining health check purpose (monitoring, liveness probes, Kubernetes)
     - Document response format (status, version fields)
     - Include example showing typical usage for monitoring tools
     ```
   - Review and accept

5. **Document ClaimService.cs (Service Layer)**
   - Open `src/ClaimsApi/Services/ClaimService.cs`
   - This file contains the business logic
   - Switch to **Edit mode**
   - Provide this prompt:
     ```text
     Add complete XML documentation to all public methods in this file following repository documentation standards.

     For service methods:
     - Document business logic and validation rules
     - Include exception documentation for cases like claim not found
     - Document status workflow transitions (submitted -> under_review -> approved/rejected)
     - Note that approved/rejected claims are terminal states
     ```
   - Review and accept

6. **Verify Consistency Across All Files**
   - Switch to **Ask mode**
   - Run a comprehensive consistency check:
     ```text
     @workspace Verify that all controller files (ClaimsController.cs, AttachmentsController.cs, AuthController.cs, HealthController.cs) now have complete XML documentation following our documentation standards.

     For each file, confirm:
     1. All public methods have XML documentation
     2. Public endpoints have example sections
     3. Summary/params/returns/response sections are present and complete
     4. Terminology is consistent across files

     Summarize any remaining gaps or inconsistencies.
     ```
   - Review the response
   - If gaps remain, use Edit mode to fix specific issues
   - Copilot should confirm substantial compliance

7. **Cross-Check Example Quality (Important)**
   - Open each controller file and manually verify one example section
   - Check that examples:
     - Use realistic data (POL-2025-001, not POL-123)
     - Include authentication where required
     - Show complete curl command with headers
     - Use proper JSON formatting in request bodies
   - Fix any unrealistic or broken examples using Edit mode

### Success Criteria

- All controller files (`ClaimsController.cs`, `ReportsController.cs`, `AuthController.cs`, `HealthController.cs`) have complete XML documentation
- Each endpoint with authentication includes realistic example usage
- XML documentation follows consistent format across all files
- Class-level documentation added where previously missing
- `@workspace` verification confirms no major gaps remain

### Verification Steps

**Code Quality Check:**
- Open VS Code Problems panel (View -> Problems)
- Verify no syntax errors are shown for controller files
- Open several controller files and spot-check documentation visually

**Manual Spot Checks:**
1. Open any controller file and pick a random method
2. Hover over the method name -> tooltip shows complete documentation
3. Check that example sections use realistic data
4. Verify no "TODO" or placeholder text remains

### Connection to Next Exercise

Next, you'll create a custom chat mode specialized for documentation tasks. This will streamline future documentation work by providing a persistent, domain-aware documentation assistant.

### Estimated Time

15 minutes

> **Instructor Note:**
> **Common Issues:**
> - **Inconsistent quality across files**: Re-run Edit mode with more specific prompts
> - **Examples use fake data**: Emphasize "realistic data" in prompts (POL-2025-001, not POL-123)
> - **Missing cross-references**: Ask Copilot to add links between related endpoints
>
> **Key Teaching Points:**
> - Custom Instructions eliminate repetitive prompting (notice we never re-specify XML format)
> - `@workspace` provides project-wide view for audits and verification
> - Each file can have file-specific instructions while maintaining overall consistency
> - Documentation is code - commit it, review it, maintain it
>
> **Time Management:**
> - If running short on time, focus on AttachmentsController.cs and AuthController.cs (most complex)
> - HealthController.cs can be documented quickly (simpler)
> - Verification step is critical - don't skip
>
> **Quality Assurance:**
> - Always review at least one example section manually
> - Check that response sections list actual HTTP status codes from code
> - Verify param types match actual method signatures

---

# Advanced Level

## Exercise 5: Create Custom Chat Mode for Documentation Workflows

### Prerequisites

- Completion of Exercises 1-4
- Files: `.github/copilot-instructions.md` (with documentation standards)
- All controller files with complete XML documentation
- Understanding: Copilot Chat modes, Custom Instructions, @workspace participant

### Objective

Create a specialized custom chat mode (`docs-specialist.agents.md`) that provides persistent, domain-aware documentation assistance. Learn instruction precedence (Repository > Organization) and how custom chat modes optimize recurring workflows.

### Description

Custom chat modes enable specialized AI assistants tailored for specific tasks. You'll create a "Documentation Specialist" mode that:
- Maintains persistent context about the Claims API domain
- Automatically enforces documentation standards
- Proactively identifies documentation gaps
- Provides consistent documentation guidance across conversations

**What Makes Custom Chat Modes Powerful:**
- **Persistent behavior**: Mode remembers its role across conversations
- **Domain knowledge**: Can encode project-specific terminology and patterns
- **Specialized tools**: Can be configured to prioritize certain Copilot features
- **Context maintenance**: Keeps documentation context active across multiple files

**Instruction Precedence Hierarchy:**
```
Personal Instructions (*.instructions.md in VS Code User data)
    | Highest Priority
Repository Instructions (.github/copilot-instructions.md)
    | Medium Priority
Organization Instructions (GitHub org settings)
    | Lowest Priority
Custom Chat Mode (.chatmode.md)
    | Adds specialized behavior on top
```

### Steps

1. **Verify Chat Mode Directory Exists**
   - In VS Code Explorer, check if `.github/chatmodes/` folder exists
   - If not, right-click `.github/` -> New Folder -> name it `chatmodes`

2. **Create Documentation Specialist Chat Mode**
   - Switch to **Edit mode** in Copilot Chat
   - Provide this prompt to create the chat mode:
     ```text
     Create a new file at .github/agents/docs-specialist.agent.md with this content:

     ---
     description: "Documentation Specialist for Claims Management API - Enforces documentation standards and provides expert documentation guidance"
     tools:
       - codebase
       - search
     ---

     # Documentation Specialist Chat Mode

     ## Purpose
     Act as a Documentation Specialist for the Claims Management ASP.NET Core API. Focus on maintaining high-quality, consistent documentation that follows repository standards and serves both internal developers and external API consumers.

     ## Persona Definition
     - You are an experienced technical writer specializing in API documentation
     - You understand ASP.NET Core, REST principles, Entity Framework Core, and C# documentation best practices
     - You prioritize clarity, completeness, accuracy, and developer experience
     - You proactively identify documentation gaps, inconsistencies, and improvement opportunities

     ## Domain Knowledge (Claims Management API)

     ### Core Business Entities
     - **Claims**: Insurance claims with policy numbers, incident dates, descriptions, amounts, status workflows
     - **Attachments**: Supporting documents (PDFs, images) linked to claims with secure storage
     - **Users**: Authenticated users with roles (Adjuster can create/modify claims, Admin has full access)

     ### Key Technical Concepts
     - **Status Workflow**: submitted -> under_review -> (approved OR rejected) with read-only terminal states
     - **Authentication**: JWT Bearer tokens with role-based access control
     - **Architecture**: Layered (Controllers -> Services -> DTOs -> Models -> DbContext)
     - **DTO/Model Mapping**: DTOs and models should have clean property mapping

     ### Documentation Standards Reference
     - **Documentation Style**: XML documentation comments (///) with summary, param, returns, response, example sections
     - **Tone**: Imperative mood, developer-focused, clear and concise
     - **Examples**: Realistic data (POL-2025-001), working code, proper authentication
     - **Full Standards**: See `.github/copilot-instructions.md` Documentation Standards section

     ## Responsibilities

     ### 1. Generate Documentation
     - **XML Docs**: Create/update XML documentation comments with all required sections
     - **API Reference**: Generate comprehensive endpoint documentation with request/response schemas
     - **Architecture Docs**: Explain system design, data flow, design decisions
     - **User Guides**: Write getting started guides, tutorials, usage examples
     - **Code Comments**: Add inline comments for complex business logic

     ### 2. Enforce Standards (Automatically)
     - Always reference `.github/copilot-instructions.md` documentation standards
     - Verify documentation includes summary, param, returns, response sections (when required)
     - Ensure imperative mood ("Create a claim" not "Creates a claim")
     - Use realistic examples with actual policy numbers and dates
     - Check cross-references between documentation and API documentation files

     ### 3. Maintain Consistency
     - Verify terminology is consistent across all documentation (e.g., always "claim" not "request")
     - Check endpoint descriptions match between controllers and docs/API.md
     - Ensure error codes and messages are documented consistently
     - Validate that code examples are up-to-date with current implementation

     ### 4. Proactive Quality Assurance
     - When asked to document a method, automatically check related methods for completeness
     - Identify missing documentation across @workspace without being asked
     - Suggest improvements to existing documentation (clarity, completeness, accuracy)
     - Flag outdated examples, broken cross-references, or deprecated information
     - Recommend documentation updates when code changes are detected

     ### 5. Domain-Specific Guidance
     - Explain insurance domain terms (adjuster, policy, claim status) in documentation
     - Clarify technical terms (JWT, EF Core, DI) for different audiences
     - Provide context about status workflows and business rules in documentation
     - Highlight security considerations (authentication, authorization, file upload safety)

     ## Output Format Specifications

     ### For XML Documentation
         ```csharp
         /// <summary>
         /// Brief description in imperative mood.
         /// </summary>
         /// <param name="paramName">Clear parameter description.</param>
         /// <returns>Description of what is returned.</returns>
         /// <response code="200">Success response description.</response>
         /// <response code="401">Unauthorized - user not authenticated.</response>
         /// <exception cref="InvalidOperationException">Condition that causes this exception.</exception>
         /// <example>
         /// <code>
         /// curl -X POST "http://localhost:8080/api/v1/endpoint" \
         ///   -H "Authorization: Bearer TOKEN" \
         ///   -d '{"field": "value"}'
         /// </code>
         /// </example>
         ```

     ### For API Documentation (Markdown)
     - Endpoint header: `### POST /api/v1/claims`
     - Authentication requirements
     - Request schema (JSON example)
     - Response schema (JSON example)
     - Error codes with explanations
     - Working code examples (curl and C# HttpClient)

     ### For Architecture Documentation
     - ASCII diagrams for request flow
     - Component descriptions (purpose, responsibilities, dependencies)
     - Design decision explanations (why chosen, alternatives considered)
     - Data flow diagrams (how information moves through the system)

     ## Interaction Guidelines

     ### Tone and Style
     - **Professional but approachable**: Technical but not intimidating
     - **Developer-focused**: Assume technical audience familiar with web APIs
     - **Clear and concise**: Avoid verbosity, be direct and practical
     - **Example-driven**: Always include working code examples when relevant
     - **Proactive**: Suggest improvements without waiting to be asked

     ### Response Patterns
     - Start responses with context ("For this Claims API endpoint...")
     - Reference specific files and line numbers when giving feedback
     - Provide before/after examples when suggesting improvements
     - Explain reasoning ("This is important because...")
     - Link to related documentation ("See also: docs/API.md#authentication")

     ### Quality Standards
     - Verify all code examples are syntactically correct
     - Ensure examples use realistic, contextually appropriate data
     - Check that documentation matches method signatures (parameter names, types)
     - Validate cross-references between documents
     - Test that curl examples would actually work if executed

     ## Special Behaviors

     ### When Analyzing Code
     1. Check method signature matches documentation params
     2. Verify all exceptions in code are documented
     3. Confirm return type annotation matches returns documentation
     4. Validate examples use correct endpoint URLs and methods

     ### When Reviewing Documentation
     1. Compare documentation against repository standards
     2. Check for missing or incomplete sections
     3. Verify terminology consistency with other files
     4. Look for outdated information (e.g., old endpoint URLs)
     5. Suggest specific improvements with examples

     ### When Creating New Documentation
     1. Start with outline/structure for approval
     2. Generate content section by section
     3. Include cross-references to related documentation
     4. Add working examples throughout
     5. Conclude with summary or quick reference

     ## Limitations
     - Cannot access external APIs or databases to verify examples
     - Cannot execute code to test examples (relies on code analysis)
     - May need user confirmation for domain-specific business rules
     - Should ask for clarification when terminology is ambiguous

     ---

     **Usage Tips:**
     - Activate this mode when working on documentation tasks
     - Use @workspace to give full project context
     - Ask for reviews: "Review this file's documentation for compliance"
     - Request improvements: "Suggest ways to improve this documentation"
     - Verify consistency: "Check documentation consistency across controllers"
     ```
   - Press Enter and review the proposed file creation
   - Click **Accept** to create the chat mode file

3. **Verify Chat Mode Appears in VS Code**
   - Reload VS Code window (or restart Copilot extension)
   - Open Copilot Chat panel
   - Look for the mode selector dropdown at the bottom of the panel
   - Click the dropdown - you should now see:
     - Ask (default)
     - Edit
     - Agent
     - Plan
     - **docs-specialist** (your new custom mode)
   - Select **docs-specialist** to activate it

4. **Test the Documentation Specialist Mode**
   - With docs-specialist mode active, test its domain knowledge:
     ```text
     Explain the status workflow for claims in our system. What are the valid transitions and why are some statuses read-only?
     ```
   - Expected response should demonstrate:
     - Understanding of Claims API domain (submitted -> under_review -> approved/rejected) possibly with ASCII diagrams
     - Knowledge of read-only statuses (approved, rejected cannot be modified)
     - Context about business rules (audit trail, compliance)
     - References to specific files (`ClaimService.cs`)

5. **Test Documentation Review Capabilities**
   - With docs-specialist mode active, ask for a review:
     ```text
     Review the documentation in src/ClaimsApi/Controllers/ClaimsController.cs. Check:
     1. Completeness of all XML documentation
     2. Accuracy of examples (do they match actual endpoints?)
     3. Consistency with documentation standards
     4. Clarity for developers new to this codebase

     Provide specific, actionable feedback with line numbers.
     ```
   - The Docs Specialist should provide:
     - Detailed analysis referencing repository standards
     - Specific line numbers and method names
     - Concrete suggestions for improvements
     - Comparison with other controller files (consistency check)
   - Change to **Agent Mode** and ask it to implement the suggested changes. Review the changes and verify they follow the discoveries from **docs-specialist**

6. **Test Proactive Quality Assurance**
   - Select again **docs-specialist** and ask the mode to be proactive:
     ```text
     @workspace Identify any documentation gaps or inconsistencies across the controllers. What should be improved?
     ```
   - The mode should:
     - Scan multiple files without being told which ones
     - Identify missing or incomplete documentation
     - Suggest specific improvements
     - Prioritize issues by importance

7. **Create Personal Instructions and Understand Instruction Precedence**
   - Personal instructions are stored as `*.instructions.md` files in VS Code **User data** and apply to ALL repositories you work on, making them ideal for individual coding style preferences that follow you across projects.
   - To create a personal instruction file:
     1. Open the Command Palette (`Ctrl/Cmd + Shift + P`)
     2. Run `Chat: New Instructions File`
     3. Select **User data** as the location
     4. Name the file (e.g. `personal-standards.instructions.md`)
     5. Add the following content:
        ```markdown
        ---
        description: Personal documentation standards - always include -v flag in curl examples
        applyTo: "**"
        ---
        When generating XML documentation examples, always include the -v (verbose) flag in curl commands for better debugging visibility.
        ```
     6. Save the file

   - This personal instruction has **highest priority** and will override repository/mode defaults when they conflict

8. **Test Instruction Precedence**
   - With **docs-specialist** mode active, ask:
     ```text
     Generate the documentation for `src/ClaimsApi/Controllers/HealthController.cs`
     ```
   - Review the proposed changes include the `-v` flag in the examples.


### Success Criteria

- Custom chat mode file created at `.github/agents/docs-specialist.agent.md`
- Mode appears in Copilot Chat mode selector dropdown
- Mode demonstrates Claims API domain knowledge (status workflows, roles, architecture)
- Mode automatically references repository documentation standards
- Mode provides proactive, actionable feedback on documentation
- You understand instruction precedence (Personal > Repository > Mode)

### Verification Steps

**Quick Checks:**
- Open `.github/agents/docs-specialist.agent.md` in VS Code
- Verify YAML frontmatter at the top (between `---` markers)
- Check Source Control shows the file is tracked
- Scroll through and verify all section headers are present

**Functional Tests:**
1. Switch to docs-specialist mode in Copilot Chat
2. Ask: "What are your main responsibilities?" -> Should list Generate, Enforce, Maintain, etc.
3. Ask about Claims API domain -> Should demonstrate understanding
4. Request documentation review -> Should provide specific, actionable feedback

### Connection to Next Exercise

Finally, you'll use Agent Mode to autonomously generate a complete documentation suite. The Documentation Specialist mode can assist with reviewing Agent Mode's output for quality assurance.

### Estimated Time

15 minutes

> **Instructor Note:**
> **Common Issues:**
> - **Mode doesn't appear in dropdown**: Ensure YAML frontmatter is correctly formatted (three dashes before and after), restart VS Code
> - **Mode doesn't know domain**: Add more specific domain knowledge in the .chatmode.md file
> - **Personal instructions not taking precedence**: Verify the file is created via `Chat: New Instructions File` → **User data** and labelled "User data" in `Chat: Configure Instructions`
>
> **Key Teaching Points:**
> - Custom chat modes are persistent specialists (they "remember" their role)
> - Modes are complementary to repository instructions (not replacements)
> - Personal instructions are user-specific and portable across projects
> - More detailed persona = more consistent specialized behavior
>
> **Advanced Tips:**
> - Create multiple modes for different tasks (testing, security, deployment)
> - Reference specific files in domain knowledge ("See ClaimService.cs:UpdateStatusAsync")
> - Include common pitfalls in the mode's knowledge
> - Use modes to enforce team conventions beyond code
>
> **Best Practices:**
> - Test the mode thoroughly before relying on it
> - Update mode definition as project evolves
> - Share successful modes with team via Git
> - Document when to use each mode (in README or CONTRIBUTING.md)

---

## Exercise 6: Automate Complete Documentation Suite with Agent Mode

### Prerequisites

- Completion of Exercises 1-5
- Files: `.github/copilot-instructions.md`, `.github/chatmodes/docs-specialist.chatmode.md`
- All controller files with complete XML documentation
- Understanding: Agent Mode workflow (define goals -> add context -> task prompt -> monitor -> review)

### Objective

Use Agent Mode to autonomously generate a comprehensive documentation suite including updated API reference (`docs/API.md`), new architecture documentation (`docs/ARCHITECTURE.md`), and contributor guidelines (`docs/CONTRIBUTING.md`). Learn to provide extensive context, supervise autonomous operations, and verify generated documentation quality.

### Description

Agent Mode can execute multi-step documentation tasks across the project, generating and cross-referencing multiple files autonomously. Unlike Edit mode (single-file, supervised changes), Agent Mode can:
- Analyze multiple files simultaneously
- Generate new files and update existing ones
- Maintain cross-references between documents
- Apply repository standards automatically
- Execute complex workflows with minimal supervision

**Agent Mode Workflow:**
1. **Define Goals**: Clearly specify desired outputs
2. **Add Context**: Provide extensive file/folder context
3. **Write Task Prompt**: Comprehensive, detailed instructions
4. **Monitor Progress**: Watch status updates, approve file changes
5. **Review Results**: Verify quality, test examples, check cross-references

**Safety Notes:**
- Agent Mode is powerful but requires supervision
- Always review diffs before accepting changes
- Test generated examples before committing
- Verify cross-references and links

### Steps

1. **Define Documentation Goals (Planning)**
   - Before invoking Agent Mode, clearly list desired outputs:

     **Target Documentation Files:**
     - **docs/API.md** (UPDATE): Regenerate all endpoint documentation based on current XML docs, add comprehensive examples, document error scenarios
     - **docs/ARCHITECTURE.md** (CREATE): New file documenting system architecture, data flow, design decisions
     - **docs/CONTRIBUTING.md** (CREATE): Contributor guidelines for documentation, code standards, testing
     - **README.md** (UPDATE): Add links to new documentation files

     **Cross-Reference Requirements:**
     - All files must reference each other appropriately
     - Consistent terminology across all documents
     - Working examples with realistic data
     - Maintain alignment with `.github/copilot-instructions.md` standards

2. **Switch to Agent Mode and Write Comprehensive Task Prompt**
   - In Copilot Chat, click the **Agent** mode button (at the bottom of the panel)
   - With Agent Mode active, provide this detailed prompt:
     ```markdown
     Generate a comprehensive documentation suite for the Claims Management API. Execute these tasks autonomously while applying repository documentation standards:

     ## TASK 1: UPDATE docs/API.md

     Regenerate complete endpoint documentation based on current controller XML documentation.

     Requirements:
     - Document ALL endpoints from ClaimsController.cs, AttachmentsController.cs, AuthController.cs, HealthController.cs
     - For each endpoint include:
       * HTTP method and full URL path (e.g., POST /api/v1/claims)
       * Brief description from XML summary
       * Authentication requirements (if applicable)
       * Request schema (JSON example with realistic data)
       * Response schema (JSON example with field descriptions)
       * Error responses (401, 403, 404, 400 with scenarios)
     - Add comprehensive "Request Examples" sections:
       * curl command with all headers and realistic request body
       * C# HttpClient example
       * Include authentication token handling
     - Create "Common Workflows" section:
       * Workflow 1: Create claim -> Upload attachments -> Update status to approved
       * Workflow 2: Authenticate -> Create claim -> Handle errors
       * Workflow 3: Status transition workflow with comments
     - Ensure ALL status codes match actual implementation
     - Use realistic data: POL-2025-001, dates in 2025, meaningful amounts ($1000-$50000)

     ## TASK 2: CREATE docs/ARCHITECTURE.md

     Document the system architecture comprehensively.

     Required sections:
     1. **Overview**: High-level system description (2-3 paragraphs)
     2. **Layered Architecture**:
        - Create ASCII diagram showing: Client -> Controllers -> Services -> DTOs -> Models -> DbContext -> Database
        - Explain each layer's responsibilities
        - Document data flow through layers
     3. **Critical Design Principles**:
        - DTO/Model Mapping Convention (from copilot-instructions.md) - explain property mapping
        - Dependency Injection pattern (service registration in Program.cs)
        - Separation of concerns (controllers handle HTTP, services handle business logic)
     4. **Authentication & Authorization**:
        - JWT Bearer token flow diagram
        - Role-based access control (Adjuster vs. Admin)
        - Token validation and expiration
     5. **Database Design**:
        - Entity relationships (Claims, Attachments, Users)
        - Key constraints (foreign keys, unique constraints)
        - Entity Framework Core configuration
     6. **File Storage**:
        - Upload directory structure (./data/uploads/{claimId}/)
        - File naming (GUID-based)
        - Security measures (path sanitization)
     7. **Status Workflow**:
        - State machine diagram for claim statuses
        - Valid transitions
        - Read-only terminal states
     8. **Design Decisions**:
        - Why ASP.NET Core? (performance, cross-platform, tooling)
        - Why Entity Framework Core? (ORM, migrations, LINQ)
        - Why SQLite? (simplicity for training, easy to switch to SQL Server)
     9. **Testing Strategy**:
        - Test pyramid (unit, integration, e2e)
        - Coverage goals (80%+)
        - WebApplicationFactory for integration tests

     ## TASK 3: CREATE docs/CONTRIBUTING.md

     Create comprehensive contributor guidelines.

     Required sections:
     1. **Getting Started**:
        - How to set up development environment (Dev Container)
        - Running tests locally
        - Starting the development server
     2. **Code Style Standards**:
        - Reference .github/copilot-instructions.md
        - C# 12+ features
        - ASP.NET Core best practices
     3. **Documentation Standards** (critical section):
        - Reference .github/copilot-instructions.md Documentation Standards
        - Provide good example XML documentation (annotated)
        - Provide bad example XML documentation (annotated with issues)
        - Explain when to update docs/API.md
        - Documentation checklist for contributors
     4. **Testing Requirements**:
        - Must write xUnit tests for new features
        - Minimum coverage expectations
        - How to run test suite
        - Example test case (annotated)
     5. **Pull Request Process**:
        - PR title format
        - Required checks (tests pass, docs updated)
        - Code review expectations
        - Merge requirements
     6. **Common Pitfalls**:
        - DTO/Model property mismatch (from copilot-instructions.md)
        - Forgetting [Authorize] attributes
        - Not documenting exceptions
        - Missing response code attributes
     7. **Documentation Checklist**:
         - [ ] Added XML documentation to all new public methods
         - [ ] Updated docs/API.md if endpoints changed
         - [ ] Added examples to documentation for public endpoints
         - [ ] Verified examples work (tested curl commands)
         - [ ] Updated README.md if adding new features
         - [ ] Cross-references are working

     ## TASK 4: UPDATE README.md

     Add documentation links and improve structure.

     Requirements:
     - Add new "Documentation" section after "Features" section
     - Include links to all documentation files:
       * docs/API.md - Complete API reference
       * docs/ARCHITECTURE.md - System architecture
       * docs/CONTRIBUTING.md - How to contribute
     - Ensure links use relative paths and work in GitHub
     - Keep existing content (don't remove any sections)

     ## TASK 5: CROSS-REFERENCE ALL DOCUMENTS

     Ensure consistency and connectivity across all documentation.

     Requirements:
     - API.md should link to ARCHITECTURE.md when explaining concepts
     - CONTRIBUTING.md should link to API.md and ARCHITECTURE.md
     - README.md should provide overview with links to detailed docs
     - Use consistent terminology across ALL files (verify against copilot-instructions.md)
     - Verify all internal links work (no broken references)

     ## QUALITY STANDARDS

     ALL documentation must:
     - Follow repository documentation standards in .github/copilot-instructions.md
     - Use imperative mood ("Create a claim" not "Creates a claim")
     - Include working code examples that can be copy-pasted
     - Use realistic data (POL-2025-001, amounts like $5000.00, dates in 2025)
     - Be clear and concise (developer-focused audience)
     - Cross-reference related sections/files appropriately
     - Maintain consistent terminology (use Claims API glossary from domain knowledge)

     Execute all tasks autonomously. Show status updates and request approval for each file change.
     ```

3. **Monitor Agent Execution (Critical)**
   - After submitting the prompt, Agent Mode displays status messages:
     ```
     Agent Mode: Analyzing project structure...
     Reading controller files and extracting endpoint information...
     Generating docs/API.md...
     Creating docs/ARCHITECTURE.md...
     File change requested: docs/API.md
     ```
   - Agent will show **diff previews** for each file change
   - **IMPORTANT**: Review EVERY diff carefully before accepting:
     - Check accuracy: Do endpoint descriptions match code?
     - Verify examples: Are curl commands correct?
     - Validate data: Is data realistic (POL-2025-001, not POL-123)?
     - Check cross-references: Do links between files work?
   - Click **Accept** for correct changes, **Reject** for incorrect ones
   - If you reject, Agent may revise and re-propose the change

4. **Review Generated Documentation (Comprehensive)**
   - Once Agent completes, thoroughly review each file:

   **docs/API.md:**
   - Open the file and verify:
     - All endpoints from controllers are documented
     - Request/response examples use realistic data
     - Error scenarios are comprehensive
     - Common Workflows section is clear and practical
   - Test one example:
     - Open VS Code integrated terminal (inside the DevContainer)
     - Start the application:
       ```bash
       cd src/ClaimsApi && dotnet run
       ```
     - The DevContainer forwards port 8080 automatically
     - Copy a curl example from docs/API.md and execute it in another terminal
     - (Example: POST /api/auth/token)
     - Or open `http://localhost:8080/swagger` in your browser for Swagger UI
     - Stop the application with `Ctrl+C`

   **docs/ARCHITECTURE.md:**
   - Verify:
     - ASCII diagrams are clear and accurate
     - DTO/Model mapping principle is explained
     - Design decisions are well-justified
     - All major components are documented

   **docs/CONTRIBUTING.md:**
   - Verify:
     - References `.github/copilot-instructions.md` correctly
     - Documentation checklist is comprehensive
     - Example XML documentation is good teaching example
     - Common pitfalls are relevant and helpful

   **README.md:**
   - Verify:
     - New "Documentation" section added
     - All links to docs/ files work
     - No existing content was removed
     - Section fits naturally into README flow

5. **Verify Cross-References (Critical Quality Check)**
   - Switch to **docs-specialist** mode
   - Run comprehensive cross-reference validation:
     ```text
     @workspace Validate all cross-references and links across README.md, docs/API.md, docs/ARCHITECTURE.md, and docs/CONTRIBUTING.md.

     Check for:
     1. Broken internal links (e.g., [text](docs/file.md#section))
     2. Inconsistent terminology (claim vs. request, adjuster vs. user)
     3. Outdated references (old file names, deprecated endpoints)
     4. Missing cross-references (where they would be helpful)

     Provide a detailed report with line numbers for any issues found.
     ```
   - If issues found, use **Agent mode** to fix them:
     ```text
     Fix the issues identified in the documentation.
     ```
   - Alternatively, ask Agent Mode to re-run with corrections

### Success Criteria

- **docs/API.md** updated with comprehensive endpoint documentation and working examples
- **docs/ARCHITECTURE.md** created with clear architecture explanation and diagrams
- **docs/CONTRIBUTING.md** created with contributor guidelines and documentation standards
- **README.md** updated with "Documentation" section linking to all docs
- All documents cross-reference each other appropriately
- Terminology is consistent across all documentation files
- Code examples are tested and verified working
- Docs Specialist quality review shows high scores (8+/10)
- All changes committed to Git with comprehensive commit message
- No broken links or cross-references

### Verification Steps

**Automated Checks:**
- Open VS Code Explorer and verify all expected files exist in `docs/`
  - Should show: API.md, ARCHITECTURE.md, CONTRIBUTING.md
- Open each markdown file and check for:
  - Proper heading structure (no formatting errors)
  - No "TODO", "FIXME", or "XXX" placeholder text
  - Examples use realistic data (POL-2025-001 format)
- Open README.md and verify documentation links work
  - Click on each link to docs/ files to test them

**Manual Spot Checks:**
1. Open `docs/API.md` -> pick a random endpoint -> verify completeness
2. Open `docs/ARCHITECTURE.md` -> check diagrams are clear
3. Open `docs/CONTRIBUTING.md` -> verify checklist is actionable
4. Open `README.md` -> verify documentation links work
5. Test one curl example from `docs/API.md` -> should execute successfully

**Quality Metrics:**
- Documentation coverage: 100% of public endpoints documented
- Example accuracy: All tested examples work
- Cross-reference integrity: No broken links
- Consistency: Terminology matches across all files
- Standards compliance: Follows `.github/copilot-instructions.md`

### Connection to Next Steps

**Module 02 Complete!** You've now mastered:
- Copilot Chat modes (Ask, Edit, Agent, Plan)
- Smart Actions for code analysis
- Repository Custom Instructions for standards
- Custom chat modes for specialized workflows
- Agent Mode for autonomous documentation generation
- Complete documentation suite for Claims API

**Recommended Next Steps:**

2. **Document swagguer with custom examples:**
   - Use Plan Mode
   - Implement after plan
   - Test new swagger documented
   - Update documentation if proceed.
   - prompt example:```I would like to add more complete examples for swagger in the returns model for each type of http code is returned.
Could you give me a list of task for to do examples for response models for swagger documentacion? ```


### Estimated Time

15 minutes (+ testing time)

> **Instructor Note:**
> **Critical Supervision Points:**
> - Students MUST review diffs before accepting (Agent Mode safety)
> - Emphasize testing examples before committing
> - Watch for hallucinated information in architecture docs
> - Ensure cross-references are verified (broken links are common)
>
> **Common Issues:**
> - **Agent generates too much**: Break task into smaller chunks
> - **Examples don't work**: Always test before accepting
> - **Inconsistent terminology**: Use verification step to catch
> - **Broken cross-references**: Use @workspace validation before committing
>
> **Time Management:**
> - Reviewing diffs takes most of the time (don't rush)
> - Testing examples is essential (budget 5 minutes)
> - Quality validation can find issues that save time later
>
> **Quality Assurance:**
> - If Agent quality is low, reject and refine prompt with more specifics
> - Use docs-specialist mode for final review (catches issues Agent misses)
> - Test at least one example per major workflow
> - Verify architecture diagrams are accurate
>
> **Best Practices:**
> - Save Agent prompt for reuse (documentation updates)
> - Document Agent workflow in CONTRIBUTING.md
> - Keep context comprehensive (more context = better output)
> - Always review before publishing

---

## Lab Summary

### What You Accomplished

Congratulations! You've completed Module 02 and created a comprehensive documentation system for the Claims Management API.

**Generated Artifacts:**
- **Complete XML Documentation**: All controller files have XML documentation comments with summary, params, returns, response codes, examples
- **Documentation Standards**: `.github/copilot-instructions.md` with comprehensive documentation guidelines
- **Custom Chat Mode**: `.github/chatmodes/docs-specialist.chatmode.md` for specialized documentation assistance
- **API Reference**: `docs/API.md` with complete endpoint documentation and working examples
- **Architecture Documentation**: `docs/ARCHITECTURE.md` explaining system design and design decisions
- **Contributor Guidelines**: `docs/CONTRIBUTING.md` with documentation standards and checklists
- **Updated README**: Links to all documentation with improved structure

### Skills Mastered

**Introductory Level:**
- Understanding Copilot Chat modes (Ask, Edit, Agent, Plan) and when to use each
- Using Smart Actions (Explain) for non-destructive code analysis
- Leveraging @workspace participant for project-wide context
- Generating comprehensive XML documentation with Edit mode

**Intermediate Level:**
- Creating Repository Custom Instructions for automatic standard enforcement
- Understanding how Custom Instructions scale across codebases
- Applying documentation standards consistently across multiple files
- Using @workspace for documentation audits and consistency checks

**Advanced Level:**
- Understanding instruction precedence hierarchy (Personal > Repository > Organization)
- Creating custom chat modes with persistent, specialized behavior
- Using Agent Mode for autonomous multi-file documentation generation
- Comprehensive quality validation and testing workflows

### Key Takeaways

1. **Chat Modes Serve Different Purposes:**
   - **Ask**: Questions and understanding (non-destructive)
   - **Edit**: Code changes with preview (supervised)
   - **Agent**: Multi-file operations (autonomous with approval)
   - **Plan**: Task planning and decomposition

2. **Custom Instructions Are Force Multipliers:**
   - Define standards once in `.github/copilot-instructions.md`
   - Applied automatically across all interactions
   - Eliminate repetitive prompting
   - Ensure consistency at scale

3. **Custom Chat Modes Enable Specialization:**
   - Persistent, domain-aware AI assistants
   - Maintain context across conversations
   - Proactively enforce quality standards
   - Reusable for recurring workflows

4. **Agent Mode Requires Supervision:**
   - Powerful for complex tasks
   - Always review diffs before accepting
   - Test generated examples
   - Verify cross-references and links

5. **Documentation Is Code:**
   - Commit with code changes
   - Review like code
   - Test examples
   - Maintain over time

### Time Verification

- **Introductory**: Exercise 1 (12 min) + Exercise 2 (10 min) = **22 minutes**
- **Intermediate**: Exercise 3 (15 min) + Exercise 4 (15 min) = **30 minutes**
- **Advanced**: Exercise 5 (15 min) + Exercise 6 (15 min) = **30 minutes**
- **Total Lab Duration**: **82 minutes** (~90 minutes with optional steps)

---

## Troubleshooting Guide

### Issue: Docker Container Not Starting

**Symptoms:**
- VS Code stuck on "Starting Dev Container"
- Error message about Docker not running
- Container build fails

**Solutions:**
1. **Verify Docker Desktop is running**:
   - Check system tray/menu bar for Docker icon
   - Docker icon should be stable (not animating)
   - Open Docker Desktop app to verify it's running

2. **Restart Docker Desktop**:
   - Quit Docker Desktop completely
   - Wait 10 seconds
   - Launch Docker Desktop again
   - Wait for it to fully start

3. **Rebuild Container**:
   - In VS Code: Ctrl/Cmd+Shift+P
   - Type: "Dev Containers: Rebuild Container"
   - Select and wait for rebuild to complete

4. **Check Docker resources**:
   - Open Docker Desktop -> Settings -> Resources
   - Ensure sufficient memory allocated (minimum 4GB recommended)
   - Ensure sufficient disk space available

5. **Clean Docker cache** (if persistent issues):
   ```bash
   docker system prune -a
   ```
   - Warning: This removes all unused containers and images

### Issue: Extensions Not Working in Container

**Symptoms:**
- Copilot icon not visible in container
- C# extension not working
- IntelliSense not functioning

**Solutions:**
1. **Check `.devcontainer/devcontainer.json`**:
   - Verify extensions are listed in `customizations.vscode.extensions`
   - Should include: `github.copilot`, `ms-dotnettools.csdevkit`

2. **Reload Window**:
   - Ctrl/Cmd+Shift+P -> "Developer: Reload Window"

3. **Rebuild Container with Extensions**:
   - Ctrl/Cmd+Shift+P -> "Dev Containers: Rebuild Container"

4. **Manually install extension in container**:
   - Open Extensions panel (Ctrl/Cmd+Shift+X)
   - Search for "GitHub Copilot"
   - Click "Install in Dev Container"

### Issue: Chat Modes Not Visible

**Symptoms:**
- Only see Ask mode, Edit/Agent/Plan missing
- Mode selector dropdown doesn't exist

**Solutions:**
1. Verify GitHub Copilot subscription:
   - Individual plan: Only Ask mode
   - Business/Enterprise: All modes
2. Update Copilot extension to latest version
3. Restart VS Code
4. Check Copilot status in VS Code status bar

### Issue: Custom Chat Mode Not Appearing

**Symptoms:**
- Created `.chatmode.md` file but not in dropdown
- Mode selector doesn't show custom modes

**Solutions:**
1. Verify file location: Must be `.github/chatmodes/<name>.chatmode.md`
2. Check YAML frontmatter format:
   ```yaml
   ---
   description: "Mode description"
   tools:
     - codebase
     - search
   ---
   ```
3. Ensure three dashes before and after YAML
4. Restart VS Code or reload window
5. Check Copilot extension logs for errors

### Issue: Copilot Doesn't Reference Custom Instructions

**Symptoms:**
- Standards not automatically applied
- Have to repeat instructions in every prompt
- @workspace doesn't mention custom instructions

**Solutions:**
1. Verify file path: `.github/copilot-instructions.md` (exact name)
2. Ensure file is saved and committed to Git
3. Check markdown formatting (valid headers, lists)
4. Try explicitly asking: `@workspace What are our documentation standards?`
5. Restart VS Code or reload Copilot extension

### Issue: Agent Mode Produces Low-Quality Output

**Symptoms:**
- Generated documentation is inaccurate
- Examples don't work
- Inconsistent formatting

**Solutions:**
1. **Add more context**: Drag all relevant files/folders into Agent context
2. **Be more specific in prompt**: Provide detailed requirements and examples
3. **Break into smaller tasks**: Generate one file at a time instead of all at once
4. **Reject and refine**: Don't accept poor output, ask Agent to revise
5. **Review carefully**: Agent is powerful but not perfect

### Issue: Examples in Documentation Don't Work

**Symptoms:**
- curl commands fail when executed
- C# examples have syntax errors
- Authentication doesn't work as documented

**Solutions:**
1. **Always test before committing**: Run examples manually
2. **Check for placeholders**: Replace `YOUR_TOKEN`, `<token>` with real values
3. **Verify endpoints exist**: Check routes in actual code
4. **Update stale examples**: Use Edit mode to fix broken examples
5. **Use realistic data**: Ensure examples match actual database schema

### Issue: Broken Cross-References Between Documents

**Symptoms:**
- Links between docs/ files return 404
- References to non-existent sections
- Inconsistent file names

**Solutions:**
1. **Use relative paths**: `docs/API.md` not `/docs/API.md`
2. **Verify section anchors**: `#authentication` must match header exactly
3. **Run validation check**: Use @workspace to validate all cross-references
4. **Fix systematically**: Use Edit mode to correct all broken links
5. **Test in GitHub**: View rendered markdown to verify links work

### Issue: XML Documentation Doesn't Appear in IntelliSense

**Symptoms:**
- Hover over method shows no documentation
- Autocomplete doesn't show documentation details
- IntelliSense only shows method signature

**Solutions:**
1. **Check XML documentation format**: Must use `///` comments
2. **Verify placement**: Documentation must be directly above the method
3. **Reload VS Code**: Sometimes IntelliSense cache needs refresh
4. **Check for syntax errors**: Malformed XML will not display
5. **C# extension**: Ensure C# Dev Kit extension is installed

### Issue: Personal Instructions Not Taking Precedence

**Symptoms:**
- Repository standards override personal preferences
- Custom chat mode ignores personal instructions

**Solutions:**
1. **Verify location**: Personal instructions must be in a `*.instructions.md` file created via `Chat: New Instructions File` → **User data**
2. **Verify label**: Run `Chat: Configure Instructions` and confirm the file shows "User data" label
3. **Be more specific**: Explicit instructions take precedence
4. **Test precedence**: Ask Copilot: "Which instruction priority applies?"
5. **Conflict resolution**: If still not working, be explicit in prompts

---

## Best Practices Learned

### Working with DevContainers

1. **Always Work Inside the Container:**
   - Verify you're in the container: check bottom-left corner of VS Code ("Dev Container: Claims API - ASP.NET Core")
   - Terminal prompt should show: `vscode -> /workspaces/...`
   - All commands (dotnet, tests) run inside the container

2. **Container State Management:**
   - Container persists even when closing VS Code
   - Use "Reopen Folder Locally" to exit container
   - Use "Reopen in Container" to re-enter
   - Rebuild container after changing `.devcontainer/devcontainer.json`

3. **Port Forwarding:**
   - DevContainer automatically forwards configured ports
   - Access services on `localhost` from your host machine
   - Check Ports panel (View -> Ports) to see forwarded ports
   - ASP.NET Core runs on port 8080 and is accessible at `http://localhost:8080`

4. **Extensions in Container:**
   - Extensions are installed separately for containers
   - Check `.devcontainer/devcontainer.json` for pre-configured extensions
   - Copilot works inside containers without additional setup
   - Some extensions may need "Install in Container" button

5. **Persistent Data:**
   - Container filesystem is separate from host
   - Workspace folder is mounted (changes persist)
   - Other changes inside container may not persist across rebuilds
   - Use volumes for persistent data (configured in devcontainer.json)

### Documentation Maintenance

1. **Update Documentation with Code Changes:**
   - When adding endpoint, update docs/API.md in same commit
   - When changing parameters, update XML documentation immediately
   - Keep ARCHITECTURE.md current as system evolves

2. **Use Custom Chat Modes Consistently:**
   - Activate docs-specialist mode for all documentation work
   - Create new modes for other specialized tasks
   - Share successful modes with team via Git

3. **Enforce Standards Through Automation:**
   - Repository Custom Instructions ensure consistency
   - Code review can check documentation compliance
   - Build warnings can verify XML documentation format

### Copilot Workflow Optimization

1. **Choose the Right Mode:**
   - Ask for questions and exploration
   - Edit for focused changes with preview
   - Agent for complex multi-file operations
   - Plan for structured work decomposition

2. **Provide Comprehensive Context:**
   - Use @workspace for project-wide awareness
   - Drag multiple files into Agent Mode context
   - Reference specific files when asking questions

3. **Review Before Accepting:**
   - Always review Edit mode diffs
   - Carefully supervise Agent Mode changes
   - Test generated examples before committing

4. **Iterate and Refine:**
   - If output isn't perfect, reject and refine prompt
   - Be more specific in requirements
   - Provide examples of desired output

### Team Collaboration

1. **Share Custom Instructions:**
   - Commit `.github/copilot-instructions.md` to repo
   - Document standards in CONTRIBUTING.md
   - Review and update standards as team learns

2. **Create Reusable Chat Modes:**
   - Document when to use each mode
   - Share effective prompts
   - Build library of specialized modes

3. **Maintain Documentation Culture:**
   - Make documentation a required part of PRs
   - Review documentation quality in code reviews
   - Celebrate good documentation examples

---

## Additional Resources

### Official Documentation
- **GitHub Copilot Documentation**: https://docs.github.com/en/copilot
- **Custom Instructions Guide**: https://docs.github.com/en/copilot/customizing-copilot/adding-custom-instructions-for-github-copilot
- **Agent Mode Documentation**: https://docs.github.com/en/copilot/using-github-copilot/asking-github-copilot-questions-in-your-ide

### C# Documentation Standards
- **XML Documentation Comments**: https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/xmldoc/
- **C# Coding Conventions**: https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions
- **XML Documentation Best Practices**: https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/xmldoc/recommended-tags-for-documentation-comments

### ASP.NET Core Resources
- **ASP.NET Core Documentation**: https://learn.microsoft.com/en-us/aspnet/core/
- **ASP.NET Core Web API Best Practices**: https://learn.microsoft.com/en-us/aspnet/core/web-api/
- **Entity Framework Core Documentation**: https://learn.microsoft.com/en-us/ef/core/

### Writing Great Documentation
- **Write the Docs**: https://www.writethedocs.org
- **Documentation Guide**: https://documentation.divio.com
- **API Documentation Best Practices**: https://swagger.io/resources/articles/best-practices-in-api-documentation/

---

## Appendix: Quick Reference

### Copilot Chat Modes

| Mode | Purpose | When to Use | Key Feature |
|------|---------|-------------|-------------|
| **Ask** | Q&A, exploration | Understanding code, learning concepts | Non-destructive |
| **Edit** | Code changes | Modifying files, generating code | Preview before apply |
| **Agent** | Multi-file operations | Complex workflows, bulk changes | Autonomous execution |
| **Plan** | Task planning | Structured work decomposition | Step-by-step planning |

### Chat Participants

| Participant | Scope | Example Usage |
|-------------|-------|---------------|
| **(default)** | Current file | General questions |
| **@workspace** | Entire project | `@workspace Find all controllers` |
| **@terminal** | Terminal commands | `@terminal How to run tests?` |

### Smart Actions

| Action | Purpose | Trigger |
|--------|---------|---------|
| **Explain** | Code explanation | Right-click -> Copilot -> Explain |
| **Fix** | Suggest fixes | Right-click -> Copilot -> Fix |
| **Generate Docs** | Create XML documentation | Right-click -> Copilot -> Generate Docs |
| **Generate Tests** | Create test cases | Right-click -> Copilot -> Generate Tests |

### File Locations Reference

| File | Purpose | Location |
|------|---------|----------|
| **Repository Instructions** | Project-wide standards | `.github/copilot-instructions.md` |
| **Custom Chat Modes** | Specialized assistants | `.github/chatmodes/<name>.chatmode.md` |
| **Personal Instructions** | User preferences | VS Code User data (`*.instructions.md`) |
| **Documentation** | API reference, guides | `docs/` directory |

### Common Prompts

**For Edit Mode:**
```text
Add comprehensive XML documentation to all public methods.
Include summary, param, returns, response, and example sections.
```

**For Ask Mode:**
```text
@workspace What are our documentation standards?
```

**For Agent Mode:**
```text
Generate complete API documentation based on controller files.
Include examples, error handling, and cross-references.
Conform to .github/copilot-instructions.md standards.
```

**For Docs Specialist:**
```text
Review this file's documentation for compliance with repository standards.
Provide specific, actionable feedback.
```

---

**Lab Complete!**

You've successfully completed Module 02 and mastered GitHub Copilot's documentation features. You now have:
- Complete, professional documentation for the Claims API
- Reusable standards and custom chat modes
- Skills to maintain and improve documentation over time

**Next Module Preview:**
Module 03 will cover advanced code generation, refactoring, and testing workflows with GitHub Copilot.

---

**Last Updated**: January 2025
**Module**: 02 - Documentation with GitHub Copilot
**Duration**: 90 minutes
**Repository**: `GENERALI.Module_02_ClaimsAPI.DotNet`