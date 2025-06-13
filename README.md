# Replace <your-github-username> with your GitHub username
git clone https://github.com/lerdman//psychopy-web-tasks.git
cd psychopy-web-tasks
npm install
# or
yarn
"homepage": "https://<your-github-username>.github.io/psychopy-web-tasks"
"scripts": {
  "start": "react-scripts start",
  "build": "react-scripts build",
  "predeploy": "npm run build",
  "deploy": "gh-pages -d build"
}
npm install --save-dev gh-pages
# or

### 4. Run Locally

```bash
npm start
# or
yarn start
npm run deploy
# or
yarn deploy
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
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>PsychoPy Web Tasks</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
import React from 'react';
import ReactDOM from 'react-dom/client';
import { BrowserRouter } from 'react-router-dom';
import App from './App';

const root = ReactDOM.createRoot(
  document.getElementById('root')
);
root.render(
  <React.StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </React.StrictMode>
);
import React from 'react';
import { Routes, Route, NavLink } from 'react-router-dom';
import Home from './pages/Home';
import TaskUploader from './components/TaskUploader';

export default function App() {
  return (
    <div>
      <nav style={{ padding: '1rem' }}>
        <NavLink to="/" style={{ marginRight: '1rem' }}>Home</NavLink>
        <NavLink to="/upload">Upload Task</NavLink>
      </nav>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/upload" element={<TaskUploader />} />
      </Routes>
    </div>
  );
}
import React from 'react';
import { Link } from 'react-router-dom';

export default function Home() {
  return (
    <main style={{ padding: '1rem' }}>
      <h1>PsychoPy Web Tasks</h1>
      <p>Upload and share your PsychoPy experiments.</p>
      <Link to="/upload">Go to Upload</Link>
    </main>
  );
}
import React, { useState } from 'react';

export default function TaskUploader() {
  const [file, setFile] = useState(null);
  const [message, setMessage] = useState('');

  const onFileChange = (e) => {
    setFile(e.target.files[0]);
    setMessage('');
  };

  const onUpload = async (e) => {
    e.preventDefault();
    if (!file) {
      setMessage('Select a .psy or .py file first.');
      return;
    }
    try {
      const text = await file.text();
      // TODO: Save `text` to localStorage or a backend
      setMessage(`Loaded: ${file.name}`);
    } catch {
      setMessage('Failed to read file.');
    }
  };

  return (
    <section style={{ padding: '1rem' }}>
      <h2>Upload PsychoPy Task</h2>
      <form onSubmit={onUpload}>
        <input type="file" accept=".psy,.py" onChange={onFileChange} />
        <button type="submit" style={{ marginLeft: '0.5rem' }}>Upload</button>
      </form>
      {message && <p>{message}</p>}
    </section>
  );
}
