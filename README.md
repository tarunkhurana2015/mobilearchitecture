# Mobile Architecture

Defining a great mobile architecture involves outlining a robust, scalable, testable and maintainable framework that ensures high performance, secutiry and an excellent user experience.

Following are the factors to be considered for builidng a great mobile app.

## 1. Modular Design
* ### Separation of Concerns
  *   Separate the app into distinct modules, each responsible for a specific functionality. This makes the codebase easier to undertsand, test and maintain.
       > Use `Swift Package Manager` to define local modules, separated by features or functionalites for better separation of concern.

       ```swift
        let package = Package(
        name: "Feature",
        platforms: [
          .iOS(.v16)
        ],
        products: [
            // Products define the executables and libraries a package produces, making them visible to other packages.
            .library(
                name: "<FeatureName>",
                targets: ["<FeatureName>"]
          )
        ],
        dependencies: [
          .package(url: "https://github.com/pointfreeco/swift-dependencies", exact: "1.2.2"),  // 3rd party package
          .package(name: "Core", path: "../Core") // local package
        ],
        .target(
            name: "User",
            dependencies: [
                .product(name: "Dependencies", package: "swift-dependencies"), // 3rd party dependency
                .product(name: "Networking", package: "Core"), // local dependency
            ])
          ]
        )
       ```

* ### Reusable Components
  * Develop components that can be reused across different parts of the app to avoid code duplication and enhance consistency.
 
* ### SOLID Principles
  * `SOLID` is a set of five design principles. These principles help software developers design robust, testable, extensible, and maintainable object-oriented software systems.
    > `Single Responsibility Principle` - A class should only be responsible for one thing.
    > 
    > `Open Close Principle` - Software entities (classes, modules, functions, etc.) should be open for extension, but close for modifications.
    > 
    > `Liskov Subsitution Principle` - Derived or child clases/ structures must be substitutable for their base or parent class.
    >
    > `Interface Segregation Principle` - Do not force a client to implement an interface which is irrelevant for them.
    >
    > `Dependency Inversion Principle` - High level module should not be dependent on the low level module, but should depend on the abstraction to avoid tight code coupling.

