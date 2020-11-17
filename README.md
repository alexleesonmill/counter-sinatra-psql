# Solved
This is a counter web app built in Ruby using Sinatra and Capybara. This app uses PostgreSQL to store the count.

### Can you add a "Decrement" button which decreases the count by 1 each time it is pressed?
In counter.rb
```
  def decrement
    read_count = count
    result = DatabaseConnection.query("UPDATE counter SET count = '#{read_count - 1}' WHERE id=1;")
  end
```
In app.rb
```  post '/decrement' do
    @counter.decrement
    redirect '/'
  end
```
In index.erb
```
    <form action="/decrement" method="post">
      <input type="submit" value="Decrement">
    </form>
```

### Can you update the app to display the time that the count was last updated? This value should be stored in the database so that it will be accurately displayed even if the server is restarted.
In counter.rb
```
  def time
    result = DatabaseConnection.query('SELECT * FROM counter WHERE id=1;')
    result[0]['lastmodified'].to_s
  end
 ```
In index.erb
```
    <div id="time">Counter last pressed at: <%= @counter.time %></div>
```

# Questions to explore
* What is the difference in behaviour between this app and one which there is [no database](https://github.com/tatsiana-makers/count-sinatra)?
* Which of the MVC components interacts with the database?
* What parts of the code run when we run the app in our browser? You could test your assumption by adding `p` lines and checking that you see the output you expect.
* What part of the code runs when we click the "Increment" button?

