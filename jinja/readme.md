# Primer on Jinja Templating

Flask includes the powerful [Jinja](http://jinja.pocoo.org/docs/) templating language, right out of the box. It's modelled after Django templates (but it renders much faster), and, although, Flask does not force you to use any templating language, it assumes that you'll be using Jinga since it does come pre-installed.

For those who have not been exposted to a templating language before, such languagues essentially contain variables as well as some programming logic, which when evaluated (or rendered into HTML) are replaced with **actual** values. The variables and/or logic are placed between tags or delimeters. For example, Jinga templates use `{% ... %}` for expressions or logic (like for loops), while `{{ ... }}` are used for outputting the results to the template. The latter tag, when rendered, is replaced with a value or values, which are seen by the end user.

## Quick Examples

Make sure you have Jinja installed before running these examples - `pip install jinja2`

First:

```sh
>>> from jinja2 import Template
>>> t = Template("Hello {{ something }}!")
>>> t.render(something="World")
u'Hello World!'
>>>
>>> from jinja2 import Template
>>> t = Template("My favorite numbers: {% for n in range(1,10) %}{{n}} " "{% endfor %}")
>>> t.render()
u'My favorite numbers: 1 2 3 4 5 6 7 8 9 '
```

Notice how the actual output rendered to the user falls within the `{{ ... }}` tags.

## Flask Examples

1. Create the following product structure:
  ```sh
  ├── requirements.txt
  ├── run.py
  └── templates
  ```

2. Activate a virtualenv then install flask:
  ```sh
  $ pip install flask
  ```

3. Add the following code to *run.py*:
  ```python
  from flask import Flask, render_template
  app = Flask(__name__)


  @app.route("/")
  def template_test():
      return render_template('template.html', my_string="Wheeeee!", my_list=[0,1,2,3,4,5])


  if __name__ == '__main__':
      app.run(debug=True)
  ```

  Here we are establishing the route `/`, which renders the template `template.html`. We also are passing in two variables to the template, `my_string` and `my_list`.

4. Add the template:
  ```html
  <!DOCTYPE html>
  <html>
    <head>
      <title>Flask Template Example</title>
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <link href="http://netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap.min.css" rel="stylesheet" media="screen">
      <style type="text/css">
        .container {
          max-width: 300px;
          padding-top: 100px;
        }
      </style>
    </head>
    <body>
      <div class="container">
        <p>My string: {{my_string}}</p>
        <p>Value from the list: {{my_list[3]}}</p>
        <p>Loop through the list:</p>
        <ul>
          {% for n in my_list %}
          <li>{{n}}
          {% endfor %}
        </ul>
      </div>
      <script src="http://code.jquery.com/jquery-1.10.2.min.js"></script>
      <script src="http://netdna.bootstrapcdn.com/bootstrap/3.0.0/js/bootstrap.min.js"></script>
    </body>
  </html>
  ```

Save this as *template.html* in the templates directory. Notice the template tags. Can you guess the outpit before you run the app?

5. Run the app:
  ```sh
  $ python run.py
  ```

  You should see:

  ![flask-jinja](https://raw.github.com/mjhea0/thinkful-mentor/master/jinja/flask_example/flask-jinja.png)

## Inheritence

## Conclusion

That's it.
