# Rule: Generating an iOS Task List from a PRD (Swift, SwiftUI & SwiftData)

## Input
Use: $ARGUMENTS

## Goal

To guide an AI assistant in creating a detailed, step-by-step task list in Markdown format based on an existing Product Requirements Document (PRD). The task list should guide an iOS developer through implementation using Swift, SwiftUI, and SwiftData, where Views (Screens) interact directly with the data layer.

## Output

- **Format:** Markdown (`.md`)
- **Location:** `/specs/` (relative to the project root)
- **Filename:** `[YYMMDD]-tasks-[prd-file-name].md` (e.g., `250527-tasks-prd-user-profile-editing.md`)

## Process

1.  **Receive PRD Reference:** The user points the AI to a specific PRD file.
2.  **Analyze PRD:** The AI reads and analyzes the functional requirements, user stories, UI/UX specifications, and other sections of the specified PRD.
3.  **Phase 1: Generate Parent Tasks:** Based on the PRD analysis, create the file and generate the main, high-level tasks required to implement the feature. Use your judgement on how many high-level tasks to use. It's likely to be about 4-6, focusing on distinct areas like UI (Screens), data models (SwiftData), business logic within screens or helpers, and testing setup. Present these tasks to the user in the specified format (without sub-tasks yet). Inform the user: "I have generated the high-level tasks based on the PRD. Ready to generate the sub-tasks? Respond with 'Go' to proceed."
4.  **Wait for Confirmation:** Pause and wait for the user to respond with "Go".
5.  **Phase 2: Generate Sub-Tasks:** Once the user confirms, break down each parent task into smaller, actionable sub-tasks necessary to complete the parent task. Ensure sub-tasks logically follow from the parent task and cover the implementation details implied by the PRD (e.g., creating specific SwiftUI Screens, SwiftData models, functions within Screens for data manipulation, and their corresponding tests).
6.  **Identify Relevant Files:** Based on the tasks and PRD, identify potential Swift files that will need to be created or modified. List these under the `Relevant Files` section, including corresponding test files. The AI should attempt to identify the project's test folder (e.g., `YourAppTests`, or a custom folder like `Lines Tests` if evident) and infer paths based on existing project structure.
7.  **Generate Final Output:** Combine the parent tasks, sub-tasks, relevant files, and notes into the final Markdown structure.
8.  **Save Task List:** Save the generated document in the `/specs/` directory with the filename `[YYMMDD]-tasks-[prd-file-name].md`, where `[prd-file-name]` matches the base name of the input PRD file.

## Output Format

The generated task list _must_ follow this structure:

```markdown
## Relevant Files

The AI should list the types of files expected to be created or modified, along with their general purpose. Specific paths should be inferred based on the project's structure. Examples include:

- **SwiftUI Screen(s):** e.g., `[ScreenName]View.swift` or `[FeatureName]Screen.swift` - For UI presentation and direct SwiftData interaction/logic.
- **Screen Test(s):** e.g., `[ScreenName]ViewTests.swift` - Swift Testing tests for the UI Screen(s), including logic contained within.
- **SwiftData Model(s):** e.g., `[DataModelName].swift` - For representing data structures managed by SwiftData.
- **Model Test(s):** e.g., `[DataModelName]Tests.swift` - Swift Testing tests for Model(s), if applicable (e.g., for custom initializers, methods, validation logic not handled by SwiftData constraints).
- **Service/Manager Class(es) (if any):** e.g., `NetworkService.swift`, `AnalyticsManager.swift` - For handling tasks like networking or other non-UI, non-SwiftData specific logic.
- **Service/Manager Test(s) (if any):** e.g., `NetworkServiceTests.swift` - Swift Testing tests for Service/Manager classes.
- **Utility/Helper Files:** As needed for shared functionality.
- **Utility/Helper Test(s):** Tests for any utility/helper functions.

*(Note: The AI should attempt to determine the actual project source folder (e.g., `YourApp/Screens/`) and the test folder (e.g., `YourAppTests` or a custom one like `Lines Tests`) and list file paths accordingly. The examples above are illustrative of file *types* and naming conventions.)*

### Notes

- **Testing Framework:** Utilize the **Swift Testing** framework for all new unit and integration tests.
- **Test File Location:**
    - New test files (e.g., `MyScreenTests.swift`) should generally be placed within the project's primary test target folder. This folder is often named by appending "Tests" to the project name (e.g., `YourProjectNameTests`).
    - The AI should try to infer this location by looking for existing test files or folders ending in "Tests".
    - If a project uses a custom test folder structure (e.g., a root folder named `Lines Tests`), that structure should be followed.
    - Consider mirroring the source file's module or feature directory structure within the identified test folder for better organization (e.g., `YourAppTests/Screens/MyScreenTests.swift`).
- **Running Tests (Command Line):**
    - Use `xcodebuild` for automated testing scenarios. For example:
      `xcodebuild test -project YourApp.xcodeproj -scheme YourAppScheme -destination 'platform=iOS Simulator,name=iPhone 15 Pro,OS=latest'`
      (Replace `YourApp.xcodeproj`, `YourAppScheme`, simulator name, and OS version as appropriate for your project.)
- **Test Coverage:** Aim for comprehensive test coverage for new logic, including UI components/Screens (especially interaction logic and SwiftData operations triggered from the screen), SwiftData models (if they contain custom logic), and any services or utility functions.
- **Swift Testing Features:** Leverage features of Swift Testing like `@Test`, `#expect`, tags (`@Tag`), and parameterized testing for clear and maintainable tests.

