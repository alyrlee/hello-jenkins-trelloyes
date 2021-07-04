# hello-jenkins-trelloyes

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.<br>
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.<br>
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.<br>
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.<br>
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.<br>
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (Webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

##hello-jenkins-server
Backend for supporting arbitrary Trello front end clients

Note that this is not meant to be a robust, full-fledged Trello app backend. Its sole purpose is to provide a backend that can be run locally in order to demo front end apps that implement a UI for it.

To get it running
Clone this repo
cd into it
Run npm install
Run npm start
By default, this will run the server on port 8080. And it will expect clients coming from localhost:3000. If you want non-default settings, set environment variables for CLIENT_ORIGIN and SERVER_PORT before running npm start.

Seed data
Whenever you start the server, a board will be pre-loaded via a data fixture, which should make your life easier as you develop a GUI client. Specifically, you can assume that the board represented in the boards.json file will be available each time the server starts.

More details on what it do
This server supports basic CRUD ops for boards, lists, and cards.

The underlying app is extremely limited, and will not support the full range of features that real Trello supports. It supports creating, reading, updating, and deleting boards, lists, and cards.

It does not support re-ordering lists and cards, or anything beyond board names, list titles, and card text.

Here are some oddities and guidelines:

"Ceci n'est pas une vrai application" - specifically, it's got a volatile, in memory data store. Persistence you want? Look elsewhere.
CRUD ops for boards
When you read a board, you get all child components (i.e., any lists and their cards)
When you create a board, you only get to give it a name, and you cannot also create child lists and cards as part of same op.
When you delete a board, you delete all its child components
CRUD ops for lists
When you read a list, you get all child cards
When you create a list, you only get to give it a title, and you cannot also create child cards and cards as part of same op.
When you create a list, via the URL structure, you create it as a child of an existing board (i.e., POST /api/board/{{someBoardId}}/list)
When you update, read, or delete a list, you do so via a direct path to the list (e.g., DELETE /api/list/{{someListId}})
When you delete a list, you delete its card children, if any
CRUD ops for cards
When you create a card, you only get to give it text
When you create a card, via the URL structure, you create it as a child of an existing list (i.e., POST /api/list/{{someListid}/card)
When you update, read, or delete a card, you do so via a direct path to the list (e.g., DELETE /api/card/{{someCardId}})