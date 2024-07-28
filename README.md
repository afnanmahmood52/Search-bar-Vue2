# Project Documentation

## Introduction

This project is a Vue.js application designed to showcase a user-friendly interface with a search feature, tag filtering, and display of items. It uses reusable components and optimized techniques for better performance.

![project screenshot](https://github.com/user-attachments/assets/bb09145b-5e69-43cb-aecf-24f527eb94fc)

## Prerequisites

- **Node.js**: Ensure you are using Node.js version 16.

## Setup

1. **Install Dependencies**

   Navigate to the project directory and install the necessary dependencies using npm:
   ```bash
   npm install


2. **Run the Application**

Start the development server with:

bash
Copy code
npm run serve
This will launch the application in your default browser.

3. **Components**
Reusable Components
The application utilizes several reusable Vue components for modularity and maintainability:

SearchBar.vue: Contains the search input field with debounced search functionality.
Tags.vue: Displays a list of tags.
Tag.vue: Represents an individual tag with selectable functionality.
StatusSection.vue: Shows the status messages and any related information based on API responses.
CardItem.vue: Represents an item card with image, title, and description.
Card.vue: A container card component that integrates various sections like search, tags, items, and status.


4. **Constants**
The constants file defines key constants used across the application.

Explanation:
API_STATUSES: Defines different states of API calls such as loading, success, empty data, and error.
STATUS_MESSAGE: Contains various status messages used to inform the user about the state of the application or API responses.


5. **Optimization**
Debouncing has been implemented in the search functionality to optimize performance and prevent unnecessary API calls. This ensures that the search input triggers API requests only after the user has stopped typing for a short period.
