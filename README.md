# Sklep Jasia (Johnny's shop) App

This is a very simple app created as a speed run deliberately as a recruitment task. The task was to create an application for managing the stock of a little shop, enabling the admin to delete and add new positions, and for users to filter the results - just in 5 hours.

## Functionality

### Authentication and authorization
Only the admin can alter the database. In the top right corner there is an input enabling to log in (default password is 1234, which is stored in separate file - passwords.js). 

### Database
As the time was crucial in this task, I have decided not to integrate any external database, nor to create any server-side one. The database is client-side only and does not use the local storage, so it disappears after every refresh.

### Filters
The user may filter the results by every possible category, such as term, mounting method or price. The results may also be sorted.

### Creation
After succesfully logging in, admin may add new positions using provided form, which controls the input and enables creating new categories.

### Currency selector
As a bonus point, I have implemented currency selector, which dynamically calculates products' prices. It uses third-party API once the App component is mounted and fetches current conversion ratios.

## Colors, graphics, responsiveness
The logo was designed and drawn by my wife, the layout is meant to be simple and a little bit retro. App is suited to be run on mobile devices

## Frameworks and APIs

The app is written using only pure Vue.js

### Check it out

Currently the website is deployed here: https://domki-z-lasu.web.app
