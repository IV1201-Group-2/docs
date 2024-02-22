# Project Architecture

## Frontend architecture

* **Decision:** Vue with Vuetify
	* **Time:** Meeting 1 (2024-01-19)
	* **Reasoning:** Vue is a modern client-side framework that the group was familiar with. Vuetify was chosen because it was easy to set up for the latest version of Vue.
	* **Who decided:** Daniel

* **Decision:** Client-side internationalization
	* **Time:** Meeting 2 (2024-01-22)
	* **Reasoning:** We decided on storing translations on the client-side because it provides separation and low coupling between the frontend and backend. When there is a need to store a translated phrase in the database, e.g. as the result of the applicant having selected certain competences when submitting their job application, the last part of the I18n key path (the part after the path's last dot) will be stored instead of the actual translation.
	* **Who decided:** Daniel

* **Decision:** Internationalized strings should never be persisted as is, but rather their I18n keys.
	* **Time:** Meeting 2 (2024-01-22)
	* **Reasoning:** When there is a need to store an internationalized string in the database, e.g. as the result of the applicant having selected certain competences when submitting their job application, the last part of the I18n key path (the part after the path's last dot) will be stored instead of the actual translation.
	* **Who decided:** Daniel

 * **Decision:** TypeScript
 	* **Time:** 2024-01-24
  	* **Reasoning:** Adds type safety and by extension reduces time spent on troubleshooting.
   	* **Who decided:** Daniel

 * **Decision:** Vitest for tests
 	* **Time:** 2024-01-31
  	* **Reasoning:** Vitest can be automatically configured when initalizing a new Vue 3 project and is thus easy to set up. It is also bundled together with Vue Test Utils which makes it a perfect fit for a Vue SPA.
   	* **Who decided:** Daniel
  
 * **Decision:** Nest `vitest#describe()` when testing nested components
 	* **Time:** 2024-01-31
  	* **Reasoning:** When testing a nested component, for example an input field inside a form, multiple `vitest#describe()` calls should be nested to specify the exact location of the component.
   	* **Who decided:** Daniel
  
 * **Decision:** Pass TypeScript enums defined in `src/components/__test__/custom_test_utils/enums.ts` as arguments to `vitest#describe()` and `vitest#it()` when describing the (1) component, (2) action and (3) time/condition when tested behaviour occurs. Detailed documentation can be found in the aforementioned `enums.ts` file.
 	* **Time:** 2024-01-31
  	* **Reasoning:** Enforces naming conventions. 
   	* **Who decided:** Daniel
  
 * **Decision:** All functions used for validation rules should be stored inside the class `src/util/validation.ts#ValidationBuilder`.
 	* **Time:** 2024-01-31
  	* **Reasoning:** Facilitates validation handling.
   	* **Who decided:** Daniel
  
 * **Decision:** Let all non-persistent data manipulations which only purpose is to present the manipulated data in the view layer, such as sorting or internationalization, occur in the view layer.
 	* **Time:** 2024-02-12
  	* **Reasoning:** Better separation of concerns. 
   	* **Who decided:** Daniel

* **Decision:** Internationalized strings representing competences should have an associated ID in their dedicated database table.
	* **Time:** 2024-02-18
	* **Reasoning:** To accomodate the existing structure of the table dedicated to storing an applicant's competences (`competence_profile` which associates the applicant's `person_id` with a `competence_id`) when migrating from the legacy database, all internationalized competences should be associated with a `competence_id` in addition to their I18n key when persisted.
	* **Who decided:** Daniel, Azmeer

 * **Decision:** All unsuccessful API calls should be handled by displaying a [Vuetify dialog](https://vuetifyjs.com/en/components/dialogs/#api) in one of two ways: 1) either by inserting the dialog in the same component that made the API call, or 2) by calling `src/stores/error.ts#showGenericErrorMsg()` to display `src/components/generic/GenericError.vue` which is rendered in the root component `src/App.vue`. Method #1 is preferred when the cause of the error is known and customization of the dialog is required, such as adding custom buttons with custom actions. Since the cause of the error must be know in advance, this method is usually used when the cause of the error can be pinned down by the response status code. Method #2 is preferred when the error is unexpected and thus requires generic handling. Alternatively, it may also be used when the cause is unknown whereas the effect is known, e.g. personal information about the applicant cannot be retrieved for some unknown reason, but it is known that the applicant will not be able to submit their application because of the failed retrieval. In the latter scenario, the developer may pass as optional argument to the `showGenericErrorMsg()` a string to be concatenated with the I18n key path `generic-key.specific-msg.` that will be translated as the message to be displayed within the generic error dialog. If no argument is passed, the generic message specified by the I18n key path `generic-error.generic-msg` will be displayed instead. The generic error dialog allows for no customization of the actions that can be taken, and only has one button which when clicked logs out the user and returns them to the login page.
 	* **Time:** 2024-02-21
  	* **Reasoning:** Enforces consistent error handling.
   	* **Who decided:** Daniel
  
* **Decision:** The base URL (everything from the protocol to the domain, e.g. `https://test-service.herokuapp.com`) for each API service used by the client should be stored as a field inside the variable `BASE_URL` declared in `src/util/api.ts`.
	* **Time:** 2024-02-21
	* **Reasoning:** Facilitates handling of API URLS.
	* **Who decided:** Daniel

## Backend architecture

* **Decision:** Microservices
	* **Time:** Meeting 1 (2024-01-19)
	* **Reasoning:** Microservices allows the team to work in the languages and frameworks they're most comfortable with. It also lets us scale the project easily.
	* **Who decided:** The group


* **Decision:** RESTful APIs
  * **Time:** Meeting 1 (2024-01-19)
  * **Reasoning:** RESTful APIs are a good fit for our project because they are stateless, cacheable, and scalable. They also provide a good separation of concerns and are easy to understand and use.
  * **Who decided:** The group


* **Decision:** PostgreSQL
	* **Time:** Meeting 1 (2024-01-19)
	* **Reasoning:** PostgreSQL is a powerful, open-source object-relational database system. It has a strong reputation for reliability, data integrity, and correctness. It also compatible with the existing SQL dump.
	* **Who decided:** The group


* **Decision:** Server-side Data validation
	* **Time:** Meeting 1 (2024-01-19)
	* **Reasoning:** We decided to validate data on the server side to ensure that the data is correct and consistent. This is especially important when dealing with user input.
	* **Who decided:** The group


### Python-based microservices
* **Decision:** Layered architecture
	* **Time:** 2024-01-19
	* **Reasoning:** It allows for good code organization, separation of concerns, and maintainability
	* **Who decided:** Azmeer


* **Decision:** Object-oriented programming
	* **Time:** 2024-01-19
	* **Reasoning:** OOP is a good fit for the microservices we're building. It allows us to model the domain in a natural way and makes the codebase more maintainable.
	* **Who decided:** Azmeer
  

* **Decision:** Pipenv for package management
	* **Time:** 2024-01-19
	* **Reasoning:** Pipenv is a package manager for Python that is easy to use and has good support for virtual environments.
	* **Who decided:** Azmeer


* **Decision:** Flask for web framework
	* **Time:** 2024-01-19
	* **Reasoning:** Flask is a lightweight and easy-to-use framework for Python. It's a good fit for the microservices we're building.
	* **Who decided:** Azmeer


* **Decision:** Blueprint for routing
	* **Time:** 2024-01-19
	* **Reasoning:** Blueprints are a good way to organize routes in Flask. They allow us to group related routes together and make the codebase more maintainable.
	* **Who decided:** Azmeer


* **Decision:** Flask-SQLAlchemy for database access
	* **Time:** 2024-01-19
	* **Reasoning:** Flask-SQLAlchemy is a popular library for database access in Flask. It provides an easy-to-use ORM and good support for migrations. It 
	* **Who decided:** Azmeer


* **Decision:** Unit tests 
	* **Time:** 2024-01-25
	* **Reasoning:** Unit tests are a good way to ensure that the microservices work as expected. They make the codebase more maintainable and reduce time spent on troubleshooting.
	* **Who decided:** Azmeer


* **Decision:** Pytest for tests
	* **Time:** 2024-01-25
	* **Reasoning:** Pytest is a popular testing framework for Python and is easy to set up. It has good support for fixtures and mocking.
	* **Who decided:** Azmeer


* **Decision:** Python 3.9
	* **Time:** 2024-01-26
	* **Reasoning:** Python 3.9 is a good fit for the microservices we're building. It's a stable version of Python and has good support for the libraries we're using.
	* **Who decided:** Azmeer


* **Decision:** PEP8 for code formatting
	* **Time:** 2024-01-26
	* **Reasoning:** PEP8 is the standard for Python code formatting and is widely used. It makes the codebase more maintainable and readable.
	* **Who decided:** Azmeer


* **Decision:** Type hints for type safety
	* **Time:** 2024-01-29
	* **Reasoning:** Type hints make the codebase more maintainable and reduce time spent on troubleshooting. They also make the codebase more readable.
	* **Who decided:** Azmeer


* **Decision:** Singleton pattern for extensions
	* **Time:** 2024-01-31
	* **Reasoning:** The singleton pattern is a good way to organize extensions in Flask. The extensions are shared across the application and are only instantiated once.
	* **Who decided:** Azmeer


* **Decision:** Decorator for JWT authentication
	* **Time:** 2024-01-31
	* **Reasoning:** Decorators are a good way to organize JWT authentication in Flask. They allow us to apply the same authentication logic to multiple routes.
	* **Who decided:** Azmeer

* **Decision:** Logging for monitoring
	* **Time:** 2024-02-01
	* **Reasoning:** Logging is a good way to keep track of what's happening in the microservices. It makes the codebase more maintainable and helps with troubleshooting.
	* **Who decided:** Azmeer


* **Decision:** Application factory pattern
	* **Time:** 2024-02-01
	* **Reasoning:** The application factory pattern is a good way to organize the Flask app. It makes the codebase more maintainable and reduces time spent on troubleshooting.
	* **Who decided:** Azmeer


* **Decision:** Flake8 for code formatting
	* **Time:** 2024-02-02
	* **Reasoning:** Flake8 is a popular code formatter for Python and is easy to set up. It enforces PEP8 and other best practices.
	* **Who decided:** Azmeer


* **Decision:** MyPy for type checking
	* **Time:** 2024-02-02
	* **Reasoning:** MyPy is a popular type checker for Python and is easy to set up. It enforces type safety and reduces time spent on troubleshooting.
	* **Who decided:** Azmeer


* **Decision:** Pytest-cov for test coverage
	* **Time:** 2024-02-04
	* **Reasoning:** Pytest-cov is a popular test coverage tool for Python and is easy to set up. It enforces a high amount of test coverage and reduces time spent on troubleshooting.
	* **Who decided:** Azmeer


* **Decision:** CORS for security
	* **Time:** 2024-02-05
	* **Reasoning:** CORS is a good way to ensure that the microservices are secure. It makes the codebase more maintainable and reduces time spent on troubleshooting.
	* **Who decided:** Azmeer


* **Decision:** Gunicorn for production server
	* **Time:** 2024-02-07
	* **Reasoning:** Gunicorn is a popular production server for Python, easy to set up and recommended by Heroku. It 
	  provides good performance and security.
	* **Who decided:** Azmeer


* **Decision:** Global error handling
	* **Time:** 2024-02-18
	* **Reasoning:** Global error handling is a good way to ensure that the microservices work as expected. It makes the codebase more maintainable and reduces time spent on troubleshooting.
	* **Who decided:** Azmeer


* **Decision:** 

### Java-based microservices

- **Decision:** MVC architecture

  - **Time:** 2024-01-28
  - **Reasoning:** MVC adds modularity, which allows for code flexibility and being ability to modify different layers and components in isolation.
  - **Who decided:** Yas

- **Decision:** Java version 21

  - **Time:** 2024-01-28
  - **Reasoning:** Java 21 is the latest Java version that is compatible with Heroku and has the latest compatibility updates with dependencies.
  - **Who decided:** Yas

- **Decision:** Spring Boot framework

  - **Time:** 2024-01-28
  - **Reasoning:** The Spring Boot framework allows for easy dependency injection of different layers, benefiting the MVC architecture. Moreover, the framework supports the use of JUnit testing which is a widely used Java testing tool.
  - **Who decided:** Yas

- **Decision:** Spring boots @Autowired

  - **Time:** 2024-01-30
  - **Reasoning:** The @Autowired annotation maintains loose coupling.
  - **Who decided:** Yas

- **Decision:** Use of @Transactional

  - **Time:** 2024-01-31
  - **Reasoning:** For methods where anything is added or modified in the database, the @transactional annotation provides data consistency and rolls back the changes made by a method in case of an exception. Furthermore, the annotation allows for an easily readable code and reduces boilerplate code.
  - **Who decided:** Yas

- **Decision:** JUnit testing

  - **Time:** 2024-02-02
  - **Reasoning:** A widely used testing framework for Java that automates testing and is well integrated with IntelliJ IDEA.
  - **Who decided:** Yas

- **Decision:** TestContainers

  - **Time:** 2024-02-02
  - **Reasoning:** TestContainers provide a containerized database environment for testing the different layers in an isolated environment. As a new instance of the database is created for each test, the risk of test dependency is reduced. TestContainers also supports PostgreSQL.
  - **Who decided:** Yas

- **Decision:** DTO's

  - **Time:** 2024-02-02
  - **Reasoning:** DTOs achieve encapsulation of data that passes through the different layers of the application. Data transfer objects provide only the data necessary to be exposed to the client.
  - **Who decided:** Yas

- **Decision:** Lomboks annotations
  - **Time:** 2024-02-03
  - **Reasoning:** Lombok provides access to many useful annotations that reduce boilerplate code. The @Data annotation provides getters and setters. Depending on the classes implemented, @AllArgsConstructor or @NoArgsConstructor was added where a constructor was needed with all arguments for all fields or no arguments. Lastly, @Builder was useful for providing a builder pattern to easily create an object.
  - **Who decided:** Yas

### Golang-based microservices

* **Decision:** Layered architecture
  - **Time:** 2024-01-31
  - **Reasoning:** All microservices written in Go should have a layered architecture. The presentation layer is handled by the framework of choice while the service layer implements the public API and the database layer handles interactions with a real or mock database. The model layer strictly contains structures and functions that model our application architecture (database objects, API responses, etc).
  - **Who decided:** Hannes

* **Decision:** Echo framework
  - **Time:** 2024-01-31
  - **Reasoning:** We decided to use the Echo framework for handling HTTP routing and middleware. The framework is a great choice for REST APIs because it has a minimalist design that's simple to understand while being modern, production-tested and very performant. It has built-in middleware to handle recovering from errors, JWT token authentication and more.
  - **Who decided:** Hannes

* **Decision:** Go modules
  - **Time:** 2024-01-31
  - **Reasoning:** Go modules are a feature added in Go 1.13 that allows the service to declare the required Go version and its dependencies. We use this feature because it allows Heroku to automatically discover how the application should be built without requiring a Dockerfile.
  - **Who decided:** Hannes

* **Decision:** Heroku buildpack
  - **Time:** 2024-01-31
  - **Reasoning:** We use the Heroku Go buildpack to build the application without having to create a Dockerfile. Heroku automatically picks the right version of Go and downloads dependencies.
  - **Who decided:** Hannes

* **Decision:** Documentation format
  - **Time:** 2024-02-06
  - **Reasoning:** Go doesn't have an explicit format for documentation like Java but it provides some recommendations (such as "package comments should start with 'The package X does Y'"). Our projects follow all recommendations with comments for all public structures and functions.
  - **Who decided:** Hannes

* **Decision:** .env files
  - **Time:** 2024-02-06
  - **Reasoning:** Our Go microservices will load environment variables from .env files automatically using godotenv. This allows to set up a development environment easily for multiple users.
  - **Who decided:** Hannes

* **Decision:** Validation with go-playground/validator
  - **Time:** 2024-02-05
  - **Reasoning:** Echo allows us to validate parameters that are sent by the user but it doesn't provide a built-in validator. go-playground/validator is a powerful and popular choice that allows us to automatically validate that parameters are required or that they follow a certain format depending on annotiations in a structure.
  - **Who decided:** Hannes

* **Decision:** Testing with Testify
  - **Time:** 2024-02-06
  - **Reasoning:** Go doesn't have a lot of built-in functionality for testing. Testify combined with Echo allows us to simulate HTTP requests and assert certain conditions with only a few lines of code.
  - **Who decided:** Hannes

* **Decision:** Linting with golangci-lint
  - **Time:** 2024-02-06
  - **Reasoning:** golangci-lint is an aggregator for Go linters and static analysis tools. It allows us to run 100+ linters automatically and in parallel to ensure as many mistakes in the code are covered as possible. We enable all linters except a few that don't make sense for our project.
  - **Who decided:** Hannes

## Cloud hosting

* **Decision:** Heroku
	* **Time:** Meeting 3 (2024-01-24)
	* **Reasoning:** Heroku has a student offer and provides functionality for hosting microservices, logging, databases and storing secrets.
	* **Who decided:** The group

## Version control

* **Decision:** Multiple repos
	* **Time:** Meeting 2 (2024-01-22)
	* **Reasoning:** We decided on using a separate repo for every microservice (instead of a monorepo) because it's a natural fit for deploying to Heroku and our CI/CD pipeline.
	* **Who decided:** Yas

## Authentication

* **Decision:** JWT tokens
	* **Time:** Meeting 4 (2024-01-29)
	* **Reasoning:** Authentication with JWT tokens allows us to verify user details without unnecessary API communication. The only thing a microservice needs knowledge of to verify a user is a shared secret.
	* **Who decided:** Hannes

## Code documentation

* **Decision:** Full documentation coverage
	* **Time:** Meeting 1 (2024-01-19)
	* **Reasoning:** We should follow best practices for our languages and provide comments for all public functions and classes.
		* Java: Javadoc
		* Python: DocStrings
		* Go: Godoc
	* **Who decided:** The group

* **Decision:** API documentation
	* **Time:** Meeting 4 (2024-01-29)
	* **Reasoning:** All backend APIs we define should be documented in a repostitory for the purpose of collaboration and handover.
	* **Who decided:** The group

* **Decision:** Java build tools
	* **Time:** Meeting 1 (2024-01-19)
	* **Reasoning:** For microservices written in Java, Maven will be used as the build tool. For Python and Go the recommended included build tool will be used.
	* **Who decided:** Yas and Daniel

## Version control

* **Decision:** Gitflow
	* **Time:** Meeting 4 (2024-01-29)
	* **Reasoning:** We decided to use the Gitflow model for managing our branches. This means we have feature branches, a develop branch and a main branch. This works well with Scrum since every user story is supposed to add a new feature.
	* **Who decided:** The group

* **Decision:** Branch protection rules
	* **Time:** Meeting 4 (2024-01-29)
	* **Reasoning:** We will use branch protection rules in Git to prevent pushing to the main branch. Every feature needs to be sent as a pull request and reviewed by another member.
	* **Who decided:** The group

## CI/CD

* **Decision: GitHub Actions**
	* **Time:** Meeting 2 (2024-01-22)
	* **Reasoning:** We decided to use GitHub Actions for our contiguous integration because it allows us to run and deploy the project when a pull request is submitted or a branch is merged.
	* **Who decided:** Azmeer

## Testing

* **Decision: High amount of test coverage**
	* **Time:** Meeting 2 (2024-01-22)
	* **Reasoning:** We want a high amount of test coverage (70-80%) for our code to ensure it works well, even in edge cases.
	* **Who decided:** The group
