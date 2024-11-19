# Folder Structure

1. Initialize a Project:

- Create a folder named using your surname (e.g., Smith_API_Project).
- Initialize a Node.js project

```bash
npm init -y
```

2. Install Required Dependencies:

```bash
npm i express nodemon dotenv
```

3. Update `package.json` Scripts:

Add the following `scripts` to run the server easily

```bash
"dev": "nodemon index.js"
```

4 Create Essential Files:

.`env`: To store environment variables.
.`gitignore`: To exclude sensitive and unnecessary files like `.env` and `node_modules`.

## Folder and File Structure

Your project should look like this:

```bash
Smith_API_Project/
├── node_modules/
├── controllers/
│   └── itemController.js
├── models/
│   └── itemModel.js
├── routes/
│   └── itemRoutes.js
├── .env
├── .gitignore
├── index.js
├── package.json
└── package-lock.json
```
