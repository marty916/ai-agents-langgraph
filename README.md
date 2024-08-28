# Project Setup Instructions

Welcome to the course! This guide will help you set up the project structure for your final project, ensuring a clean separation between the front-end (ReactJS) and back-end (Python) code. Follow the steps below to create and configure your project environment.

## Project Folder Structure

The following is the recommended folder structure for the course project:

## Client Folder Structure

- **public/**: Contains public assets like the main HTML file, images, and other static files.
- **src/**: The source code for the ReactJS application.
  - **components/**: Contains reusable React components (e.g., buttons, form elements).
  - **pages/**: Contains page components for different routes (e.g., Home, About).
  - **services/**: Houses API service functions that communicate with the Python backend.
  - **styles/**: Contains CSS and styling files.
  - **App.js**: The main application component.
  - **index.js**: The entry point for the React application, where the app is rendered.

## Server Folder Structure

- **app/**: Main directory for backend application logic.
  - **api/**: Contains API endpoints (e.g., REST or GraphQL).
  - **models/**: Houses data models and schema definitions.
  - **services/**: Contains business logic and service functions.
  - **utils/**: Utility functions and helper modules.
  - **main.py**: The entry point for the backend server.
- **requirements.txt**: Lists Python dependencies.
- **config/**: Configuration files (e.g., for environment variables, database connections).

## Additional Files

- **README.md**: Documentation for the project, including setup instructions, usage, and contribution guidelines.
- **.gitignore**: Specifies files and directories to be ignored by git,


## Step-by-Step Setup Instructions

### 1. **Create the Project Root Directory**

1. Open a terminal or command prompt.
2. Create the main project directory and navigate into it:

```bash
mkdir project-root
cd project-root
```
### 2. Set Up the Client (ReactJS) Folder

```bash
mkdir client
cd client
npx create-react-app .
mkdir src/components src/pages src/service src/styles
```
### 3. Set Up the Server (Python) Folder
1. Go back to the root directory

```bash
cd ..
mkdir server
cd server
```
2. Set up virtual environment

```bash
python3 -m venv venv
source venv\bin\activate # For Windows venv\Scripts\activate
``` 
3. Create the folder structure for the backend

```bash
mkdir app app/api app/models app/service app/utils config
touch app/main.py requirements.txt # For Windows: echo. > app\main.py
                                   #              echo. > requirements.txt
```
4. Open the `requirements.txt` file and list the Python dependencies
```bash
fastapi
uvicorn
pydantic
requests
```
5. Install the dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure the Backend Server
1. Open `main.py` in teh `app` folder and set up a basic FastAPI server

```python
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

app = FastAPI()

# Configure CORS
app.add_middleware(
    CORSMiddleware,
    allow_origins=["http://localhost:3000"],  # React app URL
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

@app.get("/")
def read_root():
    return {"Hello": "Hello World"}
```
2. Run the backend server to test it

```bash
uvicorn app.main:app --reload
```
3. Open a browser and navigate to `http://127.0.0.1:8000` to verify teh server is running

### 5. Connect the Client and Server
1. Use the `services` folder in the ReactJS `client` to create API service functions to communicate with the backend.

```javascript
// src/services/api.js
import axios from 'axios';

const API_URL = 'http://127.0.0.1:8000';

export const getHelloWorld = async () => {
    try {
        const response = await axios.get(`${API_URL}/`);
        return response.data;
    } catch (error) {
        console.error("Error fetching data", error);
        return null;
    }
};
```

### 6. Final Steps
1. Setup .gitignore for the server

```bash
touch server/.gitignore  #Windows echo. > server/.gitignore
```
2. Add this to your server .gitignore
```bash
# Server
server/venv
server/__pycache__

# Environment
.env
```
3. Setup .gitignore for the client

```bash
touch client/.gitignore  #Windows echo. > client/.gitignore
```
2. Add this to your client .gitignore
```bash
# Client
client/node_modules
client/build

# Environment
.env
```






