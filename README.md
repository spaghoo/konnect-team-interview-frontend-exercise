# Welcome


## Submission Notes

### Custom Components

#### AddNewServiceButton

this component is a very simple button with no state or logic that just holds its own styling. a stretch goal would be to implement functionality for this button. allowing the user to create new services through a modal form.

#### PaginationButtons

This component is a simple arrow button in a circle for pagination controls. the only state or logic is depending on a passed bool it determines the direction of the arrow. wanted to hand off more logic here from the parent class and it would be a stretch goal but was not able to do it in the time.

#### PaginationNumbers

pagination numbers is a simple component that takes in a few simple pieces of data and displays info about which of the services you are seeing and how many there are total. no real complications outside of computing its various values. this and the buttons comprises the pagination row that controls that function and displays the state of it.

#### ServiceCard

this component is what makes up the bulk of the UI. it takes the data passed from each service and displays it. only logic in this component is that titles are cut off after 25 characters and descriptions after 90. It also has a child component called version bubble that will touch on next.

#### VersionBubble

this is a simple UI component that takes in the amount of versions and displays it. 

#### ServiceCatalog

this is where the bulk of the code is for this screen. it handles most of the state and logic of the functionality. if i were to have one main stretch goal it would be to take this file and do some clean up to make it a little neater and abstract out some functionality to make it more modular.

i think i do a bit too much conditional rendering for the actual catalog as well perhaps. I manage all possible states: data loaded, data is loading, call returned an error and there is no data, search returned no results. the user is notified of each state that it is in at a given time.

the state in this component is the returned services, a few variables for managing pagination, and a few variables for handling search. 

i did a custom pagination solution that is relatively barebones but gets the job done. when you see the 12 results per page (which could be changed by the user very easily if need by) you are viewing a 12 item long slice of the current array of services. of course, that array changes depending on if you are searching or not. the state of your page is preserved throughout a search so if im on page 5 and search something and browse those results,once the search bar is empty again, you are returned to the page you were on before searching. the buttons only allow you to navigate to pages that will have data.

search is done by a simple computed variable that the catalog for loop runs over. for ease, the logic for detecting if the array is the whole set or a subset is done in the computer variable, so only one call is needed in the template of the component. using some simple logic in the set function of the search query i do search debouncing to help with performance. the actual search is a ver simple filter function looking at the names of the services. the search only runs after the user has typed at least 2 letters also to help with performance. i then simply filter over the array of services case insensitive and add matches to the array. it is then returned. to display the 12 items in the catalog it takes a slice of the array depending on what page the user is on.

## Goal

Make this Vue 3 app as close to [this mock](https://www.figma.com/file/zeaWiePnc3OCe34I4oZbzN/Service-Card-List?node-id=0%3A1) as possible while utilizing best-practices, coding standards, and great code to improve the example codebase.

The styling should be responsive and look good at different browser window sizes.

The provided exercise files are a starting point; they have room for improvement. Don't treat the mock as gospel -- if you see things that don't make sense, implement what you think is right.

You may use our component library, [Kongponents](https://beta.kongponents.konghq.com), if desired; however, keep in mind we want to see the code **YOU** can write as well.

### Links

- Figma Mock: <https://www.figma.com/file/zeaWiePnc3OCe34I4oZbzN/Service-Card-List?node-id=0%3A1>
- Kongponents (for Vue 3): <https://beta.kongponents.konghq.com>

## Functional Requirements

- Ability to view the name, a brief description, and versions available for services
- Ability to search services (client-side implementation)
- User can paginate through services (client-side implementation)
- Responsive layout
- Update the `README` in the project to describe your design considerations, assumptions and trade-offs made during this exercise
- The Create Service button and clicks on service cards don't have to be operable -- could do nothing, could open a modal with a message, or could be fully implemented (stretch goal)

## Additional Considerations

- TypeScript
- Tests
- Routing and views (e.g. navigating to a given service from its card)
- Pinia state management
- Other items covered in your Panel 1 interview

## Evaluation

We will review your code to see how you work, how you approach UI, and what tradeoffs you make. Specifically we'll be looking at the following:

- How closely your implementation matches the design
- Code quality, including appropriate componentization and modularity
- Coding practices and industry standards

## How to submit the project

You have up to a week to complete the exercise, but we don't expect you to spend more than a few hours on it.

When it's ready, please send your recruiter a link to the source code in a GitHub repository (no Pull Requests).

---

## Project Setup

```sh
yarn install --frozen-lockfile
```

### Committing Changes

[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)

[Commitizen](https://github.com/commitizen/cz-cli) can be used to to help build and enforce commit messages.

It is __highly recommended__ to use the following command in order to create your commits:

```sh
yarn commit
```

This will trigger the Commitizen interactive prompt for building your commit message.

### Compile and Hot-Reload for Development

Start the backend:

```sh
yarn server
```

Separately, start the frontend:

```sh
yarn dev
```

### Build and Minify for Production

```sh
yarn build
```

### Run Unit Tests with [Cypress Component Testing](https://docs.cypress.io/guides/component-testing/introduction)

```sh
yarn test:unit # or `yarn test:unit:ci` for headless testing
```

### Run End-to-End Tests with [Cypress](https://www.cypress.io/)

```sh
yarn build
yarn test:e2e # or `yarn test:e2e:ci` for headless testing
```
