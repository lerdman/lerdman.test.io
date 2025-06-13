# lerdman.test.io
test website
{
  "name": "psychopy-web-tasks",
  "version": "1.0.0",
  "description": "A web application for uploading and sharing PsychoPy tasks.",
  "main": "src/app.js",
  "scripts": {
    "start": "webpack serve --mode development",
    "build": "webpack --mode production",
    "test": "jest"
  },
  "keywords": [
    "psychopy",
    "web",
    "tasks",
    "upload"
  ],
  "author": "Your Name",
  "license": "MIT",
  "dependencies": {
    "react": "^17.0.2",
    "react-dom": "^17.0.2",
    "react-router-dom": "^5.2.0"
  },
  "devDependencies": {
    "webpack": "^5.24.2",
    "webpack-cli": "^4.5.0",
    "webpack-dev-server": "^3.11.2",
    "babel-loader": "^8.2.2",
    "jest": "^26.6.0"
  }
npx create-react-app psychopy-web-tasks
cd psychopy-web-npx create-react-app psychopy-web-tasks
cd psychopy-wmkdir -p src/components src/pages src/util{
  "name": "psychopy-web-tasks",
  "version": "1.0.0",
  "private": true,
  "dependencies": {
    "react": "^18.0.0",
    "react-dom": "^18.0.0",
    "react-scripts": "5.0.1"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  }
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>PsychoPy Web Tasks</title>
    <meta name="viewport" content="width=device-width, initial-scale=1" />
  </head>
  <body>
    <div id="root"></div>
  </body>
</html><!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PsychoPy Web Tasks</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div id="root"></div>
    <script src="app.js"></script>
</body>
</html>
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<App />);function s(e){document.readyState==="loading"||document.readyState==="uninitialized"?document.addEventListener("DOMContentLoaded",e):e()}var d=acquireVsCodeApi();function l(){let e=document.getElementById("simple-browser-settings");if(e){let t=e.getAttribute("data-settings");if(t)return JSON.parse(t)}throw new Error("Could not load settings")}var r=l(),c=document.querySelector("iframe"),o=document.querySelector(".header"),a=o.querySelector(".url-input"),m=o.querySelector(".forward-button"),g=o.querySelector(".back-button"),L=o.querySelector(".reload-button"),E=o.querySelector(".open-external-button");window.addEventListener("message",e=>{switch(e.data.type){case"focus":{c.focus();break}case"didChangeFocusLockIndicatorEnabled":{i(e.data.enabled);break}}});s(()=>{setInterval(()=>{let t=document.activeElement?.tagName==="IFRAME";document.body.classList.toggle("iframe-focused",t)},50),c.addEventListener("load",()=>{}),a.addEventListener("change",t=>{let n=t.target.value;e(n)}),m.addEventListener("click",()=>{history.forward()}),g.addEventListener("click",()=>{history.back()}),E.addEventListener("click",()=>{d.postMessage({type:"openExternal",url:a.value})}),L.addEventListener("click",()=>{e(a.value)}),e(r.url),a.value=r.url,i(r.focusLockIndicatorEnabled);function e(t){try{let n=new URL(t),u=new URLSearchParams(location.search);n.searchParams.append("id",u.get("id")),n.searchParams.append("vscodeBrowserReqId",Date.now().toString()),c.src=n.toString()}catch{c.src=t}d.setState({url:t})}});function i(e){document.body.classList.toggle("enable-focus-lock-indicator",e)}
import React from "react";
import Home from "./pages/Home";

function App() {
  return (
    <div>
      <h1>PsychoPy Web Tasks</h1>
      <Home />
    </div>
  );
}

export default App;import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
import Home from './pages/Home';
import TaskUploader from './components/TaskUploader';

const App = () => {
    return (
        <Router>
            <Switch>
                <Route path="/" exact component={Home} />
                <Route path="/upload" component={TaskUploader} />
            </Switch>
        </Router>
    );
};

ReactDOM.render(<App />, document.getElementById('root'));

import React from "react";
import TaskUploader from "../components/TaskUploader";

function Home() {
  return (
    <div>
      <h2>Upload a PsychoPy Task</h2>
      <TaskUploader />
    </div>
  );
}

export default Home;import React from 'react';
import TaskUploader from '../components/TaskUploader';

const Home = () => {
    return (
        <div>
            <h1>Welcome to the PsychoPy Task Repository</h1>
            <p>Upload your PsychoPy task files and share them with the community.</p>
            <TaskUploader />
            {/* Additional components or lists of uploaded tasks can be added here */}
        </div>
    );
};

export default Home;

import React, { useState } from "react";

function TaskUploader() {
  const [file, setFile] = useState(null);

  const handleFileChange = (e) => {
    setFile(e.target.files[0]);
  };

  const handleUpload = (e) => {
    e.preventDefault();
    if (file) {
      alert(`File "${file.name}" selected! (Parsing not implemented)`);
      // Here you would add code to parse and display the PsychoPy file
    }
  };

  return (
    <form onSubmit={handleUpload}>
      <input type="file" accept=".psyexp,.py" onChange={handleFileChange} />
      <button type="submit">Upload</button>
    </form>
  );
}

export default TaskUploader;class TaskUploader extends React.Component {
    constructor(props) {
        super(props);
        this.state = {
            selectedFile: null,
            uploadStatus: ''
        };
    }

    handleFileChange = (event) => {
        this.setState({ selectedFile: event.target.files[0] });
    }

    handleUpload = () => {
        const { selectedFile } = this.state;
        if (selectedFile) {
            // Logic to handle file upload goes here
            this.setState({ uploadStatus: 'File uploaded successfully!' });
        } else {
            this.setState({ uploadStatus: 'Please select a file to upload.' });
        }
    }

    render() {
        return (
            <div>
                <h2>Upload PsychoPy Task</h2>
                <input type="file" accept=".psy" onChange={this.handleFileChange} />
                <button onClick={this.handleUpload}>Upload</button>
                {this.state.uploadStatus && <p>{this.state.uploadStatus}</p>}
            </div>
        );
    }
}

export default TaskUploader;
// PsychoPy file parsing logic will go here.export function parsePsychoPyFile(fileContent) {
    // Implement parsing logic for PsychoPy file content
    const parsedData = {};
    
    // Example parsing logic (to be customized based on PsychoPy file structure)
    const lines = fileContent.split('\n');
    lines.forEach(line => {
        if (line.startsWith('Task:')) {
            parsedData.taskName = line.split(':')[1].trim();
        } else if (line.startsWith('Description:')) {
            parsedData.description = line.split(':')[1].trim();
        }
        // Add more parsing rules as needed
    });

    return parsedData;
}

