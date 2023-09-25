##### MAY 29, 2023

# From Obsidian to Webpage

###### For the uninitiated [Obsidian](https://obsidian.md/) is a powerful application that allows you to takes notes that save as markdown files. When taking notes in it for my own projects I often find that I would want an easy way to share them.  In this article we will look at how to use [Flask](https://flask.palletsprojects.com/en/2.3.x/) to create an application that automatically converts your obsidian md files to webpages.

<!-- ![alt](https://raw.githubusercontent.com/EvanCoppa/guthub-stats/master/generated/overview.svg#gh-dark-mode-only) -->

### 1. Set up a Flask project:

- Install Flask using  `pip install flask`

- Install Markdown using `pip install markdown`

- Create a new directory for your project and navigate to it

- Create a new Python file, e.g., `app.py`, to define your Flask application
 

### 2.  Import the necessary Flask modules:

```python
from flask import Flask, render_template, url_for 
import markdown 
import os 
```

 

 

### 3. Create an instance of the Flask application:
    
     
```python
app = Flask(__name__)
```    
### 4.  Define a route that will handle the conversion of Markdown files:
    
     
```python
@app.route('/<path:filename>') 
def markdown_to_html(filename):    
    md_file = os.path.join('path/to/markdown/files', filename + '.md')     
        if not os.path.exists(md_file):         
            return 'File not found', 404      
        with open(md_file, 'r') as file:        
            markdown_text = file.read()         
            html_content = markdown.markdown(markdown_text)      
        
        return render_template('page.html', content=html_content)
```



### 5. Create a template file `page.html` to display the converted HTML content:
    
```
- app.py
- templates/
  - page.html
```

 Here is the content for Page.html. In Flask's template engine, the expression `{{content|safe}}` is used to output a variable called content in the HTML template while marking it as "safe" from escaping

     
```markup 
<html> 
    <head>     
        <title>Markdown to HTML</title> 
    </head> 
    <body>     
        {{ content|safe }} 
    </body> 
</html>
```

 


### 6. Run the Flask application:
    
```python
`if __name__ == '__main__':   
    app.run(debug=True)`
```
    
### 7. Start the Flask development server by executing `python app.py`.
    

Now, when you access `http://localhost:5000/filename` in your web browser, Flask will look for the corresponding Markdown file in the specified directory, convert it to HTML using the `markdown` library, and render it in the `page.html` template.  

<br />


Make sure to replace `'path/to/markdown/files'` with the actual path to your folder containing the Markdown files. Additionally, you can enhance this example by adding error handling, navigation, and other features based on your requirements.



