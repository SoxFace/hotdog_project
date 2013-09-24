# The HotDog vendor

1. In you 'apps' directory, create a new Rails app with the following command:

`rails new hotdog`


2. You can create a home page for your site with the following command

`rails g controller home index`


This command just generates a *home_controller.rb* and *home/index.html.erb* file. Just like we created without a generator script in the beginning.
As it does not create a model (no data model required) we do not need to do a rake db:migrate yet.

3. Go to *config/routes.rb* and find the line that was created by the generator and delete it:

`get "home/index"`


4. Then find the commented out root line and change it like so:

```
  # You can have the root of your site routed with "root"
  # root 'welcome#index'
```

```
  # You can have the root of your site routed with "root"
  root 'home#index'
```

5. Open a new tab from your command line (Command + T) and start your Rails server.

`rails s`


6. Go to your browser and open localhost:3000 to check that you see the Home index page you just created. We will leave it like this for the moment.

>> screenshot_1

7. Now add the functionality that enables the hotdog vendor to add and list his locations. Go back to your command line:

```
rails g scaffold Location name address suburb date:date start_time:time finish_time:time
```

8. Check the migration file that was just created to make sure everything looks right. *db/migrate/2013xxxxx_create_locations.rb*

>> screenshot_2


9. Run your migration

`rake db:migrate`


10. Go to your browser and check that you see the location index page localhost:3000/locations

>> screenshot_3


11. Add a location with test data (make up a location)

>> screenshot_4


12. Let's show the locations on the home page. Go to *app/controllers/home_controller.rb* and find the index method. Bring in the location data by adding the following line:

```
  def index
  	@locations = Location.all
  end
```


13. Now go to *app/views/home/index.html.erb*, delete the code that is already there and create a table that lists the added locations.

```
<h1>HotDog King</h1>

<h2>Locations</h2>

<table>
	<tr>
		<th>Location</th>
		<th>Where</th>
		<th>When</th>
	</tr>

<% @locations.each do |location| %>
	<tr>
		<td><%= location.name %></td>
		<td><%= location.address %>, <%= location.suburb %></td>
		<td><%= location.date.to_date %><br>
			<%= location.start_time.strftime("%H:%M") %> - <%= location.finish_time.strftime("%H:%M") %></td>
	</tr>
<% end %>
```

14. Check your home page and see that your table shows your locations.

## Bonus challenges

15. Add bootstrap to add some style to your page.

16. Try setting a default_scope in the locations model so that the locations show in chronological order: http://guides.rubyonrails.org/active_record_querying.html#applying-a-default-scope

` default_scope order: 'locations.date ASC' `

17. Add an image to the home page

18. Put an "Add location" link/button on the home page





