# Rails Helpers

### Rails helpers move complexity and logic from view, making it easier to read

  For example:
  Instead of
  ```
  <% if @user && @user.email.present? %>
    <%= @user.email %>
  <% end %>
  ```

  We could make helper
  ```ruby
  module SiteHelper
    def user_email(user)
      user.email if user && user.email.present?
    end
  end
  ```

  Which would result in the following when retrieving the email in the view
  ```
  <%= user_email(@user) %>
  ```


  Helper methods are just modules, that are available to you view.
  #### Note: You sould try not to dump all helpers in the application controller

# Built-in Helpers

## URL helpers

Hard coded path: ```"/posts/#{@post.id}"```
Route helper: ```post_path(@post)]```

#### link_to Helper

posts_path refers to the action that we created in /config/routes
```
<%= link_to 'Back to Posts', posts_path %>
<!-- this generates the HTML... -->
<a href="/posts">Back to Posts</a>
```

If we made this helper ourselves

```ruby
module ApplicationHelper
  def my_link_to(text, href)
    "<a href='#{href}'>#{text}</a>".html_safe
  end
end
```

## date helpers

[date helper methods breakdown](https://github.com/rails/rails/blob/2c97fbf6503c9199f3fe5ed06222e7226dc6fcd9/actionview/lib/action_view/helpers/date_helper.rb#L440)

### some helpers list
  - date_select

      Returns a set of select tags (one for year, month, and day) pre-selected for accessing a specified date-based attribute (identified by method) on an object assigned to the template (identified by object).
      ```
      date_select("article", "written_on")
      ```

  - datetime_select

      Returns a set of select tags (one for year, month, day, hour, and minute) pre-selected for accessing a specified datetime-based attribute (identified by method) on an object assigned to the template (identified by object).
      ```
      datetime_select("article", "written_on")
      ```

  - distance_of_time_in_words
  - distance_of_time_in_words_to_now
      ```
      0 <-> 29 secs                                                             # => less than a minute
      30 secs <-> 1 min, 29 secs                                                # => 1 minute
      1 min, 30 secs <-> 44 mins, 29 secs                                       # => [2..44] minutes
      44 mins, 30 secs <-> 89 mins, 29 secs                                     # => about 1 hour
      89 mins, 30 secs <-> 23 hrs, 59 mins, 29 secs                             # => about [2..24] hours
      23 hrs, 59 mins, 30 secs <-> 41 hrs, 59 mins, 29 secs                     # => 1 day
      41 hrs, 59 mins, 30 secs  <-> 29 days, 23 hrs, 59 mins, 29 secs           # => [2..29] days
      29 days, 23 hrs, 59 mins, 30 secs <-> 44 days, 23 hrs, 59 mins, 29 secs   # => about 1 month
      44 days, 23 hrs, 59 mins, 30 secs <-> 59 days, 23 hrs, 59 mins, 29 secs   # => about 2 months
      59 days, 23 hrs, 59 mins, 30 secs <-> 1 yr minus 1 sec                    # => [2..12] months
      1 yr <-> 1 yr, 3 months                                                   # => about 1 year
      1 yr, 3 months <-> 1 yr, 9 months                                         # => over 1 year
      1 yr, 9 months <-> 2 yr minus 1 sec                                       # => almost 2 years
      2 yrs <-> max time or date                                                # => (same rules as 1 yr)
      ```


  - select_date
  - select_datetime
  - select_day
  - select_hour
  - select_minute
  - select_month
  - select_second
  - select_time
  - select_year

  - time_ago_in_words
  - time_select
  - time_tag


  ## form helpers

  Regular way of making form
  ```
  <form action="/somepath" method="post">
    <input type="text">
    <!-- other inputs here -->
    <input type="submit" value="Submit This Form">
  </form>
  ```

  Rails way using form_tag
  ```
  <%= form_tag("/search", method: "get") do %>
    <%= label_tag(:q, "Search for:") %>
    <%= text_field_tag(:q) %>
    <%= submit_tag("Search") %>
  <% end %>

  <!-- Creates the form -->
  <form accept-charset="UTF-8" action="/search" method="get">
    <label for="q">Search for:</label>
    <input id="q" name="q" type="text" />
    <input name="commit" type="submit" value="Search" />
  </form>
  ```

  Rails by default automatically protects you from cross-site request forgery and it requires you to verify that the form was actually submitted from a page you generated. In order to do so, it generates an “authenticity token” which looks like gibberish but helps Rails match the form with your session and the application.
  ```
  Parameters: {"utf8"=>"✓", "authenticity_token"=>"jJa87aK1OpXfjojryBk2Db6thv0K3bSZeYTuW8hF4Ns=", "user"=>{"first_name"=>"foo","last_name"=>"bar","email"=>"foo@bar.com"}, "commit"=>"Submit Form"}
  ```

  Helpers you can use inside your form
  ```
  <%= text_area_tag(:message, "Hi, nice site", size: "24x6") %>
  <textarea id="message" name="message" cols="24" rows="6">Hi, nice site</textarea>

  <%= password_field_tag(:password) %>
  <input id="password" name="password" type="password" />

  <%= hidden_field_tag(:parent_id, "5") %>
  <input id="parent_id" name="parent_id" type="hidden" value="5" />

  <%= search_field(:user, :name) %>
  <input id="user_name" name="user[name]" type="search" />

  <%= telephone_field(:user, :phone) %>
  <input id="user_phone" name="user[phone]" type="tel" />

  <%= date_field(:user, :born_on) %>
  <input id="user_born_on" name="user[born_on]" type="date" />

  <%= datetime_local_field(:user, :graduation_day) %>
  <input id="user_graduation_day" name="user[graduation_day]" type="datetime-local" />

  <%= month_field(:user, :birthday_month) %>
  <input id="user_birthday_month" name="user[birthday_month]" type="month" />

  <%= week_field(:user, :birthday_week) %>
  <input id="user_birthday_week" name="user[birthday_week]" type="week" />

  <%= url_field(:user, :homepage) %>
  <input id="user_homepage" name="user[homepage]" type="url" />

  <%= email_field(:user, :address) %>
  <input id="user_address" name="user[address]" type="email" />

  <%= color_field(:user, :favorite_color) %>
  <input id="user_favorite_color" name="user[favorite_color]" type="color" value="#000000" />

  <%= time_field(:task, :started_at) %>
  <input id="task_started_at" name="task[started_at]" type="time" />

  <%= number_field(:product, :price, in: 1.0..20.0, step: 0.5) %>
  <input id="product_price" max="20.0" min="1.0" name="product[price]" step="0.5" type="number" />

  <%= range_field(:product, :discount, in: 1..100) %>
  <input id="product_discount" max="100" min="1" name="product[discount]" type="range" />
  ```

  When using PATCH, PUT, DELETE
  ```
  form_tag(search_path, method: "patch")

  <!-- Will output -->
  <form accept-charset="UTF-8" action="/search" method="post">
    <input name="_method" type="hidden" value="patch" />
    <input name="utf8" type="hidden" value="&#x2713;" />
    <input name="authenticity_token" type="hidden" value="f755bb0ed134b76c432144748a6d4b7a7ddf2b71" />
    ...
  </form>
  ```

  ### NOTE: form_for can only be used on models.





