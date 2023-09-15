# Code Busters Group Project - QA Cinema

## Contents

1. [Overview of technologies used](#overview-of-technologies-used)
2. [Requirements Gathering](#requirements-gathering)
3. [Design Choices](#design-choices)
4. [Development](#development)
5. [Testing](#testing)
6. [Deployment](#deployment)
7. [Future Steps](#future-steps)
8. [Contributors](#contributors)
9. [Acknowledgements](#acknowledgements)
10. [Instructions](#instructions)

## Overview of Technologies Used

Our objective for this project was to create a fully functioning application with utilisation of supporting tools, methodologies and technologies that encapsulate all modules we covered during our training .We have created a full-stack web application for QA Cinemas that fully conforms to a provided client specification. The website was made with ease of use and attractiveness in mind, and provides information about movies, listings, upcoming releases and the ability to log in and book tickets.

We have used the following technologies in our project:

- Jira for project management via Kanban
- Scrum as the agile methodology
- Git as the version control system
- GitHub for source code management
- HTML, CSS, JavaScript and Bootstrap for front-end development
- Python as the back-end programming language
- Flask as the API development platform
- MySQL as the database management system
- Pytest and Flask-testing for performings tests
- Jenkins for continuous integration
- Docker for containerisation

## Requirements Gathering

### MVP Checklist

Below is the MVP and wishlist specified within the project brief. Every requirement has a checkbox next to it specifying whether it has been completed or not.

#### Home
- [x] Visually appealing
- [x] Communicate the site's purpose to the visitors
- [x] Default for the entire site
- [x] Contain navigation to other sections of the site

#### Login
- [x] Allow users to sign up and log into an account
- [x] Be navigable from the home page at a minimum
- [x] Accessible via the top right-hand side of the site’s pages
- [x] Login via a username and password on a created account or sign up for a new account using the same method
- [x] Password should have basic security requirements (special character, upper and lower-case letters, numbers)

#### Listings
- [x] Include a gallery of movie posters for movies currently showing
- [x] Part of overall site navigation
- [x] Feature at least 4 brand-new releases as movie images, with each image having its own page
- [x] Each image has supporting text including title, actors, director, and showing times

#### Opening Times
- [x] List the opening times
- [ ] Part of overall site navigation 

#### New Releases
- [x] Gallery of movie posters for forthcoming movies
- [ ] Part of overall site navigation
- [x] Feature at least 4 brand-new releases as movie images, with each image having its own page
- [x] Each image has supporting text including title, actors, director, and showing times

#### Classifications
- [x] Part of overall site navigation
- [x] State the standard film classifications and their icons
- [x] Rules and conditions relating to each classification
- [x] May include other relevant facts
- [x] May link out to external resources with more detail

#### Screens
- [x] Include an image of the seating plan and decoration of a standard screen
- [x] Include the same but also for deluxe screen

#### Booking
- [x] Part of overall site navigation
- [x] Include movie title, screening date and time, number of seats, name of booker, ticket type (adult or child), concession

#### Payment
- [x] Include card holder’s name, card number, expiry date, CVC
- [ ] Details should be saved and passed onto an external merchant for processing

#### Services
- [x] Include info about what the cinema offers, including food/drinks and other amenities
- [x] Part of overall site navigation
- [x] Basic prices for popcorn, hot dogs, fizzy drinks
- [x] Feature the indoor restaurant and arcade

#### Discussion Board
- [x] Part of overall site navigation
- [x] Users can comment on movie-related topics
- [x] Users’ posts should be moderated to ensure that inappropriate content is not shown

#### Search Functionality
- [x] Feature a search bar that lets users search by keyword
- [x] Links to relevant content are returned in a list from the search terms

#### About
- [x] Dedicated to who QA Cinemas are, as well as the team who made the website
- [x] Part of overall site navigation
- [x] Name of each team member appears on the page
- [ ] Small paragraph on each member
- [x] Contain generic contact info
- [x] Small paragraph on who QA Cinemas are

#### Background
- [x] Background color on any page should not be white

#### Navigation
- [x] Should be able to navigate to various areas of the site in a uniform and predictable manner
- [x] Navigation is present on all pages of the site and is uniform across all pages

#### Footer (Wishlist)
- [ ] Links to commonly accessed pages (Home, About, Contact)
- [ ] Identical on all pages

#### Logo (Wishlist)
- [ ] Custom logo that depicts the site’s name and a picture of a movie reel
- [ ] Must appear on the front page
- [ ] Should fit with the overall aesthetic of the site

### Reasoning behind Unfinished Parts of the MVP

- **Opening Times:** We added this information to the About page to avoid clutter in the navigation bar.
- **New Releases** We merged the information in the New Releases page to the Listings page according to our acceptance criteria (see User Story document in the documentation folder and the Kanban section below for more information).
- **Payment:** Details are not passed onto an external merchant for processing due to a lack of time.
- **About:** Instead of a small paragraph on each team member, we created an origin story to connect emotionally with customers.
- **Footer and Logo (Wishlist):** These were lower-priority items, and the footer was deemed unnecessary as essential links and contact information are already accessible on the site, and a footer would affect the site's aesthetic appeal.

### Risk Assessment

A relatively simple risk assessment was conducted during the early stages of the requirements gathering stage. For each risk, things such as probability, impact, severity, and mitigation were declared. Moreover, we created a simple Risk Assessment Matrix which can be seen below:

![Risks Assessment Matrix](/documentation/screenshots/risk_assessment_matrix.png)

## Analysis and Design

### Architecture

### Entity-Relationship Diagram (ERD)

The creation of an entity-relationship diagram was essential during the early stages of the SDLC. Due to how Agile projects work, the latter has been continuously redefined in order to successfully meet the requirements set out during the requirements gathering step.

With that being said, here is the most up-to-date version:

![Final ERD draft](/documentation/screenshots/final_erd_draft.png)

### Classes definition

Similar to the creation of the ERD, defining our classes/models and reviewing how they would have interacted with each other was something that needed to be done in order to set up a good foundation for the later SDLC stages (i.e., coding, testing).

However, in the current state and for what was achievable, all the modules were successfully designed following the 3 normalisation forms.

Here we can see how the models interact with each other using the Reverse Engineer feature of MySQL Workbench:

![MySQL Workbench - Reverse Engineer](/documentation/screenshots/mysql_workbench.png)


Moreover, a more in-depth specification regarding the components can be found below:

#### User

| Field         | Data Type  | Constraints       |
|---------------|------------|-------------------|
| user_email    | String(30) | Primary Key       |
| username      | String(20) | Not Null          |
| first_name    | String(30) | Not Null          |
| last_name     | String(30) | Not Null          |
| hash          | String(60) | Not Null          |

#### Booking

| Field            | Data Type   | Constraints       |
|------------------|-------------|-------------------|
| booking_id       | Integer     | Primary Key       |
| movie_id         | Integer     | Not Null, Foreign Key (movie.movie_id) |
| screening_time   | DateTime    | Not Null          |
| user_email       | String(30)  | Not Null, Foreign Key (user.user_email) |
| concession       | Boolean     | Not Null          |

#### Ticket

| Field         | Data Type  | Constraints       |
|---------------|------------|-------------------|
| ticket_id     | Integer    | Primary Key       |
| ticket_type   | String(30) | Not Null          |
| price         | Float      | Not Null          |

#### TicketBooking

| Field             | Data Type  | Constraints       |
|-------------------|------------|-------------------|
| ticket_booking_id | Integer    | Primary Key       |
| ticket_id         | Integer    | Not Null, Foreign Key (ticket.ticket_id) |
| booking_id        | Integer    | Not Null, Foreign Key (booking.booking_id) |
| seat_number       | String(10) | Not Null          |

#### Movie

| Field             | Data Type  | Constraints       |
|-------------------|------------|-------------------|
| movie_id          | Integer    | Primary Key       |
| title             | String(30) | Not Null          |
| release_date      | DateTime   | Not Null          |
| poster_path       | String(255)| Not Null          |
| banner_path       | String(255)| Not Null          |
| status            | String(20) | Not Null          |
| plot              | Text       | Not Null          |
| classification_id | Integer    | Not Null, Foreign Key (classification.classification_id) |

#### Payment

| Field             | Data Type  | Constraints       |
|-------------------|------------|-------------------|
| payment_id        | Integer    | Primary Key       |
| booking_id        | Integer    | Not Null, Foreign Key (booking.booking_id) |
| timestamp         | DateTime   | Not Null          |
| card_holder_name  | String(50) | Not Null          |
| card_number       | String(255)| Not Null          |
| expiry_date       | DateTime   | Not Null          |
| security_code     | String(255)| Not Null          |
| amount            | Float      | Not Null          |
| status            | String(20) | Not Null          |

#### MenuService

| Field         | Data Type  | Constraints       |
|---------------|------------|-------------------|
| item_id       | Integer    | Primary Key       |
| name          | String(30) | Not Null          |
| type          | String(20) | Not Null          |
| price         | Float      | Not Null          |
| image_path    | String(255)| Not Null          |

#### DiscussionBoard

| Field         | Data Type  | Constraints       |
|---------------|------------|-------------------|
| post_id       | Integer    | Primary Key       |
| title         | String(255)| Not Null          |
| user_email    | String(30) | Not Null, Foreign Key (user.user_email) |
| content       | String(255)| Not Null          |
| timestamp     | DateTime   | Not Null          |

#### Classification

| Field             | Data Type  | Constraints       |
|-------------------|------------|-------------------|
| classification_id | Integer    | Primary Key       |
| name              | String(30) | Not Null          |
| icon_path         | String(255)| Not Null          |
| rules_and_conditions | String(255)|             |

#### Genre

| Field         | Data Type  | Constraints       |
|---------------|------------|-------------------|
| genre_id      | Integer    | Primary Key       |
| name          | String(30) | Not Null          |

#### MovieGenre

| Field             | Data Type  | Constraints       |
|-------------------|------------|-------------------|
| movie_genre_id    | Integer    | Primary Key       |
| genre_id          | Integer    | Not Null, Foreign Key (genre.genre_id) |
| movie_id          | Integer    | Not Null, Foreign Key (movie.movie_id) |

#### Cast

| Field         | Data Type  | Constraints       |
|---------------|------------|-------------------|
| cast_id       | Integer    | Primary Key       |
| first_name    | String(30) | Not Null          |
| last_name     | String(30) | Not Null          |
| gender        | String(10) | Not Null          |
| role          | String(30) | Not Null          |

#### MovieCast

| Field             | Data Type  | Constraints       |
|-------------------|------------|-------------------|
| movie_cast_id     | Integer    | Primary Key       |
| cast_id           | Integer    | Not Null, Foreign Key (cast.cast_id) |
| movie_id          | Integer    | Not Null, Foreign Key (movie.movie_id) |

#### Screen

| Field         | Data Type  | Constraints       |
|---------------|------------|-------------------|
| screen_id     | Integer    | Primary Key       |
| screen_number | Integer    | Not Null, Unique  |
| screen_type   | String(20) | Not Null          |
| capacity      | Integer    | Not Null          |
| seating_plan_img_path | String(255)|         |

#### MovieScreen

| Field             | Data Type  | Constraints       |
|-------------------|------------|-------------------|
| movie_screen_id   | Integer    | Primary Key       |
| screen_id         | Integer    | Not Null, Foreign Key (screen.screen_id) |
| movie_id          | Integer    | Not Null, Foreign Key (movie.movie_id) |
| showing_time      | DateTime   | Not Null          |


## Development

### GitHub Workflow

We utilised feature-branches in our project, namely 7  branches: main, dev, feature-front-end, feature-flask, feature-database, feature-testing and feature-docker. We would aim to work in separate branches in order to minimise merging issues. Furthermore, we created pull requests to merge code that we had been working on to the dev branch (see screenshots). On the last day, we pushed all the code from dev to main. 
We also set up branch protection for our important branches, namely main and feature-database (see screenshots). We had to review each change before accepting the pull request, which added an extra layer of protection.

## Testing

## Deployment

## Future Steps

## Contributors

W3schools, QA community, Bootstrap, Earl Gray's amazing code.


## Acknowledgements

To our trainers, Earl and Leon for their support. To our colleagues for cheering us on. Lastly, to each and every member of Code Busters for giving 100% and making it a pleasure to work together. Our legacy will live on in this repo…

## Instructions

### Installation Instructions

Here are the essential setup instructions required for connecting to the group repository and launching the webpage. These instructions assume that all group members have been added as contributors to the GitHub repository. Given that this project will be utilizing feature branches, the "git pull" command should be regularly employed to keep each group member's local machine synchronized with the repository.

1. Clone the group repository to your local machine:

   ```shell
   git clone https://github.com/fkia413/Codebusters

2. Navigate to the project directory:

   ```shell
   cd ams-group-project

3. Install the necessary dependencies using pip:

   ```shell
   pip3 install -r requirements.txt

4. Ensure your local copy is up-to-date by pulling the latest changes from the repository:

   ```shell
   git pull

5. Create the required database tables or structures:

   ```shell
   python3 create.py

6. Launch the web application:

   ```shell
   python3 app.py

### Deployment Instructions

### Testing Instructions