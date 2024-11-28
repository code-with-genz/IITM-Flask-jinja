# IITM-Flask-jinja
This is my First Project in Flask framework

## Topic :  A to Z Service Management App

## Description
This project aims to build a Service Management App using knowledge from Modern App Development 1. The app is named **A to Z Service Management App**.

### Technology Used
1. **SQLite – Python (sqlite3 and Flask)**:  
   - SQLite was chosen for binding data to endpoints over SQLAlchemy.
   - Libraries:
     - **sqlite3**: Connects to the SQLite database.
     - **Flask**: A lightweight, open-source Python-based web framework. Includes:
       - `Flask`: Handles HTTP requests (e.g., RESTful APIs like GET, POST, etc.).
       - `render_template`: Renders Jinja2 templates (HTML pages).
       - `request`: Captures data and query parameters from the user side.
       - `redirect`: Redirects the browser to a different URL.
       - `url_for`: Routes to a specific URL by referring to a function name.
       - `send_file`: Sends files (e.g., JPG, PDF) from the server to the client for download.
       - `send_from_directory`: Displays backend files (e.g., JPG, PNG) on the frontend.
2. **Jinja2 and Bootstrap**:
   - Jinja2: For UI templating.
   - Bootstrap: For better CSS and built-in JavaScript functionalities like dropdowns.

---

## Functionalities
1. **Registration**: Separate pages for Customer, Admin, and Professionals.
2. **Login**: Separate login pages for Customer, Admin, and Professionals.
3. **UUID System**: Each user has a unique ID (UUID), and dashboards are accessible only via UUID.
4. **Dashboards**:
   - Three types: Customer, Professional, and Admin.
   - Each dashboard includes features specific to the user role.
5. **Service Management**:
   - Customers can create new service requests and track their status.
   - Professionals can view and accept/reject service requests for services they are registered for (e.g., a hairdresser sees only haircut requests).
6. **Data Flow**:
   - Information is sent from the client side to the backend server.
   - Some data is transmitted via forms, others as parameters.
7. **Admin Features**:
   - Create and price new services.
   - View all information about new service requests.
8. **Search Functionality**:
   - Common for all users (Admin, Customer, Professional) with user-specific search parameters.
9. **Professional Profiles**:
   - Professionals can view their profile and information.
   - Service requests are only visible to verified professionals.

---

```mermaid
erDiagram
    admin {
        TEXT email PK "Primary Key, unique email"
        TEXT password "Admin password"
    }
    customer {
        TEXT id PK "Primary Key, unique customer ID"
        TEXT full_name "Customer's full name"
        TEXT email "Unique email for customer"
        TEXT password "Customer password"
        TEXT mb_no "Customer mobile number"
        TEXT address "Customer address"
        TEXT city "Customer city"
        TEXT pincode "Customer pincode"
        INTEGER block "Block status (default: 0)"
    }
    professional {
        TEXT id PK "Primary Key, unique professional ID"
        TEXT full_name "Professional's full name"
        TEXT email "Professional's email"
        TEXT mb_no "Professional's mobile number"
        TEXT password "Professional's password"
        TEXT address "Professional's address"
        TEXT city "Professional's city"
        TEXT pincode "Professional's pincode"
        BLOB id_proof "ID proof as a binary file"
        TEXT main_service_type "Main service type"
        TEXT speciality "Specialized service"
        INTEGER experience "Years of experience"
        INTEGER rating "Rating (optional)"
        INTEGER block "Block status (default: 0)"
        INTEGER verified "Verification status (default: 0)"
    }
    service {
        TEXT id PK "Primary Key, unique service ID"
        TEXT name_or_type "Service name or type"
        TEXT sub_type "Service sub-type"
        TEXT description "Service description"
        INTEGER base_price "Base price for the service"
    }
    service_inti_or_close {
        TEXT service_init_id PK "Primary Key, unique service initialization ID"
        TEXT customer_id FK "Foreign Key: references customer.id"
        TEXT customer_name "Customer's name"
        TEXT customer_mobile "Customer's mobile number"
        TEXT customer_address "Customer's address"
        TEXT customer_city "Customer's city"
        TEXT customer_pincode "Customer's pincode"
        TEXT service_id FK "Foreign Key: references service.id"
        TEXT service_main "Main service type"
        TEXT service_sub_type "Service sub-type"
        TEXT customer_status "Customer's status for the service"
        INTEGER price "Service price"
        TEXT accepted_prof_id "Professional ID who accepted the request"
        TEXT accepted_prof_name "Professional's name who accepted the request"
        TEXT accepted_prof_number "Professional's contact number"
        TEXT reject_prof_id "ID of professional(s) who rejected"
        TEXT professional_status "Professional's status"
        DATETIME date "Date of service initiation or closure"
    }

    customer ||--o{ service_inti_or_close : "makes"
    professional ||--o{ service_inti_or_close : "handles"
    service ||--o{ service_inti_or_close : "requested"
```

