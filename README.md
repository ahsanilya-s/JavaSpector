::: titlepage
**JavaSpector**

*Java Code Quality Analysis Platform*

Software Design Document

Version 3.0

:::

# Introduction

JavaSpector is a comprehensive Java code quality analysis platform that
combines advanced Abstract Syntax Tree (AST) parsing with AI-powered
recommendations to detect code smells, security vulnerabilities, and
maintainability issues in Java projects. Built with a modern React+Vite
frontend and Spring Boot backend, the platform serves as an automated
code review assistant, enabling development teams to maintain high code
quality standards throughout the software development lifecycle.

## Project Scope

The project encompasses multiple interconnected modules designed to
provide end-to-end code quality assessment capabilities.

### Completed Modules

::: description
Secure user registration, login, and session management with BCrypt
password encryption, ensuring data protection and user privacy
compliance. Integrated with React Router DOM for seamless navigation and
protected routes.

ZIP/JAR file upload with drag-and-drop support, extraction, and Java
file collection capabilities supporting project structures up to 50MB.
Real-time upload progress tracking with visual feedback.

Twelve sophisticated detectors implementing complex algorithms for
comprehensive code smell detection:

-   Long Method Detector (cyclomatic and cognitive complexity)

-   Code Duplication Detector

-   Broken Modularization Detector (cohesion analysis)

-   Complex Conditional Detector

-   Deficient Encapsulation Detector

-   Empty Catch Block Detector

-   Long Identifier Detector

-   Long Parameter List Detector

-   Long Statement Detector

-   Magic Number Detector

-   Missing Default Case Detector

-   Unnecessary Abstraction Detector

Ollama AI service integration with fallback mechanisms for intelligent
code recommendations. Provides context-aware suggestions for refactoring
and code improvement when external services are unavailable.

Comprehensive text-based reporting with severity categorization
(Critical, Warning, Suggestion), visual diagram generation using
PlantUML, and PDF export capabilities using jsPDF. Reports include
executive summaries, detailed issue breakdowns, and actionable
recommendations.

Persistent storage and retrieval of analysis sessions with detailed
metrics, enabling trend analysis, code quality improvement tracking, and
comparative analysis across multiple project versions.

Modern React 18.3.1 + Vite 7.1.7 frontend featuring:

-   Radix UI component library for accessible, production-ready
    components

-   Tailwind CSS v4 for utility-first styling with PostCSS optimization

-   next-themes for seamless dark/light mode switching

-   Recharts for interactive data visualization and analytics

-   Framer Motion for smooth animations and transitions

-   React Hook Form for efficient form validation

-   Lucide React icons for consistent iconography

-   Responsive design optimized for desktop, tablet, and mobile devices

Administrative interface for user management, system monitoring,
configuration control, and analytics dashboard with real-time metrics
visualization.
:::

### Key Features Implemented

The platform incorporates several advanced features that distinguish it
from conventional static analysis tools:

::: description
Utilizes both cyclomatic and cognitive complexity metrics to provide
nuanced code quality evaluation beyond simple line counts.

Integration with JavaParser library enables immediate Abstract Syntax
Tree generation and analysis upon file upload, with progress tracking
and visual feedback in the UI.

Three-tier classification system (Critical, Warning, Suggestion)
prioritizes issues based on their impact on code quality and
maintainability.

Comparison capabilities allow developers to track code quality
improvements over time and identify regression patterns.

Contextual suggestions powered by Ollama AI provide actionable guidance
for addressing identified issues, with intelligent fallback mechanisms
ensuring continuous service availability.

Access control mechanisms with JWT-based authentication ensure that
uploaded code remains protected and accessible only to authorized users.
Files are stored with unique identifiers and proper access validation.
:::

# Design Methodology and Software Process Model

## Design Methodology: Object-Oriented Programming

The DevSync project follows Object-Oriented Programming (OOP)
principles, providing a robust foundation for building maintainable and
extensible software. This methodology was selected based on the
following justifications:

### Encapsulation

Each detector class, such as `LongMethodDetector` and
`CodeDuplicationDetector`, encapsulates specific analysis logic and
maintains internal state through private methods and fields. This design
principle ensures data integrity by preventing unauthorized access to
internal implementation details while providing clear, well-defined
interfaces for module interaction. For example, the complexity
calculation algorithms remain hidden within detector classes, exposing
only the final analysis results through public methods.

### Inheritance

The project utilizes inheritance through Spring Boot's component
hierarchy and JPA entity relationships. All detectors share common
analysis patterns inherited from base classes while extending
functionality for specific detection scenarios. This hierarchical
structure reduces code duplication and ensures consistent behavior
across the detector family.

### Polymorphism

The detector system demonstrates polymorphism where different detector
implementations are processed uniformly through common interfaces. This
enables flexible execution of the analysis pipeline, allowing new
detectors to be added without modifying existing orchestration logic.
The runtime binding of detector implementations supports extensibility
and testing through mock implementations.

### Abstraction

Complex analysis algorithms are abstracted into high-level interfaces,
hiding implementation details while providing clear contracts for
functionality. Users of the analysis engine interact with simplified
APIs without needing to understand the underlying AST traversal
algorithms or metric calculation formulas.

## Software Process Model: Iterative and Incremental Development

The project follows an Iterative and Incremental Development model,
chosen for its flexibility and risk mitigation capabilities in complex
software projects.

### Iterative Approach

The system was developed through multiple iterations, with each
iteration focusing on specific functionality:

1.  **Iteration 1:** Core authentication and user management

2.  **Iteration 2:** File processing and extraction pipeline

3.  **Iteration 3:** Basic code analysis with initial detectors

4.  **Iteration 4:** Report generation and visualization

5.  **Iteration 5:** AI integration and advanced recommendations

6.  **Iteration 6:** Admin panel and system monitoring

This approach allowed continuous refinement and improvement of existing
features based on feedback from each iteration.

### Incremental Delivery

Features were delivered incrementally, starting with core functionality
and progressively adding advanced capabilities. This enabled early
testing and validation, ensuring that foundational components were
stable before building dependent features.

### Risk Mitigation

The iterative approach allowed early identification and resolution of
technical challenges, particularly in AST parsing complexity and AI
service integration. Prototyping during early iterations exposed
potential issues before significant development investment.

### Flexibility

The incremental model provided flexibility to adapt requirements based
on testing feedback and emerging needs. Fallback mechanisms for AI
service unavailability were added in response to reliability concerns
identified during integration testing.

# System Overview

DevSync is an intelligent Java code analysis platform designed to
improve software quality through automated detection of code smells,
security vulnerabilities, and maintainability issues. The system
combines traditional static analysis techniques with modern AI-powered
insights to provide comprehensive code quality assessment.

## Functionality Context

The platform analyzes uploaded Java project files and generates detailed
reports containing actionable recommendations. Users can track code
quality improvements over time through historical analysis comparison
and receive AI-generated suggestions for code enhancement. The workflow
supports individual developers performing personal code reviews as well
as team leads monitoring project-wide code quality metrics.

## Design Context

The system architecture follows a client-server model where a React.js
frontend communicates with a Spring Boot backend through RESTful APIs.
The backend integrates multiple analysis engines and external AI
services, providing a unified interface for code quality assessment
regardless of the underlying analysis mechanism.

## Background Information

Modern software development faces increasing complexity in maintaining
code quality across large codebases. Manual code reviews are
time-consuming and may miss subtle issues that automated tools can
detect consistently. DevSync addresses this challenge by automating code
analysis using advanced algorithms and AI-driven recommendations,
reducing the burden on human reviewers while improving detection
coverage.

## Architectural Design

### Modular Program Structure

The DevSync system is decomposed into four major modules, each
responsible for distinct aspects of the platform's functionality.

#### Frontend Module (React+Vite)

The presentation layer consists of React components organized by
functionality, built with modern tooling:

::: description
Handle user login, registration, and session management with secure
token storage using React Router DOM for navigation.

Display analysis results with interactive visualizations using Recharts,
historical trends, and quick-access functionality with smooth
transitions powered by Framer Motion.

Comprehensive component library built with Radix UI primitives including
dialogs, dropdowns, accordions, tabs, tooltips, and more. Styled with
Tailwind CSS for consistent design and full accessibility compliance.

Dynamic dark/light mode switching using next-themes with persistent user
preferences and seamless transitions.

Manages all backend communication using Axios (v1.12.2) with request
interceptors, error handling, and response transformation.

Vite-powered development environment providing instant hot module
replacement (HMR), optimized production builds, and fast development
server.
:::

#### Backend Module (Spring Boot)

The application layer implements business logic through a layered
architecture:

::: description
REST endpoints handling HTTP requests with validation and response
formatting.

Business logic implementation with transaction management and
cross-cutting concerns.

Data access abstraction using Spring Data JPA with custom query methods.

Orchestrates detector execution and result aggregation.
:::

#### Analysis Engine Module

The core processing component responsible for code quality assessment:

::: description
JavaParser integration for source code parsing and syntax tree
generation.

Specialized analyzers for different code smell categories.

Formats analysis results into human-readable reports with visual
diagrams.

Ollama service connection with graceful degradation for service
unavailability.
:::

#### Data Management Module

Persistence and storage management:

::: description
Account data, preferences, and access control.

Tracking of past analyses with comparison capabilities.

Secure storage and retrieval of uploaded projects and generated reports.
:::

### Module Relationships and Collaboration

The system modules collaborate through well-defined interfaces to
provide comprehensive code analysis functionality. The frontend
communicates with the backend through RESTful APIs for authentication,
file uploads, and result retrieval. Controllers delegate business logic
to services, which interact with repositories for data persistence. The
analysis engine coordinates detector execution, report generation, and
AI service communication with fallback mechanisms.

Data flows unidirectionally from user input through processing layers to
storage, with query paths returning results through the same layered
structure. This separation ensures that changes to one layer do not
cascade unnecessarily to others.

*Note: The detailed box-and-line diagram is provided in Appendix A.*

### Detailed Architecture Mapping

The system implements a four-tier architecture with clear responsibility
boundaries:

#### Client Tier (Presentation Layer)

::: description
Functional components with hooks for state and lifecycle management,
utilizing React 18.3.1 features.

Context API for global state with local component state for UI
interactions, enhanced with React Hook Form for form validation.

Centralized Axios instance with interceptors for authentication and
error handling.

Radix UI primitives providing accessible, unstyled components including
Accordion, Alert Dialog, Avatar, Checkbox, Dialog, Dropdown Menu,
Navigation Menu, Popover, Progress, Radio Group, Scroll Area, Select,
Slider, Switch, Tabs, Toggle, and Tooltip.

Tailwind CSS v4.1.16 with PostCSS for utility-first styling,
class-variance-authority for component variants, and tailwind-merge for
class name optimization.

next-themes library providing seamless dark/light mode switching with
system preference detection and persistent storage.

Recharts library for interactive data visualization and analytics
dashboards.

Framer Motion for smooth, performant animations and transitions
throughout the interface.
:::

#### Server Tier (Application Layer)

::: description
Spring MVC controllers with request validation and response
serialization.

Service classes implementing domain logic with transactional boundaries.

External service connectors for AI and potential future integrations.

Spring Security configuration with JWT-based authentication.
:::

#### Data Tier (Persistence Layer)

::: description
JPA repositories with custom queries for complex data retrieval.

Domain entities with JPA annotations and validation constraints.

MySQL database with optimized schema design.

File system storage for uploaded projects and generated reports.
:::

#### Analysis Tier (Processing Layer)

::: description
JavaParser integration for AST generation from source files.

Individual detector implementations for specific code smells.

Orchestration of detector execution and result aggregation.

Report formatting and diagram generation.
:::

This layered architecture ensures separation of concerns,
maintainability, and scalability while providing clear interfaces
between system components.

# Design Models

## Activity Diagram: User Registration

This activity diagram explains how a user interacts with the system
during registration and login. First, the user provides basic
credentials. The system then checks whether the user already exists in
the database. If the user is new, the registration form is displayed and
the entered data goes through a validation process to ensure
correctness. After successful validation, the user is granted access to
the dashboard. In case of invalid data, the system stops the process and
shows an error message.

![Activity Diagram for User Registration and
Login](ActivityUserRegistration.jpeg){#fig:user-reg-activity
width="80%"}

## Activity Diagram: Code Analysis

This diagram represents the main functionality of the DevSync system.
The process starts when a developer uploads a ZIP file containing source
code. The system extracts the files and runs multiple detectors to
identify code issues such as smells or bad practices. These detectors
work simultaneously to save time. After analysis, the system
communicates with the local AI service (Ollama) to generate improvement
suggestions. If the AI service is unavailable, the system follows a
fallback mechanism to ensure that a report is still generated.

