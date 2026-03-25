# Module 02 - Documentation With GitHub Copilot (2h) - Trainer Script

This is an instructor read-aloud script. Keep this file on a second screen and share only VS Code during the session.

Important: the prompts in this script are copied verbatim from `info/Module_02.DotNet.md`. Do not edit them.

## Run Of Show (120 min)

- 00:00-00:05 Waiting room / late arrivals
- 00:05-00:15 Session intro + how the lab works
- 00:15-00:20 Environment check (everyone can run the lab)
- 00:20-00:32 Exercise 1
- 00:32-00:42 Exercise 2
- 00:42-00:57 Exercise 3
- 00:57-01:00 Checkpoint + decide break length
- 01:00-01:10 Break (10 min if on time, otherwise 5 min)
- 01:10-01:25 Exercise 4
- 01:25-01:40 Exercise 5
- 01:40-01:55 Exercise 6
- 01:55-02:00 Wrap-up + survey link + close

## Pre-Flight (Before The Session)

- Open `Exercise 1/` in VS Code.
- Open Copilot Chat and verify you can send a message.
- Keep `Requirements.md` handy in case someone is blocked.

## 00:00-00:05 Waiting Room / Late Arrivals

Say:

"Hi everyone, we will start in about five minutes to give people time to join. While we wait, please open VS Code, open the `Exercise 1` folder, and make sure GitHub Copilot Chat is working."

If you are required to record the session, start recording now and say:

"Quick reminder: this session is being recorded."

## 00:05-00:15 Session Intro + How The Lab Works

Say:

"Today is a 2-hour hands-on lab about using GitHub Copilot for writing and maintaining documentation in a .NET Claims Management API."

"We will work in short exercises from introductory to advanced. I will do each exercise on screen, and you will replicate it on your machine. If you fall behind, that's fine: finish the current step, then re-join us at the next prompt."

"You have a few key files in the lab package:"

- "`Requirements.md` is the setup guide."
- "`Lab_Script.md` is the student-facing exercise guide."
- "`Prompts.md` is a copy/paste reference."
- "`Exercise 1/ ... Exercise 7/` are checkpoints you can use if you need to catch up."

"How we will interact: please stay muted by default and ask questions in the meeting chat. I will pause briefly after each exercise for quick questions."

"We will take a short break halfway through: 10 minutes if we are on time, otherwise 5 minutes."

## 00:15-00:20 Environment Check (Everyone Can Run The Lab)

Say:

"Before we begin: please confirm you can see Copilot Chat and you can send a message. If Copilot does not respond, restart VS Code and verify you are logged in with the correct GitHub account."

If troubleshooting is taking too long, say (copy/paste into meeting chat if needed):

"If you experience issues with requirements and setup of lab environment, please consider to register again in another date and join our Support Calls available every Monday and Friday. Please write an email to TechnicalExcellenceSchools@generali.com and inform us about this."

## 00:20-00:32 Exercise 1 - Explore Copilot Chat Modes And Analyze Existing Code

Say:

"Exercise 1 is about understanding the Copilot Chat modes and using Smart Actions to explain code. The goal is to build understanding before we generate documentation."

Do (on screen):

- Open `src/ClaimsApi/Controllers/ClaimsController.cs`.
- Select the `CreateClaim` method and run Smart Action: right-click -> Copilot -> Explain.

Say:

"Ask mode is for questions and understanding; it is non-destructive. Edit mode proposes changes with a diff. Agent mode can do multi-file work. Plan mode helps you structure work."

Copy/paste prompt into Copilot Chat (and optionally into the meeting chat):

```text
What security measures does this endpoint implement and why are they important for a claims management system?
```

Then copy/paste:

```text
What are the main responsibilities of the ClaimsController?
```

Then copy/paste:

```text
@workspace Summarize all authentication requirements across the controllers in this project. Which endpoints require authentication and what roles are needed?
```

Optional demo (only if time):

```
Execute the tests and fix the problems that may arise. Don't change the code, just adjust the tests.
```

Checkpoint question:

"Does everyone see the same four chat modes? If you only see Ask mode, that typically means your Copilot plan does not include the other modes."

## 00:32-00:42 Exercise 2 - Generate XML Documentation Comments With Edit Mode And Smart Actions

Say:

"Exercise 2 is our first documentation generation task: we will add XML documentation comments to the controller methods and verify them via IntelliSense."

Do (on screen):

- Switch Copilot Chat to Edit mode.
- Keep `src/ClaimsApi/Controllers/ClaimsController.cs` active.

Copy/paste prompt into Copilot Chat (and optionally into the meeting chat):

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

Say:

"Before accepting: scroll the diff. Make sure parameter names and return types match the method signature. Reject and re-run with a more specific prompt if you see inaccuracies."

Quick verify:

- Hover a documented method and confirm the tooltip shows the new XML docs.

## 00:42-00:57 Exercise 3 - Establish Documentation Standards With Repository Custom Instructions

Say:

"Exercise 3 is where we stop repeating ourselves: we define repository-wide rules in `.github/copilot-instructions.md` so Copilot applies our documentation standards automatically."

Do (on screen):