## Tasks

- [ ] 1.0 **Define SwiftData Models for [Feature Name]**
  - [ ] 1.1 Define necessary SwiftData models (e.g., `@Model class [DataEntity]`) in the appropriate models directory (e.g., `YourApp/Models/` or directly within a feature folder if co-located).
  - [ ] 1.2 Implement any custom initializers, computed properties, or methods on the SwiftData models if required by the PRD.
  - [ ] 1.3 Create basic Swift Testing files in the project's test folder (e.g., `YourAppTests/Models/`) for these models if they contain testable custom logic.
- [ ] 2.0 **Develop UI Screen(s) for [Specific Screen/Feature]**
  - [ ] 2.1 Create `[ScreenName].swift` (e.g., using SwiftUI) in the `Screens` directory (e.g., `YourApp/Screens/[FeatureName]/`).
  - [ ] 2.2 Implement basic layout elements as per PRD/design.
  - [ ] 2.3 Integrate SwiftData queries (`@Query`) and define methods within the Screen for data fetching, creation, updates, and deletion as required.
  - [ ] 2.4 Create `[ScreenName]Tests.swift` in the project's test folder (e.g., `YourAppTests/Screens/[FeatureName]/`) and write initial tests for screen structure, state, and SwiftData interactions (potentially using an in-memory SwiftData container for testing).
- [ ] 3.0 **Implement Business Logic and Interactions in [Specific Screen/Feature]**
  - [ ] 3.1 Implement logic for user interactions (button taps, gestures, form submissions) directly within the Screen's methods or in private helper functions.
  - [ ] 3.2 Handle data transformations or view-specific logic within the Screen.
  - [ ] 3.3 Write comprehensive unit tests in `[ScreenName]Tests.swift` covering the business logic, state changes, and SwiftData operations triggered from the Screen.
- [ ] 4.0 **Integrate External Services (if any) for [Data Entity/Feature]**
  - [ ] 4.1 Develop or update any necessary non-SwiftData service classes (e.g., `NetworkService.swift`) in an appropriate services directory.
  - [ ] 4.2 Implement functions for API calls or other external interactions if the feature requires them.
  - [ ] 4.3 Ensure Screens call these services where appropriate.
  - [ ] 4.4 Write tests for these service classes in the project's test folder, potentially using mock responses or dependencies.
- [ ] 5.0 **Refinement and Error Handling**
  - [ ] 5.1 Implement user-facing error messages and loading states within the Screens.
  - [ ] 5.2 Test error paths and edge cases in Screen logic and any service interactions.

Interaction ModelThe process explicitly requires a pause after generating parent tasks to get user confirmation ("Go") before proceeding to generate the detailed sub-tasks. This ensures the high-level plan