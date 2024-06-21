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
  #root to: "home#index"
  root "boards#index"
```
Use boards#index rather than home#index. Otherwise, you will receive an error. 

9. (10 min) Navigate to `.../rails/info` to see all routes that have been created.
10. You could also navigate to `/users/sign_up` to view the login page.
11. Try to sign up with alice@example.com/pass****. It will let you login.
12. (11 min) By setting up the devise gem, you get some free routes. We will mainly focus on:

```
GET/users/sign_up
GET/users/sign_in
GET/users/sign_out
GET/users/edit
```

13. Let's incorporate those into the navbar within the views/application.html.erb.

14. (16 min) type in the terminal `rails generate migration AddUserIdToBoards user_id:integer`. Here is the output:

```
bulletin-board-2 main % rails generate migration AddUserIdToBoards user_id:integer
      invoke  active_record
      create    db/migrate/20240621200921_add_user_id_to_boards.rb
```

Then, type in the terminal `rake db:migrate`.

bulletin-board-2 main % rake db:migrate
== 20240621200921 AddUserIdToBoards: migrating ================================
-- add_column(:boards, :user_id, :integer)
   -> 0.0015s
== 20240621200921 AddUserIdToBoards: migrated (0.0015s) =======================

Annotated (1): app/models/board.rb

15. Next, type in the terminal: `rails g migration AddUserIdToPosts user_id:integer`. Here is the output:

Then, type in the terminal: `rake db:migrate`.

16. Visit: https://effective-tribble-w9rpxpqg4g7cv5x5-3000.app.github.dev/rails/db/tables/users/data. The users table exists with one user, alice@example.com.

17. (18 min) Visit: https://effective-tribble-w9rpxpqg4g7cv5x5-3000.app.github.dev/rails/db/tables/posts.
A user_id column must exist.

18. In this case, it didn't exist because I previously made a mistake in typing the command. I just typed: `rails g migration AddUserIdToPosts`

Re-do, but add the keyword --force:

```
bulletin-board-2 main % rails g migration AddUserIdToPosts user_id:integer --force
      invoke  active_record
      remove    db/migrate/20240621201112_add_user_id_to_posts.rb
      create    db/migrate/20240621202359_add_user_id_to_posts.rb
bulletin-board-2 main % rake db:migrate
== 20240621202359 AddUserIdToPosts: migrating =================================
-- add_column(:posts, :user_id, :integer)
   -> 0.0015s
== 20240621202359 AddUserIdToPosts: migrated (0.0016s) ========================
```

Problem is fixed.
