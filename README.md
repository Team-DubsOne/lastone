# Vue.js and Node.js Web Application with MySQL Database

## Project Overview

This project is a complete web app with a frontend, backend, and database. It uses the Vue.js framework for the frontend, the Express.js framework for the backend on a Node.js app, and a MySQL database. You can start setting up this project from [this link](https://github.com/mohammadrony/emarket#project-setup).

### Project UI Overview

#### For Users without Logging In

This e-commerce system features three levels of **category system (category, sub-category, sub-sub-category)** and some products with different pieces of information in each category. You can also **search for products** with keywords and price ranges in a category. You can see other **customer reviews** for those products as well. Then, you can add as many **products to the cart and checkout**. To checkout with your product in your cart, you need to provide shipping information and some contact information. Then, you have to pay the bill with your card using the **Stripe checkout method**, and your order will be placed. A link will be sent to your email to monitor your order status with the contact information and the products you are buying. On the home screen, there is a promotion of products available for new and top selling products.

#### For Users Logging In

Including features from above. By logging in to the system or signing up, you can have a **wishlist to save products** in the database and find them later. You can also **add a review or rating to a product**. If you forget your password, you can reset it by **sending a verification code**. This web app also includes a **user profile**. You need to verify your email to create your account.

#### For Admin Users

Including features from above. As an admin, you have a custom way to **create or delete a product** from any category. You can also **create, edit, or delete a category**. You can also **delete any other customer's review** of a product. In the admin panel, you have a list of all registered users in your system, and you can **change their role** to give them admin access. You also have an **order list** with the user's contact information, shipping address, and product information.

### Programming Overview

#### Frontend Description

This project uses many good features of Vue.js(version 2). The web app features **state management with multiple modules** in the store directory. For the frontend, there's an authentication process with a **reset password** feature that includes email automation. By using **Stripe's payment method**, the web app can process different kinds of cards and currencies supported by Stripe. From the routing pages, you'll find detailed code about how to **restrict someone visiting a route** and show a default page for an **unauthenticated request or any wrong URL** entered. There are also other features, including real-time updates without reloading the page, and more.

#### Backend Description

**RESTful APIs** and authentication management are the two important parts of the backend. The **session middleware and JWT authentication** helped get data from the database securely. Most of the **email automation** is done in the backend. The payment session is generated, and **Sequelize ORM** can be used to work with different types of databases. This project worked with the MySQL database here. **Media files are saved** and public URLs generated. I hope you find this project useful. If you still have any questions, create an issue or ask me anyway.

### Topics included in the project

#### Frontend

- [Vue.js](https://vuejs.org/)
- [State management - Vuex](https://vuex.vuejs.org/)
- [Vue routing](https://vuejs.org/v2/guide/routing.html)
- [Component design - Bootstrap Vue](https://bootstrap-vue.org/)
- [Payment gateway - Stripe](https://stripe.com/)

#### Backend

- [Node.js](https://nodejs.org/en/)
- [Express.js](http://expressjs.com/)
- [RESTful API](https://en.wikipedia.org/wiki/Representational_state_transfer)
- [Authentication - Passport.js](http://www.passportjs.org/)
- [Mail automation - Nodemailer](https://nodemailer.com/about/)
- [Database interfacing - Sequelize](https://sequelize.org/)

#### Database

- [MySQL](https://www.mysql.com/)

#### Tutorials followed

- [YouTube - The Earth Is Square - Learn Vue 3 for Beginners](https://www.youtube.com/watch?v=ZqgiuPt5QZo)
- [YouTube - Program With Erik - BootstrapVue introduction](https://www.youtube.com/watch?v=-DyKeMa5tYY&list=PL-lxoPS_1OXWb4BlDuSsUrkq66hM5pG33)
- [YouTube - freeCodeCamp.org - Backend frontend combining](https://www.youtube.com/watch?v=Fa4cRMaTDUI&list=PLWKjhJtqVAbnadueQ-C5keMQQiQau_i0D)
- [YouTube - Stripe Developers - Stripe Checkout](https://www.youtube.com/watch?v=UjcSWxPNo18)
- [YouTube - Academind - Uploading an Image](https://www.youtube.com/watch?v=srPXMt1Q0nY)
- [YouTube - Esterling Accime - Send Email with Node.js](https://www.youtube.com/watch?v=Va9UKGs1bwI)

## Project Setup

### Cloning the repository

To clone this repository, use the following command:

```bash
git clone https://github.com/mohammadrony/emarket.git
```

### Installing server dependencies

To install server dependencies, from `server` directory use this following command:

```bash
cd server && npm install
```

### Installing shop dependencies

To install shop dependencies, from `shop` directory use this following command:

```bash
cd shop && npm install
```

### Configuring MySQL Server

To configure MySQL server, use the following command:

```bash
sudo apt install -y mysql-server
```

To setup root user password

```bash
sudo mysql
> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '12345678';
```

To properly configure the MySQL database server, you can refer to this [tutorial](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04). Using MySQL password as `12345678` will match the default configuration in `server/src/config/config.js` file.

To create a database called `mydb`, you can use the following command after logging into the MySQL shell as the root user:

```bash
mysql -u root -p
> CREATE DATABASE mydb;
> exit
```

### Setting Up Environment Variables

#### Stripe Payment Integration

To set up payment integration with Stripe, you need to follow these steps:

1. Rename the `.env.template` file in the `server` directory to `.env`.
2. Create a Stripe account (if you haven't already).
3. Find your Stripe secret key for the `server/.env` file on your [Stripe account dashboard](https://dashboard.stripe.com/test/apikeys).
4. Update the Stripe publishable key in `shop/src/components/Checkout/BuyItem.vue` with the publishable key from your Stripe account.

#### Email Automation Integration

To send emails from a Google account using a program, you need to follow these steps:

1. Enable [2-step verification](https://myaccount.google.com/signinoptions/two-step-verification) for your account.
2. Generate an [app password](https://myaccount.google.com/apppasswords) (a 16-digit password) for your account.
3. Use this app password in the `.env` file located in the `server` directory as follows:

```env
EMARKET_EMAIL=<your_email>
EMARKET_PASSWORD=<your_app_password>
```

For more detailed information on generating app passwords, you can refer to this [Stack Overflow answer](https://stackoverflow.com/questions/45478293/username-and-password-not-accepted-when-using-nodemailer) and the [steps to generate app passwords](https://www.getmailbird.com/gmail-app-password/) in a Google account.

If you don't want to use a Gmail account to send emails, you can configure the transporter for sending email in the controller files located in `server/src/controllers/*`.

Here is what the `.env` file should look like in the `server` directory.

```env
EMARKET_EMAIL=<your_email>
EMARKET_PASSWORD=<your_app_password>
STRIPE_SECRET_KEY=<your_stripe_secret_key>
```

### BootstrapVue Package Recommendation

To ensure that BootstrapVue runs smoothly and without any component issues, it is recommended to use the `vue@2.6.12` and `bootstrap@4.6.1` versions of the packages mentioned by [BootstrapVue](https://bootstrap-vue.org/docs).

### Check Database Configuration for the application

Please make sure to check and match the database configuration for user, password, and database information. You can find this configuration file at `server/src/config/config.js`.

### Feed Some Data to the Database for the Website

To add some initial data to the database for the website, run the following command:

```bash
cd server && npm run seed
```

### Starting the Backend Server First

Start the backend server first with the following command:

```bash
cd server && npm start
```

### Starting the Vue Application in Another Terminal

To start the Vue application in another terminal window, run the following command:

```bash
cd shop && npm run serve
```

### Verify Your Application is Running

Your application should be running locally on port 8080. Verify this by going to <http://localhost:8080> in your web browser.

Thank you.
