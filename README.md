Assignment Submission Portal

This is a backend system for managing assignment submissions between users and admins.

Features:
- User registration and authentication
- Admin registration and authentication
- Assignment creation and submission
- Assignment review and status updates by admins

Prerequisites:
- Node.js (v14 or later)
- MongoDB (v4 or later)
- Postman (for API testing)

Setup and Running Instructions:

1. Clone the repository:
   git clone https://github.com/yourusername/assignment-submission-portal.git
   cd assignment-submission-portal

2. Install dependencies:
   npm install

3. Set up environment variables:
   Create a .env file in the root directory with the following content:
   MONGODB_URI=mongodb://localhost:27017/assignment_portal
   JWT_SECRET=your_very_long_and_secure_random_string
   PORT=3000
   
   Replace 'your_very_long_and_secure_random_string' with an actual secure random string.

4. Ensure MongoDB is running on your system.

5. Start the server:
   npm start

   You should see a message indicating that the server is running and connected to MongoDB.

Testing with Postman:

1. Open Postman and create a new collection named "Assignment Submission Portal"

2. Add the following requests to your collection:

   a. Register User:
      - Method: POST
      - URL: http://localhost:3000/api/users/register
      - Headers: Content-Type: application/json
      - Body (raw JSON):
        {
            "username": "testuser",
            "password": "testpassword"
        }

   b. User Login:
      - Method: POST
      - URL: http://localhost:3000/api/users/login
      - Headers: Content-Type: application/json
      - Body (raw JSON):
        {
            "username": "testuser",
            "password": "testpassword"
        }

   c. Upload Assignment (requires auth token from login):
      - Method: POST
      - URL: http://localhost:3000/api/users/upload
      - Headers: 
        Content-Type: application/json
        Authorization: Bearer <paste_token_here>
      - Body (raw JSON):
        {
            "task": "Complete assignment 1",
            "admin": "<admin_id_here>"
        }

   d. Register Admin:
      - Method: POST
      - URL: http://localhost:3000/api/admins/register
      - Headers: Content-Type: application/json
      - Body (raw JSON):
        {
            "username": "adminuser",
            "password": "adminpassword"
        }

   e. Admin Login:
      - Method: POST
      - URL: http://localhost:3000/api/admins/login
      - Headers: Content-Type: application/json
      - Body (raw JSON):
        {
            "username": "adminuser",
            "password": "adminpassword"
        }

   f. Accept Assignment (requires admin auth token):
      - Method: POST
      - URL: http://localhost:3000/api/admins/assignments/<assignment_id>/accept
      - Headers: 
        Content-Type: application/json
        Authorization: Bearer <paste_admin_token_here>

3. Run these requests in order, replacing <paste_token_here>, <admin_id_here>, <assignment_id>, and <paste_admin_token_here> with actual values obtained during testing.

Troubleshooting:
- If you encounter a "MongoDB connection error", ensure that MongoDB is running and that the MONGODB_URI in your .env file is correct.
- If you see "Port already in use" error, change the PORT number in your .env file.
- For any "Module not found" errors, try deleting the node_modules folder and running npm install again.
- If you get authentication errors in Postman, ensure you're using the correct and up-to-date token in the Authorization header.

Security Notes:
- Never commit your .env file to version control.
- In a production environment, ensure you're using HTTPS and have proper security measures in place.

API Endpoints:

Users:
- POST /api/users/register - Register a new user
- POST /api/users/login - User login
- POST /api/users/upload - Upload a new assignment (requires authentication)
- GET /api/users/admins - Get list of admins (requires authentication)

Admins:
- POST /api/admins/register - Register a new admin
- POST /api/admins/login - Admin login
- GET /api/admins/assignments - Get assignments for admin (requires authentication)
- POST /api/admins/assignments/:id/accept - Accept an assignment (requires authentication)
- POST /api/admins/assignments/:id/reject - Reject an assignment (requires authentication)

Contributing:
Please read CONTRIBUTING.md for details on our code of conduct, and the process for submitting pull requests.

License:
This project is licensed under the MIT License - see the LICENSE.md file for details.
