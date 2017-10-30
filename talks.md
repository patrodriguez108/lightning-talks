# Rails Helpers

## link_to Helper

posts_path refers to the action that we created in /config/routes
```
<%= link_to 'Back to Posts', posts_path %>
<!-- this generates the HTML... -->
<a href="/posts">Back to Posts</a>
```

If we made this helper ourselves

```
module ApplicationHelper
  def my_link_to(text, href)
    "<a href='#{href}'>#{text}</a>".html_safe
  end
end
```

## date helpers

[date helper methods breakdown](https://github.com/rails/rails/blob/2c97fbf6503c9199f3fe5ed06222e7226dc6fcd9/actionview/lib/action_view/helpers/date_helper.rb#L440)

#### some helpers list
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
