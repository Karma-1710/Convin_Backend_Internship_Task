# Convin_Backend_Internship_Task (Daily Expense Sharing Application)

### Description
This documentation provides an overview and setup instructions for the Convin backend intern task, which involves building a Daily Expenses Sharing Application using Python Django Framework and PostgreSQL as the database.

### Prerequisites
- Python 3.11.5
- PostgreSQL (with pgAdmin for management)
- Git
- Postman

### Setup Instructions

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/Karma-1710/Convin_Backend_Internship_Task.git
   cd Convin_Backend_Internship_Task

2. **Set Up Virtual Environment:**
   ```bash
   python -m venv env

3. **Activate the Environment:**
   ```bash
   .\env\Scripts\activate

4. **Install the dependencies:**
   ```bash
   pip install -r requirements.txt

5. **Database Setup:**
    - Open pgAdmin and ensure it is running on localhost port 5432.
    - In Servers, create a new Database named ConvinDB.
    - Create a Login/Group Role named ConvinUser with password 'convin' and grant all privileges including:
         - Can Login
         - SuperUser
         - Create roles
         - Create databases

   In case of Custom DB or User name, Make sure to update in .env file in Backend directory
   ```bash
   DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': os.getenv('DB_NAME'),
        'USER': os.getenv('DB_USER'),
        'PASSWORD': os.getenv('DB_PASSWORD'),
        'HOST': os.getenv('DB_HOST'),
        'PORT': os.getenv('DB_PORT'),
    }
   }

6. **Migrate Database Changes:**
   ```bash
   cd backend
   python manage.py makemigrations
   python manage.py migrate

7. **Run Django Server:**
   ```bash
   python manage.py runserver
   
### The server will be accessible at http://localhost:8000.

## API Endpoints

1. User Registration
   - POST '/api/user/register/'
     ```bash
     {
      "email": "test@gmail.com",
      "name": "Test",
      "mobile": "0000099999",
      "password": "testpassword"
      }

2. User Authentication
    - POST '/api/token/' (Get the Bearer Access Token from here using Postman)
      ```bash
      {
      "email": "test@gmail.com",
      "password": "testpassword"
      }
    - POST '/api/token/refresh/'
      
3. User Management
    - GET '/api/users/'
    - POST '/api/user/getbyemail/'
  
4. Expense Management
     - POST '/api/create-expense/' (Protected Route - Bearer Token required, Copy the Access token and paste it into Authorization Tab inside Token)
         - equal split method
           ```bash
           {
            "amount": "100.00",
            "title": "Equal Split Expense",
            "description": "Example expense with equal split method",
            "split_method": "equal"
           }
        - exact split method
          ```bash
          {
            "amount": "200.00",
            "title": "Exact Split Expense",
            "description": "Example expense with exact split method",
            "split_method": "exact",
            "exact_splits": [
                 {"user": 1, "split_amount": "50.00"},
                 {"user": 2, "split_amount": "100.00"},
                 {"user": 3, "split_amount": "50.00"}
            ]
          }

       - percentage split method
         ```bash
           {
            "amount": "500.00",
            "title": "Percentage Split Expense",
            "description": "Example expense with percentage split method",
            "split_method": "percentage",
            "percentage_splits": [
                 {"user": 1, "percentage": "30.0"},
                 {"user": 2, "percentage": "40.0"},
                 {"user": 3, "percentage": "30.0"}
             ]
          }
5. Balance Sheet
      - GET /api/balance-sheet/  (Protected Route - Bearer Token required, Copy the Access token and paste it into Authorization Tab inside Token)

6. User Expenses
      - GET /api/user/current-user-expenses/  (Protected Route - Bearer Token required, Copy the Access token and paste it into Authorization Tab inside Token)

7. Other Endpoints
      - GET /api/get-all-expenses/
      - GET /api/user/<int:user_id>/expenses/
  
## Additional Features:
- Comprehensive API Documentation
- Downloadable Balance Sheets
- User Authentication and Authorization
- Integration with PostgreSQL for robust data management
- Optimized Streaming response for large datasets in Creation of balance sheets

8. ## Run Test Cases:
   To run the test cases, execute the following commands while in the virtual environment:
   ```bash
   cd backend
   python manage.py test api

## ER DIAGRAM

![ERD](https://github.com/user-attachments/assets/d10a4c4d-ea55-4e15-8e91-0020db461930)

# Conclusion
This documentation outlines the setup, API endpoints, and features of the Convin backend intern task for a Daily Expenses Sharing Application.