export function validatePsychoPyFile(fileContent) {
    // Implement validation logic for PsychoPy file content
    const isValid = fileContent.includes('Task:') && fileContent.includes('Description:');
    return isValid;
}# PsychoPy Web Tasks

A simple React app to upload and display PsychoPy task files.
{
  "name": "psychopy-web-tasks",
  "version": "1.0.0",
  "description": "A web application for uploading and sharing PsychoPy tasks.",
  "main": "src/app.js",
  "scripts": {
    "start": "webpack serve --mode development",
    "build": "webpack --mode production",
    "test": "jest"
  },
  "keywords": [
    "psychopy",
    "web",
    "tasks",
    "upload"
  ],
  "author": "Your Name",
  "license": "MIT",
  "dependencies": {
    "react": "^17.0.2",
    "react-dom": "^17.0.2",
    "react-router-dom": "^5.2.0"
  },
  "devDependencies": {
    "webpack": "^5.24.2",
    "webpack-cli": "^4.5.0",
    "webpack-dev-server": "^3.11.2",
    "babel-loader": "^8.2.2",
    "jest": "^26.6.0"
  }
npx create-react-app psychopy-web-tasks
cd psychopy-web-npx create-react-app psychopy-web-tasks
cd psychopy-wmkdir -p src/components src/pages src/util{
  "name": "psychopy-web-tasks",
  "version": "1.0.0",
  "private": true,
  "dependencies": {
    "react": "^18.0.0",
    "react-dom": "^18.0.0",
    "react-scripts": "5.0.1"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  }
}s
