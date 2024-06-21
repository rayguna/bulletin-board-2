# bulletin-board-2

Target: https://bulletin-board-2.matchthetarget.com/

Lesson: https://learn.firstdraft.com/lessons/137

Video: https://share.descript.com/view/qpQZz1iDN8a

Grading: https://grades.firstdraft.com/resources/7d036602-19b3-406d-a496-62cdd9c9db80

<hr>

Notes:

1. (1:23) Start the server with bin/dev. - website loads correctly
2. (2 min) Load data with `rails sample_data`. 
3. Use cookies to sign in and sign out.
4. Use a gem called devise for a boilerplate for sign up, sign out, edit profile, cancel account, password reset email, etc. The gem has been added to the project.
5. Setup devise:
- Install the gem with `rails generate devise:install`.
- Follow instructions in the terminal.
- (5 min) Navigate into config/environments/development.rb and insert the following script:
```
config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }
```
- Go ro config/environments/routes.db and add: ` root to: "home#index"` and, subsequently, comment out the get("/", ...) statement.
- Ensure you have flash messages in app/views/layouts/application.html.erb.
     For example:
       <p class="notice"><%= notice %></p>
       <p class="alert"><%= alert %></p>

This was done previously.

6. (7 min) Go to config/initializers/devise.rb. Go to line 269 and modify :delete to :get

```
 # The default HTTP method used to sign out a resource. Default is :delete.
  config.sign_out_via = :get #:delete
```

7. (8 min) Generate users table by typing into the terminal: `rails g devise user`. 
8. Create database tables with `rake db:migrate`.

(9 min) When you fo to routes.bd, you will find that the file has been modified. It contains the line that says devise for :users.

```
Rails.application.routes.draw do
  devise_for :users
  #for devise gem
  root to: "home#index"
```
(10 min) 
