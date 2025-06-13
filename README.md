git clone https://github.com/lerdman/psychopy-web-tasks.git
cd psychopy-web-tasks
npm install
npm start
{
  "homepage": "https://lerdman.github.io/psychopy-web-tasks",
  "scripts": {
    "start":     "react-scripts start",
    "build":     "react-scripts build",
    "predeploy": "npm run build",
    "deploy":    "gh-pages -d build"
  }
}
npm install --save-dev gh-pages
npm run deploy
# or
yarn add --dev gh-pages
yarn deploy
npm install react-router-dom@6
# or
yarn add react-router-dom@6
psychopy-web-tasks/
├── public/
│   └── index.html       # Single HTML page
└── src/
    ├── index.js         # App entry
    ├── App.js           # Router & layout
    ├── pages/
    │   └── Home.js      # Homepage
    └── components/
        ├── TaskUploader.js  # File upload form
        └── TaskList.js      # (Future) display uploaded tasks
