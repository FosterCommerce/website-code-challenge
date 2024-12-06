# Foster Comerce: PHP-based Website Code Challenge

## Overview

For this assessment, you’ll be building a web-based customer relationship management system.

There are two CSV files which you will use to seed your database:
- [customers.csv](./customers.csv)
- [purchase_history.csv](./purchase_history.csv)

You are free to approach this assessment in any way you choose, but please ensure the steps for reviewing your solution are clearly outlined.

You may use packages that assist in development (e.g., CSV parsing), but avoid using packages that directly solve the challenge requirements.

## Deliverables

- A GitHub repository for your completed solution.
    - If you’re uncomfortable creating a public one, you can create a private repository and add our reviewers GitHub accounts (we'll provide you with their usernames).
- Instructions on how we can get the project up and running locally.
    - Include any environment variables which might be required
    - **NB:** It should be possible to set up the application *without* importing a database dump.
- A short, 10-minute or less screen-recording walking us through your solution.
    - In addition, code should be heavily commented to walk reviewers through the solution.

## Framework

- You may use any PHP web framework you’re comfortable with to complete this assessment (We prefer CraftCMS/Yii2 or Laravel) or none at all, it’s up to you.
- Should you choose to a REST API, include Swagger/OpenAPI docs and UI _or_ a [Bruno](https://www.usebruno.com/) collection for easier reviewing.
- The standards and best practices for your framework of choice should be followed.

### Frontend

- For styling your solution, Tailwind CSS must be used.
- Any interactivity should use Alpine.js.
  - Framework-specific implementations are fine too, for example:
    - [Sprig](https://putyourlightson.com/plugins/sprig) for Craft CMS websites
    - [Livewire](https://livewire.laravel.com/) for Laravel apps

## Database Setup

- Use any database that can be easily set up in a non-Windows environment (e.g., using ddev or Docker Compose). Databases such as SQLite, MySQL, or others are compatible.

## Requirements

Each item represents a new requirement, simulating a scenario where tasks evolve and build upon each other. Earlier tasks may lack the context or details introduced in later ones.

1. **Validate, sanitize and import customer data**
    1. Validate and sanitize
        - Before we can import data, we need to ensure that customer data is in the correct format.
        - Ensure the customer data is in the correct format before importing it
        - Create some way to
            - Validate a customer record
                - `name` should only contain alphabetic characters
                - `email` should follow standard email format.
                - `phone_number` should match the pattern `XXX-XXX-XXXX`.
                - `created_at` date should be in `YYYY-MM-DD` format.
            - Format a customer record
                - `email` must be converted to lowercase.
        - Note that the CSV data provided is already valid and formatted correctly.
    2. **Import data**
        - Create two tables: `customers` and `purchase_history`.
            - customers table:
                - Fields:
                    - `id` (primary key),
                    - `name`
                    - `email` (unique)
                    - `phone_number`
                    - `created_at`
            - purchase_history table:
                - Fields:
                    - `id` (primary key)
                    - `customer_id` (foreign key)
                    - `purchasable`
                    - `price`
                    - `quantity`
                    - `total`
                    - `purchase_date`
        - Import data from the `customers.csv` and `purchase_history.csv` files
        - Uses the method for validating and sanitizing data to validate and format customer data before it’s imported
        - Ensure purchase records link to the corresponding customer based on the customer_email column in the CSV file and the `customer_id` column in the database.
3. **Fetch customers**
    - Build two views:
      1. List all customers in the database along with their latest purchase (if any).
      2. Lists all purchases for a single customer.
    - Both views should be sortable by date
    - Selecting a customer in the customers view should show the purchases view.
    - It's up to you how you want this to look.
4. **Calculate customer Loyalty Points**
    - Requires a new field to be added on the `customer` table
    - This should only be done _once_ initially and persisted.
    - Calculate loyalty points for each customer
        - For every $10 spent, award 1 loyalty point
        - For every 10 purchases, award an additional 10 loyalty points
        - Only purchases from **01 January 2022** onward are eligible for loyalty points
    - Update each customer’s `loyalty_points` field in the `customers` table based on this calculation.
5. **Add purchases**
    - Build a form that allows a user to submit a new purchase for a customer
    - They should be able to use the customer's ID to associate a purchase with a customer
    - It should accept all the fields in the `purchase_history` table
    - The customers loyalty points should be updated to include the new purchase
        - Refer back to the requirements for loyalty points calculations
6. **Generate a report**
    - Build a view which shows a customer report with
      - Average spend per month across _all_ customers
      - Total loyalty points awarded each month
    - The report does not need any special filtering capabilities
    - Must be sortable by
      - Date
      - Total loyalty points
      - Average spend
    - Can be exported to CSV