## 2. Scalability
* ### Flexible Architecture
  *   Ensure the archietcture can easily accomodate new features and functionalities without significant changes to the existing codebase.
  *   Separate out the business logic into it's own layer also known as the the `Domain` layer.
      > Adapt the `Clean Architecture Principles` to separate the layers for better flexibility.
      > 
      > ![cleanarch_icon drawio](https://github.com/tarunkhurana2015/mobilearchitecture/assets/9640541/d7953f34-82fb-4f7b-b6a7-31a7a52a59fe)


* ### Miscroservices
  *  For backend services, use a microservices architecture to allow independent scaling and deployment of services.

## 3. Performance
Mobile app performance involves several strategies:
  * Responsive UI
  * Effecient Resource Management
  * Reliable Speed

  Following are the strategies for enhancing the app's performance.  
  * `Measure and Identifiy Performance bottlenecks`
    * Use profiling tools like `App Instumentation` to identify bottlenecks, such as `CPU usage`, `Memory leaks` and `Netwotk latency`.
    * Analyze performance metrices and identify areas of improvements.   
  * `Optimize UI Rendering`
    * Use efficient UI components like `collection views` to efficiently render the lists.
    * Use `Pagination`
    * Use `Lazy Loading`
    * Implement `asynchronous data` loading to avoid blocking of the main thread.
    * Reduce the layers, views and subviews to minimize rendering menthods.
  * `Improve Networking Performance`
    * Use asynchronous networking API like `URLSesssion` for making network requests to prevent blocking of the main thread.
    * Implement `network caching` mechanisms to reduce network requests and improve app responsiveness.
    * Optimize netwwork `payload size` by using techniques like `gzip`.
  * `Improve Memory Usage`
    * Profile memory usage using instruments to identify memory leaks and excessive memory consumption.
    * Use lazy loading and on demand initilization to load resources when needed.
    * Use `struct: Stack` over `classes: Heap`
    * Define classes to `final` to optimize the memory.
    * Use `CopyOnWrite` to optize the memory usage.
  * `Reduce CPU Usage`
    * Profile CPU intensive tasks.
    * Optimize the algorithm and data structures.
    * Use language based `concurrency` models for better thread management.
    * Minimize unnecessary CPU-intesive tasks.
  * `Optimize File I/O and Disk Usage`
    * Minimize the file I/O operations, especially on the main thread, to prevent blocking the UI.
    * Use background thread for File I/O operations.
    * Optimize File access patterns and cache frequently accessed files or data in memory to reduce disk I/O latency.
  * `Optimize the Battery life`
    * Minimize the background activity and use energy-efficient API's to prevent battery life.
    * Optimize location services, background fetch and push notifications.

## 4. Security
Following are the security strategies for the mobile apps
* `Use Secure Authentication`
    * Use Apple's secured authentication mechanism (biometric) such as `TounchID`, `FaceID` and `PassKkeys`
    * Use 2 factor authentication.
* `Data Encryption`
    * Encrypt sensitive data such as `user credentials`, `payment details` and `transaction data` in trannsit and at rest.
    * Use symmetric `AES` based encryption mechanisms to protect data from unauthorized access.
    * Use `CryptoKit` `NSFileProtection` api's
    * > Use strong encryption algorithms with appropriate key lenghts.
      >
      > Hash the password sent over the network.
      > 
      > Generate random keys for each encryption operations.
      >
      > Store the encryption keys separate from the encrypted data.
      >
      > Use keychain for storing keys
      >
      > Regulary update allgorithm and keys
 * `Secure Network Communication`
    * Use `HTTPs/ TLS` for network communications.
    * Implement certificate pinning to prevent man in the middle attack.
 * `Tokenization`
    * Implement tokenization to replace sensitive data (credit card number) with unique tokens.
 * `Secure Code Practice`
    * Secure coding practice to mitigate common vulnerabilities such as SQL injections.
    * Regularly update libraries and depedencies.
 * `Authorization`
    * Implement role based access control to ensure that users have appropriate permission based on their role.
 * `Session Management`
    * Use short lived sesion tokens.
    * enforce session expiration policies.
 * `Security Testing`
    * Conduct regular secutiry audit.
    * Perform static code analysis.
    * Perform penetration testing.
    * Analyze network and device logs.

## 5. Testing
 * Automated Testing: Implement a comprehensive suite of unit, integration, and UI tests to catch bugs early and ensure the app's stability.
 * Continuous Integration (CI): Use CI tools to automate the build and testing process, ensuring that code changes are continuously validated.

## 6. User Enperience
 * Intuitive Design: Follow platform-specific design guidelines (Human Interface Guidelines for iOS, Material Design for Android) to ensure a familiar and intuitive user experience.
 8 Accessibility: Ensure the app is accessible to users with disabilities by following accessibility best practices and guidelines.

## 7. Maintainability
 * Clean Code Practices: Follow clean code principles and coding standards to make the codebase easy to read and maintain.
 * Documentation: Maintain comprehensive documentation for the codebase, including API documentation, architecture diagrams, and code comments.

## 8. Resiliency
 * Error Handling: Implement robust error handling and logging mechanisms to gracefully handle failures and provide useful diagnostics.
 * Redundancy and Failover: For backend services, ensure redundancy and failover mechanisms to maintain service availability.

## 9. Analytics
 * Performance Monitoring: Use tools like Firebase/ Sentry Performance Monitoring or New Relic to monitor the app's performance in real-time.
 * User Analytics: Implement analytics to track user behavior, identify issues, and make data-driven decisions for improvements.

## 10. Continous Improvements
 * Feedback Loop: Regularly gather feedback from users and stakeholders to identify pain points and areas for improvement.
 * Iterative Development: Use agile methodologies to continuously iterate and improve the app based on feedback and changing requirements.
