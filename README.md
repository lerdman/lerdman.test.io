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

function App() {
  return (
    <div>
      <nav style={{ margin: '1rem' }}>
        <NavLink to="/" style={{ marginRight: '1rem' }}>
          Home
        </NavLink>
        <NavLink to="/upload">
          Upload Task
        </NavLink>
      </nav>

      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/upload" element={<TaskUploader />} />
      </Routes>
    </div>
  );
}

export default App;
import React from 'react';
import { Link } from 'react-router-dom';

function Home() {
  return (
    <main style={{ padding: '1rem' }}>
      <h1>PsychoPy Web Tasks</h1>
      <p>Welcome to the PsychoPy Task Repository.</p>
      <Link to="/upload">Upload your PsychoPy task</Link>
    </main>
  );
}

export default Home;
import React, { useState } from 'react';

function TaskUploader() {
  const [file, setFile] = useState(null);
  const [status, setStatus] = useState('');

  const handleFileChange = (e) => {
    setFile(e.target.files[0]);
    setStatus('');
  };

  const handleUpload = async (e) => {
    e.preventDefault();
    if (!file) {
      setStatus('Please select a file to upload.');
      return;
    }

    try {
      const content = await file.text();
      // TODO: parse & validate content
      setStatus(`File "${file.name}" loaded. (Parsing not yet implemented)`);
    } catch (err) {
      setStatus('Error reading file.');
    }
  };

  return (
    <section style={{ padding: '1rem' }}>
      <h2>Upload PsychoPy Task</h2>
      <form onSubmit={handleUpload}>
        <input
          type="file"
          accept=".psy,.py"
          onChange={handleFileChange}
        />
        <button type="submit" style={{ marginLeft: '0.5rem' }}>
          Upload
        </button>
      </form>
      {status && <p>{status}</p>}
    </section>
  );
}

export default TaskUploader;
npm start


