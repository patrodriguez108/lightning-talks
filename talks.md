# link_to Helper

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
