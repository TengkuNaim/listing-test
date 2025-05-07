# User Listing Application

A responsive frontend application that displays a list of users with filtering, sorting, and pagination capabilities.

## Features

- **User List Display**: Shows user information in both mobile and desktop optimized views
- **Search Functionality**: Filter users by name or email
- **Sorting Options**: Sort by name, registration date, or country
- **Pagination**: Navigate through user pages
- **User Details Modal**: Click any user to view detailed information
- **Refresh Capability**: Fetch new random users with the refresh button
- **Responsive Design**: Works on all device sizes

## Technologies Used

- Vue.js 3 (Composition API)
- Tailwind CSS for styling
- Random User API for data
- Vue Components:
  - UserCard - Profile header section
  - UserList - Main listing with search/sort/pagination
  - UserDialog - User details modal

## Project Structure
src/
├── components/
│ ├── UserCard.vue # Profile header component
│ ├── UserDialog.vue # User details modal
│ └── UserList.vue # Main listing with controls
├── pages/
│ └── index.vue # Main page layout


## Setup Instructions

1. Clone the repository:
   ```bash
   git clone [repository-url]
   cd my-project
   continue with the next README for NUXT coonfiguration
