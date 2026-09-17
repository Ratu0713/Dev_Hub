# MyGit

MyGit is a **Git-like version control system** built with Node.js.
It provides basic repository and version-control operations through a command-line interface (CLI).

The project supports repository initialization, file staging, commits, pushing commits to AWS S3, pulling commits from S3, and reverting to a specific commit.

---

## 🚀 Features

* Initialize a new repository
* Add files to the staging area
* Create commits with commit messages
* Push commits to AWS S3
* Pull commits from AWS S3
* Revert the repository to a specific commit
* Command-line interface using Yargs
* MongoDB connection for backend/server functionality
* Environment variable support using dotenv

---

## 🛠️ Technologies Used

* **Node.js**
* **JavaScript**
* **Yargs** – CLI command handling
* **Express.js** – Server
* **MongoDB**
* **Mongoose** – MongoDB object modeling
* **AWS S3** – Remote commit storage
* **dotenv** – Environment variable management
* **Body-parser** – JSON request parsing
* **CORS** – Cross-Origin Resource Sharing

---

## Project Structure

```text
backend/
├── config/
├── controllers/
├── middleware/
├── models/
├── myGit/
├── routes/
├── .env
├── .gitignore
├── config.json
├── index.js
├── package.json
└── package-lock.json
---

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone <your-github-repository-url>
```

### 2. Go to the project directory

```bash
cd MyGit
```

### 3. Install dependencies

```bash
npm install
```

---
---

# 💻 CLI Commands

MyGit provides the following commands:

```text
start
init
add <file>
commit <message>
push
pull
revert <commitId>
```

---

## 1. Start Server

Starts the Express server and connects to MongoDB.

```bash
node index.js start
```

Expected output:

```text
Database set is done :)
```

---

## 2. Initialize Repository

Creates a new MyGit repository.

```bash
node index.js init
```

This initializes the required repository structure.

Example:

```text
myGit/
├── staging/
└── commits/
```

---

## 3. Add a File

Adds a file to the staging area.

```bash
node index.js add index.js
```

The selected file is copied to the staging area and becomes ready for committing.

Example:

```text
Working Directory
       │
       ▼
    index.js
       │
       │  mygit add
       ▼
   Staging Area
       │
       ▼
myGit/staging/
```

---

## 4. Commit Changes

Creates a new commit from the staged files.

```bash
node index.js commit "Initial commit"
```

A unique commit ID is generated for the commit.

Example:

```text
myGit/
└── commits/
    └── abc123/
        ├── index.js
        └── commit.json
```

The commit stores the files along with commit information such as the commit message and date.

---

## 5. Push Commits

Uploads commits to AWS S3.

```bash
node index.js push
```

The local commit data is stored remotely in an S3 bucket.

```text
Local Repository
      │
      │ push
      ▼
   AWS S3
      │
      ▼
Remote Commits
```

---

## 6. Pull Commits

Downloads commits from AWS S3.

```bash
node index.js pull
```

This retrieves the remote commit data and stores it in the local repository.

```text
AWS S3
  │
  │ pull
  ▼
Local Repository
  │
  ▼
myGit/commits/
```

---

## 7. Revert to a Commit

Reverts the working directory to the state stored in a specific commit.

```bash
node index.js revert <commitId>
```

Example:

```bash
node index.js revert abc123
```

The files from the specified commit are restored to the project directory.

```text
                 Commit
                   │
                   │
                   ▼
          myGit/commits/abc123
                   │
                   │ revert
                   ▼
            Project Directory
```

---

# 🔄 MyGit Workflow

The basic workflow is:

```text
                ┌─────────────┐
                │   mygit     │
                │    init     │
                └──────┬──────┘
                       │
                       ▼
                Working Directory
                       │
                       │ add
                       ▼
                 Staging Area
                       │
                       │ commit
                       ▼
                    Commit
                       │
                       │ push
                       ▼
                   AWS S3
                       │
                       │ pull
                       ▼
              Local Commit Store
                       │
                       │ revert
                       ▼
              Previous Project State
```

---

# 🧠 How the Commands Work

### `init`

Initializes the repository.

### `add`

Moves/copies selected files into the staging area.

### `commit`

Creates a snapshot of the staged files and generates a commit ID.

### `push`

Uploads commits to AWS S3.

### `pull`

Downloads commits from AWS S3.

### `revert`

Restores files from a selected commit.

---

# ☁️ AWS S3 Integration

AWS S3 is used as the **remote storage layer** for commits.

The architecture is:

```text
             MyGit CLI
                 │
        ┌────────┼────────┐
        │        │        │
        ▼        ▼        ▼
      Add     Commit    Revert
                 │
                 ▼
          Local Commits
                 │
                 │ Push
                 ▼
              AWS S3
                 │
                 │ Pull
                 ▼
          Local Repository
```

---

# 🌐 Server

The project also contains an Express.js server.

The server:

* Creates an Express application
* Parses JSON requests
* Connects to MongoDB using Mongoose
* Uses environment variables through dotenv

Example:

```javascript
const app = express();
const port = process.env.PORT || 3000;
```

---

# 📦 Dependencies

Install the required packages using:

```bash
npm install
```

Main dependencies:

```text
express
mongoose
yargs
dotenv
cors
body-parser
```

---

# 🔒 Security

Do not expose sensitive credentials.

Never commit:

```text
.env
AWS access keys
AWS secret keys
MongoDB passwords
```

Use `.gitignore`:

```text
node_modules/
.env
```

---

# 🚧 Future Improvements

Possible future improvements include:

* Recursive directory support
* Better Git-like revert functionality
* Branch support
* Diff between commits
* Delete detection during revert
* Commit history command
* Status command
* Remote repository support
* Authentication
* Web-based repository interface
* Conflict detection and resolution

---

# 👨‍💻 Author

**Ratul Sarkar**

B.Tech Computer Science & Engineering

---

## 📄 License

This project is created for educational and development purposes.
