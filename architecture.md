# Project Architecture

## Frontend architecture

* **Decision:** Vue with Vuetify
	* **Time:** Meeting 1 (2024-01-19)
	* **Reasoning:** Vue is a modern client-side framework that the group was familiar with. Vuetify was chosen because it was easy to set up for the latest version of Vue.
	* **Who decided:** Daniel

* **Decision:** Client-side internationalization
	* **Time:** Meeting 2 (2024-01-22)
	* **Reasoning:** We decided on storing translations on the client-side because it provides separation and low coupling between the frontend and backend. The database will store IDs that are presented in the appropriate language by the frontend view.
	* **Who decided:** Daniel

## Backend architecture

* **Decision:** Microservices
	* **Time:** Meeting 1 (2024-01-19)
	* **Reasoning:** Microservices allows the team to work in the languages and frameworks they're most comfortable with. It also lets us scale the project easily.
	* **Who decided:** The group

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