- Create `.github/` folder if needed.
- Switch to Edit mode.

Copy/paste prompt into Copilot Chat (and optionally into the meeting chat):

````text
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
````

Now verify the instructions are being applied.

Copy/paste prompt into Copilot Chat:

```text
Review the XML documentation in src/ClaimsApi/Controllers/ClaimsController.cs against our repository documentation standards. List any gaps or non-compliant elements.
```

Then test automatic application.

Copy/paste prompt into Copilot Chat:

```text
Add documentation to all methods in this file.
```

## 00:57-01:00 Checkpoint + Decide Break Length

Say:

"We are at the halfway mark. If you are on track, take a 10-minute break. If you are behind, take a 5-minute break and then we will continue."

## 01:00-01:10 Break

Say:

"Please be back at :10 past the hour. When you return, we will apply the standards across multiple files and then create a documentation specialist mode and generate a documentation suite with Agent mode."

## 01:10-01:25 Exercise 4 - Apply Standards Across Multiple Files With Workspace Context

Say:

"Exercise 4 scales the workflow: we audit documentation coverage, then apply our standards across multiple controllers and the service layer."

Audit prompt:

```text
@workspace Analyze all controller files under src/ClaimsApi/Controllers/ and create a summary table showing:
1. Filename
2. Whether XML documentation is complete according to our documentation standards
3. Specific missing elements (summary, params, returns, response codes, examples)
4. Priority level (High/Medium/Low) based on method complexity
```

Then document `AuthController.cs`:

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

Then document `HealthController.cs`:

```text
Add complete XML documentation to all methods in this file following repository documentation standards.

For health check endpoint:
- Add class-level documentation explaining health check purpose (monitoring, liveness probes, Kubernetes)
- Document response format (status, version fields)
- Include example showing typical usage for monitoring tools
```

Then document `ClaimService.cs`:

```text
Add complete XML documentation to all public methods in this file following repository documentation standards.

For service methods:
- Document business logic and validation rules
- Include exception documentation for cases like claim not found
- Document status workflow transitions (submitted -> under_review -> approved/rejected)
- Note that approved/rejected claims are terminal states
```

Consistency check:

```text
@workspace Verify that all controller files (ClaimsController.cs, AttachmentsController.cs, AuthController.cs, HealthController.cs) now have complete XML documentation following our documentation standards.

For each file, confirm:
1. All public methods have XML documentation
2. Public endpoints have example sections
3. Summary/params/returns/response sections are present and complete
4. Terminology is consistent across files

Summarize any remaining gaps or inconsistencies.
```

## 01:25-01:40 Exercise 5 - Create Custom Chat Mode For Documentation Workflows

Say:

"Exercise 5 creates a specialized assistant: a documentation specialist mode that helps us enforce standards and review docs consistently."

Create the mode (Edit mode prompt):

````text
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
````

Test the mode:

```text
Explain the status workflow for claims in our system. What are the valid transitions and why are some statuses read-only?
```

Review prompt:

```text
Review the documentation in src/ClaimsApi/Controllers/ClaimsController.cs. Check:
1. Completeness of all XML documentation
2. Accuracy of examples (do they match actual endpoints?)
3. Consistency with documentation standards
4. Clarity for developers new to this codebase

Provide specific, actionable feedback with line numbers.
```

Proactive QA prompt:

```text
@workspace Identify any documentation gaps or inconsistencies across the controllers. What should be improved?
```

Instruction precedence test prompt:

```text
Generate the documentation for `src/ClaimsApi/Controllers/HealthController.cs`
```

## 01:40-01:55 Exercise 6 - Automate Complete Documentation Suite With Agent Mode

Say:

"Exercise 6 is Agent mode: we give a structured task and let Copilot generate multiple documentation files with cross-references. Your job is supervision: review diffs, reject hallucinations, and test at least one example."

Agent Mode prompt:

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

Cross-reference validation (docs-specialist):

```text
@workspace Validate all cross-references and links across README.md, docs/API.md, docs/ARCHITECTURE.md, and docs/CONTRIBUTING.md.

Check for:
1. Broken internal links (e.g., [text](docs/file.md#section))
2. Inconsistent terminology (claim vs. request, adjuster vs. user)
3. Outdated references (old file names, deprecated endpoints)
4. Missing cross-references (where they would be helpful)

Provide a detailed report with line numbers for any issues found.
```

Fix prompt (Agent mode):

```text
Fix the issues identified in the documentation.
```

## 01:55-02:00 Wrap-Up + Survey Link + Close

Say:

"We covered: Ask/Edit/Agent/Plan modes, Smart Actions, repository instructions, custom modes, and Agent mode for multi-file documentation generation."

"Key takeaway: treat documentation like code. Review diffs, verify accuracy, and keep docs updated with changes."

Post the LAB feedback survey link in the meeting chat and say:

"Please fill our LABS feedback survey, it takes a few minutes for you and it is super important for us to improve our School !"

Link:

https://welearngenerali.qualtrics.com/jfe/form/SV_6eSxmtUuuvITaMC

If needed, remind about prerequisites and support:

"If you had environment issues today, please consider registering again in another date and join the support calls."

Stop the recording and end the meeting.