![Activity Diagram for Code Analysis
Workflow](ActivityCodeAnalysis.jpg){#fig:code-analysis-activity
width="80%"}

## Class Diagram: Whole System

The class diagram provides a structural overview of the DevSync system.
It shows the main classes, their attributes, and methods, along with the
relationships between them. Key components such as the UserController,
UploadController, and ReportGenerator coordinate system behavior. The
diagram also highlights how data is managed and stored in the database.
Overall, this diagram acts as a blueprint that helps developers
understand how different parts of the system are organized.

![Class Diagram for DevSync System](classDiagram.jpg){#fig:class-diagram
width="80%"}

## Sequence Diagram: User Registration

This sequence diagram illustrates the step-by-step interaction involved
in user registration and login. It shows how the user communicates with
the graphical interface, which then forwards requests to the
authentication controller. The controller validates the data by
interacting with the database. An alternative (Alt) flow is included to
handle both successful and failed login scenarios, clearly showing
system behavior in each case.

![Sequence Diagram for User
Registration](SD-userRegistration.jpeg){#fig:user-reg-seq width="80%"}

## Sequence Diagram: Code Analysis and AI Feedback

This sequence diagram focuses on the detailed workflow of code analysis.
The UploadController manages the entire process by coordinating file
extraction, detector execution, and communication with the AI service.
Once analysis is complete, the generated report is saved in the system
history and then displayed to the user. This diagram highlights how
different components interact in a well-defined order to complete the
analysis task.

![Detailed Sequence for Code Analysis and AI
Integration](SD-UplaodController.jpeg){#fig:upload-controller-seq
width="80%"}

## System Sequence Diagram (SSD)

The system sequence diagram presents a high-level view of the system
from an external perspective. It treats the system as a black box and
only shows interactions between the developer and the system. The
diagram covers major events such as uploading source code, starting the
analysis process, and retrieving past analysis results from history.

![System Sequence Diagram (High
Level)](systemsequancediagram.jpeg){#fig:ssd width="80%"}

## State Transition Diagram: System States

This diagram describes how the system changes its state during
execution. Initially, the system remains in an idle state. When a file
is uploaded, it moves to the uploading state, followed by the analyzing
state. The diagram also includes error states, such as invalid files or
detector failures, and shows how the system either recovers from these
errors or safely returns to the idle state.

![State Transition Diagram of the
System](stateTransitionDiagram.jpg){#fig:state-transition width="80%"}

# Data Design

## Overview

DevSync is a code quality analysis system that transforms uploaded Java
projects into structured analysis reports. The system processes source
code files, detects code smells using twelve specialized detectors, and
stores analysis results in a relational database while maintaining
file-based report storage. This hybrid approach balances query
performance with storage efficiency for large report files.

## Data Architecture

### High-Level Data Flow

The data transformation pipeline processes user uploads through multiple
stages, each refining the data representation:

``` {frame="single" fontsize="\\small"}
User Upload (ZIP/JAR) via React Frontend
        |
        v
Vite Dev Server / Production Build
        |
        v
Axios HTTP Request to Spring Boot Backend
        |
        v
File Extraction & Validation
        |
        v
Java Source Code Parsing (JavaParser AST)
        |
        v
Code Analysis Engine (12 Detectors)
        |
        v
Issue Detection & Scoring
        |
        v
Ollama AI Recommendations (with fallback)
        |
        v
Report Generation (TXT/Visual/PDF)
        |
        v
Database Persistence + File Storage
        |
        v
JSON Response to Frontend
        |
        v
Recharts Visualization & UI Presentation
```

### System Layers

The data architecture spans six distinct layers, each with specific
responsibilities:

1.  **Presentation Layer:** React 18.3.1 + Vite 7.1.7 frontend with
    Radix UI components, Tailwind CSS styling, and Recharts
    visualization. Handles user interaction, data visualization, and
    responsive design across devices.

2.  **Communication Layer:** Axios HTTP client with interceptors for
    authentication, error handling, and request/response transformation.
    Manages REST API communication between frontend and backend.

3.  **Application Layer:** Spring Boot controllers and services manage
    request routing, business orchestration, and transaction boundaries.

4.  **Business Logic Layer:** Code analysis engine with twelve
    specialized detectors implements core analysis algorithms, AST
    traversal, and metric calculation.

5.  **Data Access Layer:** JPA repositories provide abstracted database
    operations with transaction management and query optimization.

6.  **Persistence Layer:** MySQL database and file system storage
    maintain durable data records with proper indexing and access
    control.

## Data Transformation and Processing

### Input Data Transformation

The system processes input data through six sequential stages, each
transforming the data into increasingly refined representations.

#### Stage 1: File Upload Processing

**Input:** Multipart file (ZIP/JAR format, maximum 50MB) uploaded via
React frontend with drag-and-drop support or file picker

**Process:**

-   Frontend validates file type and size before upload

-   Axios sends multipart/form-data request with progress tracking

-   Backend extracts compressed files to a temporary directory

-   Generate a unique folder name using timestamp and UUID

-   Validate project file structure for expected Java project layout

-   Verify file integrity and scan for malformed archives

-   Real-time progress updates sent to frontend via WebSocket or polling

**Output:** Extracted project directory structure with validated
contents and upload confirmation

#### Stage 2: Source Code Parsing

**Input:** Java source files (.java extension)

**Process:**

-   JavaParser generates Abstract Syntax Tree (AST) for each source file

-   CompilationUnit objects created containing parsed syntax structure

-   AST nodes extracted including classes, methods, fields, and
    statements

-   Symbol resolution performed for type reference analysis

**Output:** Structured CompilationUnit objects representing source code

#### Stage 3: Code Analysis

**Input:** CompilationUnit AST objects

**Process:**

-   Twelve detector instances analyze AST in parallel where possible

-   Detector-specific algorithms traverse relevant AST nodes

-   Metrics calculated including LOC, complexity, cohesion, and coupling

-   Threshold comparison identifies violations and generates issues

**Output:** Collection of CodeIssue objects with location and severity

#### Stage 4: Issue Aggregation

**Input:** Raw issue strings from detector components

**Process:**

-   Parse issue format: `[Severity] [Type] File:Line - Message`

-   Extract structured fields into typed objects

-   Calculate severity distribution counts

-   Compute grading metrics based on issue weights

**Output:** Structured analysis results map with aggregated statistics

#### Stage 5: Report Generation

**Input:** Analysis results map with issue data and AI recommendations

**Process:**

-   Format issues into human-readable text with contextual information

-   Generate PlantUML class and sequence diagrams

-   Calculate summary statistics and overall quality grades

-   Create comprehensive report with executive summary

-   Generate PDF version using jsPDF for download capability

-   Prepare JSON response with structured data for frontend
    visualization

**Output:** Text report file, visual diagram images, PDF document, and
JSON data for Recharts visualization

#### Stage 6: Data Persistence and Presentation

**Input:** Analysis results, metadata, and generated reports

**Process:**

-   Map results to JPA entity objects

-   Validate constraints and referential integrity

-   Execute database transactions with rollback support

-   Store report files to designated file system location

-   Send JSON response to frontend via Axios

-   Frontend processes data for Recharts visualization

-   Update UI with analysis results, charts, and downloadable reports

-   Apply theme-aware styling using next-themes

-   Animate transitions using Framer Motion

**Output:** Persisted database records, stored report files, and
interactive dashboard with visualizations

### Data Processing Algorithms

The analysis engine employs several key algorithms for code quality
assessment:

#### Cohesion Index Calculation

``` {frame="single" fontsize="\\small"}
cohesionIndex = usedFields / totalFields
```

This metric measures how comprehensively methods utilize class fields.
Values range from 0.0 (low cohesion, indicating potential god class) to
1.0 (high cohesion, indicating focused responsibility). The system flags
classes with cohesion index below 0.4 as exhibiting broken
modularization.

#### Coupling Count Calculation

``` {frame="single" fontsize="\\small"}
couplingCount = count(unique external dependencies)
```

This metric counts distinct external class references within a class.
High coupling (values greater than 6) indicates excessive dependencies
that reduce maintainability and increase change impact.

#### Cyclomatic Complexity

``` {frame="single" fontsize="\\small"}
complexity = 1 + count(decision_points)
```

Cyclomatic complexity measures the number of independent execution paths
through a method. Decision points include if statements, loops, case
labels, and boolean operators. Methods with complexity above 10 are
flagged as requiring refactoring.

#### Cognitive Complexity

``` {frame="single" fontsize="\\small"}
cognitiveComplexity = sum(nesting_penalties) + sum(structural_penalties)
```

Cognitive complexity measures human comprehension difficulty, accounting
for nesting depth and control flow breaks. Unlike cyclomatic complexity,
it penalizes deeply nested structures more heavily. Values above 15
indicate hard-to-understand code requiring simplification.

#### Issue Density

``` {frame="single" fontsize="\\small"}
issueDensity = totalIssues / (totalLOC / 1000)
```

Issue density normalizes the issue count per thousand lines of code,
enabling fair comparison across projects of different sizes.

#### Grading Algorithm

``` {frame="single" fontsize="\\small"}
score = 100 - (critical * 10 + warning * 5 + suggestion * 2)
```

The grading system assigns letter grades based on weighted issue counts:

-   **A+ (95--100):** Excellent code quality with minimal issues

-   **A (90--94):** Very good quality with few minor issues

-   **B (80--89):** Good quality with some improvement areas

-   **C (70--79):** Acceptable quality requiring attention

-   **D (60--69):** Below average quality with significant issues

-   **F (below 60):** Poor quality requiring major refactoring

## Data Storage

### Database Storage (MySQL)

The system uses MySQL as the primary relational database with the
following configuration:

**Database Name:** `devsyncdb`

The database stores persistent system data including users, settings,
and analysis history. Core tables include:

::: description
User account information including credentials and profile data

Per-user configuration preferences and notification settings

Records of all analysis sessions with summary metrics

Git commit-level analysis results for repository tracking

System-wide configuration parameters
:::

### File System Storage

Report files and uploaded projects are stored in a structured file
system hierarchy:

**Base Directory:** `uploads/`

``` {frame="single" fontsize="\\small"}
uploads/
  +-- {timestamp}/
  |     +-- {project_name}/
  |     +-- report.txt
  |     +-- diagrams/
  |            +-- class_diagram.png
  |            +-- sequence_diagram.png
```

Files are organized using timestamp-based unique folders to prevent
naming collisions. Report file paths are stored in the database and
served through backend controllers with appropriate access control.

### In-Memory Processing

During analysis, temporary data structures are utilized for processing
efficiency:

-   Analysis results map (cleared after report generation to free
    memory)

-   Singleton detector instances (reused across analyses for efficiency)

-   AST objects retained only during the analysis lifecycle

-   Caching of frequently accessed configuration values

## Summary

The DevSync data design implements a robust and scalable architecture
that transforms uploaded source code into structured AST
representations, processes them through twelve configurable detectors,
and stores results using a hybrid database and file-based approach. The
modern React 18.3.1 + Vite 7.1.7 frontend provides an intuitive,
accessible interface with:

-   Radix UI component library for production-ready, accessible
    components

-   Tailwind CSS v4 for efficient, utility-first styling

-   next-themes for seamless dark/light mode switching

-   Recharts for interactive data visualization

-   Framer Motion for smooth animations and transitions

-   jsPDF for client-side PDF generation

-   React Hook Form for efficient form validation

The design supports extensibility through modular detector architecture,
efficient processing through parallel analysis where applicable, and
long-term analysis tracking through persistent storage. The separation
of transactional data (database) from large artifacts (file system)
optimizes both query performance and storage efficiency while
maintaining system maintainability. The frontend-backend separation
enables independent scaling, technology updates, and enhanced user
experience through modern web technologies.

# Human Interface Design

## System Functionality from User Perspective

### Landing Page Experience

Users are greeted with a comprehensive landing page that showcases
DevSync's capabilities through:

#### Hero Section

Prominent call-to-action with clear value proposition - \"Eliminate Java
Code Smells\" with gradient text effects and animated background
elements that create visual engagement without distraction.

#### Feature Showcase

Interactive sections highlighting key capabilities:

-   AST-based code analysis with visual code examples

-   AI-powered recommendations with mock analysis results

-   Multi-dimensional quality assessment with metric explanations

-   Historical tracking capabilities with trend visualization

#### How-to-Use Guide

Step-by-step process visualization:

1.  Sign up and login with visual indicators

2.  Upload project with drag-and-drop demonstration

3.  Receive analysis with sample report preview

4.  Collaborate with team sharing features

#### Theme Switching

Users can toggle between dark and light modes with smooth transitions,
ensuring comfortable viewing in different environments and personal
preferences.

### Authentication Flow

#### Registration Process

Streamlined signup with real-time validation:

-   Username availability checking with immediate feedback

-   Email format validation with clear error messaging

-   Password strength indicators with security requirements

-   Success confirmation with automatic redirection

#### Login Interface

Secure authentication with user-friendly features:

-   Email/password combination with remember me option

-   Clear error messaging for invalid credentials

-   Social login placeholders for future OAuth integration

-   Password recovery options (planned enhancement)

### Main Dashboard Experience

#### Upload Interface

Intuitive file upload with multiple interaction methods:

-   Drag-and-drop zone with visual feedback during hover and drop states

-   Traditional file browser integration with file type filtering

-   Upload progress indication with real-time status updates

-   File validation with clear acceptance criteria (ZIP files only)

#### Analysis Progress

Real-time feedback during processing:

-   Progress indicators showing current analysis stage

-   Estimated completion time based on project size

-   Cancellation option for long-running analyses

-   Error handling with detailed failure explanations

#### Results Visualization

Comprehensive analysis presentation:

-   Severity-based issue categorization with color coding (Critical,
    Warning, Suggestion)

-   Numerical summaries with visual progress bars

-   Detailed analysis summary in formatted text blocks

-   Interactive report viewing with modal dialogs

### Historical Analysis Management

#### History Panel

Chronological analysis tracking:

-   Timeline view of previous analyses with project names and dates

-   Quick metrics overview for each analysis session

-   Filtering and search capabilities for large analysis histories

-   Comparison tools for tracking improvement trends

#### Report Access

Seamless report retrieval and viewing:

-   One-click access to detailed analysis reports

-   Full-screen report viewing with syntax highlighting

-   Download options for offline review and sharing

-   Print-friendly formatting for documentation purposes

### Administrative Interface

#### Admin Dashboard

Comprehensive system management:

-   User account overview with registration statistics

-   System performance metrics with real-time monitoring

-   Analysis volume tracking with usage patterns

-   Administrative controls for user management

#### User Management

Detailed user administration:

-   User account listing with search and filter capabilities

-   Account status management with activation/deactivation controls

-   Usage statistics per user with analysis frequency tracking

-   Security monitoring with login attempt tracking

## Feedback Information Display

### Success Feedback

#### Analysis Completion

Clear success indicators with actionable next steps:

-   Completion notifications with issue count summaries

-   Success animations with visual confirmation

-   Immediate access to results with prominent view buttons

-   Sharing options for team collaboration

#### User Actions

Positive reinforcement for user interactions:

-   Registration success with welcome messaging

-   Login confirmation with personalized greetings

-   File upload success with processing initiation

-   Settings updates with immediate effect confirmation

### Error Handling and Guidance

#### Validation Errors

Helpful error messaging with correction guidance:

-   Form validation with field-specific error indicators

-   File upload errors with format and size requirement explanations

-   Authentication failures with clear resolution steps

-   Network errors with retry mechanisms and offline indicators

#### System Errors

Graceful error handling with user-friendly explanations:

-   Analysis failures with detailed error descriptions and suggested
    solutions

-   Service unavailability notifications with estimated recovery times

-   Data access errors with alternative action suggestions

-   Timeout handling with automatic retry options

### Informational Feedback

#### Process Status

Transparent system state communication:

-   Loading states with descriptive text and progress indicators

-   Queue position for analysis processing during high load

-   System maintenance notifications with scheduled downtime information

-   Feature availability status with alternative options

#### Educational Content

Contextual help and guidance:

-   Tooltips explaining technical terms and metrics

-   Help sections with detailed feature explanations

-   Best practices recommendations integrated into workflows

-   Tutorial overlays for first-time users

## Screen Objects and Actions

### Navigation Objects and Actions

#### Header Navigation Bar

**Objects:** Logo, Theme Toggle Button, Admin Panel Button, Logout
Button

**Actions:**

-   Logo Click: Context-dependent navigation

-   Theme Toggle: Switch between dark and light modes with smooth
    transition animations

-   Admin Panel: Navigate to admin login (if not authenticated) or admin
    dashboard (if authenticated)

-   Logout: Clear user session, display confirmation toast, redirect to
    landing page

#### Sidebar Navigation (Dashboard)

**Objects:** Dashboard Link, New Analysis Link, History Link, Settings
Link

**Actions:**

-   Dashboard: Return to main upload interface, reset any active
    analysis

-   New Analysis: Clear current results, focus on upload area, display
    new analysis prompt

-   History: Open history panel modal, load user's analysis history with
    pagination

-   Settings: Open settings modal with user preferences and
    configuration options

### Upload Interface Objects and Actions

#### File Upload Area

**Objects:** Drag-and-drop Zone, File Browser Button, Selected File
Display, Upload Progress Bar

**Actions:**

-   Drag Over: Highlight drop zone with visual feedback, show acceptance
    indicator

-   File Drop: Validate file type and size, display file name, enable
    analyze button

-   Click to Browse: Open file selection dialog, filter for ZIP files
    only

-   File Selection: Update interface with selected file name, show file
    size and validation status

#### Analysis Control Buttons

**Objects:** Analyze Project Button, Cancel Analysis Button, New
Analysis Button

**Actions:**

-   Analyze Project: Initiate file upload, start analysis pipeline, show
    progress indicators

-   Cancel Analysis: Abort current analysis, clean up temporary files,
    return to upload state

-   New Analysis: Reset interface, clear previous results, prepare for
    new file upload

### Results Display Objects and Actions

#### Metrics Cards

**Objects:** Critical Issues Card, Warnings Card, Suggestions Card

**Actions:**

-   Card Hover: Highlight card with subtle animation, show additional
    context

-   Card Click: Filter detailed results by severity level, expand
    relevant sections

-   Metric Animation: Count-up animation when results are first
    displayed

#### Analysis Summary Panel

**Objects:** Summary Text Area, Show Report Button, Download Button,
Share Button

**Actions:**

-   Show Report: Open full report in modal dialog, format content for
    readability

-   Download Report: Generate downloadable report file, trigger browser
    download

-   Share Results: Generate shareable link, copy to clipboard with
    confirmation

### Report Viewing Objects and Actions

#### Report Modal Dialog

**Objects:** Report Content Area, Close Button, Search Box, Print Button

**Actions:**

-   Content Scroll: Smooth scrolling with syntax highlighting
    preservation

-   Search: Highlight matching text, navigate between search results

-   Print: Format report for printing, open print dialog with optimized
    layout

-   Close: Save scroll position, close modal with fade animation

#### Report Navigation

**Objects:** Section Headers, Line Numbers, Issue Links, AI Analysis
Section

**Actions:**

-   Section Click: Jump to specific report section, update navigation
    state

-   Issue Link: Navigate to source code location, highlight problematic
    code

-   AI Section Toggle: Expand/collapse AI analysis, show/hide
    recommendations

### History Management Objects and Actions

#### History List Interface

**Objects:** History Items, View Report Links, Delete Buttons, Filter
Controls

**Actions:**

-   History Item Click: Expand item details, show analysis summary

-   View Report: Load historical report, open in report modal

-   Delete Analysis: Confirm deletion, remove from history, update
    display

-   Filter/Sort: Apply filters, re-order list, update pagination

#### History Search and Filter

**Objects:** Search Input, Date Range Picker, Project Filter, Sort
Dropdown

**Actions:**

-   Search Input: Real-time filtering, highlight matching results

-   Date Range: Filter by analysis date, update results dynamically

-   Project Filter: Group by project name, show project-specific history

-   Sort Options: Re-order by date, issues count, or project name

### Administrative Interface Objects and Actions

#### User Management Panel

**Objects:** User List Table, Search Box, Action Buttons, Status
Indicators

**Actions:**

-   User Row Click: Expand user details, show analysis statistics

-   Search Users: Filter user list, highlight matching entries

-   Status Toggle: Activate/deactivate user accounts, update status
    indicators

-   View User Activity: Show detailed user analysis history and system
    usage

#### System Monitoring Dashboard

**Objects:** Metrics Cards, Performance Graphs, Alert Indicators, System
Controls

**Actions:**

-   Metrics Refresh: Update real-time statistics, animate value changes

-   Graph Interaction: Zoom into time periods, show detailed metrics

-   Alert Click: Show alert details, provide resolution actions

-   System Controls: Restart services, clear caches, update
    configurations

### Form Objects and Actions

#### Authentication Forms

**Objects:** Input Fields, Submit Buttons, Validation Messages, Social
Login Buttons

**Actions:**

-   Input Focus: Show field requirements, clear previous errors

-   Real-time Validation: Check input format, show validation status

-   Form Submit: Validate all fields, show loading state, handle
    responses

-   Social Login: Redirect to OAuth provider, handle authentication flow

#### Settings Forms

**Objects:** Preference Toggles, Configuration Inputs, Save Button,
Reset Button

**Actions:**

-   Toggle Switch: Update preference immediately, show confirmation

-   Input Change: Mark form as modified, enable save button

-   Save Settings: Validate inputs, update user preferences, show
    success message

-   Reset Form: Restore default values, clear modifications, confirm
    action

This comprehensive interface design ensures intuitive user interactions
while providing powerful functionality for code analysis and system
management. The design emphasizes clarity, feedback, and efficiency to
support productive development workflows.

## User Interface Screens

This section presents the user interface designs for both administrative
and end-user application screens. All interfaces follow consistent
design principles including responsive layouts, accessibility
compliance, and theme support.

### Admin Module Screens

The administrative interface provides system management capabilities for
platform administrators.

![Admin Dashboard---Main control panel providing an overview of system
metrics, recent activities, and quick access to administrative
functions.](adashboard.png){#fig:admin-dashboard width="90%"}

![Admin Projects---Project management interface displaying all uploaded
projects with filtering, sorting, and bulk action
capabilities.](adProjects.png){#fig:admin-projects width="90%"}

![Admin Reports---Analytics and reporting screen showing aggregated code
quality metrics across all projects and
users.](adReports.png){#fig:admin-reports width="90%"}

![Admin Settings---System configuration options including analysis
thresholds, AI service settings, and security
policies.](adSetting.png){#fig:admin-settings width="90%"}

![Admin User Profile---Individual user profile view with account
details, activity history, and administrative
actions.](aduser.png){#fig:admin-user width="90%"}

![Admin Users---User list and management panel with search, filtering,
and role assignment capabilities.](adUsers.png){#fig:admin-users
width="90%"}

### Application Screens

The end-user interface provides code analysis and reporting
functionality for developers.

![GitHub History---Version control activity log showing commit analysis
results and code quality trends over repository
history.](Github.png){#fig:github-history width="90%"}

![Landing Page---Initial application interface presenting platform
features, benefits, and call-to-action
elements.](LandingPage.png){#fig:landing-page width="90%"}

![Registration Page---User account creation form with validation
feedback and terms
acceptance.](RegistrationPage.png){#fig:registration-page width="90%"}

![User Settings---Personal configuration screen for notification
preferences, theme selection, and account
management.](setting.png){#fig:user-settings width="90%"}

![Upload Area---File upload interface with drag-and-drop support,
progress indication, and file validation
feedback.](uploadarea.png){#fig:upload-area width="90%"}

![User Account---Profile and account details page showing usage
statistics and subscription
information.](useraccount.png){#fig:user-account width="90%"}

![Welcome Home Page---User dashboard after login displaying recent
analyses, quick actions, and personalized
recommendations.](WelcomeHomePage.png){#fig:welcome-home width="90%"}

# Implementation

This chapter discusses the implementation details of the DevSync code
quality analysis system. The core modules are presented in pseudocode
form following proper coding standards. The system implements a
multi-detector architecture with AI-assisted analysis and GitHub
integration.

## Web Application Architecture

The DevSync platform is implemented as a full-stack web application with
a clear separation between frontend and backend components. The frontend
is built using React 18.3.1 with Vite 7.1.7 as the build tool, providing
a modern, responsive user interface with hot module replacement during
development. The backend utilizes Spring Boot framework with Java,
offering RESTful API endpoints for all system operations.

### Frontend Implementation

The React-based frontend leverages a component-driven architecture with
functional components and React Hooks for state management. Key
implementation features include:

-   **Component Library:** Radix UI primitives provide accessible,
    unstyled components that are customized using Tailwind CSS utility
    classes for consistent styling across the application.

-   **Styling System:** Tailwind CSS v4.1.16 with PostCSS enables
    utility-first styling with minimal custom CSS, ensuring responsive
    design and theme consistency.

-   **Theme Management:** next-themes library implements seamless
    dark/light mode switching with persistent user preferences stored in
    local storage.

-   **Data Visualization:** Recharts library renders interactive charts
    and graphs for analysis metrics, providing visual insights into code
    quality trends.

-   **Animation Framework:** Framer Motion adds smooth transitions and
    animations throughout the interface, enhancing user experience
    without compromising performance.

-   **Form Handling:** React Hook Form manages form state and validation
    efficiently, reducing re-renders and improving form performance.

-   **HTTP Communication:** Axios v1.12.2 handles all API requests with
    interceptors for authentication token injection and centralized
    error handling.

-   **Routing:** React Router DOM manages client-side routing with
    protected routes for authenticated users and role-based access
    control.

### Backend Implementation

The Spring Boot backend implements a layered architecture following
industry best practices:

-   **Controller Layer:** REST controllers handle HTTP requests, perform
    input validation using Bean Validation annotations, and return
    standardized JSON responses.

-   **Service Layer:** Business logic is encapsulated in service classes
    with transactional boundaries managed by Spring's \@Transactional
    annotation.

-   **Repository Layer:** Spring Data JPA repositories provide database
    abstraction with custom query methods for complex data retrieval
    operations.

-   **Security Layer:** Spring Security with JWT-based authentication
    secures API endpoints, with role-based authorization for
    administrative functions.

-   **Analysis Engine:** Custom analysis engine orchestrates twelve
    specialized detector components, each implementing specific code
    smell detection algorithms.

-   **AI Integration:** Service layer components integrate with Ollama
    AI service using HTTP client with fallback mechanisms for service
    unavailability.

-   **File Management:** Multipart file upload handling with validation,
    extraction to temporary directories, and secure file storage with
    access control.

### Communication Protocol

The frontend and backend communicate through RESTful APIs using JSON
data format. All API endpoints follow REST conventions with appropriate
HTTP methods (GET, POST, PUT, DELETE) and status codes. Authentication
is handled via JWT tokens passed in Authorization headers, with token
refresh mechanisms for extended sessions. File uploads use
multipart/form-data encoding with progress tracking support.

### Deployment Configuration

The application supports both development and production environments.
In development, Vite dev server runs on port 5173 with proxy
configuration for backend API calls to Spring Boot running on port 8080.
Production builds are optimized with code splitting, tree shaking, and
asset minification. The backend can be deployed as a standalone JAR file
or containerized using Docker for scalable deployment.

## Code Analysis Engine

The Code Analysis Engine serves as the central orchestrator for all code
quality detectors. It manages detector lifecycle, configuration, and
result aggregation.

::: algorithm
**Input:** projectPath (string), userSettings (UserSettings object)\
**Output:** analysisResults (Map containing issues, metrics, and
statistics)

::: algorithmic
results $\gets$ empty Map allIssues $\gets$ empty List severityCounts
$\gets$ empty Map detectorCounts $\gets$ empty Map
configureDetectors(userSettings) javaFiles $\gets$
collectJavaFiles(projectPath) totalLOC $\gets$ 0, totalClasses $\gets$
0, totalMethods $\gets$ 0 continue cu $\gets$ parseJavaFile(file)
fileIssues $\gets$ analyzeFile(cu, file.name, detectorCounts)
allIssues.addAll(fileIssues) updateSeverityCounts(fileIssues,
severityCounts) totalLOC $\gets$ totalLOC + countLinesOfCode(cu)
totalClasses $\gets$ totalClasses + countClasses(cu) totalMethods
$\gets$ totalMethods + countMethods(cu) results.put(\"issues\",
allIssues) results.put(\"severityCounts\", severityCounts)
results.put(\"detectorCounts\", detectorCounts)
results.put(\"totalLOC\", totalLOC) results.put(\"totalClasses\",
totalClasses) results.put(\"totalMethods\", totalMethods) results
:::
:::

::: algorithm
**Input:** compilationUnit (AST), fileName (string), detectorCounts
(Map)\
**Output:** issues (List of detected code smells)

::: algorithmic
issues $\gets$ empty List detectorIssues $\gets$
detector.detect(compilationUnit) issues.addAll(detectorIssues)
detectorCounts.increment(detector.name, detectorIssues.size()) issues
:::
:::

## Long Method Detection

The Long Method Detector identifies methods that violate size and
complexity thresholds using multiple metrics including cyclomatic
complexity, cognitive complexity, and nesting depth.

::: algorithm
**Input:** compilationUnit (AST), thresholds (Configuration)\
**Output:** issues (List of long method violations)

::: algorithmic
issues $\gets$ empty List methods $\gets$
extractAllMethods(compilationUnit) info $\gets$ analyzeMethod(method)
score $\gets$ calculateComplexityScore(info) severity $\gets$
mapScoreToSeverity(score) issue $\gets$ formatIssue(severity, info,
generateSuggestions(info)) issues.add(issue) issues
:::
:::

::: algorithm
**Input:** methodInfo (MethodInfo object)\
**Output:** score (double between 0.0 and 1.0)

::: algorithmic
lineScore $\gets$ min(1.0, methodInfo.lineCount / criticalThreshold)
complexityScore $\gets$ min(1.0, methodInfo.cyclomaticComplexity /
maxComplexity) cognitiveScore $\gets$ min(1.0,
methodInfo.cognitiveComplexity / maxCognitive) nestingScore $\gets$
min(1.0, methodInfo.nestingDepth / maxNesting) responsibilityScore
$\gets$ min(1.0, methodInfo.responsibilityCount / 3) methodType $\gets$
determineMethodType(methodInfo) weight $\gets$
getMethodTypeWeight(methodType) score $\gets$ weight $\times$ (lineScore
$\times$ 0.35 + complexityScore $\times$ 0.25 + cognitiveScore $\times$
0.20 + nestingScore $\times$ 0.10 + responsibilityScore $\times$ 0.10)
score
:::
:::

::: algorithm
**Input:** methodDeclaration (AST node)\
**Output:** complexity (integer)

::: algorithmic
complexity $\gets$ 1 complexity $\gets$ complexity +
countNodes(methodDeclaration, IfStmt) complexity $\gets$ complexity +
countNodes(methodDeclaration, ForStmt) complexity $\gets$ complexity +
countNodes(methodDeclaration, WhileStmt) complexity $\gets$ complexity +
countNodes(methodDeclaration, DoStmt) complexity $\gets$ complexity +
countNodes(methodDeclaration, SwitchEntry) complexity $\gets$
complexity + countNodes(methodDeclaration, ConditionalExpr) complexity
$\gets$ complexity + countLogicalOperators(methodDeclaration) complexity
:::
:::

## Code Quality Grading System

The Grading System evaluates overall code quality using
industry-standard metrics and issue density calculations.

::: algorithm
**Input:** severityCounts (Map), totalLOC (integer)\
**Output:** gradeResult (GradeResult object)

::: algorithmic
GradeResult(\"N/A\", 0, 0, \"Cannot grade\") critical $\gets$
severityCounts.get(\"Critical\") high $\gets$
severityCounts.get(\"High\") medium $\gets$
severityCounts.get(\"Medium\") low $\gets$ severityCounts.get(\"Low\")
totalIssues $\gets$ critical + high + medium + low GradeResult(\"A+\",
100.0, 0.0, \"Perfect code quality\") weightedIssues $\gets$ (critical
$\times$ 10.0) + (high $\times$ 5.0) + (medium $\times$ 2.0) + (low
$\times$ 0.5) kloc $\gets$ totalLOC / 1000.0 issueDensity $\gets$
totalIssues / kloc baseScore $\gets$ calculateBaseScore(issueDensity)
finalScore $\gets$ applyPenalties(baseScore, critical, high,
issueDensity) letterGrade $\gets$ mapScoreToGrade(finalScore)
qualityLevel $\gets$ getQualityLevel(letterGrade) recommendation $\gets$
generateRecommendation(letterGrade, critical, high)
GradeResult(letterGrade, finalScore, issueDensity, qualityLevel,
recommendation)
:::
:::

::: algorithm
**Input:** issueDensity (double, issues per KLOC)\
**Output:** score (double between 0 and 100)

::: algorithmic
\- (issueDensity / 0.5) $\times$ 10 ratio $\gets$ (issueDensity - 0.5) /
(2.0 - 0.5) - (ratio $\times$ 10) ratio $\gets$ (issueDensity - 2.0) /
(5.0 - 2.0) - (ratio $\times$ 10) ratio $\gets$ (issueDensity - 5.0) /
(10.0 - 5.0) - (ratio $\times$ 10) max(0, 60 - (issueDensity - 10.0)
$\times$ 2)
:::
:::

## AI-Assisted Code Analysis

The AI Assistant Service integrates with multiple AI providers to
generate intelligent code improvement suggestions.

::: algorithm
**Input:** reportContent (string), userSettings (UserSettings)\
**Output:** aiAnalysis (string)

::: algorithmic
generateFallbackAnalysis(reportContent) provider $\gets$
userSettings.aiProvider analyzeWithOllama(reportContent, userSettings)
generateFallbackAnalysis(reportContent) analyzeWithOpenAI(reportContent,
userSettings) analyzeWithAnthropic(reportContent, userSettings)
generateFallbackAnalysis(reportContent)
:::
:::

::: algorithm
**Input:** reportContent (string), settings (UserSettings)\
**Output:** analysis (string)

::: algorithmic
prompt $\gets$ createPrompt(reportContent) model $\gets$
settings.aiModel OR \"deepseek-coder:latest\" requestBody $\gets$
createJSON(model, prompt) request $\gets$
createHTTPRequest(\"http://localhost:11434/api/chat\", requestBody)
request.setHeader(\"Content-Type\", \"application/json\")
request.setTimeout(120 seconds) response $\gets$
httpClient.send(request) jsonResponse $\gets$ parseJSON(response.body)
content $\gets$ jsonResponse.get(\"message\").get(\"content\") \"=== AI
ANALYSIS (Ollama) ===\\n\" + content throw IOException(\"Ollama request
failed\")
:::
:::

::: algorithm
**Input:** reportContent (string)\
**Output:** prompt (string)

::: algorithmic
\"Provide 3 actionable tips to maintain excellent code quality\"
limitedContent $\gets$ reportContent.substring(0, 3000) prompt $\gets$
\"You are a senior Java code reviewer. Analyze this report:\\n\" prompt
$\gets$ prompt + \"1. Top 3 critical issues needing immediate
attention\\n\" prompt $\gets$ prompt + \"2. Specific refactoring
suggestions with examples\\n\" prompt $\gets$ prompt + \"3. Best
practices to prevent these issues\\n\\n\" prompt $\gets$ prompt +
\"Report:\\n\" + limitedContent prompt
:::
:::

## GitHub Integration

The GitHub Controller manages repository analysis by fetching code from
GitHub, extracting it, and running quality analysis on specific commits.

::: algorithm
**Input:** token (string), owner (string), repo (string), sha (string),
userId (string)\
**Output:** commitAnalysis (CommitAnalysis object)

::: algorithmic
headers $\gets$ createHTTPHeaders() headers.set(\"Authorization\",
\"token \" + token) headers.set(\"User-Agent\", \"DevSync-App\") url
$\gets$ \"https://api.github.com/repos/\" + owner + \"/\" + repo +
\"/zipball/\" + sha response $\gets$ httpClient.GET(url, headers)
extractPath $\gets$ \"uploads/github\_\" + owner + \"\_\" + repo +
\"\_\" + sha.substring(0, 7) createDirectory(extractPath) zipFile
$\gets$ saveToFile(extractPath + \".zip\", response.body) unzip(zipFile,
extractPath) delete(zipFile) analysisResult $\gets$
analysisEngine.analyzeProject(extractPath) severityCounts $\gets$
analysisResult.get(\"severityCounts\") analysis $\gets$ new
CommitAnalysis() analysis.setUserId(userId) analysis.setRepoOwner(owner)
analysis.setRepoName(repo) analysis.setCommitSha(sha)
analysis.setTotalIssues(analysisResult.get(\"totalIssues\"))
analysis.setCriticalIssues(severityCounts.get(\"Critical\"))
analysis.setWarnings(severityCounts.get(\"High\"))
analysis.setReportPath(extractPath)
commitAnalysisRepository.save(analysis) analysis
:::
:::

::: algorithm
**Input:** zipFilePath (string), destDir (string)\
**Output:** None (extracts files to destination)

::: algorithmic
createDirectory(destDir) zipStream $\gets$
openZipInputStream(zipFilePath) entry $\gets$ zipStream.getNextEntry()
file $\gets$ new File(destDir, entry.name) file.mkdirs()
file.parent.mkdirs() outputStream $\gets$ openFileOutputStream(file)
buffer $\gets$ new byte\[1024\] len $\gets$ zipStream.read(buffer)
outputStream.write(buffer, 0, len) outputStream.close()
zipStream.closeEntry() zipStream.close()
:::
:::

## Report Generation

The Report Generator creates comprehensive analysis reports with syntax
highlighting and detailed issue descriptions.

::: algorithm
**Input:** analysisResults (Map), projectPath (string), gradeResult
(GradeResult)\
**Output:** reportPath (string)

::: algorithmic
report $\gets$ new StringBuilder()
report.append(generateHeader(projectPath))
report.append(generateGradeSummary(gradeResult))
report.append(generateMetricsSummary(analysisResults)) issues $\gets$
analysisResults.get(\"issues\") groupedIssues $\gets$
groupIssuesByFile(issues) report.append(\"\\n=== \" + file + \"
===\\n\") fileIssues $\gets$ groupedIssues.get(file)
report.append(formatIssue(issue))
report.append(generateRecommendations(analysisResults)) reportPath
$\gets$ projectPath + \"/report.txt\" writeToFile(reportPath,
report.toString()) reportPath
:::
:::

# Testing & Evaluation

This section presents comprehensive test cases for the DevSync code
quality analysis platform. All tests were manually executed to verify
system functionality, reliability, and correctness across all modules.

## Testing Methodology

The testing approach follows a structured methodology covering multiple
testing levels:

-   **Unit Testing:** Individual component and method validation

-   **Functional Testing:** Feature-level testing with different user
    roles

-   **Business Rules Testing:** Decision table-based validation

-   **Integration Testing:** Module interaction and data flow
    verification

All test cases include Test Case ID, Description, Input values, Expected
Result, and Status (Pass/Fail).

## Unit Testing

Unit tests verify individual components and methods in isolation.

### Authentication Module

**Test ID**   **Description**                **Input**                                                                 **Expected Result**                    **Status**
  ------------- ------------------------------ ------------------------------------------------------------------------- -------------------------------------- ------------
UT-AUTH-001   Valid user registration        username: \"testuser\", email: \"test@mail.com\", password: \"pass123\"   User created, password encrypted       Pass
UT-AUTH-002   Duplicate email registration   Existing email                                                            Error: \"Email already exists\"        Pass
UT-AUTH-003   Empty username                 username: \"\", email: \"test@mail.com\", password: \"pass123\"           Error: \"All fields required\"         Pass
UT-AUTH-004   Short password                 username: \"user\", email: \"test@mail.com\", password: \"12345\"         Error: \"Password must be 6+ chars\"   Pass
UT-AUTH-005   Password encryption            password: \"mypass123\"                                                   BCrypt hash stored, not plaintext      Pass

: Unit Test Cases - User Registration

**Test ID**   **Description**         **Input**                                           **Expected Result**                      **Status**
  ------------- ----------------------- --------------------------------------------------- ---------------------------------------- ------------
UT-AUTH-006   Valid login             email: \"test@mail.com\", password: \"pass123\"     Token generated, user data returned      Pass
UT-AUTH-007   Invalid email           email: \"wrong@mail.com\", password: \"pass123\"    Error: \"Invalid credentials\"           Pass
UT-AUTH-008   Invalid password        email: \"test@mail.com\", password: \"wrongpass\"   Error: \"Invalid credentials\"           Pass
UT-AUTH-009   Empty credentials       email: \"\", password: \"\"                         Error: \"Email and password required\"   Pass
UT-AUTH-010   Password verification   Correct password vs stored hash                     BCrypt match returns true                Pass

: Unit Test Cases - User Login

### File Processing Module

**Test ID**   **Description**        **Input**                      **Expected Result**                   **Status**
  ------------- ---------------------- ------------------------------ ------------------------------------- ------------
UT-FILE-001   Valid ZIP upload       Valid ZIP file, 5MB            File accepted, extraction starts      Pass
UT-FILE-002   Empty file upload      Empty file object              Error: \"No file uploaded\"           Pass
UT-FILE-003   Oversized file         ZIP file 60MB                  Error: \"File too large. Max 50MB\"   Pass
UT-FILE-004   Invalid file type      PDF file                       Error: \"File type not allowed\"      Pass
UT-FILE-005   ZIP extraction         Valid ZIP with Java files      Files extracted to unique folder      Pass
UT-FILE-006   Unique folder naming   Same filename uploaded twice   Two unique folders created            Pass
UT-FILE-007   JAR file upload        Valid JAR file                 File accepted and extracted           Pass

: Unit Test Cases - File Upload

### Code Analysis Engine

**Test ID**   **Description**              **Input**                 **Expected Result**           **Status**
  ------------- ---------------------------- ------------------------- ----------------------------- ------------
UT-DET-001    Method with 150 lines        Method: 150 LOC           Issue detected: Long Method   Pass
UT-DET-002    Method with 50 lines         Method: 50 LOC            No issue detected             Pass
UT-DET-003    High cyclomatic complexity   Method: complexity 15     Issue: High complexity        Pass
UT-DET-004    High cognitive complexity    Method: cognitive 20      Issue: Hard to understand     Pass
UT-DET-005    Deep nesting                 Method: 5 nested levels   Issue: Excessive nesting      Pass

: Unit Test Cases - Long Method Detector

**Test ID**   **Description**           **Input**                       **Expected Result**       **Status**
  ------------- ------------------------- ------------------------------- ------------------------- ------------
UT-DET-006    Hardcoded number          Code: \"if (x \> 100)\"         Issue: Magic number 100   Pass
UT-DET-007    Named constant            Code: \"if (x \> MAX_VALUE)\"   No issue detected         Pass
UT-DET-008    Multiple magic numbers    Code with 5 hardcoded values    5 issues detected         Pass
UT-DET-009    Allowed values (0,1,-1)   Code: \"return 0;\"             No issue detected         Pass

: Unit Test Cases - Magic Number Detector

**Test ID**   **Description**           **Input**                        **Expected Result**        **Status**
  ------------- ------------------------- -------------------------------- -------------------------- ------------
UT-DET-010    Empty catch block         try-catch with empty body        Issue: Empty catch block   Pass
UT-DET-011    Catch with logging        Catch block with log statement   No issue detected          Pass
UT-DET-012    Catch with comment only   Catch with \"// TODO\" comment   Issue: Empty catch block   Pass

: Unit Test Cases - Empty Catch Detector

### Grading System

**Test ID**    **Description**           **Input**                          **Expected Result**         **Status**
  -------------- ------------------------- ---------------------------------- --------------------------- ------------
UT-GRADE-001   Perfect code              0 issues, 1000 LOC                 Grade: A+, Score: 100       Pass
UT-GRADE-002   Low issue density         2 issues, 1000 LOC, density: 2.0   Grade: B, Score: 80-89      Pass
UT-GRADE-003   High issue density        50 issues, 1000 LOC, density: 50   Grade: F, Score \< 60       Pass
UT-GRADE-004   Critical issues penalty   10 critical, 1000 LOC              Severe score reduction      Pass
UT-GRADE-005   Zero LOC handling         0 issues, 0 LOC                    Grade: N/A, message shown   Pass

: Unit Test Cases - Grade Calculation

### AI Integration Module

**Test ID**   **Description**      **Input**                    **Expected Result**            **Status**
  ------------- -------------------- ---------------------------- ------------------------------ ------------
UT-AI-001     Ollama available     AI enabled, Ollama running   AI analysis generated          Pass
UT-AI-002     Ollama unavailable   AI enabled, Ollama offline   Fallback analysis used         Pass
UT-AI-003     AI disabled          AI disabled in settings      No AI analysis attempted       Pass
UT-AI-004     Prompt generation    Report with issues           Structured prompt created      Pass
UT-AI-005     Clean code prompt    Report with 0 issues         Tips for maintaining quality   Pass
UT-AI-006     Timeout handling     Request exceeds 120s         Timeout error, fallback used   Pass

: Unit Test Cases - AI Service

## Functional Testing

Functional tests verify complete features from user perspective.

### User Registration and Login

**Test ID**   **Description**                    **Input**               **Expected Result**                  **Status**
  ------------- ---------------------------------- ----------------------- ------------------------------------ ------------
FT-REG-001    Complete registration flow         Valid user details      Account created, redirect to login   Pass
FT-REG-002    Registration with existing email   Email already in DB     Error shown, form not cleared        Pass
FT-REG-003    Form validation                    Invalid email format    Real-time validation error           Pass
FT-REG-004    Password strength indicator        Weak password entered   Strength indicator shows weak        Pass
FT-REG-005    Successful registration message    Valid registration      Success toast, auto-redirect         Pass

: Functional Test Cases - Registration Flow

**Test ID**    **Description**          **Input**                        **Expected Result**                    **Status**
  -------------- ------------------------ -------------------------------- -------------------------------------- ------------
FT-LOGIN-001   Successful login         Valid credentials                Token stored, redirect to dashboard    Pass
FT-LOGIN-002   Failed login             Invalid credentials              Error message, stay on login page      Pass
FT-LOGIN-003   Session persistence      Login, close browser, reopen     User still logged in                   Pass
FT-LOGIN-004   Logout functionality     Click logout button              Session cleared, redirect to landing   Pass
FT-LOGIN-005   Protected route access   Access dashboard without login   Redirect to login page                 Pass

: Functional Test Cases - Login Flow

### Code Analysis Workflow

**Test ID**   **Description**            **Input**                        **Expected Result**                   **Status**
  ------------- -------------------------- -------------------------------- ------------------------------------- ------------
FT-ANAL-001   Complete analysis flow     Upload valid ZIP                 Analysis complete, report generated   Pass
FT-ANAL-002   Drag and drop upload       Drag ZIP to upload area          File accepted, upload starts          Pass
FT-ANAL-003   Progress indication        Upload large file                Progress bar shows percentage         Pass
FT-ANAL-004   Analysis results display   Analysis completes               Metrics cards show counts             Pass
FT-ANAL-005   Report viewing             Click \"View Report\"            Modal opens with formatted report     Pass
FT-ANAL-006   Report download            Click download button            TXT file downloaded                   Pass
FT-ANAL-007   New analysis               Click \"New Analysis\"           Form reset, ready for new upload      Pass
FT-ANAL-008   Multiple file analysis     Upload 3 projects sequentially   All 3 saved to history                Pass

: Functional Test Cases - File Upload and Analysis

### Analysis History Management

**Test ID**   **Description**          **Input**                 **Expected Result**           **Status**
  ------------- ------------------------ ------------------------- ----------------------------- ------------
FT-HIST-001   View history list        Click history button      List of past analyses shown   Pass
FT-HIST-002   History sorting          Default view              Sorted by date descending     Pass
FT-HIST-003   View historical report   Click report in history   Report content displayed      Pass
FT-HIST-004   History search           Search by project name    Matching results filtered     Pass
FT-HIST-005   Empty history state      New user, no analyses     \"No analyses yet\" message   Pass
FT-HIST-006   History pagination       User with 50+ analyses    Paginated results shown       Pass

: Functional Test Cases - History Features

### GitHub Integration

**Test ID**   **Description**           **Input**                      **Expected Result**                  **Status**
  ------------- ------------------------- ------------------------------ ------------------------------------ ------------
FT-GIT-001    Connect GitHub account    Enter valid token              Repositories list loaded             Pass
FT-GIT-002    Invalid token             Enter invalid token            Error: \"Failed to fetch repos\"     Pass
FT-GIT-003    View repository commits   Select repository              Commit list displayed                Pass
FT-GIT-004    Analyze specific commit   Select commit, click analyze   Analysis runs on commit code         Pass
FT-GIT-005    Commit history tracking   Analyze multiple commits       History shows commit-specific data   Pass
FT-GIT-006    Repository download       Download repo as ZIP           ZIP file downloaded successfully     Pass

: Functional Test Cases - GitHub Features

### Admin Panel Functionality

**Test ID**   **Description**      **Input**              **Expected Result**                **Status**
  ------------- -------------------- ---------------------- ---------------------------------- ------------
FT-ADM-001    Admin login          Admin credentials      Access to admin panel              Pass
FT-ADM-002    Dashboard metrics    View dashboard         Total users, issues displayed      Pass
FT-ADM-003    User management      View users list        All users with details shown       Pass
FT-ADM-004    View user details    Click on user          User profile with analyses shown   Pass
FT-ADM-005    Delete user          Delete user action     User and analyses removed          Pass
FT-ADM-006    System settings      Modify max file size   Setting saved and applied          Pass
FT-ADM-007    Maintenance mode     Enable maintenance     Users see maintenance message      Pass
FT-ADM-008    Reports overview     View all reports       Aggregated report data shown       Pass
FT-ADM-009    Monthly analytics    View monthly chart     Chart shows analysis trends        Pass
FT-ADM-010    Issue distribution   View pie chart         Chart shows severity breakdown     Pass

: Functional Test Cases - Admin Dashboard

### User Settings Management

**Test ID**   **Description**      **Input**                       **Expected Result**                       **Status**
  ------------- -------------------- ------------------------------- ----------------------------------------- ------------
FT-SET-001    Enable AI analysis   Toggle AI enabled               Setting saved, AI used in next analysis   Pass
FT-SET-002    Disable detector     Disable Magic Number detector   Detector not run in analysis              Pass
FT-SET-003    Change AI provider   Select different provider       Provider used in next analysis            Pass
FT-SET-004    Adjust thresholds    Change max method length        New threshold applied                     Pass
FT-SET-005    Reset to defaults    Click reset button              All settings restored to defaults         Pass
FT-SET-006    Theme switching      Toggle dark/light mode          Theme changes immediately                 Pass

: Functional Test Cases - User Settings

## Business Rules Testing

Business rules testing validates decision logic using decision tables.

### File Upload Validation Rules

**Condition**           **T1**   **T2**   **T3**   **T4**   **T5**   **T6**
  ---------------------- -------- -------- -------- -------- -------- --------
File exists               Y        Y        Y        Y        Y        N
File size \<= 50MB        Y        Y        Y        N        Y        \-
File type allowed         Y        Y        N        Y        Y        \-
Maintenance mode          N        Y        N        N        N        \-
**Action**                                                          
Accept file               X                                         
Reject - maintenance               X                                
Reject - file type                          X                       
Reject - file size                                   X              
Reject - no file                                                       X
**Test ID**             BR-01    BR-02    BR-03    BR-04    BR-05    BR-06
**Status**               Pass     Pass     Pass     Pass     Pass     Pass

: Decision Table - File Upload Validation

### Grading Rules

**Condition**             **T1**   **T2**   **T3**   **T4**   **T5**   **T6**
  ------------------------ -------- -------- -------- -------- -------- --------
Issue density \< 0.5        Y        N        N        N        N        N
Issue density \< 2.0        \-       Y        N        N        N        N
Issue density \< 5.0        \-       \-       Y        N        N        N
Issue density \< 10.0       \-       \-       \-       Y        N        N
Issue density \>= 10.0      \-       \-       \-       \-       Y        \-
Total LOC = 0               \-       \-       \-       \-       \-       Y
**Action**                                                            
Grade A (90-100)            X                                         
Grade B (80-89)                      X                                
Grade C (70-79)                               X                       
Grade D (60-69)                                        X              
Grade F (0-59)                                                  X     
Grade N/A                                                                X
**Test ID**               BR-07    BR-08    BR-09    BR-10    BR-11    BR-12
**Status**                 Pass     Pass     Pass     Pass     Pass     Pass

: Decision Table - Grade Assignment

### AI Analysis Rules

**Condition**         **T1**   **T2**   **T3**   **T4**   **T5**
  -------------------- -------- -------- -------- -------- --------
AI enabled (user)       Y        Y        Y        N        Y
AI enabled (admin)      Y        Y        N        Y        Y
Ollama available        Y        N        Y        Y        N
**Action**                                               
Use Ollama AI           X                                
Use fallback                     X                          X
Skip AI analysis                          X        X     
**Test ID**           BR-13    BR-14    BR-15    BR-16    BR-17
**Status**             Pass     Pass     Pass     Pass     Pass

: Decision Table - AI Analysis Execution

### User Access Control Rules

**Condition**         **T1**   **T2**   **T3**   **T4**   **T5**
  -------------------- -------- -------- -------- -------- --------
User logged in          Y        Y        Y        N        N
Is admin                Y        N        N        Y        N
Owns resource           \-       Y        N        \-       \-
**Action**                                               
Grant admin access      X                                
Grant user access                X                       
Deny access                               X                 X
Redirect to login                                  X        X
**Test ID**           BR-18    BR-19    BR-20    BR-21    BR-22
**Status**             Pass     Pass     Pass     Pass     Pass

: Decision Table - Access Control

## Integration Testing

Integration tests verify interactions between modules.

### Frontend-Backend Integration

**Test ID**   **Description**         **Input**                     **Expected Result**            **Status**
  ------------- ----------------------- ----------------------------- ------------------------------ ------------
IT-API-001    Registration API call   POST /api/auth/signup         User created, 200 response     Pass
IT-API-002    Login API call          POST /api/auth/login          Token returned, 200 response   Pass
IT-API-003    File upload API         POST /api/upload with file    Analysis result returned       Pass
IT-API-004    History fetch API       GET /api/upload/history       User history array returned    Pass
IT-API-005    Report fetch API        GET /api/upload/report        Report content returned        Pass
IT-API-006    CORS handling           Request from localhost:5173   CORS headers present           Pass
IT-API-007    Error response format   Invalid request               JSON error with message        Pass
IT-API-008    Token authentication    Request with invalid token    401 Unauthorized               Pass

: Integration Test Cases - API Communication

### Database Integration

**Test ID**   **Description**          **Input**                   **Expected Result**                  **Status**
  ------------- ------------------------ --------------------------- ------------------------------------ ------------
IT-DB-001     User persistence         Save new user               User stored in DB with ID            Pass
IT-DB-002     Analysis history save    Save analysis result        Record created with timestamp        Pass
IT-DB-003     User settings save       Update user settings        Settings persisted correctly         Pass
IT-DB-004     Foreign key constraint   Delete user with analyses   Cascade delete or constraint error   Pass
IT-DB-005     Query by user ID         Fetch user analyses         Correct records returned             Pass
IT-DB-006     Transaction rollback     Error during save           No partial data saved                Pass
IT-DB-007     Concurrent access        Multiple users upload       No data corruption                   Pass
IT-DB-008     Null value handling      Save with null fields       Defaults applied or error            Pass

: Integration Test Cases - Database Operations

### Analysis Engine Integration

**Test ID**   **Description**          **Input**                     **Expected Result**                **Status**
  ------------- ------------------------ ----------------------------- ---------------------------------- ------------
IT-ENG-001    All detectors run        Project with various issues   All detector results aggregated    Pass
IT-ENG-002    Detector configuration   User disables 3 detectors     Only enabled detectors run         Pass
IT-ENG-003    Issue aggregation        Multiple files analyzed       Issues grouped by file             Pass
IT-ENG-004    Severity counting        Mixed severity issues         Correct counts per severity        Pass
IT-ENG-005    LOC calculation          Multi-file project            Total LOC summed correctly         Pass
IT-ENG-006    Grade calculation        Analysis results              Grade computed from metrics        Pass
IT-ENG-007    Report generation        Analysis complete             Report file created                Pass
IT-ENG-008    Parser error handling    Invalid Java file             Error logged, analysis continues   Pass

: Integration Test Cases - Detector Coordination

### AI Service Integration

**Test ID**   **Description**      **Input**               **Expected Result**           **Status**
  ------------- -------------------- ----------------------- ----------------------------- ------------
IT-AI-001     Ollama connection    Send analysis request   Response received             Pass
IT-AI-002     Prompt formatting    Report content          Structured prompt sent        Pass
IT-AI-003     Response parsing     AI response JSON        Content extracted correctly   Pass
IT-AI-004     Timeout handling     Long-running request    Timeout after 120s            Pass
IT-AI-005     Fallback mechanism   Ollama unavailable      Fallback analysis generated   Pass
IT-AI-006     Report appending     AI analysis complete    AI section added to report    Pass

: Integration Test Cases - AI Service Communication

### GitHub Integration

**Test ID**   **Description**          **Input**                 **Expected Result**            **Status**
  ------------- ------------------------ ------------------------- ------------------------------ ------------
IT-GIT-001    Fetch repositories       Valid GitHub token        Repository list returned       Pass
IT-GIT-002    Fetch commits            Repository selected       Commit list returned           Pass
IT-GIT-003    Download repository      Commit SHA provided       ZIP file downloaded            Pass
IT-GIT-004    Extract and analyze      ZIP downloaded            Code extracted and analyzed    Pass
IT-GIT-005    Save commit analysis     Analysis complete         CommitAnalysis record saved    Pass
IT-GIT-006    Commit history query     User and repo specified   Historical analyses returned   Pass
IT-GIT-007    Authentication failure   Invalid token             Error message returned         Pass
IT-GIT-008    Rate limit handling      Excessive requests        Rate limit error handled       Pass

: Integration Test Cases - GitHub API Integration

### File System Integration

**Test ID**   **Description**           **Input**                   **Expected Result**                 **Status**
  ------------- ------------------------- --------------------------- ----------------------------------- ------------
IT-FS-001     Create upload directory   First upload                uploads/ folder created             Pass
IT-FS-002     Extract ZIP file          Valid ZIP uploaded          Files extracted to folder           Pass
IT-FS-003     Write report file         Report generated            TXT file written to disk            Pass
IT-FS-004     Read report file          Report path provided        Content read successfully           Pass
IT-FS-005     Unique folder creation    Same file uploaded twice    Two unique folders exist            Pass
IT-FS-006     Cleanup temp files        Analysis complete           Temporary ZIP deleted               Pass
IT-FS-007     Permission handling       Write to protected folder   Error handled gracefully            Pass
IT-FS-008     Large file handling       45MB ZIP file               Extraction completes successfully   Pass

: Integration Test Cases - File Operations

### End-to-End Integration

**Test ID**   **Description**          **Input**                              **Expected Result**               **Status**
  ------------- ------------------------ -------------------------------------- --------------------------------- ------------
IT-E2E-001    New user complete flow   Register, login, upload, analyze       All steps successful              Pass
IT-E2E-002    Multiple analyses        Upload 3 projects                      All saved to history              Pass
IT-E2E-003    Settings impact          Change settings, analyze               Settings applied correctly        Pass
IT-E2E-004    Admin workflow           Admin login, view users, reports       All admin features work           Pass
IT-E2E-005    GitHub workflow          Connect, select repo, analyze commit   Commit analysis saved             Pass
IT-E2E-006    Report lifecycle         Upload, analyze, view, download        Complete report lifecycle         Pass
IT-E2E-007    Session management       Login, analyze, logout, login          Session handled correctly         Pass
IT-E2E-008    Error recovery           Upload fails, retry                    System recovers, retry succeeds   Pass

: Integration Test Cases - Complete Workflows

## Detector-Specific Testing

Comprehensive testing of all twelve code smell detectors.

### Broken Modularization Detector

**Test ID**   **Description**       **Input**                        **Expected Result**            **Status**
  ------------- --------------------- -------------------------------- ------------------------------ ------------
DT-BM-001     Low cohesion class    Class with cohesion \< 0.4       Issue: Broken Modularization   Pass
DT-BM-002     High coupling class   Class with 8+ dependencies       Issue: High coupling           Pass
DT-BM-003     Well-designed class   Cohesion \> 0.6, coupling \< 5   No issue detected              Pass
DT-BM-004     God class detection   Large class, low cohesion        Critical issue detected        Pass

: Test Cases - Broken Modularization Detection

### Complex Conditional Detector

**Test ID**   **Description**      **Input**                       **Expected Result**          **Status**
  ------------- -------------------- ------------------------------- ---------------------------- ------------
DT-CC-001     Simple condition     if (x \> 0)                     No issue detected            Pass
DT-CC-002     Complex AND/OR       if (a && b \|\| c && d)         Issue: Complex conditional   Pass
DT-CC-003     Nested conditions    Multiple nested if statements   Issue detected               Pass
DT-CC-004     Ternary complexity   Complex ternary expression      Issue: Hard to read          Pass

: Test Cases - Complex Conditional Detection

### Deficient Encapsulation Detector

**Test ID**   **Description**        **Input**                        **Expected Result**              **Status**
  ------------- ---------------------- -------------------------------- -------------------------------- ------------
DT-DE-001     Public fields          Class with public fields         Issue: Deficient encapsulation   Pass
DT-DE-002     Private with getters   Private fields, public getters   No issue detected                Pass
DT-DE-003     Protected fields       Protected fields in class        Issue detected                   Pass
DT-DE-004     Constants allowed      public static final fields       No issue detected                Pass

: Test Cases - Deficient Encapsulation Detection

### Long Parameter List Detector

**Test ID**   **Description**              **Input**                **Expected Result**          **Status**
  ------------- ---------------------------- ------------------------ ---------------------------- ------------
DT-LP-001     Method with 3 params         Normal parameter count   No issue detected            Pass
DT-LP-002     Method with 8 params         Excessive parameters     Issue: Long parameter list   Pass
DT-LP-003     Constructor with 10 params   Constructor overload     Issue detected               Pass
DT-LP-004     Threshold boundary           Exactly 6 parameters     No issue (at threshold)      Pass

: Test Cases - Long Parameter List Detection

### Long Statement and Identifier Detectors

**Test ID**   **Description**        **Input**                  **Expected Result**      **Status**
  ------------- ---------------------- -------------------------- ------------------------ ------------
DT-LS-001     Normal statement       Statement 80 chars         No issue detected        Pass
DT-LS-002     Very long statement    Statement 200 chars        Issue: Long statement    Pass
DT-LI-001     Normal variable name   \"userName\" (8 chars)     No issue detected        Pass
DT-LI-002     Very long name         50+ character identifier   Issue: Long identifier   Pass

: Test Cases - Long Statement Detection

### Missing Default and Unnecessary Abstraction Detectors

**Test ID**   **Description**          **Input**                   **Expected Result**              **Status**
  ------------- ------------------------ --------------------------- -------------------------------- ------------
DT-MD-001     Switch with default      Complete switch statement   No issue detected                Pass
DT-MD-002     Switch without default   Missing default case        Issue: Missing default           Pass
DT-UA-001     Interface with 1 impl    Single implementation       Issue: Unnecessary abstraction   Pass
DT-UA-002     Interface with 3 impls   Multiple implementations    No issue detected                Pass

: Test Cases - Missing Default and Unnecessary Abstraction

### Memory Leak Detector

**Test ID**   **Description**            **Input**                    **Expected Result**     **Status**
  ------------- -------------------------- ---------------------------- ----------------------- ------------
DT-ML-001     Unclosed stream            FileInputStream not closed   Issue: Resource leak    Pass
DT-ML-002     Try-with-resources         Proper resource management   No issue detected       Pass
DT-ML-003     Static collection growth   Static list keeps growing    Issue: Memory leak      Pass
DT-ML-004     Listener not removed       Event listener registered    Issue: Potential leak   Pass

: Test Cases - Memory Leak Detection

## Performance and Load Testing

**Test ID**   **Description**              **Input**                       **Expected Result**         **Status**
  ------------- ---------------------------- ------------------------------- --------------------------- ------------
PT-001        Small project analysis       10 Java files, 1000 LOC         Complete in \< 5 seconds    Pass
PT-002        Medium project analysis      50 files, 5000 LOC              Complete in \< 30 seconds   Pass
PT-003        Large project analysis       200 files, 20000 LOC            Complete in \< 2 minutes    Pass
PT-004        Concurrent uploads           5 users upload simultaneously   All complete successfully   Pass
PT-005        Database query performance   Fetch 100 history records       Response in \< 1 second     Pass
PT-006        Report generation speed      Generate 50-page report         Complete in \< 3 seconds    Pass
PT-007        AI analysis timeout          AI request exceeds limit        Timeout at 120 seconds      Pass
PT-008        Memory usage                 Analyze large project           Memory stays under 2GB      Pass

: Performance Test Cases

## Security Testing

**Test ID**   **Description**         **Input**                     **Expected Result**             **Status**
  ------------- ----------------------- ----------------------------- ------------------------------- ------------
ST-001        Password encryption     Store user password           BCrypt hash stored              Pass
ST-002        SQL injection attempt   Malicious input in login      Input sanitized, no injection   Pass
ST-003        XSS prevention          Script in username            Script escaped in output        Pass
ST-004        Unauthorized access     Access report without login   Redirect to login               Pass
ST-005        CSRF protection         Cross-site request            Request rejected                Pass
ST-006        File path traversal     Upload with ../ in name       Path sanitized                  Pass
ST-007        Token validation        Use expired token             401 Unauthorized                Pass
ST-008        Admin privilege check   User access admin endpoint    403 Forbidden                   Pass

: Security Test Cases

## Usability Testing

**Test ID**   **Description**            **Input**                  **Expected Result**                **Status**
  ------------- -------------------------- -------------------------- ---------------------------------- ------------
UT-UI-001     Responsive design          View on mobile device      Layout adapts correctly            Pass
UT-UI-002     Dark mode toggle           Switch theme               Smooth transition, colors change   Pass
UT-UI-003     Error message clarity      Trigger validation error   Clear, helpful message shown       Pass
UT-UI-004     Loading indicators         Start analysis             Progress shown throughout          Pass
UT-UI-005     Navigation intuitiveness   New user explores UI       All features discoverable          Pass
UT-UI-006     Form validation feedback   Enter invalid data         Real-time feedback provided        Pass
UT-UI-007     Accessibility compliance   Use screen reader          All elements accessible            Pass
UT-UI-008     Button states              Hover, click, disable      Visual feedback clear              Pass

: Usability Test Cases

## Test Summary

### Overall Test Results

**Test Category**         **Total Tests**   **Passed**   **Failed**   **Pass Rate**
  ------------------------ ----------------- ------------ ------------ ---------------
Unit Testing                    45              45           0            100%
Functional Testing              52              52           0            100%
Business Rules Testing          22              22           0            100%
Integration Testing             48              48           0            100%
Detector Testing                32              32           0            100%
Performance Testing              8              8            0            100%
Security Testing                 8              8            0            100%
Usability Testing                8              8            0            100%
**Total**                     **223**        **223**       **0**        **100%**

: Test Summary by Category

### Test Coverage Analysis

The comprehensive test suite covers:

-   **All 12 Code Smell Detectors:** Each detector tested with multiple
    scenarios

-   **Complete User Workflows:** Registration, login, upload, analysis,
    history

-   **Admin Functionality:** User management, system settings, analytics

-   **GitHub Integration:** Repository connection, commit analysis,
    history tracking

-   **AI Integration:** Multiple providers, fallback mechanisms, error
    handling

-   **Database Operations:** CRUD operations, transactions, constraints

-   **File System Operations:** Upload, extraction, storage, retrieval

-   **Security Mechanisms:** Authentication, authorization, input
    validation

-   **Performance Characteristics:** Response times, concurrent access,
    resource usage

-   **User Interface:** Responsiveness, accessibility, theme support

### Conclusion

All 223 test cases passed successfully, demonstrating that the DevSync
platform meets its functional, non-functional, and quality requirements.
The system handles normal operations, edge cases, and error conditions
appropriately. Manual testing confirmed that all modules integrate
correctly and the complete workflows function as designed.

# System Architecture Diagram

This appendix provides the detailed box-and-line diagram referenced in
Section 3.3.2, illustrating the complete system architecture and module
relationships.

## High-Level Architecture

![System Architecture Diagram](BoxAndLine.jpg){#fig:system_arch
width="80%"}

## Data Flow Diagram

    User Upload → File Validation → ZIP Extraction → Java File Collection
         ↓
    AST Parsing (JavaParser) → Detector Execution (Parallel) → Issue Aggregation
         ↓
    Grading Calculation → AI Analysis (Ollama) → Report Generation
         ↓
    Database Persistence ← → File System Storage → User Dashboard Display

# Technology Stack and Dependencies

This appendix details all technologies, frameworks, libraries, and
dependencies used in the DevSync platform.

## Backend Technologies

### Core Framework

**Technology**    **Version**   **Purpose**
  ----------------- ------------- ----------------------------------
Java              21            Primary programming language
Spring Boot       3.5.6         Application framework
Spring Boot Web   3.5.6         RESTful API development
Spring Boot JPA   3.5.6         Database abstraction layer
Spring Security   3.5.6         Authentication and authorization
Maven             3.11.0        Build and dependency management

: Backend Core Technologies

### Database and Persistence

**Technology**        **Version**   **Purpose**
  --------------------- ------------- ---------------------
MySQL                 8.0.33        Relational database
Hibernate (via JPA)   Included      ORM framework
MySQL Connector       8.0.33        JDBC driver

: Database Technologies

### Code Analysis Libraries

**Library**        **Version**   **Purpose**
  ------------------ ------------- -------------------------------
JavaParser         3.25.9        AST parsing and code analysis
PlantUML           1.2023.12     Diagram generation
iText7             8.0.2         PDF generation
Jackson Databind   2.15.2        JSON processing

: Analysis and Processing Libraries

## Frontend Technologies

### Core Framework

**Technology**     **Version**   **Purpose**
  ------------------ ------------- ---------------------------
React              18.3.1        UI library
React DOM          18.3.1        DOM rendering
Vite               7.1.7         Build tool and dev server
React Router DOM   7.9.4         Client-side routing

: Frontend Core Technologies

### UI Component Libraries

**Component**     **Version**
  ----------------- -------------
Accordion         1.2.3
Alert Dialog      1.1.6
Avatar            1.1.3
Checkbox          1.1.4
Dialog            1.1.6
Dropdown Menu     2.1.6
Navigation Menu   1.2.5
Popover           1.1.6
Progress          1.1.2
Radio Group       1.2.3
Scroll Area       1.2.3
Select            2.1.6
Slider            1.2.3
Switch            1.1.3
Tabs              1.1.3
Toggle            1.1.2
Tooltip           1.1.8

: UI Component Libraries (Radix UI)

### Styling and Design

**Technology**             **Version**   **Purpose**
  -------------------------- ------------- ------------------------------
Tailwind CSS               4.1.16        Utility-first CSS framework
PostCSS                    8.5.6         CSS processing
Autoprefixer               10.4.21       CSS vendor prefixing
class-variance-authority   0.7.1         Component variant management
tailwind-merge             Latest        Class name optimization
clsx                       Latest        Conditional class names

: Styling Technologies

### Data Visualization and Animation

**Library**     **Version**   **Purpose**
  --------------- ------------- -------------------------------
Recharts        2.15.2        Chart and graph visualization
Framer Motion   12.23.24      Animation library
Lucide React    0.487.0       Icon library
React Icons     5.5.0         Additional icons

: Visualization and Animation Libraries

### Form and State Management

**Library**       **Version**   **Purpose**
  ----------------- ------------- --------------------------------
React Hook Form   7.55.0        Form validation and management
Axios             1.12.2        HTTP client
next-themes       0.4.6         Theme management

: Form and State Management

### Additional Frontend Libraries

**Library**                **Version**   **Purpose**
  -------------------------- ------------- ----------------------------
jsPDF                      2.5.1         Client-side PDF generation
react-syntax-highlighter   16.1.0        Code syntax highlighting
embla-carousel-react       8.6.0         Carousel component
sonner                     2.0.3         Toast notifications
cmdk                       1.1.1         Command menu
vaul                       1.1.2         Drawer component

: Additional Frontend Libraries

## Development Tools

**Tool**                **Version**   **Purpose**
  ----------------------- ------------- ------------------------
ESLint                  9.36.0        JavaScript linting
TypeScript Types        Latest        Type definitions
Vite Plugin React       5.0.4         React support for Vite
Maven Compiler Plugin   3.11.0        Java compilation

: Development and Build Tools

## External Services

**Service**   **Endpoint**      **Purpose**
  ------------- ----------------- ------------------------------
Ollama AI     localhost:11434   AI-powered code analysis
GitHub API    api.github.com    Repository and commit access

: External Service Integrations

## System Requirements

### Server Requirements

-   **Operating System:** Windows, Linux, or macOS

-   **Java Runtime:** JDK 21 or higher

-   **Memory:** Minimum 2GB RAM, Recommended 4GB+

-   **Storage:** 500MB for application, additional space for uploads

-   **Database:** MySQL 8.0 or higher

### Client Requirements

-   **Browser:** Modern browser (Chrome 90+, Firefox 88+, Safari 14+,
    Edge 90+)

-   **JavaScript:** Enabled

-   **Screen Resolution:** Minimum 1024x768, Optimized for 1920x1080

-   **Internet Connection:** Required for API communication

# Database Schema

This appendix provides the complete database schema for the DevSync
platform.

## Entity Relationship Overview

![System Architecture Diagram](erdofsystem.png){#fig:architecture
width="80%"}

## Sample Queries

### Retrieve User Analysis History

    SELECT * FROM analysis_history
    WHERE user_id = ?
    ORDER BY analysis_date DESC
    LIMIT 10;

### Calculate Monthly Analysis Count

    SELECT DATE_FORMAT(analysis_date, '%Y-%m') as month,
           COUNT(*) as analyses
    FROM analysis_history
    GROUP BY month
    ORDER BY month DESC;

### Get Issue Distribution

    SELECT SUM(critical_issues) as critical,
           SUM(warnings) as warnings,
           SUM(suggestions) as suggestions
    FROM analysis_history;

# API Endpoints Reference

This appendix documents all REST API endpoints available in the DevSync
platform.

## Authentication Endpoints

**Endpoint**                **Method**   **Description**
  --------------------------- ------------ ------------------------------------
/api/auth/signup            POST         Register new user account
/api/auth/login             POST         Authenticate user and return token
/api/auth/users             GET          Get all users (admin only)
/api/auth/profile/:userId   GET          Get user profile information

: Authentication API Endpoints

### POST /api/auth/signup

**Request Body:**

    {
      "username": "string",
      "email": "string",
      "password": "string"
    }

**Response (200 OK):**

    "User registered successfully"

### POST /api/auth/login

**Request Body:**

    {
      "email": "string",
      "password": "string"
    }

**Response (200 OK):**

    {
      "message": "Login successful",
      "userId": "string",
      "username": "string",
      "token": "string"
    }

## Code Analysis Endpoints

**Endpoint**             **Method**   **Description**
  ------------------------ ------------ -----------------------------
/api/upload              POST         Upload and analyze project
/api/upload/report       GET          Retrieve analysis report
/api/upload/history      GET          Get user's analysis history
/api/upload/visual       POST         Generate visual report
/api/upload/fix-counts   POST         Fix report issue counts

: Code Analysis API Endpoints

### POST /api/upload

**Request (multipart/form-data):**

    file: [ZIP/JAR file]
    userId: "string"

**Response (200 OK):**

    "✅ Advanced Analysis Complete!
    �� Extracted to: uploads/[folder]
    �� Java files: [count]
    �� Lines of Code: [count]
    �� Report: [filename]
    �� Issues detected: [count]
    �� Grade: [grade] ([score]%)
    �� Issue Density: [density] issues/KLOC
    ⭐ Quality: [level]
    �� AI analysis: [status]
    �� Report path: [path]"

### GET /api/upload/report

**Query Parameters:**

    path: "string" (report file path)
    userId: "string"

**Response (200 OK):**

    [Report content as text]

## GitHub Integration Endpoints

**Endpoint**                 **Method**   **Description**
  ---------------------------- ------------ ------------------------------
/api/github/test             GET          Test GitHub API connectivity
/api/github/repos            POST         Get user's repositories
/api/github/commits          POST         Get repository commits
/api/github/download         POST         Download repository
/api/github/analyze-commit   POST         Analyze specific commit
/api/github/commit-history   GET          Get commit analysis history

: GitHub API Endpoints

### POST /api/github/repos

**Request Body:**

    {
      "token": "string"
    }

**Response (200 OK):**

    [
      {
        "name": "string",
        "full_name": "string",
        "owner": { ... },
        "updated_at": "timestamp",
        ...
      }
    ]

### POST /api/github/analyze-commit

**Request Body:**

    {
      "token": "string",
      "owner": "string",
      "repo": "string",
      "sha": "string",
      "userId": "string",
      "commitMessage": "string",
      "commitDate": "timestamp"
    }

**Response (200 OK):**

    {
      "id": "number",
      "userId": "string",
      "repoOwner": "string",
      "repoName": "string",
      "commitSha": "string",
      "totalIssues": "number",
      "criticalIssues": "number",
      "warnings": "number",
      "suggestions": "number",
      "reportPath": "string",
      "analysisDate": "timestamp"
    }

## Admin Endpoints

**Endpoint**               **Method**   **Description**
  -------------------------- ------------ -----------------------------
/api/admin/dashboard       GET          Get dashboard statistics
/api/admin/users           GET          Get all users
/api/admin/users/:userId   GET          Get user details
/api/admin/users/:userId   PUT          Update user
/api/admin/users/:userId   DELETE       Delete user
/api/admin/projects        GET          Get all projects
/api/admin/reports         GET          Get all reports
/api/admin/settings        GET          Get admin settings
/api/admin/settings        POST         Save admin settings
/api/admin/settings/init   POST         Initialize default settings
/api/admin/fix-counts      POST         Fix report counts

: Admin API Endpoints

### GET /api/admin/dashboard

**Response (200 OK):**

    {
      "totalUsers": "number",
      "totalIssues": "number",
      "aiAnalysisCount": "number",
      "criticalIssues": "number",
      "warningIssues": "number",
      "suggestionIssues": "number",
      "cleanFiles": "number"
    }

## Settings Endpoints

**Endpoint**            **Method**   **Description**
  ----------------------- ------------ --------------------
/api/settings/:userId   GET          Get user settings
/api/settings/:userId   POST         Save user settings

: Settings API Endpoints

## Error Responses

**Status Code**   **Meaning**             **Example Response**
  ----------------- ----------------------- ------------------------------
400               Bad Request             \"Invalid input data\"
401               Unauthorized            \"Authentication required\"
403               Forbidden               \"Access denied\"
404               Not Found               \"Resource not found\"
500               Internal Server Error   \"Server error occurred\"
503               Service Unavailable     \"System under maintenance\"

: Common Error Responses

## CORS Configuration

All endpoints support CORS with the following configuration:

    Allowed Origins: http://localhost:5173, * (configurable)
    Allowed Methods: GET, POST, PUT, DELETE, OPTIONS
    Allowed Headers: Content-Type, Authorization

# Code Smell Detection Rules

This appendix provides detailed detection rules and thresholds for all
twelve code smell detectors.

## Long Method Detector

### Detection Criteria

**Metric**              **Threshold**   **Severity**
  ----------------------- --------------- --------------
Lines of Code (LOC)     \> 100          Critical
Cyclomatic Complexity   \> 10           High
Cognitive Complexity    \> 15           High
Nesting Depth           \> 4            Medium

: Long Method Detection Thresholds

### Calculation Formulas

**Cyclomatic Complexity:**

    complexity = 1 + count(if) + count(for) + count(while)
               + count(case) + count(&&) + count(||)

**Cognitive Complexity:**

    cognitive = sum(nesting_penalties) + sum(structural_penalties)
    where nesting_penalty = nesting_level for each control structure

## Magic Number Detector

### Detection Rules

**Rule**             **Description**
  -------------------- --------------------------------------
Hardcoded literals   Numeric literals not in constants
Allowed values       0, 1, -1 (common programming idioms)
Context exceptions   Array indices, loop counters

: Magic Number Detection Rules

## Empty Catch Block Detector

### Detection Criteria

-   Catch block with no statements

-   Catch block with only comments

-   Catch block with only TODO markers

## Broken Modularization Detector

### Cohesion Metrics

**Metric**       **Threshold**   **Interpretation**
  ---------------- --------------- --------------------------
Cohesion Index   \< 0.4          Low cohesion (God Class)
Cohesion Index   0.4 - 0.6       Moderate cohesion
Cohesion Index   \> 0.6          High cohesion (Good)

: Cohesion Thresholds

**Cohesion Formula:**

    cohesionIndex = usedFields / totalFields
    where usedFields = unique fields accessed by methods

### Coupling Metrics

**Dependencies**   **Level**           **Action**
  ------------------ ------------------- ------------
\< 5               Low coupling        Acceptable
5 - 7              Moderate coupling   Review
\> 7               High coupling       Refactor

: Coupling Thresholds

## Complex Conditional Detector

### Detection Rules

**Condition**                           **Threshold**
  --------------------------------------- ---------------
Logical operators in single condition   \> 3
Nested if statements                    \> 3 levels
Ternary operator complexity             \> 2 nested

: Complex Conditional Thresholds

## Deficient Encapsulation Detector

### Detection Rules

-   Public non-final fields

-   Protected fields (except in inheritance hierarchies)

-   Package-private fields without justification

-   Exceptions: public static final constants

## Long Parameter List Detector

### Thresholds

**Parameter Count**   **Severity**   **Recommendation**
  --------------------- -------------- ---------------------------
\<= 3                 None           Acceptable
4 - 6                 Low            Consider parameter object
7 - 9                 Medium         Refactor recommended
\>= 10                High           Refactor required

: Parameter List Thresholds

## Long Statement Detector

### Detection Criteria

**Characters**   **Action**
  ---------------- ------------
\<= 120          Acceptable
121 - 150        Warning
\> 150           Critical

: Statement Length Thresholds

## Long Identifier Detector

### Naming Thresholds

**Identifier Type**   **Max Length**   **Recommendation**
  --------------------- ---------------- --------------------
Variable              30 characters    Use abbreviations
Method                40 characters    Simplify name
Class                 35 characters    Reconsider design

: Identifier Length Thresholds

## Missing Default Detector

### Detection Rules

-   Switch statements without default case

-   Enum switches missing cases

-   Exception: Complete enum coverage

## Unnecessary Abstraction Detector

### Detection Criteria

**Pattern**                         **Issue**
  ----------------------------------- -------------------------------
Interface with 1 implementation     Unnecessary abstraction
Abstract class with no subclasses   Unused abstraction
Single-method interface             Consider functional interface

: Abstraction Detection Rules

## Memory Leak Detector

### Detection Patterns

**Pattern**              **Description**
  ------------------------ ---------------------------------
Unclosed resources       Streams, connections not closed
Static collections       Growing static lists/maps
Event listeners          Registered but not removed
Thread locals            Not cleaned up
Inner class references   Implicit outer class reference

: Memory Leak Patterns

## Severity Classification

**Severity**   **Description**
  -------------- ------------------------------------------------------------------------------------------
Critical       Severe issues requiring immediate attention (security, memory leaks, major design flaws)
High           Important issues affecting maintainability (complex methods, high coupling)
Medium         Moderate issues affecting code quality (long parameters, missing defaults)
Low            Minor issues and suggestions (naming conventions, minor improvements)

: Issue Severity Levels

## Grading Scale

**Grade**   **Score**   **Issue Density**      **Quality Level**
  ----------- ----------- ---------------------- -------------------
A+          95-100      \< 0.5 issues/KLOC     Excellent
A           90-94       0.5-1.0 issues/KLOC    Very Good
B           80-89       1.0-2.0 issues/KLOC    Good
C           70-79       2.0-5.0 issues/KLOC    Acceptable
D           60-69       5.0-10.0 issues/KLOC   Below Average
F           0-59        \> 10.0 issues/KLOC    Poor

: Code Quality Grading Scale

# Installation and Deployment Guide

This appendix provides step-by-step instructions for installing,
configuring, and deploying the DevSync platform.

## Prerequisites

### Required Software

**Software**   **Version**      **Purpose**
  -------------- ---------------- --------------------------
JDK            21 or higher     Java runtime environment
Node.js        18.x or higher   Frontend build tools
MySQL          8.0 or higher    Database server
Maven          3.8 or higher    Backend build tool
Git            Latest           Version control

: Required Software Components

### Optional Software

**Software**   **Version**   **Purpose**
  -------------- ------------- --------------------------
Ollama         Latest        AI-powered analysis
Docker         Latest        Containerized deployment

: Optional Software Components

## Backend Installation

### Step 1: Clone Repository

    git clone https://github.com/your-repo/devsync.git
    cd devsync

### Step 2: Configure Database

Create MySQL database:

    mysql -u root -p
    CREATE DATABASE devsyncdb;
    CREATE USER 'devsync'@'localhost' IDENTIFIED BY 'password';
    GRANT ALL PRIVILEGES ON devsyncdb.* TO 'devsync'@'localhost';
    FLUSH PRIVILEGES;
    EXIT;

### Step 3: Configure Application Properties

Edit `src/main/resources/application.properties`:

    # Database Configuration
    spring.datasource.url=jdbc:mysql://localhost:3306/devsyncdb
    spring.datasource.username=devsync
    spring.datasource.password=password
    spring.jpa.hibernate.ddl-auto=update

    # Server Configuration
    server.port=8080

    # File Upload Configuration
    spring.servlet.multipart.max-file-size=50MB
    spring.servlet.multipart.max-request-size=50MB

    # Security Configuration
    spring.security.user.name=admin
    spring.security.user.password=admin123

### Step 4: Build Backend

    mvn clean install

### Step 5: Run Backend

    mvn spring-boot:run

Or run the JAR file:

    java -jar target/devsync-0.0.1-SNAPSHOT.jar

## Frontend Installation

### Step 1: Navigate to Frontend Directory

    cd frontend

### Step 2: Install Dependencies

    npm install

### Step 3: Configure Environment

Create `.env` file:

    VITE_API_URL=http://localhost:8080
    VITE_APP_NAME=DevSync

### Step 4: Run Development Server

    npm run dev

Access at: `http://localhost:5173`

### Step 5: Build for Production

    npm run build

Production files will be in `dist/` directory.

## Ollama AI Setup (Optional)

### Step 1: Install Ollama

Download from: `https://ollama.ai`

### Step 2: Pull AI Model

    ollama pull deepseek-coder:latest

### Step 3: Start Ollama Service

    ollama serve

Service runs on: `http://localhost:11434`
